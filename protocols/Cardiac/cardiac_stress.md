# Cardiac Stress (Adenosine Stress/Rest Perfusion CMR — T1 Mapping + LGE)

**Version:** 1.0 | **Date:** 2026-08-29 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Heart centred over the coil.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly. ECG leads on the anterior chest wall, clear of the coil elements.
- **Laser Landmark:** Mid-sternum at heart level.
- **ECG:** Vector ECG — optimise the R wave (largest amplitude, no T-wave oversensing). Every sequence in this protocol is ECG-gated, so a poor trigger degrades the entire study.
- **IV Access:** **Two lines** — one dedicated to the adenosine infusion, one for contrast. Contrast and adenosine must not share a cannula.
- **Monitoring:** Continuous ECG + pulse oximetry throughout; BP before and during adenosine. Crash trolley and aminophylline available before the stress phase starts.
- **Contraindication screen (adenosine):** Severe asthma/COPD with bronchospasm, 2nd/3rd degree AV block (without pacemaker), sick sinus syndrome, hypotension (SBP < 90), recent ACS, caffeine/theophylline not withdrawn at least 12–24 h before the study.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — a small breath-hold taken at the same point every time is sufficient; oversized held breaths are unnecessary. Consistency matters most: the T1 maps and perfusion stack must not drift between acquisitions. Warn the patient that one series — the perfusion — has a long breath-hold: when the breath can no longer be held, resume shallow normal breathing, and do not attempt to take a new breath-hold mid-series.
- **eGFR check:** Gadolinium — confirm eGFR above 30 before the cumulative multi-dose protocol.

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–5)
- **Phase 1 — Rest function:** Cines 3C/4C/2C/LVOT + aortic flow (#6–10)
- **Phase 2 — Setup:** Positioning sweep → native T1 → true pre (#11–13)
- **Phase 3 — Stress:** Water bolus primes the injector → adenosine 180 s + BP checks → response check → stress T1 @ 30 s countdown → contrast 4 ml/s + stress perfusion (#14). *Inadequate response → step-up dose, new 60 s countdown*
- **Phase 4 — Recovery:** HR baseline + 6 min HR recovery wait → dose 2 → rest perfusion (#15)
- **Phase 5 — LGE:** Dose 3 → volumetry fills the ~7 min wait (#16) → TI scout → overviews → PSIR → optional high-res (#17–22)

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Phase 3 | Gadolinium — dose 1 | 4 ml/s | Stress first-pass perfusion |
| Phase 4 | Gadolinium — dose 2 | 4 ml/s | Rest first-pass perfusion |
| Phase 5 | Gadolinium — dose 3 (top-up) | 4 ml/s | Cumulative dose to the LGE range |
| Phase 3 | Adenosine infusion | 140 µg/kg/min, ~3 min [AI ADDED] | Maximal coronary vasodilation |

**Total contrast: double dose (0.2 mmol/kg) split into three doses** — dose 1 (stress perfusion), dose 2 (rest perfusion), dose 3 (LGE top-up). 0.2 mmol/kg = 0.4 ml/kg of Dotaram (0.5 mmol/ml); if Gadovist (1.0 mmol/ml) is substituted, halve the volume to 0.2 ml/kg to deliver the same dose.

---

## 3. Imaging Series

### Phase 0 — Surveys & Localizers

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 1 | `t2_trufi_tra_thorax_bh` | Axial | True axial | Heart only — no aortic arch. The axial planning localizer | BH (end-insp) |
| 2 | `t2_trufi_cor_thorax` | Coronal | True coronal (plain only) | Whole thorax — anterior chest wall → spine; thoracic inlet → diaphragm | BH |
| 3 | `trufi_pseudo_2c_loc` | Pseudo 2C | Single slice through LV apex + mitral valve centre — planned on #1 | LV + LA — apex → mitral annulus | BH |
| 4 | `trufi_pseudo_4c_loc` | Pseudo 4C | Single slice ⟂ pseudo-2C through apex + both AV valves — planned on #3 | All 4 chambers | BH |
| 5 | `trufi_shortaxis_loc` | Pseudo SAX | ⟂ interventricular septum, ∥ mitral valve plane — planned on #4 | Base → apex, extending basally to include the left atrium (for 3C planning) | BH |

### Phase 1 — Rest Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 6 | `cine_tfi_retro_3c` | 3C (LVOT) | Bisects LV + outflow tract — planned on SA (#5) | LV, LA, LVOT, aortic root | BH |
| 7 | `cine_tfi_retro_4c` | 4C | Through RV angle + LV centre — planned on SA (#5) | All 4 chambers | BH |
| 8 | `cine_tfi_retro_2c` | 2C | Bisects LV, ∥ septum insertion line — planned on SA (#5) | LV + LA | BH |
| 9 | `cine_tfi_retro_lvot_noscout` | LVOT | ⟂ 3C view, through and bisecting the LVOT — planned on #6. No auto-scout | LVOT + aortic valve | BH |
| 10 | `flow_150_tp_retro_bh_ao` | Through-plane | ⟂ ascending aorta, just above the sinotubular junction | Ascending aorta cross-section | BH |

### Phase 2 — Native T1 & Perfusion Setup

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 11 | `dynamic_tfl_sr_tpat_sax` | SAX stack | **Positioning acquisition** — quick multislice SAX sweep in perfusion format (no contrast), purpose: place SAB/SAM/SAA for the T1 map and perfusion stack. Copied by all T1 maps and perfusion runs | Whole LV short axis — base → apex | BH → shallow |
| 12 | `t1_map` (native) | SAX ×3 | Copy Slice from #11 | Basal, mid, apical SAX | BH |
| 13 | `dynamic_tfl_sr_pre` | SAX ×3 | Copy Slice from #11 — **true pre-contrast baseline, 10 serial measurements** at the three slices | Basal, mid, apical SAX | BH |

### Phase 3 — Adenosine Stress

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Test water bolus (dose 1) + automatic pause** | — | Prime the injector for the first contrast dose; automatic pause before the contrast injection | — | — |
| — | **Base BP + adenosine countdown 180 s** | — | Base BP logged; infusion at 140 µg/kg/min. BP measured & logged at 150 s and 90 s countdown; radiologist reviews the BP/HR response | — | — |
| — | **Response check + last BP / step-up** | — | Adequate (BP ↓ ≥10 mmHg or HR ↑ ≥10 bpm): proceed — stress T1 map at 30 s countdown, last BP at 20 s countdown, inject contrast only after the BP cuff has fully deflated. Inadequate: add adenosine dose, new 60 s countdown, stress T1 map at peak, inject after it finishes | — | — |
| — | **Stress T1 map — at 30 s countdown** | SAX ×3 | Copy Slice from #11 — at countdown 30 s (peak stress) | Basal, mid, apical SAX | BH |
| — | `t1map_nativestress` 5(6)3SA | SAX ×3 | Copy Slice from #11. MOLLI 5(6)3 | Basal, mid, apical SAX | BH |
| — | **Contrast — 4 ml/s** | — | Gadolinium bolus at 4 ml/s + saline flush [Confirm dose] | — | — |
| 14 | `dynamic_tfl_sr_stress_C` | SAX ×3 | Copy Slice from #11 | Basal, mid, apical SAX | BH → shallow |

### Phase 4 — Recovery & Rest Perfusion

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **6 min wait** | — | Adenosine stopped. Wait until HR returns to baseline, then 6 min | — | — |
| — | **Contrast — dose 2** | — | 2nd gadolinium dose at 4 ml/s — injected after the 6 min wait | — | — |
| 15 | `dynamic_tfl_sr_rest_C` | SAX ×3 | Copy Slice from #11 — **start immediately with the injection** | Basal, mid, apical SAX | BH → shallow |

### Phase 5 — Post-Contrast & LGE

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **3rd dose injection** | — | Top-up dose at 4 ml/s, injected **immediately before** the volumetry cine; LGE imaging starts ~7 min after the 3rd dose | — | — |
| 16 | `cine_tfi_retro_sa_volumetry_c` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |
| 17 | `ti_scout` | SAX single | Single SA location at the thickest myocardium (mid-ventricular) | Single mid SAX slice | BH |
| 18 | `de_overview_tfl_4c` | 4C | Copy Slice from #7 — prospective gating, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 19 | `de_overview_tfl_2c` | 2C | Copy Slice from #8 — prospective gating, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 20 | `de_overview_tfl_sax` | SAX stack | Copy Slice from #16 — prospective gating, TI increased gradually | Entire myocardium wall — whole LV | BH |
| 21 | `de_trufi_overview_12si_psir_fb` | SAX ×12 | Copy Slice from #16 — 12 slices | Base → apex | FB |
| 22 | `de_high-res_tfl_fs_sax` | SAX stack (optional 2D) | Copy Slice from #16 — only if radiologist finds a suspicious lesion on #21; TI set from #17, incremented | Base → apex, built slice-by-slice upward toward the apex | BH |

---

## 4. Sequence Rationale

### Core Strategy

The study answers three questions in one sitting: **Is there inducible ischemia?** (adenosine stress/rest first-pass perfusion — a reversible dark defect in stress that fills in at rest), **Is there microvascular dysfunction?** (stress T1 reactivity — the T1 rise at peak adenosine, which is blunted in microvascular disease), and **Is there scar or fibrosis?** (LGE). Rest cine function and aortic flow complete the picture: volumes, EF, wall motion, and aortic regurgitation.

The protocol is built around a single adenosine infusion that serves two stress acquisitions: the stress T1 map at peak vasodilation (at countdown 30 s), then the stress perfusion first pass — one stressor, two measurements, one contrast bolus.

### Phase 0 — Surveys & Localizers (#1–#5) — the planning stage

This phase **is** the planning — every later plane is derived from it. TrueFISP is balanced SSFP: blood is bright regardless of flow velocity, myocardium dark — the ideal contrast for planning and cine.

**`t2_trufi_tra_thorax_bh` (#1)** — the axial TrueFISP survey — is the **axial planning localizer**: heart-only coverage, no aortic arch needed, the starting point for every subsequent step.

**`trufi_pseudo_2c_loc` (#3), `trufi_pseudo_4c_loc` (#4), `trufi_shortaxis_loc` (#5)** — the pseudo-2C/4C/SAX — are single-slice steps of the **planning cascade**: "pseudo" because each is an approximation of the true long-axis geometry, refined at the next step. The cascade ends at the pseudo-SAX (#5), which shows the true short-axis geometry — the true cine long axes (3C/4C/2C) are then planned back from it (Phase 1):

1. **Axial → pseudo 2C (#3):** on the axial localizer, place a single slice along the LV long axis, through the LV apex and the centre of the mitral valve — the first approximation of the 2-chamber view. Coverage: LV + LA, apex → mitral annulus.
2. **Pseudo 2C → pseudo 4C (#4):** on the pseudo-2C image, prescribe a plane perpendicular to it whose trace passes through the LV apex and the centre of the mitral valve, continuing to the tricuspid valve — the first approximation of the 4-chamber view.
3. **Pseudo 4C → SA localizer (#5):** on the pseudo-4C, prescribe the short-axis stack **perpendicular to the interventricular septum and parallel to the mitral valve plane**. Coverage runs base → apex and extends basally to include the **left atrium** — the cine 3C is planned from these basal slices later.

### Phase 1 — Cine Function & Flow (#6–#10)

**Retrospective gating** (all cines): data are acquired continuously and sorted into cardiac phases afterwards — every phase of the cardiac cycle is covered including late diastole, and the acquisition tolerates arrhythmia better than prospective triggering. Each long-axis cine is a single breath-held slice.

**True cine planning — back from the SA localizer.** The true long-axis cines are not planned from the pseudo views — they are planned on the SA localizer (#5), which shows the true short-axis geometry:

- **`cine_tfi_retro_3c` (#6):** on the SA, the plane that bisects the LV and also bisects the outflow tract — its trace runs through the centre of the LV cavity and the centre of the LVOT/aortic valve seen on the basal slices.
  - **What it shows:** the LV long axis with the LVOT and aortic valve opening into the aortic root — the outflow-tract view. Assesses aortic valve motion and AS/AR (aortic stenosis/aortic regurgitation) jets, the subvalvular outflow, and the anteroseptal/inferolateral walls and septal motion.

- **`cine_tfi_retro_4c` (#7):** on the SA, the plane through the angle of the RV and the centre of the LV — the trace joins the RV corner (acute margin) to the LV centre, bisecting the LV. Check the other SA slices: the plane must avoid the aorta on every other SA plane.
  - **What it shows:** all four chambers — the septum and lateral LV wall profiled on either side, mitral and tricuspid valve function, RV size and function, both atria. The reference view for global function and regional septal/lateral wall motion.

- **`cine_tfi_retro_2c` (#8):** on the SA, the plane that bisects the LV and parallels the line joining the two RV septal insertions — a vertical plane cutting through the anterior and posterior walls, not the septum.
  - **What it shows:** LV + LA only, cut through the anterior and posterior (inferior) walls — the two walls that lie perpendicular to the septum and are not profiled en face in the 4C. Assesses anterior/inferior wall motion, the mitral valve, and LA size.
  
- **`cine_tfi_retro_lvot_noscout` (#9):** planned on `cine_tfi_retro_3c` (#6), not on the SA — a plane perpendicular to the 3C that passes through and bisects the LVOT; acquired with no auto-scout (`noscout`) because the geometry is already known from #6.
  - **What it shows:** the outflow tract in its orthogonal long axis — aortic valve opening, the subvalvular region (dynamic LVOT obstruction), and the aortic root.

**`flow_150_tp_retro_bh_ao` (#10):** ⟂ to the ascending aorta, just above the sinotubular junction (~ level of the right pulmonary artery) — a clean perpendicular cross-section, with perpendicularity verified against the aorta in **both orthogonal aortic views**: the slice must cut the aorta on end in both projections, not just one.
  - **What it does:** a through-plane **phase-contrast (velocity-encoded)** sequence — moving spins acquire phase proportional to velocity, and the aortic flow curve over the cardiac cycle gives forward volume, regurgitant fraction, and stroke volume. Retrospective gating + breath-hold gives the cleanest through-time flow curve.
  - **How it works:** a bipolar gradient pair along the slice axis gives moving spins a residual phase proportional to velocity, while static tissue cancels to zero — the sequence outputs a magnitude image (anatomy) and a phase image (velocity per pixel). Through-plane encoding measures exactly the flow crossing the slice plane; summing the pixel velocities over the vessel gives instantaneous flow rate. Retrospective gating reconstructs the flow curve over the cardiac cycle — integrating it yields stroke volume, forward volume, and regurgitant fraction.
  - **Segments:** with retrospective gating the acquisition is divided into segments — the number of k-space lines acquired per heartbeat. This is the temporal-resolution vs scan-time lever: fewer segments per beat → more cardiac phases reconstructed (finer flow curve) but a longer acquisition; more segments → shorter scan but coarser temporal sampling. Segments do not affect velocity sensitivity — that is set by the VENC.
  - **VENC (velocity encoding):** the 150 in the name is the velocity-encoding limit. Velocities above it wrap around and masquerade as reversed flow (aliasing) — check the whole flow curve for wrapping; if VENC 150 is exceeded (high-velocity jet, e.g. aortic stenosis), repeat at a higher VENC (400 cm/s).

### Phase 2 — Native T1 & Perfusion Setup (#11–#13)

**What this phase does (overview)**

Phase 2 lays the foundation for both stress measurements. Three things happen, all at the same three SAX slices (SAB/SAM/SAA):

1. **The geometry is established** — `dynamic_tfl_sr_tpat_sax` (#11) sweeps the whole LV in perfusion format; from its images you place the three slices SAB/SAM/SAA, which every following acquisition copies.
2. **The baseline state is measured** — `t1_map` (#12) captures the native myocardial T1: the "before" of the stress reactivity measurement, and a tissue-characterisation readout in its own right (fibrosis, oedema, amyloid).
3. **The perfusion baseline is captured** — `dynamic_tfl_sr_pre` (#13) runs the true pre-contrast acquisition (10 serial measurements) at the three slices: the S0 baseline signal for perfusion analysis and the final setup confirmation before adenosine starts.

**The design rule:** one geometry, two measurements, all slice-matched — reactivity (stress T1 − native T1) and perfusion (stress − rest) are only interpretable if they read the same myocardium.

**`dynamic_tfl_sr_tpat_sax` (#11) — positioning sweep**
A quick multislice SAX sweep in perfusion format (saturation-recovery TurboFLASH, no contrast), covering the whole LV and discarded after planning.
- **Purpose:** localize the three slices SAB/SAM/SAA — chosen so they image well in the real perfusion runs (nulling, coverage, slice-per-RR fit). Perfusion format is deliberate: the geometry and contrast preview transfer directly to `t1_map` and the perfusion acquisitions.
- **Slice placement:** the levels are set on the positioning sweep using the **systolic phase of the 4C and 2C cines** as the long-axis reference. Systole is chosen deliberately: by end-systole the mitral annulus has descended to its most apical position, so a basal slice placed just below it at that phase stays clear of the valve for the whole cardiac cycle — the contracting heart has already moved the annulus to its lowest point, and diastole only carries it back basally, away from the slice. SAB (basal) sits just below the mitral annulus/LVOT, avoiding outflow-tract partial volume; SAM (mid) at the papillary muscle level; SAA (apical) distal to the papillary tips, where the myocardium still forms a complete ring around the cavity. All three ⟂ LV long axis, one slice per heartbeat — all three must fit within one RR interval (single-shot readout per beat).

**`t1_map` (#12) — native T1 map**
Three SAX slices, copy #11, MOLLI, breath-hold.
- **What T1 mapping is & how it's done:** a T1 map is an image where every pixel's value *is* the tissue's T1 in milliseconds — quantitative, not just weighted. MOLLI does it in three steps: a 180° inversion pulse flips the magnetization upside-down, then single-shot images are acquired at successive inversion times (one per heartbeat, motion-corrected), each sampling the exponential recovery curve at a different point; a pixel-wise fit of that curve returns the T1 value. Long-T1 tissue (more water, fibrosis, amyloid) recovers slowly; short-T1 (fat, iron) recovers fast.
- **What it does here:** the native map is (a) the baseline for stress T1 reactivity — healthy myocardium lengthens ~6% under adenosine as blood volume rises; a blunted rise means microvascular dysfunction — and (b) a tissue-characterisation readout: elevated native T1 flags fibrosis, oedema, amyloid.
- **The B(R)A sampling scheme:** T1 mapping schemes are written as image blocks separated by a recovery pause — **B(R)A** = B images acquired in consecutive heartbeats **B**efore the pause, **R**ecovery heartbeats without imaging (letting magnetization recover before the next inversion), then A images **A**fter the pause — B+A samples in one breath-hold. **R is heart-rate-dependent: the recovery heartbeat count increases as the RR interval decreases** — at a faster heart rate each beat allows less recovery time, so more beats are needed to restore the magnetization before the next inversion. The scheme is protocol-dependent; see the T1 mapping protocol.

**`dynamic_tfl_sr_pre` (#13) — the true pre**
Three SAX slices, copy #11, breath-hold.
- **What it does:** the true pre-contrast acquisition — 10 serial measurements at the three slices. Provides the baseline signal (S0) for perfusion analysis and the final setup confirmation immediately before the stress choreography, so nothing fails during the stress run.

**The perfusion sequence family — how stress/rest will image**
`dynamic_tfl_sr` is the perfusion sequence: each heartbeat, a saturation-recovery pulse nulls the myocardium, then a single-shot TurboFLASH readout images all three SAX slices within one RR interval (T-PAT temporal parallel imaging accelerates this). The images are T1-weighted — the gadolinium bolus arriving in perfused myocardium shortens T1 and turns it bright; a territory supplied by a stenosed artery receives little or no bolus and stays dark. **Stress vs rest** distinguishes reversible ischemia (dark under stress, bright at rest) from fixed defects. Three runs of the family are used across the study — `dynamic_tfl_sr_pre` (#13, pre-contrast baseline), `dynamic_tfl_sr_stress_C` (#14, at peak adenosine), `dynamic_tfl_sr_rest_C` (#15, post-recovery) — all sharing the slices placed by #11.

### Phase 3 — Adenosine Stress

The choreography, timed from the start of the infusion:

- **Priming — test water bolus + automatic pause:** before the stress phase, a test water (saline) bolus is run for the first contrast dose to verify the injector line and timing; the injector then holds an automatic pause before the actual contrast injection.
- **"countdown 180 s (+0 s)" — base BP + adenosine start:** log the base BP, start adenosine at 140 µg/kg/min, countdown 180 s. Maximal coronary vasodilation is reached at ~3 min. Vasodilatation raises flow 3–4× in normal vessels; a stenosed territory is already maximally dilated and cannot increase — the relative flow difference is what the perfusion images show.
- **BP schedule:** BP is measured and logged at **"countdown 150 s (+30 s)"** and **"countdown 90 s (+90 s)"** — the base BP and every subsequent measurement are logged.
- **Radiologist review:** the radiologist is called to review the change in BP and HR during the stress before proceeding.
- **Response check — adequate vs inadequate (after the radiologist review, before the stress T1 map):**
  - **Adequate response** — BP ↓ ≥ 10 mmHg OR HR ↑ ≥ 10 bpm: no additional medication needed. Proceed — stress T1 map at 30 s countdown, last BP at **"20 s (+160 s)"**, then inject the contrast **only after the BP cuff has fully deflated** — an inflated cuff compresses the arm veins and would delay or blunt the bolus.
  - **Inadequate response** — neither criterion met: add a dose of adenosine and start a new 60 s countdown (**"60 s (+60 s)"** from the step-up); acquire the stress T1 map at peak, then inject the contrast after the countdown finishes. Without an adequate response, both the stress T1 map and the stress perfusion are meaningless.
- **"countdown 30 s (+150 s)" — `t1map_nativestress` (stress T1 map):** acquired at peak stress when the countdown reaches 30 s (= +150 s), timed so it finishes just before the bolus injection (last BP at +160 s, contrast at +180 s) — the map captures maximal hyperemia and the bolus timing is not disturbed. In the step-up branch, the map is acquired at the equivalent point of the new 60 s countdown.
- **"countdown 0 s (+180 s)" — Contrast at 4 ml/s + `dynamic_tfl_sr_stress_C` (#14):** the bolus is injected at peak stress, at 4 ml/s for a tight first-pass bolus, followed by a saline flush at the same rate. The acquisition starts with the injection — breath-hold for as long as possible through the bolus, then shallow breathing. ~50–60 dynamics cover the bolus passage through the RV, lungs, and LV myocardium.

### Phase 4 — Recovery & Rest Perfusion (#15)

- **6 min wait:** adenosine stopped; wait until the HR returns to baseline, then a further 6 min — both for the patient to recover and for the first-pass contrast to clear from the blood pool.
- **Contrast — dose 2:** the second of the three doses is injected after the wait (the total double dose is split into three: stress, rest, LGE top-up).
- **`dynamic_tfl_sr_rest_C` (#15):** the rest perfusion starts **immediately with the injection**, at identical slices — comparing stress and rest separates reversible ischemia from fixed defects.

### Phase 5 — Post-Contrast & LGE (#16–#22)

**What this phase does (overview):** after the rest perfusion, the third (top-up) dose is injected **immediately before** the SA volumetry cine — completing the double-dose split — and brings tissue concentrations to the LGE range. The phase then splits into two jobs: the **SAX volumetry** fills the ~7-minute wait after the 3rd dose, and at ~7 min the **late gadolinium enhancement (LGE) images** are acquired. Infarct and fibrosis have an expanded extracellular space where gadolinium accumulates and washes out slowly; normal myocardium nulls on an inversion-recovery image, scar stays bright.

**Part 1 — SAX Volumetry**

**`cine_tfi_retro_sa_volumetry_c` (#16):** the function measurement of the study — **ejection fraction** from Simpson's-method LV volumes, EF, and mass.
- **Planning:** on the **diastolic phase** of the cines; contiguous slices ⟂ LV long axis, no gaps.
- **Coverage:** the whole ventricle, and a bit beyond — the first (most apical) image shows **no blood pool** (it lies beyond the apex), and the last (most basal) image lies **past the mitral valve level** — so no myocardium is excluded at either end. A stack shorter than this at either end drops myocardium and skews the EF.
- **Mechanism — how EF is measured from this acquisition:** the stack is **retrospectively gated**, so every slice contains the full cardiac cycle, and it is contiguous from base to apex. EF uses the **modified Simpson's method (disk summation)**: on the end-diastolic and end-systolic frames of each slice, the endocardial border is traced — the enclosed bright blood pool (TrueFISP blood is bright, brighter still post-contrast) gives the slice's cross-sectional area; area × slice thickness = that slice's volume at that phase. Summing all slices at end-diastole gives **EDV**, at end-systole gives **ESV**, and **EF = (EDV − ESV) / EDV**. The coverage rules above exist precisely to make the summation valid — a missing apical or basal slice is a missing disk, and a gap breaks the stack. Myocardial mass is derived from the epicardial vs endocardial contours (myocardial volume × myocardial density).

**Part 2 — Late Gadolinium Enhancement**

The LGE principle: at the equilibrium phase, scar/fibrosis holds onto gadolinium (expanded extracellular space, slow washout) and stays **bright** on an inversion-recovery image, while normal myocardium is **nulled (dark)**. Everything from here on depends on the TI being right.

**`ti_scout` (#17):** performed at the **7-min mark (the late gadolinium enhancement window)** at a **single SA location through the thickest myocardium** (typically mid-ventricular). A Look-Locker series sweeps through inversion times to find the TI that nulls normal myocardium — it appears uniformly dark, while infarcted tissue keeps a different (brighter) look, which is exactly the contrast the DE images rely on. The **optimal TI is where normal myocardium is most uniformly dark without a dark rim**: a dark rim at the myocardial border means the blood pool is nulling too (TI too short) — the rim itself is the interface voxels, partial-volumed between the nulled blood pool and the myocardium — which would hide subendocardial scar against it; at the correct TI the myocardium is dark and the blood pool stays bright.

**DE overview series — prospective gating.** All three are IR-prepared TurboFLASH, **prospectively gated** (one image per slice, acquired at a fixed cardiac phase):
- **`de_overview_tfl_4c` (#18):** 4C.
- **`de_overview_tfl_2c` (#19):** 2C.
- **`de_overview_tfl_sax` (#20):** SAX stack.
The **TI setting is increased gradually across the DE series** — as contrast washes out of the myocardium, T1 lengthens and the null point drifts later, so each subsequent series needs a slightly longer TI. They also verify the enhancement pattern and nulling before the definitive images.

**`de_trufi_overview_12si_psir_fb` (#21) — TrueFISP PSIR overview:** a 12-slice SAX stack with phase-sensitive inversion recovery, free-breathing. PSIR is insensitive to TI error — the robust whole-ventricle survey that catches enhancement anywhere (including RV and thrombus) even if the TI is imperfect. **After this series, consult the radiologist** — if a suspicious lesion is found, proceed to the optional high-res series (#22).

**`de_high-res_tfl_fs_sax` (#22) — high-res FS SAX (optional):** the definitive, targeted LGE acquisition — an **optional 2D series**, performed only if the radiologist finds a suspicious lesion on the overviews/PSIR. The TI is set (from the TI scout, incremented for the elapsed washout). Acquired as a **2D series — the SAX stack is built by repeatedly acquiring single 2D slices, stacking upward towards the apex**, each slice individually breath-held. Fat saturation removes the bright epicardial fat signal so thin subepicardial enhancement is not masked, and the high in-plane resolution delineates infarct transmurality, which drives viability-based decisions.

- **Why both the DE overviews and the PSIR are needed:** both detect scar, but each fails in the way the other is immune to — together they close the gaps:
    - **The DE overviews alone are not safe — TI-dependent:** magnitude-reconstructed IR-TurboFLASH contrast lives and dies by the TI — too short and it is the infarct itself that nulls (gadolinium shortens its T1, so its null point arrives earlier than normal myocardium's), turning the scar dark and invisible (**false negative**); too long and normal myocardium stays bright (**false positive**) — and the TI drifts as contrast washes out.
    - **The PSIR is the safety net — TI-insensitive:** phase-sensitive reconstruction reads the sign of the magnetization, so the contrast direction survives TI error; free-breathing whole-ventricle coverage catches enhancement anywhere (RV, thrombus, unexpected territories). Its blind spots — lower resolution, bSSFP dark-rim/flow artifacts — are what the breath-held, TI-optimized overviews compensate for: better scar contrast in planes matched to the cines, and a live check that the scout TI works.
    - **The division of labour:** the overviews find the scar and prove the TI; the PSIR guarantees nothing is missed. Only when the two agree — or either flags a suspicion — is the optional high-res series spent on the lesion.

- **How the high-res series differs from the DE overviews (#18–#20):**
    - **Mechanism:** same IR-TurboFLASH readout and gating — the difference is strategy: the overviews are standard-resolution multi-slice; the high-res series is segmented 2D, one slice per breath-hold, fat-saturated.
    - **Result:** fast routine survey vs much sharper in-plane resolution with dark (suppressed) epicardial fat.
    - **What they look for:** the overviews answer "is there enhancement, and is the TI right?"; the high-res series answers "how thick is the scar, and is it transmural?".
    
- **How the high-res series differs from the PSIR overview (#21):**
    - **Mechanism:** the PSIR is free-breathing TrueFISP with phase-sensitive IR — contrast independent of TI errors; the high-res series is segmented 2D IR-GRE, breath-held, magnitude-reconstructed — contrast depends on the TI being exactly right, in exchange for higher in-plane resolution and fat saturation.
    - **Result:** PSIR = fast, robust, TI-foolproof, lower resolution; high-res = TI-dependent, sharper, fat removed.
    - **What they look for:** the PSIR is the catch-all — enhancement anywhere (RV, thrombus, unexpected territories); the high-res series is the definitive measurement of scar thickness and transmurality on the region the radiologist flagged.

---

## 5. Variations

**Arrhythmia / poor breath-hold — real-time cine fallback:** the real-time cine rescues the **retrospective-gated cine sequences only** — the mapping, perfusion, and LGE sequences remain gated. Full fallback description: `cardiac_non-stress.md` Variations.
    - **What to swap:** `cine_tfi_retro_3c/4c/2c/lvot_noscout/sa_volumetry_c` → the `cine_trufi_cs_rt_adapt_*` real-time counterparts, same planes and coverage, no other parameter changes.
    - **What it does not rescue:** the T1 maps, the perfusion runs, and the aortic flow — note these limitations in the report.

**Inadequate stress response**
- Step up the adenosine dose (up to 210 µg/kg/min) before the stress T1 map and perfusion — without an adequate HR/symptom response the stress data are non-diagnostic.

**Aortic stenosis / high-velocity jet suspected**
- Repeat the flow sequence at VENC 400 cm/s — 150 cm/s aliases at stenotic velocities.

**Suspected myocarditis / oedema**
- Add edema imaging — **T2 mapping (preferred, quantitative)** or a T2 STIR SAX stack (traditional) — and extend the FS LGE to 2C/4C high-res — oedema + subepicardial enhancement pattern is the myocarditis signature. What sequence to add is per radiologist choice — T1/T2 mapping are not necessarily default.

---

## 6. Alerts

### Pre-stress

| Check | Improve |
|---|---|
| **Caffeine/theophylline** — withdrawn 12–24 h? | Caffeine blocks the adenosine receptor — blunted stress response |
| **Total gadolinium dose + eGFR** — cumulative dose within limit? | The check matters because a **double dose Dotaram** is given, split into three (stress, rest, top-up) — check before, not after. **If eGFR < 30: consult the radiologist** — adjust the dose or consider switching to **Gadovist** |
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | Choose the ECG lead with the cleanest R wave (largest amplitude, no T-wave oversensing) — every sequence is gated, so a poor trigger degrades the entire study |
| **Breath-hold consistency** — same end-inspiratory position on T1 maps and perfusion? | Slice drift between pre/stress/rest acquisitions breaks the comparison |
| **VENC** — any aliasing in the aortic flow? | Aliased phase wraps velocities — repeat at higher VENC (400 cm/s) |

### Stress phase

| Check | Improve |
|---|---|
| **Emergency equipment** — aminophylline + crash trolley available before the stress phase? | Adenosine can cause AV block/bronchospasm — reversal must be at hand |
| **Contrast line separate from adenosine line** — correct side and gauge? | Contrast and adenosine must each connect to an IV line of the correct gauge — usually R side for contrast, L side for adenosine — and the **BP cuff must not be on the same side as the adenosine infusion** (cuff inflation would pinch the line and interrupt the infusion). Shared lines dilute or delay the bolus — flat first-pass curves |
| **Adenosine response** — BP ↓ ≥10 mmHg or HR ↑ ≥10 bpm? | Adequate: proceed (last BP at 20 s countdown, inject after cuff deflated). Inadequate: step up the dose, new 60 s countdown — an inadequate response makes stress T1 and stress perfusion meaningless |
| **BP cuff** — fully deflated before the contrast injection? | An inflated cuff compresses the arm veins and delays or blunts the bolus — the last BP at 20 s countdown exists to allow deflation time |
| **Stress T1 timing** — acquired at peak adenosine, at 30 s countdown? | Too early = no hyperemia; too late = collides with the bolus and the 20 s BP |
| **Perfusion breath-hold** — shallow breath-hold held as long as possible, then normal breathing resumed? | Keep the breath-hold shallow — do not exaggerate it: a deep held breath shifts the heart and causes motion when released. Hold as long as possible through the first pass, then resume normal breathing |

### Post-stress

| Check | Improve |
|---|---|
| **TI correctness** — normal myocardium dark on the DE and high-res series? | The nulling TI sits around ~300 ms for normal myocardium — verify it on the DE and high-res images, not just at the scout. If the myocardium looks bright (nulling off) or the delay has shifted, re-scout and re-measure rather than adjusting blindly |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-29 | — | Initial build — 22 workflow steps. TrueFISP surveys + pseudo-localizer cascade + retro cine (3C/4C/2C/LVOT) + aortic flow VENC 150 + native T1 map + adenosine stress (BP schedule, response check, stress T1 map at 30 s countdown, stress perfusion) + rest perfusion + SA volumetry + TI scout + DE overviews (4C/2C/SAX/TrueFISP PSIR FB) + optional high-res FS SAX LGE. Double dose 0.2 mmol/kg split into three |
