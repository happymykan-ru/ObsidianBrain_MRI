# PNS (Paranasal Sinuses MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-01 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil
- **Laser Landmark:** Nasion
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions. Swallow-related motion is less problematic in the paranasal sinuses than in the nasopharynx/oropharynx (sinuses are anterior and relatively immobile), but still degrades the post-contrast sequences.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_cor_PNS` | Coronal | ⟂ hard palate | Frontal sinus → maxillary floor. A/P: nasal soft tissue → sphenoid sinus | **None** |
| 2 | `t2_stir_tra` | Axial | ∥ hard palate | Frontal sinus → hard palate. Centre on paranasal sinuses | **None** |
| 3 | `t1_se_tra` | Axial | Copy Slice from #2 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 4 | `resolve_4scan_trace_tra_PNS` | Axial | Copy Slice from #2 | — | **None** |
| 5 | `t1_vibe_fs_tra_PNS_C` | Axial | Copy Slice from #2 | — | **None** |
| 6 | `t1_tse_r_cor_PNS_fs_C` | Coronal | Copy Slice from #1 | — | **None** |

*#4: RESOLVE DWI fills the post-contrast delay. Target ~3–5 min before post-contrast T1 (#5, #6).*

---

## 3. Sequence Rationale

### Core Strategy

Paranasal sinus imaging sits at the intersection of inflammatory disease and tumour assessment. The primary clinical questions are: (1) is the ostiomeatal complex (OMC) patent, and are there anatomical variants that complicate FESS? (2) Is there bone erosion suggesting tumour, fungal disease, or complicated sinusitis? (3) Is there orbital or intracranial extension? The protocol is built around the **coronal plane as primary** — the surgical view for endoscopic sinus surgery — and prioritises bone detail (T1 SE, not TSE) and uniform fat suppression in a hostile B0 environment (STIR, not chemical FS, for the pre-contrast axial). Unlike NP and oral cavity protocols, motion-robust radial acquisitions (StarVIBE) are not required because the paranasal sinuses are anterior and relatively immobile; TSE coronally gives crisper bone and dural detail. There is no dedicated lower neck sequence — nodal staging is not the primary concern. Perineural spread in PNS tumours follows V2 (infraorbital nerve → pterygopalatine fossa → foramen rotundum) and the olfactory nerves (through the cribriform plate), not V3/vidian nerve toward the vertex.

---

**`t2_tse_cor_PNS` (#1)**
T2 TSE coronal without fat saturation. The coronal plane is the **primary diagnostic plane** for paranasal sinus imaging. The ostiomeatal complex — the common drainage pathway of the maxillary, anterior ethmoid, and frontal sinuses — is oriented coronally. Every key structure falls naturally into a single coronal slice: the uncinate process, infundibulum, hiatus semilunaris, middle meatus, ethmoid bulla, and the frontal recess. This is also the surgical view for FESS (functional endoscopic sinus surgery) — what the radiologist reports coronally maps directly to what the surgeon sees through the endoscope.

No fat saturation: natural contrast between mucosal thickening (bright T2), air (dark), bone (dark), and orbital fat (bright) is preserved. Chemical FS would suppress orbital fat and make the medial orbital wall (lamina papyracea) harder to delineate — precisely where orbital complications of sinusitis must be assessed.

**Coverage:** Frontal sinus (superior) → floor of maxillary sinus (inferior). Anterior: nasal bone and soft tissue. Posterior: sphenoid sinus. The frontal recess and sphenoethmoidal recess must both be fully visualised — these are the drainage pathways for the frontal and posterior ethmoid/sphenoid sinuses respectively.

*Plane:* **Coronal** is sequenced first because it answers the primary clinical question (OMC patency, FESS anatomy) and guides interpretation of the axial stack.

---

**`t2_stir_tra` (#2)**
T2 STIR axial. STIR (Short Tau Inversion Recovery) is chosen over chemical fat saturation because the paranasal sinuses are a **worst-case B0 environment**: the ethmoid air cells, sphenoid sinus, frontal recess, and mastoids create multiple air-bone interfaces that shatter field homogeneity. Chemical fat sat fails patchily adjacent to these interfaces — precisely where mucosal disease sits. STIR, being inversion-recovery-based, is immune to B0 inhomogeneity and gives uniform fat suppression across the entire sinus field.

**Coverage:** Frontal sinus (superior) → hard palate (inferior), centred on the paranasal sinuses. The axial plane is complementary to the coronal: it profiles the maxillary sinus anterior/posterior walls, the pterygopalatine fossa (key conduit for perineural spread along V2), the nasopharynx and Eustachian tube orifices, and the sphenoid sinus relationship to the cavernous sinus laterally.

---

**`t1_se_tra` (#3)**
T1 **Spin Echo** (SE, not TSE!) axial. Pre-contrast. Matched geometry to #2 for direct enhancement comparison post-contrast.

The distinction between SE and TSE matters here more than in NP or oral cavity. The paranasal sinuses are defined by thin bony walls — the lamina papyracea (~0.2–0.4 mm), cribriform plate, fovea ethmoidalis, and the walls of the sphenoid sinus. TSE introduces turbo-factor-related blurring: later echoes in the echo train are acquired with reduced signal, blurring fine edges in the final image. A conventional SE has no turbo factor — each TR fills a single k-space line at the same TE, giving a sharper point spread function. Early bone erosion, dehiscence of the lamina papyracea, or a subtle breach of the cribriform plate can be the difference between sinusitis confined to the sinus and disease that has entered the orbit or anterior cranial fossa.

Pre-contrast T1 SE also provides the bone marrow signal baseline — marrow replacement in the clivus, skull base, or pterygoid plates by tumour will be assessed against this.

---

**Contrast**
Standard dose IV gadolinium. DWI (#4) fills the post-injection delay. Target ~3–5 min before post-contrast T1 (#5, #6).

---

**`resolve_4scan_trace_tra_PNS` (#4)**
RESOLVE DWI, 4-scan trace. Acquired post-contrast during the enhancement delay.

The key diagnostic question DWI answers in PNS imaging: **is this a solid tumour or inspissated (thickened) secretions / a mucocele?** Paranasal sinus pathology often presents as an opacified sinus on CT, and the distinction on T2 alone can be ambiguous:

- **Inspissated secretions / mucocele:** T2-dark (proteinaceous content), no restricted diffusion. The proteinaceous contents of a mucocele may actually show facilitated diffusion (ADC bright) — the water mobility in these chronic collections can be higher than expected.
- **Solid tumour (SCC, adenocarcinoma, inverted papilloma, lymphoma, esthesioneuroblastoma):** Cellular, restricted diffusion (ADC dark). Inverted papilloma is particularly important — it's a benign but locally aggressive tumour with malignant potential that requires complete surgical excision. DWI helps distinguish it from inflammatory polyps pre-operatively.
- **Fungal sinusitis (allergic fungal rhinosinusitis):** T2-very-dark due to paramagnetic fungal metabolites (iron, manganese, calcium). DWI adds little diagnostically — the T2 signal void is the characteristic finding. On post-contrast T1, the inflamed mucosa enhances but the fungal material centrally does not.

RESOLVE (readout-segmented EPI) is essential: the skull base and paranasal sinuses produce severe susceptibility distortion on single-shot EPI. The petrous bone, sphenoid, ethmoid air cells, and frontal sinus floor create multiple air-bone interfaces. RESOLVE's segmented k-space readout reduces phase-encode errors at each interface. 4-scan trace gives more isotropic diffusion weighting than 3-scan, reducing directional bias in an anatomically complex region.

---

**`t1_vibe_fs_tra_PNS_C` (#5)**
T1 VIBE FS axial post-contrast. Matched geometry to #2/#3.

Post-contrast axial with fat saturation. The enhancing pattern distinguishes pathology: inflamed mucosa enhances physiologically (linear, thin); mucocele content does not enhance; solid tumour enhances variably. VIBE (volumetric interpolated breath-hold examination) is a 3D gradient echo — thin contiguous slices allow multiplanar viewing of the enhancing margins.

**Coverage & anatomical questions answered:**
- **Pterygopalatine fossa:** Enhancing tissue replacing the normal fat pad → perineural spread along V2 (maxillary nerve), which courses from the infraorbital nerve through the pterygopalatine fossa to foramen rotundum and Meckel's cave.
- **Orbital invasion:** Enhancement breaching the lamina papyracea → orbital complication (subperiosteal abscess, orbital cellulitis). The medial rectus and optic nerve must be assessed.
- **Intracranial extension:** Enhancement crossing the cribriform plate or fovea ethmoidalis → anterior cranial fossa involvement. The olfactory bulbs and gyrus rectus are the first intracranial structures encountered.
- **Cavernous sinus:** Enhancing tissue lateral to the sphenoid sinus → cavernous sinus extension (urgent — cranial nerves III, IV, V1, V2, VI are at risk).

VIBE (gradient echo) is acceptable for the axial plane here because the axial plane cuts through fewer air-bone interfaces than the coronal; susceptibility artefact is less problematic axially. For the coronal plane (#6), TSE is used specifically because the coronal slice through the ethmoid roof is susceptibility-sensitive.

---

**`t1_tse_r_cor_PNS_fs_C` (#6)**
T1 **TSE** coronal with fat saturation. Post-contrast. Matched geometry to #1.

This is the sequence the ENT surgeon studies most closely — the coronal plane is the surgical view. TSE (not VIBE) is used coronally, and this is a deliberate choice unique to PNS among the head and neck protocols:

- **Less susceptibility at air-bone interfaces:** The coronal plane through the paranasal sinuses cuts through the ethmoid roof, sphenoid roof, and frontal recess — all air-bone interfaces. TSE is inherently less susceptible to field distortions than gradient echo: VIBE has no 180° refocusing pulse, so susceptibility-related dephasing accumulates. At 3T especially, VIBE through the ethmoid roof can show signal dropout that mimics or obscures the cribriform plate — the very structure most critical for detecting intracranial spread.
- **Better dural enhancement depiction:** The thin line of physiological or pathological dural enhancement above the cribriform plate and planum sphenoidale is crisper on TSE. On VIBE, blooming from the adjacent frontal lobe parenchyma and bone can blur this critical interface. A subtle dural tail of enhancement can be the only sign of early intracranial extension.
- **Less motion-sensitive anatomy:** The paranasal sinuses are anterior and relatively immobile — swallowing moves the pharyngeal wall but does not significantly displace the sinuses. TSE is more motion-sensitive than StarVIBE's radial acquisition, but the sinuses are in a quiet zone. This is why StarVIBE is used for NP and oral cavity (the nasopharynx and oropharynx move with every swallow) but TSE is preferred for PNS.

FS confirms enhancing tumour against suppressed orbital, mucosal, and subcutaneous fat.

**Coverage:** Matches #1 — frontal sinus → maxillary floor. Anterior nasal soft tissue to posterior sphenoid sinus. The fovea ethmoidalis (ethmoid roof — the thinnest part of the anterior skull base) and cribriform plate must fall within the stack. These are the sites of early intracranial extension and iatrogenic injury during FESS.

---

## 4. What Each Sequence Answers

- **OMC patency and FESS anatomy:** T2 coronal (#1) — uncinate process attachment, infundibulum width, Haller cells, concha bullosa, paradoxical middle turbinate, sphenoethmoidal (Onodi) cell relationship to optic nerve. These variants change the surgical approach.
- **Bone erosion:** T1 SE axial (#3) — sharp bone detail without TSE blurring. Compare marrow signal to post-contrast T1_C (#5, #6).
- **Solid tumour vs inspissated secretions:** DWI (#4) — restricted diffusion favours tumour. The enhancing pattern on post-contrast T1_C (#5, #6) confirms: tumour enhances; mucocele content does not.
- **Orbital extension:** T2 coronal (#1) and T1 TSE coronal FS_C (#6) — lamina papyracea integrity, subperiosteal abscess, medial rectus displacement, optic nerve compression.
- **Intracranial extension:** T1 TSE coronal FS_C (#6) — dural enhancement above the cribriform plate/fovea ethmoidalis. Axial VIBE_C (#5) confirms. T2 coronal (#1) shows the pre-contrast anatomy.
- **Perineural spread (V2):** Axial STIR (#2) and T1 VIBE FS axial_C (#5) — fat replacement and enhancement in the pterygopalatine fossa, foramen rotundum, and cavernous sinus.
- **Fungal sinusitis:** T2 coronal (#1) and STIR (#2) — T2 signal void from paramagnetic fungal metabolites (iron, manganese, calcium). Post-contrast T1_C (#5, #6) — enhancing inflamed mucosa surrounding non-enhancing fungal material.

---

## 5. Comparison with NP and Oral Cavity Protocols

Paranasal sinuses, nasopharynx, and oral cavity are all head and neck subsites imaged with contrast — but the anatomy, clinical question, and surgical approach differ, and the protocols reflect this.

1. **PNS is anatomical/surgical, NP and oral cavity are oncological.** PNS protocol is built for FESS planning and local disease characterisation — the coronal plane comes first because that's the surgical view. NP and oral cavity protocols are built for tumour staging with wide coverage and nodal mapping.

2. **Motion profile dictates technique.** The nasopharynx and oropharynx swallow — StarVIBE is essential. The paranasal sinuses are anterior and relatively stationary — TSE works well, and its lower susceptibility at air-bone interfaces is an advantage.

3. **Bone detail matters more in PNS.** The lamina papyracea, cribriform plate, and fovea ethmoidalis are sub-millimetre structures. T1 SE (not TSE) preserves edge sharpness for detecting early erosion. In NP and oral cavity, soft tissue contrast is the priority and TSE blurring at bone edges is acceptable.

4. **DWI answers a different question.** PNS: tumour vs inspissated secretions (is this opacified sinus a mucocele or a tumour?). NP/oral cavity: tumour cellularity and nodal characterisation (SCC and NPC are both ADC-dark). The question is fundamentally different.

5. **Perineural spread follows different nerves.** NPC tracks V3 and vidian nerve to the vertex (vertex coverage crucial). PNS tumours track V2 through the pterygopalatine fossa to foramen rotundum (axial plane profiles this). Oral cavity tumours track lingual and inferior alveolar nerves inferiorly toward the mandible (no vertex needed).

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Frontal sinus to maxillary floor on all sequences? Frontal recess and sphenoethmoidal recess fully included on coronal (#1, #6)? | Reposition if frontal recess clipped (FESS planning incomplete). Extend stack inferiorly if maxillary floor cut off |
| **Bone** — Lamina papyracea, cribriform plate, fovea ethmoidalis sharply defined on T1 SE (#3)? | T1 SE is the only SE sequence in any head/neck protocol — confirm it was prescribed as SE, not TSE. If TSE was used erroneously, re-acquire with SE. Check bone windows on post-contrast T1 coronal (#6) |
| **Post-contrast** — Contrast present? Mucosal enhancement (linear, thin) confirmed? Any enhancing solid component? | If absent: check IV line, confirm injection. Physiological mucosa enhances — its absence suggests no contrast.

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-01 | — | Initial — 6 sequences (T2 coronal, STIR axial, T1 SE axial, RESOLVE DWI, T1 VIBE FS axial, T1 TSE coronal FS) |
