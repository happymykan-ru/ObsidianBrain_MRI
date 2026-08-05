# MR Enteroclysis (MR Enterography with Contrast and Buscopan)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. The small bowel extends from the upper abdomen to the pelvis — two body coils stacked in landscape (upper abdomen + pelvis) or a single coil in portrait orientation for smaller patients.
- **Laser Landmark:** Mid-abdomen (umbilicus level). Split-FOV acquisition for abdomen and pelvis.
- **Verbal Instructions:** Breath-hold commands essential — reproducible hold at the same depth for all sequences.
  - **Inspiration:** if coronal FOV is limiting.
  - **Expiration:** if AP coverage is limiting.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].
- **Buscopan (Hyoscine butylbromide):** Two doses of 10 mg IV, timed with the protocol. Buscopan paralyzes bowel smooth muscle — abolishes peristalsis for the post-contrast dynamic phases. Contraindications: glaucoma, prostatic hypertrophy, myasthenia gravis, tachyarrhythmia. Confirm absence of contraindications before administration.
- **Oral Contrast:** [Confirm — mannitol solution, polyethylene glycol, or biphasic agent]. Ingested over ~45 min before scanning to distend the small bowel. The biphasic agent is dark on T1 and bright on T2, providing positive bowel-to-wall contrast on both sequences.

---

## 2. Imaging Series

### Pre-Buscopan — Motility Assessment

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_trufi_cor_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Entire small bowel | **Superior oblique** over heart | Free breathing |
| 2 | `t2_haste_cor_bh` | Coronal | True coronal | — | Copy Sat from #1 | Breath-hold |

*#1: TrueFISP coronal — survey. Bowel contents bright, free-breathing.*  
*#2: HASTE coronal — breath-hold anatomical reference.*  

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 3 | `t2_trufi_cor_1slice_bh_cine` (multiple) | Coronal | True coronal. Single slice per acquisition, repeated at multiple positions to cover the entire small bowel | One slice position per acquisition. Entire small bowel covered by multiple cine stations | **None** | Breath-hold per cine |

*#3: Motion study — single-slice TrueFISP cine at multiple positions across the small bowel. Each cine acquisition captures peristaltic activity at one location. Repeated at enough positions to assess motility throughout the entire small bowel. Performed BEFORE Buscopan — peristalsis must be assessable.*  

