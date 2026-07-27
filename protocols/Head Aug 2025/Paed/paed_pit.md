# Paediatric Pituitary (Sellar/Suprasellar MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil — paediatric-specific if available. Use the smallest coil that fits.
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. For infants, feed/swaddle and scan during natural sleep if possible.
- **IV Access:** Age-appropriate gauge. Injection rate: [Confirm age/weight-based protocol]. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_se_sag_pit` *(<2yr)* / `t1_tse_sag_pit` *(>2yr)* | Sagittal | ∥ midline | Sella + suprasellar cistern | **Posterior** (venous sinus) |
| 2 | `t1_tse_cor_2mm_pit` | Coronal | ⟂ sella floor / ∥ pituitary stalk | Cavernous sinus L → cavernous sinus R | **None** |
| 3 | `t2_tse_cor_2mm_pit` | Coronal | Copy Slice from #2 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 4 | `t1_tse_cor_2mm_dynamic_C` *(>6yr only)* | Coronal | Copy Slice from #2 | — | **Parallel** (anterior + posterior to slab) |
| 5 | `t1_tse_cor_2mm_fs_pit_C` | Coronal | Copy Slice from #2 | — | **None** |
| 6 | `t1_tse_sag_pit_C` | Sagittal | Copy Slice from #1 | — | **None** |

*#1: SE for <2yr (sharper, no T2 blurring for the small pituitary). TSE for >2yr.*
*#4: Dynamic only if >6yr — before this age the pituitary enhancement pattern (portal vs systemic supply) is not reliably established. Inject contrast after the 1st measurement; sequence includes a 10 s pause. See `pituitary.md` for dynamic rationale.*

---

## 3. Sequence Rationale

### Core Strategy

Built on the adult `pituitary.md` template with paediatric modifications. All sequences use TSE (or SE for the smallest patients) — the sphenoid sinus air creates B0 inhomogeneity at the sella floor regardless of age. The paediatric pituitary is smaller; 2 mm coronal slices remain adequate.

**`t1_se_sag_pit` (<2yr) / `t1_tse_sag_pit` (>2yr) (#1)**
T1 sagittal. Profiles the anterior/posterior pituitary, infundibulum, optic chiasm, and hypothalamus. <2yr: SE (conventional spin echo) — one 180° pulse per TR means no T2 blurring, giving sharper depiction of the small infant pituitary. TSE's slight blurring matters more when the target is only a few millimetres across. >2yr: TSE — the pituitary is larger and the faster acquisition suits the older child.

**`t1_tse_cor_2mm_pit` (#2)**
Pre-contrast T1 TSE coronal 2 mm. Symmetric view of the cavernous sinuses, carotid siphons, pituitary stalk, and optic chiasm. Matched to post-contrast FS (#5) for enhancement comparison.

**`t2_tse_cor_2mm_pit` (#3)**
T2 TSE coronal 2 mm. CSF is bright — defines the suprasellar cistern, optic chiasm, and any cystic components.

**Contrast**
Standard dose IV gadolinium, age/weight-adjusted. Dynamic coronal (#4) captures the enhancement time course if the child is >6yr. Post-contrast FS (#5) and sagittal (#6) follow.

**`t1_tse_cor_2mm_dynamic_C` (>6yr) (#4)**
Dynamic T1 TSE coronal. Same portal-vs-systemic supply rationale as adult — only applicable after age 6, when the pituitary vascular supply pattern is mature. Before age 6, the enhancement kinetics are unreliable (developing pituitary vasculature). See `pituitary.md` for full dynamic rationale.

**`t1_tse_cor_2mm_fs_pit_C` (#5)**
Post-contrast T1 TSE coronal with fat saturation, 2 mm. Fat sat suppresses clival marrow — enhancing pituitary tissue stands out. Thin coronal slices profile cavernous sinus invasion. A non-fat-sat post-contrast coronal is not needed as a separate pathology variation — paediatric pituitary pathology rarely presents with the intrinsic T1 hyperintensity (adult apoplexy, Rathke's) that requires non-fat-sat subtraction.

**`t1_tse_sag_pit_C` (#6)**
Post-contrast T1 TSE sagittal. Suprasellar extension, optic chiasm compression, hypothalamic involvement.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Age** — correct sagittal T1 selected? | <2yr: SE. >2yr: TSE |
| **Dynamic (#4)** — child >6yr? | If <6yr, omit #4. Dynamic enhancement pattern is not reliable in the developing pituitary |
| **Coverage** — sagittal includes optic chiasm and hypothalamus? Coronal includes both cavernous sinuses? | Reposition if suprasellar cut off or cavernous sinus clipped. Paediatric sella is smaller — confirm the pituitary is centred |
| **Post-contrast FS (#5)** — fat saturation uniform? | Re-shim if clival marrow not suppressed. Pre-contrast coronal (#2) is the non-fat-sat fallback for subtraction |
| **Post-contrast** — contrast present? Confirm enhancement | If absent: check IV line, confirm injection |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-27 | — | Initial — 6 sequences (age-adapted: SE vs TSE sagittal, dynamic >6yr only) |
