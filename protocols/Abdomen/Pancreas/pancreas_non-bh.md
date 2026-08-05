# Pancreas Non-Breath-Hold (Free-Breathing Pancreas MRI)

**Version:** 1.0 | **Date:** 2026-08-04 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

As `pancreas.md`. All sequences are free-breathing or respiratory-triggered. Fasting not required.

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Whole pancreas | **Superior oblique** over heart | Free breathing |
| 2 | `t2_haste_fs_tra_p2_non-bh_pancreas` | Axial | True axial | Pancreas only. Head → tail + ampulla | **None** | Free breathing |
| 3 | `t2_haste_tra_p2_non-bh_pancreas` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 4 | `t2_heavy_haste_fs_tra_non-bh_pancreas` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 5 | `t2_trufi_cor_p2_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 6 | `t1_tfl_in-phase_tra_trig` | Axial | True axial | Pancreas only | **None** | Respiratory triggered |
| 7 | `t1_tfl_opp-phase_tra_trig` | Axial | Copy Slice from #6 | — | **None** | Respiratory triggered |

*#1–#4: HASTE T2 — single-shot, motion-robust. #2 = FS lesion detection, #3 = non-FS anatomical reference, #4 = heavy T2 duct/cyst assessment.*  
*#5: TrueFISP — same as pancreas.md, already free-breathing.*  
*#6–#7: T1 TFL in/opp — respiratory-triggered. No Dixon; in and opposed phase acquired separately at different TE.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s | — | — | — |
| 8 | `t1_starvibe_fs_tra_non-bh_dyn_C` | Axial | Copy Slice from #6 | Pancreas only | **None** | Free breathing. Multiple measurements over ~3 min. Inject contrast after 1st measurement |
| 9 | `ep2d_diff_b50_300_800_tra_pancreas` | Axial | Copy Slice from #6 | Pancreas only | **None** | Free breathing |

*#8: StarVIBE dynamic — same as liver_non-bh.md. 1st measurement = pre-contrast baseline, contrast injected after, remaining measurements capture arterial → PVP → delayed passage.*  
*#9: DWI — pancreas-only FOV.*

---

## 3. Sequence Rationale

### Core Strategy

This is the free-breathing variant of `pancreas.md`. The key substitutions follow the same pattern as `liver_non-bh.md`: T2 TSE → HASTE (single-shot), T1 VIBE Dixon → TFL in/opp (respiratory triggered), TWIST dynamic → StarVIBE radial (1st measurement = baseline). TrueFISP and DWI are unchanged (already free-breathing). See `liver_non-bh.md` for technique trade-offs.

**Why all-HASTE, not BLADE:** `liver_non-bh.md` uses BLADE for the primary T2 FS axial because BLADE has higher SNR than HASTE and the liver FOV is large. BLADE requires a minimum FOV (~15–20 cm) for enough independent rotating blades to provide effective motion correction. A pancreas-only FOV is too small — the blade count drops and the motion-correction benefit degrades. HASTE has no minimum FOV constraint and is the better choice for small-FOV targets. The lower SNR of HASTE is acceptable because the pancreas is assessed on multiple complementary sequences (T2, T1, dynamic enhancement, DWI).

---

**Why T1 TFL uses respiratory triggering (not free breathing):**

Unlike HASTE (single-shot T2, <1 s per slice), TFL is a single-shot T1 with magnetization preparation — the T1 contrast depends on the recovery period between slices. Respiratory triggering gates each slice acquisition to a consistent respiratory phase, ensuring the pancreas is at the same position for each slice and the T1 contrast is not confounded by motion. In `liver_non-bh.md`, TFL is free-breathing because the liver is a larger target and slice position variation is less critical; the pancreas is smaller and more mobile — respiratory triggering improves slice-to-slice consistency.

---

**Why T2 SPACE ERCP is optional:**

The SPACE is respiratory-triggered and takes several minutes — in a non-BH patient, breathing is often irregular, which degrades navigator triggering. It can be attempted: if the patient breathes regularly enough for consistent triggering, the SPACE is diagnostic. If breathing is too erratic and the SPACE is non-diagnostic, the heavy T2 HASTE axial (#4) provides motion-robust ductal assessment. Baseline ductal anatomy should have been established on a prior MRCP or standard pancreas protocol; the HASTE is sufficient for follow-up.

---

**Post-contrast:** Same StarVIBE dynamic technique as `liver_non-bh.md` (1st measurement = baseline, contrast injected after). Differs from liver_non-bh in two ways: (1) no separate delayed phases — the pancreas does not need a 5 min delayed phase (enhancement peaks at PVP and washes out by 2 min), so the continuous StarVIBE acquisition alone suffices; (2) the arterial window uses pancreas criteria (coeliac/SMA bright, parenchyma dark — earlier than the liver window). DWI (#9) is pancreas-only FOV, same b-values.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Whole pancreas on all sequences? | Free breathing → diaphragmatic excursion. Prescribe stacks slightly wider |
| **TFL triggering** — Consistent respiratory phase across #6 and #7? | If trigger irregular: slice position mismatch between in and opposed phase confounds dropout interpretation |
| **StarVIBE arterial phase** — Coeliac/SMA bright, parenchyma dark? | See `pancreas.md` for optimal pancreatic arterial window. StarVIBE temporal resolution is lower than TWIST — the arterial peak may be missed if the bolus is fast |
| **Post-contrast** — Contrast present? | If absent: check IV line, confirm injection |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-04 | — | Initial — 9 sequences. Free-breathing pancreas protocol. HASTE T2, TFL trig, StarVIBE dynamic. SPACE ERCP dropped |
