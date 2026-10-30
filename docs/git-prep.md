---
title: Git prep
description: Software and git setup before the EAGW2026 Hands-on Boot Camp
permalink: /git-prep/
---

## Do we need a Git prep page?

**Yes.** The boot camp uses one shared repository (one directory per team), a common conda environment, and organizer-prepared slim data. Students should arrive with the environment installed and a test notebook already run, so Day 1 can start on science rather than debugging installs. Target completion: **13 November 2026**.

This page is the draft checklist. Paths and package pins will be finalized when the shared environment file is published (target **6 November**).

## 0. What you need

| Requirement | Notes |
|---|---|
| Laptop | macOS, Linux, or Windows (WSL2 strongly preferred on Windows) |
| Disk space | ~5–8 GB free (conda env + slim data; more if you pull optional catalogs) |
| Accounts | [GitHub](https://github.com/) account (and GitLab/`git.ligo.org` only if we host data there) |
| Background | Python + `numpy` / `scipy` / `matplotlib` / Jupyter basics |

No HPC access is required. Google Colab / a JupyterHub mirror will be offered as fallback.

## 1. Install Git (and Git LFS)

```bash
git --version
```

If missing: install via [git-scm.com](https://git-scm.com/) or your package manager.

Large data may use Git LFS (same pattern as the 2025 Hands-on school):

```bash
# install from https://git-lfs.com then:
git lfs install --skip-smudge
```

`--skip-smudge` avoids auto-downloading every LFS file on clone; pull only what your team needs.

## 2. Install conda / mamba

We recommend [Miniforge](https://github.com/conda-forge/miniforge) (conda-forge by default):

```bash
conda --version
# or
mamba --version
```

## 3. Clone the school repository

Once the shared repo URL is published (this draft site’s companion repo):

```bash
git clone https://github.com/ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
```

SSH alternative (if your GitHub SSH key is set up):

```bash
git clone git@github.com:ohannuks/eagw2026-hands-on.git
```

### Optional: work on a personal fork

1. Fork the repository on GitHub.
2. Clone **your fork**.
3. Add the upstream remote so you can pull organizer updates:

```bash
git remote add upstream https://github.com/ohannuks/eagw2026-hands-on.git
git fetch upstream
git merge upstream/main   # or: git rebase upstream/main
```

## 4. Create the common environment

```bash
conda env create -f environment.yml
conda activate eagw2026-hands-on
```

Expected core stack (exact pins TBD in `environment.yml`):

- Python 3.11+
- `numpy`, `scipy`, `matplotlib`, `jupyter`, `astropy` (Planck18 cosmology)
- `ligo.skymap` (Q1 cross-match)
- `precession` (Q3 remnant kicks)
- `pAGN` (common AGN disk grid; Gangardt et al. 2024)
- team-specific helpers as needed (ZTF light-curve I/O for Q2, etc.)

Update later without rebuilding from scratch:

```bash
conda env update -f environment.yml --prune
```

## 5. Pull slim data (when published)

Organizers will publish pre-slimmed GW sky maps, posterior columns, AGN catalog subset, and ZTF light curves **before 13 November**. Typical pattern:

```bash
# if data are in Git LFS:
git lfs pull -I data/common/**
git lfs pull -I data/q1/**    # only your team’s extras

# or via the helper script (to be finalized):
bash scripts/fetch_data.sh
```

An **offline USB / local-server copy** will also be available at Ewha (prepared by 18 November).

## 6. Run the smoke test

```bash
conda activate eagw2026-hands-on
jupyter notebook notebooks/smoke_test.ipynb
# or: jupyter lab
```

You should be able to import the core packages and produce a trivial plot. Team starter notebooks live under `notebooks/q1` … `notebooks/q5` and must run end-to-end on a clean machine by **13 November** (organizer gate).

## 7. Git habits during the boot camp

- Work in your team directory: `teams/qN/` (or `notebooks/qN/` + `results/qN/`).
- Commit often with short messages; push to your fork or team branch at checkpoints.
- Do **not** commit multi‑GB raw catalogs or full PE sample sets — only slim derivatives and figures.
- Prefer one notebook (or small module set) that regenerates the **representative figure**.

Suggested first-day commits after team pairing:

```bash
git checkout -b team-qN
# edit notebooks / scripts
git add notebooks/qN results/qN
git commit -m "Q N: science question + first sketch of figure"
git push -u origin team-qN
```

## 8. Troubleshooting

| Symptom | Try |
|---|---|
| `conda` conflicts / long solves | Use `mamba`; or create env from the frozen `environment.lock.yml` once published |
| Windows path / compile errors | Use WSL2 Ubuntu; avoid native Windows Python for `ligo.skymap` |
| Cannot download GWOSC / catalog files | Use the on-site offline copy; ask a tutor |
| Git LFS quota / slow pulls | Pull only your team’s paths with `-I`; share USB data |

<div class="note warn">
<strong>Deadline reminder:</strong> environment installed + smoke test run by <strong>13 November</strong>. If anything fails, email the Hands-on leads before you travel so we can fix it remotely.
</div>

## Related links

- [Sessions & plans]({{ '/sessions/' | relative_url }}) — timetable and deliverables
- [Projects Q1–Q5]({{ '/projects/' | relative_url }}) — science questions and materials
- 2025 precedent: [souvik-jana/hands-on-school-2025](https://github.com/souvik-jana/hands-on-school-2025) (clone + `env_setup.sh` + Git LFS pattern)
