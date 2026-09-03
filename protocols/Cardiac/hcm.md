# HCM (Hypertrophic Cardiomyopathy CMR)

**Version:** 1.0 | **Date:** 2026-09-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

Same as `cardiac_non-stress.md` — the stress arm is removed:

- **Position:** Supine, head-first. Heart centred over the coil.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly. ECG leads on the anterior chest wall, clear of the coil elements.
- **Laser Landmark:** Mid-sternum at heart level.
- **ECG:** Vector ECG — optimise the R wave (largest amplitude, no T-wave oversensing). Every sequence in this protocol is ECG-gated, so a poor trigger degrades the entire study.
- **IV Access:** **One line** — contrast only; no adenosine, so no second line, no BP cuff choreography, no contraindication screen, and no caffeine restriction.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — consistency matters most: the T1 maps must not drift between acquisitions. (No perfusion run here — the stress protocol's long-hold warning does not apply.)
- **eGFR check:** Gadolinium — confirm eGFR above 30 before the protocol [Confirm threshold].

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–4)
- **Phase 1 — Rest function & obstruction:** 3C stack + 4C/2C cines + LVOT noscout + aortic flow (#5–9)
- **Phase 2 — Native tissue:** T1 maps — SAx3 + 4C + 2C + pathological site (#10–13)
- **Phase 3 — Contrast:** Single dose at 2 ml/s → 7 min wait
- **Phase 4 — Function:** SA volumetry fills the 7-min wait (#14)
- **Phase 5 — LGE:** TI scout → PSIR overviews 4C/2C/SA → 12-slice FB PSIR → high-res T1 seg FS SA (#15–20)

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Phase 3 | Gadolinium — single dose [Confirm mmol/kg — see note] | 2 ml/s | LGE equilibration |

**Total contrast: single dose** [Confirm]. The stress protocol splits 0.2 mmol/kg across three injections; a fibrosis-focused cardiomyopathy exam is the setting where a double dose is the common alternative — dose per local practice.

---

## 3. Imaging Series

### Phase 0 — Surveys & Localizers

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 1 | `t2_trufi_tra_thorax_bh` | Axial | True axial | Heart only — no aortic arch. The axial planning localizer | BH (end-insp) |
| 2 | `trufi_2c_ipat` | Pseudo 2C | Single slice through LV apex + mitral valve centre — planned on #1 | LV + LA — apex → mitral annulus | BH |
| 3 | `trufi_4c_ipat` | Pseudo 4C | Single slice ⟂ pseudo-2C through apex + both AV valves — planned on #2 | All 4 chambers | BH |
| 4 | `trufi_shortaxis_ipat` | Pseudo SAX | ⟂ interventricular septum, ∥ mitral valve plane — planned on #3 | Base → apex, extending basally to include the left atrium (for 3C planning) | BH |

### Phase 1 — Rest Function & Obstruction

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 5 | `cine_tf2d13_retro_3c_stack` | 3C stack | Parallel 3C slices — bisect LV + outflow tract, planned on SA (#4) | Across the stack: full LV + LVOT width, wall-to-wall (septal → lateral epicardium). Each slice: LV + LA + LVOT | BH |
| 6 | `cine_tf2d13_retro_4c` | 4C | Through RV angle + LV centre — planned on SA (#4) | All 4 chambers — apex included (apical variant) | BH |
| 7 | `cine_tf2d13_retro_2c` | 2C | Bisects LV, ∥ septum insertion line — planned on SA (#4) | LV + LA | BH |
| 8 | `cine_tf2d13_retro_lvot_noscout` | LVOT | ⟂ 3C view, through and bisecting the LVOT — planned on #5. No auto-scout | LVOT + aortic valve | BH |
| 9 | `flow_150_tp_retro_bh_epat_ao` | Through-plane | ⟂ ascending aorta, just above the sinotubular junction | Ascending aorta cross-section | BH |

### Phase 2 — Native Tissue (T1 Maps)

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 10 | `t1_map_native_sab/sam/saa` | SAX ×3 | SAB/SAM/SAA — placed on the SA localizer (#4), systolic-phase reference (cardiac_non-stress #10) | Basal, mid, apical SAX | BH |
| 11 | `t1_map_native_4c` | 4C | Copy from #6 | LV long axis — apex included | BH |
| 12 | `t1_map_native_2c` | 2C | Copy from #7 | LV long axis | BH |
| 13 | `t1_map_native_pathological_site` | Pathology site | Planned on the maximal hypertrophy / pathology — e.g. the thickest segment or the apical cap [Confirm placement practice] | The pathological segment | BH |

### Phase 3 — Contrast

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Contrast — 2 ml/s** | — | Single gadolinium dose at 2 ml/s [Confirm dose] + saline flush. No perfusion run, so no first-pass timing | — | — |
| — | **7 min wait** | — | LGE imaging starts ~7 min after the injection | — | — |

### Phase 4 — Post-Contrast Function

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 14 | `cine_tf2d13_retro_sa_volumetry` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |

### Phase 5 — LGE

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 15 | `ti_scout` | SAX single | Single SA location at the thickest myocardium (mid-ventricular) | Single mid SAX slice | BH |
| 16 | `de_overview_tfi_psir_4c` | 4C | Copy from #6 | Entire myocardial wall — base → apex | BH |
| 17 | `de_overview_tfi_psir_2c` | 2C | Copy from #7 | Entire myocardial wall — base → apex | BH |
| 18 | `de_overview_tfi_psir_sa` | SAX stack | Copy from #14 | Entire myocardial wall — whole LV | BH |
| 19 | `de_trufi_overview_12sl_psir_fb` | SAX ×12 | Copy from #14 — 12 slices | Base → apex | FB |
| 20 | `tfl13_2d_t1_seg_fs_c_sa` | SAX stack (2D) | Copy from #14 — [Confirm: routine or optional] | Base → apex, built slice-by-slice toward the apex | BH |

---

## 4. Sequence Rationale

### Core Strategy

**HCM is a genetic sarcomere disease that thickens the heart — and the thickness is the disease.** Myocyte disarray and interstitial fibrosis produce asymmetric hypertrophy (wall thickness ≥ 15 mm, or ≥ 13 mm with a family history — most often the basal septum), with a dynamic left ventricular outflow tract obstruction driven by **systolic anterior motion (SAM)** of the mitral valve, and microvascular ischemia that lays down focal replacement fibrosis. The exam therefore answers four questions: **how thick and where** (the cines, including the 3C stack through the septum), **is there obstruction** (the LVOT cine + aortic flow), **what is the tissue** (native T1 — the diffuse fibrosis read), and **how much scar** (LGE — the replacement fibrosis read; ≥ 15% of LV mass is the sudden-cardiac-death/ICD threshold). Contrast for LGE completes the instrument.

### The disease — hypertrophy, SAM, and the dynamic obstruction

**The mechanism chain:** the hypertrophied basal septum narrows the LVOT → blood accelerates through the narrowing, and the fast stream exerts a Venturi/drag force on the adjacent anterior mitral leaflet → the leaflet is pulled anteriorly during systole — the **systolic anterior motion (SAM)** — until it touches the septum (the **SAM-septal contact**). The contact plugs the already-narrow LVOT intermittently — the mid-systolic obstruction — and the leaflets no longer coapt properly, so the valve leaks (eccentric, posteriorly directed mitral regurgitation).

- **Dynamic, not fixed:** the contact develops mid-to-late systole, so the obstruction appears as systole progresses — HCM's gradient is late-peaking, unlike fixed aortic stenosis where the valve is narrowed from the start.
- **Predisposing anatomy:** an elongated anterior leaflet, anteriorly displaced papillary muscles, and abnormal chordal attachments all make SAM more likely.

### When to use this protocol

- Suspected or newly diagnosed HCM — confirmation and mapping: maximal wall thickness, distribution (asymmetric septal, apical, concentric, mid-ventricular)
- Family screening — genotype-positive relatives; serial CMR as the phenotype evolves
- Risk stratification — LGE extent and EF are the sudden-death-risk inputs
- Pre-procedural planning — myectomy / alcohol septal ablation: obstruction localisation, fibrosis extent
- Serial follow-up — after septal reduction therapy

### How this differs from the other cardiac protocols

- **The cines gain the obstruction question:** the 3C is acquired as a **stack** through the septum (#5), and the LVOT cine + aortic flow (#8–9) are read for SAM and the LVOT gradient — HCM's signature hemodynamic problem. In cardiac_non-stress the same views serve generic valvular/functional questions; in amyloidosis the question does not exist at all.
- **The maps become native-T1-only and targeted:** no T2 map (chronic HCM is not an edema disease); the native T1 extends beyond the standard SAx3 with the 4C, 2C and pathological-site placements (#11–13) — aimed at the maximal hypertrophy and the apical variant. No post-contrast maps, so no ECV in this build — the amyloidosis protocol measures it.
- **The LGE block is all-PSIR and read for HCM:** every overview is phase-sensitive — thick walls and diffuse fibrosis make the TI null unreliable, so TI-robust PSIR replaces the TI-dependent magnitude overviews of cardiac_non-stress. The interpretation is HCM-specific (the Phase 5 LGE reading).
- **The thick-heart differential (vs amyloidosis):** echo shows a thickened ventricle in both — CMR separates them: native T1 mildly-to-moderately ↑ in HCM (fibrosis) vs markedly ↑ in amyloid (the highest of any cardiomyopathy) vs shortened in Fabry; LGE patchy mid-wall + RV insertions vs a diffuse subendocardial ring with a difficult null (the full three-way pattern read in Phase 5).

### Phase 0 — Surveys & Localizers (#1–#4) — the planning stage

Same planning cascade as `cardiac_non-stress.md` Phase 0 (the localizers here run with iPAT, as in thalassemia #1–4): axial localizer (#1) → pseudo 2C (#2) → pseudo 4C (#3) → SA localizer (#4), prescribed ⟂ interventricular septum and ∥ mitral valve plane, with coverage extending basally to include the left atrium.

### Phase 1 — Cine Function & Flow (#5–#9)

Identical planning to `cardiac_non-stress.md` #5–#9 — retrospective gating, planned back from the SA localizer — with the HCM-specific upgrades below:

**`cine_tf2d13_retro_3c_stack` (#5) — the 3C acquired as a stack:** parallel slices across the LV + outflow tract — the HCM upgrade of the standard single 3C, and the only cine that needs one:
    - **Why only the 3C is stacked:** the 4C/2C answer single-plane questions — global function, the four chambers, the apex, the valves — all read off one slice each. The 3C is hunting a **narrow, moving target**: the SAM–septal contact and its jet run somewhere along the LVOT, and the spot varies between patients and shifts through systole; the maximal septal bulge is equally local. A single 3C slice can sit just off the jet core or the thickest point and show a clean-looking outflow — the false negative. The stack guarantees the outflow volume is covered, so at least one slice carries them in-plane.
    - **Coverage — wall-to-wall in the stack direction:** the stack spans from the septal epicardium across the cavity to the lateral-wall epicardium. Thickness is measured endocardium-to-epicardium, so both borders must be in the image. The wall-only edge slices are the coverage margin.

**`cine_tf2d13_retro_4c` (#6):** through the RV angle + LV centre — all four chambers, global function, septal/lateral wall motion; the apex is where the **apical variant** thickens the ventricle, and the 4C shows it.

**`cine_tf2d13_retro_2c` (#7):** bisects LV, ∥ septum insertion line — LV + LA, anterior/posterior wall motion, mitral valve.

**`cine_tf2d13_retro_lvot_noscout` (#8):** ⟂ the 3C, through and bisecting the LVOT, no auto-scout (as cardiac_non-stress #8). In HCM this is **the obstruction view**: the anterior mitral leaflet visibly contacting the septum during systole — the contact itself — plus the mid-systolic jet, which appears as a dark signal void streaking through the bright blood pool (turbulence dephases the spins), and the aortic valve motion. Read together with the 3C stack (#5) — the obstruction views of Phase 1.

**`flow_150_tp_retro_bh_epat_ao` (#9):** through-plane phase-contrast ⟂ ascending aorta just above the sinotubular junction (check on-end in both AO views), VENC 150 — the aortic volume measurement. The sequence produces a flow curve across the cardiac cycle. The area under the forward systolic part of the curve is the **forward volume**; the area under the backward diastolic part is the **regurgitant volume**; their ratio gives the **regurgitant fraction**; and what remains after subtracting the leak — forward minus regurgitant — is the **stroke volume**.

**Aortic placement vs LVOT placement — why the slice position matters in HCM:**
    - **For flow volume, the two placements are equivalent:** through-plane PC measures volume flow (velocity × area, integrated over the cycle), and no branch vessels take blood between the LVOT and the sinotubular junction (the coronaries sip ~1% of the stroke volume) — so stroke volume and regurgitant fraction come out the same at both levels. The aortic placement serves exactly that role here.
    - **For velocity, they are not:** the HCM obstruction is **subvalvular** — the SAM–septal contact narrows the LVOT below the aortic valve, and velocity peaks at that narrowest point (the vena contracta), reaching 3–5 m/s. By the time the jet has travelled the length of the LVOT, passed the valve and re-expanded in the wide aortic root, it has partly dissipated — above the valve the peak velocity is lower.
    - **Consequence:** the aortic slice gives clean volumes but cannot measure the gradient. The velocity curve still carries the indirect signature of obstruction — late-peaking and dagger-shaped, the ventricle pushing against a progressively closing outlet.
    - **Why an LVOT slice might be wanted in HCM:** the gradient — the pressure drop across the obstruction — is the hemodynamic severity metric: ≥ 30 mmHg at rest defines obstructive HCM and drives management (drugs vs myectomy/alcohol septal ablation). It is quantified from the peak velocity at the narrowest point via the simplified Bernoulli, **ΔP = 4v²** (the proximal velocity is omitted — negligible at a normal ~1 m/s). A through-plane PC at the LVOT therefore gives a resting gradient estimate — the slice sits at the stenosis itself, below the valve, in the jet core — though echo Doppler remains the reference (it measures both velocities and can provoke). Costs: the jet shifts through systole, and VENC 150 aliases immediately (above 1.5 m/s ≈ 9 mmHg) — significant gradients need VENC 400+.

### Phase 2 — Native T1 Maps (#10–#13)

- **`t1_map_native` (#10–#13) — the native T1 map set, one question at four placements:** breath-held MOLLI, scheme **5(_)3** — the B(R)A sampling scheme and the RR-dependent scheme table are explained in `cardiac_non-stress.md` #10.
    - **`t1_map_native_sab/sam/saa`** (#10)
    - **`t1_map_native_4c`** (#11)
    - **`t1_map_native_2c`** (#12)
    - **`t1_map_native_pathological_site`** (#13)

**Why native T1 is the HCM tissue read:**
    - **Hypertrophy is not all muscle.** Myocyte disarray and interstitial fibrosis lengthen native T1 — the diffuse fibrosis burden is read even before LGE-visible focal scar appears, and LGE-negative HCM can still carry an elevated T1.
    - **It points at the differential:** a markedly elevated T1 argues amyloid rather than HCM; a shortened T1 argues Fabry or iron — see How this differs from the other cardiac protocols.

**Why does HCM extend the map set beyond the SAx3 — when no other cardiac protocol does?**
    - **The true apex is the SAx3's blind spot — and the apical variant lives there:** the three SAX levels end distal to the papillary tips, a slice short of the actual apex. The other protocols' diseases are never there — myocarditis is inferolateral subepicardial, amyloid and iron are diffuse — so any three standard levels catch them. But apical HCM puts its hypertrophy exactly in the true apex, and the 4C is the long-axis plane that shows it: without the 4C map, the diseased segment of an apical HCM patient has no quantitative tissue coverage at all.
    - **HCM's hypertrophy is segment-specific:** the other protocols ask diffuse questions that any three levels answer; HCM asks a local one — what is the thickest segment made of — and that segment can sit anywhere (basal septum, mid-wall, lateral wall, apex). The 4C/2C run base-to-apex along two wall pairs, so together with the SAx3 they put more of the wall surface fully in-plane — raising the chance the hypertrophied segment is sampled completely rather than partial-volumed at a SAX slice edge; the pathological-site map (#13) then does the dedicated close-up.
    - **The read is segmental:** elevated native T1 in HCM is most meaningful in the hypertrophied segment — including LGE-negative HCM, where the T1 rise is the only tissue abnormality — so the segment must actually be in-plane on a map.

**No T2 map, no post-contrast maps:** chronic HCM is not an edema disease, so the non-stress T2 map is dropped; and without post-contrast maps there is no ECV in this build.

### Phase 3 — Contrast

A single gadolinium dose at **2 ml/s** + saline flush — no first-pass perfusion to capture, so the slow rate suffices. After the injection, the **7-minute wait** lets the contrast equilibrate — the same LGE physiology as cardiac_non-stress.

### Phase 4 — Post-Contrast Function (#14)

**`cine_tf2d13_retro_sa_volumetry` (#14) — SA volumetry:** identical to `cardiac_non-stress.md` #12 — diastolic-phase planning, contiguous stack from beyond the apex (no blood pool) to past the mitral valve level, filling the 7-minute wait. EF via modified Simpson's disk summation. HCM note: the cavity is small and the walls thick — the EF can read supranormal while the stroke volume stays low; report the volumes, not just the EF.

### Phase 5 — LGE (#15–#20)

**Why fibrotic myocardium enhances late:** the same LGE physiology as cardiac_non-stress Phase 5 — after the 7-minute wait, gadolinium has equilibrated in the extracellular space; fibrosis replaces myocytes with an expanded extracellular matrix, so contrast accumulates there, washes out slowly, and stays **bright** against nulled **dark** myocardium. HCM's fibrosis comes in two forms — **focal replacement fibrosis** (microvascular ischemia; LGE-visible) and **diffuse interstitial fibrosis** (raises background T1 everywhere; makes the null harder).

- **`ti_scout` (#15):** at the 7-min mark, single SA at the thickest myocardium. Optimal TI = normal myocardium most uniformly dark without a dark rim (blood pool nulling + interface partial volume — see cardiac_stress #17). In HCM the thickest myocardium is exactly where the null must be verified.
- **`de_overview_tfi_psir_4c` (#16), `de_overview_tfi_psir_2c` (#17), `de_overview_tfi_psir_sa` (#18) — PSIR overviews, three planes:** phase-sensitive IR reconstruction — TI-robust (the sign-sensitive read survives an imperfect TI, as in the myocarditis late overviews). HCM's thick walls and diffuse fibrosis make the TI null unreliable across segments, so all three breath-held overviews are PSIR rather than the TI-dependent magnitude IR of non-stress. Three planes because the fibrosis pattern is patchy.
- **`de_trufi_overview_12sl_psir_fb` (#19) — 12-slice free-breathing PSIR:** a second whole-ventricle base → apex PSIR pass, free-breathing with averaging. Both overview sets cover the whole ventricle — the difference is the breathing: the free-breathing averaging raises the SNR for the subtle patchy HCM fibrosis and rescues patients who cannot hold breath, and the PSIR read stays the TI-insensitive catch-all (RV, thrombus, any territory — as cardiac_non-stress #17).
- **`tfl13_2d_t1_seg_fs_c_sa` (#20) — the high-res 2D SA:** segmented T1-weighted TurboFLASH, fat-saturated, built slice-by-slice toward the apex — fat saturation unmasks thin subepicardial enhancement, high resolution measures transmurality — a GRE readout free of the SSFP dark-rim/banding artifacts of the TrueFISP PSIR overviews (the same high-res sequence as cardiac_non-stress #18). [Confirm: routine or optional after radiologist review.]

**The HCM LGE reading — how the bright spots are read:**
    - **Pattern — patchy mid-wall in the hypertrophied segments + RV insertions:** LGE shows scar as bright spots against nulled dark muscle, so the *location* of the spots is the diagnosis:
        - **Mid-wall:** the spots sit in the **middle layer** of the wall — unlike infarct, which starts at the inner layer.
        - **Patchy:** scattered, many small spots — microvascular ischemia in muscle that outgrew its small-vessel supply.
        - **Hypertrophied segments:** the spots concentrate in the **thickest muscle** — the disease sites themselves.
        - **RV insertion points:** the two corners where the RV wall meets the septum — mechanical stress of a thick, stiff septum; enhance characteristically.
        - **Contact point:** repeated SAM–septal contact can leave a "kiss lesion" — endocardial thickening/fibrosis at the contact point on the septum — visible as focal enhancement.
    - **Extent is the metric:** the quantity, not just the presence, drives the decision — LGE extent is measured as the percentage of LV mass showing enhancement, and at **≥ 15%** the sudden-cardiac-death risk rises enough that an ICD is considered. The report must quantify.
    - **Differential — three diseases, three scar patterns:**
        - **Ischemic:** subendocardial, confined to one coronary territory — the inner layer dies first in the starved artery's zone.
        - **Amyloid:** a diffuse subendocardial ring around the whole circumference — no territory logic, with a difficult null.
        - **HCM:** scattered mid-wall spots in the thick segments — neither a territorial wedge nor a global ring.

---

## 5. Variations

**Apical HCM**
- The apical variant thickens the apex, where the standard views are weakest: the SA volumetry stack must extend to the true apex (often one slice more than usual); the 4C map (#11) + pathological-site map (#13) are the quantitative reads; the 12-slice FB LGE (#19) covers the apical cap.

**VENC step-up**
- High gradients alias VENC 150 — if the flow phase wraps, repeat at VENC 400 (as cardiac_non-stress).

---

## 6. Alerts

| Check | Improve |
|---|---|
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | Choose the ECG lead with the cleanest R wave (largest amplitude, no T-wave oversensing) — every sequence is gated, so a poor trigger degrades the entire study |
| **eGFR** — confirmed above 30 before contrast? | Single-dose protocol but still gadolinium — check before, not after |
| **Breath-hold consistency** — same small end-inspiratory position on the T1 maps? | Slice drift between the maps breaks the T1/LGE comparison |
| **LVOT planning** — 3C stack and LVOT cine through the outflow tract; SAM–septal contact and the jet caught? | The obstruction is dynamic — if the jet is not seen on the cines, the views are off-plane |
| **Maximal wall thickness** — measured in diastole at the thickest segment? | The diagnostic criterion (≥ 15 mm) — measure and document it |
| **Flow VENC** — any aliasing in the aortic flow? | Aliased phase wraps velocities — if wrapping appears, repeat at VENC 400 |
| **T1 map placement** — SAx3 levels correct; pathological site on the maximal hypertrophy; apex covered by the 4C map (apical variant)? | A misplaced map misses the diseased segment — the map set is targeted, so targeting must be right |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |
| **LGE timing** — 7 min reached before the LGE run starts? | Too early, the contrast is not equilibrated — diffuse uptake, no clean null |
| **TI correctness** — myocardium dark on the high-res tfl series, contrast clean on the PSIR overviews? | PSIR forgives an imperfect TI, not a wrong one — contrast falls off as the TI drifts; and the high-res tfl13 is magnitude IR, fully TI-dependent. If the null looks off, re-scout and re-measure rather than adjusting blindly |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-03 | — | Initial build — 20 workflow steps. Non-stress cardiac base restructured for the thick heart: iPAT localizer cascade + tf2d13 cines (3C stack / 4C / 2C / LVOT noscout) + aortic flow VENC 150 ePAT + native T1 maps (SAx3 + 4C + 2C + pathological site; no T2 map, no ECV) + single-dose contrast + SA volumetry (fills the 7-min wait) + TI scout + all-PSIR LGE (4C/2C/SA + 12-slice FB) + TurboFLASH T1 seg FS SA high-res. HCM fibrosis reading: patchy mid-wall / RV insertion, ≥ 15% LV mass ICD threshold; amyloid/Fabry differential |
