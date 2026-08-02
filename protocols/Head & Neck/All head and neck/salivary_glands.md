# Salivary Glands (Salivary Gland MRI with Contrast and DCE)

**Version:** 1.0 | **Date:** 2026-08-02 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil
- **Laser Landmark:** Angle of mandible
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions. Swallowing moves the parotid and submandibular region — this is the motion-sensitive zone. During the DCE acquisition, the patient must remain completely still — any movement displaces the gland and contaminates the time-intensity curve with signal from different tissue at each time point.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_cor_fs` | Coronal | ⟂ hard palate | See coverage note below | **None** |
| 2 | `t2_tse_cor` | Coronal | Copy Slice from #1 | — | **None** |
| 3 | `t2_stir_tra` | Axial | ∥ hard palate | See coverage note below | **None** |
| 4 | `t1_se_tra` | Axial | Copy Slice from #3 | — | **None** |
| 5 | `resolve_4scan_trace_tra` | Axial | Copy Slice from #3 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 6 | `t1_vibe_tra_dyn_C` | Axial | Copy Slice from #3 | — (covers whole parotid) | **None** |
| 7 | `t1_vibe_fs_tra_C` | Axial | Copy Slice from #3 | — | **None** |
| 8 | `t1_starvibe_fs_cor_C` | Coronal | Copy Slice from #1 | — | **None** |
| 9 | `MPR` | Sag+Ax | — | Whole volume | — |

*#6: DCE acquisition covers the whole parotid gland. A single slice through the most enhancing portion of the lesion is selected retrospectively for mean curve plotting. Off normalization — raw signal intensity displayed. 

### Workflow: Coronal First → Axial Coverage

The coronal sequences (#1, #2) are acquired **first**. From the coronal images, the parotid gland is directly visualised and the exact axial coverage is determined — the axial stack is prescribed to cover the full craniocaudal extent of the parotid as seen on the coronal. This ensures the parotid tail is not clipped, which can happen when axial coverage is prescribed from a midline sagittal scout alone (the parotid is a lateral structure and its inferior extent is underestimated on a midline view).

### Coronal Coverage (#1, #2, #8)

| Boundary | Landmark |
|----------|----------|
| **Posterior** | Back of ear (retroauricular / mastoid) |
| **Anterior** | Symphysis menti (chin) |
| **Superior–Inferior** | Full parotid + submandibular region |

### Axial Coverage (#3, #4, #5, #7) — Two Options

Axial coverage is set from the coronal images. Choose **one** option based on clinical indication and apply to all axial sequences.

**Option A — Parotid-Only Lesions**

| Boundary | Landmark |
|----------|----------|
| **Superior** | Zygomatic arch |
| **Inferior** | Angle of mandible (~C2) |
| **Anterior** | Anterior border of mandibular ramus |
| **Posterior** | Mastoid tip / sternocleidomastoid |
| **Centre** | External auditory canal (tragus) |

Used for: known parotid tumour (pleomorphic adenoma, Warthin tumour, suspected parotid malignancy), parotid lump of unknown aetiology. The submandibular and sublingual glands are excluded.

**Option B — All Salivary Glands (Parotid + Submandibular + Sublingual)**

| Boundary | Landmark |
|----------|----------|
| **Superior** | Zygomatic arch |
| **Inferior** | Hyoid bone (~C3) |
| **Anterior** | Symphysis menti (chin) |
| **Posterior** | Mastoid tip / sternocleidomastoid |
| **Centre** | Angle of mandible |

Used for: suspected sialadenitis, sialolithiasis (stone), Sjögren's syndrome, bilateral salivary gland disease, or when the primary gland of concern is unclear. The submandibular gland and floor of mouth (sublingual glands) are fully included.

---

## 3. Sequence Rationale

### Core Strategy

Salivary gland imaging centres on **tumour characterization**. The primary clinical question is: what is this parotid lump? The differential of a parotid mass — pleomorphic adenoma, Warthin tumour, or malignancy (mucoepidermoid carcinoma, adenoid cystic carcinoma, adenocarcinoma, lymphoma, metastases) — drives treatment from surveillance to surgical excision to neck dissection. DCE (dynamic contrast enhancement) is the key discriminating sequence: the time-intensity curve pattern differentiates benign from malignant with high accuracy when combined with T2 signal and morphology. No other head and neck protocol uses DCE.

---

**`t2_tse_cor_fs` (#1)**
T2 TSE coronal with fat saturation. The coronal plane profiles the parotid — the gland drapes over the mandible and extends inferiorly as the tail, best seen coronally. The bilateral parotid glands, submandibular glands, and cervical nodal chains appear in symmetric comparison on a single coronal slice.

Fat saturation is essential: the parotid is a fat-containing encapsulated gland. Normal parotid parenchyma is T1-bright (fatty) and T2-intermediate. On T2 FS, the fatty background is suppressed and any T2-hyperintense lesion stands out against the dark gland. A pleomorphic adenoma, with its abundant myxoid/chondroid stroma, is brightly T2-hyperintense — the FS makes this unmistakable.

---

**`t2_tse_cor` (#2)**
T2 TSE coronal without fat saturation. Paired with #1 for complementary contrast — identical geometry, different tissue weighting.

The non-fat-sat T2 preserves natural tissue planes that FS suppresses:
- **Parotid capsule** — The thin fibrous capsule separating parotid tissue from surrounding fat. On FS, the capsule and adjacent fat are both dark and indistinguishable. On non-FS, the dark capsule stands out against bright fat.
- **Facial nerve plane** — The facial nerve (CN VII) divides the parotid into superficial and deep lobes as it passes through the gland. The nerve itself is not directly visible on T2, but the fat plane between the superficial and deep lobes is seen on non-FS. A tumour in the superficial lobe can be excised via superficial parotidectomy with facial nerve preservation; a deep lobe tumour requires total parotidectomy with nerve mobilisation. The surgeon needs the non-FS T2 coronal to plan this approach.
- **Tumour-muscle interface** — The deep lobe abuts the medial pterygoid, masseter, and parapharyngeal space, separated by a thin fat plane. On FS, this fat plane is suppressed — parotid parenchyma (fatty, now dark) and the adjacent muscle (intermediate signal) lose their natural boundary, making it harder to assess whether tumour has breached the parotid capsule into the masticator space. Non-FS preserves the bright fat plane between gland and muscle for clear margin assessment.

---

**`t2_stir_tra` (#3)**
T2 STIR axial. STIR (Short Tau Inversion Recovery) is chosen over chemical fat saturation because the parotid and submandibular region sits adjacent to the mandible, mastoid tip, and oral cavity air — multiple air-bone-soft tissue interfaces. Chemical FS fails patchily at these interfaces; STIR, being inversion-recovery-based, is immune to B0 inhomogeneity and provides uniform fat suppression.

The axial plane profiles:
- **Deep lobe of parotid** — The parotid wraps around the posterior mandible; the deep lobe extends medially through the stylomandibular tunnel into the parapharyngeal space. A deep lobe tumour can present as a parapharyngeal mass rather than a parotid lump — the axial plane shows this medial extension.
- **Facial nerve plane (retromandibular)** — On axial, the facial nerve plane runs lateral to the retromandibular vein. A tumour lateral to the vein is superficial lobe; medial is deep lobe. This surgical distinction is best assessed axially.
- **Submandibular gland** — Profiled axially at the floor of mouth level, posterior to the mylohyoid muscle.
- **Parapharyngeal fat** — Displacement (not invasion) by a deep lobe parotid tumour confirms parotid origin rather than a primary parapharyngeal tumour.

Non-tumour pathology also assessed on STIR:
- **Sialadenitis / stones:** Gland enlargement, ductal dilation, and inflammatory stranding. Post-contrast VIBE (#7) confirms asymmetric gland enhancement (inflamed gland enhances avidly). Stones may appear as T1-dark filling defects within the duct on T1 SE (#4).
- **Sjögren's syndrome:** Bilateral "salt and pepper" appearance — multiple T2-hyperintense foci (lymphocytic infiltrates) throughout both parotid glands. T1 SE (#4) shows fatty replacement of glands in chronic disease. Progresses to increased risk of lymphoma — any dominant nodule with restricted diffusion (#5) and rapid enhancement (#6, #7) is concerning.

**Coverage:** Per Section 2 — Option A (parotid-only) or Option B (all salivary glands).

---

**`t1_se_tra` (#4)**
T1 **Spin Echo** (SE, not TSE!) axial. Pre-contrast. Matched geometry to #3 for direct enhancement comparison.

The distinction between SE and TSE matters here more than in NP or oral cavity — the parotid tumour capsule and its relationship to the facial nerve plane are sub-millimetre structures. TSE introduces turbo-factor-related blurring: later echoes in the train are acquired with reduced signal, blurring fine edges. A conventional SE has no turbo factor — each TR fills a single k-space line at the same TE, giving a sharper point spread function. Early capsular breach, irregularity, or the thin tumour-facial nerve interface can be the difference between superficial parotidectomy and total parotidectomy with nerve sacrifice.

T1 SE also exploits the parotid's intrinsic T1 hyperintensity: normal parotid parenchyma is fatty (T1-bright). A T1-dark mass within bright gland tissue is highly conspicuous even without contrast. The pre-contrast T1 defines the tumour extent before any enhancement alters the gland signal. This is the baseline for all post-contrast comparison.

**Coverage:** Matches #3.

---

**`resolve_4scan_trace_tra` (#5)**
The key diagnostic question DWI answers in salivary gland imaging: **pleomorphic adenoma vs cellular tumour (Warthin or malignant).**

- **Pleomorphic adenoma:** Abundant myxoid/chondroid stroma — water diffuses freely through the loose extracellular matrix → **ADC bright** (facilitated diffusion, high ADC value). This is a distinguishing feature: a T2-hyperintense parotid mass with high ADC is almost certainly a pleomorphic adenoma.
- **Warthin tumour:** Densely cellular oncocytic epithelium with lymphoid stroma → **ADC dark** (restricted diffusion). Combined with T2-intermediate signal and Type B DCE curve, this triad is diagnostic.
- **Malignant tumour (mucoepidermoid carcinoma, adenoid cystic carcinoma, adenocarcinoma):** Cellular → **ADC dark**. Cannot be distinguished from Warthin by DWI alone — the DCE curve (#6) separates them.

4-scan trace gives more isotropic diffusion weighting than 3-scan, reducing directional bias when the parotid sits against the mastoid and mandible — both sources of susceptibility artefact. RESOLVE's readout-segmented EPI reduces distortion at the mandible and mastoid compared to single-shot EPI.

---

**Contrast**
Standard dose IV gadolinium. DCE (#6) starts ~20 s post-injection (fixed delay). The injection must be precisely timed — the DCE curve shape depends on capturing the arterial phase, early enhancement, and wash-out.

---

**`t1_vibe_tra_dyn_C` (#6)**
T1 VIBE axial **dynamic contrast-enhanced (DCE)**. This is the defining sequence of salivary gland MRI — no other head and neck protocol uses DCE. The acquisition covers the whole parotid gland and is acquired repeatedly over 3–5 minutes. After the scan, a single slice through the most enhancing portion of the lesion is selected **retrospectively**, an ROI is placed in the most enhancing portion, and a time-intensity curve (mean curve) is generated.

The time-intensity curve separates the three major parotid tumours:

| Curve Type | Pattern | Tumour | Mechanism |
|------------|---------|--------|-----------|
| **Type A** | Persistent increase (progressive, no wash-out) | **Pleomorphic adenoma** | Myxoid/chondroid stroma — slow, gradual contrast accumulation into the extracellular matrix. Enhancement continues to rise throughout the acquisition |
| **Type B** | Rapid wash-in → rapid wash-out | **Warthin tumour** | Highly vascular oncocytic epithelium + lymphoid stroma. Contrast enters rapidly via abundant capillaries and washes out quickly — the hallmark early peak followed by signal decline |
| **Type C** | Rapid wash-in → plateau (no significant wash-out) | **Malignant** (mucoepidermoid, adenoid cystic, adenocarcinoma, lymphoma, metastases) | Tumour angiogenesis — leaky, disorganised capillaries. Contrast accumulates rapidly and persists in the interstitial space without wash-out |

**Acquisition parameters:** Fixed delay ~20 s post-injection start. Runs ~3–5 minutes. *Off normalization:* the mean curve displays raw signal intensity (absolute values), not normalized to baseline (pre-contrast = 1.0). [AI ADDED — Verify: "off normalization" = raw signal intensity displayed rather than normalised to pre-contrast baseline?]

**Practical note on ROI placement:** After acquisition, select the single slice through the most avidly enhancing portion of the lesion. Place the ROI in the most enhancing region, avoiding cystic/necrotic areas and visible vessels. A poorly placed ROI (e.g., in a non-enhancing cystic component) will produce a flat curve that mischaracterises the tumour. If the lesion is heterogeneous, consider a second ROI in a different region.

**After DCE completes, proceed directly to #7 and #8.** Enhancement is already 3–5 min post-injection — the optimal post-contrast T1 window is now.

---

**`t1_vibe_fs_tra_C` (#7)**
T1 VIBE FS axial post-contrast. Matched geometry to pre-contrast T1 SE (#4). The enhancing tumour margin is assessed against suppressed glandular fat.

Post-contrast axial answers the surgical questions:
- **Deep lobe involvement:** Enhancing tumour medial to the retromandibular vein → deep lobe → total parotidectomy.
- **Capsular integrity:** Smooth enhancing margin → encapsulated (pleomorphic adenoma). Irregular, infiltrative margin → possible malignancy.
- **Perineural spread:** Enhancing tissue along the facial nerve (CN VII) — the nerve exits the stylomastoid foramen, enters the parotid, and divides within the gland. Adenoid cystic carcinoma has a notorious predilection for perineural spread; enhancing tissue tracking along the expected nerve course raises suspicion.
- **Nodal enhancement:** Enhancing Level IB, II, or intraparotid nodes → nodal staging.

VIBE (gradient echo) is acceptable axially — the axial plane through the parotid has fewer air-bone interfaces than the coronal. For the coronal plane (#8), StarVIBE's radial acquisition handles the motion and susceptibility differently.

---

**`t1_starvibe_fs_cor_C` (#8)**
T1 StarVIBE FS coronal. Swallowing moves the parotid and submandibular region vertically — the parotid drapes over the mandible and the submandibular gland sits against the mylohyoid, both displaced by the tongue base and pharyngeal wall during a swallow. StarVIBE is motion-robust. FS suppresses glandular and subcutaneous fat — enhancing tumour is conspicuous.

Coronal plane profiles the parotid tail, submandibular gland, and bilateral cervical nodes for symmetric comparison — the same anatomical coverage as the pre-contrast coronals (#1, #2). MPR (#9) provides sagittal and axial reformatted views.

**Coverage:** Matches the coronal coverage (back of ear → symphysis menti). No vertex is needed — salivary gland tumours do not track perineurally to the vertex.

---

**`MPR` (#9)**
Multiplanar reconstruction from StarVIBE (#8). Sagittal and axial reformatted views. The sagittal plane is particularly useful for parotid tail tumours — the tail extends inferiorly and its full craniocaudal extent is seen on a single sagittal slice.

---

## 4. Comparison with NP and Oral Cavity Protocols

The base sequence set is essentially the same as oral cavity. Both protocols need the T2 FS + non-FS coronal pair for surgical anatomy: in oral cavity it defines the tumour boundary against tongue musculature; in salivary glands it defines the facial nerve plane and capsular integrity against the fatty parotid background. Two differences matter:

**1. DCE is unique to salivary glands.** No other head and neck protocol uses dynamic contrast imaging. NP and oral cavity SCC are both T2-intermediate, ADC-dark, and enhance avidly — there is no benign mimic that DCE would separate. In salivary glands, pleomorphic adenoma (benign, common, T2-bright, ADC-bright, Type A DCE curve) and Warthin tumour (benign, common, T2-intermediate, ADC-dark, Type B DCE curve) are both more common than primary parotid malignancy. DCE is essential because T2 signal and DWI alone cannot distinguish Warthin from malignancy (both are ADC-dark) — the DCE curve makes the distinction.

**2. T1 SE (not TSE) for pre-contrast axial — shared with PNS.** Both need sharp margin detail (lamina papyracea/cribriform in PNS; tumour capsule/facial nerve plane in salivary glands). NP and oral cavity use TSE because soft tissue contrast is the priority.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Parotid fully included on all sequences? | Reposition if clipped |
| **DCE ROI placement** — ROI in the most enhancing portion? Avoided cystic/necrotic areas and vessels? | A poorly placed ROI (cystic component, vessel) produces a flat or spurious curve. Review the DCE source images and re-place ROI if needed |
| **DCE curve interpretation** — Are T2 signal, DWI/ADC, and DCE curve type concordant? | Discordance demands scrutiny: ADC-bright + Type C curve → re-examine the DCE ROI; T2-bright + ADC-dark → unusual for pleomorphic adenoma, consider myoepithelioma or other variant |
| **Motion** — Swallowing artefact on StarVIBE (#8)? Tongue movement on DCE (#6)? | Movement during DCE displaces the gland and contaminates the time-intensity curve. If the DCE is degraded: it cannot be repeated (contrast is already in). The post-contrast VIBE (#7) and StarVIBE (#8) must be diagnostic |
| **Post-contrast** — Contrast present? Confirm glandular and mucosal enhancement | If absent: check IV line, confirm injection |
| **Fat saturation** — uniform on T2 FS coronal (#1), VIBE FS axial (#7), and StarVIBE (#8)? | Narrow manual shim over the parotid |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-02 | — | Initial — 9 sequences (DCE, MPR). Two coverage options (parotid-only, all salivary glands) |
