# Primovist Non-Breath-Hold (Free-Breathing Hepatobiliary Contrast Liver MRI)

**Version:** 1.0 | **Date:** 2026-08-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

As `liver_non-bh.md`. Primovist-specific: dose 0.1 mL/kg, withdraw from factory pre-filled syringe, **hand injection** (volume too small for power injector — risks contrast left in tubing). Saline flush.

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver | **Superior oblique** over heart | Free breathing |
| 2 | `t1_tfl_in-phase_tra_non-bh` | Axial | True axial | Whole liver | **None** | Free breathing |
| 3 | `t1_tfl_opp-phase_tra_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |

### Post-Contrast — Dynamic Phases

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Primovist, hand injection | — | — | — |
| 4 | `t1_starvibe_fs_tra_non-bh_dyn_C` | Axial | Copy Slice from #2 | Whole liver | **None** | Free breathing. Multiple measurements over ~3 min. Inject after 1st measurement |
| 5 | `t1_starvibe_fs_tra_non-bh_delay_5min_C` | Axial | Copy Slice from #2 | — | **None** | Free breathing, ~5 min |

### Post-Contrast — Hepatobiliary Wait (T2 sequences)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 6 | `t2_fblade_fs_tra_non-bh` | Axial | Copy Slice from #2 | Whole liver | **None** | Free breathing |
| 7 | `t2_haste_fs_tra_p2_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 8 | `t2_haste_tra_p2_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 9 | `t2_heavy_haste_tra_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 10 | `t2_trufi_cor_p2_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |

*T2 BLADE variant from liver_non-bh.md, reordered post-contrast per primovist workflow. #6 = primary FS, #7 = HASTE backup, #8 = non-FS reference, #9 = heavy HASTE.*

### Post-Contrast — Late Phases

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 11 | `t1_starvibe_fs_tra_non-bh_delay_10min_C` | Axial | Copy Slice from #2 | — | **None** | Free breathing, ~10 min |
| 12 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #2 | Whole liver | **None** | Free breathing |
| — | *Pause ~5 min* | — | — | — | — | — |
| 13 | `t1_starvibe_fs_tra_non-bh_delay_20min_C` | Axial | Copy Slice from #2 | — | **None** | Free breathing, ~20 min |

*#11: Optional early hepatobiliary check — see rationale. #13: Diagnostic hepatobiliary phase. See primovist.md for lesion behaviour.*

---

## 3. Sequence Rationale

### What This Protocol Is

This is the **T2 BLADE variant of `liver_non-bh.md`, reorganized into `primovist.md` ordering**, with Primovist-specific modifications. The pre-contrast, T2, and DWI sequences are identical to `liver_non-bh.md` — they are simply reordered to fill the hepatobiliary uptake waiting period (same workflow strategy as `primovist.md`). The dynamic and delayed phases use StarVIBE instead of TWIST (same substitution as `liver_non-bh.md`).

**Differences from `liver_non-bh.md`:** Pre-contrast is lean (no T2 axials, deferred to post). T2 axials acquired post-contrast during the hepatobiliary wait. Two additional StarVIBE phases at 10 and 20 min for hepatobiliary assessment. Hand-injected Primovist instead of power-injected extracellular contrast.

**Differences from `primovist.md`:** All free-breathing techniques (TFL, StarVIBE, BLADE/HASTE) replace breath-hold equivalents (VIBE Dixon, TWIST, TSE).

---

### Why Two Hepatobiliary Delays

`primovist.md` has a single hepatobiliary phase at 20 min — each additional acquisition costs a breath-hold. In the non-BH protocol, StarVIBE is free-breathing: adding a measurement at 10 min costs only ~1–2 min of scan time. It provides:

- **Early check:** If liver function is good, uptake may already be diagnostic at 10 min — the 20 min becomes confirmatory.
- **Motion insurance:** If the 20 min StarVIBE is degraded by motion or irregular breathing, the 10 min phase is a backup.

If scan time is tight, the 10 min phase can be dropped — the 20 min is the diagnostic requirement.

---

### Image Quality

See `liver_non-bh.md` for technique trade-offs (BLADE vs HASTE, TFL vs VIBE, StarVIBE vs TWIST). See `primovist.md` for hepatobiliary phase lesion behaviour. See `liver_routine.md` for dynamic enhancement patterns.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Whole liver on all sequences? | Free breathing → diaphragmatic excursion. Prescribe stacks slightly wider |
| **Post-contrast** — Contrast present? Hepatobiliary uptake by 20 min? | If absent: check IV line. If no uptake: impaired hepatocyte function (cirrhosis, high bilirubin) — extend delay |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-03 | — | Initial — 13 sequences. T2 BLADE variant of liver_non-bh reorganized per primovist ordering. StarVIBE dyn + 5/10/20 min |
