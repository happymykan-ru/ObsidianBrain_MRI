# NP for IMRT (Nasopharynx IMRT Planning Protocol)

**Version:** 1.0 | **Date:** 2026-07-28 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil (two options):**
  - **With RT mask:** 2 body coils wrapped around the head RT mask + 1 4-channel flex coil over the neck, with a soft pad between the RT mask and flex coil. Use the same RT mask that will be used during IMRT delivery.
  - **Without RT mask:** Standard head and neck coil. Head alignment is critical — all axial sequences are straight (no gantry tilt). Any head tilt cannot be compensated by prescription tilting. Ensure the head is properly aligned before starting.
- **Laser Landmark:** Nasion
- **Immobilization:** RT mask with bite block (if mask used). Positioning must match treatment delivery exactly.
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra_no_tilting_NP` | Axial | Straight axial (no gantry tilt) | Above anterior cranial fossa → below tongue (~C3/C4). Centre on NP | **None** |
| 2 | `t1_tse_tra_no_tilting_NP` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t1_tse_cor_obl_3mm_NP` | Coronal Oblique | ⟂ skull table | Centre on NP. Posterior border of maxillary sinus → sphenoid | **None** |
| 4 | `resolve_diff_tra_no_tilting_NP` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 5 | `resolve_diff_tra_neck` | Axial | ⟂ axis of neck | Hyoid → supraclavicular fossa | **None** |
| 6 | `t1_starvibe_fs_cor_NP_C` | Coronal | ⟂ hard palate | Centre on NP. Must include vertex | **None** |
| 7 | `MPR` | Sag+Ax | — | Centre on NP. Vertex included | — |
| 8 | `t1_vibe_fs_tra_no_tilting_NP_C` | Axial | Straight axial (no gantry tilt) | Expanded axial coverage: vertex → lower neck. Centre on NP | **None** |

*All axial sequences use straight (no gantry tilt) prescription — tilted images must be resampled for the IMRT planning system, degrading resolution and introducing interpolation errors.*
*#3: Pre-contrast coronal oblique — provides baseline coronal anatomy for RT planning reference.*
*#5: Separate neck DWI for nodal staging — nodal involvement changes the radiation field.*

---

## 3. Sequence Rationale

### Core Strategy

IMRT planning requires a geometrically accurate dataset that can be directly imported into the treatment planning system without reformatting. Every sequence choice is driven by RT planning requirements: straight axial geometry, coverage that matches the treatment volume, and sequences that define the tumour extent for target delineation.

