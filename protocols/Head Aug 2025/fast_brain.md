# Fast Brain (Ultra-Fast Brain MRI with Contrast)

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
| 1 | `t2_tse_tra_p3` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_dark_fluid_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `ep2d_diff_3scan_trace_p2` | Axial | Copy Slice from #1 | — | **None** |
| 5 | `ep2d_tra_hemo` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 6 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |
| 7 | `t1_fl2d_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **None** |
| 8 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 9 | `t1_vibe_fs_tra_C` | Axial | Copy Slice from #1 | — | **Inferior** |

*All sequences are ~20 s each. Total scan time: ~5 min including contrast injection.*

---

## 3. Sequence Rationale

### Core Strategy

Every sequence in this protocol is approximately 20 seconds. Speed is achieved through high parallel imaging (p2, p3), low spatial resolution, and single-shot acquisitions where possible. This is a throughput/emergency protocol — not a replacement for standard contrast_brain, but sufficient to rule out major pathology and triage patients.

### How Speed Is Achieved

| Sequence | Mechanism | ~Time |
|---|---|---|
| `t2_tse_tra_p3` | GRAPPA ×3 cuts phase-encode steps by 2/3 | ~20 s |
| `t1_fl2d_tra` | 2D FLASH — inherently fast (short TR, slice-by-slice) | ~20 s |
| `t2_dark_fluid_tra` | Single-shot or accelerated TSE FLAIR | ~1min 20 s |
| `ep2d_diff_3scan_trace_p2` | Single-shot EPI, 3 directions, p2 | ~20 s |
| `ep2d_tra_hemo` | Single-shot EPI | ~50 s |
| `t1_fl2d_tra_C` + `t1_fl2d_cor_C` | 2D FLASH — two planes | ~20 s each |
| `t1_vibe_fs_cor_C` + `t1_vibe_fs_tra_C` | Ultra-fast 3D VIBE — low res, high BW, high GRAPPA | ~20 s each |

---

**`t2_tse_tra_p2` (#1)**
Turbo spin echo with GRAPPA ×2. Core axial T2 anatomy — edema, gliosis, white matter disease. p2 shortens the echo train, reducing scan time and motion sensitivity.

**`t1_fl2d_tra` (#2)**
Pre-contrast 2D FLASH axial. Fast, motion-insensitive (slice-by-slice). Baseline T1 reference matched in geometry to post-contrast FLASH (#6) for enhancement comparison. No sat band: short TR has no slack.

**`t2_dark_fluid_tra` (#3)**
CSF-suppressed T2 FLAIR axial. Periventricular and cortical/subcortical lesion detection. Fast variant — single-shot or high acceleration.

**`ep2d_diff_3scan_trace_p2` (#4)**
Single-shot EPI DWI. 3 orthogonal directions averaged to trace image with GRAPPA ×2. Single-shot = immune to inter-shot motion. p2 reduces echo train → less distortion. Susceptibility distortion at skull base is expected — document if it obscures the posterior fossa.

**`ep2d_tra_hemo` (#5)**
Ultra-fast T2*-weighted EPI for haemorrhage screening. Single-shot, long TE, magnitude-only. Replaces full SWI (~4 min) when speed is critical — but with trade-offs: no phase mask (no susceptibility amplification), lower spatial resolution, and coarser slice thickness. SWI maps microbleeds and deep veins at ~1 mm isotropic with phase-enhanced contrast; ep2d_hemo rules out large bleeds but may miss small microbleeds. Acquired pre-contrast to avoid contrast leakage mimicking blood products.

**Contrast**
Standard dose IV gadolinium. Post-contrast sequences (#6–#9) begin immediately. Target ~3 min from injection to post-contrast T1.

**`t1_fl2d_tra_C` (#6) & `t1_fl2d_cor_C` (#7) — Ultra-fast FLASH**
Two-plane 2D post-contrast T1. Both ~20 s, slice-by-slice, no fat sat. FLASH provides clean T1 with good gray-white contrast — #6 matches pre-contrast (#2) for subtraction/enhancement comparison; #7 adds a quick coronal anatomical reference.

**`t1_vibe_fs_cor_C` (#8) & `t1_vibe_fs_tra_C` (#9) — Ultra-fast VIBE**
3D T1 with fat saturation, ~20 s each, coronal + axial. 

**Why two-plane ultra-fast VIBE instead of one-plane standard VIBE (~2.5 min, contrast_brain)?**
 Standard VIBE gives one diagnostic-quality coronal in 2.5 minutes. Two ultra-fast VIBEs give coronal and axial coverage in ~42 seconds total — the speed comes from low resolution, high GRAPPA, and high bandwidth. Neither plane is diagnostic resolution, but two screening planes cover more anatomy than one high-res plane: coronal for skull base/sellar/meningeal enhancement, axial for standard pre/post comparison. The diagnostic post-contrast detail comes from FLASH (#6, #7).

**Why both FLASH and VIBE post-contrast?**
Both are T1-weighted but at ~20 s they trade resolution for complementary contrast. FLASH: gray-white differentiation, anatomy. VIBE FS: fat suppressed, enhancement conspicuity. No single ~20 s sequence does both — four looks across two planes and two contrast mechanisms in ~80 seconds.

---

## 4. Pathology-Based Variations

- **Acute stroke / no haemorrhage concern:** Omit `ep2d_tra_hemo` (#5)

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack if any sequence is short |
| **`t2_tse_tra_p2`** — SNR adequate with p2? | If noisy, reduce to p1 — scan time increases |
| **`ep2d_tra_hemo`** — susceptibility dropout at skull base? | Document for radiologist |
| **`t1_vibe_fs_cor_C`** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection, repeat if extravasation suspected |
| **Total scan time** — patient tolerating? | Abort remaining if patient deteriorating |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 9 sequences, all ~20 s |
