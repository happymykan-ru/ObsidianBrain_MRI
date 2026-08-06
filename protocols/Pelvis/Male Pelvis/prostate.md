# Prostate (Multiparametric Prostate MRI with Dynamic Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the symphysis pubis.
- **Immobilization:** Pelvic binder over the pelvic region — reduces respiratory motion transmitted to the pelvis and minimizes anterior abdominal wall movement.
- **Laser Landmark:** Symphysis pubis
- **Verbal Instructions:** Shallow breathing during the dynamic contrast acquisition — breath-hold is not required but the patient must not move. Deep breathing causes pelvic floor motion that degrades the DCE.
- **Buscopan (Hyoscine butylbromide):** 10–20 mg IV, prior to the exam. Onset ~1 min, peak effect ~1–2 min. Paralyses rectal smooth muscle — the prostate sits directly against the rectum; rectal peristalsis displaces the gland and degrades DCE. Contraindications: glaucoma, urinary retention (BPH with obstruction), myasthenia gravis, tachyarrhythmia.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Buscopan** | — | 10–20 mg IV, prior to exam | — | — | — |
| 1 | `t2_spc_sag` | Sagittal | True sagittal | Prostate + seminal vesicles + bladder base. | **None** | Free breathing |
| 2 | `t2_tse_tra` | Axial Oblique | ⟂ posterior prostate wall | Prostate + seminal vesicles. Base → apex | **None** | Free breathing |
| 3 | `t2_tse_cor` | Coronal Oblique | ∥ posterior prostate wall | Prostate + seminal vesicles + pelvic floor. A/P: pubic symphysis → rectum | **None** | Free breathing |
| 4 | `t1_vibe_dixon_tra_bh_320` | Axial Oblique | Copy Slice from #2 | Prostate + pelvic nodes. FOV 320 mm | **None** | Breath-hold |
| 5 | `resolve_diff_b50_500_tra_prostate` | Axial Oblique | Copy Slice from #2 | Prostate only | **A/P** (anterior + posterior skin margins) | Free breathing |
| 6 | `resolve_diff_b1500_tra_prostate` | Axial Oblique | Copy Slice and Sat from #5 | — | — | Free breathing |

### Dynamic Contrast (DCE)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 7 | `t1_vibe_tra_dyn` | Axial Oblique | Copy Slice from #2 | Prostate only | **None** | Shallow breathing. Multiple measurements. Inject contrast after 2 baseline measurements |
| 8 | `t1_vibe_fs_tra_bh_320_C` | Axial Oblique | Copy Slice from #2 | Prostate + pelvic nodes. FOV 320 mm | **None** | Breath-hold |

---

## 3. Sequence Rationale

### Core Strategy

Multiparametric prostate MRI (mpMRI) combines T2 anatomy, DWI, and DCE for PI-RADS lesion detection, localization, and risk stratification. The clinical question: is there a clinically significant prostate cancer (Gleason ≥3+4), where is it, and is there extracapsular extension or seminal vesicle invasion? The three parameters are scored independently on PI-RADS and combined for an overall assessment category.

All axial and coronal sequences are oblique — aligned perpendicular and parallel to the posterior prostate wall. The prostate sits obliquely in the pelvis, tilted posteriorly. True axial slices cut obliquely through the gland and distort the zonal anatomy; oblique planes aligned to the prostate give true cross-sections for accurate capsule and zonal assessment.

---

### Pre-Contrast

