# Endometriosis (Deep Infiltrating Endometriosis MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-pelvis.
- **Immobilization:** Pelvic binder.
- **Laser Landmark:** Centre of body coil
- **Verbal Instructions:** Shallow breathing throughout.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to exam. Paralyses bowel — reduces peristaltic motion that degrades the high-resolution sagittal images of the rectovaginal septum and pouch of Douglas. Contraindications: glaucoma, urinary retention, myasthenia gravis, tachyarrhythmia.
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Buscopan** | — | 10–20 mg IV, prior to exam | — | — | — |
| 1 | `t2_tse_sag` | Sagittal | True sagittal | Pelvis. Uterus + rectovaginal septum + pouch of Douglas + bladder. L/R: both adnexae | **None** | Free breathing |
| 2 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #1 | — | **None** | Free breathing |
| 3 | `t2_tse_tra` | Axial | True axial | Pelvis. Iliac crest → perineum. Both ovaries + pelvic sidewall | **None** | Free breathing |
| 4 | `resolve_diff_b50_800_tra` | Axial | Copy Slice from #3 | Pelvis | **A/P** (anterior + posterior skin margins) | Free breathing |
| 5 | `t1_vibe_dixon_tra_pre` | Axial | Copy Slice from #3 | Pelvis | **None** | Breath-hold |

*#1: T2 TSE sagittal — the primary plane for DIE. Pouch of Douglas, rectovaginal septum, uterosacral ligaments, and bladder dome profiled in one view.*  
*#2: T2 SPACE sagittal — 3D T2 with MPR for any plane.*  
*#3: T2 TSE axial — ovaries, pelvic sidewall, uterosacral ligament origins.*  
*#4: DWI b=50, 800 — endometriomas and incidental findings.*  
*#5: T1 VIBE Dixon axial — pre-contrast baseline. Haemorrhagic endometriomas are T1-hyperintense — must be documented before contrast.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. No specific delay required | — | — | — |
| 6 | `t1_vibe_dixon_tra_C` | Axial | Copy Slice from #5 | Pelvis | **None** | Breath-hold |
| 7 | `t1_vibe_dixon_sag_C` | Sagittal | Copy Slice from #1 | Pelvis. Uterus + rectovaginal septum + pouch of Douglas | **None** | Breath-hold |

*#6–#7: Post-contrast T1 axial + sagittal. Enhancing peritoneal deposits and endometriotic nodules.*  

---

## 3. Sequence Rationale

### Core Strategy

Deep infiltrating endometriosis (DIE) MRI maps the extent of endometriotic deposits for surgical planning. The clinical question: which compartments are involved (anterior — bladder; middle — uterus, ovaries; posterior — rectovaginal septum, rectum, uterosacral ligaments), and how deeply do the deposits infiltrate? The protocol uses high-resolution T2 sagittal as the primary plane (the pouch of Douglas and rectovaginal septum are profiled sagittally), T1 pre-contrast to identify haemorrhagic endometriomas, and post-contrast T1 for enhancing peritoneal deposits.

---

### Plane Choices

- **Sagittal is the primary diagnostic plane.** The pouch of Douglas, rectovaginal septum, uterosacral ligaments, and bladder dome are all profiled in one sagittal view. An endometriotic nodule appears as T2-dark fibrotic tissue infiltrating the rectovaginal fat plane or tethering the rectum to the posterior cervix. The depth of invasion into the rectal wall (serosa → muscularis → submucosa) is assessed sagittally. The bladder dome deposit is also sagittally profiled.
- **Axial is the complementary plane.** The ovaries are assessed for endometriomas (T1-bright, T2-dark cystic lesions with "shading" on T2 from chronic haemorrhage). The pelvic sidewall and uterosacral ligament origins are profiled axially. Post-contrast axial shows enhancing peritoneal deposits along the broad ligament and pelvic sidewall.
- **No dedicated coronal T2.** The sagittal and axial planes plus SPACE MPR provide sufficient coverage. The coronal plane adds little for the rectovaginal septum (which runs A/P and is profiled sagittally) or the uterosacral ligaments (which run A/P from the cervix to the sacrum).
- **T1 pre-contrast is essential.** Endometriomas contain blood products at various stages — they are intrinsically T1-hyperintense without contrast. If only post-contrast T1 is acquired, haemorrhagic endometriomas are indistinguishable from enhancing masses. Pre-contrast T1 must be documented.

---

### Pre-Contrast

**T2 TSE sagittal (#1):** The primary plane. The rectovaginal septum is a thin fat plane between the posterior cervix/vagina and the anterior rectal wall. DIE obliterates this fat plane — the rectum is tethered posteriorly toward the cervix/uterus (retroflexed uterus with "kissing ovaries" sign). Endometriotic nodules are T2-dark fibrotic tissue. The depth of rectal wall invasion — serosal tethering vs muscularis involvement vs submucosal nodule — determines the surgical approach (shave vs disc resection vs segmental resection). The uterosacral ligaments are assessed for thickening and nodularity. The bladder dome is assessed for an anterior compartment deposit.

**T2 SPACE sagittal (#2):** 3D T2 with isotropic MPR — provides reformatted views in any plane for surgical mapping.

**T2 TSE axial (#3):** Ovaries — endometriomas are T2-dark cysts (chronic haemorrhage produces T2 shortening, the "shading" sign). Bilateral endometriomas often adherent behind the uterus = "kissing ovaries." Pelvic sidewall and uterosacral ligament origins. Hydrosalpinx (associated tubal disease).

**DWI (#4):** Endometriomas can show restricted diffusion — not a diagnostic feature of endometriosis per se, but useful for distinguishing endometrioma from functional cyst. Also screens for incidental pelvic malignancy (endometrial cancer, ovarian cancer — both show restricted diffusion).

**T1 VIBE Dixon axial (#5):** Pre-contrast T1. Endometriomas are T1-hyperintense from blood products (methaemoglobin). This intrinsic T1 signal must be documented before contrast — otherwise a T1-bright endometrioma post-contrast is ambiguous (blood products vs enhancement).

---

### Post-Contrast

**T1 VIBE Dixon axial + sagittal (#6, #7):** Enhancing peritoneal deposits — endometriotic implants are vascularized and enhance with contrast. An enhancing nodule in the rectovaginal septum or along the uterosacral ligament confirms active endometriosis. Endometriomas do not enhance (the cyst wall may enhance mildly, but the contents remain unenhanced). No specific contrast delay is required.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **T1 pre-contrast** — Acquired before contrast? Endometriomas T1-hyperintense? | If only post-contrast T1 is acquired: haemorrhagic endometriomas are indistinguishable from enhancing lesions. The pre-contrast T1 (#5) is essential |
| **Sagittal coverage** — Pouch of Douglas, rectovaginal septum, and bladder dome included? | If the rectovaginal septum is clipped: DIE cannot be excluded. The sagittal FOV must extend from the bladder anteriorly to the sacrum posteriorly |
| **Bowel preparation** — Rectum adequately empty? | If the rectum is full of stool: the rectovaginal septum is compressed — DIE assessment is limited. Rectal emptying (micro-enema or fasting) may be required |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 7 sequences. T2 sagittal primary plane + axial + SPACE + DWI + pre/post T1 Dixon. Sagittal + axial post-contrast |
