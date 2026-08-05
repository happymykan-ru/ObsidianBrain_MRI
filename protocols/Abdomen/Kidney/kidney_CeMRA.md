# Kidney CeMRA (Renal MRI with Contrast-Enhanced MRA)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the renal arteries (slightly above the kidney centre, ~L1 level).
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** End-expiration breath-holds preferred. During the CeMRA: do not move — the subtraction mask and arterial phase must be perfectly co-registered.
- **IV Access:** Minimum 20G (pink). Injection rate: at least 2 mL/s; 3 mL/s preferred for tight CeMRA bolus. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_bh_p2` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both kidneys | **Superior oblique** over heart | Breath-hold |
| 2 | `t2_tse_fs_tra_p2_mbh` | Axial | True axial | Both kidneys. Upper pole → lower pole | **None** | Multi breath-hold |
| 3 | `t2_tse_tra_p2_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t1_vibe_twist_dixon_tra_pre` | Axial | True axial | Both kidneys | **None** | Breath-hold |
| 5 | `t2_trufi_sag_vessel` | Sagittal | True sagittal | Abdominal aorta, renal artery origins, and kidneys | **None** | Free breathing |

*#1–#3: T2 survey and lesion detection — same as kidney.md but no T1 Dixon (axial in/opp phase is dropped; the TWIST pre (#4) serves as anatomical T1 reference).*  
*#4: Pre-contrast TWIST baseline — water-only image. Also serves as the pre-contrast T1 for the single post-contrast T1 (#10 or #14).*  
*#5: TrueFISP sagittal — vessel scout. Profiles the abdominal aorta, renal artery origins, and the craniocaudal course of the renal arteries.*

### CeMRA — Choose One Pathway

**Pathway A — Care Bolus (visual triggering)**

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 6A | `angio3d_cor_pre` | Coronal | From vessel scout (#5). Slab covering the aorta and both renal arteries | Aorta (above renal origins) → distal renal arteries | **None** | Breath-hold |
| — | **Contrast** | — | Check FOV consistency. Standard dose, ≥2 mL/s | — | — | — |
| 7A | `care_bolus_cor` | Coronal | Copy Slice from #6A — select the slice with most overlap with the renal arteries on the vessel scout. Single monitoring slice | Single slice through renal arteries | **None** | Free breathing |
| 8A | `angio3d_cor_post_C` | Coronal | Copy Slice from #6A | — | **None** | Breath-hold |
| 9A | `t1_vibe_twist_dixon_tra_post` | Axial | Copy Slice from #4 | Both kidneys | **None** | Breath-hold, immediately after #8A |

*#6A: Pre-contrast mask for subtraction.*  
*#7A: Visual Care Bolus — radiographer watches the monitoring slice and triggers manually when contrast reaches the renal arteries.*  
*#8A: Arterial phase CeMRA — triggered immediately upon contrast arrival.*  
*#9A: Single post-contrast T1 — replaces the multiphasic dynamic phases in kidney.md. Acquired after the CeMRA (~60–90 s post-injection), approximating the nephrographic phase.*

**Pathway B — Test Bolus (measured transit time)**

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 6B | `angio3d_cor_pre` | Coronal | From vessel scout (#5). Slab covering the aorta and both renal arteries | Aorta (above renal origins) → distal renal arteries | **None** | Breath-hold |
| 7B | `test_bolus_tra` | Axial | Single slice through the descending aorta, above the renal artery origins | Single slice through descending aorta | **None** | Free breathing. Dynamic acquisition over ~60 s after test dose injection |
| — | **Contrast** | — | Check FOV consistency. Standard dose, ≥2 mL/s, timed to the measured transit delay | — | — | — |
| 8B | `angio3d_cor_post_C` | Coronal | Copy Slice from #6B | — | **None** | Breath-hold |
| 9B | `t1_vibe_twist_dixon_tra_post` | Axial | Copy Slice from #4 | Both kidneys | **None** | Breath-hold, immediately after #8B |

*#6B: Pre-contrast mask for subtraction.*  
*#7B: Test bolus — a small test dose (~2 mL) is injected and a dynamic single-slice acquisition at the descending aorta (above the renal origins) measures the arm-to-aorta transit time. The measured delay is used to time the full-dose CeMRA (#8B).*  
*#8B: Arterial phase CeMRA — timed to the measured transit delay from the test bolus.*  
*#9B: Single post-contrast T1 — nephrographic phase, same as Pathway A.*

---

## 3. Sequence Rationale

### Core Strategy

This is a combined renal mass characterization + renal artery MRA. The clinical question is twofold: (1) is there a renal artery stenosis (renovascular hypertension workup, pre-operative planning for partial nephrectomy), and (2) is there a renal mass? The protocol replaces the multiphasic dynamic phases of `kidney.md` (AP, PVP, delayed) with a CeMRA + a single nephrographic-phase T1.

**Key differences from `kidney.md`:**

- **No T1 VIBE Dixon** — the axial Dixon (in/opp phase) is dropped. The TWIST pre (#4) serves as the anatomical T1 reference. Chemical shift assessment is not the primary goal when MRA is the indication.
- **No multiphasic dynamics** — AP, PVP, and delayed phases are replaced by a single post-contrast T1 acquired after the CeMRA. This single acquisition falls in the nephrographic window (~60–90 s) and provides renal parenchymal assessment. Enhancement kinetics and washout are sacrificed; the mass is characterized by T2 signal, DWI (if added), and the single post-contrast T1 rather than a full dynamic series.
- **No DWI** — DWI would prolong the exam and compete with CeMRA timing. If mass characterization is critical, DWI can be added pre-contrast.
- **TrueFISP sagittal** — replaces the coronal TrueFISP in `kidney.md`. The sagittal plane profiles the aorta and renal artery origins (the renal arteries arise from the anterior aortic wall at L1–L2 and course posteriorly to the renal hila). This is the vessel scout for CeMRA planning.
- **CeMRA** — the central sequence. Coronal slab covering the aorta and both renal arteries. Subtraction of the pre-contrast mask (#6A/B) from the post-contrast acquisition (#8A/B) produces a pure renal arteriogram.

---

### Care Bolus vs Test Bolus

**Care Bolus (Pathway A):** A single coronal monitoring slice is placed through the renal arteries. The radiographer watches in real time and must prepare the breath-hold in advance: instruct the patient to breath-hold when contrast is seen entering the left ventricle (before it reaches the aorta). The CeMRA is triggered when contrast arrives at the renal arteries.
- **Advantage:** Simpler, faster, no extra contrast dose.
- **Disadvantage:** Relies on operator reaction time and judgement; venous reflux or mistiming can degrade the arterial phase.
**Choice:** Care Bolus is the default.

**Test Bolus (Pathway B):** A small test dose (~2 mL) is injected and a dynamic axial single-slice acquisition is placed at the level of the descending aorta **before** the renal artery origins. The exact transit time from arm vein to descending aorta is measured from the time-intensity curve. The full-dose CeMRA delay is calculated from this measured transit.
- **Advantage:** More accurate timing — accounts for individual haemodynamics.
- **Disadvantage:** The small test dose (~2 mL) recirculates and may appear in the renal veins during the subsequent full-dose CeMRA, contaminating the subtraction; extra contrast dose (relevant in renal patients).
- **Indication:** When transit time may be abnormal (heart failure → prolonged; aortic aneurysm → turbulent flow/delayed; central venous stenosis or SVC obstruction → collateral rerouting; severe aortic stenosis → reduced output). Also when precise timing is critical: renal transplant assessment, suspected accessory renal artery stenosis.

---

### Sequence Details

**TrueFISP sagittal (#5):** Profiles the abdominal aorta and renal artery origins. The renal arteries arise from the anterior aortic wall and course posteriorly to the hila. The sagittal plane shows the craniocaudal level of each renal artery origin (right is typically higher than left, though variable). Used to plan the CeMRA coronal slab.

**Angio3D coronal (#6A/B, #8A/B):** The coronal slab is prescribed from the vessel scout to cover the aorta from above the renal origins to below, and both renal arteries laterally to the hila. Same coronal CeMRA rationale as `CeMRA.md` — the coronal plane puts the craniocaudal aortic axis in-plane. Care Bolus uses visual triggering; Test Bolus uses the measured transit delay.

**Post-contrast T1 (#9A/B):** Single axial acquisition — falls in the nephrographic window (~60–90 s post-injection, depending on CeMRA acquisition time and transit). Renal parenchyma uniformly enhances. Replaces the dedicated AP, PVP, and delayed phases of `kidney.md`. The mass is assessed on the single nephrographic image; there is no washout or delayed phase characterization.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both kidneys on all sequences? CeMRA slab covers aorta and both renal arteries to the hila? | Reposition if clipped. Accessory renal arteries arise from the aorta below the main renal origins — if the CeMRA slab ends at the main renal artery, an accessory artery is missed |
| **Care Bolus** — Contrast arrival visually confirmed at the renal arteries? | If triggered late: venous contamination. If triggered early: insufficient arterial filling. If mistimed: the single post-contrast T1 (#9A/B) still provides nephrographic parenchymal assessment |
| **Test Bolus** — Transit time measured accurately? ROI placed correctly on the renal artery? | If the ROI is misplaced (renal vein instead of artery, or off-target): the measured delay is wrong and the CeMRA will be mistimed |
| **Post-contrast** — Contrast present? Renal parenchyma enhancing on #9A/B? | If absent: check IV line, confirm injection. The CeMRA (#8A/B) also confirms contrast delivery |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 9 sequences (CeMRA + single nephrographic T1). Two pathways: Care Bolus or Test Bolus. No multiphasic dynamics, no DWI |
