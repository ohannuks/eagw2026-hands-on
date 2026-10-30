---
title: Git prep
description: uv setup and official PE / skymap / ZTF data download for EAGW2026 Hands-on
permalink: /git-prep/
---

## Do we need a Git prep page?

**Yes.** The boot camp uses one shared repository (one directory per team), a common **`uv`** environment, and official public PE samples, sky maps, and ZTF light curves. Students should arrive with the environment installed, data fetched (or the fetch script verified), and a smoke-test notebook already run, so Day 1 can start on science. Target completion: **13 November 2026**.

## 0. What you need

| Requirement | Notes |
|---|---|
| Laptop | macOS, Linux, or Windows (**WSL2** strongly preferred on Windows) |
| Disk space | ~5–10 GB free for the `uv` env + selected events; much more if you pull full Zenodo PE releases |
| Accounts | [GitHub](https://github.com/) (for the repo). IRSA/ZTF queries need no login for the basic light-curve API |
| Background | Python + `numpy` / `scipy` / `matplotlib` / Jupyter basics |

No HPC access is required. An offline USB copy will also be available on site (by 18 Nov).

## 1. Install Git and uv

```bash
git --version
```

Install **uv** (Python package/environment manager — we use it for *everything*):

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# or: https://docs.astral.sh/uv/getting-started/installation/
uv --version
```

Optional Git LFS (only if we later store slim derivatives in-repo):

```bash
git lfs install --skip-smudge
```

## 2. Clone the school repository

```bash
git clone https://github.com/ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
```

SSH:

```bash
git clone git@github.com:ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
```

### Optional: personal fork

```bash
# after forking on GitHub and cloning your fork:
git remote add upstream https://github.com/ohannuks/eagw2026-hands-on.git
git fetch upstream
git merge upstream/main
```

## 3. Create the environment with uv

From the repo root:

```bash
uv sync
```

This creates `.venv/`, installs every dependency pinned in `uv.lock` / declared in `pyproject.toml` (numpy, scipy, matplotlib, jupyter, astropy, gwosc, gwpy, ligo.skymap, pesummary, precession, zenodo-get, ztfquery, …).

Update later:

```bash
uv sync --upgrade
```

Run any tool **through uv** (do not activate conda):

```bash
uv run python -c "import numpy, astropy, gwosc; print('ok')"
uv run jupyter lab
# or
uv run jupyter notebook
```

## 4. Official data: PE samples, sky maps, ZTF flares

Organizers will also ship **slim** subsets under `data/` before 13 Nov. You should still know how to pull the **official** public releases yourself.

Helper script (all commands via `uv run`):

```bash
uv run python scripts/fetch_data.py --help
uv run python scripts/fetch_data.py all --events GW190521 GW231123
```

Outputs go to:

| Path | Contents |
|---|---|
| `data/pe/` | Official PE HDF5 releases |
| `data/skymaps/` | Official PE sky-map FITS (and optional Zenodo tarballs) |
| `data/ztf/` | ZTF light curves (IRSA CSV) for ZTF19abanrhr |

### 4a. Parameter estimation samples (official)

**Preferred (per event): GWOSC Event API → HDF5 link**

```bash
uv run python scripts/fetch_data.py pe --events GW190521 GW231123
```

What this does:

1. Resolves the event on the [GWOSC Event API](https://gwosc.org/eventapi/html/) (GWTC catalogs).
2. Downloads the official PE data-release HDF5 linked from that event page.

Manual alternative — open the event on GWOSC and download the PE file from the event page, e.g.:

- Portal: [https://gwosc.org/eventapi/html/](https://gwosc.org/eventapi/html/)
- Catalog docs: [GWTC-5.0](https://gwosc.org/GWTC-5.0/) (O4b / GW231123 and other GWTC-5 events)
- GW190521 lives in earlier catalogs (GWTC-2.1 / GWTC-3); the script walks catalogs until it finds the event.

**Bulk (large): Zenodo GWTC-5.0 PE data release**

PE samples for GWTC-5.0 are split across two Zenodo records ([part 1](https://zenodo.org/records/20348005), [part 2](https://zenodo.org/records/20348006)):

```bash
# WARNING: full records are huge (many × 100 MB–GB HDF5 files). Prefer per-event downloads.
uv run python scripts/fetch_data.py zenodo-pe
# equivalent:
uv run zenodo_get 20348005 -o data/pe/zenodo_20348005
uv run zenodo_get 20348006 -o data/pe/zenodo_20348006
```

To pull **one** named file from Zenodo without the whole record, use the record file URL from the Zenodo page, or:

```bash
uv run zenodo_get 20348005 -g '*GW231123*' -o data/pe/zenodo_20348005
```

Read PE HDF5 with `pesummary` / `h5py`:

```bash
uv run python - <<'PY'
from pesummary.io import read
f = read("data/pe/GW190521_PEDataRelease.hdf5")
print(f.labels)          # available analyses / waveform mixes
print(list(f.samples_dict.keys())[:10])
PY
```

### 4b. Sky maps (official)

**Preferred (per event): GWOSC → FITS skymap**

```bash
uv run python scripts/fetch_data.py skymaps --events GW190521 GW231123
```

Use with `ligo.skymap`:

```bash
uv run python - <<'PY'
from ligo.skymap.io import read_sky_map
m, meta = read_sky_map("data/skymaps/GW190521_skymap.fits", nest=True)
print(meta)
PY
```

**Bulk archived skymaps (Zenodo)**

```bash
# GWTC-5.0 archived PE skymaps
uv run python scripts/fetch_data.py skymaps --events GW231123 --bulk gwtc5

# GWTC-2.1 archived PE skymaps (covers GW190521)
uv run python scripts/fetch_data.py skymaps --events GW190521 --bulk gwtc2.1
```

Direct tarball references used by the script:

| Catalog | Zenodo | Tarball |
|---|---|---|
| GWTC-5.0 | [20276105](https://zenodo.org/records/20276105) | `IGWN-GWTC5p0-29ebe06b7_25-Archived_Skymaps.tar.gz` |
| GWTC-2.1 | [6513631](https://zenodo.org/records/6513631) | `IGWN-GWTC2p1-v2-PESkyMaps.tar.gz` |

### 4c. ZTF flare data (official IRSA)

Primary test case: **ZTF19abanrhr** associated with AGN **J124942.3+344929** (Graham et al. 2020; candidate counterpart to GW190521).

**IRSA ZTF Light Curve API** (no account required for this query):

```bash
uv run python scripts/fetch_data.py ztf --object ZTF19abanrhr
```

This queries:

`https://irsa.ipac.caltech.edu/cgi-bin/ZTF/nph_light_curves`  

with `POS=CIRCLE <RA> <Dec> <radius>` at the AGN position (default RA = 192.426223°, Dec = +34.824839°, radius ≈ 7″) and writes `data/ztf/ZTF19abanrhr_irsa.csv`.

API docs: [IRSA ZTF light-curve interface](https://irsa.ipac.caltech.edu/docs/program_interface/ztf_lightcurve_api.html).

Optional broker page (metadata / public transient view): [Lasair · ZTF19abanrhr](https://lasair-ztf.lsst.ac.uk/objects/ZTF19abanrhr/).

Optional same pull via `ztfquery` (still IRSA under the hood):

```bash
uv run python scripts/fetch_data.py ztf --object ZTF19abanrhr --ztfquery
```

Quick look:

```bash
uv run python - <<'PY'
import pandas as pd
df = pd.read_csv("data/ztf/ZTF19abanrhr_irsa.csv", comment="#")
print(df.columns.tolist()[:20])
print(df.head())
PY
```

Control-sample AGN light curves for Q2 will be prepared by organizers (same IRSA API, many positions); do not scrape thousands of objects until that list is published.

## 5. Run the smoke test

```bash
uv run jupyter notebook notebooks/smoke_test.ipynb
# or: uv run jupyter lab
```

You should import the core stack and produce a trivial plot. Team starters will live under `notebooks/q1` … `notebooks/q5` and must run end-to-end by **13 November**.

## 6. Git habits during the boot camp

- Work in your team paths: `notebooks/qN/`, `results/qN/`.
- Commit often; push to your fork or team branch at checkpoints.
- Do **not** commit multi‑GB raw PE releases, full skymap tarballs, or large ZTF dumps — only slim derivatives and figures (`data/raw` style trees are gitignored).
- Prefer one notebook (or small module) that regenerates the representative figure.

```bash
git checkout -b team-qN
git add notebooks/qN results/qN
git commit -m "Q N: science question + first sketch of figure"
git push -u origin team-qN
```

## 7. Troubleshooting

| Symptom | Try |
|---|---|
| `uv` not found | Re-open the shell after install, or add `~/.local/bin` to `PATH` |
| GWOSC timeout | Retry; or download the HDF5/FITS from the event page in a browser; or use Zenodo bulk for that catalog |
| Zenodo too large | Download **one event file** only (`zenodo_get -g '*EVENT*'`), not the whole record |
| `ligo.skymap` / HEALPix issues on Windows | Use WSL2 |
| Empty IRSA CSV | Widen `--radius-deg` slightly; check RA/Dec; confirm IRSA is reachable |
| Offline at the venue | Use the USB / local-server copy prepared by 18 Nov |

<div class="note warn">
<strong>Deadline:</strong> <code>uv sync</code> + smoke test + at least one successful PE/skymap/ZTF fetch (or confirmed offline copy) by <strong>13 November</strong>. Email the Hands-on leads before travel if anything fails.
</div>

## Related links

- [Sessions & plans]({{ '/sessions/' | relative_url }})
- [Projects Q1–Q5]({{ '/projects/' | relative_url }})
- GWOSC: [Event portal](https://gwosc.org/eventapi/html/) · [GWTC-5.0 docs](https://gwosc.org/GWTC-5.0/)
- Zenodo PE: [GWTC-5.0 part 1](https://zenodo.org/records/20348005) · [part 2](https://zenodo.org/records/20348006)
- ZTF: [IRSA light-curve API](https://irsa.ipac.caltech.edu/docs/program_interface/ztf_lightcurve_api.html) · [Lasair ZTF19abanrhr](https://lasair-ztf.lsst.ac.uk/objects/ZTF19abanrhr/)
