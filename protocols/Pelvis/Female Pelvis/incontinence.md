# Incontinence (Pelvic Floor MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the symphysis pubis.
- **Laser Landmark:** Symphysis pubis
- **Verbal Instructions:** Shallow breathing throughout. Do not perform a Valsalva or straining manoeuvre during the acquisition — images are acquired at rest. Dynamic straining sequences may be added separately if required.
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].
- **Patient Preparation:** Moderately full bladder — the bladder base and urethrovesical junction are better delineated against a distended bladder. The patient may be asked to void partially if overdistended.

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_tse_sag` | Sagittal | True sagittal | Pelvic floor. Pubic symphysis → sacrum/coccyx. L/R: both levator ani origins | **None** | Free breathing |
| 2 | `t2_tse_tra` | Axial | True axial | Pelvic floor. Bladder base → perineum | **None** | Free breathing |
| 3 | `t2_tse_cor` | Coronal | True coronal | Pelvic floor. A/P: pubic symphysis → sacrum | **None** | Free breathing |
| 4 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #1 | — | **None** | Free breathing |
| 5 | `t1_vibe_dixon_tra_pre` | Axial | Copy Slice from #2 | Pelvic floor | **None** | Breath-hold |

*#1–#3: T2 TSE in 3 planes — pelvic floor anatomy. Levator ani, puborectalis, endopelvic fascia, urethra, bladder neck, vagina, rectum.*  
*#4: T2 SPACE sagittal — 3D T2 with isotropic resolution. MPR for pelvic floor assessment in any plane.*  
*#5: T1 VIBE Dixon axial — pre-contrast baseline. In/opposed phase for fat.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. No specific delay required | — | — | — |
| 6 | `t1_vibe_dixon_tra_C` | Axial | Copy Slice from #5 | Pelvic floor | **None** | Breath-hold |
| 7 | `t1_vibe_dixon_cor_C` | Coronal | Copy Slice from #3 | Pelvic floor | **None** | Breath-hold |

*#6–#7: Post-contrast T1 axial + coronal. Enhancing cystocele/rectocele mucosa and pelvic floor soft tissues.*  

---

## 3. Sequence Rationale

### Core Strategy

Pelvic floor MRI assesses the anatomical integrity of the pelvic floor support structures in patients with urinary incontinence or pelvic organ prolapse. The clinical question: is there a levator ani defect, puborectalis tear, or endopelvic fascial weakness explaining the patient's symptoms? The protocol is a high-resolution anatomical survey of the entire pelvic floor, supplemented by post-contrast T1 for organ descent visualization.

**Key differences from `urethral_diverticulum.md`:**

- **Coverage is the entire pelvic floor** — pubic symphysis to sacrum/coccyx, levator origins to hiatus. Diverticulum is small FOV focused on the urethra only.
- **T2 SPACE sagittal added** — 3D T2 for pelvic floor anatomy. Levator ani defects, puborectalis tears, and endopelvic fascial integrity are assessed. MPR provides views in any plane. Diverticulum does not need this.
- **No post-micturition sequences** — incontinence is an anatomical assessment at rest. Voiding dynamics are evaluated on clinical exam and urodynamics. Diverticulum needs post-void imaging to demonstrate retained contents.
- **No specific contrast delay** — contrast enhances the pelvic floor soft tissues and cystocele/rectocele mucosa. Diverticulum uses a 60 s delay for inflamed wall enhancement.

---

### Pre-Contrast

**T2 TSE sagittal (#1):** The primary pelvic floor plane. Shows the bladder base, urethrovesical junction, urethra, vagina, and rectum in one view. The pubococcygeal line (PCL — from the inferior pubic symphysis to the last coccygeal joint) is drawn on this plane; organ descent below the PCL on straining defines prolapse. At rest, the bladder base and cervix/vaginal vault should be above the PCL.

**T2 TSE axial (#2):** Profiles the levator ani sling in cross-section — the puborectalis and iliococcygeus muscles form a U-shaped sling around the urethra, vagina, and rectum. A levator ani defect appears as discontinuity or thinning of the muscle. The axial plane also shows the endopelvic fascia and the urethral support ligaments.

**T2 TSE coronal (#3):** Profiles the levator ani origins from the pubic bone and arcus tendineus. A tear at the pubic insertion (the most common site of levator injury) is best seen coronally. Also shows the obturator internus and pelvic sidewall.

**T2 SPACE sagittal (#4):** 3D T2 with isotropic resolution. MPR provides reformatted views of the pelvic floor in any plane — useful for measuring levator ani bulk, identifying fascial defects, and assessing the pelvic floor hiatus dimensions. SPACE also gives a volumetric overview for surgical planning.

**T1 VIBE Dixon axial (#5):** Pre-contrast baseline. In/opposed phase for any incidental fat-containing lesions.

---

### Post-Contrast

**T1 VIBE Dixon axial + coronal (#6, #7):** Post-contrast T1. Enhancing pelvic floor soft tissues, cystocele mucosa (contrast pools in the dependent portion of the prolapsed bladder), and rectocele. The coronal plane shows the levator ani origins and pelvic sidewall enhancement. No specific contrast delay is required — enhancement of the pelvic floor is not time-critical.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Entire pelvic floor from pubic symphysis to coccyx on all sequences? Levator ani origins included? | Reposition if clipped. The levator ani origins at the pubic bone are the most common site of injury — if not included, the primary anatomical question cannot be answered |
| **Bladder filling** — Moderately full bladder? | If empty: the bladder base and urethrovesical junction are collapsed. If overdistended: the bladder may displace pelvic structures. The patient should not void before the exam |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 7 sequences. T2 in 3 planes + T2 SPACE + pre/post T1 Dixon. Pelvic floor anatomical protocol |
