# Pancreas (Dedicated Pancreas MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-04 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-pancreas (L1–L2 level, slightly inferior to liver centring).
- **Laser Landmark:** Xiphoid or slightly below (mid-pancreas level)
- **Verbal Instructions:** End-expiration breath-holds preferred — reproducible diaphragm position. Same breath-hold depth across all sequences.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].
- **Patient Preparation:** Fasting is not required. The primary purpose is pancreatic parenchymal imaging (mass characterization, enhancement kinetics, vascular staging). The optional ERCP sequence (#6) may have reduced ductal visualization quality from gastric/duodenal fluid in a non-fasted patient — this is acceptable because (1) the pancreatic duct is still assessed on the heavy T2 axial (#3), and (2) if high-quality ductal imaging were the clinical priority, a dedicated fasted MRCP would have been ordered. 
---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Whole pancreas | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_tse_fs_tra_pancreas` | Axial | True axial | Pancreas only. Head → tail + ampulla | **None** | Multi breath-hold |
| 3 | `t2_heavy_tse_fs_tra_mbh_pancreas` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t2_haste_tra_p2_mbh_pancreas` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 5 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Pancreas only | **None** | Breath-hold |
| 6 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 7 | `t2_space_cor_p2_trig_ERCP` | Coronal Oblique | Angle on axial to cover the pancreas and CBD | Pancreas + ampulla. CBD from hilum → ampulla | **L/R** (arms) | Respiratory triggered |
| 8 | `t1_vibe_twist_dixon_tra_pre` | Axial | Copy Slice from #5 | — | **None** | Breath-hold |

*#1–#5: Liver screen sequences adapted for pancreas-only coverage. See `liver_routine.md` for individual sequence rationale (same sequences, different coverage).*  
*#6: TrueFISP coronal — vessels and bile bright without contrast. Portal vein, splenic vein, SMV patency.*  
*#7: Optional — only if no prior MRCP. T2 SPACE for pancreaticobiliary ductal assessment (3T: `t2_tse3d_cor_p2_trig_ERCP`). Same technique as MRCP.md. If a recent MRCP exists, skip this sequence.*  
*#8: Pre-contrast TWIST baseline — water-only image. Same as liver_routine.md.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency — verify post-contrast FOV matches pre-contrast #8. Standard dose, 2 mL/s | — | — | — |
| 9 | `t1_vibe_twist_dixon_tra_bh_art_5phase` | Axial | Copy Slice from #8 | Pancreas only | **None** | Breath-hold. Fixed delay 30 s |
| 10 | `t1_vibe_twist_dixon_tra_PVP` | Axial | Copy Slice from #8 | — | **None** | Breath-hold, 20 s after #9 |
| 11 | `t1_vibe_twist_dixon_tra_Delay_2min` | Axial | Copy Slice from #8 | — | **None** | Breath-hold, ~2 min |
| 12 | `ep2d_diff_b50_300_800_tra_pancreas` | Axial | Copy Slice from #8 | Pancreas only | **None** | Free breathing |

*#9–#11: Dynamic phases — same as liver_routine.md but pancreas-only coverage.*  
*#12: DWI — same b-values as liver. Pancreas-only FOV for higher in-plane resolution.*  

---

## 3. Sequence Rationale

### Core Strategy

Dedicated pancreas MRI characterizes a known or suspected pancreatic lesion (adenocarcinoma, pancreatic neuroendocrine tumour [PNET], pancreatitis, cystic lesion) and stages local extent (vascular involvement, nodal disease, metastases). The protocol is essentially a liver protocol with pancreas-only coverage, plus an optional MRCP sequence for ductal assessment.

**Key differences from `liver_routine.md`:**

- **Coverage is pancreas-only** — all axial sequences are prescribed to cover the pancreas from head to tail with a small FOV for higher in-plane resolution. The liver is not included.
- **Heavy T2 axial retained** — in liver protocols, heavy T2 separates fluid from solid lesions. In pancreas, it images the pancreatic duct (dilated duct = obstruction by mass or stricture) and characterizes cystic lesions (IPMN, mucinous cystic neoplasm, pseudocyst). The duct and cyst contents are bright.
- **Optional ERCP sequence (#7)** — only if no prior MRCP. Same T2 SPACE/TSE as `MRCP.md`, focused on the pancreaticobiliary junction. If a recent MRCP is available, skip to avoid redundancy.
- **No delayed 5 min** — pancreatic enhancement peaks at PVP and washes out by 2 min; 5 min adds no diagnostic value for pancreas. The 2 min delayed phase covers fibrous tumour stroma (pancreatic adenocarcinoma is desmoplastic) and capsular enhancement.
- **DWI pancreas-only** — small FOV, high in-plane resolution. Restricted diffusion in a pancreatic mass = highly cellular (adenocarcinoma, PNET, lymphoma). In pancreatitis, diffusion is facilitated (oedema). DWI also detects small liver metastases on the b=50 or b=800 images if liver coverage overlaps incidentally.

---

### Pre-Contrast

**T2 sequences (#1–#4):** Same logic as `liver_routine.md` but pancreas-only. HASTE coronal survey (#1) — A/P from anterior to posterior abdominal wall. The pancreas is retroperitoneal and its exact position varies with patient habitus; covering the full A/P extent ensures it is included. T2 TSE FS (#2) = primary lesion detection — a pancreatic mass is mildly T2-hyperintense against the intermediate-signal parenchyma. Heavy T2 (#3) = pancreatic duct and cystic lesion assessment. HASTE non-FS (#4) = motion-robust T2 anatomical reference.

**T2 TrueFISP (#6):** Same as `liver_routine.md` — vessels and bile bright without contrast. Portal vein, splenic vein, and SMV patency assessed in the coronal plane.

**T1 VIBE Dixon (#5):** Same as `liver_routine.md` — in/opp phase for fat (diffuse fatty infiltration of the pancreas, intralesional fat in lipoma or well-differentiated PNET), intrinsic T1-hyperintensity (blood products in haemorrhagic pancreatitis, proteinaceous content in mucinous lesions).

**T2 SPACE ERCP (#7):** Optional — performed only if no prior MRCP exists. On a first-time pancreas MRI, the ductal anatomy must be established: is the pancreatic duct dilated (upstream mass or stricture), is there ductal communication with a cystic lesion (IPMN — side-branch or main-duct type), is there an anomalous pancreaticobiliary junction? The SPACE profiles the entire duct in one acquisition. If a recent MRCP already answers these questions, skip this sequence — the heavy T2 axial (#3) provides sufficient ductal assessment for follow-up. See `MRCP.md` for full technique rationale (3T uses T2 TSE 3D).

**T1 TWIST pre (#8):** Same as `liver_routine.md` — pre-contrast baseline for dynamic phases. Water-only image only.

---

### Post-Contrast

**Arterial phase (#9):** Same timing and 5-phase TWIST as `liver_routine.md`. Arterial phase is critical for:
- **Pancreatic neuroendocrine tumour (PNET, hypervascular):** Brightly enhancing against the non-enhancing pancreas background. The arterial phase is the most sensitive for detecting small PNETs.
- **Adenocarcinoma (hypovascular):** Hypoenhancing relative to pancreas. Best seen on PVP, but the arterial phase assesses arterial anatomy for surgical planning (SMA, coeliac axis, hepatic artery variants).
- **Arterial involvement:** Tumour encasement or narrowing of the SMA, coeliac trunk, or hepatic artery = unresectable.

**Portal venous phase (#10):** Same as `liver_routine.md`. This is the **most important phase for pancreatic adenocarcinoma** — the normally enhancing pancreatic parenchyma is bright, and the hypovascular tumour is dark. Maximum tumour-to-parenchyma contrast. Also assesses:
- **Venous involvement:** SMV, portal vein, splenic vein — tumour abutment or encasement determines resectability.
- **Liver metastases:** Hypovascular metastases (colorectal-type pattern) are most conspicuous on PVP as hypoenhancing nodules against enhancing liver.

**Delayed 2 min (#11):** Pancreatic adenocarcinoma is desmoplastic with abundant fibrous stroma — contrast is retained in the extracellular matrix, producing delayed persistent enhancement. The tumour may appear less distinct at 2 min than at PVP (the parenchymal enhancement washes out but the fibrotic tumour retains contrast). Useful for characterizing the fibrous component of the tumour.

**DWI (#12):** Same as `liver_routine.md` — b=50, 300, 800. Pancreas-only FOV. Restricted diffusion = cellularity (adenocarcinoma, PNET, lymphoma). DWI also provides a screen for liver metastases within the incidental coverage.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Whole pancreas from head to tail on all sequences? Ampulla included? | Reposition if tail clipped (splenic hilum). The pancreatic tail is the most commonly missed region — it extends to the splenic hilum, further lateral than expected |
| **Breath-hold consistency** — Same depth as liver protocol | See `liver_routine.md` Alerts |
| **Arterial phase** — Coeliac axis and SMA brightly opacified, pancreatic parenchyma still dark? | The optimal pancreatic arterial window is earlier than the liver arterial window — the pancreas has purely arterial supply. Once the parenchyma begins enhancing, a hypervascular PNET becomes isointense and may be invisible. The liver arterial marker (portal vein bright, hepatic veins dark) is already too late for pancreas. Review all 5 TWIST phases for the earliest frame with arterial opacification and non-enhancing parenchyma |
| **DWI** — Small-FOV pancreas DWI diagnostic? | EPI at the pancreatic tail suffers from susceptibility artefact at the stomach (air-fluid interface). If distorted: the pancreatic head and body should still be diagnostic |
| **ERCP sequence** — Only if no prior MRCP? | If recent MRCP is available: skip #6. Avoid redundant acquisition |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-04 | — | Initial — 12 sequences. Pancreas-only FOV. TrueFISP coronal. Optional ERCP sequence. Dynamic phases per liver_routine. No delayed 5 min |
