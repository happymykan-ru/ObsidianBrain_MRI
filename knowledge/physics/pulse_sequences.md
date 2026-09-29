# Pulse Sequences & Physics — Knowledge Hub

**Version:** 1.0 | **Date:** 2026-09-08

> Why this exists: everything in `/protocols/` is built from a small set of Siemens pulse-sequence families. This knowledge base explains **what each family is, what contrast it produces, what it is good for, and what knobs you can turn** — the physics underneath your 81 protocol files. Protocol-specific parameters always override general ranges here ([hierarchy rule — CLAUDE.md]).

## How to read a Siemens sequence name

Sequence tokens in this vault follow a predictable pattern (Siemens console terminology, lowercase_with_underscores):

```
weighting_family_fatsat_plane          e.g.  t2_tse_fs_tra   → T2-weighted turbo spin echo, fat-saturated, axial
                                           t1_vibe_dixon_cor → T1-weighted VIBE with Dixon fat suppression, coronal
```

| Token fragment | Meaning |
|---|---|
| `t1 / t2 / pd` | Weighting |
| `tse / se / space / haste / blade` | Spin-echo family members |
| `fl2d / fl3d / vibe / trufi / starvibe` | Gradient-echo family members |
| `ep2d / resolve` | Echo-planar / segmented-EPI readouts |
| `mprage / mp2rage / tfl` | Magnetization-prepared gradient echo |
| `stir / tirm / flair / dark_fluid` | Inversion-recovery variants |
| `dixon` | Dixon fat–water separation |
| `fs` | Fat saturation (spectral) |
| `tra / sag / cor / sa / 4c` | Plane (axial / sagittal / coronal / short axis / 4-chamber) |
| `_p2 / _p3 / _p4` | GRAPPA (iPAT) acceleration factor |
| `_cs4 / _cs6` | Compressed sensing factor |
| `_C` | Post-contrast |
| `_dyn` | Dynamic (multiple frames) |
| `_bh / _mbh / _non-bh / _trig` | Breath-hold / multiple breath-hold / free-breathing / respiratory-triggered |
| `_iso` | Isotropic voxels (MPR source) |
| `_r` (e.g. `t1_tse_r`, `t2_tseR`) | Restore (driven-equilibrium) pulse |
| `_sms` | Simultaneous multi-slice (multiband) |
| `_rt` | Real-time |

Full reverse index: [[sequence_token_glossary]] — every token family → generic type → where it is used.

---

## Table A — Sequence quick reference: contrast & what it is good for

