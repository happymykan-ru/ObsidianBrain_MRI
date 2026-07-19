# Orbit (Orbital MRI ± Contrast)

**Version:** 1.0 | **Date:** 2026-07-19 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. Instruct patient to close eyes and keep them still — eye movement causes motion artefact in the orbits.
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra_3mm_orbit` | Axial | ∥ optic nerves (∥ hard palate) | Superior orbital rim → inferior orbital rim | **None** |
| 2 | `t1_tse_tra_3mm_orbit` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dixon_cor_3mm_orbit` | Coronal | ⟂ hard palate | Anterior globe → orbital apex | **None** |
| 4 | `t1_tse_cor_3mm_orbit` | Coronal | Copy Slice from #3 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 5 | `t1_tse_fs_tra_3mm_orbit_C` | Axial | Copy Slice from #1 | — | **None** |
| 6 | `t1_tse_fs_cor_3mm_orbit_C` | Coronal | Copy Slice from #3 | — | **None** |

*See Pathology-Based Variations for optional sequences.*

---

## 3. Sequence Rationale

### Core Strategy

All sequences use TSE (spin echo), not GRE. The orbits sit between the ethmoid air cells and maxillary sinuses — severe B0 inhomogeneity at every air-bone-soft tissue interface. GRE would bloom and lose signal; TSE's 180° refocusing pulses correct for static field inhomogeneity.

Fat suppression is essential because orbital fat is the brightest structure on T1 and T2 — it masks the optic nerve, extraocular muscles, and enhancing lesions.

**`t2_stir_tra_3mm_orbit` (#1)**
T2 STIR axial. STIR is used for the axial plane because it slices through the ethmoid air cells bilaterally — the worst air-tissue interfaces in the orbit, where B0 is heavily distorted. Chemical fat sat fails here, right where the optic nerve and orbital apex sit. STIR doesn't depend on B0: it nulls fat by T1 relaxation (TI ~150–170 ms at 1.5T), not chemical shift. Uniform fat suppression at the cost of lower SNR. Axial profiles the optic nerves and extraocular muscles in their long axis.

**`t1_tse_tra_3mm_orbit` (#2)**
T1 TSE axial without fat suppression. Pre-contrast baseline — the bright orbital fat provides natural contrast against the darker optic nerve, muscles, and globe. Matched geometry to post-contrast T1 FS (#5) for enhancement comparison.

**`t2_tse_dixon_cor_3mm_orbit` (#3)**
T2 TSE Dixon coronal. Dixon is used for the coronal plane because it runs parallel to the ethmoid-maxillary interface rather than across it — B0 is less disrupted, so chemical-shift fat suppression works. Dixon provides water-only images with better SNR than STIR, plus in-phase and opposed-phase images for free: fatty muscle infiltration (thyroid eye disease) and fat-containing lesion characterization (dermoid — signal dropout on opposed phase). Coronal profiles extraocular muscles and optic nerve-sheath complex in cross-section, symmetric L/R comparison.

**`t1_tse_cor_3mm_orbit` (#4)**
T1 TSE coronal without fat suppression. Pre-contrast coronal baseline matched to post-contrast T1 FS (#6). Same TSE rationale — GRE would fail at the ethmoid-maxillary interface.

**Contrast**
Standard dose IV gadolinium. Target ~3–5 min delay before post-contrast T1 (#5, #6).

**`t1_tse_fs_tra_3mm_orbit_C` (#5)**
Post-contrast T1 TSE axial with fat saturation. Enhancing lesions (optic neuritis, tumours, inflammatory pseudotumour, thyroid eye disease activity) become conspicuous against suppressed orbital fat. Matched geometry to pre-contrast T1 (#2) for direct comparison and subtraction.

**`t1_tse_fs_cor_3mm_orbit_C` (#6)**
Post-contrast T1 TSE coronal with fat saturation. Coronal profiles the enhancement pattern across the extraocular muscles, optic nerve-sheath, and lacrimal gland — symmetric comparison is essential for orbital pathology.

### Optional Sequences

**`t1_vibe_fs_tra_orbits_dyn_C`**
Dynamic 3D T1 VIBE with fat saturation. 1 pre-contrast + 3 post-contrast measurements with 20 s delay between each. VIBE (a GRE) is used despite the susceptibility risk because the temporal requirement outweighs it — enhancement kinetics (wash-in slope, peak enhancement time) cannot be captured by conventional TSE. The 20 s temporal resolution distinguishes arterial, capillary, and venous phases through the orbital soft tissues.

**`t2_tse_obl_sag_fs_2mm_orbit` + `t1_tse_obl_sag_fs_2mm_orbit_C` [Optional]**
Oblique sagittal T2 and post-contrast T1 TSE with fat saturation, 2 mm slices. Prescribed perpendicular to each optic nerve (L and R separately) — true cross-section of the nerve-sheath complex. T2 shows anatomy (nerve diameter, CSF sleeve, sheath thickening). T1 post-contrast shows enhancement (sheath vs parenchymal, tram-track, perineural spread). Which sequence is needed depends on the indication (see Pathology-Based Variations).

---

## 4. Pathology-Based Variations

- Add `t1_vibe_fs_tra_orbits_dyn_C` for:
  - **Cavernoma:** [Department] Progressive centripetal fill-in is the hallmark — early peripheral nodular enhancement with gradual centripetal filling on delayed phases. Dynamic VIBE with 20 s temporal resolution captures this pattern and distinguishes cavernoma from other orbital masses.
  - **Thyroid eye disease:** [AI ADDED] Time-intensity curves distinguish active inflammation (rapid enhancement) from chronic fibrosis (slow/no enhancement), guiding immunosuppression vs surgery.

- Add oblique sagittal (L/R, perpendicular to each optic nerve):
  - **Optic neuritis:** `t2_tse_obl_sag_fs_2mm_orbit`. Axial overestimates nerve diameter due to partial volume — true cross-section gives accurate swelling measurement. T2 is sufficient; enhancement is assessed on axial/coronal T1 FS (#5, #6).
  - **Optic nerve sheath meningioma:** `t2_tse_obl_sag_fs_2mm_orbit` + `t1_tse_obl_sag_fs_2mm_orbit_C`. T2 shows the anatomy (sheath thickening, mass, nerve displacement). T1 post-contrast shows the pathognomonic tram-track enhancement (enhancing sheath surrounding non-enhancing nerve) — only reliably seen in true cross-section. Both are needed.
  - **Perineural tumour spread:** `t2_tse_obl_sag_fs_2mm_orbit` + `t1_tse_obl_sag_fs_2mm_orbit_C`. T2 shows sheath thickening if present. T1 post-contrast shows a thin ring of enhancement along the sheath — the earliest sign, caught before thickening develops. Both are needed.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Motion** — eye movement causing ghosting? | Instruct patient to keep eyes closed and still throughout. If severe, consider shorter TSE turbo factor |
| **Coverage** — superior to inferior orbital rim on all series? Both globes fully included? | Reposition if orbital roof or floor clipped |
| **Post-contrast** — contrast present? Confirm enhancement of normal structures (extraocular muscles, nasal mucosa) | If absent: check IV line, confirm injection |
| **Post-contrast T1 FS (#5, #6)** — fat saturation uniform? | If chemical fat sat fails near ethmoid sinuses, add `t1_tse_tra_3mm_orbit_C` (copy #2 geometry) and subtract pre #2 from post for enhancement map |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 6 sequences + 2 optional variations |
