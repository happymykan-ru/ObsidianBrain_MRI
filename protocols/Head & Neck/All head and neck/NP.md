# NP (Nasopharynx MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil. Full coverage from skull base to supraclavicular fossa is required for nodal staging.
- **Laser Landmark:** Nasion
- **Immobilization:** Foam padding.
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions — swallowing motion degrades the nasopharyngeal and nodal sequences.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra_NP` | Axial | ∥ hard palate (⟂ nasopharynx) | Part of orbit → C2/C3. Centre on NP | **None** |
| 2 | `t1_tse_tra_NP` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 3 | `resolve_4scan_trace_tra_NP` | Axial | Copy Slice from #1 | — | **None** |
| 4 | `t1_starvibe_fs_cor_NP_C` | Coronal | ⟂ hard palate | Centre on NP. Must include vertex of skull for perineural spread | **None** |
| 5 | `MPR` | Sag+Ax | — | Centre on NP. Vertex included | — |
| 6 | `t1_vibe_fs_tra_NP_C` | Axial | Copy Center from #1 | — (includes vertex for RT staging) | **None** |
| 7 | `t1_vibe_dixon_tra_lower_neck_C` | Axial | ⟂ axis of neck | Hyoid → supraclavicular fossa | **None** |

*#6: For RT planning, ensure coverage includes the vertex — perineural spread can track along cranial nerves to the skull vertex.*
*Tilting: following the hard palate is functionally equivalent to being perpendicular to the nasopharynx.*

---

## 3. Sequence Rationale

### Core Strategy

Nasopharyngeal carcinoma (NPC) staging requires assessment of the primary tumour (skull base invasion, perineural spread, retropharyngeal nodes) and comprehensive nodal staging down to the supraclavicular fossa. The protocol covers from skull base to clavicles using a combination of nasopharynx-targeted and neck sequences. All sequences use STIR or fat saturation — fat suppression is essential to distinguish enhancing tumour from the bright mucosal and nodal fat.

**`t2_stir_tra_NP` (#1)**
T2 STIR axial. STIR provides uniform fat suppression across the skull base and nasopharynx where B0 inhomogeneity from the sphenoid sinus, ethmoid air cells, and mastoids defeats chemical fat sat. The primary tumour is mildly T2 hyperintense against the suppressed background. Axial plane is standard for NPC staging — profiles the fossa of Rosenmüller, parapharyngeal space, and retropharyngeal nodes.

**Coverage:** Part of orbit → C2/C3, centred on the nasopharynx. Why the orbit? NPC spreads superiorly through the skull base via the foramen lacerum and foramen ovale to the cavernous sinus and orbital apex. The inferior orbital fissure is a direct conduit from the pterygopalatine fossa to the orbit — perineural tumour can track both ways. Clipping the orbit means missing this key route of spread. Why C2/C3 inferiorly? The retropharyngeal nodes (Level VII) sit anterior to the prevertebral muscles at C1–C3. Extending beyond C3 adds no additional nasopharyngeal nodal coverage — the lower cervical chains are covered by the dedicated lower neck sequence (#7).

**`t1_tse_tra_NP` (#2)**
Pre-contrast T1 TSE axial. Baseline for enhancement comparison. TSE avoids susceptibility artefact at the skull base-air interfaces. Matched geometry to post-contrast VIBE (#6) for subtraction.

**Contrast**
Standard dose IV gadolinium. DWI (#3) fills the post-injection delay. Target ~3–5 min before post-contrast T1 (#4–#7).

**`resolve_4scan_trace_tra_NP` (#3)**
RESOLVE DWI, 4-scan trace. Post-contrast — fills the enhancement delay while providing diagnostic DWI. NPC is cellular and shows restricted diffusion (ADC dark). 4 orthogonal directions give a more isotropic trace than 3-scan, reducing directional bias in the anisotropic skull base environment. RESOLVE reduces susceptibility distortion at the petrous bone and sphenoid — critical for the nasopharynx where EPI would fail.

**`t1_starvibe_fs_cor_NP_C` (#4)**
T1 StarVIBE FS coronal. StarVIBE uses a stack-of-stars radial k-space acquisition — the centre of k-space is continuously oversampled with each radial spoke. This makes it inherently motion-robust: swallowing, breathing, and carotid pulsation appear as radial streaks rather than coherent ghosts that simulate pathology. Coronal plane profiles the nasopharynx, skull base, cavernous sinuses, and bilateral cervical nodal chains for symmetric comparison. FS suppresses mucosal and nodal fat. This is the primary post-contrast sequence.

**Coverage:** Centred on the nasopharynx. Superior-inferior: must include the vertex of the skull — perineural tumour tracks along cranial nerves (V3 through foramen ovale, vidian nerve through the pterygopalatine fossa) all the way to the skull vertex. Anterior-posterior: nasal cavity/anterior maxilla through the prevertebral muscles and C-spine. NPC spreads anteriorly into the nasal cavity and paranasal sinuses; posteriorly it invades the prevertebral space and clivus. MPR (#5) provides sagittal and axial reformats with the same coverage.

**`MPR` (#5)**
Multiplanar reconstruction from StarVIBE (#4). Sagittal and axial reformatted views.

**`t1_vibe_fs_tra_NP_C` (#6)**
T1 VIBE FS axial. Matched geometry to pre-contrast T1 (#2) for direct enhancement comparison. Axial is the standard staging plane — the post-contrast axial pair confirms local tumour extent and retropharyngeal nodal enhancement. VIBE (Cartesian) is acceptable for the nasopharynx because the axial plane has less motion sensitivity than coronal; StarVIBE (#4) covers the motion-vulnerable coronal plane.

**`t1_vibe_dixon_tra_lower_neck_C` (#7)**
T1 VIBE Dixon axial lower neck. Dixon acquires water-only, fat-only, and in/opposed phase images in one acquisition.

**Coverage:** Hyoid → supraclavicular fossa. This is a separate acquisition from the nasopharynx because the lower neck requires different coil coverage, B1 shimming, and slice prescription. NPC nodal spread follows the internal jugular chain (Level II–IV) and spinal accessory chain (Level V) down to the supraclavicular fossa. The hyoid is the anatomical boundary between the upper neck (covered by the nasopharynx-targeted sequences) and the lower neck. Extending inferiorly to the clavicles ensures Level IV and supraclavicular nodes are included — nodal status at these levels changes staging from N1 to N3. In/opposed phase helps characterize nodes (fatty hilum dropout on opposed phase). Separate acquisition from the nasopharynx because the coil coverage and B1 shimming differ between skull base and lower neck.

---

## 4. What Each Sequence Answers

- **Perineural spread:** Coronal StarVIBE (#4) — trace V3 (mandibular nerve) from masticator space through foramen ovale to Meckel's cave, and the vidian nerve from pterygopalatine fossa through the vidian canal. Axial and reformatted sagittal confirm.
- **Skull base invasion:** STIR (#1) — marrow replacement in the clivus and petrous apex. Post-contrast VIBE (#6) confirms enhancing tumour.
- **Nodal staging:** Lower neck Dixon (#7) — NPC nodes follow Level II (upper internal jugular), Level V (spinal accessory), and retropharyngeal (Level VII). Any node >10 mm short axis or with central necrosis is suspicious.

---

## 5. Pathology-Based Variations

- **RT planning:** Extend `t1_vibe_fs_tra_NP_C` (#6) coverage to include the vertex — the radiation oncologist needs the full extent of perineural disease for target delineation.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex included on StarVIBE (#4) and MPR (#5)? Lower neck Dixon (#7) reaches clavicles? | Reposition if vertex clipped (perineural spread) or supraclavicular nodes cut off |
| **Motion** — swallowing artefact on StarVIBE (#4)? | Instruct patient to breathe quietly and avoid swallowing. StarVIBE is motion-robust but severe swallowing may still degrade |
| **Fat saturation** — uniform on StarVIBE (#4) and VIBE axial (#6) near the skull base? | Chemical fat sat fails near the sphenoid and mastoid air cells — precisely where the primary tumour sits. If patchy: manually shim with the shim volume narrowed over the nasopharynx. Lower neck Dixon (#7) has no air sinuses and rarely fails |
| **Post-contrast** — contrast present? Confirm mucosal and nodal enhancement | If absent: check IV line, confirm injection |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-27 | — | Initial — 7 sequences (StarVIBE, lower neck Dixon, 4-scan DWI) |
