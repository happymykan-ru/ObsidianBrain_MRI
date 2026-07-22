# Brain + Viewing Wand (Neuronavigation / Surgical Planning with Contrast)

**Version:** 1.0 | **Date:** 2026-07-22 | **Scanner:** [Confirm 1.5T/3T]

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
| 1 | `t2_tse_tra_p3_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dark_fluid_tra_brain` | Axial | Copy Slice and Sat from #1 | — | — |
| — | **Contrast** | — | — | — | — |
| 4 | `resolve_3scan_trace_tra_p2_brain` | Axial | Copy Slice from #1 | — | **None** |
| 5 | `t1_fl3d_sag_viewing_wand_C` | Sagittal | ∥ midline | Whole brain | **None** |
| 6 | `MPR` | Cor+Ax | — | Whole brain | — |
| 7 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |

*#5: The 3D dataset is loaded directly into the surgical neuronavigation system. MPR (#6) provides coronal and axial reformats from this source. Axial MPR must be ordered bottom-to-top (inferior → superior) — navigation systems expect this direction.*

---

## 3. Sequence Rationale

### Core Strategy

This protocol is designed for surgical planning with intraoperative neuronavigation (viewing wand). Every sequence choice is driven by the requirement that the 3D T1 dataset must be geometrically accurate, free of distortion, and compatible with the navigation software.

**`t2_tse_tra_p3_brain` (#1)**
T2 TSE axial with GRAPPA ×3. Core axial anatomy. p3 accelerates acquisition — surgical patients may be less tolerant of long scan times. Reference plane.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast T1 baseline. Matched to post-contrast (#7) for enhancement comparison and subtraction.

**`t2_tse_dark_fluid_tra_brain` (#3)**
CSF-suppressed T2 FLAIR. Non-enhancing tumour infiltration beyond the enhancing margin guides the surgical resection boundary.

**Contrast**
Standard dose IV gadolinium. DWI (#4) fills the post-injection delay. Target ~5 min before the 3D T1 (#5).

**`resolve_3scan_trace_tra_p2_brain` (#4)**
RESOLVE DWI placed post-contrast to fill the enhancement delay. Acute ischaemia, cellular tumour components. No time penalty — DWI runs while contrast equilibrates.

**`t1_fl3d_sag_viewing_wand_C` (#5)**
3D T1 FLASH sagittal — the neuronavigation dataset. This is the key surgical planning sequence. FLASH 3D (spoiled GRE) is chosen over VIBE or MPRAGE for stereotactic accuracy: no fat saturation (fat sat can create subtle geometry shifts at tissue interfaces), minimal geometric distortion (GRE readout with short TE), and good gray-white contrast for tumour delineation. Sagittal source gives the best axial and coronal reformats (#6) because phase-encode runs A/P, keeping distortion away from the surgical field. The dataset is exported directly to the neuronavigation system for intraoperative guidance.

**`MPR` (#6)**
Multiplanar reconstruction from the FLASH 3D (#5). Coronal and axial reformatted views — the surgeon reviews all three planes for surgical approach planning.

**`t1_fl2d_tra_brain_C` (#7)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map. Provides a conventional axial post-contrast reference alongside the 3D dataset.

---

## 4. How This Differs from Standard contrast_brain

- **`t1_fl3d_sag` replaces `t1_vibe_fs_cor`:** FLASH 3D without fat saturation is the gold standard for stereotactic planning. VIBE's fat sat can introduce subtle geometry shifts at tissue interfaces — unacceptable for navigation where millimetre accuracy matters. FLASH 3D has minimal geometric distortion.

- **Sagittal source instead of coronal:** The surgical approach is most commonly from the vertex or frontal/parietal convexity — sagittal profiles the approach trajectory in-plane. Sagittal acquisition places the phase-encode in A/P direction, keeping distortion away from the brain centre where the surgical target sits. Most navigation systems also prefer sagittal source data for registration to the patient's midline.

- **No fat sat on the 3D dataset:** Fat sat pulses create small frequency shifts that translate to spatial shifts at fat-water boundaries (scalp-skull, marrow-cortex). The error is small (~1–2 mm) but matters when targeting a tumour margin.

- **FLASH 3D instead of MPRAGE:** MPRAGE has B1 inhomogeneity — contrast varies across the brain, with the tumour margin appearing differently at the vertex vs the skull base. FLASH 3D gives consistent T1 contrast everywhere, which navigation software depends on for threshold-based tumour segmentation.

---

## 5. Pathology-Based Variations

- **MRA requested:** Add `TOF_3D_cs` (pre-contrast) and `TOF_3D_cs_C` (post-contrast). Compressed sensing (cs) TOF is used instead of standard multi-slab TOF — CS allows higher acceleration with less SNR penalty. Pre-contrast TOF shows the native arterial anatomy; post-contrast TOF shows the enhancing tumour-vessel relationship and venous involvement. The surgeon needs to know exactly where major vessels sit relative to the tumour for the approach trajectory. Coverage: the TOF must cover the vessels along the surgical approach, not the tumour itself (the tumour is on the T1 3D). Capture the relevant territory — ACA/pericallosal for frontal tumours, MCA for temporal, vertebrobasilar for posterior fossa.

- **Stereotactic planning only (no brain request):** For known tumours where full brain characterization has already been completed on a prior scan, the protocol is reduced to `t1_vibe_sag_viewing_wand_C` + `MPR` only. VIBE is used here because the dataset is for navigation registration only — the tumour has already been fully characterized, and the scan time saving (VIBE is faster than FLASH 3D) matters more than the slight resolution trade-off. No pre-contrast, no FLAIR, no DWI — just the 3D dataset for the navigation system.

- **Fast viewing wand (motion-prone or throughput):** Replace `t1_fl3d_sag` (#5) with `t1_vibe_sag` — scan time drops from ~3.5 min to ~1.5 min. Both are spoiled GRE. VIBE is faster because three things are enabled by default: slice interpolation (fewer partitions acquired), partial Fourier in the slice direction (~6/8 acquired), and optimized short TR (~3–5 ms vs ~8 ms for FLASH 3D). All three multiply to halve the scan time. Geometric accuracy is preserved — interpolation fills between acquired voxels without shifting them. VIBE's fat sat is OFF for the same geometric accuracy reasons. Trade-off: lower through-plane resolution, slightly noisier images, but for a patient who cannot stay still, a lower-resolution dataset without motion artefact is better than a high-resolution one degraded by movement.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — entire head contour included on the 3D (#5)? Nose not clipped anteriorly, vertex included superiorly, scalp not clipped posteriorly or laterally? | Navigation systems need the full head surface (including nose and entire scalp) for registration — both in-plane FOV and through-plane partitions must cover the full head. If any contour is clipped, extend FOV or increase partitions |
| **`t1_fl3d_sag` (#5)** — isotropic? | Do NOT change slice thickness, matrix, or FOV from protocol defaults. Any change that breaks isotropy degrades reformat quality and navigation accuracy |
| **MPR (#6)** — axial reformat ordered bottom-to-top? | Navigation systems expect inferior → superior slice order. Standard top-to-bottom ordering inverts the display |
| **Post-contrast** — contrast present? Confirm tumour enhancement | If absent: check IV line, confirm injection. Navigation depends on enhancing tumour margin for targeting |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-22 | — | Initial — 7 sequences (FLASH 3D for neuronavigation) |
