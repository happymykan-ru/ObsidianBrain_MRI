# Renal Volume (Renal Volumetry MRI)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the kidneys.
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** End-expiration breath-holds preferred. Consistent breath-hold depth across all sequences.
- **IV Access:** Not required — non-contrast protocol.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both kidneys | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t1_vibe_dixon_cor_bh` | Coronal | True coronal | Both kidneys | **None** | Breath-hold |
| 3 | `t2_haste_fs_obl_cor_mbh` (R then L) | Oblique Coronal | ∥ long axis of each kidney | Entire kidney per side | **None** | Multi breath-hold |
| 4 | `t2_haste_fs_obl_sag_mbh` (R then L) | Oblique Sagittal | ∥ long axis of each kidney | Entire kidney per side | **None** | Multi breath-hold |
| 5 | `t2_haste_fs_obl_tra_mbh` (R then L) | Oblique Axial | ⟂ long axis of each kidney | Entire kidney per side | **None** | Multi breath-hold |

*#1–#2: Standard coronal survey + T1 Dixon for anatomy and fat assessment.*  
*#3–#5: Oblique planes per kidney, right side first then left. The kidneys are not aligned with the cardinal body planes — each is imaged along its own long axis (oblique coronal and sagittal) and perpendicular to it (oblique axial).*  

---

## 3. Sequence Rationale

### Core Strategy

Renal volume measurement for pre-transplant assessment or polycystic kidney disease monitoring. The clinical question is purely anatomical: what is the volume of each kidney? No contrast, no DWI, no lesion characterization.

The kidneys are retroperitoneal organs angled obliquely — the upper poles are more posterior and medial, the lower poles more anterior and lateral. Each kidney tilts slightly differently. Measuring length on a true coronal underestimates kidney size because the kidney is cut obliquely rather than along its true long axis. Accurate volume measurement requires:
- **Oblique coronal** along the long axis → true craniocaudal length (CCC measurement)
- **Oblique sagittal** along the long axis → orthogonal confirmation of length
- **Oblique axial** perpendicular to the long axis → true cross-sectional area at each level, summed (area × slice thickness) for volume

Each kidney is imaged separately because their axes differ.

---

### Positioning Workflow

The goal is to align three planes to each kidney's individual long axis. The kidneys are oblique in both L/R (upper pole medial, lower pole lateral) and A/P (upper pole posterior, lower pole anterior). Correcting for both requires an intermediate step:

1. **True coronal + axial localizer:** Standard scouts — both kidneys visible. The coronal shows the L/R tilt of each kidney; the axial shows the kidneys in cross-section.

2. **Oblique sagittal localizer:** On the true coronal localizer, draw an oblique sagittal line along the L/R tilt of the kidney (upper pole to lower pole). This produces a **pseudo-sagittal** image — corrected for L/R tilt but **not yet for A/P tilt**. At this stage, the kidney's A/P angulation (upper pole posterior, lower pole anterior) is now visible on this image.

3. **True oblique coronal:** On the oblique sagittal localizer, draw a line along the kidney's true long axis — the A/P tilt is now visible and can be corrected. This produces the **true oblique coronal** — fully aligned to the kidney's long axis in both L/R and A/P. This gives the true craniocaudal length for measurement.

4. **True oblique sagittal + true oblique axial:** From the true oblique coronal, prescribe both remaining planes: the **true oblique sagittal** (along the long axis — orthogonal confirmation of length) and the **true oblique axial** (perpendicular to the long axis — true cross-sections for volume calculation, with no geometric distortion from oblique slicing).

---

### Sequence Details

**T2 HASTE coronal (#1):** Standard true coronal survey. Shows both kidneys in overview — size, position, cysts, hydronephrosis.

**T1 VIBE Dixon coronal (#2):** Coronal T1 for anatomical reference. In/opposed phase for fat assessment if needed.

**Oblique coronal (#3 R/L):** T2 HASTE FS, prescribed parallel to the long axis of each kidney from the sagittal oblique localizer. The kidney is profiled in its true craniocaudal length. FS suppresses peri-renal fat, making the kidney contour crisp for measurement.

**Oblique sagittal (#4 R/L):** T2 HASTE FS, prescribed parallel to the long axis of each kidney from the coronal localizer. Provides an orthogonal view of the kidney length for confirmation. The oblique sagittal also profiles the kidney in the A/P dimension — anterior and posterior margins are delineated.

**Oblique axial (#5 R/L):** T2 HASTE FS, prescribed perpendicular to the long axis of each kidney from the sagittal oblique or coronal oblique localizer. Each slice represents a true cross-section through the kidney. Summing the area of each slice (× slice thickness) gives the renal volume. The perpendicular prescription ensures no geometric distortion from oblique slicing.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Oblique prescription** — Oblique coronal and sagittal are truly parallel to the long axis of each kidney? Oblique axial is truly perpendicular? | If the plane is misaligned: kidney length is underestimated (cut obliquely) and cross-sectional area is overestimated (ellipse instead of circle). Confirm the plane passes through the upper and lower poles on two orthogonal localizers |
| **Coverage** — Entire kidney included in all oblique stacks? | Reposition if upper or lower pole clipped. The oblique stacks are small FOV — check that no pole is missed |
| **Breath-hold consistency** — Same depth across all oblique acquisitions? | If inconsistent: the kidney shifts between sequences and measurements are not comparable. End-expiration preferred |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 5 sequences (×2 kidneys). Oblique coronal, sagittal, and axial for renal volumetry. Non-contrast |
