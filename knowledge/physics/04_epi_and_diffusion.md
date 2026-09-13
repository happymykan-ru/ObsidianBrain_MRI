# EPI, Diffusion & Functional MRI

**Version:** 1.0 | **Date:** 2026-09-08

This family is built on one readout — **echo-planar imaging (EPI)** — which fills all of k-space in a *single shot* by rapidly alternating the readout gradient. EPI is the fastest readout in MRI, and its unique failure modes (distortion, ghosting) dominate the physics of everything below: diffusion, perfusion, and fMRI all ride on EPI because they need a *snapshot* of the whole image while some transient contrast (diffusion weighting, a contrast bolus, brain activation) is alive.

Two threads run through the whole file:

1. **Why single-shot?** Diffusion gradients, first-pass contrast, and BOLD changes are transient — the image must be captured in one instant, not assembled over seconds.
2. **Why is EPI distorted, and what do we do about it?** Off-resonance accumulates across the long readout as pixel shifts. The cures (shorter echo trains via parallel imaging, segmented readouts like RESOLVE, swapping phase-encode direction, and the non-EPI alternative HASTE-DWI from file 02) each have their own price.

Values throughout are recommended typical ranges — your protocols win where they conflict.

---

## 1. The EPI Readout (single-shot and segmented)

**What it is —** The readout engine: after one excitation, the readout gradient alternates polarity back and forth, tracing a **zig-zag (boustrophedon) path through k-space** — one "row" per gradient lobe, each row acquired in the time it normally takes one line. A 128-row image needs ~50–100 ms total. Two flavors:

- **Single-shot EPI (ss-EPI)**: all rows after *one* excitation — the snapshot engine of DWI/DSC/BOLD.
- **Segmented/multishot EPI**: the path is split into several shots (RESOLVE uses 3–7 readout segments, each a few rows, with a navigator between shots).

**Contrast & good for —** The *contrast* is whatever the preparation before the readout creates (diffusion weighting, inversion, saturation); EPI itself is a T2\*-weighted readout. Its job is speed: an entire brain volume in ~100 ms × (slices per TR).

**How it runs —**

```
RF    90° (or prep)
       ▄▄▀
G_read   ▁▂▃▄▅▆▇█▇▆▅▄▃▂▁▂▃▄▅▆▇█▇▆▅▄▃▂▁ ...  ← zig-zag through k-space rows
G_phase  ▁ ▁ ▁ ▁ ▁ ▁ ▁ ▁ ▁ ▁ ... tiny blips between rows
k_y  → row 1 (left→right), blip, row 2 (right→left), blip, row 3 …
```

- **Physics deep-dive — the distortion problem, from first principles.**

    - **The mechanism: a phase ramp in disguise.** Every row of k-space is read at a slightly later time, and an off-resonance spin (Δf: field error, susceptibility, chemical shift, eddy currents) accumulates phase in time — Δφ = 2π·Δf·t. Time marches with row number, and row number *is* k_y — so the phase error is a **linear ramp in k_y**: Δφ = 2π·Δf·(echo spacing)·row. A linear phase ramp in k_y is mathematically identical to a genuine phase-encode of a displaced position (multiplying k-space by e^(i·k_y·Δy) shifts the image by Δy — the Fourier shift theorem, the same one behind BLADE's motion story in file 02). The reconstruction cannot tell gradient-phase from off-resonance phase, so it faithfully places each voxel at the *wrong* position — a clean displacement, not blur:

      ```
      pixel shift ∝ Δf × echo spacing × EPI factor       (along the phase-encode axis)
      ```

    - **Per-voxel, so the error field's shape decides the look.** The shift is proportional to each voxel's own Δf. Where Δf is uniform, every voxel shifts equally — the region just translates. Where Δf *varies* across space (a gradient in the error — skull base, sinuses, air-tissue), neighboring voxels shift by different amounts: the image **stretches** where they are pulled apart and **compresses** where they are pushed together — and where voxels compress, their signal piles up into bright bands; where they stretch, it dims. This is the same physics as the chemical-shift artifact on the readout axis (fat shifts along readout while kx is swept) — one mechanism, two axes, two magnitudes: the blip-direction error is huge because the train spans ~50–100 ms, the readout's small because it spans ~1 ms.

    - **What controls the size of it — and the cures.** Distortion grows with total readout duration (EPI factor × echo spacing), which is why it is worst at high resolution and why **parallel imaging is a distortion cure, not just a speed cure** — GRAPPA/SMS skip rows and divide the effective echo spacing (and so the shift) by the acceleration factor. The shift direction depends on the sign of Δf and the blip direction: swapping phase-encode (A>>P → P>>A) flips the distortion, and acquiring both (blip-up/down pairs) lets software estimate and remove the field-induced shift. Fat is off-resonance by ~220 Hz (1.5T) / 440 Hz (3T) — at 3T unsuppressed fat can shift entirely across the image, hence mandatory fat suppression on EPI (SPAIR — B₁-robust, the DWI standard).

    - A second, EPI-specific artifact: **Nyquist/odd–even ghosting** — even rows are read left→right, odd rows right→left; if the two sets are not perfectly aligned (eddy currents, timing), a half-FOV shifted ghost appears. Modern scanners correct it with reference scans; residual ghosts signal gradient timing problems.

- **Physics deep-dive — segmented EPI with diffusion (RESOLVE), and the navigator that makes it work.**

    - **What segmentation buys.** Dividing the readout into 3–7 shots — each reading only a few rows — shortens the per-shot readout: off-resonance accumulates little per shot, so distortion and blur fall and higher resolution becomes possible than in ss-EPI. Each shot is a complete mini-sequence: its own 90°, its own diffusion pair (identical, same b), its readout segment, then the navigator:

      ```
      one shot (repeated per segment):

      RF:    90°           180°                         (diffusion prep — same pair, same b, every shot)
              ▀▄            ▀▄
      G_diff:   ▄▄▄▄▄▄        ▄▄▄▄▄▄
      G_read:                            ▁▃▅▇█▇▅▃▁    ← EPI readout, only a FEW rows
      G_phase:                           ▁▁▁▁▁        ← few blips = segment N
      signal:                                    ✦✦✦    ← segment N of k-space
      navigator:                                      ░░  ← fixed small 2D acquisition (below)
      ```

    - **The problem segmentation creates.** Each shot is a separate excitation, and diffusion gradients are enormous — any tiny motion between shots stamps each shot with its own phase error (a constant phase plus a linear ramp = a spatial shift, possibly higher orders). Uncorrected, the segments disagree and recombine into inter-shot phase ghosts. (ss-EPI never faces this: one shot = the whole image, and a global phase is invisible in the magnitude.)

    - **The navigator — a fixed, identical thumbnail in every shot.** The navigator is *not part of the segment*: it is a separate, small, fully-sampled 2D acquisition (a low-resolution block of the k-space center), identical in design in every shot. Because all navigators cover the same k-space, they reconstruct directly comparable low-resolution images of the slice — thumbnails whose only differences are the motion between shots.

    - **The correction is registration.** Align each shot's thumbnail against the reference (shot 1's): the measured shift (Δx, Δy) is that shot's motion fingerprint. A spatial shift corresponds to a linear phase ramp in k-space (the shift theorem again), so the reconstruction multiplies the shot's segment by the *conjugate* ramp — undoing the shot's shift — and the now-aligned segments combine into one k-space. The segments themselves are never registered against each other; the navigators mediate.

    - **The limits.** The navigator is acquired just *after* the segment — motion in between goes uncorrected. And only low-order errors (shift) are measured: rotation and non-rigid motion produce higher-order phase the registration cannot fix — the residual shot-misalignment ghosts. That residual risk is one reason body DWI sometimes stays single-shot, where each slice is one snapshot and the problem never arises.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| EPI factor | full image single-shot vs 3–7 segments (RESOLVE) | Fewer rows per shot = less distortion/blur, longer scan |
