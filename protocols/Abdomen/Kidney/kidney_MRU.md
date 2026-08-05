# MRU (MR Urography with Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. The entire urinary tract from kidneys to bladder must be covered (~40–50 cm). **One body coil in portrait orientation** (rotated 90°) for smaller patients. —  **Two body coils stacked in landscape** for larger patients — upper coil over kidneys, lower coil over pelvis/bladder.
- **Laser Landmark:** Mid-abdomen (umbilicus level). The split upper/lower FOV acquisition strategy covers the full craniocaudal extent.
- **Verbal Instructions:** End-expiration breath-holds. Consistent breath-hold depth crucial for the split-FOV sequences — the upper and lower stacks must abut without gap or overlap. For the excretory phases: breathe quietly, no breath-hold required once the dynamic phases are complete.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].
- **Patient Preparation:** A moderately full bladder improves distal ureter and bladder base visualization.

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Kidneys → bladder | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_haste_sag_mbh` | Sagittal | True sagittal | L/R: midline → lateral margins. Kidneys → bladder | **None** | Multi breath-hold |
| 3 | `t2_tse_fs_tra_p2_mbh_upper` | Axial | True axial | Kidneys → mid-ureters | **None** | Multi breath-hold |
| 4 | `t2_tse_fs_tra_p2_mbh_lower` | Axial | True axial | Mid-ureters → bladder | **None** | Multi breath-hold |
| 5 | `t1_vibe_dixon_tra_p4_bh_upper` | Axial | True axial | Kidneys → mid-ureters | **None** | Breath-hold |
| 6 | `t1_vibe_dixon_tra_p4_bh_lower` | Axial | True axial | Mid-ureters → bladder | **None** | Breath-hold |
| 7 | `t1_vibe_dixon_cor_p4_bh` | Coronal | True coronal | Kidneys → bladder | **None** | Breath-hold |
| 8 | `t2_trufi_cor_p2_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 9 | `t2_space_cor_p3_trig_iso` | Coronal | True coronal. Slab covering both kidneys, ureters, and bladder | Kidneys → bladder | **L/R** (arms) | Respiratory triggered |
| 10 | `angio3d_cor_pre` | Coronal | True coronal. Slab covering both kidneys, ureters, and bladder | Kidneys → bladder | **None** | Breath-hold |

*#1–#2: T2 HASTE coronal + sagittal survey — entire urinary tract.*  
*#9: T2 SPACE — heavily T2 static-fluid 3D. Non-contrast urogram equivalent. Isometric resolution for MPR.*  

### Post-Contrast — Excretory Phases

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s | — | — | — |
| 11 | `angio3d_cor_C_2min` | Coronal | Copy Slice from #10 | — | **None** | Breath-hold, ~2 min post-injection |
| 12 | `angio3d_cor_C_5min` | Coronal | Copy Slice from #10 | — | **None** | Breath-hold, ~5 min post-injection |
| 13 | `t1_vibe_dixon_tra_p4_bh_upper_C` | Axial | Copy Slice from #5 | Kidneys → mid-ureters | **None** | Breath-hold, after #12 |
| 14 | `t1_vibe_dixon_tra_p4_bh_lower_C` | Axial | Copy Slice from #6 | Mid-ureters → bladder | **None** | Breath-hold, after #13 |
| 15 | `t1_vibe_dixon_cor_p4_bh_C` | Coronal | Copy Slice from #7 | Kidneys → bladder | **None** | Breath-hold, after #14 |
| 16 | `angio3d_cor_C_10min` | Coronal | Copy Slice from #10 | — | **None** | Breath-hold, ~10 min post-injection |
| 17 | `angio3d_cor_C_15min` | Coronal | Copy Slice from #10 | — | **None** | Breath-hold, ~15 min post-injection |

*#11–#12: Early excretory Angio3D — contrast entering the collecting system.*  
*#13–#15: T1 post-contrast — same split-FOV as pre, now with enhancement.*  
*#16–#17: Late excretory Angio3D — contrast in the ureters and bladder.*  

---

## 3. Sequence Rationale

### Core Strategy

MR urography assesses the entire upper urinary tract — kidneys, collecting system, ureters, and bladder — for obstruction, filling defects, and congenital anomalies. The clinical question is: is there obstruction, at what level, and what is the cause (stone, stricture, urothelial tumour, extrinsic compression)? The protocol combines renal parenchymal imaging (T2, T1 Dixon, post-contrast T1) with urographic imaging (T2 SPACE, multiple delayed Angio3D phases).

**Key differences from `kidney.md`:**

