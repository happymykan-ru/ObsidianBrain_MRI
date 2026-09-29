# Physics Foundations

**Version:** 1.0 | **Date:** 2026-09-08

> The physics primer for everything else in this knowledge base. Read this first if the other files assume too much. Equations are the few that matter in daily protocol work; each is tied to a decision you actually make on the console.

---

## 1. Spin, magnetic moment, and the Larmor equation

Atomic nuclei with an odd number of protons and/or neutrons possess **spin** — an intrinsic angular momentum that gives the nucleus a tiny magnetic moment. In clinical MRI the signal comes almost entirely from **¹H protons** (water and fat, ~10⁸ per mm³ of tissue).

Place the spin in the main magnetic field **B₀** and it precesses around B₀ at the **Larmor frequency**:

```
ω₀ = γ · B₀

γ (gyromagnetic ratio of ¹H) = 42.58 MHz/T

@1.5T → ω₀ ≈ 63.9 MHz     @3T → ω₀ ≈ 127.7 MHz
```

**Why it matters on the console:** every RF pulse frequency is tuned to this. Larmor frequency scales with field strength — which is why the same tissue shows the same *ppm* chemical shift but double the *Hz* separation at 3T (see §7 and Dixon in file 03).

A tiny population excess aligns along B₀ (Boltzmann distribution) → net **longitudinal magnetization M_z**. This equilibrium magnetization scales roughly with B₀² — the fundamental SNR advantage of 3T:

```
SNR ∝ B₀        (per unit time, all else equal: 3T ≈ 2× the SNR of 1.5T)
```

## 2. Excitation — RF as B₁

A resonant RF pulse (at ω₀) tips M_z toward the transverse plane. The **flip angle α** is set by the pulse amplitude × duration:

```
α = γ · B₁ · t_pulse
```

- α = 90° → maximum transverse magnetization (all of M₀ rotated into the xy-plane) — basis of spin echo
- α < 90° (e.g. 10–30° in gradient echo) → only part of M₀ is used each TR, but M_z recovers fast → short TR becomes possible → **low-flip-angle T1-weighted imaging** (Ernst angle, §5)
- Nothing is "used up" — excitation redistributes magnetization, and T1 relaxation returns it to equilibrium

## 3. Relaxation — T1, T2, T2*

After excitation the spins return to equilibrium along two independent clocks.

### T1 (spin–lattice relaxation) — recovery of M_z
Energy is given back to the molecular lattice. Longitudinal magnetization recovers exponentially:

```
M_z(t) = M₀ · (1 − e^(−t/T1))
```

T1 is always ≥ T2, and **T1 lengthens with field strength** (e.g. white matter ~600 ms @1.5T → ~830 ms @3T; myocardium ~950 @1.5T → ~1200 @3T). Consequences you adjust for at 3T: longer TR to keep T1 weighting, longer TI for nulling, smaller flip angles.

### T2 (spin–spin relaxation) — decay of M_xy
Local field fluctuations dephase the spins; transverse magnetization decays:

```
M_xy(t) = M₀ · e^(−t/T2)
```

T2 is tissue-intrinsic (edema and fluid long, iron/protein short). T2 does **not** change much with field strength.

### T2* — the observed decay
Static field inhomogeneities (main-field imperfections, susceptibility differences at tissue interfaces, iron, blood products) add a reversible dephasing term:

```
1/T2* = 1/T2 + γ·ΔB_inhom

ΔB terms scale with B₀  →  T2* shortens at 3T
```

The reversible part (γ·ΔB) is what a **180° refocusing pulse** or a **gradient rephasing lobe** can recover — this is the entire difference between spin echo and gradient echo (next section). Long-T2* effects (iron, deoxyhemoglobin, hemosiderin) underpin T2* imaging, SWI, BOLD fMRI, and DSC perfusion.

## 4. Echo formation — RF echo vs gradient echo

An echo is a coherent re-growth of transverse signal after intentional dephasing. Two ways to make one:

### (a) RF (spin) echo — 90° then 180°
- 90° tips M into the transverse plane; spins dephase with spread Δφ over time TE/2 (due to both T2* processes *and* static inhomogeneity)
- A 180° pulse **flips the phase of every spin** (φ → −φ)
- After another TE/2, static dephasing has unwound: the inhomogeneity term is refocused, and only true T2 decay remains