| Parallel imaging | GRAPPA 2 (DWI); SMS 2 (faster volume) | Divides effective echo spacing → *less distortion per unit time* |
| Phase-encode direction | A>>P or P>>A | Flips distortion; choose to push artifacts out of the region of interest (e.g. temporal lobes) |
| Fat suppression | SPAIR (standard), Fat Sat | Without it, fat shifts/ghosts across the phase axis |
| Blip-up/down pairs | on (correction) | Enables post-hoc field-based distortion correction |

**Artifacts & pitfalls —** Distortion (above); dropout where off-resonance is extreme; Nyquist ghosting; fat ghosts at 3T. Motion during the diffusion prep ruins every flavor — the gradients can't tell diffusion from patient motion (single-shot freezes only the readout). RESOLVE additionally needs phase-consistent shots, so it wants a still patient and earns its place where anatomy is static but distortion matters (skull base, head-and-neck); moving anatomy favors single-shot (ss-EPI or HASTE-DWI).

**Used in this vault —** Underneath everything in this file: single-shot EPI diffusion (liver, kidney, pancreas, breast, brain trace), an EPI-T2\* hemorrhage screen, DSC perfusion and BOLD fMRI (entry 7), the SMS DTI (entry 4), and RESOLVE segmented diffusion wherever distortion matters — the majority of the vault's diffusion, and the brain protocols' default.

---

## 2. DWI / ADC — Diffusion-Weighted Imaging

**What it is —** An EPI image made sensitive to the *random thermal motion of water* by a pair of strong gradient pulses straddling a 180° refocus (Stejskal–Tanner) — a spin-echo EPI (90° excitation, 180° refocusing; the 180° also removes static dephasing). The vault runs it as RESOLVE (readout-segmented, low distortion — the brain default) or ss-EPI (abdomen), plus the non-EPI HASTE-DWI (file 02) for the skull base.

**How it runs —**

```
RF:     90°               180°                          ← then the EPI readout
         ▀▄                ▀▄
G_diff:     ▄▄▄▄▄▄            ▄▄▄▄▄▄     ← two identical unipolar lobes, one each
             │← δ →│           │← δ →│        side of the 180° — not a continuous
             └──────── Δ ─────────┘            bipolar pair; the gap is the point
G_read:                                          ▁▃▅▇█▇▅▃▁…   ← EPI zig-zag, after
```

**Contrast & good for —** Diffusion restriction: **acute stroke** (minutes after onset), abscess vs necrotic tumor, highly cellular tumors (lymphoma, high-grade glioma), cholesteatoma, and lesion characterization anywhere. ADC (the quantitative map) separates true restriction from T2 effects.

