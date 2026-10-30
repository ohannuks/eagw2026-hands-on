# EAGW2026 Hands-on School

**Cross-correlating ZTF flares with gravitational waves to study AGN channels**  
19–21 November 2026 · Ewha Womans University, Seoul  
Satellite to [EAGW2026](https://sites.google.com/view/eagw2026/home) (Yonsei, 23–25 November)

## Website

https://ohannuks.github.io/eagw2026-hands-on/

| Page | Purpose |
|---|---|
| [Home](docs/index.md) | Hands-on homepage |
| [Git prep](docs/git-prep.md) | **`uv` setup** + official PE / skymap / ZTF download instructions |
| [Sessions & plans](docs/sessions.md) | Timetable and deliverables |
| [Plotting exercises](docs/exercises.md) | Fetch GW + ZTF data and make example plots |

## Quick start (students) — all via `uv`

```bash
# install uv: https://docs.astral.sh/uv/getting-started/installation/
git clone https://github.com/ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
uv sync

# official PE samples + sky maps + ZTF19abanrhr light curve
uv run python scripts/fetch_data.py all --events GW190521

uv run jupyter notebook notebooks/first_light.ipynb
uv run jupyter notebook notebooks/exercises/
```

Full detail: **[Git prep](https://ohannuks.github.io/eagw2026-hands-on/git-prep/)** · **[Plotting exercises](https://ohannuks.github.io/eagw2026-hands-on/exercises/)**.

## Repository layout

```
docs/               # GitHub Pages site
scripts/fetch_data.py
pyproject.toml      # uv project / dependencies
notebooks/exercises # Fetch + plot GW / ZTF examples
data/               # Downloaded PE, skymaps, ZTF (gitignored raw)
materials/          # Templates, reading lists
```

## Contacts

Otto Hannuksela, Chunglee Kim, Keiko Kokeyama, Albert Kong, Paul Martens, Jun Gyu Park, Surojit Saha · chunglee.kim AT ewha.ac.kr
