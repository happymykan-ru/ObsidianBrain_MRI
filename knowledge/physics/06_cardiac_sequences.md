# Cardiac Sequences

**Version:** 1.0 | **Date:** 2026-09-08

Cardiac MRI adds one constraint no other region has: **the heart beats**, and each beat moves the anatomy. Every cardiac sequence is built around the answer — synchronization to the ECG:

- **Prospective triggering** — the scanner waits for the R-wave, then acquires a fixed window (used when a specific phase is wanted: dark blood, LGE).
- **Retrospective gating** — data are acquired *continuously* and sorted by their position in the cardiac cycle afterward (used for cine — nothing is missed, arrhythmic beats can be rejected).
- **Segmentation** — only a few k-space lines per heartbeat (segments/views per segment), repeating over many beats until the image is filled.

And almost everything runs in a **breath-hold** or under respiratory gating, because the heart also rides the diaphragm.

The physics of the sequences themselves is mostly borrowed from files 02 and 03: the **cine** is TrueFISP (balanced SSFP), **dark blood** is double-inversion TSE, **LGE** is inversion-prepared GRE. What is *new* here is cardiac-specific physics: how the steady state and gating interact (cine), how relaxometry sequences count heartbeats (MOLLI schemes), and why LGE needs a "null" rather than "bright."

Values throughout are recommended typical ranges — your protocols win where they conflict.

---

## 1. Cine — bSSFP (TrueFISP) with Retrospective Gating

**What it is —** Balanced SSFP (file 03, entry 4) run continuously through the cardiac cycle; each cardiac phase (frame) is reconstructed from the k-space lines acquired *at that phase* across many heartbeats. Tokens: `cine_tfi_retro_*` (and the real-time/CS variant `cine_trufi_cs_rt_adapt_*`).

**Contrast & good for —** The bright-blood functional study: wall motion, cavity volumes, ejection fraction, valve morphology — typically 2-chamber, 3-chamber, 4-chamber, LVOT, and a short-axis stack for volumetry. Blood is bright (T2/T1 of balanced SSFP), myocardium intermediate, and the blood–myocardium boundary is crisp.

- **Physics deep-dive — how a movie is assembled from many beats, and why arrhythmia matters.**

    - A single heartbeat lasts ~800 ms; a k-space line needs only ~3 ms of data — but one line per heartbeat would take ~130 beats (2 minutes) per slice per frame. The cine trick is **segmentation + retro-gating**:

    - 1. **Segmentation:** each heartbeat acquires several k-space lines — the *views per segment* (VPS, typically 4–16) — all within the same short window of the cycle (same cardiac phase). Temporal resolution = VPS × TR (~30–50 ms).
    - 2. **Retrospective gating:** the scanner records each line's position within its heartbeat (from the ECG), then *after* acquisition sorts all lines into ~20–40 phase bins spanning the cycle and reconstructs one image per bin. Because data were collected continuously, even phases with few samples (diastasis) get filled over enough beats — and beats whose length deviates too far from the running average (**arrhythmia rejection**, typically ±10–20%) are discarded rather than corrupting the sort.

    - Frame count ≈ RR-interval / (VPS × TR) — shorter TR or fewer VPS → more frames but longer scan. The balanced steady state needs *short, regular* TR (banding — file 03) which is why TrueFISP rather than FLASH dominates cine: FLASH at 3T would need 2–3× longer TR for the same brightness.

    - **When gating fails — the real-time rescue.** Severe arrhythmia (atrial fibrillation with changing R-R) defeats retro-gating: no two beats match, and the sort smears. The vault's **real-time CS cine** (`cine_trufi_cs_rt_adapt_*`) drops gating entirely: continuous balanced-SSFP frames at ~30 ms temporal resolution, with **compressed sensing** reconstructing each frame from heavily undersampled data — free-breathing, arrhythmia-immune, and good enough for volumes/EF in the patient where gated cine fails (accept slightly lower spatial/temporal fidelity).

**Tunable choices —**

*Temporal behavior*

| Knob | Typical value | Turning it… |
|---|---|---|
| Views per segment | 4–16 | Fewer = finer temporal resolution, longer scan |
| Frames per cycle | ~20–30 (up to 40) | More phases = smoother movies, longer scan |
| Arrhythmia rejection | ±10–20% of mean R-R | Tighter = cleaner images, slower scan in irregular rhythms |
| Gating | retrospective (function) vs prospective (anatomy) | Retro = no phase missed; pros = shorter, but misses end-diastole |

