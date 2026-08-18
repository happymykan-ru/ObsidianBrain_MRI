# Arthrogram (MR Arthrography — Wrist / Hip / Knee)

**Version:** 1.0 | **Date:** 2026-08-17 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

Positioning and coil setup follow the respective routine joint protocols (wrist.md, hip.md, knee.md) — the joint in question is imaged identically. The arthrogram-specific step is the intra-articular injection:

- **Injection:** Intra-articular dilute gadolinium (~1:200 dilution) injected before the patient enters the magnet, or under MR guidance depending on local workflow [Confirm]. Full-strength gadolinium is too dark (T2* effects at high concentration); diluted, it is T1-bright.
- **IV Access:** Not required — the contrast is intra-articular, not intravenous.

---

## 2. Imaging Series

### Wrist Arthrogram

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_tra_wrist` | Axial | ∥ radiocarpal joint line | Proximal to DRUJ → CMC joints | **None** |
| 2 | `t2_tse_fs_tra_wrist` | Axial | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `t1_tse_cor_wrist` | Coronal | ∥ long axis of carpus | Dorsal skin → volar skin | **None** |
| 4 | `pd_tse_fs_cor_wrist` | Coronal | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 5 | `pd_tse_fs_sag_wrist` | Sagittal | ⟂ radiocarpal joint line | Radial styloid → ulnar styloid | **None** |
| 6 | `t2_me3d_cor_wrist` | Coronal | Copy Slice from #3 | Copy coverage from #3. Isotropic voxels for MPR | **None** |
| — | **Arthrogram** | — | Intra-articular dilute gadolinium (~1:200). Distension confirmed before scanning | — | — |
| 7 | `t1_tse_fs_tra_wrist_C` | Axial | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 8 | `t1_tse_fs_cor_wrist_C` | Coronal | Copy Slice from #3 | Copy coverage from #3 | **None** |

### Hip Arthrogram

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_cor_hip` | Coronal | True coronal | Both acetabuli, both greater trochanters. FOV: iliac crest → lesser trochanter | **None** |
| 2 | `t2_tse_fs_cor_hip` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `pd_tse_fs_sag_hip` | Sagittal | True sagittal | Acetabulum → greater trochanter | **None** |
| 4 | `t2_tse_dixon_tra_hip` | Axial | True axial | Above acetabular roof → below lesser trochanter. Both hips | **None** |
| — | **Arthrogram** | — | Intra-articular dilute gadolinium (~1:200). Distension confirmed before scanning | — | — |
| 5 | `t1_tse_fs_cor_hip_C` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 6 | `t1_tse_fs_sag_hip_C` | Sagittal | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 7 | `t1_tse_fs_obl_tra_hip_C` | Oblique Axial | ∥ femoral neck long axis | Femoral head-neck junction | **None** |

### Knee Arthrogram

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_fs_sag_knee` | Sagittal | ∥ ACL course | Medial → lateral femoral condyles | **None** |
| 2 | `pd_space_sag_knee` | Sagittal | Copy Slice from #1 | Copy coverage from #1. Isotropic voxels for MPR | **None** |
| 3 | `t1_se_tra_knee` | Axial | ∥ tibial plateau | Above patella → below tibiofibular joint | **None** |
| 4 | `pd+t2_tse_fs_tra_knee` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 5 | `pd_tse_fs_cor_knee` | Coronal | ⟂ tibial plateau | Half patella → popliteal fossa | **None** |
| — | **Arthrogram** | — | Intra-articular dilute gadolinium (~1:200). Distension confirmed before scanning | — | — |
| 6 | `t1_tse_fs_sag_knee_C` | Sagittal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 7 | `t1_tse_fs_tra_knee_C` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 8 | `t1_tse_fs_cor_knee_C` | Coronal | Copy Slice from #5 | Copy coverage from #5 | **None** |

---

## 3. Sequence Rationale

### Core Strategy

MR arthrography answers a question the routine protocol can only suggest: **is this intra-articular structure actually perforated?** Intra-articular dilute gadolinium distends the joint, and the T1-bright contrast enters any communication with the joint cavity — a TFCC perforation, a labral tear, a meniscal re-tear. Contrast inside the defect is direct, mechanical evidence of the tear, not an inference from fluid signal.

The three-part structure, common to all regions:

1. **Pre-arthrogram = the routine joint protocol's pre-contrast set** — the native joint state (effusion, marrow edema, anatomy) must be captured before the injection: once the joint is distended, the native fluid state is replaced and unrecoverable.
2. **Intra-articular injection** — dilute gadolinium (~1:200); full strength would be too dark on T1 due to T2* effects.
3. **Post-arthrogram = T1 FS in the planes that profile the target structure** — the dilute contrast is T1-bright against dark fat.

The contrast route is the fundamental difference from the routine protocols: **intra-articular** (outlining the joint cavity) vs **intravenous** (enhancing vascularized tissue). The question is "is the structure intact?", not "is there enhancing inflammation?"

### Wrist

The wrist arthrogram targets the **TFCC and intrinsic ligaments**. Pre-contrast is the routine wrist set with one change: the sagittal is PD FS instead of T2 FS — the labral-style detail preference. Post-contrast: coronal + axial T1 FS — contrast crossing the TFCC disc (communication between the ulnar and radiocarpal compartments) or crossing the scapholunate/lunotriquetral ligament proves the tear.

### Hip

The hip arthrogram targets the **labrum**. Pre-contrast is the routine hip set minus the oblique axial T1 (the FAI measurement plane) — the oblique plane's role here is post-contrast. Post-contrast: coronal + sagittal + oblique axial T1 FS — three planes because the labrum is a ring; the oblique axial (along the femoral neck) catches tears the two standard planes miss.

### Knee

The knee arthrogram targets **post-surgical menisci and articular cartilage**. Pre-contrast is the routine knee set, kept intact — meniscal morphology (T1 SE) and the 3D SPACE anatomy remain valuable before injection. Post-contrast: all three planes T1 FS — sagittal for the meniscal horns, coronal for the bodies and roots, axial for the patellofemoral cartilage. Contrast entering a post-repair meniscal tear proves re-tear; contrast outlining a cartilage defect proves full-thickness loss.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Injection** — Intra-articular placement confirmed? | Contrast in the soft tissues (not the joint) ruins the exam — the joint cavity will not distend and no defect can be outlined. Confirm intra-articular placement before scanning |
| **Dilution** — Contrast dilute (~1:200)? | Full-strength gadolinium is too dark on T1 — the joint fills with signal void and tears cannot be seen. Confirm the dilution before injection |
| **Distension** — Joint adequately distended? | Inadequate distension fails to drive contrast into defects — a real tear can be missed. Confirm capsular distension on the first post-contrast images |
| **Pre-contrast completion** — All pre-injection sequences acquired before the arthrogram? | Once the joint is distended with contrast, the native effusion and marrow edema state is lost — pre sequences cannot be recovered afterward |
| **R/L labeling** — Correct side confirmed on all sequences? | Same as the respective routine protocols |
| **Post-contrast planes** — All target planes acquired post-injection? | Wrist: cor + axial. Hip: cor + sag + oblique axial. Knee: sag + tra + cor. A missing plane leaves part of the target structure unassessed |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-17 | — | Initial — three regional arthrogram protocols. Wrist: routine pre (sagittal PD FS) + T1 FS cor/tra post. Hip: routine pre minus oblique axial + T1 FS cor/sag/obl tra post. Knee: routine pre + T1 FS three-plane post. Intra-articular dilute gadolinium |
