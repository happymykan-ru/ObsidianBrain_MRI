# Brachytherapy (Pre-OT) (Cervical Cancer Brachytherapy Planning MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first (treatment position — brachytherapy planning requires the same positioning as the treatment delivery)
- **Coil:** 30-channel body coil anteriorly + spine array. Higher channel count for improved SNR and parallel imaging at high resolution.
- **Laser Landmark:** Centre of body coil
- **Patient Preparation:** Vaginal gel (e.g., ultrasound gel) inserted into the vagina — distends the vaginal fornices and separates the vaginal walls, defining the tumour-vagina interface for brachytherapy contouring.
- **Immobilization:** As per treatment positioning — leg and pelvic supports per the brachytherapy setup.
- **Privacy:** The patient is in a vulnerable position. Cover the patient with blankets. Lower curtains during setup. Minimize exposure and time in the room.
- **Verbal Instructions:** Shallow breathing throughout.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to exam. Paralyses bowel — essential for high-resolution T2 and DCE. Contraindications: glaucoma, urinary retention, myasthenia gravis, tachyarrhythmia.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Vaginal gel** | — | Insert prior to imaging | — | — | — |
| — | **Buscopan** | — | 10–20 mg IV, prior to exam | — | — | — |
| 1 | `t2_tse_true_tra_pelvis_2mm` | Axial | True axial | Whole pelvis. Iliac crest → perineum | **None** | Free breathing |
| 2 | `t2_tse_sag` | Sagittal | True sagittal | Uterus + cervix + vagina. L/R: both parametria + adnexae | **None** | Free breathing |
| 3 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #2 | — | **None** | Free breathing |
| 4 | `t2_tse_obl_cor` | Coronal Oblique | ∥ cervical canal | Tumour + uterine body + cervix + upper vagina. A/P: bladder → rectum | **None** | Free breathing |
| 5 | `t2_tse_obl_tra` | Axial Oblique | ⟂ cervical canal | Tumour + both parametria (to pelvic sidewalls) | **None** | Free breathing |
| 6 | `resolve_diff_b50_1500_obl_tra` | Axial Oblique | Copy Slice from #5 | Tumour only | **A/P** (anterior + posterior skin margins) | Free breathing |
| 7 | `t1_vibe_dixon_true_tra_pelvis` | Axial | True axial | Whole pelvis | **None** | Breath-hold |


### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s. Inject after 1st measurement | — | — | — |
| 8 | `t1_vibe_dixon_sag_dyn_C` | Sagittal | Copy Slice from #2 | Tumour + uterus + cervix | **None** | Shallow breathing. Multiple measurements. Inject contrast after 1st measurement |
| 9 | `t1_vibe_dixon_obl_tra_C` | Axial Oblique | Copy Slice from #5 | Tumour + parametria | **None** | Breath-hold |
| 10 | `t1_vibe_dixon_obl_cor_C` | Coronal Oblique | Copy Slice from #4 | Tumour + uterine body + cervix | **None** | Breath-hold |
| 11 | `t1_vibe_dixon_true_tra_pelvis_delayed` | Axial | Copy Slice from #7 | Whole pelvis | **None** | Breath-hold, delayed |


---

## 3. Sequence Rationale

### Core Strategy

Brachytherapy planning MRI maps the tumour for intracavitary/interstitial radiotherapy delivery. The clinical question: what is the exact tumour volume and its relationship to the applicator, bladder, rectum, and sigmoid? Unlike staging MRI (which answers FIGO stage and nodal status), brachytherapy planning answers a contouring question — where to draw the high-risk CTV (HR-CTV) and what dose constraints apply to adjacent organs at risk.

**Key differences from `Ca_cervix_or_corpus.md` (staging protocol):**

