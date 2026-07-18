# BLADE Brain (Motion-Robust Brain MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-07-18 | **Scanner:** [Confirm 1.5T/3T]

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
| 1 | `t2_blade_tra_p2` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_blade_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t1_blade_sag` | Sagittal | ∥ midline | [Confirm coverage] | **None** |
| 4 | `t2_dark_fluid_blade_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 5 | `resolve_3scan_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 6 | `t1_blade_tra_C` | Axial | Copy Slice from #1 | — | **None** |
| 7 | `t1_fs_blade_tra_C` | Axial | Copy Slice from #1 | — | **None** |
| 8 | `t1_vibe_fs_cor_CAIPIRINHA_4_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |

*#8 is optional. Add when coronal post-contrast coverage is needed and patient can tolerate the extra ~30 s.*

---

## 3. Sequence Rationale

### Core Strategy

BLADE (Siemens' PROPELLER) acquires overlapping radial blades rotating through k-space. Each blade is a low-resolution image — patient motion between blades is corrected by registering blades before final combination. The k-space centre is oversampled by every blade, improving SNR and providing intrinsic motion correction. This protocol is designed for patients who cannot stay still: tremor, confusion, paediatric, or emergency.

Unlike the ultra-fast protocol (all ~20 s sequences), BLADE uses diagnostic resolution — the time penalty of PROPELLER (each blade is a full echo train) is accepted in exchange for motion immunity.

### When to Use This Instead of contrast_brain or fast_brain

| Patient | Protocol | Rationale |
|---|---|---|
| Cooperative, routine | `contrast_brain` | Best image quality |
| Throughput / emergency | `fast_brain` | All ~20 s, lower resolution |
| Motion-prone / restless | `blade_brain` | Motion-immune, diagnostic resolution |

---

**`t2_blade_tra_p2` (#1)**
BLADE T2 axial with GRAPPA ×2. Rotating blades oversample the k-space centre — motion between blades is corrected blade-by-blade. p2 shortens the echo train without significantly degrading the radial oversampling benefit. Reference axial anatomy. Motion-robust replacement for `t2_tse_tra`.

**`t1_blade_tra` (#2)**
BLADE T1 axial. Pre-contrast T1 baseline. T1 BLADE provides diagnostic T1 contrast even with patient movement — a single head motion only degrades the blades acquired during that moment. Compares to post-contrast `t1_blade_tra_C` (#6) for enhancement. No sat band: sat pulse timing conflicts with radial trajectory.

**`t1_blade_sag` (#3)**
BLADE T1 sagittal. Adds a midline anatomical reference plane — corpus callosum, brainstem, cerebellar vermis, pituitary, and craniocervical junction. BLADE makes sagittal viable in a way conventional TSE cannot: in a motion-prone patient, sagittal TSE is the worst sequence because the phase-encode direction runs A/P, so head movement creates ghosting that propagates across the entire midline. BLADE's radial blades contain motion to individual blade times rather than propagating it — each blade is a low-resolution image, and only the blades acquired during movement are degraded. The result is a diagnostic sagittal in a patient where conventional sagittal TSE would be unreadable.

**`t2_dark_fluid_blade_tra` (#4)**
BLADE FLAIR axial. CSF-suppressed T2 with PROPELLER motion correction. FLAIR's long TR makes it the most motion-vulnerable sequence in any brain protocol — BLADE directly addresses this. Periventricular/cortical lesion detection without motion degradation.

**`resolve_3scan_tra_p2` (#5)**
RESOLVE (readout-segmented EPI) DWI with GRAPPA ×2. 3 orthogonal directions averaged to trace. RESOLVE's readout segmentation already reduces distortion vs single-shot EPI; p2 further shortens the echo train. Acquired pre-contrast. Fills the post-injection delay (~3–5 min) while providing diagnostic DWI.

**Contrast**
Standard dose IV gadolinium. ~5 min delay before post-contrast BLADE T1 sequences (#6, #7).

**`t1_blade_tra_C` (#6)**
Post-contrast BLADE T1 axial. Matches pre-contrast `t1_blade_tra` (#2) for enhancement comparison. BLADE's motion correction is most valuable here — post-contrast T1 in a restless patient without BLADE is frequently non-diagnostic. No coronal BLADE T1 post-contrast: each full BLADE acquisition adds several minutes of radial oversampling. In a motion-prone patient whose enhancement window is limited, the axial pair (#6, #7) is the priority — it preserves the pre/post comparison plane. Adding a diagnostic BLADE coronal risks the patient deteriorating mid-acquisition or the enhancement window closing.

**`t1_fs_blade_tra_C` (#7)**
Post-contrast BLADE T1 axial with fat saturation. Suppresses bright scalp and marrow fat, making peripheral and meningeal enhancement more conspicuous. The non-fat-sat (#6) and fat-sat (#7) serve different jobs: #6 matches the pre-contrast baseline (#2) with identical tissue contrast for a clean pre/post comparison — no fat suppression artefacts to confuse enhancement interpretation. #7 is the problem-solver — if something suspicious is seen at the periphery or near the dura, fat sat confirms whether it is true enhancement or just bright fat. In a motion-prone patient where re-acquisition is risky, acquiring both in one pass is safer than discovering later you chose wrong.

**`t1_vibe_fs_cor_CAIPIRINHA_4_C` (#8) — Optional**
Ultra-fast 3D T1 coronal post-contrast with CAIPIRINHA parallel imaging ×4. CAIPIRINHA (Controlled Aliasing In Parallel Imaging Results In Higher Acceleration) intentionally aliases slices and unaliases them using multi-coil sensitivity data — this allows much higher acceleration factors (×4) with significantly less SNR penalty than conventional GRAPPA at the same factor. 

*Why add this as an option?* BLADE's strength (motion immunity) is also its weakness (time cost) — a diagnostic BLADE coronal takes several minutes, which is why the core protocol (#6, #7) stays axial. But if the patient is tolerating the scan well and coronal post-contrast coverage is needed (skull base, sellar, meninges), this ultra-fast VIBE fills the gap in ~30 seconds. It is not diagnostic resolution — the CAIPIRINHA acceleration trades some SNR for speed — but it gives a fat-saturated coronal screening view that covers the anatomy BLADE axial cannot fully profile. Add when clinically indicated; omit if the patient is deteriorating or the enhancement window is closing.

## 4. Pathology-Based Variations

- **Acute stroke:** Consider adding MRA if DWI shows restricted diffusion
- **SWI:** Add if microbleed screening needed. SWI is not motion-robust; consider whether `ep2d_tra_hemo` (~20 s) is an acceptable compromise
- **Severe motion despite BLADE:** Omit fat-saturated T1 (#7) — the non-fat-sat BLADE (#6) is the priority post-contrast sequence

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack if any sequence is short |
| **BLADE sequences** — radial streak artefact? | Usually from undersampling — confirm p2 is not too aggressive. Reduce to p1 if present |
| **`t1_blade_tra_C`** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection, repeat if extravasation suspected |
| **Motion** — still present despite BLADE? | BLADE corrects inter-blade motion but severe continuous tremor may still degrade. Assess slice-by-slice and re-acquire only the worst sequences |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 8 sequences (BLADE-based + RESOLVE DWI) |
