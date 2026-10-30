# EAGW2026 Hands-on Boot Camp

**Binary Black Holes in AGN — GW, EM, Lensing, and Dark Matter**  
19–21 November 2026 · Ewha Womans University, Seoul  
Satellite to [EAGW2026](https://sites.google.com/view/eagw2026/home) (Yonsei, 23–25 November)

## Website

https://ohannuks.github.io/eagw2026-hands-on/

| Page | Purpose |
|---|---|
| [Home](docs/index.md) | Hands-on homepage |
| [Git prep](docs/git-prep.md) | **`uv` setup** + official PE / skymap / ZTF download instructions |
| [Sessions & plans](docs/sessions.md) | Timetable and work distribution |
| [Projects Q1–Q5](docs/projects.md) | Science questions, materials, fallbacks |

## Quick start (students) — all via `uv`

```bash
# install uv: https://docs.astral.sh/uv/getting-started/installation/
git clone https://github.com/ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
uv sync

# official PE samples + sky maps + ZTF19abanrhr light curve
uv run python scripts/fetch_data.py all --events GW190521 GW231123

uv run jupyter notebook notebooks/smoke_test.ipynb
```

Full detail: **[Git prep](https://ohannuks.github.io/eagw2026-hands-on/git-prep/)**.

## Repository layout

```
docs/               # GitHub Pages site
scripts/fetch_data.py
pyproject.toml      # uv project / dependencies
notebooks/q1–q5     # Starter notebooks (to be filled)
data/               # Downloaded PE, skymaps, ZTF (gitignored raw)
materials/          # Templates, reading lists
```

## Contacts

Hands-on content: Otto Hannuksela, Paul Martens, Surojit Saha, Albert Kong  
LOC: Chunglee Kim, Jun Gyu Park · chunglee.kim AT ewha.ac.kr
