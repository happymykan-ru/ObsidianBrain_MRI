# Spin-Echo Family

**Version:** 1.0 | **Date:** 2026-09-08

The defining feature of everything in this family: a **180° refocusing pulse** (or a train of them) forms the echo. Because the refocusing pulse reverses static field variations, signal decays with **T2 rather than T2*** — spin echo is inherently immune to B₀ inhomogeneity, susceptibility, and chemical-shift dephasing. That immunity is why TSE remains the anatomical workhorse even where gradient echo is faster.

The price: 180° pulses are power-hungry (**SAR**), every refocusing pulse takes time (**minimum echo spacing**), and each refocus only handles one slice at a time (except HASTE/SPACE tricks described below).

Values throughout are recommended typical ranges — your protocols may fix a specific number, and the protocol wins where they conflict.

---

## 1. Conventional Spin Echo (SE)

**What it is —** The original MRI sequence and the reference for contrast fidelity: one 90° excitation, one 180° refocus, one k-space line per TR.

**Contrast & good for —** T1-weighted (or PD-weighted) anatomy with the sharpest edges MRI can produce. There is no turbo blur and no steady-state contamination — the image is exactly what the spin-echo equation predicts. Today it survives where edge sharpness or geometric fidelity matters more than speed: small structures, fine measurements, and T1 near surgical clips.

**How it runs —**

```
RF    90°                         180°
       ▄▄▀                          ▀▄▄
       |____________TE/2___________|______TE/2______|
G_read |_dephase_|____________readout___________|    echo sampled at TE
G_phase|_ step N _|                                  one phase step per TR
TR     |<----------------- TR ------------------->|   next line = step N+1
```

**Physics —** The 90° tips the magnetization into the transverse plane. Over the first TE/2 the spins dephase — partly from true T2 processes (random, irreversible) and partly from static causes (B₀ inhomogeneity, susceptibility, chemical shift), which are *systematic*: every spin in a voxel accumulates the same extra phase. The 180° pulse rotates each spin's phase by 180° (φ → −φ), so over the second TE/2 the systematic dephasing *unwinds* exactly, while the random T2 loss does not. At TE the static terms are gone; only T2 decay remains:

```
S = k · PD · (1 − e^(−TR/T1)) · e^(−TE/T2)
```

One phase-encode step per TR, so N_phase TRs per average — this is why SE is slow, and why it needs short TR to be practical: keep TR short and the (1 − e^(−TR/T1)) term makes T1-short tissues (fat, post-contrast, methemoglobin) bright → T1 weighting.

**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| TR — T1-weighted | 1.5T: ~400–650 ms · 3T: ~550–900 ms | TR is set near the tissue T1 of interest — that is what creates T1 contrast. T1 lengthens ~20–30% at 3T, so TR must rise with field to keep the same contrast and SNR. Shorter TR = stronger weighting, less signal |
| TR — PD-weighted | 1.5T: ~2000–3000 ms · 3T: ~2500–4000 ms | PD needs TR ≫ T1 (roughly 2–3× the longest T1 in the field of view) so that *all* tissues fully recover and T1 differences vanish. Longer = purer PD + more SNR, at the cost of scan time |
| TE | shortest possible (~10–30 ms, both fields) | SE is never used for true T2 here — TE must stay short or T2 decay contaminates both the T1 and PD contrast |

*Speed & SNR*

| Knob | Typical value | Turning it… |
|---|---|---|
| Averages | 1–4 | SNR grows √NEX, scan time grows NEX |
| Phase partial Fourier | 6/8 typical | ~25% time cut at ~13% SNR cost |
| GRAPPA | factor 2 | Time ÷2, SNR penalty 1/(g·√R) ≈ −29% |

**Artifacts & pitfalls —** Slow (one line per TR) — the reason every other member of this family exists. Motion ghosts appear along the phase-encode axis, as in all cartesian sequences. Through-plane flow (vessels and CSF crossing the slice) produces two *different* artifacts — worth understanding separately because the cures differ (deep-dive below).

- **Physics deep-dive — through-plane flow: what is lost, what ghosts, and what GMR can actually fix.**

    - A spin echo requires every spin to experience **both** RF pulses: the 90° tips it into the transverse plane, the 180° at TE/2 is what *refocuses* it. Through-plane flow breaks this contract in two distinct ways.

    - **1. Signal loss — "washout" (a displacement problem).** Between the 90° and the 180°, a spin moving perpendicular to the slice travels a distance v·TE/2. If it leaves the slice before the 180° fires, it is never refocused — no echo from that spin, no matter what gradients do afterward:

      ```
      washout threshold velocity ≈ slice thickness / (TE/2)

      example: 4 mm slice, TE 20 ms  →  v ≈ 4 mm / 10 ms ≈ 0.4 m/s  →  arterial flow washes out
      ```

    - Fast arterial flow (carotid/vertebral, ~0.4–1 m/s systolic) largely vanishes — the normal SE flow void; slower flow (CSF, veins) only partially washes out, giving reduced, inconsistent signal. At the *entry slice* of a stack, freshly arriving blood is paradoxically bright (entry-slice phenomenon). This loss is position-based — **GMR cannot restore spins that physically left the slice** (it rephases phase, not displacement).

    - **2. Ghosting — "pulsation ghosts" (a timing problem).** Cardiac pulsation modulates flow velocity continuously. In a non-ECG-gated multi-slice acquisition, each TR lands at a different, unsynchronized point of the cardiac cycle — so for a given slice, successive phase-encode lines sample the vessel/CSF at *different velocities*, i.e. different washout fractions and different positions. The vessel's apparent signal therefore oscillates along k_y with the heart rate. Any periodic modulation along the phase-encode direction reconstructs as **replicated copies of the vessel displaced along the phase-encode axis** — pulsation ghosts (classically CSF ghosts over the cord in spine imaging, carotid ghosts across the brain). The ghost spacing is set by TR × heart rate; the direction is always phase-encode because that is the axis along which line-to-line inconsistencies accumulate.

    - **3. What GMR (flow compensation) does — and its limits.** GMR adds gradient lobes that null the **first gradient moment M₁** at the echo, so the phase a spin accrues from *constant velocity* (φ = γ·M₁·v) becomes zero. Two effects follow: laminar *steady* flow (a range of constant velocities across the vessel) regains coherent phase → less signal loss from intravoxel velocity spread; and the velocity-phase component of ghosting shrinks. But three things remain: (a) the extra lobes need time → **minimum TE lengthens**, which on a T1 sequence is real cost (more T2 decay, less T1 purity); (b) pulsatile flow is *accelerating* — GMR nulls M₁, not M₂, so the residual acceleration term still ghosts (GMR reduces but does not abolish pulsation ghosts); (c) washout (mechanism 1) is untouched.

    - **Cure hierarchy for through-plane flow artifacts —** GMR first if ghosts dominate and TE allows; if washout voids are the problem, shorten TE or accept (SE-T1 flow voids are often diagnostically useful — they confirm flow); swap the phase-encode direction so ghosts fall away from the anatomy of interest; add saturation bands upstream of the pulsatile source (e.g. below the cord for CSF, over the neck vessels for brain) to kill the signal before it enters; and only ECG/peripheral triggering truly freezes pulsatile flow — reserved for cases where ghosts persist and the sequence is long enough to tolerate it.

