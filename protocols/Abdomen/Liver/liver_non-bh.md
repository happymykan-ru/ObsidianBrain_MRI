# Liver Non-Breath-Hold (Free-Breathing Multiphasic Liver MRI)

**Version:** 1.0 | **Date:** 2026-08-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array
- **Laser Landmark:** Centre of body coil (mid-liver, ~xiphoid level)
- **Verbal Instructions:** Breathe quietly and regularly throughout the entire exam — no breath-holds are required. The sequences are motion-robust (single-shot HASTE, radial StarVIBE) and designed to be acquired during free breathing.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver | **Superior oblique** over heart | Free breathing |
| — | **T2 axial — choose Variant A or B** | — | — | — | — | — |
| 2A | `t2_haste_fs_tra_p2_non-bh` | Axial | True axial | Whole liver | **None** | Free breathing |
| 3A | `t2_haste_tra_p2_non-bh` | Axial | Copy Slice from #2A | — | **None** | Free breathing |
| 4A | `t2_heavy_haste_fs_tra_non-bh` | Axial | Copy Slice from #2A | — | **None** | Free breathing |
| — | **or** | — | — | — | — | — |
| 2B | `t2_fblade_fs_tra_p3_non-bh` | Axial | True axial | Whole liver | **None** | Free breathing |
| 3B | `t2_fblade_tra_p3_non-bh` | Axial | Copy Slice from #2B | — | **None** | Free breathing |
| 4B | `t2_heavy_haste_fs_tra_non-bh` | Axial | Copy Slice from #2B | — | **None** | Free breathing |
| 5B | `t2_haste_fs_tra_p2_non-bh` | Axial | Copy Slice from #2B | — | **None** | Free breathing |
| — | **(shared)** | — | — | — | — | — |
| 6 | `t2_trufi_cor_p2_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 7 | `t1_tfl_in-phase_tra_non-bh` | Axial | True axial | Whole liver | **None** | Free breathing |
| 8 | `t1_tfl_opp-phase_tra_non-bh` | Axial | Copy Slice from #7 | — | **None** | Free breathing |

*Variant A — all HASTE: motion-robust single-shot T2. Lower SNR and softer contrast, but each slice is independent of breathing. Use when the patient has irregular or deep breathing (severe dyspnoea, unable to lie still) — HASTE tolerates more motion than BLADE.*
*Variant B — BLADE + HASTE: BLADE (PROPELLER) for the FS + non-FS T2 pair — higher SNR and better tissue contrast than HASTE, free-breathing compatible. HASTE FS backup (#5B) in case BLADE FS is degraded. Heavy T2 (#4B) stays HASTE (BLADE at long TE is too slow). Use when the patient breathes regularly and can lie relatively still — BLADE quality depends on consistent breathing rhythm.*
*#7–#8: T1 TFL (TurboFLASH) — single-shot T1 per slice. In-phase and opposed-phase acquired separately.*

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 9 | `t1_starvibe_fs_tra_non-bh_dyn_C` | Axial | Copy Slice from #7 | Whole liver | **None** | Free breathing. First measurement = pre-contrast baseline. Contrast injected after 1st measurement. Subsequent measurements over ~3 min |
| 10 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #7 | Whole liver | **None** | Free breathing |
| 11 | `t1_starvibe_fs_tra_non-bh_delay_5min_C` | Axial | Copy Slice from #7 | — | **None** | Free breathing, ~5 min post-injection |

*#8: StarVIBE has a stack-of-stars radial acquisition — motion-robust, free breathing. Multiple consecutive measurements over ~3 min: 1st measurement = baseline/mask, contrast injected, remaining measurements capture arterial → PVP → delayed passage. No separate pre-contrast acquisition needed.*
*#10: Late delayed phase with the same StarVIBE acquisition.*

---

## 3. Sequence Rationale

### Core Strategy

This protocol is the free-breathing alternative to `liver_routine.md` for patients who cannot breath-hold (dyspnoea, poor compliance, paediatric, language barrier). Every sequence is acquired during free breathing using motion-robust techniques.

The key substitutions: T2 TSE → T2 HASTE or BLADE (two variants). T1 VIBE Dixon → T1 TFL in/opp (separate sequences). TWIST VIBE dynamic → StarVIBE radial.

**Image quality trade-off:** HASTE has the lowest SNR and softest tissue contrast but is maximally motion-robust (single-shot per slice). BLADE has higher SNR and better contrast (multi-shot, rotating k-space blades) but requires a regular breathing rhythm — irregular breathing causes blurring. T1 TFL is single-shot — lower SNR and spatial resolution than VIBE, no Dixon. StarVIBE has lower temporal resolution than TWIST but is motion-robust (radial acquisition). Overall: a motion-degraded breath-hold exam is non-diagnostic; a motion-robust, lower-SNR free-breathing exam is diagnostic.

---

### Pre-Contrast

**`t2_haste_cor_non-bh` (#1)**
T2 HASTE coronal. Single-shot TSE — each slice acquired in <1 second, independent of breathing. Coronal survey of the whole liver, biliary tree, and relationship to diaphragm. Superior oblique sat band over the heart suppresses cardiac ghosting into the liver dome.

**T2 axial — two variants:**

Two options for the T2 axial sequences, selected based on the patient's breathing pattern:

- **Variant A (all HASTE):** T2 HASTE FS + non-FS pair. Maximally motion-robust — single-shot per slice, independent of breathing. Use for irregular/deep breathing.
- **Variant B (BLADE + HASTE backup):** T2 BLADE (PROPELLER) FS + non-FS pair. Higher SNR and better tissue contrast — multi-shot with rotating k-space blades. Motion between blades causes blurring, not ghosting. Use for regular breathing. Heavy T2 stays HASTE. HASTE FS (#5B) serves as backup for the BLADE FS if degraded. The non-FS BLADE has no backup (anatomical reference only).

**`t2_heavy_haste_fs_tra_non-bh` (#4A/B)**
Heavily T2 HASTE FS. Same in both variants — HASTE is the only free-breathing option at long TE. Only fluid-filled structures remain bright.

**`t2_haste_fs_tra_p2_non-bh` (#5B)**
HASTE FS — in Variant B, backup to BLADE FS (#2B). In Variant A, the primary FS T2 is already HASTE so this is not used.

**`t2_trufi_cor_p2_non-bh` (#6)**
T2 TrueFISP coronal. Very short TR — essentially motion-insensitive. Blood and bile are bright. Portal vein, hepatic veins, IVC, and biliary tree assessed in the coronal plane.

**`t1_tfl_in-phase_tra_non-bh` (#7)**
T1 TurboFLASH (TFL) in-phase axial. TFL is a 2D single-shot spoiled gradient echo — each slice is acquired in <1 s, free breathing. Unlike VIBE (3D, breath-hold, Dixon-capable), TFL is a 2D single-shot technique: lower SNR, thicker slices, and no Dixon support, so in-phase and opposed-phase must be acquired as two separate sequences. The benefit is motion robustness — breathing cannot cause intra-slice ghosting. In-phase TE (~2.4 ms at 1.5T, ~4.8 ms at 3T) where water and fat signal add constructively. Higher SNR than opposed-phase, preserved fat planes. Assesses liver morphology, intrinsic T1-hyperintensity, and iron deposition.

**`t1_tfl_opp-phase_tra_non-bh` (#8)**
T1 TurboFLASH opposed-phase axial. Matched to #6 but at the opposed-phase TE (~1.2 ms at 1.5T, ~2.4 ms at 3T). Signal dropout confirms intracellular lipid — diffuse steatosis or intralesional fat.

---

### Post-Contrast

**`t1_starvibe_fs_tra_non-bh_dyn_C` (#9)**
T1 StarVIBE FS axial, multiple consecutive measurements over ~3 minutes. Replaces the breath-hold TWIST VIBE dynamic phases.

StarVIBE uses a stack-of-stars radial k-space acquisition — the centre of k-space is sampled with every radial spoke, making it inherently motion-robust. Respiratory motion during free breathing produces radial streaks rather than coherent phase-encode ghosts.

**Workflow:** The first measurement is the pre-contrast baseline (mask). Contrast is injected after the 1st measurement completes. Subsequent measurements are acquired back-to-back over ~3 minutes, capturing the entire enhancement passage — arterial, portal venous, and early delayed phases — without timing sensitivity. The temporal resolution is lower than TWIST (each measurement takes longer), but the motion robustness means the patient doesn't need to breath-hold.

**Arterial phase identification:** Review the measurement series for the frame where portal vein is enhanced but hepatic veins are not yet enhanced — same criterion as the routine protocol.

**`ep2d_diff_b50_300_800_tra` (#10)**
DWI, single-shot EPI. Same as the routine protocol — free breathing with signal averaging. b=50, 300, 800.

**`t1_starvibe_fs_tra_non-bh_delay_5min_C` (#11)**
T1 StarVIBE FS axial, single measurement ~5 min post-injection. Late delayed phase — haemangioma fill-in, cholangiocarcinoma persistent enhancement.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Whole liver on all sequences? | Free breathing causes diaphragmatic excursion — the liver dome position varies. Check that all sequences cover the full liver despite respiratory motion. Prescribe stacks slightly wider than the anatomical liver extent |
| **Post-contrast** — Contrast present? Hepatic artery and portal vein enhance on StarVIBE measurements? | If absent: check IV line, confirm injection |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-03 | — | Initial — 11 sequences (BLADE + HASTE T2, TFL in/opp, StarVIBE dynamic, DWI, StarVIBE delayed). Free-breathing alternative to liver_routine.md |