- **Head-first, treatment position** — brachytherapy planning MRI must replicate the position used for treatment delivery. Staging MRI is feet-first.
- **Vaginal gel** — distends the vaginal fornices, separating the vaginal walls and defining the tumour-vagina interface. In staging, the vagina is collapsed and this boundary is ambiguous.
- **30-channel body coil + 2 mm true axial T2** — higher resolution for contouring accuracy. True axial is required because the brachytherapy CT planning system registers images in true axial; oblique planes cannot be fused.
- **DWI b=1500 (not b=800)** — higher b-value suppresses normal cervical stroma and benign tissue signal, making the tumour stand out for volume delineation. Same principle as prostate DWI.
- **Both true axial and oblique axial T2** — true axial for CT fusion; oblique axial for parametrial assessment (same staging rationale).
- **No optional abdomen, no T1 TSE Dixon** — brachytherapy is local treatment planning; nodal staging is already completed on the prior staging MRI.
- **Delayed post-contrast true axial** — contrast enhances the tumour stroma, defining the HR-CTV boundary for contouring. The delayed phase maximizes tumour-to-stroma contrast.

---

### Pre-Contrast

**T2 TSE true axial 2 mm (#1):** High-resolution true axial. The 2 mm slices provide accurate contours for the brachytherapy planning system (GEC-ESTRO guidelines). True axial is essential — the CT-based planning system fuses images in true axial; oblique planes cannot be registered. Coverage includes the entire pelvis from iliac crest to perineum for nodal reference (previously staged).

**T2 TSE sagittal (#2):** The primary sagittal plane. With vaginal gel, the fornices are distended — the tumour-vagina interface and the distance to bladder and rectum are clearest on this plane. The sagittal plane also shows the uterine axis for applicator insertion planning.

**T2 SPACE sagittal (#3):** 3D T2 with MPR — volumetric overview for the radiation oncologist to assess tumour in any plane.

**T2 TSE oblique coronal (#4) + oblique axial (#5):** Same oblique T2 planes as the staging protocol — parallel and perpendicular to the cervical canal. These assess parametrial invasion and craniocaudal extent. In brachytherapy, the oblique axial is particularly important for defining the lateral extent of the HR-CTV (parametrial disease cannot be treated with intracavitary alone — requires interstitial needles).

**DWI b=50, 1500 (#6):** High b-value for tumour conspicuity. The b=1500 image suppresses normal cervix and benign tissue — the tumour stands out as a bright focus. Used for volume delineation: the ADC map (from b=50 and b=1500) identifies the cellular tumour core. PI-RADS prostate DWI principle applied to cervix.

**T1 VIBE Dixon true axial (#7):** Pre-contrast baseline, true axial for CT fusion. In/opposed phase for any incidental findings.

---

### Post-Contrast

**T1 VIBE Dixon sagittal DCE (#8):** Same DCE as the staging protocol — 1st measurement = baseline, contrast injected after. Enhancement kinetics confirm tumour viability and extent.

**T1 VIBE Dixon oblique axial (#9) + oblique coronal (#10):** Post-contrast oblique planes. The enhancing tumour margin defines the HR-CTV boundary. The oblique axial is the primary plane for lateral parametrial extent.

**T1 VIBE Dixon true axial delayed (#11):** Delayed post-contrast true axial — contrast has accumulated in the tumour stroma, maximizing the tumour-to-background contrast for contouring the treatment volume. True axial for direct transfer to the planning system.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Positioning** — Head-first treatment position? Vaginal gel inserted? Patient covered and curtains lowered? | If gel omitted: vaginal fornices collapsed — tumour-vagina interface ambiguous for contouring. Ensure privacy throughout |
| **True axial** — 2 mm T2 true axial (#1) acquired? True axial post-contrast (#11) acquired? | Oblique planes cannot be fused with the planning CT. If only obliques are acquired: contours must be manually transferred — degrades accuracy |
| **DCE timing** — Contrast injected after the 1st measurement | Reminder: inject after 1st measurement, not before |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 11 sequences. Head-first treatment position, vaginal gel, 2 mm true axial T2. DWI b=1500. True axial + oblique T2 planes for planning CT fusion |
