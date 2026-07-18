# Plain Brain (Non-Contrast Brain MRI)

**Version:** 1.0 | **Date:** 2026-07-18 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_mprage_cor` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 3 | `MPR reformat` | Sag+Ax | — | Whole brain | — |
| 4 | `t2_tse_flair_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 5 | `resolve_diffusion_tra` | Axial | Copy Slice from #1 | — | **None** |

---

## 3. Sequence Rationale

**`t2_tse_tra` (#1)**
Core anatomical sequence. T2 contrast is sensitive to edema, gliosis, infarction, and white matter disease. High in-plane resolution with good gray/white differentiation.
*Plane:* **Axial** is the standard screening plane — best visualisation of the ventricular system, basal ganglia, internal capsule, and cortical sulcal pattern. Most pathology (edema, infarcts, MS plaques) is assessed relative to these axial landmarks.

**`t1_mprage_cor` (#2)**
3D high-resolution T1-weighted gradient echo. Excellent gray/white matter contrast. Structural/anatomical reference. Source data for MPR reformats (#3).
*Plane:* **Coronal** 3D acquisition maximises reformat quality in sagittal and axial planes (phase-encode S/I → clean reformats in the other two planes). Coronal source reduces wraparound artefact vs sagittal 3D. Native coronals valuable for hippocampal, sellar, and vertex assessment.

**`MPR reformat` (#3)**
Multiplanar reconstruction from the MPRAGE (#2). Generates sagittal and axial anatomical views without additional scan time.
*Plane:* **Sagittal** — midline structures (corpus callosum, brainstem, vermis). **Axial** — conventional axial T1 reference. Both reformatted from 3D coronal source.

**`t2_tse_flair_tra` (#4)**
T2-weighted with CSF nulling. Suppresses ventricular/sulcal CSF, making periventricular and cortical/subcortical lesions conspicuous. Essential for MS, small vessel ischaemia, encephalitis.
*Plane:* **Axial** — matches the T2 axial plane (#1) so periventricular lesion burden can be directly compared. Periventricular white matter and cortex best profiled in axial plane.

**`resolve_diffusion_tra` (#5)**
Diffusion-weighted imaging via readout-segmented EPI (RESOLVE). Detects restricted diffusion: acute ischaemia (within minutes), abscess vs necrosis, highly cellular tumours (lymphoma, high-grade glioma). Less distortion vs single-shot EPI.
*Plane:* **Axial** — standard DWI plane. Symmetrical hemisphere comparison. Minimises through-plane distortion at skull base where susceptibility is worst. Matches T2/FLAIR for side-by-side lesion correlation.

---

## 4. Pathology-Based Variations

- **SWI:** Add when screening for microbleeds (CAA, hypertension), trauma (diffuse axonal injury), cavernomas, haemorrhagic tumours/metastases, or calcified lesions. Also useful for venous anatomy visualisation.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack if any sequence is short |
| **MPRAGE** — motion/ghosting? | Re-acquire. |
| **RESOLVE DWI** — true restriction vs T2 shine-through on ADC? | Document true restriction. If distorted at skull base: flip phase-encode (A>>P → P>>A) and repeat. |
| **RESOLVE DWI** — SNR adequate, water peak centred and narrow? | Re-shim if water peak is broad or shifted — fat suppression and EPI distortion depend on good shim

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 5 sequences |
