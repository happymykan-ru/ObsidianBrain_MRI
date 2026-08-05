# FIA (Fistula-in-Ano MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the symphysis pubis.
- **Immobilization:** Pelvic binder over the pelvic region.
- **Laser Landmark:** Symphysis pubis
- **Verbal Instructions:** Shallow breathing throughout. No breath-hold required — the pelvis is stationary.
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing requirement. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_stir_tse_cor_p2` | Coronal Oblique | ∥ anal canal | Perianal region. Center anal axis. Anal verge → above levator ani. Inferior border includes buttock margin. A/P: symphysis pubis → sacrum | **None** | Free breathing |
| 2 | `t2_stir_tse_tra_p2` | Axial Oblique | ⟂ anal canal | Perianal region. Center anus. Inferior coverage includes buttock margin | **None** | Free breathing |
| 3 | `t1_tse_tra_p2` | Axial Oblique | Copy Slice from #2 | — | **None** | Free breathing |
| 4 | `t1_vibe_dixon_tra_pre` | Axial Oblique | Copy Slice from #2 | — | **None** | Breath-hold |

*#1–#2: T2 STIR — fluid-sensitive, uniform fat suppression. Coronal oblique (parallel to anal canal) and axial oblique (perpendicular). Fistula tracks are T2-hyperintense against dark fat.*  
*#3: T1 TSE axial oblique — anatomical reference. The sphincter complex (internal and external anal sphincters) is profiled.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. Delay 2 min before scanning | — | — | — |
| 5 | `t1_vibe_dixon_tra_C` | Axial Oblique | Copy Slice from #4 | — | **None** | Breath-hold |
| 6 | `t1_vibe_dixon_cor_C` | Coronal Oblique | Copy Slice from #1 | — | **None** | Breath-hold |

*#5–#6: Post-contrast T1 axial + coronal oblique, delayed 2 min. Enhancing granulation tissue lines the fistula track. Abscesses show rim enhancement. The 2 min delay allows contrast to accumulate in the inflammatory tissue.*  

---

## 3. Sequence Rationale

### Core Strategy

Perianal fistula MRI maps the fistula track relative to the sphincter complex for surgical planning. The clinical question: what is the Parks classification of the fistula (intersphincteric, transsphincteric, suprasphincteric, extrasphincteric), where is the internal opening (at the dentate line), and are there secondary extensions or abscesses? The protocol combines fluid-sensitive T2 STIR (fistula track conspicuity) with delayed post-contrast T1 (granulation tissue enhancement).

All axial and coronal sequences are oblique — aligned perpendicular and parallel to the anal canal. The anal canal is angled anteriorly from the anorectal junction to the anal verge; true axial and coronal planes cut obliquely through the sphincters. Oblique planes give true cross-sections for accurate sphincter assessment.

---

### Pre-Contrast

**T2 STIR coronal oblique (#1):** STIR provides uniform fat suppression across the perineum — the perianal region has multiple air-skin interfaces where chemical FS would fail. The coronal oblique plane (parallel to the anal canal) profiles the entire sphincter complex, levator ani, and ischiorectal fossae in one view. The fistula track is T2-hyperintense against the dark suppressed fat. The internal opening at the dentate line and the relationship to the levator plate are assessed.

**T2 STIR axial oblique (#2):** Perpendicular to the anal canal. This is the primary plane for Parks classification. Each axial slice shows the anal canal in true cross-section — the internal sphincter (smooth muscle, intermediate signal), external sphincter (striated muscle, dark), and the intersphincteric plane (fat, bright on STIR suppressed to dark). A fistula track crossing the external sphincter = transsphincteric; confined to the intersphincteric plane = intersphincteric; above the levator ani = suprasphincteric. Secondary extensions and abscesses (T2-hyperintense collections) are identified.

**T1 TSE axial oblique (#3):** Anatomical reference. The sphincter complex is delineated on T1 with preserved fat planes — useful when STIR fat suppression obscures the intersphincteric plane boundaries. TSE avoids susceptibility artefact at the perianal air-skin interface.

**T1 VIBE Dixon (#4):** Pre-contrast baseline. Fistula tracks are not visible on pre-contrast T1 unless there is haemorrhage or proteinaceous content. The pre-contrast image is essential for distinguishing true enhancement from intrinsic T1-hyperintensity in the post-contrast images.

---

### Post-Contrast

**T1 VIBE Dixon axial + coronal oblique (#5, #6):** Delayed 2 min post-injection. The fistula track is lined with granulation tissue — this enhances avidly on post-contrast T1. A non-enhancing T2-hyperintense track on STIR that enhances on post-contrast T1 = active fistula. A non-enhancing track = chronic/quiescent fistula (mature fibrous track without active inflammation). Abscesses appear as rim-enhancing fluid collections. The 2 min delay allows contrast to accumulate in the inflammatory tissue — earlier phases may underestimate the extent of enhancement.

The coronal oblique (#6) provides an overview of the entire track from the internal opening to the external opening. The axial oblique (#5) sections the track at each level for sphincter relationship and Parks classification.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Oblique planes** — Coronal parallel to the anal canal? Axial perpendicular? | If true axial is used instead: the sphincters are cut obliquely — the intersphincteric plane is distorted and Parks classification is unreliable |
| **Post-contrast delay** — 2 min delay observed before scanning? | If scanned too early: granulation tissue enhancement is incomplete, underestimating the true extent of the fistula track |
| **Post-contrast** — Contrast present? Fistula track enhancing? | If absent: check IV line, confirm injection. A non-enhancing track on post-contrast may be chronic/quiescent — correlate with STIR signal |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 6 sequences. Oblique axial/coronal per anal canal. T2 STIR + T1 TSE + delayed post-contrast T1 Dixon. 2 min delay |
