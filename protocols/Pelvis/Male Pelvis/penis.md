# Penis (Penile MRI with Dynamic Contrast — Peyronie's / Cancer / Fracture)

**Version:** 1.0 | **Date:** 2026-08-07 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Small FOV centred over the penis.
- **Penis Positioning:** The penis should be gently straightened and positioned on the anterior abdominal wall (pointing cranially). A folded towel placed between the thighs supports the scrotum and elevates the testes. If the penis is left draped over the scrotum, the shaft curves and the short-axis plane cannot be consistently defined along the length.
- **Immobilization:** The penis may be gently secured with tape to the lower anterior abdominal wall in a neutral, straight position — this prevents motion and maintains a consistent long axis for planning. Do not stretch or distort.
- **Laser Landmark:** Symphysis pubis
- **Verbal Instructions:** Shallow breathing throughout. No breath-hold required during the dynamic acquisition — but the patient must remain still to avoid misregistration on subtraction images.
- **IV Access:** 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t1_vibe_dixon_bh_tra_pelvis` | Axial | True axial | Pelvis. Iliac crests → below symphysis pubis. FOV 320 mm | **None** | Breath-hold |
| 2 | `t2_space_sag` | Sagittal | True sagittal | Penis + penile root + pubic symphysis + prostate + bladder base. L/R: both hemiscrotums if testes are in FOV | **None** | Free breathing |
| 3 | `t2_tse_tra_short_axis_penis` | Axial Oblique (Short Axis) | ⟂ long axis of penile shaft (planned from #2) | Penis only. Penile root → glans tip | **None** | Free breathing |
| 4 | `t2_tse_cor_long_axis_penis` | Coronal Oblique (Long Axis) | ∥ long axis of penile shaft (planned from #2) | Penis full length. Crura at ischial rami → glans tip. A/P: dorsal skin surface → ventral skin surface | **None** | Free breathing |
| 5 | `stir_tse_tra_short_axis_penis` | Axial Oblique (Short Axis) | Copy Slice from #3 | Copy Slice from #3 | **None** | Free breathing |
| 6 | `stir_tse_sag` | Sagittal | Copy Slice from #2 | Copy Slice from #2. Penis full length | **None** | Free breathing |
| 7 | `t1_vibe_dixon_sag_pre` | Sagittal | Copy Slice from #2 | Penis only. Pre-contrast baseline | **None** | Breath-hold |

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Standard dose. Inject at 2 mL/s. Dynamic acquisition starts with injection — no delay required. | — | — | — |
| 8 | `t1_vibe_dixon_sag_dyn_C` | Sagittal | Copy Slice from #7 | Penis only | **None** | Shallow breathing. Multiple measurements. Inject at start of acquisition |
| 9 | `t1_vibe_dixon_tra_short_axis_penis_C` | Axial Oblique (Short Axis) | Copy Slice from #3 | Copy Slice from #3 | **None** | Breath-hold |
| 10 | `t1_vibe_dixon_cor_long_axis_penis_C` | Coronal Oblique (Long Axis) | Copy Slice from #4 | Copy Slice from #4 | **None** | Breath-hold |
| 11 | `t1_vibe_dixon_bh_tra_pelvis_C` | Axial | Copy Slice from #1 | Copy Slice from #1. FOV 320 mm | **None** | Breath-hold |

---

## 3. Sequence Rationale

### Core Strategy

Penile MRI characterizes penile pathology where ultrasound is equivocal or insufficient for surgical planning. The three primary indications:

1. **Peyronie's disease** — plaque detection, characterization (active vs chronic), and pre-operative curvature mapping
2. **Penile cancer** — depth of invasion, corporal involvement, urethral involvement, and nodal staging
3. **Penile fracture** — tunica albuginea integrity, haematoma extent, and associated urethral injury

The protocol combines high-resolution T2 in two orthogonal penile planes with STIR for uniform fat suppression. The dynamic post-contrast acquisition (#8) is the clinical decision point — it distinguishes active inflammatory plaque (medical management) from chronic fibrotic plaque (surgical management).

All oblique sequences (#3–5, #9–10) are planned relative to the long axis of the penile shaft as seen on the sagittal T2 SPACE (#2). The penis does not lie in a fixed anatomical plane — planning must follow the shaft.

---

### Pre-Contrast

**T1 VIBE Dixon BH axial pelvis (#1):** Wide-FOV (320 mm) pelvic survey for pre-contrast nodal and bone assessment.

**T2 SPACE sagittal (#2):** 3D high-resolution T2 with isotropic resolution. The sagittal plane is the anatomical road map — it profiles the full penis (base at pubic symphysis to glans tip), the penile crura attached to the ischial rami, and the relationship to the pubic symphysis, prostate, and bladder base. From this sequence, the oblique short-axis and long-axis planes are planned along the actual penile shaft. MPR provides reformatted views in any plane without additional scan time.

**T2 TSE short axis + long axis (#3, #4):** High-resolution T2 in two orthogonal planes aligned to the penile shaft — the **primary anatomical sequences**. Normal anatomy: the paired corpora cavernosa (dorsal, separated by a thin septum) and corpus spongiosum (ventral, containing the urethra) are T2-hyperintense; the tunica albuginea is T2-dark. Buck's fascia and the dartos fascia are thin T2-dark peripheral lines.

The **short axis (#3)** provides cross-sections perpendicular to the shaft. Peyronie's plaque appears as focal T2-dark thickening or nodularity of the tunica albuginea (most commonly dorsal, 70%) — the cross-section precisely localizes plaque around the penile circumference. In cancer: depth of invasion relative to the tunica albuginea — corporal invasion replaces the normal bright cavernosal signal with T2-intermediate tumour. In fracture: disruption of the T2-dark tunica line, with the torn edge potentially retracted and associated heterogeneous haematoma.

The **long axis (#4)** profiles the full length from penile crura at the ischial rami to the glans tip, including the suspensory ligament at the penile base. This plane shows plaque craniocaudal extent, the point of maximal curvature, and the angle of deformity — all required for surgical planning (plication vs grafting vs prosthesis). In cancer: craniocaudal tumour extent relative to the glans and penile root determines the surgical margin.

**STIR TSE short axis + sagittal (#5, #6):** Short tau inversion recovery provides **uniform fat suppression immune to B0 inhomogeneity** — critical because the penis has multiple air-skin interfaces (penis-scrotum-thighs, scrotal folds) where chemical (spectral) fat saturation would fail patchily, producing bright residual fat that obscures oedema. STIR makes oedema uniformly bright against dark suppressed fat.

Perilesional oedema around a Peyronie's plaque indicates active inflammation and correlates with contrast enhancement on the dynamic series (#8). Acute fracture shows diffuse soft tissue oedema and haematoma surrounding the tunica defect. Infection (cavernositis, abscess) appears as diffuse or focal hyperintensity within the corpora or surrounding soft tissues. The **short axis (#5)** localizes oedema circumferentially; the **sagittal (#6)** tracks it along the full length of the shaft and dorsal penile fascia.

**T1 VIBE Dixon sagittal pre (#7):** Pre-contrast T1 baseline. Four Dixon contrasts (in-phase, opposed-phase, water-only, fat-only) from a single breath-hold. Detects intrinsic T1 hyperintensity: subacute haemorrhage (methaemoglobin in fracture/haematoma), proteinaceous fluid, or fat (penile lipoma, inguinal hernia fat — confirmed by opposed-phase signal dropout). Also serves as the **unenhanced mask** for subtraction images from the dynamic series (#8) — plaque enhancement is often subtle against the intermediate T1 signal of the corpora cavernosa (slow-flowing venous blood), so subtraction is essential.

---

### Post-Contrast

**T1 VIBE Dixon sagittal dynamic (#8):** Multiple consecutive sagittal VIBE acquisitions — **the decision-making sequence for Peyronie's disease**. Temporal resolution ~15–20 s per measurement captures both arterial and venous phases of penile enhancement.

Active inflammatory plaque enhances avidly (inflammatory hypervascularity) and may respond to medical management (NSAIDs, pentoxifylline, intralesional verapamil, or collagenase injections). Chronic fibrotic plaque — dense acellular collagen — does not enhance and requires surgical management (tunical plication, plaque incision/excision with grafting, or penile prosthesis). Tumour enhancement pattern and depth relative to the tunica albuginea define cancer extent; corporal invasion enhances heterogeneously. In fracture, enhancement at the tunica defect confirms the acute injury.

Subtraction images (enhanced − pre-contrast mask from #7) must be generated — without them, low-grade plaque enhancement against the background corpora is easily missed.

**T1 VIBE Dixon short axis + long axis post-contrast (#9, #10):** Small-FOV post-contrast T1 in the two penile planes — primarily for **enhancement symmetry**. The corpora cavernosa and corpus spongiosum should enhance symmetrically. Asymmetric decreased enhancement suggests arterial insufficiency, venous occlusion, segmental infarction, or low-flow priapism. The orthogonal planes also provide the surgical planning dimensions (graft length, plication site relative to the glans, neurovascular bundle relationship).

**T1 VIBE Dixon axial pelvis post-contrast (#11):** Wide-FOV (320 mm) post-contrast pelvic survey. Enhancing pelvic lymph nodes (inguinal → external iliac → obturator) and bone metastases. This is the nodal staging sequence — penile cancer disseminates to inguinal nodes first, then pelvic nodes.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Positioning** — Penis straight and secured? Long axis consistent? | If the penis is curved or draped over the scrotum, the short-axis plane samples the shaft obliquely at different points along its length — cross-sectional anatomy is unreliable, and plaque thickness is overestimated. Re-position with gentle tape to the anterior abdominal wall. |
| **Oblique planning** — Short-axis truly perpendicular to the penile shaft on sagittal? Long-axis truly parallel? | Plan from the T2 SPACE sagittal (#2). The penile shaft is a visible landmark — the short-axis plane must be perpendicular to the dorsal surface of the shaft at the midpoint. Re-check on the long-axis view. |
| **Dynamic timing** — Enough temporal resolution for plaque enhancement assessment? | If the dynamic series (#8) is too slow (>30 s per measurement), the arterial phase is missed and plaque enhancement may not be captured. The corpora cavernosa fill slowly (venous inflow) — moderate temporal resolution (~15–20 s per measurement) is adequate. |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-07 | — | Initial — 11 sequences. T2 short and long axis + STIR in two planes. Dynamic sagittal post-contrast for plaque activity. Wide-FOV pelvic survey pre/post. |
