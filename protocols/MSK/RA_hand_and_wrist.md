# RA Hand and Wrist (Rheumatoid Arthritis — Bilateral, with Contrast)

**Version:** 1.0 | **Date:** 2026-08-17 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first, "superman" — both hands placed side by side above the head on a dedicated large pillow, palms up, fingers together. [Confirm — both hands at the sides is an alternative if overhead positioning is not tolerated.]
- **Coil:** Body coil — a dedicated hand and wrist coil fits one hand only; the body coil covers both hands side by side in one FOV.
- **Laser Landmark:** Level of the MCP joints.
- **Immobilization:** Small soft pads between the hands to maintain side-by-side position; cover with a mattress and secure with a strap.
- **IV Access:** Required for this contrast protocol — 20G (pink), standard dose, saline flush [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_cor_RA_hand_wrist` | Coronal | ∥ metacarpal long axis — planned from axial localizer | Dorsal skin → volar skin. Distal radioulnar joint → PIP joints, both hands | **None** |
| 2 | `t2_tse_dixon_cor_RA_hand_wrist` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `t1_tse_tra_RA_hand_wrist_R/L` | Axial | ⟂ metacarpal long axis — planned from coronal #1. Separate blocks per hand (R and L) | Distal radioulnar joint → PIP joints, per hand | **None** |
| 4 | `t2_tse_dixon_tra_RA_hand_wrist_R/L` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |
| — | **Contrast** | — | Standard dose. | — | — |
| 5 | `t1_tse_dixon_cor_RA_hand_wrist_C` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 6 | `t1_tse_dixon_tra_RA_hand_wrist_R/L_C` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |

---

## 3. Coverage & Plane Planning

**Coronal**
- **Coverage:** dorsal skin → volar skin. FOV: distal radioulnar joint → PIP joints, both hands side by side.
- **Planning:** Parallel to the metacarpal long axis, planned from the axial localizer — both hands lie in one FOV for side-by-side symmetry comparison. The DRUJ and wrist joints must be included (RA targets the wrist aggressively), and the FOV extends distally to the PIP joints (the MCP and PIP are the classic erosion sites).

**Axial**
- **Coverage:** Separate block per hand (R and L), perpendicular to the metacarpal long axis, planned from the coronal. Same proximal-distal extent: distal radioulnar joint → PIP joints.
- **Planning:** The axial cross-sections the joints and the flexor/extensor tendon sheaths — erosion depth and tenosynovitis are assessed here. One block cannot cover both hands at this resolution; each hand gets its own stack.

---

## 4. Sequence Rationale

### Core Strategy

RA is a bilateral, symmetric polyarticular disease — the question is not detailed anatomy of one structure but presence, distribution, and activity of inflammation across many small joints on both sides at once. Three hallmarks drive the protocol: **erosions** (non-FS T1: dark cortical defects against bright marrow), **bone marrow edema/osteitis** (FS T2: the pre-erosive sign of active disease), and **enhancing synovitis/pannus** (post-contrast T1: the defining feature of active RA). Every sequence serves one of these three — no DWI, no dynamic, no anatomy-for-its-own-sake.

### Pre-Contrast

**`t1_tse_cor` (#1):** The **erosion sequence**. Non-FS T1 gives the sharpest cortex — erosions are dark defects in the bright marrow at the bare areas of the MCP, PIP, and wrist joints. Coronal: both hands side by side, all joints compared at once.

**`t2_tse_dixon_cor` (#2):** The **edema sequence**. Water-only shows bone marrow edema (osteitis) — the earliest, pre-erosive sign of active RA — plus joint fluid and tenosynovitis. Dixon is chosen because the wide two-hand FOV has variable B0 homogeneity; its fat-water separation stays robust where spectral FS would fail. In-phase serves as the T2 anatomy reference.

**`t1_tse_tra_R/L` (#3):** Erosion anatomy in cross-section — joint and tendon-sheath detail in the second plane, per hand.

**`t2_tse_dixon_tra_R/L` (#4):** Fluid in the joints and tendon sheaths in cross-section — tenosynovitis and joint effusion localized per hand.

### Post-Contrast

**`t1_tse_dixon_cor_C` (#5):** The **activity sequence**. Enhancing synovium/pannus = active inflammation; non-enhancing = inactive or chronic disease. The Dixon water-only gives the fat-suppressed T1 for enhancement conspicuity, robust across the large FOV.

**`t1_tse_dixon_tra_R/L_C` (#6):** Enhancement localized per joint and per tendon sheath in cross-section.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **R/L labeling** — Separate axial blocks correctly labeled R and L? | Two hands, separate stacks — the single biggest mislabeling risk in this protocol. Confirm each axial block's side before and after acquisition |
| **Coverage** — Wrist, MCP, and PIP joints all included on both hands? | RA targets all three levels. Confirm the coronal FOV spans distal radioulnar joint → PIP joints with both hands fully inside |
| **Fat-water shim** — Dixon water-fat separation intact? | The large two-hand FOV stresses B0 — check the water-only images for water-fat swap or residual fat. If the separation fails, re-shim or consider swapping to STIR |
| **Post-contrast** — Contrast given, enhancement visible? | Enhancing synovitis is the defining sign of active RA. Confirm enhancement is seen before completing the exam |
| **Positioning** — Both hands flat and side by side? | A rotated or tilted hand distorts joint assessment and breaks the side-by-side symmetry. Reposition if the hands are not flat |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-17 | — | Initial — 7 sequences (+ contrast). T1 cor + T2 Dixon cor + T1/T2 Dixon axial per hand. Post-contrast: T1 Dixon cor + T1 Dixon axial per hand. Bilateral RA hand and wrist protocol with contrast |
