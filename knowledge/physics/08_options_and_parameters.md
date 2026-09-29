# Options & Parameters — the Choice Dictionary

**Version:** 1.0 | **Date:** 2026-09-08

The sequence files (02–07) answer "what am I running?" This file answers the *console-level* questions: **"which fat suppression? how much acceleration? which motion tool? what bandwidth?"** Every section follows the same shape: what it does → how it works (physics in one paragraph) → the choices → when to pick what → which sequence families expose it.

Siemens console terminology is used throughout (verified against Siemens documentation): **Fat Sat** (not "SPIR" — a Philips name), **GMR** for flow compensation (not "Flow Comp"), **SMS** for multiband, **elliptical scanning** for elliptical-centric k-space, **Care Bolus**, **PACE**, **Prescan Normalize**, **TIRM**.

Values throughout are recommended typical ranges; items that could not be verified against two independent sources carry `[UNVERIFIED]`.

---

## 1. Fat Suppression

**What it does —** Removes the bright signal of fat so that (a) contrast enhancement, edema and fluid are not hidden next to fat, (b) chemical-shift ghosts/artifacts disappear, and (c) fat-vs-water questions (adrenal, marrow) become answerable.

**How it works — five mechanisms, only two of which are "frequency-selective":**

| Option | Physics in one line | B₀ sensitivity | B₁ sensitivity | Post-contrast safe? | Cost |
|---|---|---|---|---|---|
| **Fat Sat** (spectral presat, CHESS-class) | A ~100–110° pulse tuned to the fat resonance saturates fat before the readout | **High** — mistuned off-center/at edges → fat not suppressed or water suppressed | medium | yes | fast, low SAR |
| **SPAIR** (adiabatic spectral IR) | Adiabatic 180° inverts fat; readout at fat's null TI → fat gone regardless of B₁ | High (still spectral) | **low (adiabatic)** | yes | +SAR, slower |
| **Water excitation** | Spatial-spectral pulse excites only water; fat is never tipped | high | medium | yes | short TR preserved |
| **Dixon** | Two echoes at opposed + in-phase; water = ½(IP+OP), fat = ½(IP−OP) computed per pixel | **low** (measured, not assumed) | low | yes | +TE window; fat–water swap risk (mechanism: §2) |
| **TIRM / STIR** | Inversion + TI at fat's null — suppresses by **T1**, not frequency | **none** | none | **NO** (nulls short-T1 tissue too) | low SNR |

**When to pick what —**

