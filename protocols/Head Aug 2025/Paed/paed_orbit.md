# Paediatric Orbit (Orbital MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil — paediatric-specific if available. Use the smallest coil that fits.
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. Instruct the child to close eyes and keep them still — eye movement causes motion artefact in the orbits. For infants, feed/swaddle and scan during natural sleep if possible.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra_orbit` | Axial | ∥ optic nerves | Superior orbital rim → inferior orbital rim | **None** |
| 2 | `t1_tse_tra_orbit` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_cor_fs_orbit` | Coronal | ⟂ hard palate | Anterior globe → orbital apex | **None** |
| — | **Contrast** | — | — | — | — |
| 4 | `t1_tse_fs_tra_orbit_C` | Axial | Copy Slice from #1 | — | **None** |
| 5 | `t1_tse_fs_cor_orbit_C` | Coronal | Copy Slice from #3 | — | **None** |

---

## 3. Sequence Rationale

### Core Strategy

All sequences use TSE — the paediatric orbit has the same B0 challenges as adult (ethmoid air cells), compounded by smaller anatomy. Fat suppression is essential: orbital fat masks the small-calibre paediatric optic nerve and extraocular muscles.

**`t2_stir_tra_orbit` (#1)**
T2 STIR axial. Same rationale as adult orbit — STIR provides uniform fat suppression regardless of B0 distortion near the ethmoid air cells. Axial profiles the optic nerves and extraocular muscles in their long axis.

**`t1_tse_tra_orbit` (#2)**
Pre-contrast T1 TSE axial. Baseline for post-contrast comparison. TSE avoids GRE susceptibility at the ethmoid-air interface. No fat sat — the bright orbital fat provides natural contrast against the darker nerve and muscles.

**`t2_tse_cor_fs_orbit` (#3)**
T2 TSE coronal with fat saturation. Cross-sectional view of both optic nerves for symmetric comparison. Chemical fat sat is used instead of adult Dixon — paediatric orbits are smaller with proportionally larger B0 distortion from ethmoid air cells. Dixon's water-fat separation algorithm is more likely to fail here; simple FS TSE is more reliable. The Dixon bonus (in/opposed phase for fat-containing lesions) is less relevant in paediatric orbital pathology.

**Contrast**
Standard dose IV gadolinium, age/weight-adjusted. Target ~3–5 min delay before post-contrast T1.

**`t1_tse_fs_tra_orbit_C` (#4)**
Post-contrast T1 TSE axial with fat saturation. Enhancing lesions become conspicuous against suppressed orbital fat. Matched geometry to pre-contrast (#2) for comparison and subtraction.

**`t1_tse_fs_cor_orbit_C` (#5)**
Post-contrast T1 TSE coronal with fat saturation. Profiling the enhancement pattern across the extraocular muscles, optic nerve sheath, and lacrimal gland — symmetric comparison is essential.

---

## 4. How This Differs from Adult orbit

- **No pre-contrast T1 coronal:** The adult protocol includes a pre-contrast T1 coronal baseline. Here it is omitted — the paediatric orbit is small, and a pre-contrast coronal T1 adds scan time without additional diagnostic value. The post-contrast FS coronal T1 (#5) is the key coronal sequence.

- **T2 FS coronal instead of Dixon coronal:** The adult protocol uses Dixon coronal for water-only images with better SNR and in/opposed phase bonus. Paediatric orbits are smaller with proportionally larger B0 distortion from ethmoid air cells — Dixon's water-fat separation algorithm is more likely to fail. Simple chemical fat sat TSE is more reliable. The Dixon bonus (fatty infiltration, dermoid characterization) is less relevant in paediatric orbital pathology (retinoblastoma, rhabdomyosarcoma, optic pathway glioma).

- **No dynamic option, no oblique sagittal option as standard:** Adult orbital pathology (thyroid eye disease, cavernoma, optic neuritis) requires dynamic perfusion and dedicated oblique sagittal optic nerve views. Paediatric orbital pathology is different — these are added per indication only (see Section 5).

- **Simpler overall:** Five core sequences vs six in adult. The paediatric protocol focuses on the essential pre/post contrast pair with T2 STIR and FS coronal for anatomical coverage.

---

## 5. Pathology-Based Variations

### Retinoblastoma (Combined Brain + Orbit Protocol)

Retinoblastoma is a tumour of the retina that can spread along the optic nerve and present with trilateral disease (bilateral retinal tumours + pineal/suprasellar primitive neuroectodermal tumour). Brain sequences are essential for staging. The orbit sequences use thinner slices (2 mm) for the smaller paediatric eye, and T2 SPACE replaces standard 2D T2 for isotropic multi-planar assessment.

- `t2_tse_tra_brain`
- `t1_fl2d_tra_brain`
- `resolve_3scan_trace_tra_brain` *(DWI — retinoblastoma is highly cellular, restricts diffusion)*
- `t1_tse_tra_2mm_orbit` *(pre-contrast T1, thin slices for the small globe)*
- `t2_space_tra_orbit` *(3D isotropic — replaces STIR and FS coronal, provides reformats in any plane for the small globe)*
- `t2_tse_obl_sag_2mm` *(L/R, perpendicular to optic nerve — optic nerve invasion is the key staging question)*
- Contrast
- `t1_tse_obl_sag_2mm_orbit_C` *(post-contrast T1 oblique sagittal — optic nerve enhancement = spread)*
- `t1_tse_tra_2mm_orbit_C` *(post-contrast T1 axial)*
- `t1_vibe_fs_cor_brain_C` *(post-contrast whole brain coronal — screens for trilateral disease: pineal and suprasellar tumours)*

The oblique sagittal sequences are the most critical: they show whether retinoblastoma extends along the optic nerve toward the chiasm. If the optic nerve is involved, enucleation alone is insufficient — the nerve must be resected. T2 SPACE provides isotropic 3D anatomical context. DWI helps distinguish retinoblastoma (restricted diffusion, highly cellular) from benign intraocular masses.

Fat sat is deliberately omitted on the orbit T1 sequences. Retinoblastoma enhances intensely — fat sat is not needed for conspicuity. Adding it in the small paediatric orbit risks two problems at the worst possible location: chemical fat sat fails near the ethmoid air cells, creating patchy bright signal that can mimic optic nerve enhancement, and the failure artefact sits right where you are looking for spread. Subtraction of the non-fat-sat pre/post T1 pair gives a cleaner enhancement map of the optic nerve than a fat-sat sequence that may partially fail near the critical anatomy.

Post-contrast VIBE FS coronal brain screens for trilateral disease (pineal and suprasellar tumours).

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Coverage** — superior to inferior orbital rim on all series? Both globes fully included? | Adjust slice stack for paediatric orbit dimensions |
| **Motion** — eye movement causing ghosting? | If restless: use shortest sequences first. Reduce turbo factor or increase parallel imaging. For continuous slow motion consider BLADE; for sudden movements pause and re-acquire |
| **Post-contrast T1 FS (#4, #5)** — fat saturation uniform? | If chemical fat sat fails near ethmoid sinuses, add post-contrast T1 without fat sat and subtract from pre (#2) |
| **Post-contrast** — contrast present? Confirm enhancement | If absent: check IV line, confirm injection |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-27 | — | Initial — 5 sequences + retinoblastoma variation |
