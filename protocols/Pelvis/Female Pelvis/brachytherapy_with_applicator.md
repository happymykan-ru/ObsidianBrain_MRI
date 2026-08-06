# Brachytherapy (With Applicator) (Cervical Cancer Brachytherapy Verification MRI)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first (treatment position)
- **Coil:** 30-channel body coil anteriorly + spine array.
- **Laser Landmark:** Centre of body coil
- **Immobilization:** As per treatment positioning — leg and pelvic supports.
- **Safety — Applicator:** The brachytherapy applicator (tandem and ring/ovoids) protrudes from the vagina. When moving the patient into the bore: advance the table slowly. Ensure the applicator does not contact the bore wall or coil. Have a second person guide the applicator if needed. Confirm clearance before starting the scan.
- **Privacy:** The patient is in a vulnerable position with instrumentation. Cover the patient with blankets. Lower curtains during setup. Minimize exposure and time in the room.
- **Verbal Instructions:** Shallow breathing throughout. Do not move — the applicator position must not shift.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to exam. Paralyses bowel. Contraindications: glaucoma, urinary retention, myasthenia gravis, tachyarrhythmia.
- **IV Access:** Not required — non-contrast protocol. The applicator position is verified on T2 anatomy; no enhancement assessment is needed.

---

## 2. Imaging Series

| 1 | `t2_tse_true_tra_pelvis_2mm` | Axial | True axial | Whole pelvis. Iliac crest → perineum | **None** | Free breathing |
| 2 | `t2_tse_obl_sag` | Oblique Sagittal | ∥ applicator axis | Applicator + uterus + cervix + vagina | **None** | Free breathing |
| 3 | `t2_tse_obl_cor` | Oblique Coronal | ∥ applicator axis | Applicator + uterus + cervix | **None** | Free breathing |
| 4 | `t2_tse_obl_tra` | Oblique Axial | ⟂ applicator axis | Applicator + cervix + parametria | **None** | Free breathing |

*Oblique planes (#2–#4) are planned from localizers — see workflow section for the full step-by-step method.*  

---

## 3. Sequence Rationale

### Core Strategy

This is the brachytherapy verification scan — the applicator is in place and its position must be confirmed before treatment delivery. The clinical question: is the applicator centred within the cervix, and are the distances to organs at risk (bladder, rectum) consistent with the pre-OT treatment plan? If the applicator has shifted relative to the plan, the dose distribution changes — the tumour may be underdosed or organs at risk overdosed.

The true transverse oblique axial (#4) is the key plane: a cross-section perpendicular to the applicator axis shows the applicator as a perfect circle centred within the cervical stroma. The physicist measures the distance from the applicator to the parametria, bladder, and rectum on this plane and compares it to the pre-OT plan.

**Key differences from `brachytherapy_pre-OT.md`:**

- **Applicator in situ** — the oblique planes are planned along the applicator axis (the tandem), not the native cervical canal. The applicator may alter the uterine axis (straightens an anteverted uterus), so planes planned from the native anatomy on the pre-OT scan may not match the applicator position.
- **No contrast, no DWI, no DCE** — verification, not tumour delineation. The tumour was already contoured on the pre-OT scan.
- **Sequential oblique planning** — the planes are obtained stepwise from localizers (TruFi 2D → oblique coronal localizer → sagittal localizer → diagnostic sequences). See workflow below.
- **Oblique axial = true transverse of the cervix** — the plane perpendicular to the applicator axis is the true cross-section of the cervix. The physicist checks the applicator position relative to the parametria, bladder, and rectum on this plane.

---

### Sequential Planning Workflow — How the True Cross-Sectional Oblique Axial (#4) Is Obtained

Each plane is planned from the previous acquisition. The applicator has two degrees of tilt — A/P (the tandem angled anteriorly/posteriorly) and L/R (angled left/right). These are corrected sequentially:

1. **TruFi 2D localizer:** Quick 3-plane scout. The applicator is visible.

2. **Oblique coronal localizer:** Planned from the sagittal TruFi view — draw a line along the applicator. Corrects **A/P tilt only**. The L/R tilt is not yet corrected.

3. **Sagittal localizer:** Planned from the oblique coronal localizer. On the A/P-corrected coronal, the L/R deviation of the tandem is now visible. Draw a sagittal line along the tandem — both **A/P and L/R tilts are now corrected**. This is the first fully aligned view.

4. **True axial pelvis (#1):** Standard true axial, no tilting. Pelvic anatomical reference. The applicator will appear oblique/elliptical on this plane — that is expected.

5. **Oblique sagittal (#2):** Copies the geometry of the sagittal localizer — both tilts are already corrected. Higher resolution.

6. **Oblique coronal (#3):** Planned from #2. On the oblique sagittal: rotate 90°, then tilt along the long axis of the tandem. The resulting plane is parallel to the applicator in the coronal plane — profiles the tandem and ring/ovoids.

7. **Oblique axial (#4 = true transverse):** Perpendicular to **both** #2 and #3. The resulting plane is a **true cross-section of the cervix**. If #2 and #3 were correctly aligned, the applicator appears as a **perfect circle** — the verification of correct tilt. Distance to parametria (lateral), bladder (anterior), and rectum (posterior) is measured here.

---

## 4. Post-Acquisition Workflow

1. **Check with physicist:** Review the true transverse oblique axial (#4) with the medical physicist. Confirm the applicator position is acceptable and the images are suitable for treatment planning.
2. **Send to Varian:** Export images to the Varian treatment planning system via Terarecon. Ensure all oblique planes (#2, #3, #4) and the true axial (#1) are sent.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Applicator safety** — Clear of the bore and coil? Patient not moving? | Advance table slowly. A second person guides the applicator. Confirm clearance before scanning. If the patient moves: the applicator may shift — re-check position before treatment delivery |
| **Oblique planes** — All planes planned from the applicator axis, not the native cervical canal? | The applicator may straighten the uterus — planes planned from the pre-OT scan may not match. Always plan from the applicator as seen on the localizers |
| **True transverse (#4)** — Scroll through the slices: does the applicator stay in the same position on every slice? | If the applicator shifts from slice to slice: the plane is not truly perpendicular — it cuts obliquely through the applicator. A correctly perpendicular plane shows the applicator as a stationary circle in cross-section on all slices. Confirm with the physicist before sending |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 4 sequences. Applicator in situ, sequential oblique planning from localizers. Non-contrast verification protocol |
