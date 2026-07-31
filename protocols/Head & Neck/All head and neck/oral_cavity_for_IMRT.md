# Oral Cavity for IMRT (Oral Cavity / Oropharynx IMRT Planning Protocol)

**Version:** 1.0 | **Date:** 2026-07-31 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Standard head and neck coil. Head alignment is critical — all axial sequences are straight (no gantry tilt). Any head tilt cannot be compensated by prescription tilting. Ensure the head is properly aligned before starting.
- **Laser Landmark:** Nasion
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions — swallowing motion degrades the oropharyngeal and nodal sequences.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra_no_tilting_oral_cavity` | Axial | Straight axial (no gantry tilt) | Hard palate → hyoid bone (~C3). Centre on oropharynx | **None** |
| 2 | `t1_se_tra_no_tilting_oral_cavity` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_fs_dixon_cor` | Coronal | ⟂ hard palate | Anterior lips/oral tongue → past prevertebral muscles. Centre on oropharynx | **None** |
| 4 | `t2_stir_tra_no_tilting_neck` | Axial | Straight axial (no gantry tilt) | Hyoid (~C3) → supraclavicular fossa. Centre on mid-neck | **None** |
| 5 | `t1_se_tra_no_tilting_neck` | Axial | Copy Slice from #4 | — | **None** |
| 6 | `resolve_4scan_trace_tra_oral_cavity` | Axial | Copy Slice from #1 | — (hard palate level = skull base) | **None** |
| — | **Contrast** | — | — | — | — |
| 7 | `resolve_4scan_trace_tra_neck` | Axial | ⟂ axis of neck (can tilt) | Continues from #6. Hyoid (~C3) → supraclavicular fossa. Abut #6 with slight overlap | **None** |
| 8 | `t1_starvibe_fs_cor_oral_cavity_C` | Coronal | ⟂ hard palate (can tilt) | Centre on oropharynx. S/I: must include vertex → extended inferiorly for upper nodal stations (Level I–II). A/P: lips → past prevertebral | **None** |
| 9 | `MPR` | Sag+Ax | — | Whole volume (from #8) | — |
| 10 | `t1_vibe_fs_tra_no_tilting_C` | Axial | Straight axial (no gantry tilt) | Ventricles level → hyoid/cricoid (~C3/C4). Centre on oral cavity. Continue to lower neck | **None** |
| 11 | `t1_vibe_dixon_tra_C_lower_neck` | Axial | ⟂ axis of neck (can tilt) | Hyoid/cricoid (~C3/C4) → supraclavicular fossa. Centre on lower neck. Abut #10 with slight overlap | **None** |

*All axial sequences through the oral cavity use straight (no gantry tilt) prescription — tilted images must be resampled for the IMRT planning system, degrading resolution and introducing interpolation errors.*
*#7, #8, #11: can tilt — neck and coronal sequences are for diagnostic/nodal characterisation, not IMRT co-registration, so tilting is acceptable.*
*#8: StarVIBE = stack-of-stars radial VIBE. Motion-robust for swallowing artefact. Must include vertex — the IMRT dose calculation grid requires full craniocaudal coverage.*

---

## 3. Sequence Rationale

IMRT planning demands a geometrically accurate dataset — straight axial geometry and full craniocaudal coverage (ventricles → clavicles). Each sequence must either contribute to target delineation or provide anatomical reference for co-registration and dose calculation. The protocol splits into oral cavity and neck acquisitions because coil loading, B1 shimming, and FOV requirements differ between these regions.

**`t2_stir_tra_no_tilting_oral_cavity` (#1)**
T2 STIR axial, straight. STIR provides uniform fat suppression across the oral cavity and oropharynx where B0 inhomogeneity from dental amalgam and mandible defeats chemical fat sat. The primary tumour is mildly T2 hyperintense against the suppressed background. Axial plane profiles the tongue base, tonsillar fossa, parapharyngeal space, and retropharyngeal nodes — the standard plane for oropharyngeal tumour staging.

**Coverage:** Hard palate → hyoid bone (~C3), centred on the oropharynx. The hard palate is the natural roof of the oral cavity — oral cavity tumours do not spread superiorly through the skull base (unlike NPC). The hyoid marks the boundary between oropharynx and hypopharynx; extending to C3 includes the full tongue base, floor of mouth, and Level II nodes.

**`t1_se_tra_no_tilting_oral_cavity` (#2)**
Pre-contrast T1 SE axial, straight. Matched geometry to #1 for pre-/post-contrast enhancement comparison. T1 provides the anatomical reference for MRI-CT co-registration — bony landmarks (mandible, maxilla, hard palate, vertebral bodies) are high-contrast on T1. Axial plane matches the standard IMRT planning orientation.

**`t2_tse_fs_dixon_cor` (#3)**
T2 TSE Dixon coronal, ⟂ hard palate. Dixon provides water-only, in-phase, and opposed-phase from one acquisition. Coronal plane profiles the oral tongue, floor of mouth, and cervical nodes for symmetric left-right comparison — the tongue extends superior-inferiorly, and coronal is the plane that best captures tumour depth of invasion into the tongue musculature.

**Coverage:** Anterior lips/oral tongue → past prevertebral muscles, centred on oropharynx. Anteriorly must include the lips and oral tongue surface — SCC spreads along the mucosal surface and the anterior margin defines the surgical boundary. Posteriorly past the prevertebral muscles is needed because the prevertebral space and retropharyngeal nodes must be fully covered. 

**`t2_stir_tra_no_tilting_neck` (#4)**
T2 STIR axial through the full neck, straight. STIR uniformly suppresses fat across the neck so nodes are conspicuous. Pre-contrast nodal mapping of the entire cervical chain guides the elective nodal irradiation field — the radiation oncologist needs to see which nodal stations are involved before contrast.

**Coverage:** Hyoid (~C3) → supraclavicular fossa, centred on mid-neck. Abuts the oral cavity STIR (#1) at C3 with slight overlap. Level I (submental, submandibular) is the first-echelon drainage for oral tongue and floor of mouth SCC — these nodes sit high and anterior and must be specifically covered. Extending to the clavicles ensures Level IV and supraclavicular nodes are included; involvement here upstages disease.

**`t1_se_tra_no_tilting_neck` (#5)**
Pre-contrast T1 SE axial neck, straight. Pre-contrast anatomical reference for the neck portion of the planning volume. Matched geometry to #4 — the pre-/post-contrast pair (#5 + #11) confirms nodal enhancement. Bony landmarks (vertebral bodies, clavicles, sternum) for MRI-CT co-registration of the lower planning volume.

**`resolve_4scan_trace_tra_oral_cavity` (#6)**
RESOLVE DWI, 4-scan trace, straight. Oral cavity SCC is cellular and restricts diffusion — the ADC map defines tumour extent beyond the enhancing margin for GTV delineation. 4-scan trace reduces directional bias. RESOLVE's readout-segmented EPI reduces susceptibility distortion at the mandible and dental amalgam where single-shot EPI would fail. Straight geometry for IMRT planning.

**Coverage:** Copy slice from #1 — hard palate (skull base level) → hyoid (~C3). The hard palate is the bony landmark for the skull base; coverage from this level already includes the skull base structures needed for dose calculation to the brainstem and temporal lobes.

Standard dose IV gadolinium. Target ~3–5 min delay. Post-contrast sequences immediately follow.

**`resolve_4scan_trace_tra_neck` (#7)**
RESOLVE DWI through the neck. Placed post-contrast to fill the enhancement delay. Nodal restricted diffusion detects micrometastases before nodes enlarge — the radiation oncologist needs to decide per nodal station whether to irradiate. Perpendicular to the cervical spine axis (can tilt) — this is for nodal characterisation, not IMRT co-registration.

**Coverage:** Continues from #6. Hyoid (~C3) → supraclavicular fossa. Abuts #6 with slight overlap — no gap between the two DWI acquisitions that would miss Level II/III junction nodes.

**`t1_starvibe_fs_cor_oral_cavity_C` (#8)**
T1 StarVIBE FS coronal, ⟂ hard palate (can tilt). StarVIBE uses stack-of-stars radial k-space acquisition — the centre of k-space is continuously oversampled with each radial spoke. Swallowing moves the pharyngeal wall vertically, in-plane in the coronal plane — precisely where radial sampling converts coherent ghosts to incoherent streaks. This is the primary post-contrast sequence: enhancing tumour margin defines the GTV against suppressed mucosal and nodal fat. MPR (#9) provides sagittal and axial reformatted views.

**Coverage:** Centred on oropharynx. S/I: must include the vertex → extended inferiorly to cover upper nodal stations (Level I–II). A/P: lips/oral tongue → past prevertebral muscles. Although oral cavity perineural spread follows the lingual and inferior alveolar nerves inferiorly (not superiorly to the vertex like NPC), the IMRT dose calculation grid requires full craniocaudal imaging — the radiation oncologist cannot dose-constrain critical intracranial structures (brain, superior sagittal sinus) if they are outside the imaging volume.

**`MPR` (#9)**
Multiplanar reconstruction from StarVIBE (#8). Sagittal and axial reformatted views for tumour extent assessment without additional scan time. Sagittal is particularly useful for tongue primaries — it shows the anterior-posterior tumour extent and depth of invasion in a single plane.

**`t1_vibe_fs_tra_no_tilting_C` (#10)**
T1 VIBE FS axial, straight. The enhancing tumour margin on this sequence defines the gross tumour volume (GTV). Pre- and post-contrast axial pair (#2 + #10) confirms enhancement. VIBE (Cartesian 3D GRE) is acceptable for axial — less motion sensitivity than coronal; StarVIBE (#8) covers the motion-vulnerable coronal plane. Straight geometry for IMRT co-registration.

**Coverage:** Ventricles level → hyoid/cricoid (~C3/C4), centred on the oral cavity. Extending superiorly to the lateral ventricles includes the brain for intracranial dose calculation — the brainstem, optic chiasm, and temporal lobes must be visible for dose constraints. Extending inferiorly beyond pre-contrast #1 to C3/C4 covers nodal Levels I–III. Does not extend to the supraclavicular fossa — that is separately covered by the lower neck Dixon (#11).

**`t1_vibe_dixon_tra_C_lower_neck` (#11)**
T1 VIBE Dixon axial lower neck, ⟂ cervical spine axis (can tilt). Dixon acquires water-only, in-phase, and opposed-phase images in one acquisition. Separate from #10 — dedicated shimming over the lower neck and the larger S/I coverage needed for the full treatment volume. Dixon is used rather than standard FS because the lower neck has irregular geometry (large FOV, curved contours, tracheal air, B1 drop-off at coil edge) — Dixon separates fat and water mathematically based on the fixed chemical shift (~3.5 ppm), making it more robust to B0 inhomogeneity than a frequency-selective saturation pulse. Post-contrast, only the water-only (fat-suppressed T1) image is of interest — enhancing nodes against dark fat.

**Coverage:** Hyoid/cricoid (~C3/C4) → supraclavicular fossa, centred on the lower neck. Abuts the oral cavity VIBE (#10) with slight overlap. Supraclavicular fossa coverage is essential — involvement at this level upstages N2 → N3, changing the radiation field from unilateral to bilateral neck irradiation.

---

## 4. How This Differs from Diagnostic Oral Cavity

The core difference is geometric accuracy for IMRT planning vs diagnostic characterisation. Tilted images must be resampled to straight axial during treatment planning import — resampling degrades spatial resolution and introduces interpolation errors at tissue boundaries, compromising GTV delineation. Every oral cavity axial sequence uses straight geometry so all sequences share the same DICOM coordinate space for direct image fusion.

**T2 Dixon coronal replaces T2 FS + T2 non-FS coronals.** Diagnostic prioritises contrast quality: two separate T2 coronals (`t2_tse_cor_fs` + `t2_tse_cor`), each optimised independently — FS tuned for fat suppression fidelity, non-FS at the ideal TE for tumour-muscle contrast. The cost: two scans, longer time, and motion between them means the FS and non-FS images are inherently misregistered. IMRT prioritises geometric certainty: a single `t2_tse_fs_dixon_cor` provides water-only, in-phase, and opposed-phase — three perfectly co-registered contrasts, no motion misregistration, plus opposed-phase marrow assessment. The cost: lower SNR (signal split across echoes) and the in-phase TE is fixed, which may not be the optimal TE for tumour-muscle contrast. For diagnostic reporting, contrast fidelity wins. For IMRT target delineation, knowing that the water-only tumour boundary and the in-phase anatomical boundary are spatially identical wins.

**Neck coverage.** Diagnostic oral cavity stops at the hyoid (~C3) — it covers the primary tumour and retropharyngeal/Level II nodes but does not assess the lower cervical chains. IMRT must cover the full nodal drainage of oral cavity SCC: Level I (submental, submandibular) through Levels II–IV to the supraclavicular fossa. This adds pre-contrast neck STIR + T1 SE (#4, #5), a dedicated neck DWI (#7), and a separate post-contrast lower neck Dixon VIBE (#11). Nodal status at each level determines the elective nodal irradiation field — the radiation oncologist needs to see every station. 

**T1 SE instead of T1 TSE for pre-contrast T1.** Diagnostic uses TSE — the refocusing pulses reduce susceptibility artefact at the oropharyngeal air-soft tissue interfaces. IMRT uses SE because sharper boundaries are needed for MRI-CT co-registration accuracy. TSE's turbo factor introduces mild blurring across tissue interfaces. Oral cavity has less severe susceptibility than the skull base (no sphenoid/ethmoid air cells), so SE is feasible.

---

## 5. How This Differs from NP for IMRT

Both protocols share the same IMRT principles — straight axial geometry on co-registration sequences, split DWI, StarVIBE coronal + MPR, vertex coverage, separate neck sequences — but differ in pre-contrast composition, contrast weighting, and nodal emphasis driven by the different tumour biology.

**Vertex coverage — same requirement, different reason.** Both protocols include vertex on StarVIBE and MPR, and superior coverage to the brain on axial VIBE (ventricles for OC, vertex for NP). NP needs it because perineural tumour tracks directly along V3 and the vidian nerve superiorly through the skull base to the vertex. Oral cavity perineural spread follows the lingual and inferior alveolar nerves inferiorly toward the mandible — the vertex is not a perineural route. The vertex is included for dose calculation completeness: critical intracranial structures (brainstem, optic chiasm, temporal lobes) must be within the imaging volume for dose constraints, and the dose grid cannot extend beyond what is imaged.

**Registration approach.** NP uses a dedicated pre-contrast T1 coronal oblique (⟂ skull table) for MRI-CT co-registration — the anterior cranial fossa floor is the most stable, reproducible bony landmark for aligning the skull base to the planning CT, and pre-contrast T1 provides clean bony anatomy before enhancement. Oral cavity does not use a dedicated coronal — registration relies on the pre-contrast T1 SE axial sequences (#2, #5). Straight axial geometry matches the CT acquisition plane, and the mandible, maxilla, hard palate, and vertebral bodies provide sufficient bony landmarks at the oral cavity level. The T2 Dixon coronal (#3) serves tumour delineation (T2-defined tumour depth into tongue muscle), not registration.

**Neck assessment.** NP assesses the neck with post-contrast DWI alone — NP nodes are primarily retropharyngeal (Level VII, covered by the NP-targeted STIR) and Level II–V along the internal jugular and spinal accessory chains. DWI is sufficient because the clinical question per station is binary: restricted diffusion = disease. Oral cavity SCC has more extensive nodal drainage through Level I (submental, submandibular) as first-echelon nodes, then Level II–IV to supraclavicular fossa. Level I is unique to oral cavity, sits high and anterior, and DWI alone does not reliably distinguish Level I nodes from adjacent submandibular gland and muscle without anatomical reference. Pre-contrast STIR + T1 SE (#4, #5) provide this anatomical map. Post-contrast lower neck Dixon (#11) adds robust fat-suppressed T1 for nodal enhancement — complementing DWI with morphological assessment.

**Post-contrast axial: single (NP) vs split (OC).** Consequence of the neck assessment difference above. NP: one VIBE FS — DWI handles nodes. OC: VIBE FS + lower neck Dixon — Dixon provides robust fat sat for nodal assessment in the irregular lower neck, and cannot share an acquisition with chemical FS.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Geometry** — all axial sequences straight (no gantry tilt)? | Confirm tilt = 0 on oral cavity axials. Neck DWI, StarVIBE coronal, and lower neck Dixon can tilt |
| **Coverage** — overlap at C3/C4 between oral cavity and neck sequences? | Slight overlap at the hyoid — a gap misses Level II/III junction nodes. |
| **Motion** — swallowing or tongue movement? | Swallowing ghosts on StarVIBE coronal. Tongue motion blurs T2 Dixon coronal and creates ghost replicas on axial VIBE. Instruct patient to keep still |
| **Fat saturation and diffusion** — uniform fat suppression? Fat suppressed on b=0? | Manual shim over oropharynx if fat sat is patchy. Re-shim if fat is bright on diffusion b=0 |
| **Lower neck** — no wrap artefact on Dixon? | Wrap from shoulders degrades supraclavicular nodes. Swap phase and slice directions if needed |
| **Post-contrast** — contrast present? | If absent, check IV line and confirm injection |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-31 | — | Initial — 11 sequences (straight axial for IMRT, split OC/neck DWI, pre-contrast neck STIR/T1, T2 Dixon coronal, separate lower neck Dixon) |
| 1.1 | 2026-07-31 | — | Corrections: #6 DWI OC includes skull base; #7 neck DWI explicitly tiltable; #8 StarVIBE includes vertex + can tilt; #10 VIBE OC starts ventricles level; #11 lower neck Dixon explicitly tiltable. Updated Sections 3, 4, 5, 7 accordingly |
| 1.3 | 2026-07-31 | — | Restructured: Section 3 expanded with coverage-focused rationale; Section 5 converted to prose (no table); content deduplicated between rationale and difference sections |