**`t2_stir_tra_no_tilting_NP` (#1)**
T2 STIR axial, straight geometry (no gantry tilt). Same STIR rationale as diagnostic NP — uniform fat suppression across the skull base. For why straight geometry is required, see Section 4.

**Coverage:** Above anterior cranial fossa → below tongue (~C3/C4), centred on the nasopharynx. Superiorly this includes the inferior frontal lobes and orbital apex — NPC spreads to the cavernous sinus and orbit via the foramen lacerum and inferior orbital fissure. Inferiorly the tongue base sits at C3–C4 — extending below the tongue includes the full oropharynx and Level II–III nodes. This is a larger superior-inferior coverage than diagnostic NP because IMRT planning needs the full craniocaudal extent for dose calculation and target delineation.

**`t1_tse_tra_no_tilting_NP` (#2)**
Pre-contrast T1 TSE axial, straight geometry. Baseline for target delineation — the pre-contrast T1 defines the non-enhancing tumour extent and surrounding anatomy.

**`t1_tse_cor_obl_3mm_NP` (#3)**
Pre-contrast T1 TSE coronal oblique, 3 mm slices. Not present in diagnostic NP — added for MRI-CT co-registration. Prescribed perpendicular to the skull table (anterior cranial fossa floor), centred on the nasopharynx. For why pre-contrast coronal anatomy and why the skull table plane, see Section 4.

**Coverage:** Posterior border of maxillary sinus → sphenoid. The maxillary sinus posterior wall is the anterior boundary of the pterygopalatine fossa (PPF) — a small fat-filled space behind the maxilla where V2 (maxillary nerve) and the vidian nerve converge. NPC perineural spread passes through the PPF; clipping the posterior maxillary sinus clips the PPF. Posteriorly, the sphenoid bone and clivus are where NPC directly invades the skull base. The post-contrast StarVIBE (#6) covers the full vertex for perineural tracking upward; this pre-contrast coronal is focused on the skull base itself.

**`resolve_diff_tra_no_tilting_NP` (#4)**
RESOLVE DWI through the nasopharynx, straight geometry. The primary tumour is cellular and restricts diffusion — the ADC map helps define the tumour extent beyond the enhancing margin. Straight geometry for the same IMRT compatibility reason.

**Contrast**
Standard dose IV gadolinium. Post-contrast sequences immediately follow. Target ~3–5 min delay.

**`resolve_diff_tra_neck` (#5)**
RESOLVE DWI through the neck. A separate DWI acquisition covering the cervical nodes. In diagnostic NP, the lower neck is covered by the Dixon VIBE — here the DWI adds nodal characterization because nodal involvement changes the radiation field (elective neck irradiation vs involved-field). Restricted diffusion in nodes raises suspicion even if they are not enlarged.

**Coverage:** Hyoid → supraclavicular fossa. The hyoid sits at ~C3 — this abuts the inferior extent of the NP DWI (#4, below tongue at C3/C4) with slight overlap. No gap between the two DWI acquisitions. Unlike the NP sequences, this is tiltable — prescribed perpendicular to the cervical spine axis. The neck DWI is for nodal characterization, not IMRT planning registration, so tilting is acceptable.

**`t1_starvibe_fs_cor_NP_C` (#6)**
StarVIBE FS coronal. Same motion-robust radial acquisition as diagnostic NP. Post-contrast enhancement defines the tumour margin for target delineation. MPR (#7) provides sagittal and axial reformats.

**Coverage:** Centred on the nasopharynx. Superior-inferior: must include the vertex — perineural tumour tracks along cranial nerves (V3 through foramen ovale, vidian nerve through the pterygopalatine fossa) to the skull vertex. Anterior-posterior: nasal cavity/anterior maxilla through the prevertebral muscles and C-spine. NPC spreads anteriorly into the nasal cavity and paranasal sinuses; posteriorly it invades the prevertebral space and clivus.

**`MPR` (#7)**
Multiplanar reconstruction from StarVIBE (#6). Sagittal and axial reformatted views.

**`t1_vibe_fs_tra_no_tilting_NP_C` (#8)**
VIBE FS axial, straight geometry. The enhancing tumour margin defines the gross tumour volume (GTV) for IMRT planning. Pre- and post-contrast axial sequences have different coverage — the pre-contrast T1 covers standard NP axial extent; the post-contrast VIBE covers the full treatment volume.

**Coverage:** Vertex → lower neck, centred on the nasopharynx. Posteriorly, include the spinal canal and both anterior and posterior cervical triangles — the posterior triangle (Level V, spinal accessory chain) is a common route of NPC nodal spread and must be included. Anteriorly, include the maxillary sinuses, nasal cavity, and oropharynx. For why vertex-to-lower-neck coverage and the role of dose calculation, see Section 4.

---

## 4. How This Differs from Standard Diagnostic NP

The core difference is geometric accuracy for RT planning vs diagnostic characterization.

- **No gantry tilt on all axial sequences:** The diagnostic protocol follows the hard palate to profile the nasopharynx in true cross-section — better for diagnostic assessment of the fossa of Rosenmüller and parapharyngeal space. IMRT uses straight axial because the planning system works in the scanner's DICOM coordinate space. Tilted images must be resampled to straight axial during import — resampling degrades spatial resolution and introduces interpolation errors at tissue boundaries, compromising target delineation accuracy. Straight axial avoids this entirely: every sequence is in the same coordinate space for direct image fusion.

- **Added pre-contrast T1 coronal oblique:** Not present in diagnostic NP. The radiation oncologist needs coronal anatomy before contrast to co-register the MRI with the planning CT. Post-contrast enhancement can obscure the baseline bony landmarks and soft tissue boundaries the CT needs to align to. A pre-contrast coronal T1 provides a clean anatomical reference for MRI-CT fusion. The skull table (anterior cranial fossa floor) is chosen as the prescription reference because it is the most stable, reproducible bony landmark on the sagittal scout — the radiation plan is referenced to bony anatomy, and the skull base is the key reference plane.

- **Two DWI acquisitions (NP + neck) instead of one:** Diagnostic NP has a single 4-scan DWI through the nasopharynx. IMRT adds a separate neck DWI for nodal assessment — nodal involvement changes the radiation field from localized to elective neck irradiation. The NP DWI is straight axial (IMRT registration); the neck DWI is tilted perpendicular to the cervical spine (for nodal characterization, not registration).

- **No lower neck Dixon — DWI instead for nodal assessment:** Diagnostic NP uses Dixon for nodal staging — Dixon (T1-weighted, water-only) shows nodal anatomy, size, enhancement, and in/opposed phase helps characterize morphology (fatty hilum). The radiologist is characterizing individual nodes: is this node enlarged, necrotic, enhancing? IMRT uses DWI because the clinical question is binary per nodal station: is there disease here or not? Restricted diffusion can detect micrometastases before a node enlarges. The radiation oncologist needs to decide whether each nodal station receives irradiation — DWI answers this more directly than Dixon. Size and morphology from Dixon are secondary to the presence of restricted diffusion.

- **Expanded VIBE axial coverage (vertex → lower neck):** The StarVIBE coronal detects whether perineural tumour reaches the vertex (qualitative — is there disease?). The VIBE axial provides the full craniocaudal image volume for dose calculation (quantitative — dose to every tissue plane). The radiation oncologist cannot plan to tissue they cannot see: if perineural tumour tracks to the vertex, the vertex must be within the imaging volume or it will not be included in the radiation field. Even if no disease is present, the absence must be confirmed — clipping the vertex clips the dose grid, and dose to critical structures at the upper margin (brain, optic chiasm) is calculated from incomplete data. Posterior cervical triangle (Level V) must also be included — a common NPC nodal spread route that diagnostic NP may not fully cover.

For what each sequence answers (perineural spread, skull base invasion, nodal staging), see `NP.md` Section 4. The diagnostic content is the same; the acquisition geometry is different.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Geometry** — all axial sequences straight (no gantry tilt)? | Confirm tilt is set to zero. If any sequence has tilt, it must be resampled for the planning system — re-acquire with straight geometry |
| **Coverage** — vertex included on StarVIBE (#6), MPR (#7), and axial VIBE (#8)? | Reposition if vertex clipped |
| **Fat saturation** — uniform on all post-contrast VIBE/StarVIBE (#6, #8) across the skull base and lower neck? | Tight manual shim over the nasopharynx and neck. Fat sat can fail near the nasopharynx and sphenoid sinus air-tissue interfaces; lower neck should be uniform but verify |
| **Motion** — swallowing artefact on StarVIBE (#6)? | Swallowing moves the pharyngeal wall vertically — in-plane in the coronal plane, creating ghosts. Axial VIBE is perpendicular to this motion (through-plane blurring only, less severe). Instruct patient to breathe quietly and avoid swallowing |
| **Diffusion (#4, #5)** — fat suppressed on b=0 images? | If fat is bright on b=0, the water peak was mis-selected during prescan — the fat sat pulse is tuned to the wrong frequency. Nodes sit in fat; unsuppressed fat can mimic restricted diffusion. Re-shim and ensure the automatic frequency selection is correct |
| **Post-contrast** — contrast present? Confirm mucosal and nodal enhancement | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-28 | — | Initial — 8 sequences (straight axial for IMRT planning) |