- **Split-FOV upper/lower:** The urinary tract from kidneys to bladder exceeds a single FOV. T2 TSE, T1 Dixon, and post-contrast T1 are each acquired as two separate stacks — upper (kidneys to mid-ureters) and lower (mid-ureters to bladder). The stacks must abut without gap or overlap.
- **No multiphasic dynamics, no DWI.** Mass characterization is secondary; drainage is primary. Single post-contrast T1 replaces AP/PVP/delayed.
- **T2 SPACE — non-contrast urogram.** Heavily T2 3D with isometric resolution. Static fluid (urine in the collecting system, ureters, bladder) is bright. Shows hydronephrosis and ureteric dilation without contrast. MPR provides views of the entire urinary tract.
- **Multiple delayed Angio3D phases** (2, 5, 10, 15 min). These are the urographic phases — contrast excretion fills the collecting system, ureters, and bladder progressively over time. Each Angio3D captures a later stage of contrast transit. Subtracted from the pre-contrast mask (#10), they produce pure excretory urograms showing the contrast-opacified tract without background tissue.
- **T2 HASTE sagittal** — profiles the ureterovesical junction and bladder base in the sagittal plane. Also assesses the bladder wall.
- **No TrueFISP sagittal vessel scout** — the Angio3D is a urogram, not an MRA. Coronal TrueFISP covers both vessels and ureters.

---

### Pre-Contrast

**T2 HASTE coronal + sagittal (#1–#2):** Whole-tract survey from kidneys to bladder. The sagittal plane profiles the ureterovesical junction and bladder base.

**Split-FOV T2 TSE FS (#3–#4):** Upper stack: kidneys to mid-ureters. Lower stack: mid-ureters to bladder. FS for lesion detection along the entire tract. No non-FS T2 axial is needed — the HASTE coronal and sagittal surveys (#1, #2) provide the anatomical reference, and the T2 SPACE (#9) covers the fluid-filled tract. Adding non-FS axials would double T2 scan time with minimal gain for a protocol where drainage, not mass characterization, is the primary question.

**Split-FOV T1 VIBE Dixon (#5–#6) + coronal (#7):** Pre-contrast baseline for the post-contrast T1. In/opposed phase for fat and intrinsic T1 signal. p4 for short breath-hold given the long FOV.

**TrueFISP coronal (#8):** Vessels and ureters bright without contrast. Portal vein, IVC, and ureteric course assessed in the coronal plane. Provides a motion-robust overview of the entire tract.

**T2 SPACE (#9):** Heavy T2 3D with isometric resolution — the non-contrast urogram. Static urine is bright; the collecting system, ureters, and bladder lumen are visualized. Shows hydronephrosis, ureteric dilation, and filling defects (stone = dark against bright urine). Respiratory triggered. MPR from the 3D volume provides views of the entire urinary tract in any plane. This is the equivalent of a CT KUB without contrast — shows the fluid-filled tract without needing excretion.

---

### Post-Contrast — Excretory Phases

**Angio3D delayed phases (#11, #12, #16, #17):** The core urographic sequences. A coronal 3D slab covering kidneys to bladder is acquired at progressive delays after contrast injection — 2, 5, 10, and 15 min. Each is subtracted from the pre-contrast mask (#10) to produce a pure excretory urogram.

- **2 min (#11):** Contrast in the renal parenchyma and beginning to enter the collecting system (nephrogram → early pyelogram).
- **5 min (#12):** Contrast in the renal pelvis and upper ureters.
- **10 min (#16):** Contrast in the mid/distal ureters.
- **15 min (#17):** Contrast in the distal ureters and bladder. Full tract opacification.

The four delayed phases track contrast transit through the entire urinary tract. An obstructed system shows delayed or absent excretion distal to the obstruction. A filling defect (urothelial tumour, stone) persists across all phases. A long stricture shows gradual narrowing with delayed distal filling.

**Post-contrast T1 (#13–#15):** Split-FOV axial upper + lower, plus coronal. Acquired after the 5 min Angio3D — the early excretory phases take priority for capturing contrast transit into the collecting system. Renal parenchymal enhancement persists well beyond 5 min, so tumour characterization is not compromised by the delay. By this time, excreted contrast is already in the collecting system, adding diagnostic value to the T1. The T1 sequences also fit practically into the 5-to-10-minute gap between Angio3Ds. Matched to pre-contrast for enhancement comparison. Urothelial tumours enhance — an enhancing mural nodule or wall thickening in the renal pelvis, ureter, or bladder. Stones show no enhancement.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Split-FOV alignment** — Upper and lower stacks correctly positioned? 2D T2 TSE: use stacking (abut without gap). 3D T1 VIBE: ensure overlap (3D slab boundary fall-off) | If gapped: a segment of ureter is missed (mid-ureteric stone or tumour) |
| **Excretory timing** — Contrast in the collecting system by 2–5 min? In the bladder by 15 min? | If no excretion by 15 min: impaired renal function or obstruction. Extend the delay to 30–45 min. If unilateral delayed excretion: unilateral obstruction or poor function |
| **T2 SPACE** — Hydronephrosis and ureteric dilation visible? Full tract covered? | If respiratory trigger is irregular: the SPACE may be degraded. The HASTE and TrueFISP are motion-robust backups |
| **Angio3D subtraction** — Mask (#10) and post-contrast acquisitions co-registered? | If patient moves between mask and post: subtraction fails — ring artefacts at the kidney margins. Re-acquire with a new mask if movement is identified early |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 17 sequences. Split-FOV upper/lower. T2 SPACE non-contrast urogram + Angio3D delayed excretory phases (2/5/10/15 min). Full urinary tract from kidneys to bladder |
