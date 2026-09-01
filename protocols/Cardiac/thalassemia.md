# Thalassemia (Iron Overload CMR — Heart & Liver T2*)

**Version:** 1.0 | **Date:** 2026-09-01 | **Scanner:** [Confirm 1.5T/3T — iron T2* thresholds are calibrated at 1.5T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Heart centred over the coil for the cardiac phases; the liver is then centred for the liver phase via the scout views — no physical re-landmarking.
- **Coil:** Body matrix coils anteriorly + spine array posteriorly — the same setup covers both the heart and the liver.
- **Laser Landmark:** Mid-sternum at heart level; the liver centering is done on the console.
- **ECG:** Vector ECG — optimise the R wave. The cardiac sequences are ECG-gated; the liver sequences are ungated.
- **IV Access:** **None** — this exam uses no contrast at all.
- **Breath-Hold Coaching:** Consistent **end-inspiratory** breath-holds, kept small — the multi-echo T2* sequences depend on it: any motion during the echo train breaks the decay fit.

---

## 2. Workflow Overview

- **Phase 0 — Planning:** Localizers + pseudo-2C/4C/SAX cascade (#1–4)
- **Phase 1 — Rest function:** Cines 3C/4C/2C + SA volumetry (#5–8) — no contrast in this exam, so no post-contrast phase
- **Phase 2 — Heart iron:** Multi-echo heart T2* (#9)
- **Phase 3 — Liver:** Table reposition to centre the liver → HASTE / TSE FS / VIBE Dixon anatomy (#10–12) → liver T2* (#13)

**No contrast** — the entire exam is native.

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
| 8 | `cine_tf2d13_retro_sa_volumetry` | SAX stack | ⟂ LV long axis — contiguous stack, planned on the diastolic phase | Whole ventricle — first slice no blood pool, last slice past the mitral valve level | BH |

### Phase 2 — Heart Iron

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| 9 | `fl2d5_10echo_heart` | SAX single | Single mid-ventricular SA slice [Confirm "5"] — 10 echoes at increasing TE | Single mid-ventricular slice, septum in-plane | BH |

### Phase 3 — Liver

| # | Series | Plane | Angulation | Coverage | Breathing |
|---|--------|-------|------------|----------|-----------|
| — | **Table reposition + localizer** | — | Centre on the liver via the scout views — no physical re-landmarking | — | — |
| 10 | `t2_haste_cor_mbh` | Coronal | True coronal — liver localizer | Liver — dome → inferior tip | Multi-BH |
| 11 | `t2_tse_fs_tra_mbh` | Axial | True axial | Liver — dome → inferior tip | Multi-BH |
| 12 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Liver — dome → inferior tip | BH |
| 13 | `fl2d1_14echo_liver` | Axial single | Single axial slice through the right liver lobe — 14 echoes at increasing TE | Right lobe, avoiding vessels | BH |

---

## 4. Sequence Rationale

### Core Strategy

The iron-overload exam: **how much iron is in the heart and the liver?** Transfusion-dependent thalassemia patients accumulate iron with no excretion pathway — the **liver** is the storage pool (loaded first), the **heart** is the danger pool (loaded later; cardiomyopathy, arrhythmia, heart failure). **T2\*** is the biomarker for both: iron is strongly paramagnetic, and its microscopic deposits create field inhomogeneities that accelerate transverse decay in a gradient echo — the more iron, the shorter the T2\*. One breath-held multi-echo acquisition per organ, a decay fit, and the iron load is quantified — **no contrast needed**, which is why this protocol is entirely native.

### When to use this protocol

- Thalassemia major and other transfusion-dependent anaemias — baseline and serial chelation monitoring (the heart T2\* decides chelation intensity and urgency)
- Hereditary hemochromatosis — genetic iron *absorption* disorder (no transfusions): the liver loads first, the heart late — and unlike cirrhosis, cardiac iron is reversible if caught early. Treatment is venesection; both organs are measured
- Pre- and post-chelation comparisons — the T2\* values are the treatment metric

### How this differs from cardiac_non-stress

- **No contrast at all:** the exam is fully native — no post-contrast phase.
- **The heart T2\* replaces the mapping/LGE block (#9):** a multi-echo gradient echo becomes the tissue question — iron shortens native T1 too, but T2\* is the validated biomarker with clinical thresholds, so the T1/T2 maps are omitted.
- **Cines reduced, no flow:** 3C/4C/2C + volumetry only — function is monitored, valvular flow is not the question.
- **A liver phase is appended (#10–13):** the exam finishes at the liver — anatomy + liver T2\*, the whole-body iron read.

### Phase 0 — Surveys & Localizers (#1–#4) — the planning stage

Same planning cascade as `cardiac_non-stress.md` Phase 0 (the localizers here run with iPAT): axial localizer (#1) → pseudo 2C (#2) → pseudo 4C (#3) → SA localizer (#4), prescribed perpendicular to the interventricular septum and parallel to the mitral valve plane, with coverage extending basally to include the left atrium.

### Phase 1 — Cine Function (#5–#8)

Identical cines to `cardiac_non-stress.md` #5–#7, plus the volumetry — which here runs **pre-contrast** (no contrast exists in this exam):
- **`cine_tf2d13_retro_3c` (#5):** bisects LV + outflow tract — the LVOT view: aortic valve motion, AS/AR (aortic stenosis/aortic regurgitation) jets, anteroseptal/inferolateral walls.
- **`cine_tf2d13_retro_4c` (#6):** through the RV angle + LV centre (avoid the aorta on other SA slices) — all four chambers, global function, septal/lateral wall motion.
- **`cine_tf2d13_retro_2c` (#7):** bisects LV, ∥ septum insertion line — LV + LA, anterior/posterior wall motion, mitral valve.
- **`cine_tf2d13_retro_sa_volumetry` (#8):** the contiguous SA stack, diastolic planning, beyond-the-apex to past-the-mitral-valve coverage — EF via modified Simpson's disk summation (mechanism as in cardiac_non-stress #12). Function is monitored because transfusional overload eventually becomes an iron cardiomyopathy.

### Phase 2 — Heart Iron (#9)

**`fl2d5_10echo_heart` (#9) — the heart T2\* measurement:** the exam's core sequence.
    - **How the sequence is built — one excitation, many echoes:** a single RF pulse tips the magnetization, then 10 gradient-echo readouts at increasing TE sample the decay — one echo per image, one breath-hold, gated to a single cardiac phase; the signal decays as e^(−TE/T2\*).
    - **Slice positioning:** a single **mid-ventricular short-axis slice at the papillary muscle level**, planned from the SA localizer — mid-LV, away from the LVOT base and the apex.
    - **The ROI:** the **interventricular septum** — drawn inside the septal myocardium, clear of the blood-pool and epicardial borders (partial volume), and avoiding the RV insertion points. The septum is the safe region: the posterior wall and the lung/liver interfaces distort the decay with off-resonance, while the septum sits furthest from them — its decay is the cleanest monoexponential: plot ln(signal) vs TE, and the slope is −1/T2\*.
    - **The thresholds:** heart T2\* **> 20 ms normal; 10–20 ms mild-moderate overload; < 10 ms severe** — the value that drives chelation urgency and predicts heart-failure risk.

**MOLLI, T2 mapping, and T2\* — sampling cadence matched to each curve's timescale:**
    - **T1 recovery (MOLLI):** the curve lives for seconds (~1000–1100 ms) — one sample per heartbeat, spread across consecutive heartbeats (the B(R)A scheme, cardiac_non-stress).
    - **T2-prep (T2 map):** **spin-echo-prepared** — it refocuses static field inhomogeneities, so it is blind to iron's microscopic field distortions; and each prep builds its own curve, which dies within ~200 ms — one TE per heartbeat, a fresh curve rebuilt every beat.
    - **T2\* (multi-echo GRE):** **gradient echo with no refocusing** — the inhomogeneities act freely, which is why iron shortens T2\* far more than T2; the curve lives for ~40–50 ms — the whole decay fits inside a single heartbeat, sampled as an echo train; repetition across heartbeats only averages for SNR.

### Phase 3 — Liver (#10–#13)

After the heart, the **table repositions to centre the liver** (via the scout views), and the liver block runs — ungated, multi-breath-hold:

**`t2_haste_cor_mbh` (#10):** HASTE coronal, multi-breath-hold — the liver localizer (robust single-shot TSE, motion-tolerant); provides the planning geometry for the axial sequences and the T2\* slice.

**`t2_tse_fs_tra_mbh` (#11):** T2 TSE fat-sat axial — liver anatomy; an iron-laden liver is markedly **dark** on T2W — the visual confirmation of overload before the T2\* quantifies it.

**`t1_vibe_dixon_tra_bh` (#12):** T1 VIBE Dixon axial — the standard liver survey (as in the liver protocols); Dixon adds water/fat separation because steatosis commonly coexists with iron in these patients.

**`fl2d1_14echo_liver` (#13) — the liver T2\* measurement:**
    - **How it is built:** the same multi-echo gradient echo as the heart sequence — one excitation, **14 echoes** at increasing TE, one breath-hold, **ungated** (the liver needs no ECG); the signal decays as e^(−TE/T2\*).
    - **Why 14 echoes vs the heart's 10:** the liver's dynamic range is far broader — a normal liver T2\* is ~25–30 ms, and severe overload plunges below 1.4 ms. The wider echo span covers both ends of that range: long echoes to fit the normal liver's slow decay, short echoes to catch the severely overloaded one. The heart (normal ~40–50 ms, severe < 10 ms) spans a narrower range, so 10 echoes suffice.
    - **Slice positioning:** a single **axial slice through the right lobe**, placed in homogeneous parenchyma — avoiding the large vessels (portal branches, hepatic veins) and the dome edge, whose flow and susceptibility distort the decay.
    - **The ROI:** a large homogeneous region of right-lobe parenchyma, clear of vessels and the liver edge (lung base above, bowel below).
    - **The thresholds:** roughly **> 6.3 ms normal; 2.8–6.3 ms mild; 1.4–2.8 ms moderate; < 1.4 ms severe** at 1.5T (LIC-calibrated) [Confirm local calibration].
    - **Why both organs are measured:** the liver is the storage pool — it loads first and reflects the total body iron; the heart loads late and drives the mortality. Under chelation the liver empties faster than the heart, so the two can disagree — both are followed.

---

## 5. Variations

**Replacing `fl2d*` with `T2StarMap` — the map-based versions:**
    - **`fl2d5_10echo_heart` / `fl2d1_14echo_liver` (standard):** output the **raw echo images**; the T2\* is computed afterwards — you draw the ROI (septum / right-lobe parenchyma) and the software fits the decay inside it, reporting one T2\* value for the region.
    - **`T2StarMap_8echo_heart` / `T2StarMap_12echo_liver` (map versions):** the scanner fits **pixel by pixel, inline** — the output is a finished T2\* map (every pixel carries a value, usually colour-coded) plus a fit-quality map showing where the exponential was clean. Any segment can be read and patchy deposition is seen rather than averaged away — at the cost of a longer acquisition (29 s / 25 s vs 19 s / 18 s).
    - **The trade — and why the standard stays primary:** both are single-slice — the difference is the output, not the coverage. The map is less operator-dependent (no ROI placement), but the fit-quality map must be checked — bad pixels mean bad values. And the validated thresholds (>20 / 10–20 / <10 ms heart) were established on the standard septum-ROI method — so keep the `fl2d*` sequences as the primary, threshold-driven metric, and use the `T2StarMap` versions as the supplement when deposition looks patchy or segmental detail is needed.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **ECG trigger** — lead with the cleanest R wave chosen for gating? | The cardiac sequences (including the T2* echoes) are gated — a poor trigger degrades them all |
| **Breath-hold consistency** — clean end-inspiratory hold on the multi-echo sequences? | Motion during the echo train breaks the exponential fit — the T2* value becomes garbage |
| **Wrap-around** — any wrapping artifact at the image edges? | The cardiac FOV is small — signal outside it (arms, chest wall) can wrap into the image. If wrapping appears, increase the FOV |
| **SAX volumetry contiguous** — no gaps, apex included, basal slice below the annulus? | Simpson's volumes/EF are wrong with missing or partial-volume slices |
| **Heart T2* ROI** — septum measured, fit quality checked? | The septum is the clean ROI (furthest from lung/liver susceptibility); check the decay is a clean exponential — a distorted curve needs a re-acquisition |
| **Liver T2* slice** — right lobe, vessels avoided? | Vessels disrupt the fit — place the slice in homogeneous parenchyma |
| **Field strength** — T2* thresholds match the scanner? | Iron T2* reference values are calibrated at 1.5T — at 3T the values run shorter and the same thresholds do not apply |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-01 | — | Initial build — 13 workflow steps. Non-stress cardiac base minus contrast (localizers + retro cines 3C/4C/2C + pre-contrast SA volumetry) + heart T2* (fl2d5 10-echo, mid-ventricular SA, septum ROI) + liver phase (table reposition, HASTE/TSE FS/VIBE Dixon anatomy, fl2d1 14-echo liver T2*). No contrast, no maps — T2* is the iron biomarker. T2*StarMap options (heart 8-echo, liver 12-echo) as variations |
