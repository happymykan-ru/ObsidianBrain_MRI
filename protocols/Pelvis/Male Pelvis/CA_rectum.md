# CA Rectum (Rectal Cancer Staging MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-pelvis.
- **Immobilization:** Pelvic binder.
- **Laser Landmark:** Center of body coil
- **Verbal Instructions:** Shallow breathing throughout.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to the exam. Reduces rectal peristalsis — essential for high-resolution oblique T2 sequences where bowel motion degrades the CRM measurement. Contraindications: glaucoma, urinary retention, myasthenia gravis, tachyarrhythmia.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Buscopan** | — | 10–20 mg IV, prior to exam | — | — | — |
| 1 | `t2_tse_sag_3mm_rectum` | Sagittal | True sagittal | Rectum + mesorectum. Sacral promontory → anal verge | **None** | Free breathing |
| 2 | `t2_spc_sag_rectum` | Sagittal | Copy Slice from #1 | — | **None** | Free breathing |
| 3 | `t2_tseR_long_axis_3mm_rectum` | Coronal Oblique | ∥ rectal wall at tumour level (craniocaudal tumour extent) | Tumour-bearing segment. A/P: sacrum → bladder | **None** | Free breathing |
| 4 | `t2_tseR_short_axis_3mm_rectum` | Axial Oblique | ⟂ rectal wall at tumour level (through-plane tumour depth) | Tumour-bearing segment + mesorectal fascia | **None** | Free breathing |
| 5 | `t1_vibe_dixon_short_axis(plain cut only)` | Coronal Oblique | Copy Slice from #4 | Pelvic nodes. Iliac bifurcation → anal verge | **None** | Breath-hold |

*#1: T2 TSE sagittal 3 mm — high-resolution tumour localization and distance from the anal verge.*  
*#2: T2 SPACE sagittal — 3D T2 with MPR. Isotropic reformats for any plane.*  
*#3: T2 TSE long axis — coronal oblique, parallel to the rectal wall. Craniocaudal tumour extent.*  
*#4: T2 TSE short axis — axial oblique, perpendicular to the rectal wall. Primary plane for T-stage and CRM.*  
*#5: T1 VIBE Dixon — pelvic nodal survey. Only the plain (pre-contrast) cut is needed if no dynamic contrast is planned.*  

### Decision — Low Rectal Tumour (0–5 cm from anal verge)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 6 | `t2_tseR_long_axis_3mm_anus` | Axial Oblique | ⟂ anal canal | Anal canal + sphincter complex | **None** | Free breathing |
| 7 | `t2_tseR_short_axis_3mm_anus` | Coronal Oblique | ∥ anal canal | Anal canal + sphincter complex | **None** | Free breathing |

*If tumour is >5 cm from the anal verge, skip #6–#7. The sphincter complex is not at risk; standard rectal sequences suffice.*  
*#6–#7: Dedicated high-resolution anal canal sequences. Same oblique principle as the tumour sequences, but centred on the anal canal and sphincter complex.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s | — | — | — |
| 8 | `t1_vibe_dixon_short_axis_rectum_dyn_C` | Axial Oblique | Copy Slice from #4 | —. Pelvic nodes included. Extend slab if tumour involves anus | **None** | Breath-hold |
| 9 | `t1_vibe_dixon_sag_C` | Sagittal | Copy Slice from #1 | — | **None** | Breath-hold |
| 10 | `t1_vibe_dixon_long_axis_C` | Coronal Oblique | Copy Slice from #3 | — | **None** | Breath-hold |
| 11 | `resolve_diff_b50_800_short_axis` | Coronal Oblique | Copy Slice from #4 | Tumour only | **A/P** (anterior + posterior skin margins) | Free breathing |

*#8–#10: Post-contrast T1 in all three planes. Enhancing tumour, nodes, and extramural vascular invasion.*  
*#11: DWI b=50, 800. Restricted diffusion in the primary tumour and involved nodes.*  

---

## 3. Sequence Rationale

### Core Strategy

Rectal cancer MRI stages local disease for treatment planning: T-stage (depth of invasion through the rectal wall into mesorectal fat), CRM status (distance of tumour to the mesorectal fascia — ≤1 mm = threatened), N-stage (mesorectal and pelvic sidewall nodes), and EMVI (extramural venous invasion). The protocol is built around high-resolution oblique T2 sequences aligned to the tumour-bearing segment, supplemented by DWI and post-contrast T1.