*Signal & contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| Flip angle | 1.5T ~70°; 3T 35–45° (SAR) | TrueFISP regime — file 03 |
| TR | shortest (~2.5–3.5 ms) | Banding spacing ↑, steady state stable |
| Slice stack | short-axis from base to apex | Volumetry needs contiguous slices covering both valves |

**Artifacts & pitfalls —** Banding (shim, short TR); arrhythmia smearing (rejection window, or real-time rescue); through-plane motion of the base between slices (volumetry error — the basal slice moves in and out of the plane; standard short-axis planning and contouring rules exist to handle it); off-resonance fat brightening (fat suppression when needed).

**Used in this vault —** The standard views (2/3/4-chamber, LVOT) and short-axis volumetry stack with retro-gating; the HCM variant adds a 3-chamber stack; real-time CS cine is the arrhythmia/rescue protocol.

---

## 2. Cardiac Phase-Contrast Flow (cine PC)

**What it is —** Phase-contrast (file 05, entry 2) repeated per cardiac phase with retrospective gating: a through-plane velocity map across the vessel at every phase of the cycle. Tokens: `flow_*_retro_bh_ao` (VENC 150, step-up 400).

**Contrast & good for —** Flow quantification: aortic net flow and **regurgitant fraction** (valve disease), shunt quantification (Qp:Qs from pulmonary vs aortic flow), and velocity measurement across stenoses.

**Physics — what the numbers mean, and how to get them right.** Each cardiac phase yields a phase map whose pixel values are velocities (file 05). The reading is: contour the vessel lumen (usually the aorta at the sinotubular junction), multiply velocity × lumen area per phase → flow per phase → integrate over the cycle → net flow per beat. In aortic regurgitation, diastolic flow is negative; regurgitant fraction = (reverse flow / forward flow). Two cardiac-specific pitfalls: **VENC must exceed the peak systolic velocity** (aorta ~150 cm/s typical; stenotic jets need step-up VENC ~400 — if the velocity map shows inverted *central* pixels in systole, that is aliasing, reacquire higher); and through-plane motion of the *valve plane* (the aorta moves with the heart) adds error — the measurement plane should sit a few cm distal to the valve.

**Tunable choices —** (VENC, views per segment, through-plane orientation — full table in file 05, entry 2.)

