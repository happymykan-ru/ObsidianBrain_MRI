# Epilepsy (Seizure Protocol with Contrast)

**Version:** 1.0 | **Date:** 2026-07-19 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** 32-channel head coil. Temporal lobe SNR at the periphery is critical for hippocampal assessment (#6). The 32-channel coil supports the higher acceleration factors (p2, p3) and compensates for the MP2RAGE dual-acquisition SNR penalty.
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_p3` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dark_fluid_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `t1_mp2rage_cor` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| — | *Manual reformat* | Sag+Ax | ∥ + ⟂ AC-PC line (3 mm) | Whole brain | — |
| 5 | `t2_swi3d_tra_p2` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **None** |
| 6 | `t2_tse_cor_oblique_448_2mm_epilepsy` | Cor Obl | ⟂ hippocampal long axis | Temporal pole → splenium (~40–50 mm), both temporal lobes | **None** |
| 7 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 8 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 9 | `MPR` | Sag+Ax | — | Whole brain | — |
| 10 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |

---

## 3. Sequence Rationale

### Core Strategy

Epilepsy imaging has two goals: detect epileptogenic lesions (hippocampal sclerosis, cortical dysplasia, cavernomas, tumours) and provide anatomical detail for surgical planning. The protocol combines whole-brain screening with targeted high-resolution hippocampal sequences.

**`t2_tse_tra_p3` (#1)**
T2 TSE axial with GRAPPA ×3. Core axial anatomy. p3 shortens the echo train — faster acquisition and reduced motion sensitivity. Reference plane.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. FLASH 2D — matched geometry to post-contrast (#10) for enhancement comparison and subtraction.

**`t2_tse_dark_fluid_tra` (#3)**
CSF-suppressed T2 FLAIR axial. Essential in epilepsy: cortical dysplasia, focal cortical thickening, transmantle sign, tubers, and hippocampal sclerosis all appear as FLAIR hyperintensities. FLAIR is the primary detection sequence for non-vascular epileptogenic lesions.

**`t1_mp2rage_cor` (#4)**
MP2RAGE acquires two GRE readouts at different inversion times, then calculates a uniform T1 image (UNI) from them. Standard MPRAGE has B1 inhomogeneity — T1 contrast varies across the brain, especially at 3T, and subtle cortical dysplasia or grey-white junction blurring can be masked where the field is uneven. MP2RAGE corrects this: UNI has uniform T1 contrast everywhere. The two source images (INV1, INV2) also enable quantitative T1 mapping for hippocampal sclerosis.

*PACS:* INV2 + UNI → ePR. INV1 + INV2 + UNI → archive.
*Reformat:* MP2RAGE does not have Siemens inline MPR. Manually create sagittal and axial parallel slices (3 mm) from the coronal source.

**`t2_swi3d_tra_p2` (#5)**
SWI 3D with GRAPPA ×2. Cavernomas, microbleeds, calcifications, and small vessel disease are common epileptogenic substrates. SWI detects these with far higher sensitivity than T2* GRE — the phase mask amplifies susceptibility contrast. Essential for pre-surgical planning to identify all potentially epileptogenic lesions.

**`t2_tse_cor_oblique_448_2mm_epilepsy` (#6)** — Hippocampal Sequence
T2 TSE coronal oblique, 448 matrix, 2 mm slices gives high in-plane and through-plane resolution. The diagnostic sequence for mesial temporal sclerosis.

*Plane & Coverage:* The hippocampus curves anteriorly and medially — standard coronal is not a true cross-section. On sagittal scout: the hippocampal long axis runs temporal pole → splenium. This line defines both the prescription (perpendicular to it) and the slab boundaries (~40–50 mm). Temporal pole = sharp border on temporal sagittal; splenium = bright T1 on midline.

**`resolve_3scan_trace_tra_p2` (#7)**
RESOLVE DWI with GRAPPA ×2. Acute ischaemia (stroke presenting as seizure), abscess, cellular tumours. Less distortion at skull base vs single-shot EPI.

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before post-contrast T1 (#8–#10).

**`t1_vibe_fs_cor_C` (#8)**
3D T1 post-contrast coronal with fat saturation. Whole-brain enhancement screening — tumours, inflammatory lesions, meningeal enhancement. Source data for MPR (#9).

**`MPR` (#9)**
Multiplanar reconstruction from post-contrast VIBE (#8). Sagittal and axial reformatted views.

**`t1_fl2d_tra_C` (#10)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map.

---

## 4. Epileptogenic Lesion Mapping

Each sequence in this protocol targets a different epileptogenic substrate. Here is what each lesion looks like and where you'll find it:

- **Hippocampal sclerosis** is seen on the coronal oblique T2 (#6) as volume loss, T2 hyperintensity, and loss of the normal internal laminar architecture. The MP2RAGE T1 map (#4) confirms it with quantitative T1 prolongation. FLAIR (#3) shows the associated signal change but is less specific than the dedicated hippocampal sequence.

- **Focal cortical dysplasia** lights up on FLAIR (#3) as a transmantle hyperintensity — a bright line stretching from the ventricle to the cortex. The MP2RAGE (#4) shows the blurring of the grey-white junction that defines it, with uniform contrast that eliminates B1 artefact which can mimic this finding on standard MPRAGE.

- **Cavernomas** have a characteristic popcorn appearance with a complete haemosiderin ring on SWI (#5). SWI is far more sensitive than T2* GRE for detecting small cavernomas and microbleeds.

- **Tumours** like DNET and ganglioglioma appear as well-circumscribed, cortical-based lesions on FLAIR (#3). Some enhance on post-contrast T1 (#8, #10); many do not.

- **Post-traumatic epilepsy** is driven by microbleeds and haemosiderin deposition, best seen on SWI (#5).

- **When the MRI is reported as normal**, review the coronal oblique T2 (#6) for subtle hippocampal volume asymmetry. The MP2RAGE T1 map (#4) can reveal quantitative T1 changes not visible to the eye on routine images.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? Temporal lobes fully included on coronal oblique? | Adjust slice stack |
| **Coronal oblique (#6)** — true perpendicular to hippocampal axis? | Check the images: CA1–4 laminar architecture should be crisp (not smeared), both hippocampi symmetric at each level, temporal horn = thin dark slit above hippocampus (not round). If off: represcribe |
| **Post-contrast** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 10 sequences |