**Used in this vault —** The fine-T1 detail jobs, all chosen by one principle — the *slow but exact* option wherever turbo blur would hurt a small structure: head-and-neck small parts (PNS, salivary glands, larynx, facial AVM), a fine knee measurement (meniscal extrusion), and sellar/IAM detail (the latter paired with the restore pulse, entry 7).

---

## 2. TSE — Turbo Spin Echo

**What it is —** One 90° excitation followed by **many** 180° pulses; each refocus produces one echo, and each echo fills a different k-space line. One TR therefore fills many lines. Siemens name: turbo spin echo (the `tse` in the vault tokens). The clinical workhorse of the entire vault.

**Contrast & good for —** T2 (long TR + long effective TE) for edema, marrow, soft tissue, prostate zonal anatomy — every region. T1 (short TR + short effective TE), PD, and dual-echo PD+T2 from one acquisition. If a protocol needs "anatomy with fluid sensitivity," it is almost always TSE. For T1, TSE is the tool over GRE-T1 where the 180°'s refocusing does clinical work: susceptibility regions (skull base, sinuses, metal) where GRE drops signal, and intrinsic T1-shortening (methemoglobin, melanin, proteinaceous fluid) that GRE's T2\* blooming paradoxically darkens. GRE-T1 keeps what only it does — speed, dynamics, 3D breath-holds.

**How it runs —**

```
RF   90°   180°   180°   180°   180°   180°   180°
      ▄▄▀    ▀▄▄    ▀▄▄    ▀▄▄    ▀▄▄    ▀▄▄    ▀▄▄
echoes:      ✦      ✦      ✦      ✦      ✦      ✦      ← each echo = one k-space line
              ↑
         the echo that fills k-space CENTER
         decides the image contrast → its decay
         time is the "effective TE"
```

**Scan time — the payoff of the echo train:**

```
TA = TR × N_phase × NEX / turbo factor
```

- **Physics deep-dive — why "effective TE" exists and why high turbo factors blur.**

    - In a single spin echo, TE is a single number — the whole image decays exactly to e^(−TE/T2). In TSE, each echo in the train is read out at a *different* time after the 90°, so each k-space line carries a different amount of T2 decay. Which line carries what decides the two consequences:

    - 1. **Contrast is set by the center of k-space.** k-space center encodes low spatial frequencies — the overall brightness differences between tissues. Whichever echo happens to be assigned there "stamps" the image contrast. Its decay time — *effective TE* — is roughly (position of the center echo) × (echo spacing). Reordering the phase-encode order within the train moves the center echo: put a late echo (long TE) at center → T2-weighted image; put an early one → T1/PD-flavored image. That is how one sequence family covers T1, T2 and PD.

    - 2. **Blurring is the price of the train.** High spatial frequencies (edges) live at k-space *edges*, which are filled by the earliest and latest echoes. The late echoes have decayed substantially, so high-frequency signal is weak → fine detail smears — the famous TSE blur. Blur worsens with: longer echo trains (more decay across the train), longer echo spacing, and longer effective TE. Sharpness therefore pushes you to lower turbo factors, while scan time pulls the other way.

    - A subtlety worth knowing: TSE trains stay clean only under **CPMG phase** (Carr–Purcell–Meiboom–Gill). The 90° excitation leaves the magnetization pointing along y, and the refocusing train is transmitted with a 90° phase offset — rotating around that same y-axis. Because a rotation leaves its own axis unmoved, imperfect refocusing pulses (B₁ inhomogeneity, off-resonance — the real flip is ~175°, not 180°) cannot disturb the main signal; they only mishandle the small dephased fan components, whose errors cancel in pairs, so the train decays with true T2. The scheme is species-independent — the axis comes from the pulse phases, and the 180° mirrors whatever phase each spin accumulated, water and fat alike. Break the phase relationship and the magnetization no longer returns to the same axis each echo: every echo mixes spin-echo and stimulated-echo paths of different weighting ("mixed echoes"). Reduced flip angles (<180°, the SAR lever) create that mixture on purpose — the scanner keeps CPMG phase and predicts the outcome with the **extended phase graph (EPG)**, the same machinery behind hyperechoes, SPACE's variable flip-angle schedules, and fastBLADE (entry 4).

**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| TR (T1w) | 1.5T ~450–700 · 3T ~600–900 ms | Shorter = stronger T1 weighting; 3T needs the longer end (T1 ↑ ~20–30%). Time cost is small — the turbo factor pays it |
| TR (T2w) | 1.5T ~2500–8000 · 3T ~2500–6000 ms | Longer = purer T2 + more slices/TR; 3T SAR caps the heavy-T2 end |
| TR (PDw) | 1.5T ~2000–3000 · 3T ~2500–4000 ms | TR ≫ T1 removes T1 influence; keep turbo factor ~4 or T2 leaks into the PD |
| Effective TE | T2w ~80–120 · T1w/PD ~10–30 ms | Decay time of the center echo sets the contrast: later center = deeper T2 + more blur; early center = clean T1/PD |
| Reordering | linear vs centric | Linear = robust; centric = shortest effective TE (T1w, flow) |
| Dual echo | TE1 ~10–20 / TE2 ~80–120, TR ≥2500 | PD + T2 from one acquisition |

*Speed & blur*

| Knob | Typical value | Turning it… |
|---|---|---|
| Turbo factor | T2w 16–30; T1w 2–8; PD ~4 | Doubles speed per step up — costs blur, SAR, slices-per-TR |
| Echo spacing | ~4–16 ms (Siemens designs ~7–8) | Shorter spacing = less blur at equal turbo factor; costs gradient power |
| Refocusing flip angle | 180° → 120–150° | Cuts SAR ∝ angle² (120° ≈ 44% SAR) with mild signal loss. Floor ~120°: below it, stimulated echoes dominate and contrast drifts toward T1 |
| Hyperechoes (hyperTSE) | on/off | Symmetric flip-angle ramp → all paths recombine in phase at center ("virtual 180°"); ≥65–70% SAR cut with unchanged contrast — 3T prostate standard. Outer echoes carry more stimulated-echo character, which is affordable: they fill k-space edges (resolution), not the contrast center |

*Suppression*

