# X-knife SRS (Stereotactic Radiosurgery Planning)

**Version:** 1.0 | **Date:** 2026-07-22 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. If the SRS frame or mask is used, confirm compatibility with the head coil before positioning.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Branch A: Tumor (Metastasis, Glioma, Schwannoma, Meningioma)

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_fl2d_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t2_space_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **None** |
| — | **Contrast** | — | — | — | — |
| 3 | `t1_fl3d_sag_x-knife_C` | Sagittal | ∥ midline | Whole brain | **None** |
| 4 | `MPR planning` | Cor+Ax | — | Whole brain | — |
| 5 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |

### Branch B: AVM (Arteriovenous Malformation)

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_fl2d_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t2_space_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **None** |
| — | **Contrast** | — | — | — | — |
| 3 | `TOF_3D_multi-slab_x-knife_C` | Axial | ∥ AC-PC line | Entire AVM nidus | **Superior** (venous flow) |
| 4 | `t1_fl3d_sag_x-knife_C` | Sagittal | ∥ midline | Whole brain | **None** |
| 5 | `MPR planning` | Cor+Ax | — | Whole brain | — |

*#3 (both branches): The FLASH 3D sagittal dataset is exported directly to the x-knife radiosurgery planning system. MPR (#4/5) provides coronal and axial reformatted views. No fat sat — geometric accuracy is essential for radiation targeting.*

---

## 3. Sequence Rationale

### Core Strategy

Stereotactic radiosurgery delivers high-dose radiation to a precisely defined target with sub-millimetre accuracy. Every sequence choice is driven by geometric fidelity — the 3D dataset loaded into the treatment planning system must be distortion-free. The same principles as neuronavigation apply (see `brain+viewing_wand.md`), but the target for SRS is often smaller (single metastasis, AVM nidus) and the accuracy requirement is even higher.

**`t1_fl2d_tra` (#1 — both branches)**
Pre-contrast T1 baseline. Matched to post-contrast for enhancement comparison and subtraction. FLASH 2D provides clean T1 contrast. No sat band: short TR has no slack.

**`t2_space_tra` (#2 — both branches)**
3D T2 SPACE axial, isotropic resolution. Replaces standard 2D TSE and FLAIR — SPACE provides isotropic voxels that can be reformatted in any plane for treatment planning. CSF is bright, pathology is defined against it. For tumors: the T2 SPACE shows peritumoural oedema, cystic components, and defines the brain-tumour interface. For AVM: shows flow voids of the nidus, haemosiderin from prior haemorrhage, and brain parenchyma integrity. Isotropic resolution allows the dosimetrist to reformat the T2 dataset in the same planes as the T1 3D dataset for co-registration.

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before the 3D dataset (#3).

**`t1_fl3d_sag_x-knife_C` (#3 Tumor / #4 AVM)**
3D T1 FLASH sagittal — the x-knife treatment planning dataset. FLASH 3D (spoiled GRE) is chosen for the same reasons as viewing wand: minimal geometric distortion, no fat sat (frequency shifts at fat-water boundaries cause spatial errors), consistent T1 contrast across the brain. Sagittal source optimises coronal and axial reformats with phase-encode in A/P direction away from the brain centre. This dataset is exported directly to the x-knife system for target delineation, dose calculation, and beam trajectory planning. Enhancing tumour margin = treatment target.

**`TOF_3D_multi-slab_x-knife_C` (#3 AVM only)**
Post-contrast TOF MRA. The AVM nidus is the radiosurgery target — TOF defines its vascular anatomy (feeding arteries, nidus size and shape, draining veins) in 3D. Post-contrast TOF is used instead of pre-contrast because gadolinium enhances the nidus and slow-flow components. Coverage: the entire AVM nidus must be inside the slab — this overrides standard TOF anatomical landmarks. If the nidus extends beyond the standard coverage, extend the slab.

**`MPR planning` (#4 Tumor / #5 AVM)**
Multiplanar reconstruction from the FLASH 3D dataset. Coronal and axial reformatted views for treatment planning review.

**`t1_fl2d_tra_C` (#5 Tumor only)**
Post-contrast 2D FLASH axial. Matches pre-contrast (#1) for subtraction — confirms enhancement in the conventional axial plane alongside the 3D sagittal dataset. The AVM branch omits this because enhancement is not the diagnostic question for an AVM. The TOF defines the vascular target; the FLASH 3D defines the brain parenchyma. A separate post-contrast axial FLASH adds nothing to AVM treatment planning.

---

## 4. How This Differs from Standard Brain Protocols

- **No FLAIR:** T2 SPACE provides the anatomical detail for treatment planning. FLAIR's diagnostic value (lesion detection) is secondary — the target is already known.

- **No DWI:** Treatment planning does not require diffusion. The target is a known, established lesion.

- **FLASH 3D sagittal without fat sat:** Same geometric accuracy principle as viewing wand. FLASH 3D is the gold standard for stereotactic treatment planning. No fat sat (spatial shift at tissue boundaries), sagittal source (phase-encode A/P, distortion away from brain centre), consistent T1 contrast (no B1 inhomogeneity like MPRAGE).

- **T2 SPACE instead of 2D TSE:** Isotropic 3D dataset — the dosimetrist can reformat in any plane for dose calculation and beam trajectory planning. This replaces both the axial T2 and FLAIR.

- **AVM branch adds TOF:** The nidus is a vascular target — TOF defines the arterial and venous anatomy for radiosurgery planning. Post-contrast only (contrast enhances nidus definition).

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — entire head contour included on the 3D (#3/#4)? Nose not clipped anteriorly? | Same as viewing wand — the x-knife system needs the full head surface for registration. Extend FOV or partitions if clipped |
| **`t1_fl3d_sag` (#3/#4)** — isotropic? | Do NOT change slice thickness, matrix, or FOV from protocol defaults. Any change that breaks isotropy degrades dose calculation accuracy and reformat quality |
| **AVM: TOF (#3)** — nidus fully inside the slab? | Confirm the entire AVM is covered. If the nidus extends beyond standard TOF coverage, extend the slab |
| **MPR (#4/#5)** — axial reformat ordered bottom-to-top? | Standard radiological display is top-to-bottom. The x-knife planning system expects images from inferior to superior — the dose calculation grid starts at the most inferior slice and builds upward to match the beam's-eye-view from the vertex. If the stack is reversed, the dose grid is inverted. Confirm the reformat direction |
| **Post-contrast** — contrast present? Confirm tumour or nidus enhancement | If absent: check IV line, confirm injection. The enhancing target margin defines the treatment volume |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-22 | — | Initial — 2 branches (Tumor: 5 sequences; AVM: 5 sequences) |
