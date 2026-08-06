# Generic Pelvis (General-Purpose Pelvic MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-pelvis.
- **Immobilization:** Pelvic binder.
- **Laser Landmark:** Centre of body coil
- **Verbal Instructions:** Shallow breathing throughout. If breath-hold is difficult (pelvic pain, post-operative), the StarVIBE post-contrast sequences are motion-robust.
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_tse_sag` | Sagittal | True sagittal | Pelvis. Uterus + cervix + vagina. L/R: both adnexae | **None** | Free breathing |
| 2 | `t2_tse_tra` | Axial | True axial | Pelvis. Iliac crest → perineum | **None** | Free breathing |
| 3 | `t1_tse_dixon_tra` | Axial | Copy Slice from #2 | Pelvis | **None** | Free breathing |
| 4 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #1 | — | **None** | Free breathing |
| 5 | `resolve_diff_tra_b50_800` | Axial | Copy Slice from #2 | Pelvis | **A/P** (anterior + posterior skin margins) | Free breathing |

*#1–#2: T2 TSE sagittal + axial — anatomical survey of the uterus, ovaries, and pelvic structures.*  
*#3: T1 TSE Dixon axial — pre-contrast baseline. In/opposed phase. TSE avoids susceptibility at the vaginal air interface.*  
*#4: T2 SPACE sagittal — 3D T2 with isotropic MPR.*  
*#5: DWI b=50, 800 — pelvic screening for restricted diffusion (abscess, tumour, inflamed tissues).*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. No specific delay required | — | — | — |
| 6 | `t1_starvibe_fs_tra` | Axial | Copy Slice from #2 | Pelvis | **None** | Free breathing |
| 7 | `t1_starvibe_fs_cor` | Coronal | True coronal | Pelvis. A/P: symphysis → sacrum | **None** | Free breathing |

*#6–#7: Post-contrast StarVIBE FS axial + coronal. Motion-robust radial acquisition — suitable for patients who cannot breath-hold (pelvic pain, post-operative).*  

---

## 3. Sequence Rationale

### Core Strategy

This is a **general-purpose pelvic screening protocol** for non-oncological indications where a dedicated protocol is not required. It provides anatomical T2 in two planes, 3D T2 for multiplanar review, DWI for infection/inflammation screening, and post-contrast T1 for enhancement assessment. The base protocol is gender-neutral — it serves both male and female indications. The protocol is not optimized for any single pathology — it is adequate but not definitive.

**Indications where this protocol is appropriate:**

- Pelvic inflammatory disease / tubo-ovarian abscess (female) — DWI + post-contrast for rim-enhancing collections
- Post-operative assessment (both) — haematoma vs abscess vs seroma
- Undifferentiated pelvic pain (both) — structural cause screening
- Follow-up of known benign conditions (both)
- Anatomical survey where contrast is needed but enhancement kinetics are not required

**Indications where a dedicated protocol should be used instead:**

- Cancer staging (cervical, endometrial, rectal, ovarian, prostate) → dedicated protocol with oblique planes, DCE, and/or subtraction
- Ovarian / adnexal mass characterization (O-RADS MRI) → use the pathology variation below (add arterial-phase DCE)
- Fibroid mapping → `fibroid.md`
- Endometriosis (DIE) → `endometriosis.md`
- Pelvic floor / incontinence → `incontinence.md`
- PI-RADS prostate mpMRI → `prostate.md`

---

### Sequence Details

**T2 TSE sagittal (#1) + axial (#2):** Standard pelvic survey. The uterus, ovaries, bladder, and rectum are assessed. No oblique planes — true sagittal and true axial provide adequate anatomical coverage for screening.

**T1 TSE Dixon axial (#3):** Pre-contrast baseline with TSE readout — less susceptibility at the vaginal air interface than VIBE. In/opposed phase for fat and intrinsic T1 signal. This is the pre-contrast reference for enhancement assessment.

**T2 SPACE sagittal (#4):** 3D T2 with MPR — provides reformatted views in any plane from one acquisition. Supplements the 2D T2 for volumetric assessment of adnexal masses, uterine anomalies, and pelvic pathology.

**DWI (#5):** b=50, 800, axial. Screens for restricted diffusion: abscess (pus = highly restricted), inflamed adnexa (PID), or incidental tumour (ovarian, endometrial). Not definitive for cancer characterization but identifies areas that need further investigation.

---

### Post-Contrast

**StarVIBE FS axial + coronal (#6, #7):** Radial k-space acquisition — motion-robust, free-breathing. Chosen because this protocol targets patients with pelvic pain or post-operative status who may struggle with breath-holding. StarVIBE converts respiratory motion to radial streaks rather than coherent ghosts. The axial plane assesses adnexal enhancement, abscesses, and collections; the coronal plane profiles the pelvic sidewall and peritoneal reflections. No specific contrast delay is required — enhancement of inflammatory tissue and abscess walls is not time-critical.

---

## 4. Pathology-Based Variations

- **Ovarian / adnexal mass (O-RADS MRI):** Add TWIST Dixon arterial phase for enhancement curve analysis of solid components:
  - `t1_vibe_twist_dixon_tra_pre` — pre-contrast TWIST baseline (water-only)
  - `t1_vibe_twist_dixon_tra_art_5phase` — arterial 5-phase (fixed delay 30 s, TWIST view-sharing). Axial — the ovaries are profiled axially.
  - The existing post-contrast StarVIBE (#6, #7) serves as the delayed/equilibrium phase.

  O-RADS enhancement curve: type 1 = gradual persistent (benign fibroma), type 2 = plateau (indeterminate), type 3 = washout (suspicious malignant). The arterial phase is essential — without it, the earliest post-contrast time point is the delayed StarVIBE, and types 1 and 3 (both end at the same delayed signal) cannot be distinguished. A separate PVP phase is not needed — adnexal enhancement kinetics do not require a portal venous time point; the arterial + delayed pair is sufficient for curve classification.

- **Pelvic venous assessment:** Add time-resolved venous imaging:
  - `twist_pelvis_cor` — dedicated TWIST angiography sequence, coronal. The iliac veins, ovarian veins, and IVC run craniocaudally — the coronal slab puts the vertical axis in-plane, capturing the entire pelvic venous drainage in a single FOV. Multiple phases over ~3 min. 1st measurement = baseline; inject contrast after, remaining phases capture arterial through venous filling.
  - Indications: May-Thurner syndrome (left common iliac vein compression), pelvic congestion syndrome (ovarian vein reflux), pre-operative venous mapping, vascular malformation characterization.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Entire pelvis from iliac crest to perineum? Both adnexae included? | Reposition if clipped. Adnexal masses may extend superiorly — check that the ovaries and any large cysts are fully included |
| **Contrast** — Present? Enhancing structures confirmed? | If absent: check IV line. The pre-contrast T1 (#3) and T2 (#1, #2) may still be diagnostic for anatomical questions |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 7 sequences. General-purpose pelvic protocol. StarVIBE post-contrast for motion robustness. Not a substitute for dedicated protocols |
