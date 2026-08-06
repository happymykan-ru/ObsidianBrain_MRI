# CA Cervix / Corpus (Cervical or Endometrial Cancer Staging MRI with Dynamic Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-pelvis.
- **Immobilization:** Pelvic binder.
- **Laser Landmark:** Centre of body coil
- **Verbal Instructions:** Shallow breathing throughout.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to exam. Paralyses bowel — essential for the high-resolution oblique T2 sequences and DCE. Contraindications: glaucoma, urinary retention, myasthenia gravis, tachyarrhythmia.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Survey + Optional Abdomen

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_p3_mbh` | Coronal | True coronal | Abdomen + pelvis. Diaphragm → symphysis pubis | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_trufi_cor_p2_bh_set_n_go` | Coronal | True coronal | Abdomen + pelvis | Copy Sat from #1 | Breath-hold |
| — | **Optional abdomen** | — | If abdominal nodal/metastatic survey is required | — | — | — |
| 3A | `t1_vibe_dixon_tra_p4_bh_upper_abd` | Axial | True axial | Upper abdomen: diaphragm → renal hilum | **None** | Breath-hold |
| 4A | `t1_vibe_dixon_tra_p4_bh_mid_abd` | Axial | True axial | Mid abdomen: renal hilum → iliac crest | **None** | Breath-hold |
| 5A | `t2_tse_fs_tra_p2_mbh_upper_abd` | Axial | Copy Slice from #3A | — | **None** | Multi breath-hold |
| 6A | `t2_tse_fs_tra_p2_mbh_mid_abd` | Axial | Copy Slice from #4A | — | **None** | Multi breath-hold |

*#1: T2 HASTE coronal — whole abdomen + pelvis survey for hydronephrosis, nodal disease, peritoneal deposits.*  
*#3A–#6A: Optional abdominal screen — add if full staging for para-aortic nodes and liver metastases is required. Split into upper and mid abdomen. Skip if staging is pelvis-only.*  

### Pelvis — Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Buscopan** | — | 10–20 mg IV, prior to exam | — | — | — |
| 7 | `t2_tse_sag_pelvis` | Sagittal | True sagittal | Uterus + cervix + vagina. L/R: both ovaries + adnexae | **None** | Free breathing |
| 8 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #7 | — | **None** | Free breathing |
| 9 | `t2_tse_tra_short_axis` | Axial Oblique | ⟂ cervical canal (Ca cervix) or endometrial stripe (Ca corpus) | Tumour + both parametria (to pelvic sidewalls). S/I: above tumour → below vaginal fornices (cervix) or fundus → below cervix (corpus) | **None** | Free breathing |
| 10 | `t2_tse_tra_long_axis` | Coronal Oblique | ∥ cervical canal (Ca cervix) or endometrial stripe (Ca corpus) | Tumour + entire uterine body + cervix + upper vagina. A/P: bladder → rectum | **None** | Free breathing |
| 11 | `t1_tse_fs_dixon_short_axis_pelvis` | Axial Oblique | Copy Slice from #9 | Whole pelvis. Iliac crest → perineum | **None** | Free breathing |
| 12 | `t1_vibe_dixon_short_axis_pelvis` | Axial Oblique | Copy Slice from #9 | Whole pelvis | **None** | Breath-hold |
| 13 | `resolve_diff_b50_800_short_axis` | Axial Oblique | Copy Slice from #9 | Whole pelvis | **A/P** (anterior + posterior skin margins) | Free breathing |

*#9: T2 TSE short axis — perpendicular to the cervical canal or endometrial stripe. Primary staging plane.*  
*#10: T2 TSE long axis — parallel to the cervical canal or endometrial stripe. Craniocaudal extent.*  

