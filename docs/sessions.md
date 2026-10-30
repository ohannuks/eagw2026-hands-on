---
title: Sessions & plans
description: Organized summary of Hands-on session topics and plans from SOC meetings
permalink: /sessions/
---

## Source of this summary

Compiled for the **30 October 2026** SOC catch-up from:

- Chunglee’s Hands-on planning doc (*BBHs in AGN* boot-camp plan)
- Hands-on timetable sheet (final version after the **23 Oct** meeting with Shigeo)
- Full Hands-on & Workshop programme sheet
- Email updates (24–26 Oct): 10 students / 5 teams; Thursday dinner; pairing senior+junior

Timetable link (Hands-on only): [Google Sheet](https://docs.google.com/spreadsheets/d/12JaxNLvRpcNQ_qIGdwnMcD049bSnEth6SEVL4D1qmEQ/edit?gid=0#gid=0) · Full programme: [Sheet](https://docs.google.com/spreadsheets/d/1Dlgk_mWkpP3toVem5OQdpyeOSyoFWCkDW82tiIAxzkc/edit?gid=577262258#gid=577262258)

## At a glance

| Day | Date | Mode | Outcome by end of day |
|---|---|---|---|
| 0 | Wed 18 Nov | Optional / colloquium | Otto colloquium at Ewha (17:00) |
| 1 | Thu 19 Nov | Lectures + pairing | Science question, minimum deliverable, data/calc plan, proposed figure |
| 2 | Fri 20 Nov | Full hands-on | First scientifically interpretable version of the representative figure (else switch to fallback) |
| 3 | Sat 21 Nov | Finish + poster | Frozen result → draft poster → practice talk → final PDF to Chunglee by 20:00 |
| — | Mon–Tue 23–24 Nov | Workshop | Posters printed/mounted; 5‑min sparklers Tue morning |

## Day-by-day timetable (Hands-on)

### Wednesday 18 November (arrival / optional)

| Time | Session |
|---|---|
| 17:00–18:00 | Otto’s colloquium at Ewha |

### Thursday 19 November — background + kickoff

| Time | Session | Lead / notes |
|---|---|---|
| 09:30–10:00 | Welcome & ice-breakers | LOC |
| 10:00–11:00 | **Lecture 1** — BBHs in AGN | Shigeo Kimura |
| 12:00–13:30 | Lunch | Campus cafeteria together (self-pay) |
| 13:30–14:30 / 14:30–15:00 | **Lecture 2** — GW astrophysics & data | Paul Martens |
| 15:30–16:00 | Coffee | |
| 16:00–16:30 | Albert mini-tutorial (ZTF / S190521g light curves; optional) | Albert arrives ICN ~11:20 → afternoon only |
| 16:30–17:00 | Presentation | Donniel Cruz |
| 17:00–18:00 | Team pairing & quick discussion | Senior+junior pairing (Chunglee proposal by 30 Oct) |
| 18:00–19:30 | **Dinner with all participants** (Ewha-provided) | Informal science discussion (Albert’s request) |

**Day‑1 gate (by 18:00):** each team submits science question, minimum deliverable, calculation/data required, and proposed representative figure.

### Friday 20 November — working day

| Time | Session |
|---|---|
| 09:30–10:00 | Brainstorm |
| 10:00–11:00 | Quick goal presentations |
| 11:00–12:00 | Hands-on session |
| 12:00–13:30 | Lunch (provided by Ewha) |
| 13:30–14:30 | Hands-on session 2 |
| ~13:00–14:00 window | **Progress check** (~10 min/team): calculated so far, current figure, main blocker, plan for rest of day |
| 17:00–18:00 | Checkpoint presentations |

**Day‑2 gate:** interpretable first version of the representative figure; otherwise switch to the project **fallback** immediately.

### Saturday 21 November — wrap & posters

| Time | Session |
|---|---|
| 09:30–10:00 | Welcome & final roadmap |
| 10:00–12:00 | Hands-on session 3 (final calculations & interpretation) |
| 12:00–13:30 | Lunch (self-arranged; campus eateries) |
| 13:30–14:30 | Checkpoint presentations 2 · **results frozen ~14:00** for poster prep |
| 14:30–16:30 | Hands-on session 4 — wrapping up & poster writing |
| ~19:00 | 5‑min practice presentation per team with feedback |
| **20:00** | **Final poster PDF** emailed to Chunglee for printing |

### Bridge into EAGW2026 (Yonsei)

| When | What |
|---|---|
| Sun 22 / Mon 23 | Poster printing; CK pick-up Fuji Xerox ECC ~11:00 Mon; posters up at Yonsei before 13:00 |
| Mon 23 morning | Optional school satellite: results recap & paper-writing plan |
| Tue 24 morning | Poster sparkler session (5 teams × ~5 min; chairs TBD: Paul & Surojit?) |
| Tue/Wed 24–25 | Feedback during poster sessions; final 1‑hour project meeting to lock extensions |

## Work distribution (proposed for 30 Oct discussion)

Still open in Chunglee’s 26 Oct note — draft split for discussion:

| Area | Suggested lead(s) | Deliverable before camp |
|---|---|---|
| Common AGN grid + `pAGN` notebooks | Paul / Otto | Fiducial \((M, r/R_g)\) grid + disk profiles |
| Q1 spatial / skymaps | Surojit (+ Otto) | Slim sky maps + AGN catalog subset + starter cross-match notebook |
| Q2 EM / ZTF flares | Albert (+ Paul) | Cleaned ZTF19abanrhr + control sample + starter notebook; Albert tutorial Thu afternoon |
| Q3 remnant retention | Paul | Slim PE columns + `precession` kick notebook |
| Q4 propagation bias | Otto / Paul | Analytic notebook on common grid |
| Q5 environmental dephasing | Otto (+ validator) | Toy acceleration term + validated gas/DM prescriptions (**model-validation gate before 13 Nov**) |
| Repo, env file, Git prep page | Otto / Paul | This site + `uv`/`pyproject.toml` + `scripts/fetch_data.py` + smoke test |
| Student pairing | Chunglee | Proposal by 30 Oct; assign by 6 Nov if pre-reading desired |
| Posters / printing / dinners | Chunglee (LOC) | Templates + print booking |

## Common deliverables (every team)

1. Science question  
2. Principal physical model / equation  
3. Data used (or parameter grid)  
4. One representative quantitative figure  
5. Quantitative conclusion (with numbers)  
6. Main limitation  
7. Paper-extension plan  

## Organizer preparation timeline

| Deadline | Task |
|---|---|
| 23 Oct | Fix AGN catalog, event list, fiducial grid/disk model, poster size *(target from plan doc)* |
| **30 Oct** | SOC: lock session details, work distribution, pairing proposal |
| **6 Nov** | Publish `uv` env + repo; send pre-reading; assign teams (if agreed); slim data ready |
| **13 Nov** | Starter notebooks run end-to-end; students finished Git prep; poster printing booked |
| **18 Nov** | Offline USB/server copy; room Wi‑Fi & power check |
| **23 Nov** | Posters printed and displayed at Yonsei |

## Open points for 30 Oct

1. Exact titles/durations for Lecture 1–2 and whether Albert’s ZTF tutorial is in the formal timetable.  
2. Confirm work distribution and who validates Q4/Q5 formulae (model-validation gate).  
3. Confirm team assignment date (before camp vs Day 1).  
4. Poster template size and shared plotting style.  
5. Whether Hands-on homepage stays on GitHub Pages, Google Sites “Hands-on” tab, or both (link from [EAGW2026](https://sites.google.com/view/eagw2026/home)).