- **Post-contrast T1** where B₀ is decent: Fat Sat (fast) or SPAIR (uniform) — never TIRM.
- **Wide FOV, off-center anatomy, lung apex, brachial plexus, abdomen at 3T**: Dixon — the vault's default for body T1/T2 (its in/opposed echoes come free).
- **Skull base, sinuses, orbits, perineum, near metal, low field**: TIRM/STIR — where spectral fat sat *cannot* work (the vault's explicit pattern: STIR at skull base/sinuses, TIRM near metal and in whole-spine composition).
- **Metal-adjacent**: TIRM only (Dixon and spectral methods fail inside the field disturbance).
- **Fat–water *quantification*** (fat fraction, PDFF): Dixon or multi-echo methods — see §2 and file 03.

**Failure modes to recognize —** Fat Sat/SPAIR *under-suppress* where B₀ drifts (off-center FOV, diaphragm, implants) and *over-suppress* (dark water!) when mistuned the other way; Dixon *swaps* fat and water (dark rims everywhere — the signature); TIRM darkens enhancing tissue and proteinaceous fluid (file 02 entry 3). Respiratory motion can break SPAIR's steady state — triggering and SPAIR need care together.

**Supports —** TSE/SPACE/HASTE, FLASH/VIBE (SPAIR or Dixon), TrueFISP (needed at 3T for chemical-shift banding), EPI-DWI (SPAIR standard — file 04), TOF, LGE (epicardial fat).

---

## 2. Dixon — Fat–Water Separation

**What it does —** Computes a **water-only** and a **fat-only** image per pixel from one acquisition — plus the raw in-phase (IP) and opposed-phase (OP) images it was computed from. Four outputs, one scan. Unlike the RF-based methods in §1, Dixon never suppresses fat with a pulse: it acquires two echo states and *subtracts* the fat away — the separation is measured, not assumed.

**The core arithmetic — identical in every Dixon:**

```
IP = W + F         OP = |W − F|        (W = water signal, F = fat signal)
Water = (IP + OP)/2        Fat = (IP − OP)/2
```

Everything else about Dixon is only *how the two phase states are produced* — and there GRE and spin echo are opposites:

**In GRE, the two states come free from the chemical shift.** Nothing refocuses between excitation and readout, so fat and water — precessing ~220 Hz apart at 1.5T, 440 Hz at 3T — drift through one full relative cycle at a fixed rate. Every TE therefore lands at a predictable phase state: **opposed at 2.38 ms (1.5T) / 1.15–1.23 ms (3T), in-phase at twice that (4.76 / 2.3–2.46 ms)**. A dual-echo GRE simply reads one echo at each TE inside the same TR — the only cost is a longer TR.

**The GRE weakness — the swap.** The phase measured at the echo is not purely the fat–water shift: any B₀ offset (imperfect shim, susceptibility, air) adds its own phase, and the magnitude OP image hides the sign of (W − F). Two-point GRE-Dixon therefore cannot always distinguish "fat at +180°" from "water at −180° of B₀ phase" — where the field is bad it mislabels pixels: the fat–water **swap** (dark rims everywhere). Three-point and multi-echo Dixon (q-Dixon, 6 echoes) measure the B₀ phase to remove the ambiguity, and additionally model fat's multiple spectral peaks to yield a true **fat fraction (PDFF)** plus R2\*.

**In spin echo, the 180° pulse erases the very thing GRE-Dixon relies on.** This is the confusing case: the refocusing pulse exists to rewind *everything* accumulated since excitation — including the fat–water phase difference. At every correctly timed spin echo, fat and water are in phase **by construction**: there is no opposed-phase TE to schedule, because at any TE the echo finds them rephased. SE-Dixon therefore **breaks the perfect echo on purpose**. The phase difference at the echo centre is Δφ = Δω·(TE − 2·t₁₈₀) — zero for a CPMG-timed echo, where the 180° pulse sits at TE/2. Shift the refocusing pulse (in a train: the whole pulse train relative to the readouts) by δ, and a net phase **−2·Δω·δ** survives at every echo — a shift of only ~1.1 ms at 1.5T (~0.6 ms at 3T) converts an in-phase echo into an opposed-phase one. The sequence acquires two engineered echo states (in-phase train + opposed-phase train) and runs the same (IP ± OP)/2 arithmetic.

**Why anyone pays for that:** the 180° pulses also refocus B₀ inhomogeneity. In GRE the B₀ phase is what causes swaps; in SE-Dixon the engineered phase is *purely* the chemical shift, so there is no B₀ ambiguity to mislabel — the separation stays correct exactly where GRE-Dixon and spectral fat sat fail: steep field gradients (lung apex, thoracic inlet, off-center wide FOV).

**The price:** two echo states cost either a second acquisition or a lengthened echo train — scan time, SAR, more T2 decay and blur; and the shifted echo is no longer a perfect spin echo, so a trace of T2\* weighting leaks into the T2 image.

**Choices —**

| Flavor | Echo source | Outputs | Pick when |
|---|---|---|---|
| 2-point GRE | Two echoes per TR | water, fat, IP, OP | Body T1 — the default |
| Multi-echo GRE (q-Dixon, 3–6 echoes) | Three or more echoes per TR | + B₀-corrected, fat fraction (PDFF), R2* | Fat–water *quantification* |
| 2-point SE (TSE) | Two engineered echo states (shifted refocusing train) | water, fat, IP, OP | T1/T2 where B₀ is hostile |

**Sequence families that expose it —** GRE side: VIBE (dual-echo) and TWIST-Dixon — file 03. SE side: TSE and TSE3D Dixon.

**Failure modes —** the swap on 2-point GRE where B₀ is bad (signature: dark rims, water-bright structures going dark); motion between the echo pair smears the computed separation; and the two-point arithmetic assumes fat is a single resonance — fine for suppression, approximate for fat fraction (q-Dixon's multi-peak model is the fix).

---

## 3. Parallel Imaging & Acceleration

**What it does —** Acquires fewer k-space lines and uses coil-array sensitivity information to reconstruct the missing ones. Scan time ÷R. Everything in the vault's tokens (`p2/p3/p4`, `CAIPIRINHA`, `cs4/cs6`, `sms`) is some flavor of this.

**How it works —** Four distinct families:

| Tool | Mechanism | Where it shines |
|---|---|---|
| **GRAPPA** (iPAT) | k-space: skip lines; reconstruct missing lines from *autocalibration* (reference) lines using coil correlations | The clinical default, any sequence |
| **mSENSE** | Image domain: unfold the aliased image using coil sensitivity maps from a reference scan | SENSE-style alternative under the iPAT umbrella |
| **CAIPIRINHA** | 2D (slice × in-plane) *controlled aliasing* pattern for 3D — shifts the aliasing so the g-factor drops | 3D VIBE/SPACE (the vault's `CAIPIRINHA_4`) |
| **SMS (multiband)** | Excites N slices at once (multiband RF); separates them with blipped-CAIPIRINHA phase offsets | DWI/DTI/fMRI volumes (the vault's `sms`) |
| **Compressed sensing (CS)** | *Incoherent* undersampling (random/spokes) + iterative reconstruction enforcing sparsity | CS cine, CS SPACE, CS TOF, radial DCE (GRASP) |

**The price — one equation:**

```
SNR_accelerated = SNR_full / (g · √R)      R = acceleration factor, g = geometry factor ≥ 1
```

Time ÷R but SNR ÷√R, and the g-factor worsens where coil sensitivities overlap least (image center with surface arrays, thick 3D slabs). GRAPPA R2 costs ~29% SNR; R3–4 is for SNR-rich protocols. **The second, less obvious benefit:** on EPI, R also divides the *effective echo spacing* — parallel imaging shrinks distortion, not just scan time (file 04 entry 1). That is why your DWI runs p2/p3 even when time is not the constraint.

**Choices —** factor 2 routine (3T brain often 3); CS factors higher (cs4–cs6 in the vault's 3D TSE/TOF); SMS factor 2 for clinical DWI/DTI (3 degrades quality in most product guidance).

**Failure modes —** Residual aliasing when g is poor (center of large FOVs); calibration errors from motion between reference and accelerated scan; CS "washout" of small lesions if the sparsity model over-regularizes — CS factors beyond the product's validated range are not free.

---

## 4. Partial Fourier & Elliptical Scanning

**What it does —** Exploits k-space *conjugate symmetry* to skip up to half the phase-encode lines (partial Fourier) and the corners of 3D k-space (elliptical scanning). Time savings without parallel imaging.

**How it works —** A real image has conjugate-symmetric k-space: the line at −k_y is the mirror of +k_y. Acquire >half (e.g. 6/8 or 5/8) and synthesize the rest. The extra beyond half is not wasted — it provides a *low-resolution phase map* so the synthesis can correct the phase errors that break perfect symmetry (motion, eddy currents). Below ~5/8 the phase estimate degrades → ringing.

**Choices —**

| Fraction | Time saved | SNR | Notes |
|---|---|---|---|
| 7/8 | ~12% | ×0.94 | gentle |
| **6/8** | 25% | ×0.87 | the recommended default |
| 5/8 | ~38% | ×0.79 | HASTE's engine (file 02) — ringing risk below this |

Elliptical scanning zero-fills the 3D k-space corners (~21% time saving, tiny diagonal-resolution cost). Same name family but different purpose: *elliptical-centric ordering* in CE-MRA (file 05) is an acquisition *order*, not a saving — don't confuse the two.

---

## 5. Motion Management

**What it does —** Fights the two motions MRI cannot ignore: respiration (abdomen/thorax/heart) and voluntary movement (everyone). Strategy depends on whether motion is *periodic* (respiratory, cardiac — can be gated/synchronized) or *irregular* (patient motion — must be frozen, corrected, or made artifact-immune).

**The toolbox —**

| Tool | How it works | Best for | Fails when |
|---|---|---|---|
| **Breath-hold** | Acquire during apnea (VIBE 15–25 s; HASTE <1 s/slice) | Cooperative patients, short sequences | Dyspnea, children, long 3D |
| **Respiratory triggering** (bellows — PERU/PMU) | Belt signal gates acquisition to end-expiration (~20% of max signal) | Triggered TSE/SPACE in abdomen, MRCP | Irregular breathing, belt displacement |
| **PACE** (navigator) | Real-time navigator: 2D diaphragm FLASH (~100 ms) or 1D pencil beam (cardiac); acceptance ±3 mm; free-breathing pattern learning | 3D body/cardiac, NATIVE, fMRI (3D-PACE for head) | Poor navigator placement |
| **BLADE** | Rotating-blade redundancy → *retrospective* motion correction (file 02) | Restless patients, orbit, abdomen without BH | Through-plane motion (rejected, not corrected) |
| **Radial (StarVIBE, GRASP)** | Every spoke through center → motion *averages* into blur | Free-breathing dynamic body | Streak artifacts, longer min scans |
| **ECG gating** | Prospective (trigger after R-wave, fixed window — dark blood, LGE) vs retrospective (continuous + phase sorting — cine) | All cardiac | Arrhythmia (rejection or real-time CS) |
| **GMR (flow compensation / gradient-moment rephasing)** | Zeroes the first gradient moment at the echo → constant-velocity spins rephase | CSF/pulsation ghosts, 2D TOF, SWI (built-in), long-TR TSE | Lengthens minimum TE |

**Ghosting physics in one line —** motion during the *phase-encode* steps of cartesian k-space appears as ghosts shifted along the phase axis (each line was acquired at a different motion state); motion during the *readout* only blurs. Hence: swap phase-encode to push ghosts away from the anatomy of interest, and use saturation bands to kill the *source* of pulsatile signal (vessels, bowel) rather than fighting the ghost.

---

## 6. k-space Ordering & View Sharing

**What it does —** Decides *when* each part of k-space is sampled within the scan — which decides when the contrast-determining moment (bolus peak, inversion null, cardiac phase) lands in the image.

**The ordering families —**

| Ordering | Center sampled | Use |
|---|---|---|
| Linear | mid-scan | Robust default; TSE/T1 anatomy |
| Centric | first | CE-MRA (catch the peak), inversion-recovery LGE/T1 (sample right after prep), shortest effective TE |
| Elliptical-centric | first (center-out in 3D) | CE-MRA — venous suppression |
| View sharing (TWIST) | every frame (A region); periphery shared (B) | Time-resolved MRA/DCE — file 03 entry 9 |

**The rule that explains all of it —** k-space center = contrast. Any sequence with a *transient* contrast (contrast bolus, magnetization prep, cardiac phase) must schedule center sampling to coincide with that transient; any sequence with steady contrast can use any order. The classic failure — CE-MRA started too early — is a *center-timing* failure (Maki artifact, file 05), not a contrast failure.

---

## 7. SAR Management

**What it does —** Keeps the RF energy deposition (specific absorption rate, W/kg) inside regulatory limits. SAR is the ceiling that most 3T protocol design bumps against.

**The physics —** SAR ∝ (flip angle)² × duty cycle × **B₀²**. Moving 1.5T → 3T quadruples SAR before anything else changes. Limits (IEC 60601-2-33, whole-body): **Normal mode 2 W/kg, First Level 4 W/kg** (6-min average; head 3.2 W/kg) — First Level requires explicit operator confirmation on the console.

**The levers, in order of preference —**

| Lever | Effect | Cost |
|---|---|---|
| Lower refocusing flip angle (180° → 120–150°) | SAR ÷~2 | mild contrast/signal change |
| **Hyperechoes / variable-FA trains (hyperTSE, SPACE)** | 65–70% SAR cut (hyperTSE), matched contrast | SPACE's native design (file 02) |
| Longer TR / fewer slices | duty cycle down | scan time up |
| Shorter echo trains | fewer refocuses per TR | turbo factor down |
| Low-SAR RF pulse type | longer, gentler excitation pulse | longer minimum TE |

**Why some sequences are field-locked —** the vault's HASTE-DWI is explicitly 1.5T-only: diffusion gradients + SPAIR + ~100-refocus single-shot trains exceed 3T limits. TrueFISP flip angle caps at ~35–45° at 3T vs ~70° at 1.5T for the same reason. The console computes worst-case "Look Ahead" SAR and refuses to start sequences over the limit — a first-level push-through requires explicit operator action, and should be rare in protocols that respect the field.

---

## 8. Metal Artifact Reduction (WARP)

**What it does —** Recovers diagnostic signal around implants (hip/shoulder prostheses, spine hardware), where the implant's susceptibility shifts local B₀ by thousands of Hz. Mechanism of the artifact: near metal the field is *both* offset (→ in-plane pixel shift along readout, the "signal pile-up/void" crescent) and spatially varying (→ through-plane distortion — adjacent slices' anatomy is excited into the wrong plane, the "potato chip" artifact that no in-plane fix touches).

**The tools (Siemens bundles them as WARP) —**

| Tool | Mechanism | What it fixes |
|---|---|---|
| High readout bandwidth | Pixel shift ∝ Δf / BW — wider BW shrinks the in-plane shift | In-plane distortion (SNR ÷√BW is the price) |
| **VAT** (view-angle tilting) | Readout gradient tilted along the slice direction → through-plane field errors are encoded into the readout and cancel | Residual in-plane distortion at high shifts |
| **SEMAC** | Extra phase-encoding steps in the slice direction resolve the through-plane signal displacement, then re-sort it | Through-plane distortion (the big one) — time ×(SEMAC steps) |
| TIRM fat suppression | T1-based — immune to the B₀ shift that kills spectral fat sat | Fat signal around metal |

**Choices —** SEMAC steps scale with implant ferromagnetism (titanium ~3+, stainless steel needs more — the vault's hip protocols set 8–10 steps); bandwidth 500–1000+ Hz/pixel on SEMAC sequences; 1.5T is kinder than 3T for metal work (artifact scales with B₀) — the vault keeps metal-tolerant protocols on TIRM + SEMAC, and titanium implants are far more forgiving than steel.

**Failure modes —** Nothing recovers signal *inside* the immediate implant artifact (the void stays — the goal is the surrounding tissue); SNR drops with high bandwidth; scan time grows with SEMAC steps; VAT assumes a known slice geometry (oblique planes weaken it).

---

## 9. Reconstruction & Post-Processing

**What it does —** Turns raw k-space into the diagnostic images and maps — partly on the console, inline, before you look at anything.

| Tool | What it does | When it matters |
|---|---|---|
| **Inline MPR** | Auto-reformats of 3D source datasets | Every SPACE/VIBE/MPRAGE volume (file 02/03) |
| **Prescan Normalize** | Coil-sensitivity normalization from the body-coil reference prescan — removes the brightness falloff of surface arrays | EPI/Diffusion/body — standard; avoid with large metal or if the patient moved between prescan and scan |
| **Distortion Correction (DIS2D/DIS3D)** | Corrects *gradient-nonlinearity* distortion (image warping from imperfect gradients) | Large FOV/off-center; **not** the EPI susceptibility correction — that needs blip-up/down pairs + field maps (file 04) |
| **Dixon reconstruction** | Water/fat/IP/OP from one dual-echo acquisition (+ fat fraction, R2* in multi-echo q-Dixon) | Every `_dixon` token in the vault |
| **ADC map** | Inline monoexponential fit from the b-value pair | Every diffusion protocol — read ADC, not just high-b |
| **Deep Resolve** (AI reconstruction, XA50A+) | Trained networks: *Gain* (denoise), *Boost* (raw-data CNN for high acceleration), *Sharp* (resolution), *Swift Brain* (<2 min multi-contrast brain) | TSE (incl. SPACE/Dixon-TSE), HASTE, EPI-DWI — not MPRAGE (per FDA 510(k) K213693) |
| **Inline T2*/T1/T2 maps** | Relaxometry fits (files 03/06) | MyoMaps, T2StarMap, T1 map |

**The general principle —** anything quantitative (ADC, T1/T2/T2\*, PDFF) is only as good as its input images: the reconstruction amplifies what the acquisition corrupted. Normalize before you compare intensities across the FOV; correct distortion before you measure.

---

## 10. Contrast Timing Tools (CE-MRA and DCE)

**What it does —** Synchronizes the diagnostic acquisition with the contrast bolus. Full physics in file 05 entry 3; summary of the console tools:

- **Care Bolus** — real-time 2D monitoring (~1 image/s) with an ROI on the target vessel; the 3D auto-starts at a signal threshold. One injection, no math. (Vault: kidney and carotid CE-MRA.)
- **Test Bolus** — 1–2 mL test dose, dynamic series, measure arrival time T_p; delay the diagnostic scan so k-space center hits the peak (linear: T_d = T_p + T_center/2 − T_acq/2; centric: T_d = T_p − T_center). (Vault: kidney and carotid variants.)
- **Dynamic TWIST** — no timing at all: capture every phase at ~1–3 s/frame (files 03/05).
- **Delayed phases** — the vault's excretory urography (2/5/10/15 min) and hepatobiliary (20 min) phases extend the same contrast injection into washout/excretion windows — the *time after injection*, not the sequence, defines what the image shows.

---

## 11. Field Strength — 1.5T vs 3T

**What changes with B₀ — and what you must re-tune:**

| Property | 1.5T | 3T | Consequence |
|---|---|---|---|
| SNR | 1 | ~1.7–2× | Resolution/averages headroom — or shorter scans |
| SAR | 1 | ~4× (∝ B₀²) | The binding constraint: TSE/TrueFISP/HASTE design (this file §7) |
| T1 of tissues | shorter | ~20–30% longer | TR/TI/FA must be *re-set*, not copied: FLAIR TI 2000–2200 → 2200–2500 ms; fat-null 150–180 → 200–220 ms; T1w TR lengthens |
| T2 | ~unchanged | ~unchanged | T2 contrast mostly portable |
| T2* | longer | shorter (∝ B₀) | GRE/SWI/EPI more lossy: SWI TE 40 → ~20 ms; BOLD TE ~40 → ~30 ms; DSC more sensitive — but dropout worse |
| Chemical shift (fat–water) | 220 Hz | 440 Hz | In/opposed TEs halve (2.38/4.76 → 1.15–1.23/2.3–2.46 ms); fat ghosts twice as far on EPI — SPAIR mandatory |
| Susceptibility | mild | pronounced | Metal artifacts bigger (metal work favors 1.5T); banding on TrueFISP needs shorter TR/shim; MP2RAGE/StarVIBE partly exist to fight the consequences |
| Blood T1 | longer (for ASL, angiography background suppression) | shorter | NATIVE/TIRM nulls shift |

**Decision rules of thumb —** 3T for neuro (resolution, BOLD, MRA background suppression), MSK small joints, breast, prostate; 1.5T for metal, lung/air-adjacent, HASTE-DWI, cardiac T2\* (product-locked), and SAR-hostile sequences; both for abdomen (3T SNR vs 3T artifacts — your protocols already carry `_3T`-specific variants like the TSE3D MRCP substitute). Never copy a parameter table across field without re-deriving TI/TR/FA.

---

## 12. Resolution, SNR & Time — the Trade Triangle

**The universal equation (cartesian, before acceleration):**

```
SNR ∝ (voxel volume) × √(averages × phase lines) / √(readout bandwidth)

Time ∝ TR × phase lines × averages / (turbo × parallel × CS × SMS factors)
```

| Knob | SNR | Time | Resolution | Side effects |
|---|---|---|---|---|
| Matrix ↑ (smaller pixels) | ↓ (÷√2 per axis) | ↑ | ↑ | — |
| Slice thinner | ↓ | — | ↑ (z) | T2* losses at 3T |
| Averages ↑ | ↑ √N | ↑ N | — | motion blur if patient moves |
| Bandwidth ↑ | ↓ 1/√BW | ~↓ (shorter readout/TE) | — | chemical shift ↓; min TE ↓ (helps GRE) |
| FOV ↓ (same matrix) | ↓ | ↓ | ↑ in-plane | wrap-around — oversample the phase axis or saturate |

**The practical loop —** set resolution by the *diagnostic question* (small structure → small voxel), then buy back SNR at 3T with shorter scan, or buy time at 1.5T with acceleration, then *check the artifact budget* (blur from turbo factor, distortion from EPI, banding from TrueFISP). Every "free lunch" in this file (parallel imaging, CS, SMS, partial Fourier, radial, BLADE) trades one of the three corners or moves an artifact somewhere else — the art is knowing which currency the sequence can afford to spend.

---

## 13. Platform & Automation (syngo MR)

**What it is —** The operating system and feature set of the scanner itself, which determines *which of the above options exist at all* and how much is automated.

**Version lineage** (for reading protocol notes): VE11 (= syngo MR E11, 2014) → **XA10 (2018)** → XA11/XA12 → XA20 → XA30/31 → XA40 → XA50/51 (2021–23, Deep Resolve arrives) → XA60/61 (2024) → XB10 emerging. Many options discussed in this file (RESOLVE, DTI, TWIST, NATIVE, CS, Deep Resolve, MyoMaps, WARP) are licensed product options — presence on the console is not guaranteed by the software version alone.

**Automation features worth knowing** (some present in the vault's workflows): **BioMatrix** wireless respiratory/heartbeat sensors in the coils; **AutoAlign/AutoFoV** geometry automation; **Select&GO** AI table positioning; **myExam Companion** on XA; inline "Normalize," MPR, relaxometry and ADC maps (this file §9). Post-processing beyond the console runs on **syngo.via** (a separate server platform — tractography, cardiac flow analysis, spectroscopy evaluation).

---

## Key sources — Siemens Healthineers (iPAT and PACE white papers; WARP documentation; Turbo Suite; Deep Resolve FDA 510(k) K213693; syngo RESOLVE/DTI/NATIVE/TWIST pages; Magnetom World protocols); mriquestions.com (fat suppression [SPAIR vs SPIR](https://www.s.mriquestions.com/spair-v-spir.html), [operating modes/SAR](https://www.s.mriquestions.com/operating-modes.html), [partial Fourier](https://ratio.mriquestions.com/phase-symmetry.html), [phase symmetry](https://ratio.mriquestions.com/phase-symmetry.html)); papers: Griswold GRAPPA (MRM 2002), Breuer CAIPIRINHA (MRM 2006), Weigel/Hennig hyperechoes (MRM 2006), SEMAC/VAT review (PMC6024442); IEC 60601-2-33.

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — 12 option families; Dixon fat–water separation section added (§2, sections renumbered to 13) |
