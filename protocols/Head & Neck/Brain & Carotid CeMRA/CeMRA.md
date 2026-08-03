# Brain + Carotid CeMRA (Combined Brain MRI with Contrast-Enhanced MRA)

**Version:** 1.0 | **Date:** 2026-08-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil + anterior body coil + spine array. The head and neck coil covers the brain through cervical carotid; the body coils cover the aortic arch through lower neck.
- **Laser Landmark:** Glabella (brain sequences). After table shift to isocentre for CeMRA, the neck is positioned at scanner isocentre.
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly. During the CeMRA acquisition: do not swallow — swallowing moves the carotids.
- **IV Access:** Minimum 20G (pink) for 2 mL/s; 20G required for 3 mL/s. 22G (blue) is marginal — it can sustain 2 mL/s at its upper limit but cannot deliver 3 mL/s. A tight bolus is essential for CeMRA timing; use the largest gauge available.
- **Contrast Dose:** At least 15 mL or standard weight-based dose — a sufficient bolus volume is needed for dense arterial opacification on CeMRA. Saline flush: [Confirm volume].
- **Renal Function:** Check eGFR before contrast administration.

---

## 2. Imaging Series

### Phase 1 — Brain Pre-Contrast (Table at LOC)

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_p3_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dark_fluid_tra_brain` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `resolve_3scan_trace_tra_160_brain` | Axial | Copy Slice from #1 | — | **None** |
| 5 | `TOF_3D_multi-slab` | Axial | ∥ AC-PC line | Carotid siphon → above corpus callosum | **Superior** (venous flow) |

*#1: p3 = parallel imaging factor 3 (GRAPPA).*
*#4: 3-scan trace DWI. For standard brain DWI, 3-scan is sufficient; head & neck protocols use 4-scan for more isotropic diffusion weighting at the skull base.*

### Phase 2 — CeMRA (Table shifts to ISO)

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| — | **Table Position** | — | Change to ISO | — | — |
| 6 | `localizer_neck` | 3-plane | — | Arch → above circle of Willis | — |
| 7 | `vessel_scout_neck` | Coronal | — | Arch → above circle of Willis | — |
| 8 | `angio3d_cor_pre` | Coronal | From vessel scout (#7). Ensure the slab is thick enough A/P to cover the full carotid along its entire course | Aortic arch (+ part of heart if possible) → above circle of Willis | **None** |
| — | **Contrast** | — | — | — | — |
| 9 | `care_bolus_cor` | Coronal | Copy Slice from #8 — select the slice with most overlap with the carotids on the vessel scout (#7). Single monitoring slice | Single slice through carotid | **None** |
| 10 | `angio3d_cor_post` | Coronal | Copy Slice from #8 | — | **None** |
| 11 | `angio3d_cor_post_2` | Coronal | Copy Slice from #8 | — | **None** |

*#8: Pre-contrast mask for subtraction.*
*#9: Visual bolus tracking — the radiographer watches the coronal monitoring slice and triggers when contrast reaches the carotid arteries. This is not an automated Care Bolus ROI placement; it is manual visual triggering.*
*#10: Arterial phase — triggered immediately upon contrast arrival at the carotids.*
*#11: Venous phase — second post-contrast acquisition without delay. Captures venous anatomy and any delayed filling.*

### Phase 3 — Brain Post-Contrast (Table shifts to LOC)

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| — | **Table Position** | — | Change to LOC | — | — |
| 12 | `t1_vibe_fs_cor_brain_C` | Coronal | ⟂ AC-PC line | Copy center from brain sequences. Vertex → foramen magnum | **None** |
| 13 | `MPR` | Sag+Ax | — | Whole volume | — |
| 14 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |

*#13: MPR reformatted from #12.*
*#14: Matched to pre-contrast FL2D (#2) for direct enhancement comparison.*

---

## 3. Sequence Rationale

### Core Strategy

This is a combined brain and carotid exam in a single contrast injection. The clinical question is typically TIA/stroke workup: is there a carotid stenosis or dissection, AND is there an intracranial lesion (infarct, chronic ischaemia, incidental pathology)? The brain pre-contrast sequences screen the parenchyma; TOF covers the circle of Willis without contrast; the CeMRA covers the arch-to-vertex vessels with contrast; and the post-contrast brain detects enhancing lesions. A single contrast bolus serves both the CeMRA and the post-contrast brain.

---

### Phase 1 — Brain Pre-Contrast

**`t2_tse_tra_p3_brain` (#1)**
T2 TSE axial, p3 accelerated. Core anatomical sequence — oedema, gliosis, infarction, white matter disease. Axial is the standard brain plane. Sat band inferior to suppress neck vessel flow artefact. p3 (GRAPPA ×3) reduces acquisition time; the brain is a screening adjunct in this protocol — the CeMRA is the primary question, so the SNR penalty from p3 is acceptable.

**`t1_fl2d_tra_brain` (#2)**
T1 FLASH 2D axial. Pre-contrast baseline for post-contrast FL2D (#14). Matched sequence for pre/post enhancement comparison — identical contrast mechanism gives clean subtraction. In the TIA/stroke setting, blood products (haemorrhagic infarct, microbleeds from small vessel disease or CAA) are intrinsically T1-hyperintense and must be distinguished from enhancing pathology (tumour, infection) on the post-contrast pair. Blood products are bright on both pre and post; enhancement is bright only post.

**`t2_tse_dark_fluid_tra_brain` (#3)**
T2 FLAIR axial. CSF-nulled T2 — periventricular and cortical/subcortical lesions visible against dark CSF. Essential for small vessel ischaemia, MS, encephalitis. Matched geometry to T2 (#1).

**`resolve_3scan_trace_tra_160_brain` (#4)**
RESOLVE DWI, 3-scan trace. Restricted diffusion = acute ischaemia (within minutes). Less distortion at skull base vs single-shot EPI. 3-scan trace is standard for brain — the 4-scan trace used in head & neck protocols adds time for only marginal gain in isotropic quality at the sinuses and mastoids; in supratentorial brain, 3-scan is sufficient.

**`TOF_3D_multi-slab` (#5)**
Time-of-flight MRA, 3D multi-slab. Non-contrast arterial imaging of the circle of Willis. TOF exploits in-flow enhancement: unsaturated blood entering the imaging slab is bright against saturated stationary tissue. Multi-slab acquisition reduces saturation of slow/distal flow (blood travelling through a single thick slab loses signal progressively; thinner slabs refresh the in-flow effect at each slab boundary).

**Coverage:** Carotid siphon → above corpus callosum. This captures the distal ICA, MCA (M1–M3), ACA (A1–A2), posterior communicating arteries, and basilar tip. The petrous and cervical ICA are below this coverage — they are assessed by the CeMRA (#10). Venous flow from above is suppressed by a superior sat band.

---

### Phase 2 — CeMRA

The table shifts from LOC (brain isocentre) to ISO (scanner isocentre at the neck). A new localizer is acquired at the new table position, covering the arch to above the circle of Willis.

**`angio3d_cor_pre` (#8)**
3D spoiled gradient echo, coronal slab. This is the subtraction mask — acquired before contrast, subtracted from the post-contrast acquisitions (#10, #11) to produce pure arterial/venous angiograms. Both carotids sit side-by-side in the same coronal slices, and the coronal slab puts the craniocaudal axis in-plane, capturing the full arch-to-vertex extent in a single FOV.

**Coverage:** Aortic arch → above the circle of Willis. The arch origin (brachiocephalic trunk, left common carotid, left subclavian) must be included — carotid stenosis at the origin is common and missed if the arch is clipped. Superiorly, the MCA/ACA branches above the circle are included to show intracranial collateral flow. If possible, extend inferiorly to include part of the left ventricle — visualising the LV enhance confirms the bolus has passed through the pulmonary circulation and reached the systemic arteries, distinguishing true arterial inflow from venous reflux up the neck veins (which can mimic carotid filling on the Care Bolus monitoring slice). The carotid has some anterior-posterior variation along its course (the bifurcation is more anterior than the arch origin); ensure the slab is thick enough A/P to cover the full carotid on the vessel scout (#7) at every level.

**`care_bolus_cor` (#9)**
Care Bolus — single coronal monitoring slice. The slice position is copied from the Anglo3D pre-contrast slab (#8): select the slice that has the greatest overlap with the carotid arteries as seen on the vessel scout (#7). This ensures the monitoring slice passes through the carotid bifurcation or common carotid rather than a vessel-poor section of the slab.

The radiographer watches the slice in real time and triggers manually when contrast fills the common carotid artery at the monitoring slice — the leading edge of the bolus just entering the proximal ICA. This catches peak arterial concentration in the carotid during k-space centre acquisition. Triggering too late (contrast already at the intracranial ICA) contaminates the arterial phase with jugular venous filling; triggering too early (contrast still in the arch) means the carotid hasn't filled yet. Unlike automated bolus tracking (ROI-based), visual triggering allows the radiographer to account for individual haemodynamics and trigger on the carotid of interest.

**`angio3d_cor_post` (#10)**
Arterial phase CeMRA. Triggered immediately upon contrast arrival at the carotids. Captures the arterial tree from arch to intracranial circulation with peak arterial enhancement. Subtracted from the pre-contrast mask (#8) to remove background tissue.

**`angio3d_cor_post_2` (#11)**
Second post-contrast acquisition — venous/delayed phase. The same 3D slab is re-acquired without further delay. The carotids remain enhanced; the jugular veins and dural sinuses now fill. Useful for: (1) confirming arterial filling defects (true stenosis vs timing artefact — if the stenosis persists on the second phase, it's real), (2) venous anatomy and patency, (3) delayed collateral filling in severe stenosis or occlusion.

---

### Phase 3 — Brain Post-Contrast

The table returns to LOC. Post-contrast brain sequences are acquired after the CeMRA — the contrast has already circulated systemically, and brain enhancement is optimal at this point (~5–8 min post-injection).

**`t1_vibe_fs_cor_brain_C` (#12)**
T1 VIBE FS coronal. High-resolution 3D gradient echo with fat saturation. Enhancing lesions (metastases, infection, inflammation) are visible against suppressed fat. Coronal acquisition covers the full brain; MPR (#13) provides sagittal and axial reformats. VIBE is chosen because it is faster than TSE coronal for whole-brain coverage with thin slices.

**Coverage:** Vertex → foramen magnum, copied from the brain pre-contrast centre.

**`MPR` (#13)**
Multiplanar reconstruction from VIBE (#12). Sagittal and axial reformatted views.

**`t1_fl2d_tra_brain_C` (#14)**
T1 FLASH 2D axial. Matched geometry to pre-contrast FL2D (#2) for direct enhancement comparison. FL2D is used for the matched pair — the pre-contrast FL2D (#2) serves as the baseline against which enhancing lesions are identified. Any T1-hyperintensity present on both pre and post is intrinsic (blood products, calcification); anything only on the post-contrast image is enhancing pathology.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — CeMRA: arch → above circle of Willis? Slab thick enough A/P to cover the full carotid at every level? Arch and part of the heart included? | Reposition if clipped. The arch origin is the most common site of missed coverage — check that the brachiocephalic trunk, left CCA, and left subclavian are included. The arch and part of the left ventricle must be in the FOV — see below |
| **Motion** — Swallowing during CeMRA (#10)? | Swallowing moves the carotids between the mask (#8) and arterial phase (#10). On the subtracted MIP: misregistration produces dark ring artefacts around the carotid wall and blurring/doubling of the vessel contour — the carotid appears duplicated or smeared with a dark halo. **If degraded:** (1) repeat CeMRA with a 2nd contrast dose (check eGFR first — confirm renal function can tolerate additional contrast) or (2) acquire a non-contrast TOF of the carotid to salvage the exam |
| **Bolus timing** — Triggered on CCA opacification alone? | Venous reflux up the SVC/brachiocephalic veins can mimic CCA filling on the monitoring slice. Causes: SVC obstruction, right heart failure / elevated CVP, same-side dialysis AV fistula, subclavian/brachiocephalic vein stenosis. Before triggering, verify the LV has enhanced — this confirms contrast has transited the pulmonary circulation. This is why the Anglo3D slab must include the arch and at least part of the heart |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-03 | — | Initial — 14 sequences over 3 phases (brain pre, CeMRA, brain post). TOF + Care Bolus CeMRA in a single contrast injection |
