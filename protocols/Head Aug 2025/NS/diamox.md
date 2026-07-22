# Diamox (Acetazolamide-Challenged Cerebrovascular Reserve)

**Version:** 1.0 | **Date:** 2026-07-22 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 18G (green). Two contrast injections required (pre- and post-Diamox). Fixed injection rate: 4–5 mL/s for both DSC perfusion acquisitions. Saline flush: [Confirm volume].
- **Diamox:** 800 mg acetazolamide. Administer [Confirm: IV or oral?]. Peak effect at 10–15 min. [Confirm: contraindication screening — sulfonamide allergy, severe renal impairment, electrolyte disturbance.]

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_p3_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_flair_fs_cor_brain` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| [Opt] | `TOF_3D_multi-slab` | Axial | ∥ AC-PC line | Carotid siphon → above corpus callosum | **Superior** (venous flow) |
| — | **Contrast #1** | — | — | — | — |
| 4 | `ep2d_perf_pre_Diamox_C` | Axial | Copy Slice from #1 | Foramen magnum → vertex | **None** |
| 5 | `t1_vibe_fs_cor_brain_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 6 | `MPR` | Sag+Ax | — | Whole brain | — |
| 7 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |
| — | **Diamox 800 mg** | — | — | — | — |
| — | *Wait 10–15 min* | — | — | — | — |
| — | **Contrast #2** | — | — | — | — |
| 8 | `ep2d_perf_post_Diamox_C` | Axial | Copy Slice from #1 | Foramen magnum → vertex | **None** |

*#4 and #8: Inject contrast at 4–5 mL/s after the 10th measurement (same as DSC perfusion — see `GBM_DSC.md`). Two separate contrast injections are required.*

---

## 3. Sequence Rationale

### Core Strategy

Cerebrovascular reserve is the brain's ability to increase blood flow in response to a vasodilatory challenge. In steno-occlusive disease (carotid stenosis, moyamoya), the downstream vasculature is already maximally dilated to maintain perfusion at rest. Acetazolamide (Diamox) is a carbonic anhydrase inhibitor that causes cerebral vasodilation — normal vessels dilate and rCBV rises by 30–50%. Maximally dilated vessels cannot dilate further; rCBV stays flat or decreases (steal phenomenon). Two identical DSC perfusion acquisitions — one before and one after Diamox — are compared to produce the cerebrovascular reserve map.

**`t2_tse_tra_p3_brain` (#1)**
Core axial T2 anatomy. Reference plane. Established infarction, white matter disease, chronic small vessel change.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast T1 baseline. Matched to post-contrast (#7) for enhancement comparison.

**`t2_flair_fs_cor_brain` (#3)**
FLAIR FS coronal. Chronic white matter ischaemia and small vessel disease are the underlying substrate for impaired cerebrovascular reserve. Coronal plane profiles the periventricular and deep white matter. FS improves lesion conspicuity against scalp fat.

**`TOF_3D_multi-slab` [Optional]**
TOF MRA for the anatomical correlate — shows the steno-occlusive lesion (ICA stenosis, MCA occlusion, moyamoya collaterals). Optional because the diagnosis is often already established from prior imaging. See `cerebral_angiogram(no_brain_request).md` for TOF details.

**Contrast #1 — Pre-Diamox Perfusion**
Gadolinium at 4–5 mL/s. DSC perfusion (#4) captures the first-pass bolus. Post-contrast brain (#5–#7) follows.

**`ep2d_perf_pre_Diamox_C` (#4)**
DSC perfusion — baseline cerebrovascular state. EPI whole-brain every ~1–2 s, inject after 10th measurement. The rCBV map shows resting perfusion. In steno-occlusive disease, resting rCBV may be normal (compensated) or reduced (decompensated). For full DSC acquisition details, see `GBM_DSC.md`.

**`t1_vibe_fs_cor_brain_C` (#5) + `MPR` (#6) + `t1_fl2d_tra_brain_C` (#7)**
Standard post-contrast brain block. Enhancement, anatomical reference. Subtract pre (#2) from post (#7).

**Diamox 800 mg**
Acetazolamide inhibits carbonic anhydrase → increased CO₂ in brain tissue → cerebral vasodilation. Peak effect at 10–15 min after administration. [Confirm: route, contraindication screening.]

**`ep2d_perf_post_Diamox_C` (#8)**
DSC perfusion after Diamox challenge — identical acquisition to pre-Diamox (#4). Same slice position, same injection rate, same timing. The post-Diamox rCBV map is subtracted from the pre-Diamox rCBV map: regions where rCBV increased normally (>30%) have preserved reserve; regions where rCBV stayed flat or decreased (<10%) have impaired reserve or steal. This is the cerebrovascular reserve map — it identifies tissue at risk of future infarction if the steno-occlusive disease progresses.

**Contrast dose note:** Two separate injections of gadolinium are required. Total dose is double the standard brain dose. [Confirm: institutional policy on double-dose contrast for Diamox studies. Some centres use ASL perfusion for the challenge to avoid a second contrast dose.]

---

## 4. Alerts

| Check | Improve |
|---|---|
| **IV access** — 18G, well-sited, patent for two high-rate injections? | DSC requires 4–5 mL/s ×2. Test flush before starting |
| **Perfusion (#4, #8)** — identical slice position and geometry? | Post-Diamox perfusion must match pre-Diamox exactly. Use Copy Slice. Mismatched slices invalidate the reserve map |
| **Perfusion (#4, #8)** — dark blood visible on inline display? | Same as DSC — watch for vessel darkening during bolus. If no signal drop: check IV, confirm injection |
| **Diamox timing** — perfusion started 10–15 min after administration? | Peak vasodilation at 10–15 min. Scanning too early understimates reserve; too late may miss the peak |
| **Post-contrast** — contrast present on #5–#7? | Confirm enhancement. Contrast from the pre-Diamox perfusion also provides the post-contrast brain block |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-22 | — | Initial — 8 sequences + optional TOF (Diamox-challenged DSC perfusion ×2) |