| Knob | Typical value | Turning it… |
|---|---|---|
| Fat suppression | none / Fat Sat / SPAIR / Dixon | Each has its failure mode — full comparison in file 08 |

**Artifacts & pitfalls —** Crank up the turbo factor or widen the echo spacing and the image blurs, because the late echoes in the train have already decayed and carry little signal — the physics above. At 3T, SAR usually binds first — cut refocusing angle, hyperechoes, longer TR, fewer slices, in that order. Long acquisitions invite motion: lines are sampled one TR apart, so movement smears and ghosts along phase-encode — BLADE or GMR fix it. In the cervical spine, pulsatile CSF washes out over the long T2 train, darkening CSF where cord axials need it bright — hence MEDIC, not TSE-T2, there.

**Used in this vault —** Everything. Brain screening (axial T2, FLAIR-class), spine (sagittal and axial), orbit, TMJ, all MSK joints with PD/T2 variants, pelvis and prostate, abdomen with Dixon or fat saturation, and the paediatric multi-echo version that yields PD, intermediate and T2 from a single train. Where motion ruins it, your protocols swap in BLADE; where breath-holds fail, in HASTE; where isotropic 3D is needed, in SPACE — the next entries.

---

## 3. Inversion Recovery — FLAIR · STIR/TIRM · DIR · dark-blood

**What it is —** A **180° inversion prepulse** (which flips magnetization to −M₀), then a *wait* of duration **TI** while T1 recovery proceeds, then the readout (TSE/SE/SPACE). Because each tissue recovers at its own T1 rate, you can choose TI so that *one* tissue is passing through zero magnetization at readout time — that tissue contributes no signal: it is **nulled**. One physical mechanism, four clinical flavors.

**Contrast & good for —**

