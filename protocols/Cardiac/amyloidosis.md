# Amyloidosis / Fabry (Infiltrative Cardiomyopathy CMR — T1/T2 Mapping, ECV + LGE)

**Version:** 1.0 | **Date:** 2026-09-01 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

Same as `cardiac_non-stress.md`:

- **Position:** Supine, head-first. Heart centred over the coil.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly. ECG leads on the anterior chest wall, clear of the coil elements.
- **Laser Landmark:** Mid-sternum at heart level.
- **ECG:** Vector ECG — optimise the R wave (largest amplitude, no T-wave oversensing). Every sequence in this protocol is ECG-gated, so a poor trigger degrades the entire study.
- **IV Access:** **One line** — contrast only.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — consistency matters most: the T1/T2 maps and the ECV slices must not drift between acquisitions.
- **eGFR check:** Gadolinium — confirm eGFR above 30 before the protocol [Confirm threshold].
- **Hematocrit:** a same-day blood hematocrit is required for the ECV calculation — draw it at cannulation and enter it into the ECV post-processing [AI ADDED].

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–4)
- **Phase 1 — Rest function:** Cines 3C/4C/2C/LVOT + aortic flow (#5–9)
- **Phase 2 — Mapping:** Native T1 map + T2 map (#10–11)
- **Phase 3 — Contrast:** Single dose at 2 ml/s → 7 min wait
- **Phase 4 — Function:** SA volumetry fills the 7-min wait (#12)
- **Phase 5 — LGE:** TI scout → PSIR overviews → 12-slice FB → T1 seg FS SA (#13–18)
- **Phase 6 — ECV:** Post-contrast T1 map at the same three slices (#19)

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Phase 3 | Gadolinium — single dose [Confirm mmol/kg] | 2 ml/s | LGE equilibration + ECV post-contrast T1 |

**Total contrast: single dose** [Confirm]. Slow rate is deliberate: no first-pass perfusion here, so no tight 4 ml/s bolus is needed.

---

## 3. Imaging Series

### Phase 0 — Surveys & Localizers

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 1 | `t2_trufi_tra_thorax_bh` | Axial | True axial | Heart only — no aortic arch. The axial planning localizer | BH (end-insp) |
| 2 | `trufi_2c_ipat` | Pseudo 2C | Single slice through LV apex + mitral valve centre — planned on #1 | LV + LA — apex → mitral annulus | BH |
| 3 | `trufi_4c_ipat` | Pseudo 4C | Single slice ⟂ pseudo-2C through apex + both AV valves — planned on #2 | All 4 chambers | BH |
| 4 | `trufi_shortaxis_ipat` | Pseudo SAX | ⟂ interventricular septum, ∥ mitral valve plane — planned on #3 | Base → apex, extending basally to include the left atrium (for 3C planning) | BH |

### Phase 1 — Rest Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 5 | `cine_tf2d13_retro_3c` | 3C (LVOT) | Bisects LV + outflow tract — planned on SA (#4) | LV, LA, LVOT, aortic root | BH |
| 6 | `cine_tf2d13_retro_4c` | 4C | Through RV angle + LV centre — planned on SA (#4) | All 4 chambers | BH |
| 7 | `cine_tf2d13_retro_2c` | 2C | Bisects LV, ∥ septum insertion line — planned on SA (#4) | LV + LA | BH |
| 8 | `cine_tf2d13_retro_lvot_noscout` | LVOT | ⟂ 3C view, through and bisecting the LVOT — planned on #5. No auto-scout | LVOT + aortic valve | BH |
| 9 | `flow_150_tp_retro_bh_epat_ao` | Through-plane | ⟂ ascending aorta, just above the sinotubular junction | Ascending aorta cross-section | BH |

### Phase 2 — Mapping

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 10 | `t1_map_sax` (native) | SAX ×3 | SAB/SAM/SAA — placed on the SA localizer (#4), systolic-phase reference. Decision: MOLLI scheme 5(_)3 per RR (see cardiac_non-stress B(R)A scheme table) | Basal, mid, apical SAX | BH |
| 11 | `t2_map_trufisp_sax` | SAX ×3 | Copy Slice from #10 | Basal, mid, apical SAX | BH |

### Phase 3 — Contrast

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Contrast — 2 ml/s** | — | Single gadolinium dose at 2 ml/s [Confirm dose] + saline flush | — | — |
| — | **7 min wait** | — | Late LGE imaging starts ~7 min after the injection | — | — |

### Phase 4 — Post-Contrast Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 12 | `cine_tf2d13_retro_sa_volumetry_c` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |

### Phase 5 — LGE

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 13 | `ti_scout` | SAX single | Single SA location at the thickest myocardium (mid-ventricular) | Single mid SAX slice | BH |
| 14 | `de_overview_tfi_psir_4c` | 4C | Copy Slice from #6 — late PSIR, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 15 | `de_overview_tfi_psir_2c` | 2C | Copy Slice from #7 — late PSIR, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 16 | `de_overview_tfi_psir_sax` | SAX stack | Copy Slice from #12 — late PSIR, TI increased gradually | Entire myocardium wall — whole LV | BH |
| 17 | `de_trufi_overview_12sl_psir_fb` | SAX ×12 | Copy Slice from #12 — 12 slices | Base → apex | FB |
| 18 | `tfl13_2d_t1_seg_fs_c_sax` | SAX stack (2D) | Copy Slice from #12 — [Confirm: routine or optional] | Base → apex, built slice-by-slice upward toward the apex | BH |

### Phase 6 — ECV

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 19 | `t1_map_shortt1_c_sax` | SAX ×3 | Copy Slice from #10 — **post-contrast T1 map** for the ECV measurement. Short-T1 scheme (post-Gd myocardial T1 is ~350–500 ms) [Confirm timing ~10–15 min post contrast] | Basal, mid, apical SAX | BH |

---

## 4. Sequence Rationale

### Core Strategy

The infiltrative-disease exam: **which material is in the myocardium?** Two diseases, one question — amyloid deposits **interstitial protein** into the extracellular space, Fabry stores **glycosphingolipid inside the myocytes**. The tissue instrument answers by *direction*: amyloid drives native T1 and ECV dramatically **up** (interstitial expansion), Fabry drives native T1 **down** (intracellular fat-like storage) while ECV stays normal. The same three channels — T1, ECV, LGE pattern — both diagnose and separate the two diseases, and ECV doubles as the quantitative monitoring metric for therapy response.

### The two diseases — and how they change the tissue the MRI reads

**Amyloidosis** is misfolded protein deposition (AL light-chain or ATTR transthyretin) that fills the extracellular interstitium of the myocardium. The interstitium swells with protein fibrils and their associated water, and the walls thicken and stiffen around it — myocytes are progressively strangled and lost. What this does to the measurable tissue properties: the expanded extracellular space lengthens native T1 to values among the highest of any cardiac disease; ECV, which quantifies exactly that extracellular fraction, rises dramatically; after gadolinium, the enlarged interstitium acts as a large distribution volume that retains contrast; and T2 stays near normal, because this is chronic deposition without free edema. Clinically the same stiffness shows up as restrictive physiology — preserved EF, a small cavity, and dilated atria.

**Fabry disease** is different in kind: an X-linked deficiency of α-galactosidase A leaves glycosphingolipid accumulating *inside* the myocytes. The stored material is lipid-like, and fat is the tissue with the shortest T1 — so intracellular storage drags native T1 *down*, the opposite direction to amyloid and almost every other myocardial disease. The interstitium is untouched, so ECV stays normal, and T2 is likewise unremarkable. Over time the lipid-laden myocytes die and are replaced by focal fibrosis — the source of the characteristic focal enhancement (Phase 5). Clinically the myocyte swelling mimics hypertrophy, which is why Fabry presents as an HCM lookalike.

### When to use this protocol

**Suspected amyloidosis — and why each referral clue points to amyloid:**
    - **Thick walls with low-voltage ECG** — the discordance that gives amyloid away: true hypertrophy (HCM, hypertensive) generates *large* QRS voltages, but amyloid thickens the wall with electrically inert protein that separates the myocytes — so the voltage paradoxically drops as the wall thickens.
    - **HFpEF / unexplained diastolic dysfunction** — the stiff, protein-filled interstitium resists filling; restrictive physiology with preserved EF is the amyloid functional phenotype.
    - **Carpal tunnel syndrome** — amyloid deposits in the flexor retinaculum compress the median nerve, often years before the heart is involved — a systemic deposition clue (especially ATTR).

**Suspected Fabry disease — and why each clue points to Fabry:**
    - **Unexplained hypertrophy** — the storage-swollen myocytes mimic HCM; when hypertrophy appears without hypertension, aortic stenosis, or a sarcomeric HCM family history, a storage disease enters the differential — and HCM-phenotype men without sarcomere mutations should be screened for Fabry.
    - **Family history** — X-linked inheritance: affected men, variably affected female carriers.
    - **Renal disease** — glycosphingolipid deposits in the kidneys cause proteinuria and progressive CKD — a systemic storage clue.

**Disease monitoring — serial native T1 and ECV track the disease load itself:**
    - Fabry: enzyme replacement therapy supplies the missing enzyme, so the stored glycosphingolipid is broken down and cleared — as the intracellular lipid-like material disappears, native T1 rises back toward normal. Serial native T1 therefore shows whether the storage is clearing.
    - Amyloid: AL chemotherapy (or ATTR-directed therapy) stops the fibril production and allows the deposits to regress — as the interstitium empties, the extracellular space contracts and ECV falls back toward normal. Serial ECV therefore shows whether the interstitium is emptying.

### How this differs from cardiac_non-stress

- **The ECV measurement is added (#19):** a post-contrast T1 map at the same three slices, paired with the native map — ECV quantifies the extracellular volume fraction directly. Amyloid fills the interstitium, so ECV is markedly elevated (the single best amyloid biomarker and monitoring metric); Fabry stores intracellularly, so ECV stays normal. This one measurement is what this protocol exists for.
- **No edema stack, no early enhancement:** amyloid and Fabry are chronic infiltrative processes — there is no acute inflammation question, so the TIRM stack and the EGE block of the myocarditis protocol are absent.
- **The native T1 read is directional:** in the general non-stress study, elevated T1 means "some disease, identify it"; here the *direction* is diagnostic — amyloid is among the highest native T1 of any cardiac disease, Fabry is *shortened* (fat-like storage). The same sequence separates the two diagnoses before LGE is even looked at.
- **The LGE patterns type the disease:** amyloid shows diffuse circumferential subendocardial enhancement; Fabry shows the focal mid-basal inferolateral pattern — the imaging detail lives in the Phase 5 rationale.
- **Otherwise identical:** function, flow, volumetry, and the LGE block are the same sequences and planning as cardiac_non-stress (PSIR overviews as in myocarditis).

### Phase 0 — Surveys & Localizers (#1–#4) — the planning stage

Same planning cascade as `cardiac_non-stress.md` Phase 0 (the localizers here run with iPAT): axial localizer (#1) → pseudo 2C (#2) → pseudo 4C (#3) → SA localizer (#4), prescribed perpendicular to the interventricular septum and parallel to the mitral valve plane, with coverage extending basally to include the left atrium.

### Phase 1 — Cine Function & Flow (#5–#9)

Identical to `cardiac_non-stress.md` #5–#9 — retrospective gating, planned back from the SA localizer; the flow sequence runs with ePAT acceleration. 
- **`cine_tf2d13_retro_3c` (#5):** bisects LV + outflow tract — the LVOT view: aortic valve motion, AS/AR (aortic stenosis/aortic regurgitation) jets, anteroseptal/inferolateral walls.
- **`cine_tf2d13_retro_4c` (#6):** through the RV angle + LV centre (avoid the aorta on other SA slices) — all four chambers, global function, septal/lateral wall motion.
- **`cine_tf2d13_retro_2c` (#7):** bisects LV, ∥ septum insertion line — LV + LA, anterior/posterior wall motion, mitral valve.
- **`cine_tf2d13_retro_lvot_noscout` (#8):** ⟂ the 3C through and bisecting the LVOT, no auto-scout — the orthogonal outflow-tract view.
- **`flow_150_tp_retro_bh_epat_ao` (#9):** through-plane phase-contrast ⟂ ascending aorta just above the sinotubular junction (on-end in both AO views), VENC 150 — forward volume, regurgitant fraction, stroke volume. Aliasing → repeat at VENC 400. (Phase-contrast mechanics: `cardiac_stress.md` #10.)

### Phase 2 — Mapping (#10–#11)

**`t1_map_sax` (#10) — native T1 map:** same MOLLI acquisition as `cardiac_non-stress.md` #10 (B(R)A scheme and the mechanism explained there). In this protocol the native T1 is the **first diagnostic answer**: amyloid = markedly elevated T1 (interstitial protein — among the highest values of any cardiac disease); Fabry = **shortened** T1 (intracellular glycosphingolipid storage, fat-like). The direction of the map separates the two diseases before any contrast is given.

**`t2_map_trufisp_sax` (#11) — T2 map:** same as `cardiac_non-stress.md` #11. Here its role is supporting rather than central — these are chronic diseases with no significant edema; a normal T2 with a grossly abnormal T1 reinforces the infiltrative read (acute inflammation would raise both).

### Phase 3 — Contrast

A single gadolinium dose at **2 ml/s** + saline flush — no first-pass to capture, so no tight bolus is needed. After the injection, the **7-minute wait** allows the contrast to equilibrate for LGE — and the same dose later serves the ECV post-contrast T1 measurement.

### Phase 4 — Post-Contrast Function (#12)

**`cine_tf2d13_retro_sa_volumetry_c` (#12) — SA volumetry:** identical to `cardiac_non-stress.md` #12 — diastolic planning, contiguous stack beyond the apex to past the mitral valve level, filling the 7-minute wait; EF via modified Simpson's disk summation. In amyloid the thickened, stiffened ventricle characteristically shows preserved EF with a small cavity — the function read pairs with the tissue read.

### Phase 5 — LGE (#13–#18)

Same late LGE block as `myocarditis.md` #18–#23 — PSIR overviews, TI scout, 12-slice FB catch-all, and the TurboFLASH FS high-res (mechanics and PSIR rationale as in those files).

**Why the enhancement matters here:** amyloid infiltrates diffusely — the classic picture is **circumferential subendocardial enhancement** (sometimes transmural) with a **notoriously difficult null**: amyloid myocardium and the blood pool carry similar T1 after contrast, so the TI scout must separate two tissues that null almost together. PSIR's TI-insensitivity is exactly what this disease needs; the magnitude high-res series may be hard to null and is used with the incrementing TI. Fabry shows the opposite pattern: **focal mid-basal inferolateral enhancement** — replacement fibrosis where the storage-laden myocytes have died. Why this territory fails first is not fully settled, but the basal inferolateral wall carries the highest wall stress, and the glycosphingolipid also deposits in the intramural vessel endothelium — together making the storage-injured myocytes there the first to scar. The result is a focal non-ischemic mid-wall scar, easy to null, and the 4C/2C views catch it in-plane.

### Phase 6 — ECV (#19)

**`t1_map_shortt1_c_sax` (#19) — post-contrast T1 map (ECV measurement):** the defining addition of this protocol.

- **What ECV is:** the extracellular volume fraction — how much of the myocardium is extracellular space (normal ~25%; the rest is myocytes). It is measured with gadolinium because gadolinium is an *extracellular* agent: it cannot enter intact cells, so the amount a tissue absorbs at equilibrium is proportional to its extracellular volume. The formula **ECV = (1 − hematocrit) × (ΔR1_myocardium / ΔR1_blood)** compares the myocardium's uptake to blood's: ΔR1 (the change in relaxation rate, 1/T1_post − 1/T1_native) is proportional to local gadolinium concentration, and blood's own extracellular fraction is its plasma, (1 − hematocrit). Because the formula is a *ratio*, the contrast dose, clearance rate, and timing cancel out — the value is robust and comparable across scanners and centers.
- **How it is measured:** the same three slices (SAB/SAM/SAA) are re-mapped after contrast with a **short-T1 scheme** — post-gadolinium myocardial T1 drops to ~350–500 ms, so the MOLLI sampling pattern is compressed to match the shorter T1 (hence `ShortT1`). The blood pool T1 is read from an ROI in the LV cavity on the same slices, so myocardium and blood share the same gadolinium history; the same-day hematocrit (drawn at cannulation) is entered into the calculation. The post-contrast map must copy the native geometry exactly, so each voxel's ΔR1 is computed on the same myocardium.
- **What it detects:** extracellular expansion. Amyloid fills the interstitium with protein — **ECV rises dramatically** (often 40–60%+ against a normal ~25%), making it the single best amyloid biomarker and the metric used to track therapy response. Fabry's storage is *intracellular*, so **ECV stays normal** — the native-T1 direction and the ECV together separate the two diseases completely.
- **Why it runs last:** the post-contrast T1 needs the contrast to have equilibrated — the measurement sits after the LGE block, ~10–15 min post injection [Confirm timing]. If the hematocrit was not drawn, ECV cannot be computed — flag it at the start, not the end.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | Choose the ECG lead with the cleanest R wave (largest amplitude, no T-wave oversensing) — every sequence is gated, so a poor trigger degrades the entire study |
| **eGFR** — confirmed above 30 before contrast? | Single-dose protocol but still gadolinium — check before, not after |
| **Hematocrit** — same-day sample drawn and entered for the ECV calculation? | Without the hematocrit, ECV cannot be computed — draw it at cannulation, not after the scan |
| **VENC** — any aliasing in the aortic flow? | Aliased phase wraps velocities — repeat at higher VENC (400 cm/s) |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |
| **Amyloid nulling** — myocardium and blood separable at the TI scout? | In amyloid the two null almost together — if the scout cannot separate them, rely on the PSIR overviews and re-scout as washout progresses |
| **Breath-hold consistency** — same small end-inspiratory position on the maps? | ECV is computed voxel-by-voxel: each pixel pairs its own native and post-contrast T1 — if the breath-hold position drifts between the maps, T1 values from different tissue get paired and the ECV map turns to noise |
| **ECV timing** — post-contrast T1 map acquired at the equilibrium timing? | Too early and the T1 is still drifting — the ECV value shifts with the delay [Confirm timing] |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-01 | — | Initial build — 19 workflow steps. Non-stress base (localizers + retro cines + flow ePAT + native T1 + T2 map + volumetry + PSIR LGE block) with the ECV measurement added (post-contrast short-T1 map at SAB/SAM/SAA) and the directional T1/LGE reads for amyloid (↑↑ T1, ↑↑ ECV, diffuse subendocardial LGE, difficult null) vs Fabry (↓ T1, normal ECV, focal inferolateral LGE). No edema stack or early enhancement — chronic infiltrative disease |
