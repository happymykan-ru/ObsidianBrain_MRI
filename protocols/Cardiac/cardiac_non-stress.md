# Cardiac Non-Stress (Rest CMR — Function, T1/T2 Mapping + LGE)

**Version:** 2.0 | **Date:** 2026-09-01 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

Same as `cardiac_stress.md` with the stress arm removed:

- **Position:** Supine, head-first. Heart centred over the coil.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly. ECG leads on the anterior chest wall, clear of the coil elements.
- **Laser Landmark:** Mid-sternum at heart level.
- **ECG:** Vector ECG — optimise the R wave (largest amplitude, no T-wave oversensing). Every sequence in this protocol is ECG-gated, so a poor trigger degrades the entire study.
- **IV Access:** **One line** — contrast only; no adenosine, so no second line, no BP cuff choreography, no contraindication screen, and no caffeine restriction.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — a small breath-hold taken at the same point every time is sufficient; oversized held breaths are unnecessary. Consistency matters most: the T1/T2 maps must not drift between acquisitions. (No perfusion run here — the stress protocol's long-hold warning does not apply.)
- **eGFR check:** Gadolinium — confirm eGFR above 30 before the protocol [Confirm threshold].

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–4)
- **Phase 1 — Rest function:** Cines 3C/4C/2C/LVOT + aortic flow (#5–9)
- **Phase 2 — Mapping:** Native T1 map + T2 map (#10–11)
- **Phase 3 — Contrast:** Single dose at 2 ml/s → 7 min wait
- **Phase 4 — Function:** SA volumetry fills the 7-min wait (#12)
- **Phase 5 — LGE:** TI scout → DE overviews → PSIR → T1 seg FS SA (#13–18)

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Phase 3 | Gadolinium — single dose [Confirm mmol/kg] | 2 ml/s | LGE equilibration |

**Total contrast: single dose** [Confirm — stress protocol uses 0.2 mmol/kg split into three; this protocol has one injection]. Slow rate is deliberate: no first-pass perfusion here, so no tight 4 ml/s bolus is needed.

---

## 3. Imaging Series

### Phase 0 — Surveys & Localizers

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 1 | `t2_trufi_tra_thorax_bh` | Axial | True axial | Heart only — no aortic arch. The axial planning localizer | BH (end-insp) |
| 2 | `trufi_2c_loc` | Pseudo 2C | Single slice through LV apex + mitral valve centre — planned on #1 | LV + LA — apex → mitral annulus | BH |
| 3 | `trufi_4c_loc` | Pseudo 4C | Single slice ⟂ pseudo-2C through apex + both AV valves — planned on #2 | All 4 chambers | BH |
| 4 | `trufi_shortaxis_loc` | Pseudo SAX | ⟂ interventricular septum, ∥ mitral valve plane — planned on #3 | Base → apex, extending basally to include the left atrium (for 3C planning) | BH |

### Phase 1 — Rest Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 5 | `cine_tfi_retro_3c` | 3C (LVOT) | Bisects LV + outflow tract — planned on SA (#4) | LV, LA, LVOT, aortic root | BH |
| 6 | `cine_tfi_retro_4c` | 4C | Through RV angle + LV centre — planned on SA (#4) | All 4 chambers | BH |
| 7 | `cine_tfi_retro_2c` | 2C | Bisects LV, ∥ septum insertion line — planned on SA (#4) | LV + LA | BH |
| 8 | `cine_tfi_retro_lvot_noscout` | LVOT | ⟂ 3C view, through and bisecting the LVOT — planned on #5. No auto-scout | LVOT + aortic valve | BH |
| 9 | `flow_150_tp_retro_bh_ao` | Through-plane | ⟂ ascending aorta, just above the sinotubular junction | Ascending aorta cross-section | BH |

### Phase 2 — Mapping

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 10 | `t1_map_sax` (native) | SAX ×3 | SAB/SAM/SAA — placed on the SA localizer (#4), systolic-phase reference (see cardiac_stress #11 slice placement) | Basal, mid, apical SAX | BH |
| 11 | `t2_map_trufisp_sax` | SAX ×3 | Copy Slice from #10 | Basal, mid, apical SAX | BH |

### Phase 3 — Contrast

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Contrast — 2 ml/s** | — | Single gadolinium dose at 2 ml/s [Confirm dose] + saline flush. No perfusion run, so no first-pass timing | — | — |
| — | **7 min wait** | — | LGE imaging starts ~7 min after the injection | — | — |

### Phase 4 — Post-Contrast Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 12 | `cine_tfi_retro_sa_volumetry_c` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |

### Phase 5 — LGE

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 13 | `ti_scout` | SAX single | Single SA location at the thickest myocardium (mid-ventricular) | Single mid SAX slice | BH |
| 14 | `de_overview_tfi_4c` | 4C | Copy Slice from #6 — prospective gating, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 15 | `de_overview_tfi_2c` | 2C | Copy Slice from #7 — prospective gating, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 16 | `de_overview_tfi_sax` | SAX stack | Copy Slice from #12 — prospective gating, TI increased gradually | Entire myocardium wall — whole LV | BH |
| 17 | `de_trufi_overview_12sl_psir_fb` | SAX ×12 | Copy Slice from #12 — 12 slices | Base → apex | FB |
| 18 | `tfl13_2d_t1_seg_fs_sax` | SAX stack (2D) | Copy Slice from #12 — [Confirm: routine or optional] | Base → apex, built slice-by-slice upward toward the apex | BH |

---

## 4. Sequence Rationale

### Core Strategy

The non-stress study answers the structural questions: **function** (EF, volumes, wall motion), **valve and aortic flow**, and the tissue itself. Every indication in this protocol asks the same underlying question: **is there edema, fibrosis, infiltration, or scar — and is it acute or chronic?**

- **Edema** (free water) — the acute injury signature
- **Fibrosis** (diffuse or focal) — the chronic/reparative signature
- **Infiltration** (amyloid, iron, fat) — material that shouldn't be there
- **Scar/necrosis** (focal dead myocardium)

It asks no ischemia question — no adenosine, no perfusion, no stress T1. The pairing of native T1 + T2 + LGE is the instrument that reads those four tissue states and separates acute from chronic.

### When to use this protocol vs cardiac_stress

**Choose cardiac_stress (adenosine) when the patient is being evaluated for ischemia:**

1. **Chest pain — suspected ischemia** — typical/atypical chest pain with an equivocal prior test, or clean coronaries with ongoing symptoms (INOCA / microvascular): is there ischemia? The T1-reactivity + perfusion combination covers the microvascular end of the question.
2. **Borderline stenoses on CTA/angio** — the anatomy is known; is the lesion functionally significant? Perfusion answers.
3. **Ischemic muscle assessment — new-onset HF / viability** — is the failing ventricle ischemic? Perfusion defect without scar = hibernating (revascularize); matching scar = infarcted (irreversible). Perfusion + LGE answer both.
4. **Eligibility gate** — the patient must be stable: no acute infarction, unstable angina, or active myocarditis; no severe asthma/COPD, no high-grade AV block, no significant hypotension

**Choose this non-stress protocol when the question is the myocardium itself, or the patient cannot be stressed:**

1. **Acute chest pain with troponin rise and clean coronaries (MINOCA-type)** — tells the causes apart: scar in a coronary territory = infarct; edema with subepicardial scar = myocarditis; edema with no matching scar = Tako-tsubo. Suspected myocarditis presenting this way (viral prodrome, younger patient) is the same scenario.
2. **Myocarditis follow-up** — is edema still present (active inflammation), or has it been replaced by fibrosis (healed)?
3. **Cardiomyopathy / heart failure aetiology** — an echo finding or new heart failure, same question: what disease is behind this muscle? Echo shows only the shape (thick / dilated / stiff); the fibrosis pattern and infiltration reveal the disease — which is also why the muscle fails.
4. **Transplant / cardiotoxicity surveillance** — the same surveillance question: repeat scans compared against baseline, looking for diffuse tissue change before function falls — rejection shows as edema, cardiotoxicity as early fibrosis.
5. **Stress-contraindication catch-all** — post-infarct (LGE shows the infarct and its territory, cine gives function), valve/flow, or a pure function check — LGE + cine suffice and mapping is optional.

**The decision in one line:** ischemic question in a stable patient → stress; tissue question, suspected acute inflammation/edema, or stress contraindication → non-stress. The myocardium itself draws the same line: an acute or unstable myocardium — edema its tissue signature — is a contraindication to stress. And if a stress study's pre-adenosine native T1 comes back globally elevated (the edema fingerprint), pause and reconsider before stressing.

### How this differs from cardiac_stress

**The same exam minus the stress arm:** no adenosine, no BP choreography, no perfusion family, no stress T1 map; the contrast simplifies to one injection at 2 ml/s; the function and LGE blocks are identical to cardiac_stress.

**The tissue instrument — how T1, T2 and LGE separate the four tissue states:** in cardiac_stress the T1 map serves reactivity (a flow measurement). Here the mapping pair + LGE work as three channels that read the Core Strategy's four states — and the discrimination lives in the combinations:
- **Edema** — free water lengthens T2, so the T2 map is the water channel. Water also lengthens T1, which is why T1 alone is ambiguous.
- **Fibrosis** — the expanded collagen interstitium lengthens T1 while T2 stays normal: T1↑ + T2 normal = fibrosis; T1↑ + T2↑ = edema. The pairing separates chronic from acute.
- **Infiltration** — the direction of T1 plus the LGE pattern names the infiltrate: amyloid = markedly high T1 + diffuse LGE; iron = shortened T1; Fabry fat = low T1.
- **Scar/necrosis** — LGE shows focal bright scar against nulled normal myocardium; the distribution (coronary territory vs non-coronary) separates ischemic from non-ischemic disease.

**When the maps matter — and when they don't:** the maps are the essential tool whenever the answer is diffuse or pre-functional — edema, diffuse fibrosis, or infiltration are LGE-negative or non-diagnostic, so the maps are the test itself. When the question is focal (scar in a territory) or purely functional (EF, valve), LGE + cine alone answer it and mapping is optional. That is why the maps are per-radiologist choice rather than default.

### Phase 0 — Surveys & Localizers (#1–#4) — the planning stage

This phase is the **planning** — every later plane derives from it. Full planning-stage description, refer to: `cardiac_stress.md`.

**`t2_trufi_tra_thorax_bh` (#1):** the axial planning localizer, heart-only coverage — the start of all planning. (No coronal scout in this protocol.)

**The pseudo-cascade (#2–#4)** — each localizer is a single-slice approximation planned from the previous one. The cascade ends at the pseudo-SAX (#4), which shows the true short-axis geometry — the true cine long axes (3C/4C/2C) are then planned back from it (Phase 1):

1. **Axial → pseudo 2C (#2):** single slice along the LV long axis — through the apex and the mitral valve centre.
2. **Pseudo 2C → pseudo 4C (#3):** plane ⟂ to it — through the apex and the mitral valve centre, on to the tricuspid valve.
3. **Pseudo 4C → SA localizer (#4):** stack **⟂ interventricular septum, ∥ mitral valve plane** — base → apex, basal coverage including the **left atrium** (for the 3C).

### Phase 1 — Cine Function & Flow (#5–#9)

Identical sequences and planning to `cardiac_stress.md` #6–#10 — retrospective gating, planned back from the SA localizer:

- **`cine_tfi_retro_3c` (#5):** bisects LV + outflow tract. Shows the LVOT view — aortic valve motion, AS/AR (aortic stenosis/aortic regurgitation) jets, anteroseptal/inferolateral walls.
- **`cine_tfi_retro_4c` (#6):** through the RV angle + LV centre (avoid the aorta on other SA slices). Shows all four chambers — global function, both AV valves, septal/lateral wall motion.
- **`cine_tfi_retro_2c` (#7):** bisects LV, ∥ septum insertion line. Shows LV + LA — anterior/posterior wall motion, mitral valve.
- **`cine_tfi_retro_lvot_noscout` (#8):** ⟂ the 3C, through and bisecting the LVOT, no auto-scout. The orthogonal outflow-tract view.
- **`flow_150_tp_retro_bh_ao` (#9):** through-plane phase-contrast ⟂ ascending aorta just above the sinotubular junction (check on-end in both AO views), VENC 150 — forward volume, regurgitant fraction, stroke volume. Aliasing → repeat at VENC 400. (Full phase-contrast mechanics in cardiac_stress #10.)

### Phase 2 — Mapping (#10–#11)

**`t1_map_sax` (#10) — native T1 map:** three SAX slices (SAB/SAM/SAA), breath-held MOLLI.

- **How it is measured (MOLLI):** a 180° inversion pulse flips all magnetization upside-down; single-shot TrueFISP images are then acquired at successive inversion times (one per heartbeat, same cardiac phase, motion-corrected), each catching the recovery curve at a different point; a pixel-wise fit of the exponential recovery returns the T1 value for that pixel. The result is a **map** — an image where every pixel's value *is* the T1 in milliseconds: quantitative and comparable against published normal ranges, unlike a T1-weighted image where "dark" only means "darker than its neighbour".

- **Why T1 is relevant in the non-stress cardiac study:** every tissue has a characteristic T1, and it changes with composition — more interstitial water or fibrosis lengthens T1; fat or iron shortens it.
    - **It puts a number on the myocardium itself.** Cine and LGE show structure and focal scar; native T1 quantifies the tissue composition — a reproducible, scanner-comparable value in ms, which makes it the tool for following disease over time (therapy response in amyloid, resolution of inflammation in myocarditis, cardiotoxicity surveillance).
    - **It detects diffuse disease that LGE cannot.** LGE depends on contrast between focal scar and nulled *normal* myocardium — diffuse fibrosis elevates T1 everywhere, removes the normal reference, and the LGE image looks unremarkable while the native T1 map shows a global rise. This is exactly the question the non-stress study is built for: early cardiomyopathy, transplant rejection, post-infarct remote remodelling.
    - **The diagnostic values:** elevated T1 → fibrosis, edema, amyloid (markedly high); shortened T1 → iron overload, fat.
    - **It anchors the characterisation triangle.** Read together with T2 and LGE: T1↑ + T2 normal = fibrosis; T1↑ + T2↑ = edema (acute injury); focal LGE pattern = scar, diffuse T1 rise without focal LGE = non-ischemic diffuse disease.
- **How this differs from the stress protocol's T1:** in cardiac_stress, T1 mapping serves **reactivity** — the stress − native T1 difference measures how much myocardial blood volume rises under adenosine vasodilation, a microvascular function test. Here there is no stress map and no reactivity question: the single native map is the characterisation measurement itself — the tissue state against which the T2 map and LGE are interpreted.

**The B(R)A sampling scheme — why "before" and "after" images:** T1 mapping schemes are written as image blocks around a recovery pause — **B(R)A** = B images acquired in consecutive heartbeats **B**efore the pause, R **R**ecovery heartbeats without imaging, then A images **A**fter the pause (this protocol: 5(6)3).

    - **The recovery curve is only informative where it is steep.** After the inversion, the early, fast-changing part of the exponential is where tissues with different T1 separate; the flat late part adds almost nothing. With one image per heartbeat, a single inversion yields only a handful of early samples before the useful part is over.
    - **The pause exists to buy a second curve.** Rather than sample one curve's flat tail, the R-beat pause lets the magnetization partially recover, and the second inversion provides a fresh early segment — the A block. B and A are therefore the useful parts of **two different curves** stitched together, roughly doubling the informative samples without lengthening the acquisition.
    - **The Modified Look-Locker correction.** Inversion 2 starts from partially recovered magnetization (not the clean −M0 of inversion 1), so the fit treats that starting level as an unknown parameter — the "Modified" in MOLLI.
    - **R tracks the heart rate.** The pause must deliver a certain amount of recovery, which progresses in absolute time but is counted in heartbeats — at shorter RR each beat gives less recovery time, so more beats are needed (6 here vs the classic 3).
    - **Why this shape at all:** the whole scheme (~11 heartbeats) fits in one breath-hold — two short curves beat one long one.
    - **Scheme selection by RR interval:** R grows one beat per 100 ms of RR shortening:

    | RR interval | Scheme |
    |---|---|
    | 1000 ms | 5(3)3 |
    | 900 ms | 5(4)3 |
    | 800 ms | 5(5)3 |
    | 700 ms | 5(6)3 |
    | 600 ms | 5(7)3 |

**`t2_map_trufisp_sax` (#11) — T2 map:** three SAX slices, copy #10, breath-held.

- **How it is measured:** a series of single-shot TrueFISP images, each acquired after a different T2-preparation time; a pixel-wise fit of the exponential T2 decay returns the T2 value for each pixel. The result is a **map** — every pixel's value *is* the T2 in milliseconds, quantitative and comparable against published normal ranges. (The preparation module itself is explained below.)
- **Why T2 is relevant in the non-stress cardiac study:** every tissue has a characteristic T2, and it changes with composition — free water lengthens it.
    - **T2 is the edema marker.** Edema means free water, and free water means long T2. Elevated myocardial T2 flags acute infarction (edema precedes scar formation), myocarditis, Tako-tsubo cardiomyopathy, and transplant rejection.
    - **It separates acute from chronic — the pairing with T1.** Fibrosis and edema both lengthen T1, so T1 alone cannot tell them apart; T2 isolates the water. **T1↑ + T2↑ = edema (acute injury); T1↑ + T2 normal = fibrosis (chronic).** This is what distinguishes active from healed myocarditis and recent from old infarction.
    - **Quantitative follow-up:** T2 normalizes as edema resolves — a measurable marker of recovery.
- **No stress counterpart:** T2 mapping exists only in this protocol — the stress study carries no edema marker; this sequence is what the non-stress study adds to the characterisation triangle.

**The T2-prep module:** T2 decay happens in the transverse plane, so the preparation must move the magnetization there, wait, and store the result back — unlike an inversion pulse, which only starts longitudinal T1 recovery.
    - **The module, step by step:** a 90° pulse tips the magnetization into the transverse plane → it is left to decay for the chosen **T2-preparation time** (TE) — water-rich tissue decays slowly, fibrotic/iron-rich tissue decays fast — with a 180° refocusing pulse mid-wait protecting against field inhomogeneity → a final 90° stores the surviving magnetization back onto the longitudinal axis, stamped with the T2 decay.
    - **One TE per heartbeat:** each heartbeat runs one T2-prep at one TE followed by the single-shot TrueFISP readout; repeating at several TEs samples the decay curve, and the pixel-wise exponential fit returns T2.
    - **How it differs from MOLLI (T1):** the decisive difference is the timescale of the two curves. Myocardial T1 is ≈ 1000–1100 ms, so recovery spans seconds — several heartbeats — and MOLLI samples **along one curve**: one inversion, and each consecutive heartbeat is a later time point of the same still-recovering curve. Myocardial T2 is ≈ 40–50 ms, so the transverse signal is gone in ~200 ms — within a single heartbeat — and T2 mapping samples **across many curves**: each beat runs a fresh T2-prep and takes one sample from its own decay at its own TE. Both take one measurement per beat — the difference is whether consecutive beats ride one curve or rebuild it.

### Phase 3 — Contrast

A single gadolinium dose at **2 ml/s** + saline flush. The slow rate is intentional: with no first-pass perfusion to capture, there is no benefit to a tight 4 ml/s bolus — the dose only needs to reach LGE equilibrium, and the gentler injection is kinder to the vein. After the injection, the **7-minute wait** allows the contrast to equilibrate between blood and the myocardial extracellular space — the same LGE physiology as cardiac_stress.

### Phase 4 — Post-Contrast Function (#12)

**`cine_tfi_retro_sa_volumetry_c` (#12) — SA volumetry:** identical to `cardiac_stress.md` #16 — diastolic-phase planning, contiguous stack from beyond the apex (no blood pool) to past the mitral valve level, filling the 7-minute wait. EF via modified Simpson's disk summation: EDV, ESV, EF = (EDV − ESV)/EDV, mass from epicardial contours.

### Phase 5 — LGE (#13–#18)

Identical LGE block to `cardiac_stress.md` #17–#22:

**Why infarcted myocardium enhances late:** after the 7-minute wait, the gadolinium has equilibrated in the extracellular space. Infarct and fibrosis replace myocytes with an expanded extracellular matrix, so contrast accumulates there and washes out slowly — the scar keeps a short T1 and stays **bright** on the inversion-recovery image, while normal myocardium nulls **dark** at the chosen TI. LGE is therefore a map of expanded extracellular space wherever it is focal.

- **`ti_scout` (#13):** at the 7-min mark, single SA at the thickest myocardium. Optimal TI = normal myocardium most uniformly dark without a dark rim (blood pool nulling + interface partial volume — see cardiac_stress #17).
- **DE overviews — `de_overview_tfi_4c` (#14), `de_overview_tfi_2c` (#15), `de_overview_tfi_sax` (#16):** IR-TrueFISP (magnitude IR), prospective gating, entire myocardial wall; TI increased gradually across the series as contrast washes out.
- **`de_trufi_overview_12sl_psir_fb` (#17):** 12-slice PSIR free-breathing overview — TI-insensitive catch-all (RV, thrombus, any territory).
- **`tfl13_2d_t1_seg_fs_sax` (#18):** the high-res segmented 2D T1 TurboFLASH FS SAX — the equivalent of `de_high-res_tfl_fs_sax` in cardiac_stress: built slice-by-slice upward toward the apex, fat saturation unmasks thin subepicardial enhancement, high resolution measures transmurality — a GRE readout free of the SSFP dark-rim/banding artifacts of the TrueFISP overviews. [Confirm: routine here or optional after radiologist review as in the stress protocol.]

---

## 5. Variations

**Arrhythmia / poor breath-hold — real-time cine fallback:** the real-time cine is a rescue for the **retrospective-gated cine sequences only** — the mapping and LGE sequences remain gated and have no substitution.
    - **What to swap:** replace the gated cines one-for-one with their real-time (ungated) counterparts, same planes and coverage, no other parameter changes — the lower resolution is inherent to the sequence:
        - `cine_tfi_retro_3c` → `cine_trufi_cs_rt_adapt_3C`
        - `cine_tfi_retro_4c` → `cine_trufi_cs_rt_adapt_4C`
        - `cine_tfi_retro_2c` → `cine_trufi_cs_rt_adapt_2C`
        - `cine_tfi_retro_lvot_noscout` → `cine_trufi_cs_rt_adapt_LVOT`
        - `cine_tfi_retro_sa_volumetry_c` → `cine_trufi_cs_rt_adapt_SA_volumetry`
    - **Why:** retrospective gating sorts data into cardiac phases by RR — an irregular rhythm (e.g. atrial fibrillation) mis-sorts beats and produces blur, dropped phases, and reconstruction gaps. Real-time cine ignores the ECG and images continuously, so it is immune to arrhythmia and tolerates free breathing or short holds.
    - **The cost:** each real-time frame must carry its entire k-space in one shot, so spatial and temporal resolution are lower than the pooled multi-beat gated cine — function, EF, and wall motion stay diagnostic; fine valvular detail suffers.
    - **What it does not rescue:** the T1/T2 maps (the B(R)A sampling assumes a stable RR) and the aortic flow (also retrospectively gated) — note these limitations in the report.

**Suspected myocarditis**
- Add edema imaging — **T2 mapping (preferred, quantitative)** or a T2 STIR SAX stack (traditional) — and extend the FS LGE to 2C/4C high-res — oedema + subepicardial enhancement pattern is the myocarditis signature. What sequence to add is per radiologist choice — T1/T2 mapping are not necessarily default.

**Suspected aortic stenosis / high-velocity jet**
- Repeat the flow sequence at VENC 400 cm/s — 150 cm/s aliases at stenotic velocities.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | Choose the ECG lead with the cleanest R wave (largest amplitude, no T-wave oversensing) — every sequence is gated, so a poor trigger degrades the entire study |
| **eGFR** — confirmed above 30 before contrast? | Single-dose protocol but still gadolinium — check before, not after |
| **Breath-hold consistency** — same small end-inspiratory position on T1/T2 maps? | Slice drift between the maps breaks the T1/T2/LGE comparison |
| **VENC** — any aliasing in the aortic flow? | Aliased phase wraps velocities — repeat at higher VENC (400 cm/s) |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **TI correctness** — normal myocardium dark on the DE and high-res series? | The nulling TI sits around ~300 ms — verify it on the DE and high-res images, not just at the scout. If the myocardium looks bright (nulling off) or the delay has shifted, re-scout and re-measure rather than adjusting blindly |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 2.0 | 2026-09-01 | — | Major refinement — DE overviews corrected to IR-TrueFISP magnitude (`de_overview_tfi_*`); high-res noted as the GRE artifact-clean readout |
| 1.0 | 2026-08-29 | — | Initial build — 18 workflow steps. TrueFISP axial localizer + pseudo-localizer cascade + retro cine (3C/4C/2C/LVOT) + aortic flow VENC 150 + native T1 map + T2 map (TrueFISP) + single-dose contrast (2 ml/s) + SA volumetry + TI scout + DE overviews (4C/2C/SAX/PSIR FB) + T1 seg FS SA high-res. Rest CMR — no stress arm |
