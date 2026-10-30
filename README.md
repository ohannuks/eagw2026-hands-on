# EAGW2026 Hands-on Boot Camp

**Binary Black Holes in AGN — GW, EM, Lensing, and Dark Matter**  
19–21 November 2026 · Ewha Womans University, Seoul  
Satellite to [EAGW2026](https://sites.google.com/view/eagw2026/home) (Yonsei, 23–25 November)

This repository hosts:

1. The **draft Hands-on website** (GitHub Pages under `docs/`)
2. Shared **environment / notebook scaffolding** for the five project teams
3. (Later) slim data pointers and starter notebooks

## Website (draft for SOC, 30 Oct 2026)

Once Pages is enabled: `https://ohannuks.github.io/eagw2026-hands-on/`

| Page | Purpose |
|---|---|
| [Home](docs/index.md) | Hands-on homepage sketch |
| [Git prep](docs/git-prep.md) | Student software + git setup before 13 Nov |
| [Sessions & plans](docs/sessions.md) | Timetable + work distribution summary from meeting notes |
| [Projects Q1–Q5](docs/projects.md) | Science questions, materials, fallbacks |

## Quick start (students)

See **[Git prep](https://ohannuks.github.io/eagw2026-hands-on/git-prep/)** (or `docs/git-prep.md`). Short version:

```bash
git clone https://github.com/ohannuks/eagw2026-hands-on.git
cd eagw2026-hands-on
conda env create -f environment.yml
conda activate eagw2026-hands-on
jupyter notebook notebooks/smoke_test.ipynb
```

## Repository layout

```
docs/           # GitHub Pages site
notebooks/q1–q5 # Starter notebooks (to be filled)
materials/      # Templates, reading lists
environment.yml # Common conda environment
```

## Contacts

Hands-on content: Otto Hannuksela, Paul Martens, Surojit Saha, Albert Kong  
LOC: Chunglee Kim, Jun Gyu Park · chunglee.kim AT ewha.ac.kr
