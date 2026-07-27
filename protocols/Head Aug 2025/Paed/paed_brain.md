# Paediatric Brain (Age-Adapted Brain MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil — use the smallest coil that fits the child. A paediatric-specific coil is preferred if available.
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil. Additional immobilization (vacuum cushion, swaddling for infants) may be needed. For children unable to stay still, consider feeding/swaddling and natural sleep, or sedation per institutional protocol.
- **IV Access:** Age-appropriate gauge. Injection rate: [Confirm age/weight-based protocol]. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_3_echos_brain` *(<2yr)* / `t2_tse_tra_4mm` *(>2yr)* | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t1_mprage_cor_p2_brain` *(<2yr)* / `t1_mprage_cor` *(>2yr)* | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 4 | `MPR` | Sag+Ax | — | Whole brain | — |
| 5 | `resolve_3scan_trace_tra_p2` *(<2yr)* / `resolve_3scan_trace_tra` *(>2yr)* | Axial | Copy Slice from #1 | — | **None** |
| 6 | `t2_flair_fs_cor` | Coronal | Copy Slice from #3 | — | **Inferior** |
| — | **Contrast** | — | — | — | — |
| 7 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |
| 8 | `t1_vibe_fs_cor_brain_C` | Coronal | Copy Slice from #3 | — | **Inferior** |
| 9 | `MPR` | Sag+Ax | — | Whole brain | — |

*#6: Only if >1 year old. Before 1 year, myelination is too incomplete for FLAIR to be useful. Multi-echo T2 (#1) for <2yr provides multiple contrasts from a single acquisition for assessing the immature brain.*

---

## 3. Sequence Rationale

### Core Strategy

Paediatric brain imaging adapts to the developing brain. The key variables are myelination stage, brain size, and motion tolerance. Under 2 years, the brain is incompletely myelinated — sequences and parameters are adjusted accordingly. Over 2 years, the protocol converges toward the adult standard but retains paediatric-specific modifications.