**Artifacts & pitfalls —** Aliasing (above); background phase errors from eddy currents and concomitant gradients (static-tissue correction mandatory); turbulent flow dephasing at the valve underestimates peak velocity; breath-hold vs free-breathing with multiple averages (the vault's `_bh` and `_epat` variants trade breath-hold length against averaging).

**Used in this vault —** Aortic flow in the standard cardiac protocol (VENC 150 with step-up 400), with LVOT placement discussion in the HCM protocol for gradient measurement.

---

## 3. T1 Mapping — MOLLI

**What it is —** A relaxometry sequence: repeated single-shot TrueFISP images at **different inversion times**, fitted pixelwise to the T1 recovery curve → a **T1 map** (color-coded, milliseconds per pixel). Siemens: MOLLI (Modified Look–Locker Inversion). Tokens: `t1_map_*` — native (no contrast) and post-contrast (short-T1 scheme), including the stress variant `t1map_nativestress`.

**Contrast & good for —** The quantitative "tissue characterization" tool: **native T1** detects diffuse fibrosis, amyloidosis (T1 ↑↑), edema, and storage disease; **ECV** (extracellular volume fraction, from native + post-contrast T1 and hematocrit) quantifies the extracellular space — fibrosis and amyloid. Unlike LGE, it sees *diffuse* disease that has no bright scar to contrast against.

- **Physics deep-dive — why MOLLI counts heartbeats, and what the scheme notation means.**

    - Measuring T1 needs samples of the recovery curve at several times after an inversion. Two constraints collide: the whole heart moves with every beat, so each *sample* must be a single-shot image at one point in the cycle (usually diastole, ~once per heartbeat); and after an inversion the magnetization needs ~5 × T1 (~5 s) to recover before the next inversion. The **scheme notation N(p)M** encodes the compromise:

      ```
      5(3)3  =  5 images after inversion #1, 3 recovery beats (pause), 3 images after inversion #2
      → 8 sample points across 2 inversions, total ~11 heartbeats (~12–15 s breath-hold)
      ```

    - Native (no contrast) T1: **5(3)3** — 8 samples, fits the longer native T1s well.
    - Post-contrast T1: the tissue T1 is much shorter after gadolinium, so the scheme compresses: **4(1)3(1)2** — more samples early (where the curve bends), fewer late.
    - **Heart-rate adaptation:** at high heart rates the fixed pause of 3 beats is too long (recovery overshoots and the later samples are wasted); scanners use an adaptive scheme where the pause is computed from the measured R-R — your protocol's `5(6)3` notation is this adaptive form with a 6-beat pause at the patient's actual rate (in AF, schemes like 5(3)3 mis-sample; adaptive/HR-dependent versions restore accuracy).

    - The fit itself is a three-parameter monoexponential (amplitude, offset, T1) — the offset accounts for imperfect inversion — done inline with motion correction (HeartFreeze) because the single-shot images sit at slightly different cardiac phases.

    - **ECV** — the clinically most useful number — is a ratio of T1 changes, not an absolute:

      ```
      ECV = (1/T1_post − 1/T1_native)_myocardium ÷ (1/T1_post − 1/T1_native)_blood  × (1 − hematocrit)
      ```

    - The hematocrit correction matters: contrast distributes only in plasma, so the blood T1 change is diluted by red cells.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Scheme | native 5(3)3; post-Gd 4(1)3(1)2; adaptive 5(n)3 | Sample placement vs breath-hold length (above) |
| Readout | single-shot bSSFP, diastolic | The "one image per heartbeat" engine |
| Slice / coverage | 1–3 slices per breath-hold | More slices = more breath-holds |
| Native + post pair | needed for ECV | ECV = the ratio of both (formula above) |
| Heart-rate adaptation | on (AF, tachycardia) | Restores accuracy when fixed pauses mis-sample |

**Artifacts & pitfalls —** Motion between the single-shot images (inline motion correction helps; gross motion ruins the fit); off-resonance/banding inside the myocardium (shim!); T1 values are field-strength specific (**normal myocardium ~950–1050 ms @1.5T, ~1150–1230 ms @3T** — always compare against field-matched normal values); the post-contrast timing matters (T1 rises as contrast washes out — acquire at a fixed, documented time); fat within the voxel biases the fit.

**Used in this vault —** Native T1 mapping (multiple views + pathological site), the stress-reactivity native T1 variant, and post-contrast short-T1 mapping for ECV; the HCM and amyloid-class protocols extend placements and schemes (adaptive 5(6)3-style). Always read against field-matched normals — file 08 field-strength table.

---

## 4. T2 Mapping

**What it is —** Myocardial T2 measured by **T2-prepared single-shot bSSFP**: a T2-prep module (90° – [180° – 180°] – 90°) imparts T2 weighting *before* the readout, run at several prep durations, and the signal decay across prep times fits T2. Token: `t2_map_trufisp_sax`.

**Contrast & good for —** **Myocardial edema** (acute inflammation, myocarditis, acute infarction, transplant rejection): T2 is elevated wherever free water accumulates. Its advantage over T2-weighted *images* (dark-blood TIRM) is quantifiability and reproducibility — no reader judgment of "bright vs dark."

**Physics — why T2-prep instead of a long TE?** In a single-shot readout you cannot wait a long TE — the image would be one blurred snapshot of decayed signal (and T2 decay during the long EPI/bSSFP readout would add blur and off-resonance sensitivity). The T2-prep module does the waiting *before* the readout: a 90° tips magnetization to the transverse plane, a pair of 180°s refocus it for a defined duration (the *prep time*, e.g. 0 / 24 / 55 ms), a −90° returns the surviving magnetization to +z, and a spoiler kills the rest. Signal then depends on e^(−prep/T2), and the single-shot readout captures it instantly — so three separate acquisitions at prep times 0, 24, 55 ms give three points on the decay curve → pixelwise monoexponential fit → T2 map. Because each prep time is a separate scan, **motion between prep scans** (different heartbeats) is the main error source — inline registration matters. Normal myocardial T2 ≈ 52 ms @1.5T, ≈ 46 ms @3T.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Prep times | 0 / 24 / 55 ms (product standard) | The three curve samples |
| Readout | single-shot bSSFP, diastolic | Snapshot per heartbeat |
| Fit | monoexponential, inline map | T2 = decay constant |

**Artifacts & pitfalls —** Motion between prep scans; banding/off-resonance (shim); partial volume with blood (dark-blood prep variants exist); T2 elevation is not specific (edema vs blood pool — read with the T2w images and clinical context).

**Used in this vault —** Short-axis myocardial T2 mapping for edema assessment (myocarditis, acute injury).

---

## 5. Cardiac T2\* Mapping (iron)

**What it is —** Multi-echo GRE relaxometry (file 03, entry 6) applied to the myocardium: 8+ echoes from ~2 to 18 ms (1.5T), monoexponential fit → T2\* map. Tokens: `fl2d5_10echo_heart`, `T2StarMap_*`.

**Contrast & good for —** **Myocardial iron overload** (transfusional siderosis, thalassemia): myocardial T2\* < 20 ms is abnormal, and the value grades severity (20–14 mild, 14–10 moderate, <10 ms severe — the threshold that drives chelation therapy). Unlike liver iron (biopsy-able, R2\*-based), myocardial iron *requires* this MRI measurement — it is the clinical gatekeeper.

**Physics — why the heart needs its own variant.** Same physics as file 03: iron shortens T2\*; T2\* = the decay constant of a multi-echo GRE. Cardiac-specific twists: the myocardium moves, so the sequence is acquired at one cardiac phase (dark-blood prep recommended to keep the bright blood pool out of the myocardial voxels) and breath-held; T2\* in the *heart* is shorter than in the liver for the same iron load, so the echo train is designed for ~2–18 ms; and the product (MyoMaps T2\*) is **1.5T-only** — at 3T the susceptibility effects and off-resonance make the measurement unreliable, so protocols must not run it at 3T. Normals: ~36 ± 7 ms; < 20 ms abnormal.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Echoes / spacing | 8–10 echoes, TE 2–18 ms @1.5T | Samples the short-T2\* decay (file 03) |
| Field strength | **1.5T only** | 3T unreliable — protocol note |
| Dark-blood prep | recommended | Keeps blood out of the fit |
| Timing | diastolic, breath-hold | The moving target |

**Artifacts & pitfalls —** Breathing/cardiac motion between echoes; off-resonance at the lung–heart interface (posterior wall); blood partial-volume brightening the decay; compare only against 1.5T reference values.

**Used in this vault —** Cardiac iron quantification (thalassemia screening/follow-up) with the 10-echo acquisition and inline T2\* maps — together with the liver 14-echo T2\* companion.

---

## 6. First-Pass Perfusion (saturation-recovery TurboFLASH)

**What it is —** A saturation-recovery prepared single-shot readout (file 03, entry 10) acquiring the same slices **every heartbeat** while a gadolinium bolus passes — ~3 slices per beat at ~1 image per beat per slice. Tokens: `dynamic_tfl_sr_*` — pre-contrast, stress, and rest series.

**Contrast & good for —** **Myocardial ischemia**: under vasodilator stress (and at rest for comparison), segments supplied by a stenosed artery show a *delayed and reduced* first-pass enhancement — a perfusion deficit. The stress/rest pair is the diagnostic: a deficit present at stress and absent at rest = reversible ischemia; present in both = scar/infarct (with LGE to confirm).

- **Physics deep-dive — why saturation recovery, and what "first pass" means.**

    - The readout is TurboFLASH (file 03, entry 3), but the preparation is a **90° saturation pulse, not inversion** — and that choice is deliberate:

    - Inversion gives more dynamic range but its signal is *non-monotonic* (recovering through zero) and its timing is delicate — bad for a sequence that must fire every heartbeat regardless of R-R variation.
    - Saturation sets M_z to zero cleanly; after a short, fixed saturation time (TS, ~100–200 ms class), M_z = M₀(1 − e^(−TS/T1)) — **monotonic in T1**. Contrast arrives → tissue T1 shortens → signal rises. The image intensity during the bolus is a clean proxy for contrast concentration in the tissue.

    - The "first pass": the bolus is in the RV ~3–5 s after injection, LV ~5–8 s, myocardium ~8–12 s — a window of ~10–15 s before recirculation blurs the gradient between perfused and non-perfused segments. The per-heartbeat timing catches that window: the deficit image is the *brightness difference during first pass*, not at equilibrium. Perfusion is read side-by-side: rest study (normal), stress study (deficit), and LGE afterward distinguishes ischemia (no LGE) from scar (LGE in the same territory).

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Slices per beat | 3 (with T-PAT acceleration) | More coverage = coarser temporal sampling of the bolus |
| Saturation time | short, fixed | Monotonic T1 mapping (above) |
| Stress agent | vasodilator stress per protocol | The comparison arm — always pair stress with rest |
| Contrast | single dose, high-rate injection | Width/shape of the first-pass window |
| Triggering | every heartbeat, same cardiac phase | Diastolic freezing of the moving heart |

**Artifacts & pitfalls —** **Dark-rim artifact**: a dark line at the subendocardium from susceptibility at the blood–myocardium interface and partial-volume of dark blood — *the* classic false "deficit"; arrhythmia and rate changes break per-beat timing; stress side effects (hypotension, bronchospasm — monitoring per protocol); don't read a single frame — watch the whole first pass.

**Used in this vault —** Stress/rest first-pass perfusion (saturation-recovery TurboFLASH with T-PAT) as the ischemia arm of the cardiac protocol, with pre-contrast baselines.

---

## 7. LGE — Late Gadolinium Enhancement

**What it is —** An **inversion-recovery** readout acquired 8–15 minutes after contrast, with the TI chosen so that *normal myocardium is nulled (black)* — leaving scar/fibrosis, which holds contrast longer, bright against the black muscle. Tokens: `ti_scout` (the TI finder), `de_overview_tfi_*` (breath-held TrueFISP overviews — 4C/2C/SAX), `de_trufi_overview_12sl_psir_fb` (the free-breathing 12-slice variant, MOCO + 5 averages), `tfl13_2d_t1_seg_fs_*` (high-res segmented TurboFLASH), and the early-enhancement variants.

**Contrast & good for —** The viability/fibrosis reference standard: **scar** (infarct — subendocardial/transmural), **fibrosis** (DCM, HCM — mid-wall), **myocarditis** (epicardial/subepicardial, and with early Gd enhancement per Lake Louise criteria), amyloid (diffuse subendocardial). LGE's power is that normal myocardium is *black* — even subtle bright regions are conspicuous.

- **Physics deep-dive — the nulling story, and why PSIR removes the guesswork.**

    - LGE is the clinical masterclass in inversion recovery (file 02, entry 3). After contrast, normal myocardium has T1 ~ 400–500 ms; scar retains more contrast → shorter T1 (~300–400 ms). An inversion pulse inverts both; they recover toward zero; the readout happens when *normal myocardium* crosses zero (TI ≈ 0.69 × its T1, ~250–350 ms at 10–15 min post-contrast). At that instant: normal myocardium = black, scar = already past zero and positive = bright. Two practical consequences:

    - 1. **TI drifts.** Contrast washes out of the myocardium over minutes, lengthening T1 — the null moves. TI ~ 300 ms at 10 min becomes ~320 at 15 min; long LGE stacks need TI *re-adjustment* (roughly +10 ms every few minutes or per slice group).
    - 2. **The TI scout exists because of this.** A Look–Locker style series (inversion recovery repeated at ascending TIs, `ti_scout`) shows the myocardium crossing black across frames; the operator picks the TI of the darkest frame → sets it on the LGE.

    - **Why PSIR (phase-sensitive inversion recovery) removes the guesswork — and why the vault's overviews reconstruct it alongside magnitude.** Magnitude reconstruction (file 02) displays |M_z| — signal that recovered *past* zero shows bright again, which means: set the TI slightly too long, and normal myocardium turns *gray-white* — indistinguishable from scar. PSIR reconstructs with the **phase of the magnetization preserved**: tissue still negative (not yet nulled) is displayed dark, positive tissue bright, and the *zero crossing is the only ambiguity*. The contrast between scar and normal myocardium therefore stays near-maximal over a **wide range of TI (~280–360 ms)** — a PSIR LGE needs no precise TI scout and tolerates the TI drift discussed above. The vault's TrueFISP overviews — `de_overview_tfi_*` and `de_trufi_overview_12sl_psir_fb` — all reconstruct **both** a magnitude and a PSIR image: the breath-held series cover one plane each in a single hold, the free-breathing 12-slice series (MOCO + 5 averages) covers the whole ventricle; the PSIR image is this robustness applied per-slice.

    - Readout flavors matter: the **segmented high-res TurboFLASH** LGE (tfl13-class) has the best spatial resolution and scar definition but needs the TI to be right (magnitude) or uses PSIR; the **single-shot TrueFISP** overviews are faster and carry both reconstructions — their PSIR image is TI-robust — but are slightly blurrier — protocols typically run both (overview + high-res).

    - **The early-Gd arm (EGE).** Lake Louise criteria for myocarditis add *early* gadolinium enhancement (hyperemia/edema): a T1-weighted early post-contrast acquisition, an early TI scout, and early PSIR overviews — the same inversion physics, applied minutes after injection when the null target is very different (TI ~140–320 ms dark-blood variants exist to suppress the blood pool).

**Tunable choices —**

*Nulling*

| Knob | Typical value | Turning it… |
|---|---|---|
| TI | ~250–350 ms (10–15 min post-Gd); from TI scout | Nulls normal myocardium — the master knob |
| TI scout | Look–Locker, TI ~90–800 ms sweep | Finds the null per patient/per time |
| Reconstruction | magnitude vs PSIR | PSIR = TI-robust, no scout needed (above) |

*Readout*

| Knob | Typical value | Turning it… |
|---|---|---|
| Segmented IR-TurboFLASH vs single-shot TrueFISP | high-res + overviews | Resolution vs robustness — both in the vault |
| Timing post-injection | 8–15 min (scar), early <5 min (EGE) | Different null targets, different questions |
| Slice stack | short-axis full LV (+ long axes) | Coverage of the whole myocardium |
| Fat suppression | for epicardial work | Fat is bright on T1 — can mimic scar |

**Artifacts & pitfalls —** Wrong TI (magnitude LGE: too long → nulled myocardium turns bright — the classic false "diffuse scar"; PSIR cures this); TI drift over a long stack (re-scout or rely on PSIR); blood pool bright next to the myocardium (dark-blood variants; PSIR handles better than magnitude); arrhythmia ghosting in segmented scans; *false* enhancement from fat, thrombus (dark — no enhancement), and mis-registered early frames.

**Used in this vault —** The full LGE arm: TI scout (+ early variant), magnitude and PSIR overviews (4/2-chamber + short axis; 12-slice free-breathing MOCO + 5 averages), high-res segmented fat-suppressed TurboFLASH, and the early-Gd/Lake-Louise set in the myocarditis protocols.

---

## Family summary

| Sequence | Engine | What it measures | Key cardiac physics |
|---|---|---|---|
| Cine | balanced SSFP | function/volumes | segmentation + retro-gating; real-time CS rescue |
| PC flow | phase contrast | velocity/flow | VENC > peak velocity; per-phase maps |
| T1 map (MOLLI) | inversion + bSSFP shots | T1 / ECV | N(p)M schemes count heartbeats |
| T2 map | T2-prep + bSSFP | edema | prep times 0/24/55, three scans |
| T2* map | multi-echo GRE | iron | 1.5T-only; <20 ms abnormal |
| First-pass perfusion | SR-TurboFLASH | ischemia | per-heartbeat saturation recovery |
| LGE | IR readout | scar/fibrosis | null *normal* myocardium; PSIR removes TI guesswork |

---

**Key sources** — Siemens Healthineers (MyoMaps, CS cardiac cine, Advanced Cardiac/BEAT); mriquestions.com: [TrueFISP](https://www.s.mriquestions.com/true-fispfiesta.html), [cine parameters](https://mriquestions.com/cine-parameters.html), [retrospective gating](http://s.mriquestions.com/retrospective-gating.html), [dark-blood](https://www.s.mriquestions.com/dark-blood-imaging.html); papers: Messroghli MOLLI (MRM 2004), Giri T2 (MRM 2009), Anderson T2* (EHJ 2001), Kellman PSIR (JCMR 2002), SCMR 2020 protocols (JCMR); Radiopaedia: [LGE](https://radiopaedia.org/articles/late-gadolinium-enhancement-2).

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — 7 cardiac entries |