```
Result: signal at echo time TE ∝ e^(−TE/T2)      (not T2*)
```

### (b) Gradient echo — rephase with gradients only
- A negative gradient lobe dephases spins; the opposite-polarity lobe rephases them
- Gradient reversal refocuses **only the gradient-induced dephasing** — static B₀ inhomogeneity keeps accumulating

```
Result: signal ∝ e^(−TE/T2*)       (T2* contrast)
```

### Gradient-moment analysis (the physics language of flow/motion)
The phase a spin accumulates in a gradient G(t) depends on its position x(t):

```
φ = γ ∫ G(t)·x(t) dt

For a spin at constant velocity v:  x(t) = x₀ + v·t
φ = γ·[ x₀·∫G dt  +  v·∫G·t dt ]  = γ·( M₀·x₀ + M₁·v )

M₀ = ∫G dt    (zeroth moment — position encoding)
M₁ = ∫G·t dt  (first moment — velocity encoding)
```

- A **bipolar gradient pair** (e.g. −G then +G) has M₀ = 0 but M₁ ≠ 0 → static spins rephase, moving spins accumulate phase ∝ velocity → **this is phase-contrast velocity encoding** (file 05)
- A gradient waveform with M₀ = M₁ = 0 at the echo (flow compensation / **GMR** — gradient-moment rephasing) rephases both stationary and constant-velocity spins → flow artifacts removed at the cost of longer minimum TE

**Console translation:** slice-select, phase-encode and readout gradients are all designed around which moments they null — see §8.

## 5. The signal equations that decide contrast

### Spin echo (90°–180°), one TR later

```
S_SE = k · PD · (1 − e^(−TR/T1)) · e^(−TE/T2)
```

Three levers → three weightings:

| Want | TR | TE | Result |
|---|---|---|---|
| T1-weighted | **short** (~TR < T1) → tissues differ in how much M_z recovered | short (minimize T2) | S ∝ PD·(1−e^(−TR/T1)) |
| T2-weighted | long (T1 differences gone) | **long** → tissues differ in T2 decay | S ∝ PD·e^(−TE/T2) |
| PD-weighted | long | short | S ≈ PD |

### Spoiled gradient echo (FLASH) — steady state
With α < 90° and spoiling (RF phase cycling + gradient spoilers kill transverse coherence between TRs — file 03):

```
S_FLASH = k · PD · sin(α) · (1 − e^(−TR/T1)) / (1 − cos(α)·e^(−TR/T1)) · e^(−TE/T2*)
```

**Ernst angle** — the flip angle maximizing signal for a given TR/T1:

```
α_Ernst = arccos(e^(−TR/T1))
```

Short TR + α ≈ Ernst → T1 weighting at a fraction of the SE time. This is the engine of FLASH/VIBE/MPRAGE and of 3D TOF MRA.

### Balanced SSFP (TrueFISP) — fully refocused steady state
If gradients are completely balanced each TR (M₀ = 0 on all axes), transverse coherence survives across TRs and the steady state becomes:

```
S_bSSFP ∝ (T2/T1 ratio)  — formally ∝ M₀·sin(α)/(1 + cos(α) + (T1/T2)·(1 − cos(α)))
```

Fluid and blood (long T2) appear bright regardless of flow — the basis of cine, MRCP-class contrast in TrueFISP, and NATIVE MRA.

### Inversion recovery — the nulling equation
A 180° inversion pulse then wait TI:

```
M_z(TI) = M₀·(1 − 2e^(−TI/T1))

Null when:   TI = T1·ln(2) ≈ 0.693·T1
```

| Target | Null TI @1.5T | @3T |
|---|---|---|
| CSF (FLAIR) | ~2000–2200 ms | ~2200–2500 ms |
| Fat (STIR/TIRM) | ~150–180 ms | ~200–220 ms |
| Myocardium post-Gd (LGE) | ~250–350 ms (10–15 min p.i., see file 06) | ~400–500 ms |

*Magnitude reconstruction (TIRM, FLAIR): both polarities of recovered signal appear bright; only the zero-crossing is dark.*

## 6. k-space — what the gradients actually do

The MR signal is the Fourier transform of the image. As gradients run, the signal traces a path through **k-space**:

