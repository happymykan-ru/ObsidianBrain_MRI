# Pituitary (Sellar/Suprasellar MRI)

**Version:** 1.0 | **Date:** 2026-07-19 | **Scanner:** [Confirm 1.5T/3T]

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
| 1 | `t1_tse_sag_pit` | Sagittal | ∥ midline | Sella + suprasellar cistern | **Posterior** (venous sinus) |
| 2 | `t1_tse_r_cor_pit_2mm` | Coronal | ⟂ sella floor / ∥ pituitary stalk | Cavernous sinus L → cavernous sinus R | **None** |
| 3 | `t2_tse_cor_pit_2mm` | Coronal | Copy Slice from #2 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 4 | `t1_tse_cor_pit_2mm_dyn_C` | Coronal | Copy Slice from #2 | — | **Parallel** (anterior + posterior to slab) |
| 5 | `t1_tse_r_fs_cor_pit_2mm_C` | Coronal | Copy Slice from #2 | — | **None** |
| 6 | `t1_tse_sag_pit_C` | Sagittal | Copy Slice from #1 | — | **None** |

*#4: Inject contrast after the 1st measurement. Sequence includes a 10 s pause before continuing.*

---

## 3. Sequence Rationale

### Core Strategy

All sequences use TSE — the sphenoid sinus air creates severe B0 inhomogeneity at the sella floor. GRE would bloom and lose signal. TSE's 180° refocusing pulses correct for this. The pituitary is small (~5–10 mm); 2 mm coronal slices and sagittal views provide adequate through-plane resolution.

**`t1_tse_sag_pit` (#1)**
T1 TSE sagittal. Profiles the anterior/posterior pituitary, infundibulum, optic chiasm, hypothalamus, and mammillary bodies in the midline. Pre-contrast baseline — the posterior pituitary is intrinsically bright (neurophysin vesicles) and serves as an internal reference. Loss of the posterior pituitary bright spot can indicate stalk compression or infiltration.

**`t1_tse_r_cor_pit_2mm` (#2)**
T1 TSE coronal 2 mm with restore pulse. Symmetric view of the cavernous sinuses, carotid siphons, pituitary stalk, and optic chiasm. Only the coronal needs restore — 2 mm slices through the small pituitary FOV have inherently low SNR per voxel. The sagittal T1 (#1) is 3 mm — 50% more protons per voxel, so SNR is adequate without it.

**`t2_tse_cor_pit_2mm` (#3)**
T2 TSE coronal 2 mm. CSF is bright — the suprasellar cistern, optic chiasm, and relationship of any mass to surrounding structures are clearly defined. Adenomas are often mildly T2 hyperintense; cystic components are bright.

**`t2_tse_sag_pit` [Optional — non-contrast only]**
T2 TSE sagittal. Added for non-contrast pituitary exams where post-contrast sagittal T1 is unavailable. Profiles the suprasellar cistern, optic chiasm, stalk, and any cystic components in the sagittal plane. Omitted when contrast is given because post-contrast T1 sagittal (#6) provides the anatomical reference.

**Contrast**
Standard dose IV gadolinium. Dynamic coronal (#4) captures the enhancement time course through the pituitary. Post-contrast FS (#5) and sagittal (#6) follow.

**`t1_tse_cor_pit_2mm_dyn_C` (#4)**
Dynamic T1 TSE coronal. 1st measurement = pre-contrast mask. Inject contrast after the 1st measurement; the sequence includes a 10 s pause before continuing — this allows the contrast bolus to travel from the arm vein to the carotid circulation, so no dynamic frames are wasted on contrast-free tissue.

*Why does normal pituitary enhance before adenoma?* The normal anterior pituitary receives blood via the hypothalamic-hypophyseal portal system: superior hypophyseal artery → capillary plexus in median eminence → portal veins down the stalk → anterior pituitary. This is a high-flow, low-resistance short-circuit from the carotid. An adenoma loses the portal connection and develops its own direct arterial supply from capsular or inferior hypophyseal branches — small, tortuous, high-resistance neovessels. Contrast perfuses the high-flow portal system rapidly (~30–60 s) and the low-flow neovessels slowly (~60–120 s). The temporal gap — normal pituitary bright, adenoma still dark on early phases — is the key diagnostic finding for microadenomas.

Anterior and posterior parallel sat bands suppress inflowing blood from the ACA/MCA and basilar circulations. Without them, flowing blood creates bright signal that varies with time and mimics tissue enhancement on the dynamic curve.

**`t1_tse_r_fs_cor_pit_2mm_C` (#5)**
Post-contrast T1 TSE coronal with fat saturation, 2 mm. Fat sat suppresses the bright posterior pituitary and clival marrow — enhancing adenoma and normal pituitary stand out against the suppressed background. Thin coronal slices profile cavernous sinus invasion (the most common route of lateral extension).

**`t1_tse_sag_pit_C` (#6)**
Post-contrast T1 TSE sagittal. Profiles suprasellar extension through the diaphragma sellae, optic chiasm compression, and hypothalamic involvement. The sagittal view confirms the craniocaudal extent of any mass.

---

## 4. Pathology-Based Variations

- **Microadenoma (<10 mm):** Add dynamic coronal (#4). Normal pituitary enhances first (portal supply); adenoma enhances late (systemic supply) — early-phase dark lesion against bright pituitary is the key finding.
- **Macroadenoma (>10 mm):** Coronal at 3 mm, no dynamic — temporal separation not diagnostic for large masses. Carotid encasement >50% on coronal is the key surgical contraindication.
- **Post-op:** No dynamic — the question is residual tumour volume, not enhancement kinetics.
- **Pre-contrast T1-bright lesion (apoplexy, Rathke's cleft cyst, craniopharyngioma):** Add `t1_tse_r_cor_pit_2mm_C` (non fat-sat). Methaemoglobin, protein, and cholesterol are T1-bright pre-contrast — fat sat alone cannot distinguish pre-existing brightness from true enhancement. Subtract pre (#2) from post for a pure enhancement map.
- **Non-contrast pituitary:** Add `t2_tse_sag_pit`. Without post-contrast T1 sagittal, T2 sagittal provides the suprasellar anatomical reference.
- **Stalk lesion / diabetes insipidus:** Add dynamic coronal (#4). Stalk enhancement pattern with loss of posterior pituitary bright spot on pre-contrast sagittal.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — sagittal includes optic chiasm and hypothalamus? Coronal includes both cavernous sinuses? | Reposition if suprasellar cut off or cavernous sinus clipped |
| **Pre-contrast T1 (#1, #2)** — intrinsic T1 hyperintensity? (posterior pituitary is normal; other bright signal = apoplexy, Rathke's, craniopharyngioma) | If lesion is T1-bright: add `t1_tse_r_cor_pit_2mm_C` for subtraction |
| **Post-contrast** — contrast present? Confirm enhancement of normal pituitary and cavernous sinus | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 6 sequences |
