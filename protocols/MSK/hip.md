# Hip (Routine Hip MRI — Non-Contrast)

**Version:** 1.0 | **Date:** 2026-08-11 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first. Both hips should be in the FOV for side-by-side comparison — the axial plane covers both hip joints. Feet in neutral or slight internal rotation (internal rotation brings the femoral neck into the coronal plane).
- **Coil:** Body matrix coil anteriorly + spine array posteriorly. Centre over the pubic symphysis for bilateral coverage.
- **Laser Landmark:** Greater trochanter of the affected side — palpate at the widest point of the lateral hip.
- **Immobilization:** Tie both feet together with a strap and place sandbags on either side of the legs to maintain neutral hip rotation and prevent motion. The pelvis must not shift between sequences.
- **IV Access:** Not required for this non-contrast protocol. [Confirm — add IV if contrast is indicated for specific clinical question.]

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_cor_hip` | True Coronal | True coronal — planned from axial localizer | Both acetabuli and both greater trochanters anteriorly → posteriorly. FOV: Iliac crest → lesser trochanter. | **None** |
| 2 | `t2_tse_fs_cor_hip` | True Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `pd_tse_fs_sag_hip` | True Sagittal | True sagittal — ⟂ coronal, planned from axial localizer | Acetabulum medially → greater trochanter laterally (include full trochanteric insertion). FOV: Iliac crest → lesser trochanter | **None** |
| 4 | `t2_tse_dixon_tra_hip` | True Axial | True axial — ∥ pelvic brim, planned from coronal #1 | Above acetabular roof → below lesser trochanter. Both hips in FOV. Include full lesser trochanter insertion | **None** |
| 5 | `t1_tse_obl_tra_hip` | Oblique Axial | ∥ femoral neck long axis — planned from coronal #1 | Femoral head-neck junction only. Acetabular rim → intertrochanteric line | **None** |

---

## 3. Coverage & Plane Planning

**True Coronal**
- **Coverage:** Slice direction A→P: ASIS → ischial tuberosity (both acetabuli and greater trochanters swept). FOV: Iliac crest → lesser trochanter, both hips.
- **Why:** Both acetabuli are the internal normal reference — AVN and marrow edema are bilateral in 40–70% of cases. Greater trochanters must be fully swept posteriorly: trochanteric pain syndrome is common and easily clipped if the stack is too anterior. Iliac crest captures gluteus medius/minimus origin for tendinopathy grading. Lesser trochanter includes the iliopsoas insertion. Both hips in FOV for side-by-side marrow and joint comparison.

**True Sagittal**
- **Coverage:** Slice direction: acetabulum → greater trochanter lateral cortex (full trochanteric insertion). FOV: Iliac crest → lesser trochanter.
- **Why:** Each sagittal slice profiles the labrum at one clock-face position — anterior (medial) → superior (mid) → posterior (lateral). Stack must reach lateral greater trochanter for gluteal insertions and trochanteric bursitis. Do not extend medially to the pubic symphysis — wastes in-plane resolution on the labrum with no diagnostic yield. Same SI window as coronal for full joint, iliopsoas course, and proximal hamstring origin.

**True Axial**
- **Coverage:** Slice direction S→I: above acetabular roof → below lesser trochanter insertion. FOV: both hips.
- **Why:** Above the roof captures the iliopsoas crossing the anterior joint (internal snapping hip). Below the lesser trochanter captures the iliopsoas insertion — distal tendinopathy and bursitis are missed if the stack stops at the joint. Bilateral FOV is the defining purpose: joint effusion, synovial thickening, and marrow signal are compared side by side.

**Oblique Axial**
- **Coverage:** Slice direction: femoral head-neck junction — acetabular rim → intertrochanteric line. FOV: femoral head-neck cross-section, parallel to femoral neck long axis.
- **Why:** True cross-section for alpha angle measurement. A true axial cuts the femoral neck obliquely and overestimates the angle. Tight stack maximises in-plane resolution — the true axial already covers the full joint.

---

## 4. Sequence Rationale

### Core Strategy

The hip protocol assesses the femoral head (AVN, subchondral fracture, marrow edema), the acetabular labrum (tear, degeneration), the joint space (effusion, synovitis), the surrounding soft tissues (bursitis, tendinopathy), and bony morphology (cam/pincer FAI, acetabular dysplasia). A non-contrast protocol — contrast is added when labral tear confirmation is needed, infection is suspected, or a post-surgical question is asked.

The design pairs a non-FS T1 coronal with a FS T2 coronal in the same plane — anatomy and fluid side by side. A PD FS sagittal profiles the labral ring. A T2 Dixon axial provides robust fat suppression for bilateral comparison. An oblique axial T1 along the femoral neck is the FAI measurement plane.

---

### Pre-Contrast

**T1 TSE coronal (#1):** The **anatomy and marrow sequence**. T1 in the coronal plane profiles the femoral head, acetabular roof, and joint space. Fat is left bright — normal femoral head marrow is T1-bright (fatty). The earliest sign of AVN is a T1-dark subchondral line or segment replacing the normal bright marrow, often well before T2 changes appear. The acetabular sourcil (weight-bearing surface) and proximal femoral morphology are assessed. Non-FS T1 provides the sharpest bone margins and the most sensitive marrow assessment.

**T2 TSE FS coronal (#2):** The **fluid-sensitive counterpart** to #1, in the same coronal plane. T2 with FS makes joint effusion, a labral tear at the superior labrum, and bone marrow edema (transient osteoporosis, AVN progression, subchondral insufficiency fracture) maximally conspicuous. Greater trochanteric bursitis and iliopsoas bursitis are bright against dark fat. Paired with the T1 coronal (#1), the same anatomy is seen in two contrasts — T1 for structure and marrow, T2 FS for fluid and edema.

**PD TSE FS sagittal (#3):** The **labral ring sequence**. The acetabular labrum is a fibrocartilaginous ring — sagittal slices cut through it at sequential positions around the rim. Each sagittal slice profiles the labrum at one clock-face position: anterior on the most medial slices, superior on the mid slices, and posterior on the lateral slices. PD is chosen over T2 for higher SNR — the labrum is a small, thin structure that benefits from signal for crisp margins. FS makes fluid within a labral tear bright. The sagittal plane also profiles the anterior and posterior joint recesses, the iliopsoas tendon, and the proximal hamstring origin.

**T2 TSE Dixon axial (#4):** The **bilateral symmetry sequence**. The axial plane captures both hips in a single slice — joint effusion, synovial thickening, and bone marrow signal are compared side by side. T2 with FS gives fluid conspicuity; Dixon is chosen over spectral FS because the deep pelvis has challenging B0 homogeneity (bowel gas, skin folds, irregular contour) — Dixon water-only provides robust, uniform fat suppression that spectral FS cannot match in this region. The iliopsoas tendon and sciatic nerve are profiled axially.

**T1 TSE oblique axial (#5):** The **FAI measurement plane**. T1 gives the sharpest cortical bone margins. The oblique axial is prescribed parallel to the femoral neck long axis from the coronal (#1) — this provides a true cross-section through the femoral head-neck junction. The alpha angle is measured here for cam-type femoroacetabular impingement: a true axial cuts the femoral neck obliquely and overestimates the offset; the oblique axial gives the correct cross-section. Non-FS T1 also shows the cortical margin for subchondral cyst and herniation pit assessment.

---

## 5. Pathology-Based Variations

**Suspected labral tear / FAI with cartilage concern / pre-operative planning**
- Add `pd_space_cs4_cor_hip` — 3D PD FS isotropic coronal, centred over the affected hip (unilateral). Thin continuous slices through the labral ring catch small tears that can fall between 2D sagittal slices. PD contrast is optimal for articular cartilage. Surgeons use the isotropic dataset for pre-operative planning.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Both hips in coronal and axial FOV** — Bilateral coverage on coronals and axial? | The contralateral hip is the normal reference for marrow signal, joint fluid, and soft tissues. If only one hip is included, side-by-side comparison is lost |
| **R/L annotation on sagittal and oblique axial** — Correct side labelled on #3 and #5? | Sagittal and oblique axial are unilateral planes — only one hip is imaged. The wrong R/L label misattributes pathology to the wrong side |
| **Oblique axial alignment** — #5 truly parallel to the femoral neck? | A true axial or an incorrectly angled oblique axial overestimates the alpha angle. Confirm the plane parallels the femoral neck long axis on both coronal and sagittal views |
| **Labral coverage on sagittal** — All labral positions profiled? | The sagittal stack must extend from medial (anterior labrum) to lateral (posterior labrum). If the stack is too narrow, a focal tear at the 3 or 9 o'clock position is missed |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-11 | — | Initial — 5 sequences. T1 cor + T2 FS cor + PD FS sag + T2 Dixon axial + T1 oblique axial (FAI). Non-contrast hip protocol |
