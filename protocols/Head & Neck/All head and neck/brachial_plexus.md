# Brachial Plexus (Brachial Plexus MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-02 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil + anterior body coil + spine array. The brachial plexus extends from C1 to the manubrium — the head and neck coil covers the cervical portion; the body coils cover the thoracic inlet and supraclavicular fossa inferiorly.
- **Laser Landmark:** Sternal notch — palpable, sits at ~T2 level, the inferior extent of the plexus. Centring here positions the stack from C1 superiorly to the manubrium inferiorly.
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions. Breathing moves the chest wall and lung apex — the thoracic inlet portion of the plexus is respiratory-motion-sensitive.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tirm_cor` | Coronal | No tilting | A/P: touching manubrium → posterior skin margin. FOV: C1 → manubrium (~T4/T5), both plexuses | **None** |
| 2 | `t1_tse_dixon_cor` | Coronal | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dixon_tra` | Axial | ∥ C-spine (or true axial). Separate R/L | S/I: C3 → T1/T2. FOV: covering plexus in-plane | **None** |
| 4 | `t1_tse_tra` | Axial | Copy Slice from #3. Separate R/L | — | **None** |
| 5 | `t2_tse_3mm_dixon_sag` | Sagittal (true) | ∥ C-spine. Separate R/L | L/R: midline → shoulder joint | **None** |
| — | **Contrast** | — | — | — | — |
| 6 | `t1_tse_dixon_cor_C` | Coronal | Copy Slice from #1 | — | **None** |
| 7 | `t1_tse_dixon_tra_C` | Axial | Copy Slice from #3. Separate R/L | — | **None** |

*Axials and sagittals are prescribed separately for left and right.*
*Dixon is used on all T1 and T2 axial/sagittal sequences — the brachial plexus crosses the thoracic inlet where the lung apex creates severe B0 inhomogeneity. Dixon's water/fat/in/opposed-phase decomposition is immune to this; chemical FS would fail at the lung apex and supraclavicular regions.*
*Fast Dixon: used to keep total scan time manageable given the long craniocaudal coverage and multi-sequence protocol. See rationale for trade-offs.*
*#6, #7: No post-contrast sagittal — post-contrast assessment is in the coronal (overview, both sides) and axial (nerve roots, individual side) planes.*

---

## 3. Sequence Rationale

### Core Strategy

Brachial plexus imaging addresses three clinical questions: (1) Is there a compressive lesion (thoracic outlet syndrome, cervical rib, Pancoast tumour)? (2) Is there intrinsic plexus pathology (trauma — pre- or post-ganglionic, inflammation, tumour — neurofibroma, schwannoma, metastasis)? (3) What is the level and severity of nerve involvement? The protocol covers C1 to the manubrium, spanning the roots (neural foramina), trunks (interscalene triangle), divisions (behind the clavicle), cords, and proximal peripheral nerves.

Unlike the salivary glands or TMJ protocols, there is no single key sequence — the diagnosis rests on symmetry: comparing left to right across all three planes. Asymmetric T2 hyperintensity, enlargement, or enhancement of a nerve root or trunk is pathological.

---

