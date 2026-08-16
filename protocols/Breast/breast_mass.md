# Breast Mass (Breast MRI — with Contrast)

**Version:** 1.0 | **Date:** 2026-08-16 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Prone, head-first. Breasts pendent in the dedicated breast coil — they hang freely into the coil openings, no compression. Place a dedicated pillow both proximal and distal to the breast coil to support the chest and pelvis, and a dedicated head rest for the head. Arms placed over the head, each supported on a rolled mattress bundle. Lower the curtains for patient privacy during positioning.
- **Coil:** Dedicated breast coil.
- **Laser Landmark:** Nipple level.
- **Immobilization:** Comfortable prone padding. Instruct the patient to breathe quietly — respiratory motion transmits to the chest wall.
- **IV Access:** Required for this contrast protocol — 20G (pink), standard dose, injection rate minimum 2 mL/s (cannot be slower), saline flush [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_dixon_fast` | Axial | True axial — planned from scout | Above breast parenchyma (axillary tails) → below inframammary folds. Both breasts and both axillae in FOV | **Posterior** |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | Copy coverage from #1 | **Posterior** |
| 3 | `resolve_diff_tra_spair_b50_1000` | Axial | Copy Slice from #1 | Copy coverage from #1 | **Posterior** |
| 4 | `t1_fl3d_tra_VIEWS` | Axial | Copy Slice from #1 | Copy coverage from #1 | **Posterior** |
| 5 | `t1_fl3d_tra_dyn_C` | Axial | Copy Slice from #1 | Copy coverage from #1. Dynamic — contrast injected after first measurement | **Posterior** |
| 6 | `t1_fl3d_tra_VIEWS_C_delay` | Axial | Copy Slice from #1 | Copy coverage from #1 | **Posterior** |

---

## 3. Coverage & Plane Planning

**Axial (all sequences)**
- **Coverage:** Slice direction S→I: above the breast parenchyma (through the axillary tails) → below the inframammary folds. FOV: both breasts and both axillae.
- **Planning:** The axial plane is the standard breast plane — both breasts in one FOV for symmetric side-by-side comparison, chest wall included. The axillae must be in the FOV: the regional lymph nodes are part of the breast MRI question. Plan the axial from the sagittal scout — use the slice that shows the largest sagittal cross-section of the breast; if the scout does not show it, acquire fresh sagittal localizers and plan from those.
- **Phase-encode direction:** L/R. Respiratory and cardiac motion of the chest wall propagates laterally instead of A/P across the breasts.
- **Sat band:** Posterior, over the chest wall and heart — saturating the dominant motion sources (cardiac pulsation, respiratory chest wall motion) that sit directly behind the pendent breasts.

---

## 4. Sequence Rationale

### Core Strategy

Breast MRI answers four questions about a mass: is it a cyst or solid (T2), how cellular is it (DWI/ADC), how does it enhance over time (dynamic kinetics), and what does the enhancing lesion look like at high resolution (delayed morphology). All sequences are axial — the only plane with bilateral comparison.

### Pre-Contrast

**`t2_tse_dixon_fast` (#1):** The **cyst-vs-solid sequence**. Answers: is the lesion a cyst or solid? T2-bright, smooth, well-defined = cyst (benign). Solid masses are T2-intermediate. Also shows edema and chest wall invasion. Dixon (FAST variant) is chosen because the breast has poor B0 homogeneity — glandular-fat interfaces and skin folds break spectral FS; Dixon's fat-water separation is robust. Water-only = the fat-suppressed T2; in-phase = anatomical T2 reference.

**`t1_fl2d_tra` (#2):** The **high-in-plane-resolution pre-contrast T1 anatomy**. 2D FLASH gives the cleanest T1 weighting of the protocol — the anatomy and morphology read happens here. What it looks for: the mass shape and margins (spiculated margins with fat clefts = carcinoma), skin thickening (inflammatory carcinoma, infection), nipple-areolar involvement, chest wall invasion (loss of the fat plane between tumor and pectoralis), enlarged lymph nodes with or without fatty hila, and fat content of lesions. The T1-dark mass stands out against the bright fat background — the contrast that renders this morphology sharply. Quick enough to double as the pre-flight positioning and coverage check before the long acquisitions.

**`resolve_diff_tra_spair_b50_1000` (#3):** The **cellularity sequence**. Answers: how cellular is the lesion? Malignant lesions are hypercellular → restricted diffusion → bright on b1000, dark on ADC. Cysts and benign lesions do not restrict. b50 + b1000 gives the ADC map. RESOLVE (readout-segmented EPI) is chosen over single-shot EPI because it distorts far less at the skin/air interfaces — standard EPI would warp the breast contour. SPAIR fat suppression keeps the bright breast fat from masking the diffusion signal.

**`t1_fl3d_tra_VIEWS` (#4):** The **pre-contrast mask — the "already bright?" answer**. Acquired with identical geometry to the delayed post-contrast VIEWS (#6), the pair answers: was the mass already bright before contrast? Intrinsic T1 signal — fat, hemorrhage, proteinaceous content — is bright on this image and remains unchanged on #6 (and cancels in the subtraction); true enhancement is dark here and bright on #6. This distinction cannot be made on the FL2D (#2) — different contrast, different geometry. The subtraction itself does the same job quantitatively.

### Post-Contrast

**`t1_fl3d_tra_dyn_C` (#5):** The **kinetics sequence**. Multiple rapid post-contrast acquisitions. Malignant masses enhance fast and wash out (type III curve); benign lesions enhance gradually and persistently (type I); type II (plateau) sits between. The time-intensity curve is the single most diagnostic breast MRI feature. Contrast is injected after the first measurement so the baseline is part of the same series.

**`t1_fl3d_tra_VIEWS_C_delay` (#6):** The **enhancement morphology sequence**. Same high-resolution VIEWS, delayed post-contrast, subtracted against #4. This is where the BI-RADS morphology read happens — the morphology of the *enhancing* lesion, distinct from the FL2D's pre-contrast whole-mass morphology: enhancing margins (spiculated = malignant suspicion; smooth = likely benign), internal enhancement pattern (homogeneous vs heterogeneous vs rim — rim favors malignancy/necrosis), and the full extent of enhancing disease (multicentric lesions, skin or chest wall enhancement). Kinetics (#5) says *how fast* it enhances; this pair says *what the enhancing lesion looks like*.

---

## 5. Post-Processing

1. **Rotation MIP — `Rotation_MIP_of_R/L_Breast`** — generated from the 3rd dynamic series (the 2nd post-contrast frame), one MIP per breast, processed separately. Remove the heart from the projection so it does not overlie the breast.

2. **Wash-in map — `Wash_in_map (W___, C___)`** — readjust window width and level to approximately 1100 and 600. Criteria: the background must be black while the colour contrast remains sufficient — adjust until both conditions hold, then record the final values in the series name.

3. **Delayed-phase sagittal MPR — per breast, along the long axis of the breast** — reformatted from the delayed post-contrast VIEWS. Each breast reformatted separately, aligned along its long axis (nipple → midpoint of the breast's chest wall attachment), covering the whole breast out to the skin margin where the breast tissue meets the chest wall.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Positioning** — Breasts fully pendent, no fold/compression? | A folded breast or chest wall contact distorts the parenchyma and mimics or masks lesions. Reposition if the glandular tissue is not fully suspended |
| **Coverage** — Both breasts and both axillae in every sequence? | Clipped axillae lose the nodal assessment; clipped breast tissue misses peripheral lesions. Confirm on the scout before starting. If coverage is insufficient: on the **dynamic** series, **NEVER** change slices per slab — the temporal sampling and frame geometry must stay constant for kinetics; increase slice thickness instead. On the pre/post FL3D VIEWS, increasing slices per slab is allowed — the 4-minute acquisitions have time budget to spare |
| **Fat-water shim** — Frequency peak selected manually, on water? | All breast series use manual frequency peak selection: the breast is predominantly fat, so the tallest peak is fat — select it and add the water-fat shift (3.5 ppm; ≈440 Hz at 3T, ≈220 Hz at 1.5T) to land on water. If the reference frequency sits on fat, spectral FS saturates water instead: fat suppression fails — check the DWI: bright fat signal there confirms the failure |
| **Dynamic injection** — Contrast injected after the first measurement? | The first time point is the baseline for the enhancement curve. If contrast is in before the first acquisition, the baseline is lost and kinetics cannot be computed |
| **R/L labeling** — Correct side confirmed? | Bilateral anatomy — findings must be sided correctly in the report |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-16 | — | Initial — 6 sequences. T2 Dixon FAST + T1 FL2D + RESOLVE DWI b50/1000 + T1 FL3D VIEWS pre + dynamic + delayed VIEWS post-contrast. Breast mass protocol with contrast |