**T2 SPACE sagittal (#1):** 3D high-resolution T2. The sagittal plane profiles the prostate, bladder base, seminal vesicles, and rectum in one view. MPR provides reformatted axial and coronal views. SPACE gives isotropic resolution — the reformats are near-diagnostic quality. The sagittal is the first sequence because it shows the prostate tilt — from this, the oblique axial and coronal planes are planned.

**T2 TSE axial oblique (#2):** The **primary PI-RADS sequence** for the peripheral zone. Perpendicular to the posterior prostate wall. Normal peripheral zone is T2-hyperintense (glandular tissue). Cancer is T2-dark — a discrete hypointense nodule in the bright peripheral zone is the hallmark T2 finding. The transition zone is assessed on T2 for the "erased charcoal" sign (homogeneous dark signal replacing the normal heterogeneous BPH nodularity). Capsular margin, neurovascular bundles, and the rectoprostatic angle are assessed for extracapsular extension.

**T2 TSE coronal oblique (#3):** Parallel to the posterior prostate wall. Profiles the seminal vesicles (T2-bright, thin-walled) — seminal vesicle invasion appears as T2-dark tumour extending from the base into the vesicle. Also assesses the pelvic sidewall, levator ani, and obturator internus for T4 disease.

**T1 VIBE Dixon (#4):** FOV 320 for pelvic nodal survey and bone assessment. Post-biopsy haemorrhage appears T1-hyperintense (blood products) — important because haemorrhage can mimic T2-dark cancer in the peripheral zone. If the prostate is diffusely T1-bright from recent biopsy, the exam should be deferred (6–8 weeks post-biopsy). In/opposed phase for bone metastases.

---

### DWI

**RESOLVE DWI b=50, 500 (#5):** Readout-segmented EPI — reduced distortion at the rectum-prostate air-tissue interface compared to single-shot EPI. b=50 is the low-b reference (suppresses vascular signal). b=500 is the standard diffusion weighting for ADC calculation. Restricted diffusion = high signal at b=500, dark on ADC. The ADC map is the primary PI-RADS DWI parameter.

- **Peripheral zone cancer:** Restricted diffusion — bright at b=500, very dark on ADC. The most reliable PI-RADS finding.
- **Benign prostate tissue:** Facilitated diffusion — dark at b=500, bright on ADC.

**RESOLVE DWI b=1500 (#6):** High b-value. At b=1500, benign prostate tissue signal is nearly fully suppressed — the gland appears dark. Prostate cancer, being highly cellular, retains signal — tumours stand out as bright foci against the dark background. This is a visual conspicuity sequence, not used for ADC calculation. PI-RADS recommends b ≥1400 for high-b-value imaging.

---

### Dynamic Contrast (DCE)

**T1 VIBE dynamic (#7):** Multiple consecutive VIBE acquisitions over several minutes. The first two measurements are the pre-contrast baseline — contrast is injected after the 2nd measurement completes. Temporal resolution must be <10 s per measurement to adequately sample the enhancement curve. The prostate enhances from the peripheral zone inward; cancer typically shows early arterial enhancement with rapid wash-in (type 3 curve). DCE is used for PI-RADS categorization of a peripheral zone lesion: a lesion already scored 4 on DWI is not upgraded by DCE; a lesion scored 2–3 on DWI may be upgraded to 3 or 4 if DCE is positive (focal early enhancement).

DCE criteria: focal enhancement earlier or greater than the surrounding prostate tissue, with a type 3 (wash-in/wash-out) or type 2 (plateau) curve. Benign prostate tissue enhances more slowly and diffusely.

**Post-contrast T1 FS (#8):** FOV 320 nodal survey. Enhancing pelvic nodes and bone metastases. The prostate itself is not the target of this sequence — it is for staging.

---

## 4. Post-Processing

- **Perfusion Map:** Retrospectively generate from the DCE series (#7) using the MR Prostate Workflow in SyngoVia. The DCE measurements are analysed with a pharmacokinetic model to produce quantitative perfusion maps (Ktrans, Kep, Ve). Areas of high permeability correspond to tumour angiogenesis.
- **Fusion Images:** Produce 1 mm axial reformat T2 + perfusion map fusion images. The 1 mm reformats are reconstructed from the T2 SPACE (#1) and fused with the perfusion map for PI-RADS reporting.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Oblique planes** — Angulation <45° from true axial/coronal? | If the oblique angle exceeds 45°, the plane direction is swapped (Siemens inverts the phase/slice axes). The image may appear correct but the prostate orientation is altered and zonal anatomy is unreliable. Plan obliques from the sagittal SPACE (#1) and confirm the angulation remains under 45° |
| **DWI quality** — Fat suppressed on b=50 images? ADC map diagnostic? | If fat is bright on b=50: the water peak was mis-selected during prescan — the fat sat pulse is tuned to the wrong frequency. Re-shim and re-acquire. |
| **DCE data** — Perfusion map sent to PACS? | Only the perfusion map is sent — the raw DCE source images are not archived. Confirm the SyngoVia post-processing is complete and the perfusion map is in the series before ending the exam |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 8 sequences. Oblique axial/coronal per prostate wall. DWI b=50/500/1500. DCE with 2 baseline measurements. T2 SPACE sagittal 3D |
