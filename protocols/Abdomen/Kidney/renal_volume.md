# Renal Volume (Renal Volumetry MRI)

**Version:** 1.0 | **Date:** 2026-09-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the kidneys.
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** Breath-hold at shallow breathing depth — pause during quiet breathing, no deep inspiration or forced expiration. Consistent breath-hold depth across all sequences.
- **IV Access:** Not required — non-contrast protocol.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_trufi_bil_obl_sag_bh` | Oblique sagittal (double oblique, ×2) | ∥ long axis of each kidney — prescribed on both coronal and axial localizers | Each kidney, entire — both kidneys in one acquisition | **None** | Breath-hold |
| 2 | `t2_haste_cor_mbh` | Coronal | True coronal | Both kidneys | **Superior oblique** over heart | Multi breath-hold |
| 3 | `t1_vibe_dixon_cor_bh` | Coronal | True coronal | Both kidneys | **None** | Breath-hold |
| 4 | `t1_vibe_dixon_tra_bh` (±) | Axial | True axial | Both kidneys | **None** | Breath-hold |
| 5 | `t2_haste_fs_obl_cor_mbh` (R then L) | Oblique Coronal | ∥ long axis of each kidney | Entire kidney incl. all cysts, per side | **None** | Multi breath-hold |
| 6 | `t2_haste_fs_obl_sag_mbh` (R then L) | Oblique Sagittal | ∥ long axis of each kidney | Entire kidney incl. all cysts, per side | **None** | Multi breath-hold |
| 7 | `t2_haste_fs_obl_tra_mbh` (R then L) | Oblique Axial | ⟂ long axis of each kidney | Entire kidney incl. all cysts, per side | **None** | Multi breath-hold |

*#1: Double-oblique TRUFI localizer — one slab per kidney, both L/R and A/P tilt corrected in a single acquisition.*  
*#2–#4: Standard coronal survey + T1 Dixon (coronal, ± axial) for anatomy, fat assessment, and renal vascular identification.*  
*#5–#7: Oblique planes per kidney, right side first then left. The kidneys are not aligned with the cardinal body planes — each is imaged along its own long axis (oblique coronal and sagittal) and perpendicular to it (oblique axial).*  

---

## 3. Sequence Rationale

### Core Strategy

Renal volume measurement for pre-transplant assessment or polycystic kidney disease monitoring. The clinical question is purely anatomical: what is the volume of each kidney? No contrast, no DWI, no lesion characterization.

The kidneys are retroperitoneal organs angled obliquely — the upper poles are more posterior and medial, the lower poles more anterior and lateral. Each kidney tilts slightly differently. Measuring length on a true coronal underestimates kidney size because the kidney is cut obliquely rather than along its true long axis. Accurate volume measurement requires:
- **Oblique coronal** along the long axis → true craniocaudal length (CCC measurement)
- **Oblique sagittal** along the long axis → orthogonal confirmation of length
- **Oblique axial** perpendicular to the long axis → true cross-sectional area at each level, summed (area × slice thickness) for volume

The three oblique planes are mutually orthogonal: oblique coronal and oblique sagittal both contain the long axis and are perpendicular to each other; the oblique axial is perpendicular to both.

Each kidney is imaged separately because their axes differ.

---

### Positioning Workflow

The goal is to align three planes to each kidney's individual long axis. The kidneys are oblique in both L/R (upper pole medial, lower pole lateral) and A/P (upper pole posterior, lower pole anterior). The double-oblique TRUFI corrects both tilts together in a single step:

1. **True coronal + axial localizer:** Standard scouts — both kidneys visible. The coronal shows the L/R tilt of each kidney; the axial shows the A/P tilt and the renal hila.

2. **Bilateral oblique sagittal TRUFI (double oblique):** Two oblique sagittal slabs are prescribed simultaneously — one per kidney. On the coronal localizer, each slab is angled along that kidney's L/R tilt (upper pole to lower pole). On the axial localizer, the same slab is tilted along the kidney's A/P angulation. Because the slab is defined on both localizers, both tilts are corrected in one prescription — the output is a double-oblique sagittal slab through each kidney's true long axis, both kidneys acquired in a single breath-hold.

3. **Oblique coronal / sagittal / axial HASTE FS (per kidney):** From the double-oblique TRUFI image of each kidney, prescribe the three oblique HASTE FS stacks for that kidney — right side first, then left. The VIBE Dixon assists: the coronal shows each kidney's pole-to-pole L/R tilt, and the axial vessels approximate the A/P tilt — the hilar entry point anchors the short axis and confirms the long axis passes through it, a stable landmark in polycystic kidneys where cyst-distorted poles make a pole-to-pole axis unreliable. The three stacks are mutually orthogonal: oblique coronal and oblique sagittal both contain the long axis and are perpendicular to each other; the oblique axial is perpendicular to both.

---

### Sequence Details

**T2 TRUFI bilateral oblique sagittal (#1):** Fast bright-fluid (TrueFISP) sequence used as the dedicated oblique localizer. Two double-oblique sagittal slabs — one per kidney — acquired simultaneously in one breath-hold. Each slab is prescribed along that kidney's long axis on both the coronal and axial localizers, correcting the L/R and A/P tilt in a single step. Serves as the reference image for the oblique HASTE FS prescriptions.

**T2 HASTE coronal (#2):** Standard true coronal survey, single slab covering both kidneys. Shows both kidneys in overview — size, position, cysts, hydronephrosis.

**T1 VIBE Dixon coronal (#3):** Coronal T1 for anatomical reference and renal vascular overview. The vessels mark the hilar level but course roughly transversely — they do not trace the long axis — so the L/R tilt is read from the pole-to-pole kidney contour itself. In/opposed phase for fat assessment if needed.

**T1 VIBE Dixon axial (#4, ±):** Axial T1 through both kidneys. Only required if the cysts distort the kidney so much that its orientation cannot be identified. Localizes the renal artery and vein at the hilum — a stable landmark when cyst-distorted poles make a pole-to-pole axis unreliable. The pedicle courses anteromedial → posterolateral, approximating the kidney's A/P tilt: the hilar entry point anchors the short axis (the vessels course roughly along it) and confirms the long axis passes through the hilum.

**Oblique coronal (#5 R/L):** T2 HASTE FS, prescribed parallel to the long axis of each kidney from the double-oblique TRUFI. The kidney is profiled in its true craniocaudal length. FS suppresses peri-renal fat, making the kidney contour crisp for measurement. Coverage must include the entire kidney including all cysts.

**Oblique sagittal (#6 R/L):** T2 HASTE FS, prescribed parallel to the long axis of each kidney from the double-oblique TRUFI. Provides an orthogonal view of the kidney length for confirmation. The oblique sagittal also profiles the kidney in the A/P dimension — anterior and posterior margins are delineated. Coverage must include the entire kidney including all cysts.

**Oblique axial (#7 R/L):** T2 HASTE FS, prescribed perpendicular to the long axis of each kidney from the double-oblique TRUFI. Each slice represents a true cross-section through the kidney. Summing the area of each slice (× slice thickness) gives the renal volume. The perpendicular prescription ensures no geometric distortion from oblique slicing. Coverage must include the entire kidney including all cysts.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Oblique prescription** — Oblique coronal and sagittal are truly parallel to the long axis of each kidney? Oblique axial is truly perpendicular? | If the plane is misaligned: kidney length is underestimated (cut obliquely) and cross-sectional area is overestimated (ellipse instead of circle). Confirm the plane passes through the upper and lower poles on two orthogonal localizers |
| **Coverage** — Entire kidney including all cysts included in all oblique stacks? | Reposition if a pole or cyst margin is clipped. Extend the stack until the outermost cyst margin at both poles is included — cysts can project beyond the apparent renal contour |
| **Large vertical coverage on transverse stack** — very large polycystic kidney? | Use Composing (set and go) — the stack is automatically split into multiple breath-hold segments, each properly shimmed to ensure fat sat across the full coverage |
| **Fat sat on oblique stacks** — uniform fat suppression on all slices? | Re-shim if patchy. Fat sat is essential for renal volumetry — it suppresses the bright perirenal and sinus fat so the kidney contour (incl. outermost cysts) is crisply delineated; without it, boundary errors repeat on every slice and accumulate into an inaccurate total volume |
| **Breath-hold consistency** — Same depth across all oblique acquisitions? | If inconsistent: the kidney shifts between sequences and measurements are not comparable. Shallow-breathing hold — no deep inspiration or forced expiration |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 5 sequences (×2 kidneys). Oblique coronal, sagittal, and axial for renal volumetry. Non-contrast |
