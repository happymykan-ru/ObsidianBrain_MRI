# Face AVM (Facial Arteriovenous Malformation MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-01 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil
- **Laser Landmark:** Nasion
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions. Motion degrades the TWIST dynamic series (#5) — even small facial movements can obscure small feeding arteries.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_cor_fs` | Coronal | ⟂ hard palate | Forehead/supraorbital ridge → below mandible. A/P: nasal tip/lips → preauricular region. Centre on lesion | **None** |
| 2 | `t2_tse_cor` | Coronal | Copy Slice from #1 | — | **None** |
| 3 | `t2_stir_tra` | Axial | ∥ hard palate | Same S/I extent as #1. Centre on lesion | **None** |
| 4 | `t1_se_tra` | Axial | Copy Slice from #3 | — | **None** |
| — | **Contrast + TWIST dynamic** | — | — | — | — |
| 5 | `TWIST_cor_dyn` | Coronal | ⟂ hard palate | Slab narrowed over the lesion (temporal resolution priority). Centre on AVM | **None** |
| 6 | `t1_se_fs_tra_C` | Axial | Copy Slice from #3 | — | **None** |
| 7 | `t1_tse_cor_fs_C` | Coronal | Copy Slice from #1 | — | **None** |

*#1: 4 mm slice thickness — thinner than the standard 5–6 mm used in other head/neck protocols. AVMs are tortuous, small-vessel lesions and the nidus can be missed on thicker slices.*
*#5: TWIST (Time-resolved angiography With Interleaved Stochastic Trajectories) is a 4D dynamic MRA acquired during the contrast bolus passage. The slab is narrowed over the AVM to achieve frame rates of ~2–5 seconds, sufficient to separate arterial from early venous phases. TWIST replaces DWI in this protocol — DWI is not useful for vascular lesions.*

---

## 3. Sequence Rationale

### Core Strategy

Facial AVM imaging is a vascular protocol, not an oncological one. The clinical questions are: (1) Where is the nidus, and what are its arterial feeders and venous drainage? (2) Is this a high-flow AVM (early venous filling on TWIST) or a low-flow venous malformation? (3) What facial compartments are involved — skin, subcutaneous fat, muscle, bone, orbit? Treatment is embolization, surgery, or combined — the interventional radiologist and surgeon need a vascular roadmap.

The protocol is built around paired pre- and post-contrast sequences with a coronal dynamic MRA (TWIST) as the centrepiece. SE is used for the pre- and post-contrast T1 axial because the tissue-vessel interface needs to be sharp. DWI is absent — AVMs are flow voids, not cellular masses, and DWI contributes nothing. There is no lower neck sequence — AVMs are localised lesions without nodal staging requirements.

---

**`t2_tse_cor_fs` (#1)**
T2 TSE coronal with fat saturation. 4 mm slice thickness.

The coronal plane gives symmetric comparison of both sides of the face — most AVMs are unilateral and asymmetry is the earliest sign. FS suppresses the abundant facial and orbital fat. Flow voids (fast arterial flow) appear as dark serpiginous structures against the bright suppressed background. Slow-flow or thrombosed components appear T2-bright.

The 4 mm slice thickness is deliberate. AVMs are tortuous tangles of small vessels — the nidus can occupy only 1–2 slices on standard 5–6 mm acquisitions and be missed. Thinner slices improve nidus detection and delineation of individual feeding branches.

**Coverage:** Forehead/supraorbital ridge (superior) → below mandible (inferior). Anterior: nasal tip and lips. Posterior: preauricular region. AVMs of the face can involve the forehead and scalp (superficial temporal artery), cheek (facial artery, transverse facial artery), lip, periorbital region (ophthalmic artery or external carotid branches), and ear (posterior auricular artery). Superior coverage must be high enough to include forehead contributions; inferior coverage extends below the mandible to capture the facial artery as it crosses the mandibular border.

---

**`t2_tse_cor` (#2)**
T2 TSE coronal without fat saturation. Matched geometry to #1.

The anatomical reference. Without FS, the natural contrast between muscle, fat planes, parotid gland, and vessels is preserved. This shows the AVM's relationship to the mimetic muscles (orbicularis oris, zygomaticus, buccinator), masseter, parotid gland, and orbital structures — the surgeon or interventional radiologist needs to know exactly which tissue compartments are involved and which normal structures are at risk. It also confirms that dark structures on the FS sequence (#1) are true flow voids and not just dark fat or soft tissue.

---

**`t2_stir_tra` (#3)**
T2 STIR axial. Matched coverage to #1/#2.

Axial profiles the AVM's anteroposterior extent — relationship to the maxilla, mandible, buccal space, masticator space, and parapharyngeal space. STIR is chosen over chemical FS for the same reason as in PNS imaging: the face sits adjacent to paranasal sinuses, and dental hardware creates additional B0 inhomogeneity. STIR gives uniform fat suppression regardless.

---

**`t1_se_tra` (#4)**
T1 Spin Echo axial. Pre-contrast. Matched geometry to #3.

Pre-contrast baseline for enhancement comparison. T1 SE shows the pre-contrast appearance of the nidus — there may be intrinsic T1 hyperintensity from methaemoglobin in thrombosed components or slow-flow within the nidus. SE provides sharp anatomical detail for the tissue-vessel interface. This sequence also serves as the mask for subtraction from the post-contrast T1 (#6) — matched geometry is essential.

---

**Contrast + TWIST dynamic**

Standard dose IV gadolinium. Injection rate: 3 mL/s (20G) — higher than standard 2 mL/s to produce a compact bolus. A tight bolus is essential for temporal separation of arterial and venous phases on TWIST.

TWIST (#5) is acquired during the first pass of the contrast bolus. Post-contrast T1 (#6, #7) follow.

---

**`TWIST_cor_dyn` (#5)**
TWIST time-resolved dynamic MRA, coronal. Acquired during contrast bolus passage.

This is the defining sequence for AVM characterisation — the reason this protocol exists. TWIST acquires rapid sequential 3D volumes (~2–5 s temporal resolution) during the contrast bolus passage, producing a time-resolved angiogram. The coronal plane is chosen because the face is broad coronally: most AVMs involve the cheek, lip, periorbital region, or ear — all profiled well in a single coronal slab. The slab is narrowed over the lesion to maximise temporal resolution; spatial resolution is traded for speed.

TWIST answers every critical question for treatment planning:

- **Arterial feeders:** Which external carotid branches supply the nidus? Facial artery (crosses mandible → courses toward nasal ala), maxillary artery branches (infraorbital, sphenopalatine, descending palatine), superficial temporal artery (forehead and scalp AVMs), or ophthalmic artery (ICA contribution, periorbital AVMs)?
- **Nidus:** Size, morphology, and exact location of the arteriovenous shunt. The nidus enhances intensely in the arterial phase — the TWIST catches it at peak enhancement before venous filling.
- **Early venous filling:** The hallmark of AVM. Direct arteriovenous shunting means veins opacify in the arterial phase, bypassing the capillary bed. This distinguishes a high-flow AVM from a low-flow venous malformation — venous malformations fill late or not at all on arterial-phase imaging.
- **Drainage pattern:** Which veins drain the AVM? Facial vein, retromandibular vein, pterygoid plexus, ophthalmic veins → cavernous sinus? Venous hypertension, varicosities, or ectasia signal a higher-risk lesion.

TWIST replaces DWI in this protocol. DWI is not useful for vascular lesions — flow voids have no meaningful diffusion signal, and the clinical question is vascular anatomy and flow dynamics, not tissue cellularity.

---

**`t1_se_fs_tra_C` (#6)**
T1 Spin Echo FS axial. Post-contrast. Matched geometry to #3/#4.

Post-contrast T1 SE with fat saturation, matched to the pre-contrast T1 (#4) for direct enhancement comparison and digital subtraction. The nidus enhances avidly. FS suppresses facial fat so the enhancing vessels are not obscured. SE preserves sharpness — the boundary between nidus and surrounding tissue needs to be crisp for surgical and embolization planning. Axial complements the coronal post-contrast (#7) by showing anteroposterior extension and transosseous involvement — AVMs can erode the maxilla or mandible, and the axial plane profiles the bone-vessel interface.

---

**`t1_tse_cor_fs_C` (#7)**
T1 TSE coronal with fat saturation. Post-contrast. Matched geometry to #1/#2.

The primary post-contrast sequence in the surgical plane. Coronal FS post-contrast shows the full extent of the enhancing nidus, feeding arteries, and draining veins for symmetric comparison. TSE is acceptable here because the question is enhancement extent, not sub-millimetre detail. FS ensures the bright enhancing vessels are not lost in the bright facial fat.

---

## 4. What Each Sequence Answers

- **AVM detection and side:** T2 coronal FS 4mm (#1) — flow voids plus asymmetry vs contralateral side.
- **Anatomical relationships:** T2 coronal non-FS (#2) — AVM relationship to muscles, parotid, orbit, and fat planes.
- **Anteroposterior extent / bone involvement:** STIR axial (#3) — relationship to maxilla, mandible, buccal space, masticator space.
- **Pre-contrast baseline / subtraction mask:** T1 SE axial (#4) — methaemoglobin, slow flow, tissue-vessel interface.
- **Arterial feeders, nidus, early venous filling:** TWIST dynamic coronal (#5) — the defining sequence for AVM vs venous malformation.
- **Enhancing nidus and draining veins (axial):** T1 SE FS axial_C (#6) — matched to #4, bone-vessel interface.
- **Enhancing nidus and draining veins (coronal):** T1 TSE coronal FS_C (#7) — surgical plane, symmetric comparison.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Forehead to below mandible on all sequences? Lesion fully included on all series? | Reposition if the superior or inferior margin of the AVM is clipped |
| **TWIST timing** — Arterial, nidus, and venous phases clearly separated? Early venous filling demonstrated? | If bolus mistimed (venous-only filling, no arterial phase visible): the TWIST is non-diagnostic. Check injection rate (3 mL/s), confirm IV patency, and repeat with adjusted delay or a test bolus |
| **TWIST slab** — Full nidus and draining veins within the slab? | If the nidus or major draining veins extend outside the slab: widen the slab (accepting lower temporal resolution) and repeat |
| **Post-contrast** — Contrast present? Nidus enhances avidly? Subtraction possible from pre-contrast T1 (#4)? | If absent: check IV line, confirm injection. If enhancement is weak or absent: reconsider diagnosis (venous malformation, lymphatic malformation, or haemangioma) |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-01 | — | Initial — 7 sequences (T2 coronal FS 4mm, T2 coronal, STIR axial, T1 SE axial, TWIST dynamic, T1 SE FS axial_C, T1 TSE coronal FS_C) |