### Dynamic Contrast (DCE)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s. Inject after 1st measurement | — | — | — |
| 14 | `t1_vibe_fs_sag_dyn_C_pelvis` | Sagittal | Copy Slice from #7 | Tumour + uterus + cervix | **None** | Shallow breathing. Multiple measurements. Inject contrast after 1st measurement |
| 15 | `t1_vibe_dixon_short_axis_pelvis_C` | Axial Oblique | Copy Slice from #9 | Tumour + parametria / myometrium | **None** | Breath-hold. With subtraction |
| 16 | `t1_vibe_dixon_long_axis_pelvis_C` | Coronal Oblique | Copy Slice from #10 | Tumour + uterine body + cervix | **None** | Breath-hold |
| 17 | `t1_vibe_dixon_sag_pelvis_C` | Sagittal | Copy Slice from #7 | Uterus + cervix | **None** | Breath-hold |

*#14: DCE sagittal — multiple measurements. 1st measurement = pre-contrast baseline. Contrast injected after. Enhancement kinetics of the tumour.*  
*#15: Post-contrast short axis with subtraction. Enhancing tumour against suppressed background.*  
*#16–#17: Post-contrast long axis + sagittal. Anatomical coverage of the enhancing tumour.*  

---

## 3. Sequence Rationale

### Core Strategy

Cervical or endometrial cancer MRI stages local disease for treatment planning. For cervical cancer: tumour size, parametrial invasion, pelvic sidewall extension, nodal disease. For endometrial cancer: depth of myometrial invasion (<50% vs ≥50%), cervical stromal involvement, nodal disease. The protocol combines a whole-abdomen survey (optional), high-resolution oblique T2 through the tumour, whole-pelvis DWI, and dynamic contrast (DCE).

Unlike fibroid MRI (true planes only), this protocol uses oblique planes aligned to the cervical canal (Ca cervix) or endometrial stripe (Ca corpus). These planes are essential: the depth of myometrial invasion and parametrial extension must be measured perpendicular to the wall — the same principle as rectal cancer CRM. True axial slices would cut obliquely through the cervix/myometrium and distort the measurement.

---

### Survey + Optional Abdomen