**`t2_tse_tra_3_echos_brain` (<2yr) / `t2_tse_tra_4mm` (>2yr) (#1)**
<2yr: Multi-echo T2 acquires three echoes at different TEs from a single acquisition — equivalent to a PD + intermediate T2 + heavily T2-weighted sequence in one scan. Echo 1 (short TE) = proton density-like, good grey-white contrast. Echo 2 (intermediate TE). Echo 3 (long TE) = T2-weighted, CSF bright. In the immature brain, the long TE alone is insufficient — unmyelinated white matter is T2-bright and blends with grey matter; the short TE (PD) restores grey-white differentiation. Getting all three contrasts from one sequence is a major efficiency gain for an infant who may not tolerate multiple acquisitions. >2yr: Standard T2 TSE 4 mm — the brain is largely myelinated by age 2, and 4 mm matches the larger head size.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast T1 baseline — serves as the subtraction mask for post-contrast FLASH (#7). FLASH 2D is not the diagnostic T1 in this protocol — that role belongs to MPRAGE (#3). No sat band: short TR has no slack.

**`t1_mprage_cor_p2_brain` (<2yr) / `t1_mprage_cor` (>2yr) (#3)**
T1 MPRAGE coronal — the diagnostic T1 in this protocol. 3D high-resolution for grey-white differentiation in the developing brain. Unlike adult protocols where FLASH 2D carries the T1 diagnosis, paediatric brain relies on MPRAGE for cortical maturation and developmental assessment. <2yr: p2 shortens the acquisition for motion-prone infants. >2yr: standard MPRAGE.

**`MPR` (#4)**
Multiplanar reconstruction from MPRAGE (#3). Sagittal and axial reformatted views.

**`resolve_3scan_trace_tra_p2` (<2yr) / `resolve_3scan_trace_tra` (>2yr) (#5)**
RESOLVE DWI. Pre-contrast — ensures DWI is acquired early. Acute ischaemia, metabolic disease, encephalitis. <2yr: p2 reduces scan time and motion sensitivity. >2yr: standard.

**`t2_flair_fs_cor` (>1yr) (#6 — both pathways)**
T2 FLAIR with fat saturation, coronal plane. Only acquired if the child is older than 1 year. Before 1 year, white matter is incompletely myelinated and still T2-bright — a CSF-suppressed sequence provides little additional value because the white matter signal is similar to CSF anyway. After 1 year, FLAIR becomes useful for periventricular and callosal lesions. Coronal plane is chosen over axial for better periventricular and callosal assessment in children. Fat sat suppresses the bright scalp fat which is proportionally thicker in infants and young children.

**Contrast**
Standard dose IV gadolinium, age/weight-adjusted. Target ~5 min delay before post-contrast T1.

**`t1_fl2d_tra_brain_C` (#7 — both pathways)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map.

**`t1_vibe_fs_cor_brain_C` (#8) + `MPR` (#9 — both pathways)**
Post-contrast VIBE FS coronal with MPR — standard post-contrast brain block. Enhancing lesions, meningeal enhancement, infection.

---

## 4. Sequence Priority and Differences from Adult Brain

Paediatric patients have limited tolerance — the scan may end early. Sequences are ordered by clinical urgency, with the key paediatric modifications noted against the adult `contrast_brain` baseline.

**1. DWI (pre-contrast, unlike adult post-contrast delay):** The most critical sequence. Acute ischaemia, metabolic disease, and encephalitis are the questions that cannot wait. Runs first while the child is most settled.

**2. T2 axial (age-adapted):** Core anatomy. Under 2 years, multi-echo T2 gives three echo times from one acquisition — provides PD-like, intermediate, and T2 contrast simultaneously. The short TE (PD) restores grey-white differentiation lost on the long TE when white matter is unmyelinated and T2-bright. Over 2 years, standard 4 mm T2 suffices.

**3. MPRAGE — the diagnostic T1:** High-resolution 3D T1 for grey-white differentiation, cortical maturation, and developmental assessment. Unlike adult protocols where FLASH 2D carries the T1 diagnosis, here MPRAGE is the primary anatomical sequence. Pre-contrast acquisitions always run first — MPRAGE must be completed before contrast is given.

**4. Pre-contrast FLASH T1:** The subtraction mask. Lowest priority among pre-contrast sequences — the diagnostic T1 is already covered by MPRAGE. Included for enhancement comparison but can be sacrificed if time is short.

**5. FLAIR (>1yr only, coronal FS instead of adult axial):** Lesion detection. Omitted before 1 year — unmyelinated white matter and CSF are both T2-bright, so suppressing CSF adds nothing. After 1 year, coronal FS FLAIR profiles periventricular and callosal lesions better than adult axial.

**— If contrast has been given:** Post-contrast T1 (FLASH + VIBE) becomes urgent — enhancement patterns are time-dependent. Pre-contrast sequences should already be complete by this point.

**If the child becomes intolerant before contrast:** DWI + T2 + MPRAGE form an adequate non-contrast study. Omit contrast and all post-contrast sequences.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Age** — correct T2 selected? | <2yr: multi-echo T2. >2yr: standard T2 4mm |
| **FLAIR** — child >1yr? | If <1yr, omit #6. FLAIR before myelination adds no diagnostic value |
| **Coverage** — cerebellum fully included? | Check the 3D sagittal localizer — the paediatric cerebellum extends disproportionately lower than the cerebrum. Midline sagittal alone may underestimate the inferior extent |
| **Motion** — child restless? | Use shortest sequences first (Section 4). Technical strategies: reduce turbo factor on TSE to shorten echo train, increase parallel imaging (p2 on MPRAGE and DWI). For continuous slow motion (drift, tremor): consider BLADE for T2 and FLAIR — BLADE corrects inter-blade motion but adds scan time. For sudden jerky movements, BLADE does not help; pause and re-acquire when settled |
| **Post-contrast** — contrast present? Confirm enhancement | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-27 | — | Initial — 2 pathways (<2yr: 9 seq; >2yr: 9 seq) |
