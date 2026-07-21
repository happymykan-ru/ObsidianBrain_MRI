# IAM + Brain (Internal Auditory Meatus with Full Brain ± Contrast)

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
| 1 | `t2_tse_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dark_fluid_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `t2_space_tra_iso_IAM` | Axial | ∥ AC-PC line | Upper medulla → mid-pons (~30–40 mm) | **None** |
| 5 | `t1_fl2d_sag_brain` | Sagittal | ∥ midline | Whole brain | **None** |
| 6 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 7 | `t1_vibe_fs_cor_brain_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 8 | `MPR planning` | Sag+Ax | — | Whole brain | — |
| 9 | `t1_se_r_fs_tra_IAM_C` *(or `t1_tse_fs_tra_3mm_IAM_C` for 3T)* | Axial | Copy Slice from #4 | — | **None** |

*#5 is for plain brain only — omit if contrast is given.*

---

## 3. Sequence Rationale

### Core Strategy

Two tiers: full brain screening sequences detect parenchymal pathology that may present with IAM symptoms (e.g., MS plaque at the root entry zone, brainstem glioma). High-resolution targeted IAM sequences (#4, #9) specifically assess the 7th/8th nerve complexes and CPA cisterns.

**`t2_tse_tra` (#1)**
Core axial T2 anatomy. Reference plane.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. FLASH 2D — matched geometry to post-contrast sequences for enhancement comparison and subtraction.

**`t2_tse_dark_fluid_tra` (#3)**
CSF-suppressed T2 FLAIR. Periventricular/cortical lesions. Brainstem and periaqueductal plaques can present with IAM symptoms — FLAIR catches these.

**`t2_space_tra_iso_IAM` (#4)**
3D T2 SPACE isotropic — primary IAM screening sequence. Cisternographic effect (CSF bright, nerves dark). Vestibular schwannoma: CPA mass extending into or widening the IAM. Coronal reformat recommended for canalicular extension and cochlear relationship. For full details on resolution, coverage, and slice oversampling, see `IAM(no_brain_request).md`.

**`t1_fl2d_sag_brain` (#5) — Plain brain only**
Midline anatomical reference — brainstem, vermis, craniocervical junction. Omitted when contrast is given because post-contrast MPR (#9) provides the sagittal view.

**`resolve_3scan_trace_tra_p2` (#6)**
RESOLVE DWI. Acute ischaemia, abscess, cellular tumours. Less distortion at skull base vs single-shot EPI — important when assessing the CPA/brainstem.

**Contrast**
Standard dose IV gadolinium. VIBE (#7) runs first — brain enhancement screening while IAM tumour enhancement peaks slightly later. Target ~5 min delay before the IAM sequence (#9).

**`t1_vibe_fs_cor_brain_C` (#7)**
3D T1 post-contrast coronal with fat saturation. Brain enhancement screening — skull base, meninges. Source data for MPR (#8). Placed before the IAM T1 to allow adequate enhancement delay.

**`MPR planning` (#8)**
Multiplanar reconstruction from post-contrast VIBE (#7). Sagittal and axial reformatted views.

**`t1_se_r_fs_tra_IAM_C` (or `t1_tse_fs_tra_3mm_IAM_C` for 3T) (#9)**
Post-contrast T1 with fat saturation. SE with restore at 1.5T (sharper, no T2 blurring); TSE at 3T (faster, SNR compensates). See `IAM(no_brain_request).md`.

---

## 4. How This Differs from Standard Brain Protocols

This protocol is built on the `contrast_brain` template (FLASH 2D pre-contrast, FLAIR, DWI, VIBE + MPR post-contrast) with two additions: T2 SPACE IAM (#4) and T1 TSE FS IAM (#9). FLASH 2D is used instead of MPRAGE for three reasons: (1) T2 SPACE is already a long 3D acquisition — adding MPRAGE doubles the 3D burden and inflates scan time; (2) for IAM indications, the diagnostic pre-contrast sequences are SPACE and FLAIR — the T1 is purely a baseline for post-contrast comparison, and FLASH 2D does this without the unnecessary anatomical detail of MPRAGE; (3) IAM protocols may convert to contrast mid-scan, and FLASH 2D is already the correct pre-contrast baseline (same logic as `cerebral_angiogram+brain.md`).

For **plain brain**, the sagittal FLASH (#5) fills the gap: standard `contrast_brain` gets sagittal from the post-contrast MPR (#8), but the plain version skips contrast entirely and has no MPR. Without #5, there is no midline anatomical view (brainstem, vermis, craniocervical junction). T2 SPACE (#4) alone may exclude a CPA mass.

---

## 5. When to Use IAM+brain vs IAM Only

Use `IAM+brain` when symptoms could be central:
- **First presentation asymmetric SNHL** — differential includes brainstem MS, CPA meningioma, brainstem glioma
- **Vertigo with central features** — brainstem or cerebellar ischaemia, demyelination
- **Unexplained facial nerve palsy** — brainstem and CPA must be excluded

Use `IAM(no_brain_request).md` when the brain has already been screened or the question is purely local:
- **Known vestibular schwannoma follow-up** — diagnosis established, only need to assess growth/enhancement
- **NF2 screening** — bilateral vestibular schwannomas are the defining feature; IAM scan catches them while still intracanalicular and hearing-preservation surgery is possible. Brain is imaged separately for associated meningiomas/ependymomas
- **Pre-op planning for CPA/IAM surgery** — focused anatomical detail only
- **Confirmed peripheral pathology** — e.g., Ménière's diagnosed clinically (tinnitus + vertigo + fluctuating hearing loss, audiometry confirms). MRI is to exclude a retrocochlear mimic, not to diagnose Ménière's. T2 SPACE for labyrinthine hydrops, post-contrast T1 for enhancement

For pathology-based variations (facial nerve, CPA mass, cholesteatoma), see `IAM(no_brain_request).md`. Cholesteatoma in particular requires dedicated HASTE diffusion sequences not part of the standard IAM protocol.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Plain brain?** — `t1_fl2d_sag_brain` (#5) added? | If contrast not requested, #5 is mandatory. Omitted if contrast given |
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack |
| **`t2_space_tra_iso_IAM` (#4)** — IAM centred in slab? Wrapped anatomy or signal falloff reaching the lesion? | See `IAM(no_brain_request).md` Alerts |
| **`t1_tse_fs_tra_3mm_IAM_C` (#9)** — contrast present? Confirm facial nerve enhancement | If absent: check IV line, confirm injection |


---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 9 sequences (IAM targeted + full brain) |