| Flavor | What it nulls | Typical TI (1.5T / 3T) | What you get |
|---|---|---|---|
| FLAIR | CSF / free water | (1.5T) 2000–2200 ms · (3T) 2200–2500 ms | T2 weighting where the brightest normal tissue (CSF) is removed — periventricular and cortical lesions, MS plaques, small-vessel disease stand out |
| STIR (Siemens' name: TIRM) | Fat | (1.5T) 150–180 ms · (3T) 200–220 ms | T2 weighting with fat gone — marrow edema, inflammation, brachial plexus, optic nerve; works where spectral fat suppression cannot |
| DIR | CSF **and** white matter | (1.5T) TI₁ ~2200–2800 / TI₂ ~450 ms · (3T) TI₁ ~3000–3600 / TI₂ ~550–600 ms | Only gray matter and lesions remain — cortical MS plaques |
| Dark-blood TIRM | Blood | (1.5T) ~500–700 ms · (3T) ~600–800 ms, rate-dependent | Myocardial edema without the bright blood pool smearing the wall (cardiac — file 06) |

**How it runs (STIR archetype) —**

```
RF     180° invert                90°   180° 180° 180° … (TSE readout)
         ▀▄▄                        ▄▄▀   ▀▄▄  ▀▄▄  ▀▄▄
M_z:   −M₀ ──────────► recovers ───► 0 ←─ fat crosses zero HERE
         |<------------- TI ------------->|
```

- **Physics deep-dive — what nulling really does, and the trap in it.**

    - After inversion, longitudinal magnetization recovers as M_z(t) = M₀(1 − 2e^(−t/T1)). It starts at −M₀, crosses zero at

      ```
      TI_null = T1 · ln 2  ≈ 0.693 · T1
      ```

    - and then approaches +M₀. Nulling is therefore **a T1 measurement disguised as a suppression technique**: fat nulls at short TI because fat has a short T1 (~230–260 ms at 1.5T); CSF nulls at long TI because water's T1 is ~4 s. The same physics explains the *trap*: **anything with a T1 close to the null target disappears too.** STIR therefore also nulls proteinaceous fluid, subacute hemorrhage, and enhancing tissue — a lesion whose T1 happens to match fat will silently vanish from a STIR image. Consequences you must carry into protocol design:

    - STIR/TIRM is **not usable after gadolinium** (enhancing tissue has short T1 and may null or invert oddly) — use Fat Sat/SPAIR/Dixon on post-contrast T1 instead.
    - FLAIR nulls *all* free water, including pathological collections — a thin subdural effusion can be dark on FLAIR while obvious on T2. FLAIR is a complement to T2, never a replacement.
    - **Magnitude reconstruction** (TIRM = Turbo Inversion Recovery *Magnitude*; FLAIR is magnitude too): the scanner displays |M_z|, so signal that recovered past zero shows bright again. The null is a thin dark band around the zero crossing — fine for suppression, but the *contrast* between two tissues depends on where both sit on the recovery curve, not just on the null.

    - **When to prefer STIR/TIRM over spectral fat saturation (file 08)?** Spectral fat-sat targets the *fat resonance* — it needs uniform B₀, and fails off-center, at wide FOV, low field, and near metal. Inversion nulling works on *T1*, blind to B₀ and B₁ — fat is suppressed wherever it is, at the price of lower SNR and the over-suppression above. Hence the rule: STIR/TIRM is the fat-suppression of last resort for hostile-field regions (skull base, perineum, brachial plexus, whole-spine composition, near metal).

**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| TI | per flavor table above | Targets the null — wrong TI means the wrong tissue vanishes or nothing nulls cleanly |
| TR — FLAIR | (1.5T) 8000–10000 ms · (3T) 9000–11000 ms | Near-full T1 recovery is mandatory before the next inversion; 3T needs the longer end (tissue T1s lengthen, TI grows) |
| TR — STIR | (1.5T) 3000–4500 ms · (3T) 4000–6000 ms | Short TI allows a short TR — but 3T still pushes it up for the same T1-recovery reason |
| TE — FLAIR | 90–140 ms (same both fields) | Sets the T2 flavor under the null; T2 is field-insensitive, so the window does not move with 1.5T/3T |
| TE — STIR | 50–90 ms (same both fields) | Same logic — the T2-flavor window, not the null, sets TE |

*Suppression & robustness*

| Knob | Typical value | Turning it… |
|---|---|---|
| Inversion pulse | slice-selective vs non-selective | Non-selective inverts the whole body — cleaner null, but higher SAR and it hits inflowing blood too |
| Readout flavor | TSE, SPACE (3D FLAIR/DIR exist), BLADE-FLAIR | Inherits that readout's speed/blur/motion behavior |

**Artifacts & pitfalls —** Nulling depends on TI matching tissue T1 at *scan time*: after contrast, T1 shortens and a previously perfect TI misses (re-check TI whenever the protocol context changes). STIR's low SNR is inherent (small magnetization at readout) — compensate with thickness/averages, not by shortening TR. FLAIR at 3T needs the longer TI (~2400 ms) and longer TR; patients perceive the long scan. CSF nulling also darkens subarachnoid pathology — always read FLAIR against its T2 partner. Inflow artifact: blood that was not inverted can stream into the slice bright on FLAIR — non-selective inversion cures it at SAR cost.

**Used in this vault —** FLAIR is the MS/small-vessel screening contrast of the brain protocols (with a BLADE variant for motion-prone patients and a fat-sat coronal version for epilepsy work). STIR is the standard fat-suppressed T2 in the orbit, head-and-neck, MSK and mass protocols; TIRM appears where the field is hostile — brachial plexus, whole-spine composition, and combined with SEMAC near hip prostheses. The cardiac protocols use the dark-blood TIRM variant for edema, and the MS protocol uses DIR to see cortical plaques.

---

## 4. SPACE — 3D Turbo Spin Echo

**What it is —** Siemens' 3D TSE with **variable flip-angle refocusing** (internal name `tse_vfl`; the console sequence is SPACE). Instead of hammering every refocus at 180°, the scanner modulates the refocusing angles along the train — typically starting around 30–60°, rising, then varying — which lets the echoes run for 100–250+ refocuses and fill an entire 3D slab in one long echo train.

**Contrast & good for —** T2 (myelography-class bright fluid), PD (cartilage/marrow), T1. Because it is a true 3D acquisition with ~0.5–1 mm isotropic voxels, it is the **source dataset for free multiplanar reformats** — one acquisition replaces three 2D planes, at equal or better through-plane resolution, with no slice gaps. The MRCP/MRU/myelography class of static-fluid applications rides on its bright-fluid T2.

- **Physics deep-dive — why constant 180° fails for 3D, and how the variable-angle schedule keeps 200 echoes alive.**

    - A constant-180° train long enough to fill a 3D slab dies twice: **SAR** — each 180° deposits ~4× a 90°'s energy (SAR ∝ flip²), and 200 of them at 3T are not permissible — and **signal death** — every echo spends the transverse supply, so after ~20–30 refocuses there is nothing left to echo. You cannot extend such a train; you have to stop wasting magnetization.

    - The escape is the per-spin mechanics of a refocusing pulse. Pulses fire when the fan is maximally open (between echoes, by CPMG design), so every spin presents a cross-axis component set by how far it has dephased from the echo axis; the along-axis part is a spectator, untouched at any angle. What the pulse does to the cross-axis part depends only on its angle α:

    - 1. **α ≈ 180°** — a full mirror: everything reverses, a true spin echo forms, nothing is stored. Clean but expensive, and each echo consumes the population.
    - 2. **90° < α < 180°** — partial mirror plus partial parking: part of the cross-axis component is reversed (echoes), part is rotated into z (stored).
    - 3. **α < 90°** — no mirror at all: cross-axis spins are shrunk and rotated into z — the pulse *stores* rather than echoes, and does it cheaply.

    - So the flip-angle schedule is simply a dial that chooses, pulse by pulse, how much magnetization is spent on echoing versus banked along z. Magnetization parked along z stops decaying with T2 (it relaxes only with slow T1) and keeps the memory of its phase — a later, larger pulse can recall it as a **stimulated echo**. Signal that a 180° train would have burned is instead recycled.

    - The schedule, and what each zone is for. The graph below plots **the flip angle of every refocusing pulse, in the order the pulses fire** — vertical axis: the angle αₙ of pulse number n; horizontal axis: the pulses themselves, left to right (each echo is read out between two consecutive pulses). A conventional TSE would be a flat line at 180°; SPACE is this envelope:

      ```
      αₙ (flip angle of each refocusing pulse)
       180 ┤ · · · · · · · · · · · · · · · · · · · · · · · ·  ← where a constant-
       150 ┤                    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄   180° TSE would sit
       120 ┤               ▄▄▄▄▀
        90 ┤         ▄▄▄▀  ───────────────────────────────   mirrors ON above
        60 ┤       ▄▀                                       this line
        30 ┤    ▄▄▀
         0 └▄▄▄────────────────────────────────────────────►
            pulse 1                                     pulse ~250
            ramp                  body                     end
            (<90°: park     (≈120–150°: echoes flat    (train stops when the
             & pass)          & strong)                   reservoir empties —
                                                          the angle never falls)
      ```

    - **The ramp (< 90°):** every pulse parks and passes — no true mirrors — so the z-reservoir fills cheaply while pass-through remnants keep the road from emptying. Echoes exist here (recalled and multiply-passed magnetization refocuses on the same midpoint grid), but they are weak and stimulated-flavored, so they are discarded as warm-up or sent to the k-space edges.

    - **Crossing 90°:** mirrors switch on — cross-axis components start being reversed — and echoes grow real spin-echo character.

    - **The plateau (120–150°):** each pulse mirrors most of the actable magnetization (strong echoes) while parking roughly as much as it recalls — the reservoir reaches equilibrium, with the angles creeping gradually upward through the body to compensate T2 decay. Because every echo recycles magnetization through the garage instead of consuming it, the train stays flat for 100–250 echoes — an order of magnitude beyond a 180° train — and all pathways (direct, passed, parked-and-recalled) refocus on the same echo grid, so the flatness is real coherence, not averaged blur.

    - **The end of the train:** the envelope never drops — it just stops when the reservoir is exhausted. T2 decay and the spent budget win, the last echoes fade, and (like the ramp's) they fill the k-space periphery. In some designs the final angles actually creep upward toward ~180° to extract the last of the remaining magnetization — the fade is an emptying effect, never an angle collapse.

    - **In SPACE you pick a flavor, not a TE.** A TSE image is re-weighted by changing TR/TE. SPACE has no such knob: the ramp, the plateau, and the choice of which echo lands at k-space center are one package, designed together so the train stays flat and the SAR stays legal. T1-SPACE and T2-SPACE are therefore different sequences — not one sequence with different TEs.

    - **The effective TE is the echo the schedule puts at k-space center.** The T2 and bright-fluid flavors put a *late* echo there (heavy T2); the PD and T1 flavors put an *early* one. Because the train keeps all echoes flat, a late center echo still arrives at full amplitude — a 180° train would have already decayed by then and paid for it in SNR.

    - **Flat amplitude still isn't one single character.** Early echoes are mostly true spin-echo signal (direct path, pure T2). Later echoes increasingly come from magnetization that was parked and later recalled — it relaxed with T1 while parked, so those echoes carry a slight T1 flavor. An image's feel therefore depends on both *where* the center echo sits and *what mix* it contains — two schedules with the same nominal TE can look different. That is why the flavor you choose, with its designed-in center echo, is the real contrast decision.

    - The rest is 3D housekeeping: each echo encodes one (k_y, k_z) line of the slab, TR runs long (2000–4000 ms), so scan time is bought with iPAT/CAIPIRINHA/CS — never by shortening the train arbitrarily. And SAR closes the loop: energy ∝ Σαᵢ², and most pulses sit below or near the plateau's partial angles, so the whole train costs a fraction of 200 × 180² — the reason a 200-echo 3D train is legal at 3T at all.

**Tunable choices —**

*Volume & resolution*

| Knob | Typical value | Turning it… |
|---|---|---|
| Voxel shape | isotropic (~0.5–1 mm) *or* slab-style: fine in-plane + thicker z-partitions | Isotropic = lossless reformats in any plane (neuro). Thicker z = fewer partitions → faster + better SNR; reformats across z get blocky — choose per need |

*Speed & blur*

| Knob | Typical value | Turning it… |
|---|---|---|
| Turbo factor | 100–250+ | The point of SPACE; blur is managed by the angle schedule, not by lowering TF alone |
| Echo spacing | ~3–5 ms | Shorter = less blur, more gradient demand |
| Parallel imaging | iPAT 2–3; CAIPIRINHA 2×2; CS (tokens show cs4/cs6) | The real time levers for 3D TSE (file 08) |

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| Weighting flavor | T2-SPACE, PD-SPACE, T1-SPACE, dark-fluid SPACE, DIR-SPACE | Each is a different product schedule — pick the one matching your question |
| Fat suppression | none (hydrography) / Fat Sat / SPAIR / TIRM | MRCP and urography run without it (pure fluid); sialogram/myelography with it |

**Artifacts & pitfalls —** Mild T2 blur and longer minimum scan time vs one 2D plane (you pay for the third dimension — but you also *get* it); flow artifacts inside long TR (enable GMR). At the edge of the slab, signal rolls off — oversample partitions or accept the anatomy at slab center. Don't use SPACE for a single-plane quick look: 2D TSE is faster.

**Used in this vault —** Everywhere a 3D volume earns its keep: neuro anatomy that is reviewed in reformats (whole-brain T2, IAM and pituitary detail, MS double-inversion); static-fluid questions, where heavy-T2 3D delivers MRCP, MR urography, myelography and sialography; and thin-slice planes that 2D cannot match — prostate/pelvis T2, SI-joint T1, isotropic joint PD (knee, hip, ankle). Where 3T SAR rules SPACE out (some MRCP protocols), a 3D-TSE variant stands in.

---

## 5. HASTE — Single-Shot Turbo Spin Echo

**What it is —** H**alf**-**F**ourier-**A**cquisition **S**ingle-shot **T**urbo spin **E**cho: the *entire image* comes from one excitation. A very long echo train (turbo factor ~128–256) runs once, filling roughly half of k-space; the missing half is synthesized from conjugate symmetry. One slice ≈ one breath-hold beat — sub-second.

**Contrast & good for —** Heavy T2: effective TE of ~60–100 ms with an effectively infinite TR, so signal follows pure e^(−TE/T2) — *static fluid* (bile, urine, CSF, bowel content) is maximally bright and everything else fades. This is the snapshot sequence: MRCP, MR urography, bowel, fetal imaging, the breathless or uncooperative patient, and fast survey stacks.

**How it runs —**

```
RF   90° | 180° × ~150 (one single shot, one TR)
echoes:  ✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦✦
         acquire 5/8 of k-space lines only
         │ k-center echo here ─ effective TE (~60–100 ms)
         └── then fill the other 3/8 by conjugate symmetry + phase map
```

- **Physics deep-dive — why "half-Fourier" needs a phase map, and why single-shot blurs.**

    - k-space is (ideally) conjugate-symmetric: line at +k_y is the complex mirror of line at −k_y. In a perfect world you could acquire exactly half and mirror the rest. In reality, phase errors (motion, off-resonance, eddy currents) break the symmetry, so HASTE acquires a little *more* than half — typically **5/8** — and uses the extra low-resolution lines to build a smooth phase-error map, then fills the remainder: mirror + phase correction. Acquire less than ~5/8 and the phase estimate degrades → ringing/ghosting artifacts.

    - Blur: as in all TSE, each successive echo has decayed more, so a 150-echo train spans a huge T2 window — the later (edge-of-k-space) echoes are faint → HASTE is inherently blurrier than multi-shot TSE. The effective TE is a compromise: long enough for heavy-T2 contrast, short enough that the center of k-space still has signal. TR is effectively infinite → **no T1 weighting at all**; you cannot "T1-weight" a HASTE.

- **Physics deep-dive — HASTE and SPACE: the same trick, opposite purposes.**

    - Both are TSE trains that refocus below 180°, and both lean on the same machinery: a reduced-angle pulse parks magnetization along z, a later pulse recalls it as a stimulated echo, and EPG keeps the whole thing predictable. Beyond that shared engine, the two sequences could hardly be more different.

    - **SPACE: the train is the point.** A constant-180° train runs out of signal after ~20–30 echoes; a 3D slab needs 100–250. SPACE solves this by banking and recycling: a large EPG-designed envelope, ramping from ~40° to 120–150°, keeps the echoes flat for the entire train. Because its echoes are partly stimulated by design, SPACE gets something in return — the envelope *is* the contrast control: T2-, T1- and dark-fluid-SPACE are different envelopes, not different TEs (entry 4).

    - **HASTE: the contrast is fixed, and only SAR is the problem.** Single-shot forces ~150 refocusing pulses per slice; at 3T that many 180° pulses exceed the SAR limit, so the angles must come down. But HASTE has exactly one job — pure heavy T2, fluid bright — and that look depends on echoes behaving like true spin echoes. Drop toward 40° the way SPACE does and the signal fills with stimulated echoes carrying T1 flavor: the bright-fluid contrast drifts. So HASTE only dips, in a repeating pattern near 180° (e.g. 130°→90°→110°→130°) — enough to shave energy (SAR ∝ α²), keeping the stimulated fraction minimal and the contrast cost small.

    - The telling sign: at 1.5T, where SAR is a quarter of 3T, HASTE runs constant 180° — no workaround needed — while SPACE runs its envelope at every field, because the envelope is its purpose.

**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| Effective TE | 60–103 ms (MRCP 66–87) | Longer = heavier T2, darker background, more blur; shorter = SNR ↑ |
| Partial Fourier | 5/8 (4/8 only with parallel imaging) | The half-Fourier engine; don't push below 5/8 |

*Geometry & speed*

| Knob | Typical value | Turning it… |
|---|---|---|
| Slice thickness | 3–8 mm per use | Thicker = SNR for fast surveys; thin slabs (MRCP) trade SNR for selectivity |
| Averages | 1 (single-shot) | Repeat = SNR at the cost of motion immunity — the point is usually to not repeat |

*Suppression & SAR*

| Knob | Typical value | Turning it… |
|---|---|---|
| Refocusing schedule | 180° at 1.5T; variable FA at 3T | The 3T SAR valve |
| Fat suppression | Fat Sat / SPAIR; heavy-T2 often none | Spectral suppression costs SAR on top of the train — balance per protocol |

**Artifacts & pitfalls —** Blur hides lesions under ~5 mm (long train — accept the resolution limit); SAR ceiling at 3T; half-Fourier ghosting when phase drifts mid-shot; SNR is set by geometry, not averaging — each line is read once per shot and there is no intra-shot averaging, so thin slices silently kill SNR (repeating the whole shot N× is possible but multiplies time and defeats the motion advantage). Not a high-resolution anatomy sequence — pair it with TSE where detail matters.

**Used in this vault —** Wherever a motion-immune heavy-T2 snapshot is wanted: abdominal survey stacks (liver, pancreas, kidneys — coronal and sagittal breath-holds), fluid-imaging variants (thin-slab MRCP projections, MR-urography-style volumetry), and as a fast localizer in interventional work. The cholesteatoma-diffusion application is a separate animal (entry 8).

---

## 6. BLADE — PROPELLER-style motion-robust TSE

**What it is —** TSE read out in **rotating rectangular strips ("blades")** that all pass through k-space center, instead of horizontal lines: each blade is a short TSE train (8–32 lines), and successive blades are rotated by ~180°/N_blades until the disk is covered (PROPELLER physics; Siemens calls it BLADE).

**Contrast & good for —** T1/T2/PD with **built-in motion correction** — the motion-robust rescue: restless patients, orbit/posterior fossa pulsation, abdomen without breath-hold, spine in tremor. Wherever cartesian TSE ghosts, BLADE is the answer.

**k-space picture —**

```
        k_y
         │        Each blade = a short TSE train (8–32 lines)
      ◇◇◇◇◇◇◇◇   rotated by ~180°/N between blades.
       ◇◇◇   ◇◇◇
        ◇◇◇◇◇  ◇◇  Center of k-space is visited by EVERY blade →
       ◇◇◇◇◇◇◇◇    low-frequency phase errors (motion) are measured
         └──────── k_x   many times → can be unwound retrospectively
```

- **Physics deep-dive — how "oversampling the center" becomes motion correction.**

    - **Why motion shows up as phase.** The phase-encode gradient is fixed in space: for each line the scanner sets one spatial frequency k, and every position x is stamped with the phase −2π·k·x. When the object shifts by Δx, the tissue slides along that fixed gradient and receives the stamp of its new position — its original phase plus one extra term, −2π·k·Δx, identical for every piece of tissue. What matters is that the extra term depends on which k-space line is being sampled: near the center (small k) the phase error is negligible, while at the outermost lines (large k) it reaches a full 180° flip. That one fact predicts the whole damage pattern — contrast lives in the k-space center, so it survives; fine detail lives in the edges, so it smears; and because every line carries a different pose's error, the inconsistencies reconstruct as ghosts along phase-encode. It is also the key to the repair: the small, clean errors at the center let the reconstruction estimate the displacement Δx, after which every point of the blade can be multiplied by the opposite phase — undoing the motion's stamp even at the outer lines, where it was largest. Rotation is repaired differently: it gives each spin a phase change that depends on that spin's own position, so there is no single phase to undo — instead the blade's data is rotated back by the estimated angle.

    - **What BLADE's oversampling buys.** Every blade crosses the k-space center, so the same central region is measured N_blades times, at N_blades different moments — each carrying the object's current rotation and its phase ramp. Motion now shows up as what it is: *inconsistent measurements of the same data*. Because the central region's phase error is small but measurable, the reconstruction can:

    - 1. Estimate each blade's rotation and translation by correlating its central data against the others (registering the low-resolution image each blade alone forms),
    - 2. Correct the blade before gridding it into k-space — unwinding the phase ramp,
    - 3. Reject outright a blade that moved too far through-plane (its central data disagrees with all others).

    - This is *retrospective* correction — no navigator needed for in-plane motion. Through-plane motion swaps which tissue is in the slice, so it cannot be corrected — only detected and rejected, and rejection is a poor tool against continuous breathing. Hence the body pairing: a PACE navigator gates blades to a consistent respiratory position, *preventing* what correction cannot fix.

    - **The geometry: paddles tiling a disk.** Each blade is a short TSE train laid as a thin rectangle through k-space center — full length, L lines wide (blur caps the train, hence the narrow width). Rotating a paddle by 180° gives the same strip back, so N blades rotated by Δθ = 180°/N cover the full circle. Cartesian imaging fills only the square; the blades must seal the whole disk of radius k_max without gaps, because empty wedges in k-space reconstruct as streaks.

    - **The minimum is the condition that seals the rim — the math follows the mechanics.** A blade of width W, seen from the center at radius r, covers an angular span that shrinks with distance: half-angle arcsin(W/2r), smallest at the rim (r = k_max). Adjacent blades (Δθ apart) must therefore at least touch at the rim:

      ```
      Δθ ≤ 2·arcsin(W / 2·k_max) ≈ W / k_max
      ```

    - Substitute Δθ = π/N (180° divided among N blades), W = L·Δk, and k_max = Δk·N_cart/2, and it collapses to:

      ```
      N·L ≥ (π/2)·N_cart ≈ 1.57 × cartesian lines
      ```

    - Example: a 256-line cartesian scan needs ≥ ~402 blade lines — met by, say, 17 blades × 24 lines (408). This is the irreducible price of the circular acquisition; everything above it is the redundancy knob. The disk's four corner triangles outside it are never sampled — accepted, zero-filled, a small diagonal-resolution cost.

    - **Blade coverage chooses how much extra redundancy to buy.** On the Siemens console, 100% is the bare minimum that seals the disk; 125–175% keeps more blade data than sealing requires — extra overlap at the rim and extra passes through the center — giving the motion correction more correlated data to compare, at proportionally longer scan time.

- **Physics deep-dive — the blade-width trade, the effective-TE caveat, and the fastBLADE redesign.**

    - The same total data (N·L, fixed by the π/2 minimum) can be packaged as few thick blades or many thin ones, and the two extremes buy opposite things. Every blade pays a full TR (excitation + train + dead time) regardless of how many lines it carries; every line pays one echo spacing.

    - **Thin blades, many of them (small L, large N).** The short train means the amplitude envelope across the blade decays little — the lines are nearly uniform, so width-direction blur is minimal. Many blades also mean fine angular sampling (small Δθ): the disk is tiled smoothly, rim overlap is generous, and the center is visited N times — more independent low-resolution snapshots for the motion correction. The cost is overhead: each blade re-pays the full TR, so scan time is dominated by dead time, and each blade's individual estimate gets noisier as it carries fewer lines.

    - **Thick blades, few of them (large L, small N).** Fewer TRs, less dead time — faster for the same data volume. The cost is the blur itself: across a long train, each later echo is read further along its T2 decay, so the k-space envelope across the blade's width falls steeply — and a decaying k-space envelope broadens the point-spread function (blur along the width direction), worse for short-T2 tissues whose envelope drops fastest. Coarse angular sampling also leaves the rim just-sealed with little overlap — weaker motion estimates.

    - **The effective-TE caveat — contrast is adjustable, but not free.** In 2D TSE, reordering freely picks which echo fills the k-space center — TE costs nothing. A blade's middle line *is* the center line, so the scanner must instead shift the whole train (longer 90°→first-180° interval) or widen the echo spacing to land the mid-train echo on your requested TE. Both move every echo later in the T2 decay: SNR falls, the across-blade envelope steepens (more blur), TR lengthens — and the short train leaves only a narrow TE window anyway. So: choose the flavor as in TSE, but pay an SNR/blur price and accept the narrow range. The tax is one-sided: T1-BLADE's short TE costs almost nothing (near-cartesian quality); T2-BLADE pays in SNR, sharpness and time — and often compromises the weighting itself (TE pulled back, slices thickened) just to stay usable, which is exactly the margin fastBLADE exists to restore.

    - **fastBLADE — the EPG redesign of the blade itself.** A standard blade refocuses near 180°, so its echo amplitudes decay along the train and the blur envelope is unavoidable. fastBLADE applies the variable-flip-angle machinery of entry 4 (park-and-recall, EPG-designed schedules — the SPACE/hyperecho idea) *inside* the blade: the schedule holds the echo amplitudes flat across the train, removing the k-space decay envelope — the primary source of width blur. That is what lets it run wider blades at acceptable sharpness: wider blades mean fewer of them, so the same disk is covered faster. The tradeoff: flatness is bought by cycling magnetization through z-storage, so the stimulated fraction grows along the train — a small tissue-dependent weighting drift (minor residual blur) — and it remains a BLADE, retaining the family's time overhead versus cartesian. It earns its keep wherever motion robustness must meet speed: long stacks in restless patients, breath-hold-limited abdominal work, and repeated or continuous imaging where standard BLADE would be too slow.

**Tunable choices —**

*Motion & quality*

| Knob | Typical value | Turning it… |
|---|---|---|
| Blade coverage | 100–175% | ↑ = more redundancy = better motion correction + SNR, longer scan |
| Lines per blade | 8–32 | Shorter blades = less intra-blade decay; more blades needed |
| FastBLADE variant | on (cryoabdomen work) | Siemens' accelerated BLADE redesign (EPG-designed schedules) for interventional speed |

*Body of the sequence*

| Knob | Typical value | Turning it… |
|---|---|---|
| Effective TE | set on console — scanner positions the train (start shift / echo spacing) so the mid-train echo lands there | Adjustable, but it costs: longer TE = whole train later in the T2 decay → SNR ↓, blur ↑; short train = narrow range |
| Fat suppression | Fat Sat / SPAIR / dark-fluid BLADE | Standard choices; BLADE-FLAIR exists for motion-prone neuro |
| PACE pairing | on for abdomen | Navigator gating + blade self-correction = body-workhorse combo |

**Artifacts & pitfalls —** ~1.5× scan time versus cartesian TSE; radial streak/ring artifacts when blades are too few or echo trains too long; through-plane motion is rejected (data loss), not corrected; near-transverse-only design — not a sagittal/coronal rescue. Blur behaves like TSE-with-redundancy: choose lines/blade deliberately.

**Used in this vault —** Wherever motion would otherwise ghost the TSE: motion-prone neuro work (T2, T1, dark-fluid and post-contrast variants), free-breathing abdominal and MRCP imaging, spine and adrenal protocols, and MSK rescue for restless patients — with fastBLADE reserved for repeated or continuous imaging, where speed joins the motion requirement.

---

## 7. Restore (TSE-R) — driven equilibrium

**What it is —** A standard TSE with one extra pulse at the end of the echo train: a **−90° "restore" pulse** that flips whatever transverse magnetization remains *back up to +z* before the next TR begins. Siemens marks it with an `r` or `R` in the sequence name (e.g. `t1_tse_r`, `t2_tseR`).

**Contrast & good for —** (a) T1-weighted thin-slice, small-FOV work where thin slices + short TR starve the next TR of magnetization — restore recycles it into SNR and T1 sharpness; (b) a T2-flavored bright-CSF variant that runs at TR ~1500 ms instead of 3000+ while keeping CSF bright.

**How it runs —**

```
RF   90°   180°×N … (echo train)  −90° restore
      ▄▄▀    ▀▄▄ ▀▄▄ ▀▄▄          ▄▄▀
M_xy: ✦✦✦✦✦✦✦✦✦✦✦  ─────────────►  flipped to +z → next TR starts near full M₀
```

- **Physics deep-dive — what "driven equilibrium" actually rescues.**

    - Without restore, each TR of a short-TR TSE starts from whatever M_z the previous train left behind — for thin slices and short TR this is little, so signal is weak and T1 contrast muddy (every tissue saturates toward the same low value). The restore pulse is the trick of *driven equilibrium* (also called fast-recovery): the residual transverse magnetization — which would otherwise be spoiled away as wasted signal — is coherently returned to +z. The next excitation then starts from near-equilibrium magnetization instead of a depleted one. Gains: **SNR up** (you harvest signal that TSE normally throws away) and **T1 contrast restored at short TR** (tissues recover more completely between TRs).

    - The cost is a *direction* of contrast: because the restored signal carries the T2 flavor of the transverse state at the end of the train, restore brightens long-T2 tissues. Used on a T1 protocol this is a feature (pituitary/CSF stand out); used carelessly it contaminates T1 weighting — which is why T1 protocols that need *pure* T1 (e.g. post-contrast quantification) avoid it, while the bright-CSF lumbar variant embraces it deliberately: T2-like CSF brightness at half the TR.

**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| Restore on/off | T1-R: thin-slice T1; T2-R: bright fluid | Off = pure TSE (keep if T1 purity matters more than SNR) |
| TR (1.5T) | T1: ~450–800 ms either way (restore doesn't move the optimum — it removes the thin-slice SNR penalty at the short end) · T2: ~1500 ms with restore (vs ~2500–8000 without) | For T1, restore buys the SNR of a long TR at the contrast of a short TR; only the T2 flavor gets a genuine TR shortening — the T2-R trick works only at short TR |

*Geometry*

| Knob | Typical value | Turning it… |
|---|---|---|
| Slice thickness | 2–3 mm | Thin slices are why restore earns its keep — at 5 mm the benefit fades |

**Artifacts & pitfalls —** Restore reintroduces T2-flavor into whatever contrast you ask for: never add it to a sequence whose T1 contrast is the diagnostic question; the bright-CSF variant will hide lesions that *are* CSF-like. One extra RF pulse per TR — small SAR/time cost. Not needed at thick slices or long TR (little residual transverse signal to rescue).

**Used in this vault —** Two jobs. The T1-R flavor appears wherever thin-slice, small-FOV T1 must hold SNR at short TR — sellar work, the IAM (as an SE-restore at 1.5T), post-contrast head-and-neck; the T2-R flavor serves bright-CSF work in the spine and thin-slice rectal/anal T2. Whenever a protocol asks for thin slice + short TR + SNR all at once, this is the physics doing the work.

---

## 8. HASTE-DWI — non-EPI diffusion (TSE-based)

**What it is —** A single-shot TSE image made diffusion-weighted: one Stejskal–Tanner gradient pair (the same physics as EPI-DWI — file 04) is placed around the **first** refocusing pulse of the HASTE train, and the weighting it stamps then survives into every echo — so the whole image is one diffusion-weighted TSE shot.

**How it runs —**

```
        [fat sat]      90°            180°            180°            180°       …
RF:      ▀▄            ▄▀             ▀▄              ▀▄              ▀▄
G_diff:               ▄▄▄▄▄▄        ▄▄▄▄▄▄
                       │← δ →│        │← δ →│
                        └── pair straddles the FIRST 180° only ──┘
echo:                                 ✦₁              ✦₂              ✦₃  …  ✦ₙ
                                      ↑
                        diffusion-weighted — and every later echo of the
                        single-shot train carries the SAME weighting
```

- The first lobe dephases each spin by its position; the 180° mirrors the phases; the second lobe cancels the first **only for spins that stayed put** — spins that diffused in between now sit elsewhere, so they keep a random phase spread and lose signal (S = S₀·e^(−b·D)). That spread is irreversible: the later 180°s cannot refocus it, and no more diffusion gradients are played — so every echo of the train carries the same attenuation. One pair, uniformly weighted single-shot image, b set once.

**Contrast & good for —** True diffusion contrast (b ~1000-class; ADC from b0+b pairs) **where EPI cannot go**: the petrous bone and skull base. EPI's Achilles heel is susceptibility — at air-bone interfaces the field tears and the image distorts beyond use. TSE readouts refocus static field errors on every echo, so this diffusion variant is practically distortion-free there. Clinical anchor: **cholesteatoma**, whose restricted diffusion separates it from simple middle-ear fluid.

- **Physics deep-dive — the distortion-free diffusion readout, and its price.**

    - Why is EPI so distorted at the skull base? EPI fills all of k-space in one shot by *alternating* the readout gradient — it never stops to refocus the field. Off-resonance (susceptibility) accumulates across the whole readout as a large, spatially varying phase error → pixels shift (distortion) and signal drops. TSE, by contrast, inserts a 180° pulse *between every echo*; each refocus resets the accumulated off-resonance phase, so the image geometry stays true. That is the entire trick of HASTE-DWI: accept the TSE readout's slowness (one echo per refocus) in exchange for repeated refocusing.

    - The price is threefold: (1) **SNR** — a single-shot TSE is one average with a long train; diffusion weighting further decays signal, so thin-section cholesteatoma work sits at the edge of feasibility; (2) **blur** and modest resolution (long train, as in entry 5); (3) **SAR** — the most demanding combination in this family (diffusion gradients + fat suppression + ~100 refocuses). On a 1.5T scanner it is legal; at 3T it is not — which is why the vault states 1.5T-only.

**Tunable choices —**

*Diffusion*

| Knob | Typical value | Turning it… |
|---|---|---|
| b-values | b0 + b~800–1000 | ≥2 b-values for ADC; higher b = more restriction contrast, less SNR |
| Field strength | 1.5T | 3T infeasible — SAR (vault states this explicitly) |

*Readout*

| Knob | Typical value | Turning it… |
|---|---|---|
| Effective TE | long (single-shot + diffusion time) | Longer = more T2 shine-through risk, lower SNR |
| Fat suppression | Fat Sat / SPAIR | Mandatory-ish: keeps chemical-shift ghosts off the train |

**Artifacts & pitfalls —** T2 shine-through (always read the ADC, not just the high-b image); low SNR in thin anatomy (average more — it is not motion-limited here as in EPI); don't reach for it where EPI-DWI works — this is the specialist tool for the skull base, not a general diffusion replacement.

**Used in this vault —** One application: cholesteatoma imaging of the IAM/petrous bone, in both coronal and axial planes, explicitly restricted to the 1.5T scanner in the protocol notes.

---

## Family summary

| Sequence | Weighting | Speed vs SE | Motion tolerance | SAR | Slice character |
|---|---|---|---|---|---|
| SE | T1/PD | 1× | poor | low | 3–5 mm, sharpest |
| TSE | T1/T2/PD | ×turbo factor | poor–fair | medium–high | 2–5 mm |
| IR (FLAIR/STIR/DIR) | T2 + nulling | slow (long TR) | poor | high | 3–5 mm |
| SPACE | T2/PD/T1, 3D | ×100–250 | fair (long 3D) | high, managed by schedule | 0.5–1 mm iso |
| HASTE | heavy T2 | one shot/slice | **excellent** | highest | 4–8 mm |
| BLADE | T1/T2/PD | ~1.5× vs TSE | **self-correcting** | high | 3–5 mm |
| Restore | T1 sharp / bright-fluid T2 | short-TR | fair | +1 pulse/TR | 2–3 mm |
| HASTE-DWI | diffusion | one shot/slice | excellent | highest → 1.5T | 2–4 mm |

---

**Key sources** — Siemens Healthineers (MAGNETOM World protocols, hyperechoes in prostate work, syngo RESOLVE); mriquestions.com: [FSE parameters](https://www.w.mri-q.com/fse-parameters.html), [driven equilibrium](http://www.ww.mriquestions.com/driven-equilibrium.html), [SPACE](http://s.mriquestions.com/spacecubevista.html), [HASTE](http://s.mriquestions.com/hastess-fse.html), [PROPELLER](http://s.mriquestions.com/propellerblade.html); Radiopaedia: [SPACE](https://radiopaedia.org/articles/space-mri-sequence), [TIRM](https://radiopaedia.org/articles/turbo-inversion-recovery-magnitude-1), [DIR](https://radiopaedia.org/articles/double-inversion-recovery-sequence); papers: Weigel & Hennig, hyperechoes (MRM 2006); Hirokawa et al., BLADE coverage (JMRI 2008).

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — 8 spin-echo entries |