```
k(t) = γ ∫ G(t') dt'        s(t) = ∫ ρ(x)·e^(−i2π k·x) dx

k-space center  →  low spatial frequencies  →  contrast / SNR of the image
k-space edges   →  high spatial frequencies →  resolution / sharpness
```

**Golden rules for protocol work:**

1. **What lands at k-space center decides the image contrast.** In a TSE echo train, the echo placed at center = the "effective TE". In CE-MRA, centric ordering puts the arterial phase at center.
2. **Motion corrupts most where it happens at center** (ghosting/ringing) — hence BLADE repeatedly sampling center (file 02) and radial spokes always crossing center (StarVIBE, file 03).
3. **You don't have to fill all of k-space:** partial Fourier uses conjugate symmetry (file 08); parallel imaging skips lines and reconstructs from coil sensitivity (file 08); compressed sensing undersamples incoherently and iterates (file 08).
4. **Trajectory shapes:** cartesian (every clinical sequence family base), radial (StarVIBE, GRASP), rotating blades (BLADE), single-shot zig-zag (EPI), spiral (research). Each trades motion robustness, off-resonance behavior, and reconstruction complexity.

Scan time in the cartesian case:

```
TA ≈ TR × N_phase × NEX / (turbo factor × parallel factor × CS factor × SMS factor)
```

## 7. Contrast weighting — the decision logic

1. Pick the **contrast** the question demands (anatomy T1, fluid/edema T2, lesion conspicuity + FS, diffusion, etc.)
2. Pick the **family** that can deliver it with acceptable time/artifact/SAR: TSE for T2, GRE for fast T1, IR for nulling, EPI for diffusion/perfusion/fMRI
3. Set **TR/TE/TI/α** per the equations above
4. Adjust for **field strength**: 3T lengthens T1 (so TR, TI and FA rescale), doubles chemical shift in Hz, shortens T2*, quadruples SAR (∝ B₀²), roughly doubles SNR
5. Then trade against time/SNR/resolution — see the trade triangle in [[08_options_and_parameters]]

Chemical shift reminder: fat is ~3.5 ppm downfield from water → at 1.5T ≈ 220 Hz, at 3T ≈ 440 Hz. This sets in/opposed-phase TEs (2.38/4.76 ms @1.5T; 1.15–1.23/2.3–2.46 ms @3T), Dixon echo pairs, and fat-sat pulse bandwidths.

## 8. Slice selection — the gradient + RF trio

Every 2D sequence localizes a slice with the **slice-select gradient** during RF, then encodes within the slice with phase- and frequency-encoding gradients:

```
Timing diagram (2D spin echo, one TR):

RF     90° |          180° |
        ▄▄▄▀             ▀▀▀▄▄▄        (2D slice-select pulses)
G_slice    ▔▔▔\__
(select)        rephase __/▔▔▔  ...  ▔▔▔▔▔\__
            [slice select]     (180° also slice-selective)  (refocus: often weaker/''spoiler'')

G_phase    ________________   |   |_  step 1..N_phase: one phase-encode blip per TR,
                                       amplitude encodes y-position (k_y)

G_read  _______________________________|  _
(freq)  [dephase lobe]                    ▔▔▔▔▔▔▔▔ readout during echo → k_x
                                          ADC window centered on TE

Signal   ··························  ✦ echo
```

- **Slice thickness** = RF bandwidth ÷ gradient strength — stronger G_slice (thinner slice) needs wider RF bandwidth or longer pulse
- After slice selection the spins are dephased across the slice; a small **rephase lobe** (opposite polarity, ~half area) restores coherence at the echo
- The **phase-encode gradient** is stepped once per TR; each step fills one k_y line. Between TRs, a **spoiler** or rewinder handles residual coherence depending on family (spoiled vs balanced — file 03)
- **Readout**: a dephasing lobe positions k-space at the edge, then the readout gradient sweeps through center to the opposite edge while ADC samples

With 3D slabs (SPACE, VIBE, MPRAGE, TOF), the slice direction is *phase-encoded* instead (partition direction) — no slice gaps, contiguous thin partitions, and reformat freedom (MPR source), at the cost of longer minimum scan time (N_partitions multiplies TR) — mitigated by turbo/parallel/CS factors.

---

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — foundations primer |