### Post-1st Buscopan — Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **1st Buscopan 10 mg IV** | — | — | — | — | — |
| 4 | `t2_fs_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 5 | `t2_haste_cor_bh` | Coronal | Copy Slice from #2 | — | Copy Sat from #1 | Breath-hold |
| 6 | `t2_tse_tra_fs_mbh_abdomen` | Axial | True axial | Mid-liver → iliac crest. Stacked to #7 for continuous coverage | **None** | Multi breath-hold |
| 7 | `t2_tse_tra_fs_mbh_pelvis` | Axial | Copy centre from #6 | Iliac crest → symphysis pubis. Stacked from #6 | **None** | Multi breath-hold |
| 8 | `t1_vibe_tra_p2_dixon_abdomen_bh` | Axial | Copy centre from #6 | Mid-liver → iliac crest. Overlap with #9 | **None** | Breath-hold |
| 9 | `t1_vibe_tra_p2_dixon_pelvis_bh` | Axial | Copy centre from #6 | Iliac crest → symphysis pubis. Overlap with #8 | **None** | Breath-hold |

*#4–#5: Post-Buscopan TrueFISP + HASTE — bowel is now paralysed. Repeat for comparison with pre-Buscopan images.*  
*#6–#7: Split-FOV T2 TSE FS — abdomen and pelvis. Bowel wall thickening, strictures, and inflammatory changes assessed.*  
*#8–#9: Split-FOV T1 VIBE Dixon — pre-contrast baseline. In/opposed phase for fat.*  

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **2nd Buscopan 10 mg IV** | — | — | — | — | — |
| 10 | `t1_vibe_fs_tra_abdomen_bh_pre` | Axial | Copy Slice from #8 | — | **None** | Breath-hold |
| 11 | `t1_vibe_fs_tra_pelvis_bh_pre` | Axial | Copy Slice from #9 | — | **None** | Breath-hold |
| 12 | `t1_vibe_cor_fs_bh_pre` | Coronal | True coronal | Entire small bowel | **None** | Breath-hold |

*#10–#12: Pre-contrast T1 FS — the 2nd Buscopan dose ensures maximal bowel paralysis for the dynamic phases. These serve as the pre-contrast baseline for subtraction/enhancement comparison.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency. Standard dose, 2 mL/s | — | — | — |
| 13 | `t1_vibe_cor_fs_bh_arterial_C` | Coronal | Copy Slice from #12 | Entire small bowel | **None** | Breath-hold. Fixed delay 30 s |
| 14 | `t1_vibe_fs_tra_abdomen_bh_PVP_C` | Axial | Copy Slice from #10 | — | **None** | Breath-hold, 20 s after #13 |
| 15 | `t1_vibe_fs_tra_pelvis_bh_PVP_C` | Axial | Copy Slice from #11 | — | **None** | Breath-hold, after #14 |
| 16 | `t1_fl2d_cor_fs_bh_C` | Coronal | Copy Slice from #12 | — | **None** | Breath-hold, after #15 |

*#13: Arterial phase — coronal. Enhancing bowel mucosa against the dark bowel lumen. Active inflammation = mucosal hyperenhancement.*  
*#14–#15: PVP — split-FOV abdomen + pelvis. Bowel wall enhancement pattern assessed: transmural enhancement (active Crohn's), mucosal-only enhancement (quiescent disease), or absent enhancement (fibrotic stricture).*  
*#16: FL2D coronal FS — high-resolution 2D mucosal assessment.*  

---

## 3. Sequence Rationale

### Core Strategy

MR enteroclysis assesses small bowel pathology — most commonly Crohn's disease activity, stricture characterization (inflammatory vs fibrotic), and complication detection (fistula, abscess, obstruction). The protocol combines motility assessment (TrueFISP cine) with anatomical imaging (T2, T1 Dixon) and contrast-enhanced assessment of bowel wall enhancement (arterial + PVP). Buscopan is essential — it abolishes peristalsis during the dynamic phases, preventing bowel motion from degrading enhancement assessment.

**Key differences from other abdominal protocols:**

- **TrueFISP cine for peristalsis** — before Buscopan, single-slice cine acquisitions at multiple positions assess small bowel motility. Reduced or absent peristalsis at a stricture site suggests a fibrotic component; normal peristalsis proximal to a narrowed segment confirms mechanical obstruction.
- **Buscopan timing** — two doses. The 1st dose stops peristalsis for the pre-contrast T2 and T1 Dixon (eliminating motion artefact from peristaltic bowel). The 2nd dose immediately before contrast ensures maximal paralysis during the dynamic phases, when bowel wall enhancement is assessed.
- **Split-FOV abdomen + pelvis** — the small bowel extends from the diaphragm to the pelvis. T2 TSE, T1 Dixon, and PVP sequences are each split into abdomen and pelvis stacks.
- **FL2D coronal FS post-contrast** — high-resolution 2D acquisition for mucosal enhancement detail. The coronal plane shows long segments of bowel in a single image.
- **No DWI** — peristaltic bowel degrades DWI; Buscopan helps but DWI is not part of the standard enterography protocol at many centres.

---

### Pre-Buscopan — Motility Assessment

**TrueFISP coronal (#1):** Free-breathing survey. Bowel contents are bright — confirms adequate oral contrast distension before proceeding. 

**HASTE coronal (#2):** Breath-hold anatomical reference. Sharper detail for strictures, fistulae, and abscesses. 

**TrueFISP cine (#3):** Multiple single-slice TrueFISP acquisitions in the coronal plane, each at a different position along the small bowel. TrueFISP has very short TR — each frame is essentially instantaneous. Cine acquisition captures peristaltic contractions over several seconds at each position. The entire small bowel is assessed station-by-station. Normal small bowel shows regular peristaltic contractions (propagating luminal narrowing); an inflamed segment shows hyperperistalsis or normal motility; a fibrotic stricture shows absent peristalsis with fixed luminal narrowing. Performed BEFORE Buscopan — peristalsis must be present to assess.

**Technique:** On the T2 HASTE coronal (#2), identify the most posterior slice where bowel is visible. Copy that image position. Press SCAN to generate the first cine slice pending positioning. Gap forward by twice the slice thickness (×2 gapping) to position the next station. Repeat until the entire small bowel is covered from posterior to anterior. This ensures systematic coverage of all bowel loops without overlap or gaps.

---

### Post-1st Buscopan — Pre-Contrast

The 1st Buscopan dose (10 mg IV) paralyzes bowel smooth muscle.

- **TrueFISP FS (#4) + HASTE (#5):** Coronal pair repeated. Side-by-side comparison with pre-Buscopan images distinguishes fibrotic strictures (narrowing persists after paralysis — structural) from transient peristaltic narrowing (disappears after Buscopan — was just a contracted segment). The cine (#3) shows peristalsis in motion; the pre/post coronal comparison shows whether a narrowing is fixed. TrueFISP is now FS — with motion abolished, suppressing fat improves bowel wall-to-lumen contrast without the motion penalty of the pre-Buscopan version. Both assess distension, fistulae, abscesses.

- **T2 TSE FS (#6, #7):** Split-FOV abdomen + pelvis. Fluid-sensitive — bowel wall oedema (T2-bright) is the hallmark of active inflammation. Normal bowel wall is thin and T2-dark; thickening >3 mm with increased T2 signal = active Crohn's. Also detects complications: fistulae (T2-bright tracts between bowel loops or to skin/bladder), abscesses (T2-bright collections with dark rim), and fixed luminal narrowing (fibrotic stricture — dark T2 wall due to collagen, no oedema). The split-FOV ensures the entire small bowel is covered from diaphragm to perineum.

- **T1 VIBE Dixon (#8, #9):** In/opposed phase for fat. Mesenteric creeping fat — the mesentery hypertrophies and wraps around inflamed bowel loops; signal dropout on opposed phase confirms the tissue is fat, not fibrosis or phlegmon. Fatty infiltration of the bowel wall itself may be seen in chronic disease. Not the enhancement baseline — that is #10–#12 at peak 2nd Buscopan.

---

### Post-2nd Buscopan — Pre-Contrast T1 FS

A 2nd Buscopan dose (10 mg IV) ensures maximal paralysis for the dynamic phases. Pre-contrast T1 FS (#10–#12) are the enhancement baseline — separate from Dixon (#8, #9) because they share the same FS technique and bowel state as the post-contrast phases.

---

### Post-Contrast

**Arterial phase (#13):** Coronal VIBE FS. Fixed delay 30 s. The enhancing bowel mucosa is bright against the dark lumen (biphasic contrast). Active inflammation shows mucosal hyperenhancement — a bright inner layer of the bowel wall. This is the hallmark of active Crohn's disease. The coronal plane shows long segments of bowel in one slice.

**PVP (#14–#15):** Split-FOV abdomen + pelvis. Bowel wall enhancement pattern determined:
- **Mucosal enhancement only** (inner layer bright, outer layer dark) = active but superficial inflammation
- **Transmural enhancement** (full-thickness bright) = severe active inflammation, fistulizing disease
- **No or minimal enhancement** = fibrotic stricture (poor/no enhancement on all phases)
- **Stratified enhancement** (mucosa and serosa bright, submucosa dark — target sign) = active Crohn's

**FL2D coronal FS (#16):** 2D FLASH acquisition — higher in-plane resolution than VIBE. Profiles bowel wall mucosal enhancement in the coronal plane with sharper detail than the 3D VIBE phases. Long segments of bowel are seen in a single coronal slice.

---

## 4. Variations

- **Non-breath-hold:** Replace breath-hold sequences with free-breathing equivalents:
  - T2 TSE FS (post-1st Buscopan) →
    `t2_fblade_fs_tra_p3_abdomen_non-bh`
    `t2_fblade_fs_tra_p3_pelvis_non-bh`
  - T1 VIBE Dixon  →
    `t1_tfl_tra_in-phase_abdomen_non-bh` / `t1_tfl_tra_opp-phase_abdomen_non-bh`
    `t1_tfl_tra_in-phase_pelvis_non-bh` / `t1_tfl_tra_opp-phase_pelvis_non-bh`
  - Pre-contrast T1 FS (post-2nd Buscopan) →
    `t1_starvibe_fs_tra_non-bh_abdomen_pre` / `t1_starvibe_fs_tra_non-bh_pelvis_pre`
    `t1_starvibe_fs_cor_non-bh_pre`
  - Arterial phase →
    `t1_starvibe_fs_cor_non-bh_arterial_C`
  - PVP →
    `t1_starvibe_fs_tra_non-bh_abdomen_PVP_C` / `t1_starvibe_fs_tra_non-bh_pelvis_PVP_C`
    `t1_starvibe_fs_cor_non-bh_PVP_C` (replaces FL2D)
  Buscopan timing and cine remain unchanged. See `liver_non-bh.md` for BLADE, TFL, and StarVIBE technique trade-offs.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Bowel distension** — Oral contrast reached the caecum on the first TrueFISP survey (#1)? | If contrast has not reached the caecum: the distal small bowel is not distended and cannot be assessed. Wait additional time and re-check the survey before proceeding to Buscopan |
| **Breath-hold consistency** — Same depth across all sequences? | Inspiration or expiration — whichever is chosen, maintain it for all sequences |
| **Split-FOV coverage** — T2 TSE (#6, #7) properly stacked without gap? T1 VIBE (#8, #9, #10, #11, #14, #15) overlapped sufficiently to avoid 3D slab boundary fall-off? | If gapped: a segment of small bowel is missed. |
| **Post-contrast** — Contrast present? Bowel mucosa enhancing on arterial phase? | If absent: check IV line, confirm injection. The bowel wall enhancement pattern is the primary diagnostic tool |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 16 sequences. TrueFISP cine motility + Buscopan ×2 + split-FOV abdomen/pelvis + arterial/PVP. FL2D coronal post-contrast |
