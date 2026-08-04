# MRCP (Magnetic Resonance Cholangiopancreatography)

**Version:** 1.0 | **Date:** 2026-08-04 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array
- **Laser Landmark:** Centre of body coil (mid-liver)
- **Verbal Instructions:** Breath-hold commands for the axial and coronal sequences. For the respiratory-triggered SPACE: breathe quietly and regularly — the acquisition follows the breathing cycle. No contrast required.
- **Patient Preparation:** Fasting 4–6 hours before the exam — reduces gastric and duodenal fluid, which can obscure the distal CBD and ampulla. Emptying the gallbladder via fasting distends it with concentrated bile, improving visualization of gallbladder pathology. 
---

## 2. Imaging Series

### Pre-Contrast (all sequences are non-contrast)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver + pancreas | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_tse_fs_tra_p2_mbh` | Axial | True axial | Whole liver + pancreas | **None** | Multi breath-hold |
| 3 | `t2_tse_tra_p2_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Whole liver + pancreas | **None** | Breath-hold |
| 5 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 6 | `t2_space_cor_obl_p2_trig_MRCP` | Coronal Oblique | Angle on axial to cover the gallbladder, CBD, and entire pancreas | Gallbladder → ampulla. Entire pancreas included | **L/R** (arms) | Respiratory triggered |
| 7 | `t2_haste_cor_obl_thin_slab_bh` | Coronal Oblique | On axial at porta hepatis: draw line through CBD toward pancreatic head (≈ ∥ pancreatic head). Single oblique | Single thick slab (~20–40 mm) through CBD from hilum → ampulla | **None** | Breath-hold |
| 8 | `t2_haste_sag_obl_thin_slab_bh` | Sagittal Oblique | On axial at gallbladder level: draw line along long axis of gallbladder.  | Single thick slab (~20–40 mm) through gallbladder, cystic duct, and cystic duct–CBD junction | **None** | Breath-hold |

*#1–#5: Shared liver protocol sequences — screen for parenchymal cause of obstruction (mass, stone, stricture).*  
*#6: T2 SPACE is a heavily T2 3D sequence — static fluid (bile, pancreatic juice) is bright, background is dark. Respiratory triggered to eliminate breathing motion. p2 = parallel imaging. MPR from the 3D volume provides ductal views in any plane. Slab covers the gallbladder, CBD, and entire pancreas.*  
*#7: Coronal oblique along the CBD. Single thick slab single-shot HASTE — acquired in <1 s, motion-free. Equivalent to an ERCP AP projection.*  
*#8: Sagittal oblique along the gallbladder. Single thick slab single-shot HASTE — captures the cystic duct insertion. Neither thin slab covers the full pancreatic duct; the SPACE MPR handles that.*  

---

## 3. Sequence Rationale

### Core Strategy

MRCP is a non-contrast ductal imaging protocol. The clinical question is biliary or pancreatic duct obstruction: what is the level (hilum, CHD, distal CBD, ampulla) and the cause (stone, stricture, mass)? The protocol uses heavily T2-weighted sequences where static fluid is bright — bile, pancreatic juice, and any obstructed duct.

There are no dynamic phases, no DWI, and no contrast. The T1 Dixon (#4) is included for anatomical reference and fat assessment (steatosis, fat-containing lesions that may compress ducts).

The core MRCP acquisition is the **T2 SPACE 3D** (#6) — respiratory-triggered volumetric heavily T2 with thin slices. MPR provides ductal views in any plane from this single acquisition. The thin-slab HASTEs (#7, #8) are projection images that replicate ERCP views.

The shared liver sequences (#1–#5) screen for extraductal pathology — a mass at the porta hepatis, pancreatitis, liver metastases — that may explain the ductal obstruction seen on MRCP.

---

**`t2_haste_cor_mbh` (#1)**
T2 HASTE coronal survey. Same as `liver_routine.md`. Provides an overview of the biliary tree, gallbladder, and pancreatic head in the coronal plane.

**`t2_tse_fs_tra_p2_mbh` (#2) / `t2_tse_tra_p2_mbh` (#3)**
T2 TSE axial pair — FS for lesion detection, non-FS for anatomical reference. Same as `liver_routine.md`. Coverage extends inferiorly to include the entire pancreas. A pancreatic head mass causing CBD obstruction must be visible on these sequences.

**`t1_vibe_dixon_tra_bh` (#4)**
T1 VIBE Dixon axial. For fat assessment (steatosis, intralesional fat), intrinsic T1-hyperintensity (blood products, proteinaceous content in a complicated cyst or mucinous lesion), and anatomical reference of the pancreas and biliary tree.

**`t2_trufi_cor_non-bh` (#5)**
T2 TrueFISP coronal. Blood and bile are bright without contrast. Portal vein, hepatic veins, and IVC patency — portal vein thrombosis or cavernous transformation can cause biliary compression (portal biliopathy).

---

**`t2_space_cor_obl_p2_trig_MRCP` (#6)**
T2 SPACE (Sampling Perfection with Application optimized Contrasts) — a 3D heavily T2 TSE with variable flip angles. Respiratory triggered (navigator or bellows) — the acquisition follows the breathing cycle, acquiring data only during a consistent respiratory phase. This eliminates respiratory ghosting from the 3D volume.

The slab is prescribed as a coronal oblique — angled on axial to cover the gallbladder, the entire CBD from hepatic hilum to ampulla, and the full pancreas (duct of Wirsung and duct of Santorini). MPR from the 3D volume provides axial, sagittal, and curved planar reformats of the biliary tree and pancreatic duct without additional acquisitions.

Static fluid is bright; the liver, pancreas, and bowel are dark. Stones appear as filling defects within the bright duct. Strictures appear as abrupt narrowing. The ampulla is the most challenging segment — periampullary duodenal fluid can obscure the distal CBD; fasting and negative oral contrast help.

---

**`t2_haste_cor_obl_thin_slab_bh` (#7)**
Single thick slab (~20–40 mm) T2 HASTE, coronal oblique. On axial T2 at the porta hepatis, draw a line through the CBD toward the pancreatic head — this approximates parallel to the pancreatic head on axial (single oblique, axial rotation only). This profiles the CBD from hepatic hilum through to the ampulla in a single projection. Equivalent to the ERCP AP radiograph. Breath-hold, acquired in <1 s. The pancreatic duct in the body and tail is not in this slab — the SPACE MPR covers the full pancreas.

**Purpose of the thin-slab HASTEs:** The SPACE 3D (#6) is respiratory triggered and takes several minutes — if breathing is irregular, the SPACE is degraded or non-diagnostic. The thin-slab HASTEs are acquired in <1 s each (single-shot), so they are intrinsically motion-free. They serve as the bail-out when the SPACE fails. They also produce the familiar ERCP-like projection images used for communication with referring clinicians — the SPACE MPRs are the diagnostic source data; the thin slabs are the clinical summary view.

The thin slab collapses the 3D volume into a single projection — the entire duct segment is visible in one image, but small filling defects may be averaged out. The SPACE (#6) provides the thin-slice source data for confirmation.

**`t2_haste_sag_obl_thin_slab_bh` (#8)**
Single thick slab T2 HASTE, sagittal oblique. On axial at the gallbladder level, draw a line along the long axis of the gallbladder (single oblique, axial rotation only). This profiles the gallbladder, cystic duct, and the cystic duct insertion into the CBD. The CBD itself is not profiled in this plane — it is seen in cross-section or oblique profile. The purpose is gallbladder pathology and the cystic duct junction.

---

## 4. Variations

- **3T:**
  - T2 SPACE (#6) is replaced by `t2_tse_cor_p2_trig` — a 2D thick-slab T2 TSE coronal with respiratory triggering. SPACE's long 3D refocusing pulse train exceeds SAR limits at 3T; the 2D TSE uses far fewer refocusing pulses. The 3T SNR advantage partly compensates for the thicker 2D slices. Trade-off: no MPR (2D, not 3D) — ductal reformats in other planes are not possible; small stones may be averaged out by thicker slices.
  - Add `t2_haste_fs_tra_mbh` as a motion-robust axial backup — 3T amplifies TSE respiratory ghosting from higher signal in moving spins.
  - Thin slab HASTEs (#7, #8) use fat saturation: `t2_haste_fs_cor/sag_obl_thin_slab_bh`. At 1.5T, FS on a single-shot HASTE is unreliable — lower B0 homogeneity means the fat sat pulse may fail patchily on a per-slice basis. Non-FS is safer: bile is bright, fat is intermediate signal, and the ductal projection is diagnostic without FS. At 3T, higher SNR and better B0 homogeneity make FS reliable on single-shot HASTE, and fat is brighter (longer T1) so suppressing it improves ductal conspicuity on the projection image.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Fasting** — Patient fasted 4–6 hours? Gastric/duodenal fluid signal obscuring the distal CBD? | If gastric fluid is T2-bright and overlies the ampulla: give negative oral contrast and re-acquire #6 and #7. If contrast already given: the SPACE MPR may provide a plane that avoids the fluid |
| **SPACE respiratory trigger** — Consistent respiratory phase? | If trigger is irregular (erratic breathing): switch from dome triggering to phase triggering.
  - **Dome trigger:** Navigator at the diaphragm — amplitude-based. Tracks the diaphragm boundary (liver-lung interface). Sharp signal boundary can be erratic with irregular breathing.
  - **Phase trigger:** Navigator at mid-liver — phase-based. The navigator profile shifts spatially as the liver moves; that displacement produces a phase shift (Fourier shift theorem). The acceptance window is set on that phase shift rather than on an anatomical boundary. The homogeneous liver parenchyma gives a cleaner phase signal — more consistent than dome triggering when breathing is erratic.
  If still non-diagnostic: the HASTE thin slabs (#7, #8) are motion-robust and may be the only diagnostic MRCP images |
| **Coverage** — Gallbladder, entire CBD, and entire pancreas in the SPACE slab (#6)? | If CBD clipped at the ampulla: the most common site of obstruction (distal CBD stone) is missed. Extend the slab inferiorly. If pancreatic tail clipped: pancreatitis or tail mass may be missed |
| **Thin slab planning** — Coronal oblique: line through CBD toward pancreatic head on axial? Sagittal oblique: line along gallbladder long axis on axial? | Single oblique on axial only — no craniocaudal tilt. If misaligned: the CBD or cystic duct is cut obliquely instead of profiled, exaggerating or hiding pathology |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-04 | — | Initial — 8 sequences (T2 liver screen + T2 SPACE 3D MRCP + 2 thin-slab HASTE projections). Non-contrast ductal protocol |
