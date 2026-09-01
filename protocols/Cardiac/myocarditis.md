# Myocarditis (Myocarditis CMR — Edema, Early Enhancement + LGE)

**Version:** 1.0 | **Date:** 2026-09-01 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

Same as `cardiac_non-stress.md`:

- **Position:** Supine, head-first. Heart centred over the coil.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly. ECG leads on the anterior chest wall, clear of the coil elements.
- **Laser Landmark:** Mid-sternum at heart level.
- **ECG:** Vector ECG — optimise the R wave (largest amplitude, no T-wave oversensing). Every sequence in this protocol is ECG-gated, so a poor trigger degrades the entire study.
- **IV Access:** **One line** — contrast only; no adenosine.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — consistency matters most: the T1/T2 maps and the TIRM stack must not drift between acquisitions.
- **eGFR check:** Gadolinium — confirm eGFR above 30 before the protocol [Confirm threshold].

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–4)
- **Phase 1 — Rest function:** Cines 3C/4C/2C/LVOT + aortic flow (#5–9)
- **Phase 2 — Edema & mapping:** T2 TIRM dark-blood stack + native T1 map + T2 map (#10–12)
- **Phase 3 — Contrast & early enhancement:** Single dose at 2 ml/s → early Gd enhancement (optional) → early TI scout → early PSIR overviews (#13–16)
- **Phase 4 — Function:** SA volumetry fills the 7-min wait (#17)
- **Phase 5 — LGE:** TI scout → PSIR overviews → 12-slice FB → T1 seg FS SA (#18–23)

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Phase 3 | Gadolinium — single dose [Confirm mmol/kg] | 2 ml/s | Early enhancement + LGE equilibration |

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

### Phase 2 — Edema & Mapping

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 10 | `t2_tirm_15_db_sax` | SAX stack | ⟂ LV long axis — 15 slices, dark blood | Whole heart SA — base → apex | BH |
| 11 | `t1_map_sax` (native) | SAX ×3 | SAB/SAM/SAA — placed on the SA localizer (#4), systolic-phase reference. Decision: MOLLI scheme 5(_)3 per RR (see cardiac_non-stress B(R)A scheme table) | Basal, mid, apical SAX | BH |
| 12 | `t2_map_trufisp_sax` | SAX ×3 | Copy Slice from #11 | Basal, mid, apical SAX | BH |

### Phase 3 — Contrast & Early Enhancement

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Contrast — 2 ml/s** | — | Single gadolinium dose at 2 ml/s [Confirm dose] + saline flush | — | — |
| — | **Early Gd enhancement (optional)** | — | T1-weighted early post-contrast for the early enhancement ratio [Confirm sequence] — the classic hyperemia marker | — | BH |
| 13 | `ti_scout_early` | SAX single | Single SA location at the thickest myocardium — early-phase TI | Single mid SAX slice | BH |
| 14 | `de_overview_tfi_psir_sax_early_c` | SAX stack | Copy Slice from #10 — early post-contrast PSIR | Entire myocardium wall — whole LV | BH |
| 15 | `de_overview_tfi_psir_4c_early_c` | 4C | Copy Slice from #6 — early post-contrast PSIR | Entire myocardium wall — base → apex | BH |
| 16 | `de_overview_tfi_psir_2c_early_c` | 2C | Copy Slice from #7 — early post-contrast PSIR | Entire myocardium wall — base → apex | BH |
| — | **7 min wait** | — | Late LGE imaging starts ~7 min after the injection | — | — |

### Phase 4 — Post-Contrast Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 17 | `cine_tf2d13_retro_sa_volumetry_c` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |

### Phase 5 — LGE

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 18 | `ti_scout` | SAX single | Single SA location at the thickest myocardium (mid-ventricular) | Single mid SAX slice | BH |
| 19 | `de_overview_tfi_psir_4c` | 4C | Copy Slice from #6 — late PSIR, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 20 | `de_overview_tfi_psir_2c` | 2C | Copy Slice from #7 — late PSIR, TI increased gradually | Entire myocardium wall — base → apex | BH |
| 21 | `de_overview_tfi_psir_sax` | SAX stack | Copy Slice from #17 — late PSIR, TI increased gradually | Entire myocardium wall — whole LV | BH |
| 22 | `de_trufi_overview_12sl_psir_fb` | SAX ×12 | Copy Slice from #17 — 12 slices | Base → apex | FB |
| 23 | `tfl13_2d_t1_seg_fs_c_sax` | SAX stack (2D) | Copy Slice from #17 — [Confirm: routine or optional] | Base → apex, built slice-by-slice upward toward the apex | BH |

---

## 4. Sequence Rationale

### Core Strategy

The myocarditis study is the acute-inflammation exam: **is the myocardium inflamed, and how active is it?** It reads the three Lake Louise layers — **edema** (T2 TIRM + T2 map), **hyperemia** (early gadolinium enhancement), and **injury/fibrosis** (native T1 + LGE) — with the characteristic subepicardial/inferolateral enhancement pattern as the signature. Structurally it is the non-stress tissue instrument with two myocarditis-specific channels added: the dark-blood T2W stack and the early enhancement block.

### When to use this protocol

- Suspected acute myocarditis — chest pain, troponin rise, ECG changes, non-obstructed coronaries (the MINOCA-type presentation)
- Myocarditis follow-up — active inflammation vs healed (edema resolution on T2W/T2 map)
- For further information please refer to the general non-stress indications and the stress-vs-non-stress decision logic: `cardiac_non-stress.md` (an acutely inflamed myocardium must not be stressed)

### How this differs from cardiac_non-stress

- **T2 TIRM dark-blood SA stack added (#10):** the traditional edema sequence beside the T2 map — dark blood against bright edema gives regional delineation the map can't show; together the qualitative T2W and the quantitative T2 map satisfy the edema criterion from both directions.
- **The early gadolinium enhancement block (#13–#16):** hyperemia — inflamed myocardium has increased blood volume and capillary leak, so it takes up gadolinium early. The block runs ~1–3 min post contrast: the optional EGE (classic Lake Louise criterion, early enhancement ratio), its own early TI scout, and early PSIR overviews in three planes. The non-stress protocol has no early phase.
- **DE overviews are TrueFISP PSIR in both phases** — the non-stress protocol uses plain TrueFISP magnitude IR overviews; this protocol reads all enhancement on PSIR, whose TI-insensitivity suits the rapidly changing early phase and the often-subtle subepicardial patterns.
- **Otherwise identical:** cines, flow, T1/T2 maps, volumetry, and the late LGE block are the same sequences and planning as cardiac_non-stress.

### Phase 0 — Surveys & Localizers (#1–#4) — the planning stage

Same planning cascade as `cardiac_non-stress.md` Phase 0 (the localizers here run with iPAT): axial localizer (#1) → pseudo 2C (#2) → pseudo 4C (#3) → SA localizer (#4), prescribed perpendicular to the interventricular septum and parallel to the mitral valve plane, with coverage extending basally to include the left atrium.

### Phase 1 — Cine Function & Flow (#5–#9)

Identical to `cardiac_non-stress.md` #5–#9 — retrospective gating, planned back from the SA localizer; the flow sequence runs with ePAT acceleration. Condensed:
- **`cine_tf2d13_retro_3c` (#5):** bisects LV + outflow tract — the LVOT view: aortic valve motion, AS/AR (aortic stenosis/aortic regurgitation) jets, anteroseptal/inferolateral walls.
- **`cine_tf2d13_retro_4c` (#6):** through the RV angle + LV centre (avoid the aorta on other SA slices) — all four chambers, global function, septal/lateral wall motion.
- **`cine_tf2d13_retro_2c` (#7):** bisects LV, ∥ septum insertion line — LV + LA, anterior/posterior wall motion, mitral valve.
- **`cine_tf2d13_retro_lvot_noscout` (#8):** ⟂ the 3C through and bisecting the LVOT, no auto-scout — the orthogonal outflow-tract view.
- **`flow_150_tp_retro_bh_epat_ao` (#9):** through-plane phase-contrast ⟂ ascending aorta just above the sinotubular junction (on-end in both AO views), VENC 150 — forward volume, regurgitant fraction, stroke volume. Aliasing → repeat at VENC 400. (Phase-contrast mechanics: `cardiac_stress.md` #10.)

(The `tf2d13` names are the versioned form of the same single-slice 2D retro TrueFISP cines as `cardiac_non-stress.md` — not volume stacks.)

### Phase 2 — Edema & Mapping (#10–#12)

**`t2_tirm_15_db_sax` (#10) — T2 TIRM dark blood:** the traditional edema sequence, and the one place in the cardiac protocols where TIRM nulls **blood, not fat**.
    - **How it works:** a T2-weighted TSE readout is preceded by an inversion-recovery pulse timed to **blood's null point** (~450–600 ms at 1.5T) — that inversion *is* the dark-blood mechanism ("db"): flowing blood crosses zero and images **black**, while edematous myocardium — with its long T1 and long T2 — stays **bright**. Black blood outlines the edema against the cavity — bright blood pooling against bright edematous myocardium would blend the two and hide it. Fat is not suppressed, and it doesn't matter — epicardial fat sits outside the myocardium and does not obscure the edema read. Acquired pre-contrast: gadolinium shortens myocardial T1 and would corrupt the blood-null setup.
    - **Coverage:** a 15-slice short-axis stack across the whole left ventricle, base → apex — every AHA segment included, because myocarditis edema is regional and unpredictable (classically inferolateral at the base-mid level, but any segment, or even the RV, can be involved). The SA geometry matches the late LGE stack, so edema and enhancement are compared segment-by-segment — edema colocalizing with enhancement is the acute-lesion signature.
    - **Why both the TIRM stack and the T2 map:** the TIRM is the qualitative pattern-reader (regional edema, the familiar Lake Louise look) but can miss diffuse edema and is read subjectively; the T2 map is the quantitative channel that catches diffuse edema and makes follow-up comparisons. Coverage differs too — the map samples only three slices (SAB/SAM/SAA, the breath-hold cost of MOLLI-style sampling), so the TIRM's whole-heart stack is also the net that catches focal edema at levels the map never measures. They fail differently, so the protocol runs both — the edema criterion is satisfied from both directions.

**`t1_map_sax` (#11) — native T1 map:** same MOLLI acquisition and same role as `cardiac_non-stress.md` #10 — native T1 quantifies diffuse injury/fibrosis that LGE cannot see. The scheme is chosen by RR at the console (**decision**: 5(_)3 — see the B(R)A scheme and RR table in cardiac_non-stress).

**`t2_map_trufisp_sax` (#12) — T2 map:** same as `cardiac_non-stress.md` #11 — the quantitative edema channel (T2-prep module and its mechanism explained there). Elevated T2 = edema = active inflammation; normalizing T2 on follow-up = resolution.

### Phase 3 — Contrast & Early Enhancement (#13–#16)

A single gadolinium dose at **2 ml/s** + saline flush — no first-pass to capture, so no tight bolus is needed. Immediately after injection the **early enhancement window (~1–3 min)** opens:

- **Early Gd enhancement (optional):** the **hyperemia read** — the classic Lake Louise criterion 1. Inflamed myocardium is vasodilated with leaky capillaries, so gadolinium floods in fast, before any equilibrium; T1-weighted early imaging measures the early enhancement ratio (myocardium vs skeletal muscle, traditionally >4 = positive). It detects **active inflammation even when there is no necrosis yet** — the myocardium that is sick but will recover. [Confirm sequence/ratio.]
    - **When it earns its place:** when LGE is negative but suspicion is high — the early phase can support active inflammation where LGE has nothing to show (inflammation-dominant myocarditis never necroses and stays LGE-negative). On follow-up scans it is not needed — the healed-myocarditis question is edema resolution (T2) and residual fibrosis (LGE), not hyperemia.
    - **Why not rely on it alone:** early enhancement is sensitive but less specific — any hyperemia lights up (peri-infarct zones too) — and technically finicky (strict timing, ratio measurement); the late pattern is the diagnostic anchor.

- **`ti_scout_early` (#13):** the early phase needs its **own** TI: minutes after injection the blood pool and myocardial gadolinium concentrations are far higher than at 7 min, so myocardial T1 is much shorter and the null point much earlier — the late scout's TI would be wrong here. The early scout measures the early TI.

**Early PSIR overviews — `de_overview_tfi_psir_sax_early_c` (#14), `_tfi_psir_4c_early_c` (#15), `_tfi_psir_2c_early_c` (#16):** three-plane early enhancement on PSIR.
    - **Why PSIR here:** the early window is the worst moment for magnitude IR — contrast kinetics are at their fastest (blood pool concentration high and falling, myocardial uptake rising), so the myocardium's null point is a rapidly moving target and the TI scout can only sample one instant. A magnitude image lives or dies by hitting that exact TI; PSIR reads the *sign* of the magnetization instead, so the bright/dark assignment holds across a wide range of TIs — a drifting TI cannot flip or fade the contrast.
    - **The TI is still set:** PSIR forgives TI errors but does not ignore the TI — the parameter is set from the early scout, near normal myocardium's null, because that is where signal and contrast-to-noise are strongest; the sign read only protects the assignment, not the signal strength. (The magnitude-reconstructed high-res series #23 is the sequence that truly depends on the measured TI.)
    - **Why three planes + speed:** the TrueFISP readout is fast, which matters inside the short ~1–3 min window, and the three planes cover the subepicardial/lateral patterns from every direction.

After the early block, the **7-minute wait** lets the contrast equilibrate for the late LGE phase.

### Phase 4 — Post-Contrast Function (#17)

**`cine_tf2d13_retro_sa_volumetry_c` (#17) — SA volumetry:** identical to `cardiac_non-stress.md` #12 — diastolic planning, contiguous stack beyond the apex to past the mitral valve level, filling the 7-minute wait; EF via modified Simpson's disk summation.

### Phase 5 — LGE (#18–#23)

Same late LGE block as `cardiac_non-stress.md` #13–#18, on PSIR overviews:

**Why inflamed/infarcted myocardium enhances late:** after the 7-minute wait the gadolinium has equilibrated in the extracellular space; injured tissue with its expanded extracellular matrix accumulates contrast and washes out slowly — it stays **bright** on the inversion-recovery image while normal myocardium nulls **dark**. This is the **injury read — Lake Louise criterion 3** — the counterpart of the early hyperemia read: the early phase shows the inflammation that may still recover, the late phase shows the damage that remains. Its **subepicardial/inferolateral non-coronary pattern** is what makes the myocarditis diagnosis specific — the 4C and 2C views catch it in-plane and the FS high-res series measures it precisely.

- **`ti_scout` (#18):** the late TI — optimal = normal myocardium most uniformly dark without a dark rim (blood pool nulling + interface partial volume — see cardiac_non-stress #13).
- **Late PSIR overviews — `de_overview_tfi_psir_4c` (#19), `_2c` (#20), `_sax` (#21):** three-plane late enhancement; TI increased gradually across the series as contrast washes out.
    - **Why PSIR here too:** myocarditis enhancement is often thin, subepicardial, and low-contrast — exactly the pattern a slightly-off TI destroys on magnitude IR. PSIR's sign-based read keeps the assignment correct even when the TI drifts, so in this protocol sensitivity comes first in every enhancement read.
    - **Machine dependency:** PSIR is a reconstruction option on the same IR sequence, not a separate sequence — machines with older software or without the option run these overviews magnitude-reconstructed. On such a machine the overviews become TI-dependent and TI correctness turns critical, exactly as in the non-stress protocol.
- **`de_trufi_overview_12sl_psir_fb` (#22):** 12-slice PSIR free-breathing overview — TI-insensitive catch-all (RV, thrombus, any territory).
    - **Why both this and the 3-plane PSIR overviews:** with PSIR on both sets, the difference between them is coverage and breathing, not reconstruction — the three breath-held planes are the quality read in the standard geometry; the free-breathing 12-slice stack is the whole-ventricle catch-all (every segment, RV, thrombus; robust when breath-holds fail).
- **`tfl13_2d_t1_seg_fs_c_sax` (#23):** the high-res segmented 2D T1 TurboFLASH FS SAX — slice-by-slice toward the apex; fat saturation unmasks the thin subepicardial enhancement from epicardial fat; high resolution measures its thickness. [Confirm: routine or optional.]

---

## 5. Variations

**Arrhythmia / poor breath-hold — real-time cine fallback:** swap the gated cines for the `cine_trufi_cs_rt_adapt_*` real-time counterparts — same planes and coverage, no other parameter changes. The maps and LGE remain gated. Full description: `cardiac_non-stress.md` Variations.

**Suspected aortic stenosis / high-velocity jet**
- Repeat the flow sequence at VENC 400 cm/s — 150 cm/s aliases at stenotic velocities.

**Ischemia also in question**
- The MINOCA-type presentation sometimes needs the ischemia answer too — consider adding the adenosine perfusion arm (cardiac_stress) only once acute inflammation has been excluded or has resolved.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | Choose the ECG lead with the cleanest R wave (largest amplitude, no T-wave oversensing) — every sequence is gated, so a poor trigger degrades the entire study |
| **eGFR** — confirmed above 30 before contrast? | Single-dose protocol but still gadolinium — check before, not after |
| **Breath-hold consistency** — same small end-inspiratory position on TIRM, T1/T2 maps? | Slice drift between the edema stack and the maps breaks the comparison |
| **T2 TIRM quality** — blood dark, edema bright? | Dark-blood prep failed if the cavity is bright — regional edema becomes unreadable; check before moving to the maps |
| **VENC** — any aliasing in the aortic flow? | Aliased phase wraps velocities — repeat at higher VENC (400 cm/s) |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **Early enhancement window** — EGE + early scout + early overviews completed within ~1–3 min? | The early phase vanishes as contrast washes — late imaging cannot recover the hyperemia read |
| **TI correctness** — normal myocardium dark on the late DE and high-res series? | The late nulling TI sits around ~300 ms — verify on the DE and high-res images, not just at the scout. If the myocardium looks bright (nulling off) or the delay has shifted, re-scout and re-measure rather than adjusting blindly |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-01 | — | Initial build — 23 workflow steps. Non-stress base (localizers + retro cines + flow ePAT + native T1 + T2 map + volumetry + late LGE) with myocarditis-specific channels: T2 TIRM 15-slice dark-blood SA stack, early enhancement block (EGE optional + early TI scout + early PSIR overviews 3 planes), PSIR overviews in both phases, high-res FS SAX. Single-dose contrast 2 ml/s |
