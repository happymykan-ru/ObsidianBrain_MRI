# fMRI (Functional MRI — Pre-Surgical Motor, Language, and Visual Mapping)

**Version:** 1.0 | **Date:** 2026-07-22 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. Head immobilization is critical — fMRI paradigms depend on sub-voxel motion stability across hundreds of dynamic EPI frames. Additional foam wedges or a vacuum cushion may be used.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].
- **Patient Preparation:** Explain all paradigms before scanning. Confirm the patient can perform each task (hand/foot tapping, language tasks). Visual stimuli require a compatible display system or mirror setup. Audio requires compatible headphones.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_space_sag_p2_iso` | Sagittal | ∥ midline | Whole brain | **None** |
| 2 | `MPR` | Cor+Ax | — | Whole brain | — |
| 3 | `gre_field_mapping` | Axial | ∥ AC-PC line | Cerebrum only | **None** |
| 4 | `ep2d_pace_moco_motor_visual` | Axial | ∥ AC-PC line | Cerebrum only | **None** |
| 5 | `ep2d_pace_moco_Rt/Lt_hand_tapping` | Axial | Copy Slice from #4 | — | **None** |
| 6 | `ep2d_pace_moco_Rt/Lt_feet_tapping` | Axial | Copy Slice from #4 | — | **None** |
| 7 | `ep2d_pace_moco_audio` | Axial | Copy Slice from #4 | — | **None** |
| 8 | `ep2d_pace_moco_lang_picture` | Axial | Copy Slice from #4 | — | **None** |
| 9 | `ep2d_pace_moco_lang_synonym` | Axial | Copy Slice from #4 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 10 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 11 | `MPR` | Sag+Ax | — | Whole brain | — |
| 12 | `ep2d_diff_sms_mddw_20_DTI_whole_brain` | Axial | Copy Slice from #4 | Foramen magnum → vertex | **None** |
| 13 | `ep2d_diff_3scan_trace_p2` | Axial | Copy Slice from #1 | — | **None** |

*Acronyms: PACE = Prospective Acquisition CorrEction (real-time motion correction). MoCo = offline motion correction. SMS = simultaneous multi-slice. MDDW = multi-direction diffusion weighted.*

*#4–#9: fMRI paradigms. Block design: 10 sequences per block, alternating B (rest) → A (movement/task). Paradigm order may be adjusted based on clinical priority. fMRI can be acquired pre- or post-contrast — contrast does not significantly affect the BOLD signal.*
*#1 (T2 SPACE) is optional if a high-resolution 3D T1 dataset (viewing wand or SRS) has already been acquired in the same session — omit to avoid redundancy.*
*EPI coverage (#3–#9) is cerebrum only. Excluding cerebellum and brainstem keeps the TR short (~2–3 s per volume) for adequate temporal sampling of the BOLD response.*

---

## 3. Sequence Rationale

### Core Strategy

Functional MRI maps eloquent cortex (motor, language, visual) by detecting BOLD signal changes during task performance. Active neurons increase local blood flow → increased oxyhaemoglobin → decreased deoxyhaemoglobin → increased T2* signal. Hundreds of EPI volumes are acquired during alternating task and rest blocks; statistical analysis identifies voxels where signal correlates with the task paradigm. The functional maps are overlaid on the 3D anatomical dataset for surgical planning.

**`t2_space_sag_p2_iso` (#1) — Conditional**
3D T2 SPACE sagittal isotropic with GRAPPA ×2. The anatomical reference dataset for fMRI overlay — isotropic voxels allow reformats in any plane (#2). Sagittal source: same rationale as surgical planning (phase-encode A/P, clean reformats). Omit if a high-resolution 3D dataset (viewing wand `t1_fl3d_sag` or SRS `t1_fl3d_sag_x-knife`) has already been acquired in the same session — the existing dataset serves as the anatomical reference and T2 SPACE is redundant.

**`MPR` (#2)**
Multiplanar reconstruction from T2 SPACE (#1). Coronal and axial anatomical views for fMRI overlay.

**`gre_field_mapping` (#3)**
GRE field map — acquired with the same geometry as the EPI sequences. EPI is sensitive to B0 inhomogeneity which causes geometric distortion (stretching and compression along the phase-encode direction). The field map measures the local B0 offset at each voxel. Post-processing uses this to unwarp the EPI images, correcting distortion before fMRI statistical analysis. Without field map correction, functional activation can be mislocalized by several millimetres — critical when mapping near the motor or language cortex for surgical planning. Coverage is cerebrum only: excluding cerebellum and brainstem keeps the TR short for good temporal BOLD sampling. The field map must match the EPI coverage exactly — same slices, same geometry.

**`ep2d_pace_moco_motor_visual` (#4)**
Motor + visual paradigm. See paradigm selection for clinical indication.

**`ep2d_pace_moco_Rt/Lt_hand_tapping` (#5)**
Hand tapping paradigm. Alternating blocks of orchid hand gesture vs rest. Single side per run (Rt = right hand → left precentral gyrus; Lt = left hand → right precentral gyrus). Instruct the patient to keep the arm, body trunk, and head still — only the hand moves.

**`ep2d_pace_moco_Rt/Lt_feet_tapping` (#6)**
Foot tapping paradigm. Alternating blocks of foot dorsiflexion/plantarflexion vs rest. Single side per run (Rt = right foot → left paracentral lobule; Lt = left foot → right paracentral lobule). Instruct the patient to keep the arm, body trunk, and head still — only the foot moves.

**`ep2d_pace_moco_audio` (#7)**
Auditory paradigm. Alternating blocks of auditory stimulus (tones, words) vs silence → superior temporal gyrus (Heschl's gyrus) activation.

**`ep2d_pace_moco_lang_picture` (#8)**
Picture naming paradigm. Alternating blocks: static cross vs pictures. The patient thinks about what each picture represents without speaking aloud — silent naming. Activates Broca's area and Wernicke's area.

**`ep2d_pace_moco_lang_synonym` (#9)**
Synonym generation paradigm. Alternating blocks of Chinese and Korean character pairs. Chinese characters: the patient thinks about whether the pair are synonyms (semantic task). Korean characters: the patient visually compares whether they are the same character (perceptual control task). Activates prefrontal cortex and semantic network.

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before post-contrast T1 (#10–#11). Contrast may be administered before or after fMRI paradigms — gadolinium does not significantly affect the BOLD signal. The order depends on workflow preference.

**`t1_vibe_fs_cor_C` (#10) + `MPR` (#11)**
Standard post-contrast brain block. Enhancing tumour margin is overlaid with the functional maps — the surgeon needs to know the distance from the enhancing margin to eloquent cortex. This is the key surgical planning output: tumour margin + functional activation maps co-registered.

**`ep2d_diff_sms_mddw_20_DTI_whole_brain` (#12)**
DTI (diffusion tensor imaging) with 20 directions, simultaneous multi-slice (SMS), and whole-brain coverage. DTI maps white matter tract orientation — tractography reconstructs the corticospinal tract, arcuate fasciculus, and optic radiation. With fMRI mapping cortical function and DTI mapping white matter connectivity, the surgeon knows both the eloquent cortex location AND the fibre tracts connecting it. SMS (simultaneous multi-slice) accelerates the acquisition by exciting multiple slices simultaneously and unaliasing them with coil sensitivity — a 20-direction DTI with SMS is acquired in a clinically feasible time. Post-contrast placement is acceptable: gadolinium does not significantly affect diffusion signal, and DTI after contrast uses the post-injection delay efficiently.

**`ep2d_diff_3scan_trace_p2` (#13)**
Standard 3-scan trace DWI with GRAPPA ×2. Acute ischaemia, cellular tumour components. DTI (#12) is optimized for directional information (tractography), not for diagnostic diffusion contrast — the 20-direction acquisition has lower SNR per direction and a noisier ADC map. The 3-scan trace is faster, higher SNR, and produces a clean ADC map for detecting restricted diffusion. Both are needed: DTI maps the white matter tracts the surgeon must avoid; the trace DWI detects acute ischaemia and cellular tumour that the DTI may miss.

---

## 4. Paradigm Selection by Clinical Indication

Not all paradigms are needed for every patient. The choice depends on tumour location and which eloquent cortex is at risk:

- **Motor + visual (#4):** Visual mapping for occipital tumours, posterior temporal tumours (near Meyer's loop / optic radiation), or parietal tumours near the dorsal visual stream. The motor component may be redundant if separate hand (#5) and foot (#6) paradigms are already planned — #4 is primarily a visual paradigm. Omit if the tumour is distant from visual pathways and hand/foot paradigms already cover motor mapping.

- **Hand tapping (#5):** Tumour near the hand knob of the precentral gyrus (frontal/parietal convexity). The hand motor area is the most critical for surgical planning — distance from the tumour margin to hand motor activation determines resectability. Right and left hand are separate runs; each maps the contralateral hemisphere.

- **Foot tapping (#6):** Tumour near the paracentral lobule (parasagittal/falcine, medial frontal). The leg representation sits in the interhemispheric fissure and is vulnerable during interhemispheric surgical approaches. Right and left foot are separate runs.

- **Audio (#7):** Temporal lobe tumour near Heschl's gyrus or the superior temporal gyrus. Needed when the superior temporal gyrus is within or adjacent to the surgical corridor.

- **Language — picture naming (#8):** Dominant hemisphere tumour near Broca's area (inferior frontal gyrus) or Wernicke's area (superior temporal gyrus). Picture naming maps expressive language; it is the most robust language paradigm and should be included whenever language mapping is requested.

- **Language — synonym generation (#9):** Adds higher-order semantic processing areas (prefrontal, semantic network). Typically requested when the tumour is in the dominant frontal or temporal lobe and comprehensive language mapping is needed. Complements picture naming — together they cover both expressive and receptive language networks.

The radiologist selects the relevant paradigms based on tumour location. Omit paradigms that map cortex distant from the surgical target — unnecessary paradigms add scan time without clinical benefit.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Patient preparation** — all paradigms explained? Patient can perform tasks? | Demonstrate hand/foot tapping and language tasks before positioning. Confirm visual display/audio are working |
| **`gre_field_mapping` (#3)** — same geometry as EPI (#4–#9)? | Field map must match EPI slices exactly. If EPI slices are changed, re-acquire the field map |
| **fMRI paradigms (#4–#9)** — PACE active? Motion within acceptable limits? | PACE corrects small movements in real time. If the patient moved significantly during a paradigm: re-acquire that paradigm only |
| **fMRI paradigms (#4–#9)** — stimulus working? | Check in real time using the Neuro3D workflow time course evaluation. Confirm activation in the expected cortical region during task blocks |
| **Post-contrast** — contrast present? Confirm tumour enhancement | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-22 | — | Initial — 13 sequences (7 fMRI paradigms + DTI + standard brain) |