All oblique sequences are aligned to the lumen of the tumour-bearing segment, not the external rectal wall. The tumour grows within the lumen and invades through the wall — the CRM is measured from the deepest point of tumour invasion to the mesorectal fascia. Aligning the plane to the luminal axis ensures it is truly perpendicular to the direction of invasion; planning off the external wall can be distorted by the tumour itself, overestimating the CRM. The rectum curves along the sacral hollow — true axial slices cut obliquely through the wall; oblique planes give true cross-sections.

---

### Pre-Contrast

**T2 TSE sagittal 3 mm (#1):** High-resolution sagittal. The primary sequence for tumour localization — measures the distance from the lower tumour edge to the anal verge (determines surgical approach: low anterior resection vs abdominoperineal resection). Also shows the relationship to the peritoneal reflection (anteriorly, at the level of the seminal vesicles/prostate or cervix/uterus).

**T2 SPACE sagittal (#2):** 3D T2 with isotropic resolution. MPR provides reformatted oblique axial and coronal views aligned to the tumour. SPACE also gives a volumetric overview of the mesorectum and pelvic sidewall nodes.

**T2 TSE long axis (#3):** Coronal oblique, parallel to the rectal wall at the tumour level. Profiles the craniocaudal tumour extent, the relationship to the peritoneal reflection, and the pelvic sidewall. The levator ani and pelvic floor relationship is assessed for low tumours.

**T2 TSE short axis (#4):** Axial oblique, perpendicular to the rectal wall at the tumour level. This is the **primary sequence for T-stage and CRM**. The mesorectal fascia appears as a thin dark line surrounding the mesorectal fat. The distance from the deepest tumour invasion to the fascia is measured on this sequence — ≤1 mm = CRM threatened. The layers of the rectal wall and extramural venous invasion (EMVI) are assessed on this plane.

**T1 VIBE Dixon (#5):** Pelvic nodal survey. Nodes are assessed on T1 (size, contour, signal). Pre-contrast only — if no dynamic contrast is planned, this single pre-contrast acquisition suffices for nodal assessment.

---

### Low Rectal Tumour Decision

Tumours 0–5 cm from the anal verge involve or threaten the anal sphincter complex. Dedicated high-resolution oblique sequences through the anal canal (#6, #7) are added — same T2 TSE technique as the tumour sequences, but centred on the anal canal. The relationship of tumour to the internal and external anal sphincters determines whether sphincter-sparing surgery (low anterior resection) or abdominoperineal resection (APR — removal of rectum and anus with permanent colostomy) is appropriate. If the tumour is >5 cm from the verge, the sphincter complex is not at risk and these sequences are skipped.

---

### Post-Contrast

**T1 VIBE Dixon (#8–#10):** Post-contrast T1 in all three planes. The short axis (#8) covers pelvic nodes (the primary nodal plane); the sagittal and long axis are anatomical overview of the tumour. Enhancing tumour, nodes, and EMVI. The dynamic acquisition (#8) provides enhancement kinetics; if the tumour extends to the anus, adjust the slab to cover the entire tumour.

**DWI (#11):** b=50, 800. The primary tumour is cellular (restricted diffusion). Involved mesorectal nodes also show restricted diffusion. DWI helps distinguish tumour from benign fibrosis in the post-treatment setting (fibrosis is dark on DWI; viable tumour is bright at high b-value). The short axis plane aligns DWI to the same plane as the primary T2 diagnostic sequence (#4) for direct correlation.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Oblique planes** — Aligned to the lumen of the tumour-bearing segment? Angulation <45° from true axial/coronal? | If planes are misaligned: CRM is overestimated. If angulation exceeds 45°: the plane direction is swapped (Siemens inverts phase/slice axes). Plan from the sagittal T2 (#1) at the level of deepest invasion, following the lumen, not the external wall |
| **Low tumour** — Anal canal sequences (#6, #7) added if tumour is 0–5 cm from the anal verge? | If omitted: sphincter involvement cannot be assessed — surgical planning is incomplete. Measure the distance on the sagittal T2 (#1) before proceeding to the oblique sequences |
| **DWI** — b=800 tumour conspicuity adequate? Fat suppressed on b=50? | Same DWI quality checks as prostate.md |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 11 sequences (7 pre + 4 post). Oblique T2 aligned to tumour. Low rectal tumour addendum. DWI b=50/800 |
