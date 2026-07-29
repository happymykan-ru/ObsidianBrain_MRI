# Oral Cavity (Oral Cavity / Oropharynx MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-29 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head and neck coil
- **Laser Landmark:** Nasion
- **Immobilization:** Foam padding
- **Verbal Instructions:** Breathe quietly and avoid swallowing during acquisitions.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_tra` | Axial | ∥ hard palate | Hard palate → hyoid bone (~C3). Centre on oropharynx | **None** |
| 2 | `t1_tse_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_cor_fs` | Coronal | ⟂ hard palate | Anterior lips/oral tongue → past prevertebral muscles. Centre on oropharynx | **None** |
| 4 | `t2_tse_cor` | Coronal | Copy Slice from #3 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 5 | `resolve_4scan_trace_tra` | Axial | Copy Slice from #1 | — | **None** |
| 6 | `t1_vibe_fs_tra_C` | Axial | ∥ hard palate | Extended inferiorly vs pre-contrast. Centre on oropharynx | **None** |
| 7 | `t1_starvibe_fs_cor_C` | Coronal | ⟂ hard palate | Extended inferiorly vs pre-contrast. A/P: lips → past prevertebral. Centre on oropharynx | **None** |
| 8 | `MPR` | Sag+Ax | — | Whole volume | — |

*#7: StarVIBE = stack-of-stars radial VIBE. Motion-robust for swallowing artefact.*

---

## 3. Sequence Rationale

### Core Strategy

Oral cavity and oropharyngeal imaging requires assessment of the primary tumour (tongue, floor of mouth, tonsil, soft palate), mucosal extent, and nodal staging. All sequences use fat suppression or STIR — mucosal and nodal fat must be suppressed to distinguish enhancing tumour.

**`t2_stir_tra` (#1)**
T2 STIR axial. STIR provides uniform fat suppression across the oral cavity and oropharynx. Axial plane profiles the tongue base, tonsillar fossa, parapharyngeal space, and retropharyngeal nodes.

**Coverage:** Hard palate → hyoid bone (~C3), centred on the oropharynx. Superiorly, the hard palate separates the oral cavity from the nasal cavity. Inferiorly, the hyoid bone marks the boundary between the oropharynx and hypopharynx — extending to C3 includes the full tongue base, floor of mouth, and Level II nodes.

**`t1_tse_tra` (#2)**
Pre-contrast T1 TSE axial. Baseline for enhancement comparison. TSE avoids susceptibility artefact at the oropharyngeal air-soft tissue interface.

**`t2_tse_cor_fs` (#3)**
T2 TSE coronal with fat saturation. Coronal plane profiles the oral tongue, floor of mouth, and cervical nodes for symmetric comparison. FS suppresses mucosal fat.

**Coverage:** Anterior lips/oral tongue → prevertebral muscles, centred on the oropharynx. Anteriorly must include the lips and oral tongue surface — oral cavity SCC spreads along the mucosal surface. Posteriorly extends past the prevertebral muscles — the prevertebral space and retropharyngeal nodes must be fully covered.

**`t2_tse_cor` (#4)**
T2 TSE coronal without fat saturation. Pre-contrast anatomical reference — the non-fat-sat T2 provides natural tissue contrast for defining the tumour boundaries. Paired with FS coronal (#3) for complementary contrast.

**Contrast**
Standard dose IV gadolinium. DWI (#5) fills the post-injection delay. Target ~3–5 min before post-contrast T1.

**`resolve_4scan_trace_tra` (#5)**
RESOLVE DWI, 4-scan trace. Post-contrast — fills the enhancement delay. Oral cavity squamous cell carcinoma is cellular and shows restricted diffusion. 4 directions reduce directional bias.

**`t1_vibe_fs_tra_C` (#6)**
VIBE FS axial post-contrast. Enhancing tumour margin against suppressed mucosal fat.

**Coverage:** Larger than pre-contrast — extended inferiorly to cover the nodal drainage of oral cavity SCC (Levels I–IV). No vertex is needed: oral cavity perineural spread follows the lingual and inferior alveolar nerves which travel inferiorly toward the mandible, not superiorly.

**`t1_starvibe_fs_cor_C` (#7)**
StarVIBE FS coronal. Motion-robust radial acquisition — swallowing motion moves the pharyngeal wall vertically, in-plane coronally. StarVIBE's radial sampling converts motion ghosts to incoherent streaks. Coronal plane profiles the oral tongue, floor of mouth, and cervical nodes for symmetric comparison. MPR (#8) provides sagittal and axial reformats.

**Coverage:** Anterior-posterior: same as pre-contrast coronal (lips → past prevertebral muscles). Superior-inferior: extended inferiorly compared to pre-contrast for nodal coverage. No vertex is needed.

**`MPR` (#8)**
Multiplanar reconstruction from StarVIBE (#7). Sagittal and axial reformatted views.

---

## 4. Pathology-Based Variations

- **History of Ca tongue:** Pre-contrast, add `t2_tse_sag`. Sagittal is not needed for routine oral cavity imaging — the axial and coronal planes cover most primaries (floor of mouth, tonsil, retromolar trigone) adequately. For tongue primaries specifically, the tongue extends anterior-posteriorly and sagittal profiles the tumour along its long axis, showing the full anterior-posterior extent and depth of invasion in a single plane. Critical for surgical planning: the distance from tumour to tongue base determines partial vs total glossectomy.

- **History of larynx (primary of glottic, supraglottic, or subglottic carcinoma):** The standard oral cavity coverage centres on the oropharynx and stops at the hyoid (~C3) — it does not fully cover the larynx which sits lower (C4–C6). Laryngeal cartilage invasion is the key surgical question: if cartilage is involved, larynx preservation is not possible and total laryngectomy is required. The standard oral cavity sequences are insufficient for this assessment.

  Pre-contrast, add the following small-FOV sequences through the larynx:
  - `t2_stir_tra` — uniform fat suppression across the laryngeal cartilage
  - `t1_se_tra` — SE (not TSE) for sharper cartilage detail. TSE blurring from the turbo factor can obscure early cartilage invasion, which appears as a thin line of tumour signal crossing the cartilage
  - `t2_tse_fs_dixon_cor` + `t2_tse_fs_dixon_tra` — Dixon provides water-only (fat-suppressed T2 for tumour detection) and in/opposed phase images in one acquisition. In the larynx, in/opposed phase is valuable because laryngeal cartilage (thyroid, cricoid) ossifies with age: the typical laryngeal cancer patient has partially or fully ossified cartilage containing fatty marrow. Intact ossified cartilage shows signal dropout on opposed phase; tumour invasion replaces the fatty marrow and the dropout disappears. In non-ossified hyaline cartilage, T2 signal change and enhancement are the primary signs of invasion.
    - *Coronal:* profiles the laryngeal ventricle, true and false vocal cords, and the tumour-cartilage interface in cross-section.
    - *Axial:* profiles the anterior commissure (midline crossing → total laryngectomy), arytenoids, and paraglottic space (deep fat plane lateral to the vocal cord — invasion here upstages disease).

---

## 5. Comparison with NP Protocol

The oral cavity protocol shares the same structural design as `NP.md` — STIR/T1 axial, StarVIBE coronal, RESOLVE DWI, VIBE axial post-contrast — but is shifted anteriorly and inferiorly.

**1. Coverage and perineural spread:** Coverage moves from the nasopharynx/skull base down to the oropharynx and oral cavity. Perineural spread follows different routes: oral cavity tumours track along the lingual nerve and inferior alveolar nerve toward the mandible (inferiorly), not along V3 and the vidian nerve toward the vertex (superiorly). No vertex coverage is needed. Post-contrast coverage is extended inferiorly compared to pre-contrast for nodal drainage (Levels I–IV); the StarVIBE AP coverage follows the pre-contrast coronal boundaries.

**2. Addition of pre-contrast coronal:** NP does not need pre-contrast coronal — the nasopharynx is a deep midline mucosal space best assessed with post-contrast StarVIBE. Oral cavity tumours (tongue, floor of mouth) are different: the tumour margin against normal tongue musculature is best seen on T2, where tumour is hyperintense against intermediate-signal muscle. Enhancement alone can underestimate the tumour extent because the enhancing margin does not always match the T2-defined tumour boundary. The surgeon needs the T2 coronal for depth of invasion into the tongue, which determines the surgical approach.

**3. Why T2 FS + T2 non-FS:** T2 FS suppresses mucosal fat — tumour is bright against dark fat, optimal for lesion detection. T2 non-FS preserves natural tissue contrast — tongue musculature, fat planes, and anatomical boundaries are clearly seen. T1 coronal pre-contrast is not needed: T2 provides better soft tissue contrast for tongue and floor of mouth, and post-contrast T1 FS already covers enhancement assessment.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Motion** — |  |
| — Swallowing? | Swallowing moves the pharyngeal wall vertically — in-plane coronally on StarVIBE (#7), creating ghosts. Axial VIBE is perpendicular to this motion (through-plane only, milder). Instruct patient to breathe quietly and avoid swallowing |
| — Tongue movement? | Blurring on T2 coronal (#3, #4): compare tongue surface to stationary prevertebral muscles. On VIBE axial: ghost replicas of the tongue margin along the phase-encode direction. On StarVIBE: radial streaks from the moving tongue. Instruct patient to keep tongue still against the palate. If degraded: re-acquire |
| **Post-contrast** — contrast present? Confirm mucosal and nodal enhancement | If absent: check IV line, confirm injection |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-29 | — | Initial — 8 sequences + variations (Ca tongue, larynx) |
