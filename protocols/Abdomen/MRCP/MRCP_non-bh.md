# MRCP Non-Breath-Hold (Free-Breathing MRCP)

**Version:** 1.0 | **Date:** 2026-08-04 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

As `MRCP.md`. All sequences are free-breathing or respiratory-triggered — no breath-holds required. Patient breathes quietly throughout.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_p3_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver + pancreas | **Superior oblique** over heart | Free breathing |
| 2 | `t2_haste_fs_tra_non-bh` | Axial | True axial | Whole liver + pancreas | **None** | Free breathing |
| 3 | `t2_haste_tra_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 4 | `t2_fblade_fs_tra_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 5 | `t1_tfl_in-phase_tra_non-bh` | Axial | True axial | Whole liver + pancreas | **None** | Free breathing |
| 6 | `t1_tfl_opp-phase_tra_non-bh` | Axial | Copy Slice from #5 | — | **None** | Free breathing |
| 7 | `t1_starvibe_fs_tra_non-bh` | Axial | Copy Slice from #5 | — | **None** | Free breathing |
| 8 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 9 | `t2_space_cor_obl_p2_trig_MRCP` | Coronal Oblique | Angle on axial to cover the gallbladder, CBD, and entire pancreas | Gallbladder → ampulla. Entire pancreas included | **L/R** (arms) | Respiratory triggered |
| 10 | `t2_haste_cor_obl_thin_slab_trig` | Coronal Oblique | On axial at porta hepatis: draw line through CBD toward pancreatic head (≈ ∥ pancreatic head). Single oblique | Single thick slab (~20–40 mm) through CBD from hilum → ampulla | **None** | Respiratory triggered |
| 11 | `t2_haste_sag_obl_thin_slab_trig` | Sagittal Oblique | On axial at gallbladder level: draw line along long axis of gallbladder. Single oblique | Single thick slab (~20–40 mm) through gallbladder, cystic duct, and cystic duct–CBD junction | **None** | Respiratory triggered |

---

## 3. Sequence Rationale

### Core Strategy

This is the free-breathing variant of `MRCP.md` — essentially the BLADE non-BH T2 screen from `liver_non-bh.md` (with HASTE FS backup) combined with the MRCP core from `MRCP.md`. Three aspects differ from the standard MRCP:

---

**Why T1 VIBE Dixon needs three sequences to replace (#5–#7):**

T1 VIBE Dixon is a 3D breath-hold acquisition that provides water-only, fat-only, in-phase, and opposed-phase images from one scan. In the non-BH protocol:

- **TFL in-phase + opp-phase (#5, #6):** Two separate single-shot acquisitions at different TE — replace the Dixon in/opp pair. No Dixon support in TFL, so they must be acquired separately. Same trade-off as `liver_non-bh.md`.
- **StarVIBE FS (#7):** Motion-robust fat-suppressed T1 — replaces the Dixon water-only image. In `liver_non-bh.md`, StarVIBE is already part of the dynamic acquisition (1st measurement = pre-contrast baseline), so a separate pre-contrast StarVIBE is not needed. MRCP has no contrast and no dynamic phases, so a dedicated StarVIBE FS provides the fat-suppressed T1 anatomical reference.

Together these three sequences cover what one VIBE Dixon covers in the standard MRCP.

---

**Why thin slab HASTEs need respiratory triggering (#10, #11):**

In the standard MRCP, the thin slabs are breath-hold — the patient holds at end-expiration and the single slice is acquired in <1 s. The breath-hold fixes the diaphragm position. In the non-BH protocol, the patient breathes continuously — the single-shot HASTE is still acquired in <1 s (no intra-slice motion), but without triggering, the slice could be acquired at any respiratory phase. Respiratory triggering gates the acquisition to a consistent phase, ensuring the diaphragm and ductal anatomy are at the same position every time.

---

**Why no heavy T2 axial is needed:**

In liver protocols (`liver_routine.md`, `liver_non-bh.md`), heavy T2 axial separates fluid-filled lesions (cyst, haemangioma) from solid lesions — a core diagnostic function for lesion characterization. In MRCP, the SPACE 3D (#9) and thin slab HASTEs (#10, #11) are already heavily T2-weighted — static fluid is bright, background is dark. Adding a heavy T2 axial would be redundant; the same contrast is already acquired with higher spatial resolution and ductal specificity from the SPACE.

---

The remaining sequences — T2 HASTE/TrueFISP (#1–#3, #8) and SPACE (#9) — are unchanged from `MRCP.md`. BLADE (#4) is the primary T2 FS axial, with HASTE FS (#2) as the motion-robust backup (same logic as `liver_non-bh.md`). See those protocols for full technique rationale.

---

## 4. Variations

- **3T:**
  - T2 SPACE (#9) uses `t2_tse3d_cor_p2_trig_MRCP` — see `MRCP.md` for rationale (SAR limits, no MPR trade-off).
  - Thin slab HASTEs (#10, #11) use fat saturation (`t2_haste_fs_cor_obl_thin_slab_trig`, `t2_haste_fs_sag_obl_thin_slab_trig`). At 1.5T, FS on a single-shot HASTE is unreliable — lower B0 homogeneity means the per-slice fat sat pulse may fail patchily; non-FS is safer (bile is bright, fat is intermediate, the projection is diagnostic). At 3T, the wider water-fat chemical shift separation (~440 Hz vs ~220 Hz at 1.5T) makes FS robust to B0 inhomogeneities, and fat is brighter (longer T1) so suppressing it improves ductal conspicuity.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Whole liver + pancreas on all sequences? | Free breathing causes diaphragmatic excursion — prescribe stacks slightly wider |
| **SPACE respiratory trigger** — See `MRCP.md` for dome vs phase triggering | Same |
| **T1 TFL in/opp consistency** — Liver position identical between #5 and #6? | If mismatched: opposed-phase dropout confounded by slice position change. StarVIBE (#7) provides a motion-robust fat-suppressed reference |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-04 | — | Initial — 11 sequences. Free-breathing variant of MRCP.md. Liver screen from liver_non-bh.md + MRCP core from MRCP.md. 3T variant noted |
