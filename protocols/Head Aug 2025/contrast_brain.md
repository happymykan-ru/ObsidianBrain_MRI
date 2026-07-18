# Contrast Brain (Post-Contrast Brain MRI)

**Version:** 1.0 | **Date:** 2026-07-18 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_flair_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| — | **Contrast** | — | — | — | — |
| 4 | `resolve_3scan_trace_tra` | Axial | Copy Slice from #1 | — | **None** |
| 5 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 6 | `MPR` | Sag+Ax | — | Whole brain | — |
| 7 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |

---

## 3. Sequence Rationale

**`t2_tse_tra` (#1)**
Core T2 anatomy. Sensitive to edema, gliosis, infarction, white matter disease.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. 2D FLASH provides a clean anatomical reference matched in geometry to the post-contrast T1 (#7) — direct pre/post comparison for enhancement. The relatively flat T1 contrast of FLASH makes pathological enhancement stand out clearly against background tissue. No sat band: short TR has no slack for a sat pulse, and gradient echo inflow is coherent between pre/post acquisitions so it subtracts out rather than causing ghosting.

**`t2_tse_flair_tra` (#3)**
CSF-suppressed T2. Essential for periventricular and cortical/subcortical lesion detection (MS, small vessel ischaemia, encephalitis).

**Contrast**
Standard dose IV gadolinium. DWI (#4) fills the 5-minute delay post-injection — most lesions (tumours, MS plaques, meningeal disease) peak at 5–10 min. Scanning post-contrast T1 too early misses enhancement; too late risks contrast leaking into CSF and masking meningeal uptake.

**`resolve_3scan_trace_tra` (#4)**
3-scan trace DWI — three orthogonal diffusion directions averaged to produce the direction-independent trace image. Fills the post-injection delay (~3–5 min) before post-contrast T1, eliminating dead scan time. Same clinical role as standard DWI: acute ischaemia, abscess, cellular tumours. Fewer directions and lower SNR than dedicated multi-b DWI but sufficient for screening. Less distortion at skull base vs single-shot EPI.

**`t1_vibe_fs_cor_C` (#5)**
3D T1 post-contrast with fat saturation. VIBE is a fast spoiled GRE — fat saturation makes enhancing lesions and meningeal enhancement more conspicuous by suppressing bright fat signal that could mask subtle enhancement.
*Plane:* **Coronal** is the money plane for enhancement. The structures where contrast matters most — skull base, cavernous sinus, pituitary, meninges, internal auditory canals, vertex — are all profiled in-plane coronally. Axial slices cut across them obliquely, making subtle enhancement harder to appreciate against partial volume. Coronal also gives symmetric left/right comparison at a glance. The 3D source then reformats cleanly into sagittal and axial planes for the MPR (#6).

**`MPR` (#6)**
Multiplanar reconstruction from post-contrast VIBE (#5). **Sagittal:** midline and brainstem. **Axial:** conventional axial post-contrast reference. No additional acquisition.

**`t1_fl2d_tra_C` (#7)**
Post-contrast 2D T1 — identical geometry to the pre-contrast baseline (#2). Direct subtraction or visual comparison confirms enhancement. Because FLASH is inherently less T1-weighted than MPRAGE, enhancing tissue (which shortens T1) appears bright against suppressed background.

---

## 4. Pathology-Based Variations

- **SWI:** Add when screening for microbleeds, cavernomas, or haemorrhagic components.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack if any sequence is short |
| **`t1_fl2d_tra` (#2 vs #7)** — identical geometry pre and post? | Must match — mismatched slices invalidate enhancement comparison |
| **`resolve_3scan_trace_tra`** — true restriction vs T2 shine-through on ADC? | Document true restriction. If distorted at skull base: flip phase-encode (A>>P → P>>A) |
| **`t1_vibe_fs_cor_C`** — contrast present? Confirm intravascular enhancement (e.g., venous sinuses, choroid plexus) | If absent: check IV line patency, confirm injection was delivered, repeat if extravasation suspected |
| **Fat saturation** — uniform on VIBE? | Re-shim or re-acquire if fat suppression patchy |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 7 sequences |