- **Physics deep-dive — the full diffusion story, step by step.**

    - **Step 1 — what the gradients do.** The pair sits symmetrically around the 180°: lobe 1 dephases the spins, the 180° mirrors them, lobe 2 rephases — *exactly* for stationary spins, but a spin that wandered during the interval sits at a new position, so lobe 2 cannot fully undo lobe 1 → residual phase spread → signal loss. The faster water diffuses, the more loss; the sensitization is the **b-value**, and the gap Δ − δ/3 is the diffusion time — the window in which molecular motion reveals itself:

      ```
      b = γ² · G² · δ² · (Δ − δ/3)
      G  gradient amplitude      δ  lobe duration      Δ  time between lobe onsets
      ```

    - **Step 2 — the signal law, and the trap in it.** S(b) = S₀·e^(−b·D), so ADC = −(1/b)·ln(S(b)/S₀). The trap: S₀ carries T2 weighting, so T2-bright tissue stays bright on high-b even without restriction (**T2 shine-through**). ADC divides out S₀: restricted tissue is *low* ADC (dark on the map), T2-bright-but-not-restricted is normal/high — always read the ADC.

    - **Step 3 — directions, and the trace as a geometric mean.** Each direction is a complete separate acquisition — the same sequence with the diffusion gradients oriented along x, then y, then z — plus a b0 reference. "4-scan trace" means exactly that: **b0 + 3 directions** (the fourth scan is the unweighted reference, not a fourth direction). Diffusion in white matter is anisotropic (faster along axons), so a single direction only measures one projection; the three directional images are combined per voxel as the **geometric mean**:

      ```
      S_trace = (S_x · S_y · S_z)^(1/3)     ≡  arithmetic mean of the log-signals
      ```

      The geometric form is what makes trace weighting **rotation-invariant**: the mean of any three orthogonal directions equals the mean diffusivity (one third of the diffusion tensor's trace), whichever orthogonal triplet was used — the tissue's average diffusion with the directional bias averaged out. ADC is then fitted from S_trace vs S₀. b-value choice: low b (50–300) suppresses blood signal and serves body screening; b 800–1000 is the brain/liver standard; b 1500+ adds restriction contrast for prostate/neuro-oncology at SNR cost (the vault runs b-pairs and b-triples from 50→1500 by region).

    - **Step 4 — the readout choice, briefly.** RESOLVE's segmented readout cuts distortion for still anatomy (the full navigator story lives in entry 1); moving anatomy favors single-shot (ss-EPI, or non-EPI HASTE-DWI for the skull base).

- **Physics deep-dive — why high-b images are read, not fitted (why b1500 can't feed the ADC).**

    - The ADC formula assumes a **monoexponential decay** — one free-diffusing water pool, a straight line on a plot of ln(S) against b. Tissue water is not one pool: at very low b (<~200) a fast perfusion-like component contaminates the signal (IVIM), and at high b (≥1000) only the slow, restricted compartment survives — so the curve is steep at low b, roughly straight in the middle, and **flattens at high b** (the non-Gaussian/kurtosis regime):

      ```
      ln S
       │● b0
       │ |
       │  |   steep early drop — the perfusion (IVIM) component
       │   |
       │    |● b~200
       │     ╲───────────── mid-b: near-straight (tissue diffusion) ──
       │       ╲                       ╲  ← extending this line…
       │         ╲● b1000                ╲
       │           ╲⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒  high-b flattening:
       │            ⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒⌒● b1500 ← sits ABOVE the
       │                                                   mid-b extension
       └──────────────────────────────────────────────────► b
      ```

    - Fitting a monoexponential through b0 and b1500 therefore measures a compromise slope that sits *below* the true tissue line — the high-b point lies above it, because the decay has flattened. The result: a systematically **underestimated ADC**, and — the deeper problem — an ADC that **depends on which b-values you chose**: ADC(b0–b1000) ≠ ADC(b0–b1500), so the number is no longer comparable to the standard b1000-derived values the literature and thresholds use. (The formal repairs are kurtosis or biexponential modeling — extra parameters, extra b-values, beyond routine clinical practice.)

    - And a third, practical reason: at b1500 the signal in non-restricted tissue is tiny, so the high-b point is noise-dominated — a noisy point biases a two-point fit further.

    - Hence the clinical division of labor: the **high-b image is read qualitatively** — tumor and restricted tissue stay bright while normal tissue drops away (the conspicuity tool of the prostate/neuro-oncology protocols) — while the **ADC map is fitted from the standard lower-b pair** (b0/b50 + b800–1000), where the monoexponential model still holds. High b answers "where is it restricted?"; the ADC answers "how restricted?" — and the two must not be mixed.

**Tunable choices —**

*Diffusion weighting*

| Knob | Typical value | Turning it… |
|---|---|---|
| b-values | 50–1500 depending on region (see above) | Higher b = more restriction contrast, less SNR, more motion sensitivity |
| Directions | 3 (trace) routine; more for DTI | 3 orthogonal → trace; ≥6 → tensor (entry 4) |
| Number of averages | b0 ≥ high-b (SNR balance) | Diffusion images are noisy; averaging is the SNR lever |

*Readout*

| Knob | Typical value | Turning it… |
|---|---|---|
| Readout | RESOLVE (neuro/H&N/prostate) vs ss-EPI (body) | Distortion vs scan time vs motion robustness — see Step 4 |
| Segments (RESOLVE) | 3–7 | More segments = less distortion, longer scan |
| Parallel imaging | GRAPPA 2–3 | Distortion cure (entry 1) |
| Fat suppression | SPAIR standard | Mandatory on EPI — see entry 1 |
| Phase-encode direction | swapped if distortion over target | Re-route the artifact |

**Artifacts & pitfalls —** T2 shine-through (always read ADC); distortion and dropout at susceptibility (skull base, mastoid, metal) — the reason for RESOLVE/HASTE-DWI there; motion (diffusion weighting amplifies any motion — patient motion and even CSF pulsation; cardiac-trigger in the cord helps); eddy-current distortion varying with b-value direction (correction options on the scanner); Nyquist ghosts (entry 1). ADC is only as good as its b-pair — two close b-values fit noisy curves.

**Used in this vault —** The stroke/lesion brain protocol (RESOLVE, trace, b50–1000-class); head & neck and skull-base work where distortion rules (including the 1.5T non-EPI cholesteatoma variant, file 02); breast (RESOLVE + SPAIR); body (ss-EPI b50–300–800 in liver/pancreas/kidney); pelvis/rectum/prostate (RESOLVE b50–1500, with the high-b value tuned to prostate tumor conspicuity); and brachytherapy oblique axial work.

---

## 3. DTI — Diffusion Tensor Imaging

**What it is —** DWI with **≥6 non-collinear directions** — the same EPI-DWI basis as the previous entry, only more directions and different analysis — from which the full 3D diffusion behavior is reconstructed as a *tensor* (a 3×3 symmetric matrix describing how fast water diffuses along every axis). The vault's whole-brain DTI runs 20 directions with SMS.

**Contrast & good for —** White-matter architecture: **fractional anisotropy (FA)** maps show tract integrity; tractography reconstructs pathways. Uses: pre-surgical planning near eloquent tracts, trauma/axonal injury, myelination assessment, and research.

- **Physics deep-dive — from directional measurements to the fiber direction.**

    - **What DTI wants.** A single diffusion measurement returns one number — the diffusivity along one direction. White matter needs more: its diffusion has a *shape*, fast along the fibers and slow across them. DTI therefore models each voxel as a **3D ellipsoid**, whose extent in any direction is the diffusivity in that direction, and recovers it from a set of directional measurements.

    - **The ellipsoid, written as a matrix.** A 3D ellipsoid needs six numbers to specify: three axis lengths and three orientation angles. The 3×3 symmetric matrix **D** carries both — the diagonal entries hold the axis lengths as seen from the scanner's frame, and the off-diagonal entries hold the tilt:

      ```
      ┌ Dxx   Dxy   Dxz ┐
      │ Dxy   Dyy   Dyz │      D = the diffusion tensor
      └ Dxz   Dyz   Dzz ┘
      ```

      9 positions, symmetric (Dxy = Dyx…) → 6 independent numbers.

    - **What each entry means — the coupling rule.** Dᵢⱼ answers one question: *if water is pushed along axis j, how much flow results along axis i?* (Fick's law, J = −D·∇C.) Equivalently, in the random-motion picture, Dᵢⱼ is the covariance of molecular displacements — how much a molecule's motion along axis i is statistically linked to its motion along axis j.

    - The **diagonal entries** are the straight-through diffusion: Dxx = how fast water wanders along x (the variance of the displacement along x); Dyy, Dzz likewise for y and z. These three are the ellipsoid's reach along the scanner's axes.

    - The **off-diagonal entries** are the couplings — the tilt. Dxy = whether molecules moving along x also tend to move along y. That is nonzero exactly when the fibers run diagonal to the scanner's axes: a molecule diffusing along a tilted fiber moves in x and y at once, so its x-motion and y-motion are locked together — the covariance captures that lock. A fiber running pure along x has no such link: Dxy = 0. So the six numbers split cleanly: three diagonals = the speeds along the scanner's axes; three off-diagonals = the couplings that appear when the fibers run diagonal to those axes — the tilt, written as numbers. The eigen-decomposition is the search for the frame in which those couplings vanish.

    - **Aligned vs tilted, pictured:**

      ```
      aligned with the scanner frame:
      ┌ λ₁    0    0  ┐
      │  0   λ₂   0  │
      └  0    0   λ₃ ┘

      tilted:
      ┌ Dxx   Dxy   Dxz ┐
      │ Dxy   Dyy   Dyz │
      └ Dxz   Dyz   Dzz ┘
      ```

    - **Question 1 — what are D and u, and why the matmul gives the ADC.** D is the ellipsoid written in the scanner's x-y-z frame, and u is the unit vector of the applied gradient direction — its three components (uₓ, u_y, u_z) are simply that direction's coordinates in the same frame.

    - From the coupling rule, each *column* of D is the flow produced by a unit gradient along one axis: column 1 = the flow from a push along x, column 2 from y, column 3 from z. A gradient along u is a mixture of the three axis-pushes (u = uₓx̂ + u_yŷ + u_zẑ), and diffusion is linear — flows add — so the response to the mixture is the mixture of the responses. That is exactly the first multiplication:

      ```
      D · u  =  uₓ·(column 1) + u_y·(column 2) + u_z·(column 3)

      [3×3] · [3×1]  =  [3×1]        the total 3D flux produced by the gradient along u
      ```

    - The ADC is the diffusion *along* the applied direction — of that flux, how much is along u? The second multiplication reads it back, a weighted sum of the flux's components with u's components as weights:

      ```
      ADC along u  =  uᵀ · D · u

      [1×3] · [3×3] · [3×1]  =  [1×1]  =  one ADC
      ```

      Together the two steps are the definition of the diffusion coefficient: *flow along u, per unit gradient along u.* The expanded equation tells the same story term by term — diagonal terms uᵢ²·Dᵢᵢ are the direct flow along each axis; cross terms 2uᵢuⱼ·Dᵢⱼ are the tilt diverting flow between axes, doubled because the diversion works both ways:

      ```
      ADC =  uₓ²·Dxx + u_y²·Dyy + u_z²·Dzz
             + 2uₓu_y·Dxy + 2uₓu_z·Dxz + 2u_yu_z·Dyz
      ```

      The ellipsoid picture is the same statement in another language: uᵀDu = how far the ellipsoid reaches along u — point along the long axis and the number is big, point across and it is small.

    - **Question 2 — the target: the eigen-decomposition of D.** Once D is known it can be diagonalized — find the three special directions along which D only *stretches*, never rotates:

      ```
      D · eᵢ  =  λᵢ · eᵢ        (tensor times axis = the same axis, stretched by λᵢ)
      ```

      In the ellipsoid picture this is almost obvious: stretching an ellipsoid happens along its axes, so a direction lying on an axis stays on that axis. The three special directions are therefore the ellipsoid's axes — the **eigenvectors** — and the three stretch factors λ₁ ≥ λ₂ ≥ λ₃ are the axis lengths — the **eigenvalues**. Eigenvectors = the ellipsoid's orientation; eigenvalues = its shape. The clinical payoff: in white matter the largest axis λ₁ runs **along the fiber**, so the eigenvector belonging to λ₁ is the fiber direction — the orientation DTI exists to measure. Everything displayed clinically (FA, MD, axial/radial diffusivity, tractography) derives from those six numbers.

    - **Question 3 — how D is recovered: the large matmul.** Each directional measurement gives one scalar, which expanded is one equation in the six unknown entries of D. One measurement cannot pin six unknowns, so the N measurements are stacked into one system, solved per voxel:

      ```
      A (design matrix — one row per direction, [N×6]):

      ┌ u₁ₓ²   u₁y²   u₁z²   2u₁ₓu₁y   2u₁ₓu₁z   2u₁yu₁z ┐
      │ u₂ₓ²   u₂y²   u₂z²   2u₂ₓu₂y   2u₂ₓu₂z   2u₂yu₂z │
      │   ⋮      ⋮       ⋮        ⋮         ⋮         ⋮   │
      │ uₙₓ²   uₙy²   uₙz²   2uₙₓuₙy   2uₙₓuₙz   2uₙyuₙz │
      └                                                    ┘

      d (the unknowns, [6×1]):
      ┌ Dxx ┐
      │ Dyy │
      │ Dzz │
      │ Dxy │
      │ Dxz │
      │ Dyz │
      └     ┘

      m (the measurements, [N×1]):
      ┌ ADC₁ ┐
      │ ADC₂ │
      │   ⋮   │
      │ ADCₙ │
      └       ┘

      together:   A · d = m        [N×6] · [6×1] = [N×1]
      ```

    - Six directions → a square 6×6 system, solved directly. The clinical 20–30 directions → more equations than unknowns → **least squares**, the same machinery as fitting a line to many noisy points:

      ```
      d = (Aᵀ·A)⁻¹ · Aᵀ · m

      Aᵀ·A          :  [6×N] · [N×6] = [6×6]
      (Aᵀ·A)⁻¹·Aᵀ·m  :  [6×6]⁻¹ · [6×N] · [N×1] = [6×1]
      ```

      (per voxel, inline — more directions = noise-averaged, sharper eigenvectors, the reason for 20–30.)

    - **The direction sets — uniform on the sphere.** Directions are spread as evenly as geometry allows: symmetric arrangements (6/12/20 Platonic; 10/15/30 related symmetric sets) for small sets, electrostatic-repulsion-optimized sets (Jones30/60) beyond, since >20 points cannot be perfectly even on a sphere. Uniformity means every orientation is measured with equal statistical strength: no directional bias, a maximally well-conditioned solve, sharper eigenvector estimates. (Opposite directions carry the same information — diffusion is symmetric — so the sets effectively sample a hemisphere.)

    - **What gets displayed — the derived maps.** From the three axis lengths λ₁, λ₂, λ₃, everything clinical is computed:

    - **MD (mean diffusivity)** — the average of the three axis lengths: the diffusivity the voxel would have if its ellipsoid were a sphere.
      MD = (λ₁+λ₂+λ₃)/3

    - **FA (fractional anisotropy)** — how elongated the ellipsoid is, 0→1 (0 = sphere, gray matter/CSF; ~0.8+ = highly elongated, corpus callosum). A **shape score, not a speed** — FA is scale-invariant: ellipsoids with axes (2,1,1) and (1,0.5,0.5) have the same FA but different axial diffusivity; a fast sphere (2,1.8,1.8) has high axial diffusivity but low FA.
      FA = √(3/2) · √[ (λ₁−MD)² + (λ₂−MD)² + (λ₃−MD)² ] ÷ √( λ₁² + λ₂² + λ₃² )

    - **Color FA (color-coded fractional anisotropy)** — the principal axis's direction encoded as color: red = left–right, green = anterior–posterior, blue = superior–inferior, brightness = FA.
      color = the direction of the λ₁ eigenvector

    - **Axial / radial diffusivity** — the pathology fingerprint: **axonal injury** lowers λ₁ (the top speed drops); **demyelination** raises λ₂, λ₃ (water leaks across the fiber), the contrast shrinks, and **FA drops even while λ₁ is untouched**. FA falls in both diseases; axial vs radial tells you which happened.
      axial = λ₁      radial = (λ₂+λ₃)/2

    - **Tractography** — follow the λ₁ eigenvector: start at a seed voxel, step to the neighbor along its fiber direction, repeat. The chain of steps is a streamline, and bundles of streamlines are the tracts you see.

    - **SMS matters here.** 20+ directions × whole brain × averages is long. Simultaneous multi-slice (SMS/multiband, factor 2) excites and reads several slices per shot, cutting the volume time roughly in half — the vault's 20-direction DTI is exactly this.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Directions | 20 (vault), 6 minimum, 30–64 for tractography | Angular accuracy vs time (above) |
| b-value | ~1000 for FA/tractography | Higher b = sharper directionality, lower SNR |
| SMS factor | 2 | Time ÷~2 for the whole volume |
| Voxel | isotropic 2–2.5 mm | Tensor fitting needs matching resolution in all axes |
| Tensor output | FA, color FA, MD/ADC, tractography | What the scanner/via reconstructs inline |

**Artifacts & pitfalls —** Motion is the enemy (each direction is one shot — reacquire or use prospective motion correction); eddy-current and distortion vary per direction (correction mandatory before FA — otherwise FA is inflated at tissue borders); crossing fibers make single-tensor FA unreliable (two bundles at 90° look isotropic); partial voluming with CSF shrinks FA near the ventricles. SNR per direction falls as direction count rises — do not starve it.

**Used in this vault —** Whole-brain 20-direction DTI with SMS, acquired in the presurgical functional protocols *together with* the BOLD paradigm battery — BOLD maps the eloquent cortex, DTI maps the tracts; a surgeon must avoid both (BOLD is entry 7).

---

## 4. DSC Perfusion — Dynamic Susceptibility Contrast

**What it is —** A rapid T2\*-weighted EPI series (one volume every ~1.5–2 s, ~50–60 time points) tracking a **gadolinium bolus** as it passes through the brain — including the paired pre-/post-Diamox runs used for cerebrovascular reserve testing.

**Contrast & good for —** Hemodynamic maps: **rCBV** (tumor grading, especially GBM), rCBF, MTT, TTP — and, with the Diamox challenge, *cerebrovascular reserve* (whether collaterals can compensate a stenosed/occluded artery — the brain's "stress test").

- **Physics deep-dive — from the signal dip to the four maps.**

    - **The maps, up front.** Everything below derives four numbers per voxel: **CBV** — the fraction of the voxel that is blood (ml blood / 100 g tissue); **CBF** — cerebral blood flow, how fast blood passes through (ml blood / 100 g / min); **MTT** — mean transit time, how long tracer stays (seconds); **TTP** — time to peak, read straight off C(t), no derivation needed. The derivation meets CBV first — the dip's area alone yields it — and CBF last, via deconvolution.

    - **Notation, before anything else.** The scan takes ~60 frames, one every 1.5–2 s. The letter **t** always means "at frame t" — the time during the bolus passage, in frames or seconds. A notation like S(t) reads: "S, evaluated at frame t" — one number per frame.

    - **The raw signal: the bolus shortens T2\*.** Gadolinium is paramagnetic; during its first pass through the capillaries it perturbs the local field and shortens T2\* of the surrounding tissue. So the signal dips. Frame by frame:

      ```
      S(t)  =  S₀ · e^(−TE / T2*(t))

      S(t)    = the voxel's signal at frame t (measured)
      S₀      = the signal before any decay (a constant of the voxel)
      TE      = the echo time — fixed for the whole series (a scanner setting)
      T2*(t)  = the voxel's fading time at frame t — shortened by the contrast
      ```

      TE never changes; the dip happens entirely because T2\*(t) shortens while the bolus is present.

    - **Step 1 — switch to the fading *rate*.** T2\* is a time (milliseconds). Its reciprocal is a speed — how many e-folds of decay per second:

      ```
      R2*(t)  =  1 / T2*(t)
      ("the rate" — big when the fade is fast)
      ```

      Rates are the natural language here because **two decay processes stack by adding their speeds**. The contrast adds an extra dephasing mechanism on top of the tissue's own, so:

      ```
      R2*(t)  =  R2*_baseline  +  ΔR2*(t)

      R2*_baseline = the tissue's own fading speed (measured before the bolus)
      ΔR2*(t)  = the EXTRA fading speed added by the contrast at frame t
                     (zero before the bolus, largest at the dip's bottom, zero after)
      ```

      Now put this sum back into the signal equation and split the exponential (e^(a+b) = e^a · e^b):

      ```
      S(t)  =  S₀ · e^(−TE · (R2*_baseline + ΔR2*(t)))
            =  S₀ · e^(−TE · R2*_baseline) · e^(−TE · ΔR2*(t))
      (the first two factors are S_baseline — below)
      ```

      Before the bolus, ΔR2\*(t) = 0, so the pre-bolus signal is exactly those first two factors: **S_baseline = S₀ · e^(−TE · R2*_baseline)** — the tissue's own fading speed and S₀, already combined, measured in the first frames. So at any frame:

      ```
      S(t)  =  S_baseline · e^(−TE · ΔR2*(t))
      ```

      Step 2 stands on this: one division by S_baseline cancels S₀ and R2\*_baseline together — the baseline rate never needs to be known on its own.

    - **Step 2 — invert the signal equation to isolate ΔR2\*.** The signal equation contains ΔR2\* hidden inside the exponential. Pull it out in three moves:

      ```
      S(t) / S_baseline  =  e^(−TE · ΔR2*(t))
      ①  divide by the baseline signal
      ln( S(t)/S_baseline )  =  −TE · ΔR2*(t)
      ②  take the natural log
      ΔR2*(t)  =  −(1/TE) · ln( S(t) / S_baseline )
      ③  multiply by −1/TE
      ```

      (ln = natural logarithm, the inverse of the exponential.)

    - **Step 3 — the physics claim: ΔR2\* is the concentration.** For clinical doses, the extra rate the contrast adds is (approximately) proportional to how much contrast is present:

      ```
      ΔR2*(t)  ≈  k · C(t)

      C(t) = the contrast concentration in the voxel at frame t — per
             unit of whatever the voxel is made of: blood in an artery
             voxel, tissue in a brain voxel (the same conversion, two
             different samples — why A and C will carry different units)
      k    = an unknown constant, common to every voxel
      ```

      So the conversion is complete: **the measured signal, frame by frame, becomes the concentration-time curve C(t)** — up to one common constant k. Every map below is built from this curve.

    - **Step 4 — CBV from the area of the curve.** CBV = the fraction of the voxel that is blood. Contrast lives only in the blood, never in the cells, so at every single frame:

      ```
      C(t)  =  CBV  ×  C_blood(t)
      (mmol/100g tissue)   (ml blood/100g)   (mmol/ml blood)

      C_blood(t) = the concentration inside the blood arriving at the voxel
      ```

      Now sum both sides over the whole passage (∫ means "the sum over all frames" — the area under the curve):

      ```
      ∫ C(t) dt       =  CBV  ×  ∫ C_blood(t) dt
      (voxel's area)      (blood's area — the injected dose,
                           identical for every voxel)
      ```

      The blood's area is one common number (the syringe fixed it). Therefore:

      ```
      CBV  ∝  ∫ C(t) dt           ∝  ∫ ΔR2*(t) dt
      ```

      The voxel's blood volume is proportional to **the area of its first-pass dip** — a voxel with twice the blood holds twice the tracer at every instant, so its area is twice as large.

    - **Practical rules for the area.** Integrate the **first pass only** — the bolus recirculates, and the second bump must not be counted as extra blood volume. A gamma-variate fit (a curve shaped like a first-pass bolus) both excludes the recirculation and completes truncated tails in slow territories. And the acquisition must be long enough (~60–90 s) that even the slowest voxel has finished its passage.

    - **Step 5 — normalize: where the "r" comes from.** Two unknown constants remain — k (Step 3) and the blood-area constant (Step 4). Both are common to every voxel. Divide a voxel's value by a reference region's:

      ```
      rCBV  =  CBV_voxel / CBV_reference
      (both constants cancel; normal white matter = 1)
      ```

      Note: **rCBV needs no arterial measurement at all** — the area method never uses an artery.

    - **Step 6 — why flow needs more than the area.** Two voxels can have identical area (identical CBV) yet different physiology: one delivers its blood fast and briefly, the other slowly and lingeringly. The area is blind to timing — flow lives in the *shape* of the curve: **is the blood that is there actually moving?** The tool for shape is the **survival curve Res(t)**:

      ```
      Res(t)  =  the fraction of an instantaneous tracer pulse
                 still inside the voxel, t frames after it arrived

      Res(0) = 1
      (at arrival, the whole pulse is present)
      Res(∞) = 0
      (eventually all washed out)

      fast washout: Res drops quickly (rapid turnover)
      slow washout: Res lingers       (slow turnover)
      ```

      Res is a fixed curve per voxel — its transit fingerprint. The area under Res is the mean time a tracer molecule stays: **MTT = Σ Res(t)** — the counting reason is in Step 9.

    - **Step 7 — the convolution: the measured curve is the bolus echoed through R′.** Two curves are measured, both by the same signal→ΔR2\* conversion. **A(t)** — the arterial input function (AIF), the bolus at a large artery: mmol per ml of blood — the dose arriving at the brain's door, frame by frame. **C(t)** — that voxel's response: mmol per 100 g of tissue — delayed, lower, and smeared, because the tissue holds tracer for a while and releases it gradually. The units differ though the mechanism is the same: the conversion reports per unit of whatever the voxel is made of — blood in the artery voxel, tissue in the tissue voxel. These are the only two curves measured; everything from here on is derived from them. The missing piece between them is the voxel's own **response curve R′(t): the curve this voxel would produce for a perfect one-instant pulse of size one in the artery — its response per unit of arterial input, in flow units: ml blood / 100 g / min**. Each arrival is a mini-pulse, each echoed through the same response curve, and the voxel's curve is their sum:

      ```
      C(t)  =  A(0)·R′(t) + A(1)·R′(t−1) + A(2)·R′(t−2) + …
      (mmol/100g)      (mmol/ml) × (ml/100g/min)

      A(τ)      = how much arrived at frame τ
                  (index advances: later arrivals)
      R′(t−τ)   = how much of that arrival is still present now
                  (argument recedes: older arrivals have decayed further)
      ```

    - **Step 8 — the deconvolution: strip the injection away, solve for R′.** The software now asks what the tissue is like *on its own*: deconvolution removes the injection's fingerprint and solves for the response curve from Step 7. But what is R′ made of? Its height is the delivery rate — **CBF, cerebral blood flow: how fast blood passes through the voxel (ml blood / 100 g / min)**; its shape is the washout — **Res**, the survival curve from Step 6:

      ```
      R′(t)  =  CBF · Res(t)
                 │      │
                 │      └─ the shape: which FRACTION of the pulse is still inside
                 └─ the scale: how much the tap delivered in that first instant
      ```

      In the bucket picture: put one unit of dye in the tap's water at frame 0 — the table of amounts in the bucket afterwards is R′; the tap rate delivers CBF units in the first instant, so the amounts start at CBF in flow units, not 1. Everything about this voxel's perfusion lives in R′; nothing about how you injected does.

      CBF is one number — a rate; Res is a whole curve — a shape. As a pair they are ambiguous (doubling CBF and halving Res changes nothing), so pack them into one combined unknown — with it, the model becomes pure linear equations:

      ```
      C(0) = A(0)·R′(0)
      C(1) = A(0)·R′(1) + A(1)·R′(0)
      C(2) = A(0)·R′(2) + A(1)·R′(1) + A(2)·R′(0)
        ⋮
      ```

      Each frame's equation has exactly one new unknown — solve frame by frame (forward substitution). In practice the division by the near-zero A(0) would amplify noise, so the same system is solved stably by **SVD** (singular value decomposition): it keeps only the well-transmitted "channels" of the system and discards the noise-dominated ones.

    - **Step 9 — unpack R′: the three readings, then the two roles.** Everything from Step 8 is one curve, R′ — the echo of a unit instant pulse — and everything to report is a reading of it. The three readings — height, shape, area — are deduced from it in order.

      **The height is flow.** The splitting is the convention Res(0) = 1 — at the arrival instant nothing has left (Step 8's bucket), so the first value of R′ is pure CBF:

      ```
      R′(0)  =  CBF · Res(0)  =  CBF · 1
      CBF    =  R′(0)
      (a FLOW — ml blood / 100 g / min)
      ```

      **The shape, and its area, give the transit time.** With the height in hand, divide the curve by it to get the fraction curve — the shape:

      ```
      Res(t)  =  R′(t) / CBF
      ```

      Why the area of Res is the mean transit time — a counting argument. Res(t) = the fraction of the pulse still inside at frame t: a molecule that stays n frames contributes a "1" to Res at each of frames 0 … n−1 — counted exactly once per frame of its stay, and not at all afterwards. Summing Res over all frames therefore counts every molecule once per frame of its stay, whatever the mix of short-staying and long-staying molecules; divided by the number of molecules, that total is the average stay:

      ```
      Σ Res(t)  =  (total frames stayed by all molecules) / (number of molecules)
                =  average stay
                =  MTT
      (a TIME)
      ```

      **The area of the echo gives the volume** — the reunion of the two readings above:

      ```
      CBV  =  CBF × MTT
      (a VOLUME — ml blood / 100 g tissue: height × width)
      ```

      The CBV reading therefore exists twice, and the two routes must agree — the central volume theorem, a built-in self-check of the whole pipeline. **Route 1 (Step 4):** the area of the measured first-pass dip, CBV ∝ ∫ C(t) dt, normalized to a reference region → rCBV — no deconvolution, no artery; this is how rCBV is usually produced clinically, with a γ-variate fit cutting the recirculation. **Route 2 (here):** the area of the echo, Σ R′(t) = CBF × MTT — the height times the width, the byproduct of computing flow.

      **The steepness is not flow but turnover.** The natural intuition is that fast CBF means fast washout — true only inside one fixed pool. The echo has two independent knobs: the tap (CBF) and the bucket (CBV), and the drop rate turns both — the turnover, how many times the pool exchanges per minute:

      ```
      how fast the echo drops  =  CBF / CBV  =  1 / MTT
      (exchanges per minute)
      ```

      A big drum with a fast tap (high CBV, high CBF — an AVM is close) echoes **tall** and decays **slowly**; a small cup with the same tap echoes just as tall but empties fast. Same height, different steepness: the tallness is the tap, the steepness is the pool-vs-tap ratio — so "fast CBF" means "fast washout" only when CBV happens to be the same.

      Normalize CBF to a reference region → **rCBF**; the unknown k cancels, exactly as for rCBV. So the maps read, by height, shape, area: a well-perfused voxel echoes a **tall** curve (high CBF); a starved one — stroke core, misery perfusion — a **short** one. Fast washout = steep and brief; lingering blood — stenosis downstream, slow collaterals — is flat and wide, a long **MTT**. And the echo's **area** is CBV — the map read for tumor grading: angiogenesis packs more blood into every voxel, high rCBV.

    - **Where the AIF comes from in practice.** Step 7's A(t) is measured at a large artery in the image (typically the middle cerebral artery) by the same signal→ΔR2\* conversion — auto-detected by the post-processing software, or selected with one ROI click. It is not a manual anatomical calibration: the software supplies the input curve itself, and it is used only where the deconvolution needs it — rCBF and MTT (rCBV never uses an artery, Step 5). (Using one AIF for the whole brain is an approximation — the bolus arrives later in some territories; delay-insensitive variants exist.)

    - **T1 leakage — the corruption, and why preload is often skipped.** In tumors, contrast leaks out of the vessels after the first pass; the resulting T1-shortening brightening partially cancels the dip → underestimated rCBV. Cures: a small **preload dose** (¼–⅓ of the dose, before the dynamic run, saturates the interstitium so the measured bolus can't leak further), or post-processing **leakage correction** that models the contamination from the post-bolus tail. Practice often skips preload because the correction recovers most of the error, the routine question tolerates the rest, and dose economy favors skipping.

    - **Motion** corrupts every frame of the curves — all dynamics must be aligned before any map is computed; severe motion kills the curves.

    - The Diamox variant: acetazolamide (Diamox) dilates the resistance vessels of *healthy* brain. Regions whose vessels are already maximally dilated (chronic misery perfusion) cannot dilate further → blunted flow response → the post-challenge rCBV/CBF fails to rise where the pre-challenge looked normal. The paired pre/post protocol quantifies exactly this reserve.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Temporal resolution | TR ~1.5–2 s (whole brain) | Gray-matter MTT ≈ 4 s (CBV ÷ CBF); this frame rate samples each passage ~3× — enough to trace the shape whose area is MTT. Slower smears the dip; faster costs SNR and slices |
| Duration / frames | ~50–60 dynamics | Must cover pre-contrast baseline + full first pass + recirculation tail. Shorter starves the baseline (S_baseline, the division's reference) and truncates the tail — the γ-variate fit (a first-pass fit for the CBV *area*, not for CBF) and the leakage correction both suffer |
| TE | ~30–35 ms @3T (~45 ms @1.5T) | The dip's depth per unit ΔR2\* scales with TE; longer deepens the dip at SNR cost, shorter loses susceptibility sensitivity |
| Bolus injection | ~4–5 ml/s | A tight bolus sharpens A(t); a sluggish one leaves its frames nearly indistinguishable — the deconvolution matrix becomes ill-conditioned and the SVD can't resolve R′'s sharp features |
| Dose scheme | preload + dynamic dose (or leakage correction) | Preload saturates the interstitium so the measured bolus can't leak; the correction subtracts the leak afterwards — either way tumor rCBV survives |
| Readout | GRE-EPI standard | SE-EPI's 180° refocuses the static field offsets around large vessels — only diffusion-scale capillary dephasing survives → capillary weighting, at SNR cost |

**Artifacts & pitfalls —** T1 leakage underestimates rCBV wherever the barrier leaks (preload or correction, above); susceptibility dropout at the skull base makes maps there unreliable; motion misaligns the per-voxel curves — rigid correction first, severe motion kills them; the AIF's scale is uncertain (the MCA is thinner than any voxel) but auto-detection and the relative maps cancel it — an issue only if absolute CBF itself is reported; a single AIF assumes the bolus arrives everywhere at once — in low-flow territories the late arrival is folded into the response and stretches MTT (delay-insensitive deconvolution corrects it).

**Used in this vault —** GBM rCBV assessment and the paired Diamox cerebrovascular-reserve challenge; the same T2\*-bolus physics underlies first-pass perfusion of other organs where implemented.

---

## 5. BOLD fMRI — Blood Oxygenation Level Dependent Imaging

**What it is —** A T2\*-weighted EPI time series (one volume every 2–3 s) repeated through a task/rest paradigm, detecting the tiny signal change (~1–5%) caused by *local oxygen consumption vs supply* during brain activation. Tokens: `ep2d_pace_moco_*` with paradigm variants (motor, language, visual, auditory); plus the field-mapping series used to unwarp the EPI.

**Contrast & good for —** Functional localization: pre-surgical mapping of eloquent cortex (motor, language), and — more recently — resting-state networks. The "contrast" is the BOLD effect, a surrogate of neural activity via blood flow.

- **Physics deep-dive — the hemodynamic response.**

    - **Why blood-oxygen changes signal.** Deoxyhemoglobin is paramagnetic (it disturbs the local field → T2\* loss); oxyhemoglobin is not. Neural activity triggers a *local blood-flow increase that overshoots oxygen demand* — so active cortex is flushed with *more oxygenated* blood → less deoxyhemoglobin → less T2\* dephasing → **slightly higher signal** (the positive BOLD response). The response lags activity by ~4–6 s (the hemodynamic response function) and lasts ~10–15 s — which dictates the slow, block-design timing of clinical paradigms: ~20–30 s task blocks alternating with rest. The measurement math is entry 4's (DSC) exactly — a paramagnetic blood agent shifting R2\* inside the same T2\*-weighted EPI signal equation — only the agent here is endogenous deoxyhemoglobin and the effect is a 1–5% *rise* instead of a deep dip.

    - **Why TE ≈ 30 ms at 3T.** The BOLD effect is a *change in T2\* decay*: ΔS/S ∝ TE · ΔR2\*. Longer TE amplifies the effect — but signal itself decays as e^(−TE/T2\*), so beyond tissue T2\* (~50–60 ms at 3T) you are amplifying noise. The optimum sits near tissue T2\*: **TE ~30–35 ms at 3T** (~40 ms at 1.5T).

- **Physics deep-dive — the design against motion.**

    - **Why the whole design fights motion.** A 1–5% effect measured over minutes is hostage to the head staying put: on a fixed voxel grid, any motion makes a voxel's time series sample different tissue — at gray/white and CSF edges that intensity jump dwarfs the BOLD effect — and motion that occurs *with* the task mimics activation outright. Two layers of defense, one principle: estimate the head's rigid motion as 6 parameters (3 translations, 3 rotations) against a reference and undo it with the inverse transform — the layers differ only in *when*:

        - **Retrospective — realignment.** After the scan: the 6 parameters are estimated from the acquired volumes themselves, and each volume is resampled to undo them — but this cannot repair **spin-history errors**: if the head moves between the slices of a volume, the magnetization is no longer where the slice prescription expects, and the errors are baked into the raw data.

        - **Prospective — PACE** (the vault's `pace` token). Before each volume: three separate low-flip-angle navigator echoes circle the k-space center, one in each orthogonal plane. Motion shifts their phase — translation modulates the phase along the circle, rotation shifts the data pattern around it — yielding the 6 parameters in milliseconds. The inverse transform is then applied *in advance*: the scanner adjusts the slice prescription for the next volume, so the slices follow the head and the same tissue is excited every time.

      Practice stacks all of it: PACE during acquisition, realignment afterwards, and the motion parameters as nuisance regressors in the statistical model.

- **Physics deep-dive — the field map: measure ΔB₀, then undo the shift.**

    - **Two echoes, one subtraction.** BOLD's product is an anatomical claim — *this cortex activates* — and distorted EPI would place the activation on the wrong anatomy; the field map identifies the inhomogeneity (Δf per voxel) so the unwarp can put every voxel back where it belongs. A quick dual-echo GRE (`gre_field_mapping`, acquired before the BOLD series) does the measuring: a spin in an off-resonance field accumulates phase as time passes — φ = γ·ΔB₀·TE, the field × echo time — so an echo's phase *contains* the field, polluted by an unknown starting phase φ₀. One echo can't separate the two; two can: same voxel, same φ₀, different TE, so the difference cancels the common unknown and leaves the field:

      ```
      φ1 = φ₀ + γ·ΔB₀·TE1      φ2 = φ₀ + γ·ΔB₀·TE2
      φ2 − φ1  =  γ · ΔB₀ · (TE2 − TE1)
      ΔB₀  =  (φ2 − φ1) / (γ · ΔTE)
      ```

      ΔTE is known, γ is a constant — the voxel's off-resonance is read off directly, reported as Δf in Hz (measure twice, subtract the common unknown — the same move as the DSC baseline division).

    - **ΔTE is chosen so fat and water stay in phase.** Fat and water precess at different speeds (~220 Hz apart @1.5T / ~440 Hz @3T); caught out of phase at the second echo, they partly cancel and leak a fake field into the subtraction. ΔTE is picked one full precession cycle apart (~2.3 ms @3T, ~4.6 ms @1.5T) — both species land in phase at both echoes and the subtraction cannot see them. Unlike DWI, which *suppresses* fat, the field map keeps it but times it into invisibility.

    - **Phase wraps — unwrapping repairs it.** Phase only exists modulo 2π: where the field error is large (skull base), the true phase difference spans several turns and the machine reads only the remainder — the map aliases into ±π bands. Unwrapping walks the map and adds whole turns back, reconstructing the continuous field; it fails where the field changes too fast between neighbors, and voxels with no signal (air) are masked out.

    - **The unwarp is the shift formula inverted.** Entry 1: each EPI pixel was displaced by Δf × echo spacing × EPI factor. With Δf known per voxel, the reconstruction shifts every pixel *back by its own amount* — stretched regions recompress, compressed regions re-expand, and the functional volumes match true anatomy. The map is static, so the patient must not move between the map and the EPI series it corrects.

    - **What the map fixes — and what it cannot.** The map owns *geometric* distortion; physiological noise — cardiac/respiratory pulsation aliasing into the signal — is tolerated, not cured (cardiac gating exists but is rarely used clinically).

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| TE | ~30 ms (3T) | The BOLD-vs-noise optimum (above) |
| TR / volume time | 2–3 s | Two hats: **frame rate** — longer TR = slower frame rate; **recovery interval** — shorter leaves less recovery between excitations, so motion scrambles each voxel's excitation history (intensity artifact on top of misregistration). Longer: slower frames, fuller recovery. Shorter: faster frames, worse artifact |
| Paradigm | block design (task/rest alternation) | Blocks ~20–30 s let the lagged response plateau; repetitions build statistical power — and the task chosen decides which cortex appears |
| Motion correction | PACE prospective on | Real-time slice repositioning |
| Field map | `gre_field_mapping` before EPI | Distortion unwarping |
| SMS factor | 2–4 (research) | Several slices excited at once, separated by coil sensitivity — whole-brain coverage per second; the price is SNR and slice-leakage artifacts |

**Artifacts & pitfalls —** Head motion is the #1 killer (even 1–2 mm corrupts the statistics; check motion parameters); susceptibility dropout at the orbitofrontal/temporal poles (signal simply absent there); physiological noise; paradigm timing errors; the BOLD signal is *not* quantitative activity — it is a flow proxy, and diseased vasculature (steal, severe stenosis) can invert or blunt it.

**Used in this vault —** Pre-surgical mapping battery: motor (hand/foot), language (picture naming, synonyms), visual and auditory paradigms with PACE motion correction and field-map unwarping; block-design timing throughout.

---

## 6. EPI T2\* — the rapid hemorrhage screen

**What it is —** A short T2\*-weighted GRE-EPI run (fast, few slices or low resolution) whose purpose is *bleeding detection*, not quantification. Token: `ep2d_tra_hemo`.

**Contrast & good for —** Acute hemorrhage and its breakdown products: deoxyhemoglobin/hemosiderin/ferritin all shorten T2\* → dark signal ("blooming"). Used as a fast screen in the acute/fast brain protocols where a full SWI would cost time.

- **Physics deep-dive — the same darkness as SWI, minus everything SWI adds on top.**

    - **The shared mechanism: susceptibility darkening.** Blood products — deoxyhemoglobin when acute, hemosiderin/ferritin once broken down — are paramagnetic: each deposit perturbs the local field, spins nearby dephase faster, T2\* shortens, and the signal drops around (and beyond) the lesion — the "blooming" that can look larger than the bleed itself. It is the identical mechanism the DSC bolus and BOLD deoxyhemoglobin use — here the agent is the pathology, and the readout is entry 1's GRE-EPI at a longish TE.

    - **What SWI does beyond the magnitude darkness.** SWI (file 03) is a high-resolution 3D GRE that reads two more channels the hemo-screen cannot:

        - **The phase channel.** The same susceptibility field also shifts the local phase — SWI multiplies the magnitude image by a phase mask, amplifying the contrast of paramagnetic deposits beyond what T2\* darkness alone gives.

        - **The resolution — the in-plane battle.** A voxel averages everything inside it: a microbleed fills only a sliver of EPI's coarse voxel and its darkness is diluted into invisibility; SWI's ~1 mm voxels let it fill a whole voxel, which reads genuinely dark.

        - **The display — the through-plane battle.** The minimum-intensity projection keeps, per pixel, the darkest value along the slab — the microbleed's darkness, spread across a few thin slices, surfaces into one view (the inverse of the vessel MIP).

    - **What the hemo-screen gives up, and why.** EPI's phase is dominated by off-resonance and eddy-current errors — it carries no usable susceptibility phase, so phase masking is impossible. Its voxels are coarse (speed is the point), so partial volume dilutes small lesions into invisibility. And its dropout zones — the skull base, entry 1 — are exactly where some bleeds hide. All three gaps point the same way: **the screen sees gross bleeding, not microbleeds.**

    - **What it keeps: speed and robustness.** A few seconds, tolerant of the acute patient's motion — enough to answer the one question it asks: *is there a gross bleed?* A positive screen is a bleed; a negative screen is not the absence of microbleeds — that question belongs to SWI.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| TE | long enough for T2\* sensitivity | Short TE erases the point |
| Resolution/time | low-res & fast by design | Speed is the point |

**Artifacts & pitfalls —** Same EPI distortion/dropout (entry 1).

**Used in this vault —** The fast/acute brain screen.

---

## Family summary

| Sequence | Contrast engine | Readout | Standout trade |
|---|---|---|---|
| EPI readout | T2\* (whatever prep adds) | single-shot or segmented | speed ↔ distortion |
| DWI/ADC | Stejskal–Tanner gradients | ss-EPI / RESOLVE / non-EPI | distortion ↔ time (RESOLVE), SAR (non-EPI) |
| DTI | diffusion tensor (≥6 dirs) | EPI + SMS | direction count ↔ time |
| DSC perfusion | T2\* bolus tracking | GRE-EPI, ~2 s frames | T1-leakage corruption ↔ preload |
| BOLD fMRI | T2\* (hemodynamic) | EPI, ~2–3 s TR | 1–5% effect ↔ motion |
| EPI T2\* screen | T2\* (blood products) | fast GRE-EPI | speed ↔ sensitivity |

---

**Key sources** — Siemens Healthineers (syngo RESOLVE, SMS-DWI protocols, syngo DTI); mriquestions.com: [how to perform DSC](https://s.mriquestions.com/how-to-perform-dsc.html), [BOLD pulse sequences](https://www.s.mriquestions.com/bold-pulse-sequences.html), [EPI distortion/echo spacing](https://support.brainvoyager.net/brainvoyager/functional-analysis-preparation/29-pre-processing/78-epi-distortion-correction-echo-spacing-and-bandwidth); PACE white paper (Siemens); papers: Griswold GRAPPA (MRM 2002); Radiopaedia (DWI, DTI, DSC).

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-13 | — | Initial — EPI/DWI/DTI/perfusion/fMRI entries |
