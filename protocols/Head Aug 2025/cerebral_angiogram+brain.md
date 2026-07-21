# Cerebral Angiogram + Brain (Brain MRI with TOF MRA ± Contrast)

**Version:** 1.0 | **Date:** 2026-07-18 | **Scanner:** [Confirm 1.5T/3T]

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
| 3 | `t2_tse_dark_fluid_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `TOF_3D_multi-slab` | Axial | ∥ AC-PC line | Carotid siphon → above corpus callosum | **Superior** (venous flow) |
| 5 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| 6 | `t1_fl2d_sag` | Sagittal | ∥ midline | [Confirm coverage] | **None** |
| — | **Contrast** | — | — | — | — |
| 7 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 8 | `MPR` | Sag+Ax | — | Whole brain | — |
| 9 | `t1_fl2d_C` | Axial | Copy Slice from #1 | — | **None** |

*#6 is for plain brain only — omit if contrast is given.*

---

## 3. Sequence Rationale

**`t2_tse_tra` (#1)**
Core axial T2 anatomy. Edema, gliosis, infarction, white matter disease. Reference plane for the protocol.

**`t1_fl2d_tra` (#2)**
Pre-contrast 2D FLASH axial. Baseline T1 reference. FLASH 2D is used instead of MPRAGE by design — this protocol doubles as both plain and contrast brain (see Section 4). No sat band: short TR has no slack.

**`t2_tse_dark_fluid_tra` (#3)**
CSF-suppressed T2 FLAIR. Periventricular and cortical/subcortical lesion detection.

**`TOF_3D_multi-slab` (#4)**
3D time-of-flight MR angiography, multi-slab acquisition. Sequential thin slabs are acquired perpendicular to arterial flow to maximise inflow enhancement. Shows the circle of Willis and major intracranial arteries without contrast. Sat band placed **superior** to suppress venous flow signal. If the lesion or vessel of interest is not fully covered, increase slices per slab or switch to an EC/IC bypass TOF with larger coverage. For detailed TOF slab strategy, see `cerebral_angiogram(no_brain_request).md`.

**`resolve_3scan_trace_tra_p2` (#5)**
RESOLVE DWI. DWI + TOF (#4) answer the core stroke question: infarcted core (DWI bright, ADC dark) = dead tissue. Small DWI lesion + large vessel occlusion on TOF = tissue at risk (penumbra), still salvageable. DWI matching full territory = completed infarct. See `cerebral_angiogram(no_brain_request).md` for full explanation.

**`t1_fl2d_sag` (#6) — Plain brain only**
Pre-contrast 2D FLASH sagittal. Fills the midline anatomical gap left by not having an MPRAGE/MPR — corpus callosum, brainstem, vermis, craniocervical junction. Omitted when contrast is given because post-contrast VIBE (#7) and MPR (#8) provide the sagittal view.

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before post-contrast T1 sequences (#7–#9).

**`t1_vibe_fs_cor_C` (#7)**
3D T1 post-contrast coronal with fat saturation. Coronal is the money plane for skull base, sellar, and meningeal enhancement. Fat sat makes enhancement conspicuous against bright fat. 3D source provides reformats for the MPR (#8).

**`MPR` (#8)**
Multiplanar reconstruction from post-contrast VIBE (#7). Sagittal and axial reformatted views without additional acquisition.

**`t1_fl2d_C` (#9)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast baseline (#2) — subtract for pure enhancement map. Combined with VIBE FS coronal (#7) and MPR (#8), gives three-plane post-contrast T1 assessment.

---

## 4. Why FLASH 2D Instead of MPRAGE Pre-Contrast?

A plain brain + MRA could simply take `plain_brain` (t1_mprage_cor + MPR) and add TOF. This protocol deliberately does not. Three reasons:

**1. This protocol doubles as both plain and contrast brain.** The pre-contrast block is designed so that if the radiologist decides to give contrast mid-scan, no sequences need to be repeated. FLASH 2D tra (#2) is the same pre-contrast baseline used in `contrast_brain` — its geometry matches the post-contrast FLASH (#9) for enhancement comparison. If you'd run MPRAGE instead and then decided to inject, you'd have no pre-contrast FLASH to compare against the post-contrast dataset. You'd either have to re-run the pre-contrast T1 as FLASH (wasting time) or compare MPRAGE to VIBE (different sequence, different contrast weighting — unreliable comparison).

**2. TOF already provides a 3D dataset.** TOF multi-slab is a high-resolution 3D GRE that takes several minutes. Adding MPRAGE means acquiring a second large 3D GRE volume. FLASH 2D is faster and provides genuinely different tissue contrast — short TR, spoiled GRE, 2D slice-by-slice — without duplicating the 3D GRE workload. The TOF covers the vascular anatomy; FLASH covers the parenchymal T1 anatomy. Different jobs, different sequences.

**3. The sagittal FLASH fills the gap MPR would have covered.** In `plain_brain`, MPRAGE is the coronal source → MPR gives sagittal + axial reformats. Here, without MPRAGE, `t1_fl2d_sag` (#6) provides the midline anatomical view (corpus callosum, brainstem, vermis, craniocervical junction) that would otherwise be missing. It's a fast substitute for the sagittal reformat — acquired only in the plain version because the contrast version gets sagittal from the post-contrast MPR (#8).

---

## 5. Pathology-Based Variations

- **Post-coiling:** Add `TOF_fl3d_tra_C` — post-contrast TOF with high bandwidth. Coil mass causes severe susceptibility dropout on standard TOF. High bandwidth shortens the readout, reducing dephasing across the susceptibility gradient. Post-contrast shortens blood T1, compensating for inflow saturation near the coil.
- **Dissection:** Add `t1_tse_fs_tra` through the neck — see `cerebral_angiogram(no_brain_request).md` for full acquisition details
- **AVM / dural fistula:** Add `TWIST_HEAD_ePAT2×3` — see `cerebral_angiogram(no_brain_request).md` for full acquisition details. TWIST is only needed for high-flow arteriovenous shunting. Venous malformations (DVAs) do not benefit — low-flow, no arterial component, standard post-contrast T1 shows the anatomy.
- **Venous sinus thrombosis:** Consider adding `TWIST_HEAD_ePAT2×3` to assess venous flow dynamics (see `cerebral_angiogram(no_brain_request).md`). Coronal source if targeting transverse sinus.
- **Plain brain + MRA only (no contrast):** #6 (`t1_fl2d_sag`) is mandatory; #7–#9 are omitted

---

## 6. Alerts

| Check | Improve |
|---|---|
| **TOF Lesion Coverage** — lesion/vessel of interest fully covered? | If not: increase slices/slab or switch to EC/IC bypass TOF with larger coverage |
| **TOF Anatomical Coverage** — coverage adequate? Carotid siphon through pericallosal ACA? | Reposition if siphon cut inferiorly or distal ACA missing superiorly |
| **TOF** — venous contamination? (sigmoid/transverse sinus bright) | Confirm superior sat band is placed. If venous signal persists, extend or reposition sat band |
| **TOF** — slab boundary artefact? (horizontal dark lines at slab junctions) | Increase slab overlap to ≥25%. If severe, consider single-slab TOF with reduced coverage. Check source images — dark lines can mimic stenosis or occlusion on MIP |
| **`resolve_3scan_trace_tra_p2`** — true restriction vs T2 shine-through on ADC? | Document true restriction. If distorted at skull base: flip phase-encode (A>>P → P>>A) |
| **`t1_vibe_fs_cor_C`** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection, repeat if extravasation suspected |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 9 sequences (TOF + brain with contrast) |
