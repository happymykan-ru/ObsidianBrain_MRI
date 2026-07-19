# Pituitary + Brain (Sellar/Suprasellar MRI with Full Brain)

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
| 1 | `t2_tse_tra_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| 4 | `t1_tse_sag_pit` | Sagittal | ∥ midline | Sella + suprasellar cistern | **Posterior** (venous sinus) |
| 5 | `t1_tse_r_cor_pit_2mm` | Coronal | ⟂ sella floor / ∥ pituitary stalk | Cavernous sinus L → cavernous sinus R | **None** |
| 6 | `t2_tse_cor_pit_2mm` | Coronal | Copy Slice from #5 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 7 | `t1_tse_cor_pit_2mm_dyn_C` | Coronal | Copy Slice from #5 | — | **Parallel** (anterior + posterior to slab) |
| 8 | `t1_tse_r_fs_cor_pit_2mm_C` | Coronal | Copy Slice from #5 | — | **None** |
| 9 | `t1_tse_sag_pit_C` | Sagittal | Copy Slice from #4 | — | **None** |
| 10 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |

*#7: Inject contrast after the 1st measurement. 10 s pause included in sequence. See `pituitary.md` for rationale.*

---

## 3. Sequence Rationale

### Core Strategy

Two tiers: full brain screening for parenchymal pathology that may present with pituitary-region symptoms (visual field defects, hormonal disturbances). Targeted pituitary sequences (#4–#9) for dedicated sellar assessment. For pituitary-specific rationale (plane choice, dynamic timing, fat sat), see `pituitary.md`.

**`t2_tse_tra_brain` (#1)**
Core axial T2 anatomy. Reference plane.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast T1 baseline. FLASH 2D — same rationale as `contrast_brain.md`.

**`resolve_3scan_trace_tra_p2` (#3)**
RESOLVE DWI. Acute ischaemia, abscess. Pituitary apoplexy can present with acute headache and visual loss mimicking stroke — DWI distinguishes ischaemia from haemorrhagic apoplexy.

**`t1_tse_sag_pit` (#4)**
T1 TSE sagittal pituitary. Pre-contrast baseline — posterior pituitary bright spot, optic chiasm, infundibulum.

**`t1_tse_r_cor_pit_2mm` (#5)**
T1 TSE coronal 2 mm with restore pulse. Only coronal needs restore — 2 mm slices through small FOV = low SNR. Sagittal is 3 mm. See `pituitary.md`.

**`t2_tse_cor_pit_2mm` (#6)**
T2 TSE coronal 2 mm. CSF-cistern definition, cystic components.

**Contrast**
Standard dose IV gadolinium. Dynamic coronal (#7) captures the pituitary enhancement time course — inject after 1st measurement.

**`t1_tse_cor_pit_2mm_dyn_C` (#7)**
Dynamic T1 TSE coronal. 1st measurement = mask, inject contrast after it, sequence includes 10 s pause. Normal pituitary enhances first (high-flow portal system), adenoma enhances late (low-flow neovessels). See `pituitary.md` for full rationale.

**`t1_tse_r_fs_cor_pit_2mm_C` (#8)**
Post-contrast T1 TSE coronal FS 2 mm. Cavernous sinus invasion assessment. Fat sat suppresses clival marrow and posterior pituitary.

**`t1_tse_sag_pit_C` (#9)**
Post-contrast T1 TSE sagittal. Suprasellar extension, chiasm compression, hypothalamic involvement.

**`t1_fl2d_tra_brain_C` (#10)**
Post-contrast 2D FLASH axial brain. Subtract pre (#2) for enhancement map. Captures parenchymal or meningeal enhancement that pituitary-targeted sequences would miss.

---

## 4. How This Differs from Standard contrast_brain

This protocol is a modified `contrast_brain` — sequences are removed or replaced because the pituitary is the target, not whole-brain screening.

- **`t2_tse_flair_tra` ❌:** Pituitary-region symptoms (visual field defect, hormonal) rarely present with parenchymal FLAIR abnormalities. T2 brain suffices for structural lesions.
- **`t1_vibe_fs_cor_C` + `MPR` ❌:** Replaced by targeted pituitary coronal T1 FS (#8) at 2 mm. The VIBE/MPR is a whole-brain screening flyover; a 2 mm targeted coronal through the sella has far higher diagnostic value for pituitary pathology.
- **Post-contrast brain T1 placed last:** `t1_fl2d_tra_brain_C` (#10) runs after the pituitary sequences — the dynamic (#7) and targeted views (#8, #9) take priority for the enhancement window. Brain FLASH catches parenchymal or meningeal enhancement the pituitary views would miss.

---

## 5. Pathology-Based Variations

This protocol is only for pituitary-region symptoms with no brain indications (e.g., isolated visual field defect, isolated endocrine disturbance). If brain pathology is also suspected, use `contrast_brain.md` plus dedicated pituitary sequences instead.

For pituitary-specific variations (microadenoma, macroadenoma, apoplexy, stalk lesion), see `pituitary.md`.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on brain axials? Sella + suprasellar on pituitary series? | Adjust slice stack |
| **Pre-contrast T1 (#4, #5)** — intrinsic T1 hyperintensity? (posterior pituitary is normal; other bright signal = apoplexy, Rathke's, craniopharyngioma) | If lesion is T1-bright: add `t1_tse_r_cor_pit_2mm_C` (copy #5, no fat sat) for subtraction |
| **Post-contrast** — contrast present? Confirm enhancement of normal pituitary and cavernous sinus | If absent: check IV line, confirm injection |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 10 sequences |