**T2 HASTE coronal (#1):** Whole abdomen + pelvis survey. Hydronephrosis (ureteric obstruction from parametrial/sidewall extension), para-aortic lymphadenopathy, peritoneal deposits, liver metastases. The coronal plane shows both kidneys, the retroperitoneum, and the pelvic tumour in one view.

**T2 TrueFISP coronal (#2):** Vessels and fluid are bright without contrast. Adds vascular assessment to the HASTE survey — portal vein, IVC, and iliac vessel patency, plus a second overview of bowel and fluid-filled structures. 

**Optional abdomen (#3A–#6A):** Split upper and mid abdomen. T2 TSE FS detects liver metastases, para-aortic nodes against dark fat, and peritoneal deposits. T1 VIBE Dixon provides in/opposed phase for liver lesion characterization, anatomical nodal reference, and bone metastases (T1-dark marrow replacement). Added when abdominal staging is indicated:

- **Cervical cancer:** Tumour >4 cm (FIGO ≥IB2), suspected para-aortic nodes on pelvic sequences, hydronephrosis on the HASTE survey, adenocarcinoma histology (peritoneal spread risk), or pre-treatment planning for radical chemoradiotherapy (para-aortic field decision).
- **Endometrial cancer:** High-grade histology (grade 3, serous, clear cell), deep myometrial invasion (≥50%), suspected advanced stage on pelvic sequences, or pre-treatment planning for extended surgery.

Skip for early-stage, low-risk disease — pelvis-only is sufficient.

---

### Pelvis — Pre-Contrast

**T2 TSE sagittal (#7) + T2 SPACE sagittal (#8):** Both are T2 TSE, same tissue contrast. The difference is dimensionality: T2 TSE (#7) is 2D — higher in-plane resolution, the diagnostic sagittal reference. The tumour is localized — cervical cancer arises from the cervix and extends into the vaginal fornices or uterine body; endometrial cancer distends the endometrial cavity and invades the myometrium. T2 SPACE (#8) is a 3D TSE with isotropic voxels — lower in-plane resolution than 2D TSE, but MPR provides reformatted views in any plane from a single acquisition. If the dedicated oblique planes (#9, #10) are slightly misaligned, the SPACE MPR can salvage them.

**T2 TSE short axis (#9):** Axial oblique, perpendicular to the cervical canal or endometrial stripe. This is the **primary staging sequence**:
- **Cervical cancer:** Parametrial invasion — the dark cervical stromal ring is breached by T2-intermediate tumour extending into the parametrial fat. Intact stromal ring = FIGO stage ≤IB1; breached = ≥IIB. The plane perpendicular to the canal gives a true cross-section of the stromal ring — a true axial slice would cut obliquely and overestimate the apparent stromal thickness.
- **Endometrial cancer:** Depth of myometrial invasion — measured from the endometrial-myometrial junction to the deepest tumour invasion, expressed as a fraction of total myometrial thickness. <50% = FIGO IA; ≥50% = FIGO IB. The oblique plane perpendicular to the endometrial stripe gives a true measurement of invasion depth.

**T2 TSE long axis (#10):** Coronal oblique, parallel to the cervical canal or endometrial stripe. Craniocaudal tumour extent.

**T1 TSE FS Dixon short axis (#11) + T1 VIBE Dixon short axis (#12):** Both are T1 in the short axis plane — why two? T1 TSE Dixon uses a turbo spin echo readout — less susceptible to the air-tissue interface at the cervix and vagina, giving a cleaner anatomical nodal survey. T1 VIBE Dixon is a gradient echo — better for subtraction against the post-contrast VIBE (#15) because the contrast mechanism is identical (both are gradient echo). TSE provides diagnostic nodal anatomy; VIBE provides the pre-contrast subtraction baseline.

**DWI (#13):** b=50, 800, whole pelvis in the short axis plane. Coplanar with the primary T2 staging sequence (#9) for direct correlation.

---

### Dynamic Contrast (DCE)

**T1 VIBE FS sagittal dynamic (#14):** Sagittal DCE. Multiple measurements — the 1st measurement is the pre-contrast baseline; contrast is injected after. Subsequent measurements capture the enhancement kinetics of the tumour. Cervical and endometrial cancers enhance earlier and more avidly than the surrounding myometrium/cervical stroma. The sagittal plane profiles the tumour in its long axis during enhancement. Temporal resolution <10 s for adequate curve analysis.

**T1 VIBE Dixon short axis (#15):** Axial oblique post-contrast, with subtraction. Subtracting the pre-contrast baseline (#12) from the post-contrast image produces a pure enhancement map. The short axis plane (perpendicular to the wall) is where parametrial invasion and myometrial invasion are assessed — enhancement confirms the tumour extent.

**T1 VIBE Dixon long axis + sagittal (#16, #17):** Anatomical coverage of the enhancing tumour in the remaining two planes. The coronal oblique shows the lateral parametrial extent; the sagittal shows the craniocaudal extent and relationship to bladder and rectum.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Oblique planes** — Short axis truly perpendicular to the cervical canal or endometrial stripe? Angulation <45°? | If misaligned: parametrial invasion is overcalled (oblique cut widens the apparent stromal ring) or myometrial invasion depth is miscalculated. Plan from the sagittal T2 (#7) at the level of maximum tumour. Check <45° to prevent Siemens plane swap |
| **DCE timing** — Contrast injected after the 1st measurement | Reminder: inject after 1st measurement, not before |
| **Optional abdomen** — Abdomen series added if full staging required? | If omitted in a cervical cancer with suspected para-aortic nodes: staging is incomplete |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 17 sequences (4 optional). Oblique T2 aligned to cervical canal/endometrial stripe. DCE sagittal + subtraction. Whole pelvis DWI |
