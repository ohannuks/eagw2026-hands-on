---
title: Projects Q1–Q5
description: Science questions, methods, materials, and fallbacks for the five Hands-on teams
permalink: /projects/
---

## Shared setup

- **Fiducial AGN grid:** \(M_\mathrm{SMBH} = 10^6,10^7,10^8\,M_\odot\); \(r/R_g\) from \(10^1\) to \(10^5\) (log grid); Sirko & Goodman (2003) and/or Thompson et al. (2005) via **pAGN** (Gangardt et al. 2024).
- **Common events:** **GW190521** (all teams where applicable); **GW231123** for Q3 & Q4.
- **Cosmology:** Planck18 (`astropy`).
- **Catalog:** GWTC-5.0 / GWOSC for GW data; Quaia recommended for Q1; ZTF light curves for Q2.
- **Fetch official data with `uv`:** see [Git prep]({{ '/git-prep/' | relative_url }}) and `uv run python scripts/fetch_data.py --help`.
- **Undergrad-friendly:** Q3 and Q4 preferred for undergraduate members (short code path / analytic).

---

## Q1 — Spatial diagnostic

**Question.** Do well-localized GWTC-5.0 BBHs show spatial association with luminous AGN, and how much constraining power does a small sample carry?

**Boot-camp method.** Select 3–5 BBHs with the smallest 90% localization volumes; cross-match 3D sky maps with the AGN catalog (`ligo.skymap` crossmatch); compare counts to background. Optionally combine in a simple mixture likelihood for \(f_\mathrm{AGN}\).

**Materials.** Slim sky-map FITS; AGN catalog subset with luminosity & comoving distance; starter cross-match notebook.

**Figure.** AGN in 90% volume vs background expectation (and \(f_\mathrm{AGN}\) likelihood if ready).

**Fallback.** One event: AGN count vs luminosity threshold.

**Key refs.** Bartos et al. 2017; Veronesi et al. 2023, 2025; Zhu & Chen 2025; Pouw et al. 2026.

---

## Q2 — Electromagnetic diagnostic

**Question.** Given normal AGN variability, how unusual is an optical flare associated with a BBH merger? Principal test case: **GW190521–ZTF19abanrhr**.

**Boot-camp method.** Define a simple flare statistic on cleaned ZTF light curves; measure frequency in a control sample; estimate chance-coincidence probability. Also compute expected merger–flare delay vs kick (McKernan et al. 2019) using the common disk model.

**Materials.** ZTF g/r light curves of ZTF19abanrhr; control sample of similar AGN; AGN count in GW190521 volume; starter plotting notebook. Albert’s S190521g tutorial slides (optional Thu afternoon).

**Figure.** (1) candidate vs control distribution; (2) flare delay vs remnant kick.

**Fallback.** Panel (1) only, fixed amplitude threshold.

**Key refs.** Graham et al. 2020, 2023; McKernan et al. 2019; Cabrera et al. 2026; Zhu et al. 2026.

---

## Q3 — Remnant diagnostic

**Question.** For selected GWTC-5.0 BBHs, what is the probability the remnant remains in a globular cluster, nuclear star cluster, or AGN disk?

**Boot-camp method.** Remnant mass/spin/kick from PE samples via `precession` (or similar). Compare \(v_\mathrm{kick}\) to escape speeds (GC/NSC). For AGN disks use embedded condition \(v_\mathrm{kick} < (H/r)\,v_K\) on the common grid. Include GW190521 & GW231123 plus ordinary events for contrast.

**Materials.** Slim posterior columns (~10–15 events); \(H/r(r/R_g)\) from common disk model; starter kick notebook.

**Figure.** Retention probability by event & environment; for AGN, vs \(r/R_g\).

**Fallback.** GC & NSC only, fixed escape velocities.

**Key refs.** Gerosa & Berti 2019; Gerosa & Fishbach 2021; Gerosa & Kesden 2016; Varma et al. 2019.

---

## Q4 — Propagation diagnostic

**Question.** How strongly can the gravitational field and orbital motion around a SMBH modify apparent BBH properties (redshift, Doppler, lensing)?

**Boot-camp method.** On the common grid: gravitational redshift + LOS Doppler for a fixed circular-orbit reference geometry; point-mass lensing magnification & time delay for one alignment; resulting bias in inferred source-frame mass and luminosity distance.

**Materials.** Common grid + plotting template; worked redshift notebook.

**Figure.** Fractional mass bias vs \(r/R_g\) for three \(M_\mathrm{SMBH}\), split by redshift / Doppler / lensing (1% and 10% levels marked).

**Fallback.** Gravitational redshift + Doppler only.

**Key refs.** Chen, Li & Cao 2019; D’Orazio & Loeb 2020; Takahashi & Nakamura 2003.

---

## Q5 — Environmental diagnostic

**Question.** How do AGN gas interaction, centre-of-mass acceleration in the SMBH potential, and a dark-matter spike modify the GW inspiral phase of a stellar-mass BBH?

**Boot-camp method.** Use the provided toy prescriptions for (1) gas drag/torque on the **inner** binary, (2) LOS CoM acceleration \(GM_\mathrm{SMBH}/r^2\), (3) DM-spike term with checked force law. Compute \(\Delta\Phi(f)\) in LVK and LISA bands (~1 rad as order-of-magnitude reference only). Do **not** copy EMRI formulae onto the stellar-mass binary without a justified mapping.

**Materials.** Common grid, disk densities, one DM spike profile; vacuum evolution + worked acceleration notebook.

**Figure.** Dephasing budget \(\Delta\Phi(f)\) for gas / acceleration / DM with LVK & LISA bands marked.

**Fallback.** Acceleration + one validated gas term; or acceleration-only scaling study with documentation if other terms are not validated in time.

**Key refs.** Barausse, Cardoso & Pani 2014; Inayoshi et al. 2017; Yunes et al. 2011; Eda et al. 2013; Kavanagh et al. 2020.

---

## After the boot camp

Combined diagnostic map + GW190521 case study; extension milestones through **late February 2027**. After EAGW2026 we decide which diagnostics enter the joint manuscript.