**`t2_tirm_cor` (#1)**
T2 TIRM (STIR) true coronal, both sides. TIRM provides uniform fat suppression across the cervical spine, thoracic inlet, and lung apices — a region where chemical FS consistently fails due to the abrupt air-soft tissue interface at the lung apex.

The coronal plane profiles the entire plexus from roots to proximal cords in one view:
- **Nerve roots** — exiting the neural foramina at C4/C5 through T1/T2. The roots angle inferolaterally from the cord toward the interscalene triangle.
- **Trunks** — upper (C5–C6), middle (C7), lower (C8–T1). Formed in the interscalene triangle between anterior and middle scalene muscles. The lower trunk sits at the thoracic inlet near the lung apex.
- **Divisions** — behind the clavicle. Anterior divisions supply flexor compartments; posterior divisions supply extensor compartments.
- **Symmetry** — both plexuses on one image. Asymmetric T2 hyperintensity of any component is the primary finding in plexitis, compression, or radiation injury.

TIRM is sequenced first — it is the screening sequence. The radiologist looks for T2 signal abnormality and then uses the higher-resolution axial and sagittal sequences to characterize the finding.

**Coverage:** A/P: touching the manubrium and sternum anteriorly, extending posteriorly to the posterior skin margin to include all nerve roots exiting the neural foramina. The manubrium is the anterior boundary of the thoracic inlet — the divisions and cords pass through the costoclavicular space behind the clavicle and manubrium. If the anterior edge does not reach the manubrium, these structures are clipped. FOV: C1 → manubrium (~T4/T5), both plexuses in a single acquisition.

---

**`t1_tse_dixon_cor` (#2)**
T1 TSE Dixon true coronal, both sides. Pre-contrast. Dixon provides water-only, fat-only, in-phase, and opposed-phase images from one acquisition — each with a different diagnostic role:

- **Water-only:** T1-weighted with uniform fat suppression — anatomical reference with high in-plane resolution. The nerve roots, trunks, and divisions are intermediate signal against dark fat. This is the primary coronal image for morphology and size comparison.
- **In/opposed phase:** The opposed-phase image detects microscopic fat within tissues. A nerve root that drops signal on opposed phase contains fat — normal variant or chronic atrophy. A nerve that does not drop signal is pathological (no intracellular lipid).
- **Fat-only:** The background fat distribution — useful for identifying fatty atrophy of surrounding muscles (chronic denervation).

**Coverage:** Matches #1.

---

**`t2_tse_dixon_tra` (#3, R/L)**
T2 TSE Dixon axial, separate left and right. High in-plane resolution for individual nerve root assessment.

The axial plane profiles each component of the plexus in cross-section:
- **Roots** — within the neural foramina, surrounded by CSF and epidural fat. The dorsal root ganglion (DRG) sits in the foramen and is slightly T2-hyperintense normally — do not mistake for pathology.
- **Interscalene triangle** — anterior scalene (medial) and middle scalene (posterior) form a V-shaped space. The trunks pass through this space; scalene hypertrophy or fibrous bands cause thoracic outlet syndrome.
- **Costoclavicular space** — divisions pass between the clavicle (anterior) and first rib (posterior). A cervical rib or fibrous band extending from C7 to the first rib compresses the lower trunk here.
- **Subclavian vessels** — the subclavian artery and vein accompany the plexus divisions and cords. A Pancoast tumour (superior sulcus lung cancer) invades the lower trunk and subclavian vessels at the thoracic inlet.

**Coverage:** S/I: C3 → T1/T2. FOV: covering the plexus in-plane. The axial stack can be true axial or tilted to match the neck angulation — whichever gives a cleaner cross-section of the neural foramina. Separate R/L.

---

**`t1_tse_tra` (#4, R/L)**
T1 TSE axial, separate left and right. Pre-contrast. Matched geometry to #3 for enhancement comparison.

T1 axial provides the anatomical baseline: nerve size, morphology, and the surrounding fat planes. The plexus nerves are intermediate signal against bright epidural and foraminal fat — a T1-dark, enlarged nerve root is conspicuous even without contrast. This is the pre-contrast reference for post-contrast Dixon axial (#7).

**Coverage:** Matches #3. Separate R/L.

---

**`t2_tse_3mm_dixon_sag` (#5, R/L)**
T2 TSE Dixon sagittal, 3 mm. True sagittal. Separate left and right.

The sagittal plane profiles the nerve roots as they exit the neural foramina. The stack extends from midline (roots at cord origin) to the shoulder joint laterally (trunks transitioning to divisions). Medial slices show the rootlets and root origin from the cord; intermediate slices show the roots in the foramina; lateral slices show the trunks in the interscalene triangle and the divisions/cords in the supraclavicular fossa.

3 mm slices — thinner than typical head & neck axial — provide detailed foraminal assessment. At each foramen, the dorsal and ventral rootlets merge to form the spinal nerve, which immediately divides into dorsal and ventral rami. The ventral rami form the plexus — sagittal slices at the foramen show this origin.

Dixon provides water-only (fat-suppressed T2) for nerve signal without B0 failure at the foramen (bone-air interface at the uncovertebral joint and facet).

**Coverage:** Midline → shoulder joint laterally. L/R: midline → shoulder joint. Separate R/L.

---

**Contrast**
Standard dose IV gadolinium. Post-contrast sequences immediately follow. Enhancement of a nerve root or trunk is pathological — normal peripheral nerves do not enhance (the blood-nerve barrier prevents contrast extravasation). Enhancement indicates inflammation (plexitis), tumour infiltration, or post-ganglionic injury with Wallerian degeneration.

---

**`t1_tse_dixon_cor_C` (#6)**
T1 TSE Dixon true coronal, both sides. Post-contrast. Matched geometry to pre-contrast Dixon coronal (#2).

Enhancing nerve roots, trunks, or cords are directly compared side-to-side. Symmetric thin linear enhancement along nerve roots may be physiological (dorsal root ganglia enhance normally — fenestrated capillaries). Asymmetric, nodular, or mass-like enhancement is pathological.

Water-only (fat-suppressed) is the primary post-contrast image — enhancing nerve against dark fat.

---

**`t1_tse_dixon_tra_C` (#7, R/L)**
T1 TSE Dixon axial, separate left and right. Post-contrast. Matched geometry to pre-contrast T1 axial (#4).

The axial plane confirms enhancement at the foraminal level (root/DRG), interscalene triangle (trunk), and costoclavicular space (division/cord). An enhancing, enlarged nerve root in the foramen with associated T2 hyperintensity on #3 is the hallmark of inflammatory plexitis. Separate R/L allows high in-plane resolution for small structures.

No post-contrast sagittal — the coronal provides the overview and the axial provides the cross-sectional detail. Adding a post-contrast sagittal would prolong the exam without adding anatomical information not already present in the other two planes.

---

### Fast Dixon — Trade-offs

Fast Dixon keeps total scan time manageable given the long craniocaudal coverage and multi-sequence protocol. The trade-offs:

- **SNR:** Faster acquisition (higher parallel imaging factor, fewer averages) → lower SNR. In the brachial plexus, this matters at the thoracic inlet where the lung apex provides no signal — the nerves sit against a dark background and need sufficient SNR to be distinguished from surrounding fat.
- **TSE blurring:** Higher turbo factor → more echoes in the train → the later, lower-signal echoes blur fine edges. Nerve roots are 1–2 mm structures; excessive blurring can obscure the margin between nerve and surrounding fat, mimicking or hiding oedema.

In practice: accept the speed benefit because the alternative — slow Dixon with motion artefact from breathing — is worse than a slightly noisier but motion-free image. The TIRM (#1) serves as the robust fat-suppressed reference against which the Dixon images are checked.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Coronal: C1 → manubrium, touching manubrium anteriorly? Axial: C3 → T1/T2? Sagittal: midline → shoulder joint? | Reposition if coverage clipped. The lower trunk (C8–T1) at the thoracic inlet is the most common site of pathology — if the inferior boundary is too high, this is missed |
| **Symmetry** — Left and right plexuses symmetric in size, signal, and enhancement on coronal? | Asymmetry is the primary diagnostic finding. If asymmetric: check that the coronal is true coronal (not slightly oblique, which can make one side appear larger) |
| **Fat suppression** — Water-fat swap on Dixon at the thoracic inlet? Check that nerve roots are visible on water-only and not artefactually dark | If a nerve root visible on TIRM (#1) is missing on Dixon water-only: swap artefact — the signal was misassigned to the fat channel. Use TIRM as the reference. Confirm on the Dixon in-phase image (swap does not affect in-phase)
| **Motion** — Breathing artefact across the thoracic inlet on axial and coronal? | The lung apex moves with respiration — ghosting along the phase-encode direction. If severe: repeat with a breath-hold acquisition if the patient can tolerate it. Fast Dixon helps but does not eliminate respiratory motion |
| **Post-contrast** — Contrast present? Check enhancing structures: dorsal root ganglia enhance normally (fenestrated capillaries). | If absent: check IV line, confirm injection. DRG enhancement is physiological — do not mistake for pathology. Asymmetric nerve root or trunk enhancement is pathological |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-02 | — | Initial — 7 sequences (TIRM, fast Dixon throughout, coronal/axial/sagittal, separate R/L axials and sagittals) |