| Generic sequence | Family file | Contrast | Good for |
|---|---|---|---|
| Conventional SE | [[02_spin_echo_family]] | T1 / PD | Sharpest edges, no turbo blur → small structures (PNS, IAM, larynx) |
| TSE 2D (incl. dual-echo PD+T2) | [[02_spin_echo_family]] | T2 / T1 / PD | The workhorse — edema, lesions, marrow, soft tissue, every region |
| FLAIR | [[02_spin_echo_family]] | T2, CSF nulled | Periventricular/cortical lesions, MS, small-vessel disease, encephalitis |
| STIR / TIRM | [[02_spin_echo_family]] | T2, fat nulled | Marrow edema, inflammation, optic nerve, brachial plexus, near metal |
| DIR | [[02_spin_echo_family]] | T2, CSF+WM nulled | Cortical/gray-matter MS plaques |
| SPACE (3D TSE) | [[02_spin_echo_family]] | T2 / PD / T1 | Isotropic volumes + MPR; MRCP/MRU/myelography; prostate & pelvis |
| HASTE | [[02_spin_echo_family]] | Heavy T2 | Motion-immune snapshots — bowel, MRCP slabs, uncooperative patients |
| BLADE (PROPELLER) | [[02_spin_echo_family]] | T1 / T2 / PD | Motion-robust rescue — restless patients, liver without breath-hold |
| Restore (TSE-R) | [[02_spin_echo_family]] | T1/T2 + SNR | Thin slices (pituitary, IAM, rectum), bright-CSF lumbar spine |
| HASTE-DWI (non-EPI) | [[02_spin_echo_family]] | Diffusion | Cholesteatoma at petrous bone — 1.5T only (SAR) |
| FLASH (spoiled GRE 2D/3D) | [[03_gradient_echo_family]] | T1 | Fast T1, stereotactic geometry, contrast timing, breast dynamic |
| VIBE (3D spoiled GRE) | [[03_gradient_echo_family]] | T1 | Breath-hold 3D T1 — post-contrast brain, liver, DCE everywhere |
| MPRAGE / MP2RAGE | [[03_gradient_echo_family]] | T1 (prepared) | High-res gray–white anatomy; MP2RAGE = B1-uniform + quantitative T1 |
| Dixon | [[03_gradient_echo_family]] | Fat/water separated | Uniform fat suppression on any base sequence, wide FOV, lung apex |
| TrueFISP (bSSFP) | [[03_gradient_echo_family]] | Mixed T2/T1 | Bright fluid/blood — cine, bowel motility, non-contrast MRA, localizers |
| MEDIC (multi-echo GRE) | [[03_gradient_echo_family]] | T2*-family, bright CSF | Cord gray–white contrast, wrist/cartilage |
| T2* mapping | [[03_gradient_echo_family]] | Quantitative T2* | Iron overload (heart, liver) |
| SWI | [[03_gradient_echo_family]] | Susceptibility | Microbleeds, DAI, calcification vs hemorrhage, venous anatomy |
| StarVIBE (radial) | [[03_gradient_echo_family]] | T1 | Free-breathing multiphasic — dyspneic patients, liver, bowel |
| TWIST (view-sharing) | [[03_gradient_echo_family]] | T1 dynamic | Time-resolved MRA/MRV, AVMs, multi-arterial-phase liver |
| SR-TurboFLASH | [[03_gradient_echo_family]] | T1 (sat. recovery) | First-pass myocardial perfusion |
| EPI readout | [[04_epi_and_diffusion]] | T2* (fastest) | The readout under DWI/perfusion/fMRI; distortion is the cost |
| DWI / ADC (incl. RESOLVE) | [[04_epi_and_diffusion]] | Diffusion | Acute stroke, abscess vs necrosis, tumor cellularity |
| DTI | [[04_epi_and_diffusion]] | Diffusion tensor | White-matter tractography, MD/FA |
| DSC perfusion | [[04_epi_and_diffusion]] | T2* dynamic | Tumor rCBV, cerebrovascular reserve (Diamox challenge) |
| BOLD fMRI | [[04_epi_and_diffusion]] | T2* | Brain activation mapping (pre-surgical) |
| EPI T2* | [[04_epi_and_diffusion]] | T2* | Rapid hemorrhage screen |
| TOF MRA | [[05_angiography_and_flow]] | Inflow bright blood | Non-contrast arterial anatomy (circle of Willis, carotids) |
| Phase-contrast flow | [[05_angiography_and_flow]] | Velocity phase | Flow quantification — aorta, valve lesions, CSF |
| CE-MRA | [[05_angiography_and_flow]] | T1 + gadolinium | High-res arterial anatomy (renal, carotid, run-off) |
| NATIVE (non-contrast MRA) | [[05_angiography_and_flow]] | bSSFP bright blood | Renal arteries without contrast (renal failure/NSF) |
| TWIST MRA/MRV | [[05_angiography_and_flow]] | T1 dynamic | AVMs, venous congestion (May-Thurner), gonadal vein |
| MRCP / MRU (hydrography) | [[05_angiography_and_flow]] | Heavy T2 static fluid | Bile ducts, urinary tract, CSF leaks, ducts |
| Cine bSSFP | [[06_cardiac_sequences]] | Mixed T2/T1 | Wall motion, volumes, EF |
| PC flow (cardiac) | [[06_cardiac_sequences]] | Velocity phase | Valvular disease, shunt quantification |
| T1 mapping (MOLLI) | [[06_cardiac_sequences]] | T1 relaxometry | Diffuse fibrosis, ECV, amyloid |
| T2 mapping | [[06_cardiac_sequences]] | T2 relaxometry | Myocardial edema |
| T2* mapping (cardiac) | [[06_cardiac_sequences]] | T2* relaxometry | Cardiac iron overload |
| First-pass perfusion | [[06_cardiac_sequences]] | T1 dynamic | Stress/rest ischemia detection |
| LGE | [[06_cardiac_sequences]] | T1 post-null | Scar/fibrosis, viability, myocarditis (EGE) |
| MRS (sLASER CSI) | [[07_spectroscopy_and_functional]] | Chemical shift | Metabolite ratios — NAA, choline, lactate |
| ASL | [[07_spectroscopy_and_functional]] | Perfusion (labeled) | CBF without contrast — not yet in vault protocols |

