# MS (Multiple Sclerosis Protocol with Contrast)

**Version:** 1.0 | **Date:** 2026-07-19 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `dir_space_sag_iso` | Sagittal | ∥ midline | Whole brain | **None** |
| 4 | `MPR` | Cor+Ax | — | Whole brain | — |
| 5 | `t2_stir_tra_3mm_orbit` | Axial | ∥ optic nerves | Superior orbital rim → inferior orbital rim | **None** |
| 6 | `t2_tse_fs_cor_3mm_orbits` | Coronal | ⟂ hard palate | Anterior globe → orbital apex | **None** |
| — | **Contrast** | — | — | — | — |
| 7 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| 8 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 9 | `MPR` | Sag+Ax | — | Whole brain | — |
| 10 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |

*#4 is reformatted from DIR SPACE (#3). #9 is reformatted from VIBE (#8).*

---

## 3. Sequence Rationale

### Core Strategy

MS diagnosis requires two MRI findings (McDonald criteria): lesions in multiple characteristic locations (dissemination in space) and proof that lesions occurred at different times (dissemination in time). In a single scan, dissemination in space comes from DIR, T2, and orbit sequences showing lesions in periventricular, cortical, infratentorial, and optic nerve locations. Dissemination in time comes from seeing both enhancing (active) and non-enhancing (chronic) plaques on post-contrast T1 — proof that not all lesions appeared at once. DIR SPACE replaces FLAIR as the primary lesion-detection sequence. Orbit sequences screen for optic neuritis, the most common MS presentation outside the brain.

**`t2_tse_tra` (#1)**
Core axial T2 anatomy. Reference plane. T2 shows infratentorial and spinal cord lesions (part of McDonald criteria) and provides anatomical context.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. Matched to post-contrast (#10) for enhancement comparison and subtraction. Chronic MS plaques appear as T1 hypointensities (black holes).

**`dir_space_sag_iso` (#3)**
DIR (Double Inversion Recovery) SPACE, sagittal isotropic. DIR uses two inversion pulses: one nulls CSF, the other nulls normal white matter. Only lesions remain bright — grey matter, CSF, and normal white matter are all suppressed. Cortical and juxtacortical MS plaques are invisible on standard T2/FLAIR because the bright cortex and bright CSF border the lesion on both sides. DIR solves this by suppressing both, making cortical lesions detectable for the first time.

*Plane:* Sagittal source because the corpus callosum and periventricular white matter — hallmark MS locations — are best profiled in the sagittal plane, capturing the entire callosum from rostrum to splenium and the periventricular interface in one view. Coronal and axial reformats (#4) give the other planes without additional scan time.

**`MPR` (#4)**
Multiplanar reconstruction from DIR SPACE (#3). Coronal and axial reformatted DIR images — no additional acquisition time. Coronal DIR is the best plane for callosal and periventricular lesion assessment.

**`t2_stir_tra_3mm_orbit` (#5)**
T2 STIR axial 3 mm orbits. MS plaques can involve the optic nerve directly — optic neuritis is an MS lesion in the nerve, not a separate disease. The intraorbital segment (behind the globe, retrobulbar) is the most common location. STIR suppresses orbital fat: an acute MS plaque appears as a bright, swollen segment of the nerve. Axial profiles the nerve in its long axis.

**`t2_tse_fs_cor_3mm_orbits` (#6)**
T2 TSE fat-saturated coronal 3 mm orbits. Cross-sectional view of both optic nerves — symmetric comparison of nerve diameter. An acute plaque shows focal thickening on coronal. Chronic resolved plaques leave optic nerve atrophy (a thin nerve) indicating prior axonal loss. TSE avoids susceptibility artefact near the ethmoid air cells.

**Contrast**
Standard dose IV gadolinium. Target ≥5 min delay before post-contrast T1. DWI (#7) fills the delay. Enhancing lesions indicate active demyelination (dissemination in time). Simultaneous enhancing and non-enhancing lesions on the same scan meet McDonald criteria.

**`resolve_3scan_trace_tra_p2` (#7)**
RESOLVE DWI. Fills the post-contrast delay. Distinguishes acute demyelination (facilitated diffusion, ADC bright) from acute ischaemia (restricted diffusion, ADC dark). Less distortion at skull base vs single-shot EPI.

**`t1_vibe_fs_cor_C` (#8)**
3D T1 post-contrast coronal with fat saturation. Enhancing MS plaques — nodular, ring-like, or incomplete ring (open-ring sign, pathognomonic). Coronal is the money plane for periventricular and callosal enhancement.

**`MPR` (#9)**
Multiplanar reconstruction from post-contrast VIBE (#8). Sagittal and axial reformatted views.

**`t1_fl2d_tra_C` (#10)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map. Compare to pre-contrast T1 for new T1 hypointensities (black holes = chronic axonal loss).

---

## 4. Why No Dedicated T1 Orbits?

Pre- and post-contrast T1 orbit sequences are deliberately omitted. The STIR (#5) and T2 FS coronal (#6) screen for MS plaques in the optic nerve — an acute plaque appears as a bright, swollen nerve segment on STIR; a chronic resolved plaque leaves atrophy. If these are negative, no dedicated T1 is needed. If STIR flags an acute plaque, the brain post-contrast VIBE (#8) provides partial enhancement assessment of the orbital apex and proximal optic nerves. A dedicated post-contrast T1 FS orbit can be added ad hoc when STIR is positive, but is not routine.

---

## 5. Pathology-Based Variations

- **Whole spine screening:** Indicated when spinal cord symptoms are present (myelopathy, transverse myelitis), or when brain MRI is equivocal for dissemination in space — spinal cord lesions count as infratentorial under McDonald criteria. Add C-spine and T-spine sequences (see future spine protocol files).
  - *Coverage:* Foramen magnum → conus medullaris (L1–L2). Must be contiguous from foramen magnum downward — no gap between brain and C-spine. Below the conus is cauda equina, which MS does not typically involve.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? Orbital apex included on post-contrast VIBE (#8)? | Adjust slice stack. VIBE must cover the orbital apex — if STIR flags an acute plaque, VIBE provides the enhancement fallback |
| **DIR (#3)** — grey-white and CSF suppression uniform? | TI1 (CSF null) ~2800 ms at 1.5T, ~2200 ms at 3T. TI2 (WM null) ~400 ms at 1.5T, ~450 ms at 3T. If white matter not dark enough: adjust TI2. If CSF not dark enough: adjust TI1 |
| **Post-contrast** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection. ≥5 min delay needed for MS plaque enhancement |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 10 sequences |
