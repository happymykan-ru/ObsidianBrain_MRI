# Urethral Diverticulum (Urethral Diverticulum MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the symphysis pubis.
- **Laser Landmark:** Symphysis pubis
- **Verbal Instructions:** Shallow breathing throughout. The patient will be asked to void mid-exam — explain the sequence of events before starting (scan → contrast → post-contrast imaging → void → post-micturition imaging).
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].
- **Patient Preparation:** The patient should have a moderately full bladder before the exam — the urethra is better visualised against a distended bladder. Instruct the patient not to void before the scan.

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_tse_sag` | Sagittal | True sagittal | Urethra + bladder base + vagina. Small FOV | **None** | Free breathing |
| 2 | `t2_tse_tra` | Axial | True axial | Urethra + periurethral region. Small FOV | **None** | Free breathing |
| 3 | `t2_tse_cor` | Coronal | True coronal | Urethra + bladder base. Small FOV | **None** | Free breathing |
| 4 | `t1_vibe_fs_tra_pre` | Axial | Copy Slice from #2 | Urethra + periurethral region | **None** | Breath-hold |

*#1–#3: T2 TSE in 3 planes, small FOV. The urethral diverticulum is a T2-hyperintense sac-like structure arising from the urethra, often horseshoe-shaped wrapping around the posterior/lateral urethral wall.*  
*#4: Pre-contrast T1 FS — baseline for enhancement.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. Delay 60 s before scanning | — | — | — |
| 5 | `t1_vibe_fs_tra_C` | Axial | Copy Slice from #4 | Urethra + periurethral region | **None** | Breath-hold |
| 6 | `t1_vibe_dixon_cor_C` | Coronal | Copy Slice from #3 | Urethra + bladder base | **None** | Breath-hold |

*#5–#6: Post-contrast at 60 s delay. The diverticulum wall enhances (inflamed). The 60 s delay allows contrast accumulation in the wall without filling the diverticulum lumen.*  

### Post-Micturition

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Patient voids** | — | Explain to the patient: void as much as possible, then return to the table | — | — | — |
| 7 | `localizer_trufi_post_micturition` | 3-plane | — | Bladder + urethra | — | Free breathing |
| 8 | `t1_vibe_fs_tra_post_micturition_C` | Axial | Copy Slice from #5 | Urethra + periurethral region | **None** | Breath-hold |

*#7: Quick TrueFISP localizer to re-check positioning after voiding.*  
*#8: Post-micturition T1 FS axial. Retained contrast/urine in the diverticulum after voiding confirms the diagnosis — the diverticulum does not empty with micturition.*  

---

## 3. Sequence Rationale

### Core Strategy

Urethral diverticulum MRI confirms the diagnosis by demonstrating a fluid-filled, enhancing sac arising from the urethra that retains contents after voiding. The clinical presentation is often non-specific (urinary frequency, dysuria, post-void dribbling) — MRI is the gold standard for diagnosis. The protocol combines high-resolution T2 in three planes with pre/post-contrast T1 and the critical post-micturition sequence.

---

### Pre-Contrast

**T2 TSE sagittal (#1):** Profiles the urethra in its long axis — the diverticulum appears as a T2-hyperintense sac arising from the posterior or lateral urethral wall, often extending cranially behind the bladder base. The sagittal plane shows the relationship to the bladder, vagina, and pubic symphysis.

**T2 TSE axial (#2):** The primary plane for diverticulum morphology. The classic horseshoe configuration — the diverticulum wraps around the posterior and lateral aspects of the urethra — is best seen axially. The axial plane also shows the neck of the diverticulum connecting to the urethral lumen, and any septations or stones within the sac.

**T2 TSE coronal (#3):** Coronal plane profiles the craniocaudal extent of the diverticulum and its relationship to the bladder neck and pelvic floor.

**T1 VIBE FS axial pre (#4):** Pre-contrast baseline. The diverticulum may contain proteinaceous or haemorrhagic fluid, appearing T1-hyperintense — this intrinsic signal must be distinguished from enhancement post-contrast.

---

### Post-Contrast

**T1 VIBE FS axial + coronal (#5, #6):** Delayed 60 s post-injection. The diverticulum wall enhances — it is lined with inflamed urothelium and granulation tissue. The lumen remains dark (unenhanced urine/fluid). Enhancement of the wall confirms the diverticulum is the source of symptoms (active inflammation). A non-enhancing sac may be a simple paraurethral cyst rather than an inflamed diverticulum. The 60 s delay allows contrast accumulation in the inflamed wall without filling the lumen — earlier phases may be isointense to surrounding tissues.

---

### Post-Micturition

The diagnostic hallmark: after the patient voids, the bladder empties but the diverticulum does not. **`t1_vibe_fs_tra_post_micturition_C` (#8):** Retained fluid (urine mixed with excreted contrast) persists within the diverticulum — it remains T1-bright while the bladder is empty. A structure that empties with micturition is not a diverticulum (it may be a cystocele or normal urethral configuration). The TrueFISP localizer (#7) repositions after the patient returns from voiding before acquiring the diagnostic post-micturition image.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Bladder filling** — Moderately full bladder before the exam? | If empty: the urethra is collapsed and the diverticulum neck may not be visible. If overdistended: the diverticulum may be compressed by the full bladder. Instruct the patient not to void before the exam |
| **Post-micturition** — Patient able to void? Bladder empty on post-micturition images? Diverticulum retains fluid? | If the patient cannot void: the diagnosis is not excluded but the most specific finding (retained contents) cannot be assessed. If the diverticulum empties: reconsider the diagnosis |
| **Post-micturition positioning** — Same FOV and slice position as pre-void? | The patient must be repositioned identically after voiding. The TrueFISP localizer (#7) confirms alignment; adjust as needed before the post-micturition T1 (#8) |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 8 sequences. T2 in 3 planes + delayed post-contrast T1 + post-micturition imaging. 60 s contrast delay |