---

## Table B — Options quick reference: the choice dictionary

Full physics + trade-offs per option: [[08_options_and_parameters]].

| Option family | Choices | Use when |
|---|---|---|
| Fat suppression | None · Fat Sat · SPAIR · water excitation · Dixon · TIRM | Uniformity vs speed vs B0/B1 robustness vs post-contrast timing |
| Acceleration | GRAPPA/iPAT (`p2-p4`) · CAIPIRINHA · SMS · compressed sensing | Time target; each carries an SNR and artifact price |
| Partial Fourier | 4/8 – 7/8 | Cut time without parallel imaging; HASTE is half-Fourier by design |
| Motion handling | Breath-hold · respiratory trigger · PACE · BLADE · radial · ECG gating · GMR | Patient capability decides; sequence support decides the tool |
| k-space ordering | Linear · centric · elliptical · TWIST view-sharing | Contrast-determining moment (CE-MRA peak, IR nulling) |
| SAR management | Refocusing FA cut · hyperechoes · variable FA (SPACE) · Low-SAR pulse | 3T, long echo trains, high duty cycle — SAR ∝ B0² |
| Metal artifact | WARP: high bandwidth · VAT · SEMAC · TIRM | Hip/shoulder prostheses, spine hardware |
| Reconstruction | Inline MPR · Prescan Normalize · Distortion Corr. · Dixon recon · ADC map · Deep Resolve | Turn raw data into diagnostic images automatically |
| Contrast timing | Care Bolus · Test Bolus · dynamic TWIST | CE-MRA triggering; multiphasic liver |
| Field strength | 1.5T vs 3T | SNR vs SAR vs susceptibility vs chemical shift vs T1 lengthening |
| SNR/time/resolution | Averages · matrix · FOV · slice thickness · bandwidth | The universal trade triangle — see file 08 |
| Platform | syngo MR versions · BioMatrix · AutoAlign · myExam Companion | What your console can actually do |

---

## Contents

| # | File | What it covers |
|---|---|---|
| 1 | [[01_physics_foundations]] | The primer — spins, relaxation, echoes, k-space, contrast logic |
| 2 | [[02_spin_echo_family]] | SE · TSE · FLAIR/STIR/TIRM/DIR · SPACE · HASTE · BLADE · Restore · HASTE-DWI |
| 3 | [[03_gradient_echo_family]] | FLASH · VIBE · MPRAGE/MP2RAGE · Dixon · TrueFISP · MEDIC · T2* · SWI · StarVIBE · TWIST · SR-TFL |
| 4 | [[04_epi_and_diffusion]] | EPI · DWI/ADC · DTI · DSC · BOLD · EPI T2* |
| 5 | [[05_angiography_and_flow]] | TOF · PC · CE-MRA · NATIVE · TWIST · MRCP/MRU |
| 6 | [[06_cardiac_sequences]] | Cine · PC · MOLLI · T2/T2* maps · perfusion · LGE |
| 7 | [[07_spectroscopy_and_functional]] | MRS · ASL |
| 8 | [[08_options_and_parameters]] | Fat suppression · acceleration · motion · k-space · SAR · metal · recon · contrast timing · field strength · platform |
| — | [[sequence_token_glossary]] | Reverse index: vault token family → generic type → file → regions |

**Suggested reading order:** 01 → 02 → 03 → 08, then the application files (04–07) as needed.

---

## Conventions used in these files

- **Siemens vocabulary only.** Generic Siemens names (`turbo spin echo`, `VIBE`, `TrueFISP`, `HASTE`, `SPACE`, `BLADE`, `RESOLVE`, `Fat Sat`, `SPAIR`, `TIRM`, `GMR`) — no GE/Philips translations. The vault is Siemens-terminology by rule (CLAUDE.md).
- Parameter values are recommended typical ranges where no protocol in this vault fixes the number; `[UNVERIFIED]` marks a value that could not be confirmed against ≥2 independent sources.
- **Institute protocols override general knowledge** — if a protocol contradicts a general range here, the protocol wins; flag the discrepancy rather than auto-correcting.
- Each family file ends with its key sources.

---
**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial knowledge entry — hub + 9 files |
