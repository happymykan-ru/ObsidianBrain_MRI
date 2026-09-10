# Gradient-Echo (GRE) Family

**Version:** 1.0 | **Date:** 2026-09-08

The defining feature of this family: **no 180° refocusing pulse**. Echoes are formed by reversing a readout gradient, so only the *gradient-induced* dephasing is recovered — static field effects (B₀ inhomogeneity, susceptibility, chemical shift) keep accumulating. Signal therefore decays with **T2\***, not T2. That sounds like a weakness; in practice it is the engine of the fastest and most flexible sequences in MRI:

- No 180° pulses → **low SAR** and **short TR** (nothing to wait for between echoes)
- Low flip angles → only part of M_z is consumed per TR → short-TR steady-state imaging (T1 weighting in seconds)
- Sensitivity to local field → **T2\*** contrast, susceptibility imaging (SWI), BOLD, and iron quantification — and, the other side of the same coin, signal dropout wherever the field is rough (skull base, sinuses, metal), worse at 3T

Because there is no refocusing pulse, the family splits into three regimes by how they handle the *transverse magnetization left over at the end of each TR* — this one decision determines contrast, and it is the concept to master here:

1. **Spoiled** (FLASH, VIBE): leftover transverse signal is deliberately destroyed before the next TR → signal depends on how much M_z recovered → T1 weighting.
2. **Balanced** (TrueFISP): leftover signal is *completely preserved* and flows into the next TR → a coherent steady state mixing T1 and T2 → "T2/T1" contrast with bright fluid.
3. **Prepared** (MPRAGE, TurboFLASH, SR-TurboFLASH): an extra RF prep (inversion or saturation) stamps a contrast onto the magnetization *before* a fast readout — T1 contrast without waiting for TR.

Values throughout are recommended typical ranges — your protocols win where they conflict.

---

## 1. Spoiled GRE — FLASH (2D and 3D)

**What it is —** The base spoiled gradient echo: one low-flip-angle RF pulse per TR producing a **single gradient echo — one k-space line** (no echo train, no turbo factor) — with *spoiling* of residual transverse magnetization before the next TR. Siemens product name: FLASH.

**Contrast & good for —** Principally **T1**: fast T1 anatomy, post-contrast enhancement, and dynamic runs; the 3D form adds volume coverage and geometric fidelity. Beyond T1, FLASH is the base recipe under several other sequences: **T2\*** screening for blood products and iron, **PD** for cartilage, the **in-/opposed pair** for fat detection, **TOF MRA** for non-contrast angiography, **SWI** for microbleeds and venous anatomy, and **variable-flip-angle T1 mapping** for relaxometry.

**How it runs (one TR) —**

```
RF        α°
           ▀▄▄
G_read      |___dephase_|___readout__|_spoiler__|
G_phase     |_ step N _|            |
signal                        ✦ echo (at TE, decays e^(−TE/T2*))
TR         |<-------------- TR -------------->|   next: spoiler clears leftovers
```

- **Physics deep-dive — why spoiling is the whole game.**

    - After the readout, some transverse magnetization always remains. If it were left alone, the next RF pulse would partially *refocus* it into a new echo — creating "stimulated" history that mixes signal from several TRs ago. That history is exactly what a spin echo exploits (see SPACE in file 02) and what a T1-weighted GRE must *avoid*: it contaminates the simple "how much M_z recovered?" story.

    - Spoiling therefore does two things, and each kills what the other cannot:

    - 1. **Gradient spoiling** — a strong gradient lobe at the end of TR dephases the leftover transverse magnetization across each voxel so the voxel's *net* transverse signal is zero. But those fanned-out spins still exist in the transverse plane — gradient spoiling hides them, it doesn't destroy them.
    - 2. **RF spoiling** — that's why the RF phase must also be shuffled. If every pulse had the same phase, the leftover fan from one TR would meet the next pulse at the same relative angle every time: each pulse would partially refocus the previous TR's residue, building a coherent transverse history across TRs — exactly the mechanism TrueFISP cultivates deliberately (entry 4) and exactly what a T1-weighted FLASH must avoid. RF spoiling advances each pulse's phase by a different amount every TR (the Zur scheme: φ = ½φ₀·(j²+j+2), φ₀ ≈ 117°), so any earlier TR's residue meets the next pulse at an effectively random angle and its contribution averages to zero — no coherent pathway can form, and each TR becomes independent. The receiver phase rotates in lock-step so the true signal survives. Gradient spoiling zeroes the voxel average; RF spoiling kills the coherent residue; together they leave a steady state of pure longitudinal recovery.

    - With both in place, each TR is independent: excitation always starts from a clean, purely longitudinal state, and the signal equation is the simple steady state:
      ```
      S = k · PD · sin α · (1 − e^(−TR/T1)) / (1 − cos α · e^(−TR/T1)) · e^(−TE/T2*)
      ```

    - For a given TR, the flip angle that maximizes signal is the **Ernst angle**:
      ```
      α_Ernst = arccos(e^(−TR/T1))        e.g. TR 200 ms / T1 1000 ms → α ≈ 44°
      ```
    - Practical rules — 2D and 3D are the same physics pushed to opposite corners by one constraint: scan time.

    - **2D FLASH** pays one TR per phase-encode line per slice, with the other slices interleaved during the recovery wait — so a TR of 200–400 ms is affordable. At such TR the Ernst angle is ~35–50°, and protocols run *above* it (60–80°): above Ernst you trade a little SNR for stronger T1 contrast (tissues separate more). A contrast-first choice.

    - **3D FLASH** adds a partition axis, so scan time is TR × N_y × N_z (N_z 64–200): TR must shrink to 10–20 ms or the scan explodes. At TR ~15 ms the Ernst angle for T1 ~1000 ms is only ~10°, so α 10–30° sits *at* Ernst — the SNR-optimal angle. T1 contrast at such short TR is modest but adequate. A speed-first choice.

    - **TE — shortest for pure T1, with one deliberate exception.** For plain T1 weighting, TE is kept at its minimum (~2–5 ms, both 2D and 3D): any longer and T2\* decay begins to color the contrast. The exception is the in-/opposed-phase pair, where TE is set not for weighting but to precise chemical-shift values — the trick next.

    - **The in-/opposed-phase trick (chemical shift as a tool).** Fat and water protons precess at slightly different rates (fat ~3.5 ppm slower). After excitation they start in phase, drift apart, and come back together cyclically. At 1.5T the fat–water frequency difference is ~220 Hz → they are opposed every ~2.4 ms and in phase every ~4.8 ms; at 3T the difference doubles (~440 Hz) so the cycle halves (opposed ~1.2 ms, in-phase ~2.4 ms):
      ```
      TE_opposed ≈ 2.38 ms (1.5T) / ≈1.15–1.23 ms (3T)
      TE_in-phase ≈ 4.76 ms (1.5T) / ≈2.3–2.46 ms (3T)
      ```

    - A single dual-echo acquisition at both TEs yields the classic pair: opposed-phase images show *signal dropout at fat–water interfaces* (cells containing both fat and water — adrenal adenomas, hepatic steatosis, marrow) while in-phase shows no dropout — the reason a T1 "in/opp" pair is worth 30 seconds in adrenal/liver protocols.

    - **Dixon is exactly this acquisition, plus one step of arithmetic.** Two-point Dixon reads the same two echoes and computes **water = (IP + OP)/2** and **fat = (IP − OP)/2** pixelwise — one acquisition, four outputs (water, fat, IP, OP), which is why it replaced spectral fat sat as the body T1 standard. Multi-point Dixon (3–6 echoes) adds B₀ correction and fat-fraction quantification (PDFF) at the cost of more echoes per TR. The clinical difference is only what you do with the data: the plain pair is *read* (visual fat detection); Dixon is *computed* (robust fat suppression).


**Tunable choices —**

*Contrast*

| Knob | Typical value | Turning it… |
|---|---|---|
| Flip angle | 2D T1w 60–80°; 3D 10–30° | Toward Ernst maximizes SNR; above Ernst increases T1 contrast |
| TE | T1w: shortest; opposed/in-phase: the fixed chemical-shift TEs | Shortest = purest T1; the paired TEs give fat–water cancellation |
| TR | 2D 200–400 ms; 3D 10–20 ms | Shorter = faster + more T1 weighting (with Ernst-adjusted α) |
| Spoiling | always on (product default) | Turn it off and you are no longer FLASH — that is a different sequence |

*Speed & SNR*

| Knob | Typical value | Turning it… |
|---|---|---|
| Averages | 1–2 | Re-acquire and average: SNR ∝ √NEX, time ∝ NEX |
| GRAPPA | p2 | Fewer phase-encode lines, coil-reconstructed: time ÷2, SNR ≈ −29% |
| Bandwidth | chosen per sequence | One knob, three effects: lower BW = more SNR (longer sampling per pixel); higher BW = shorter minimum TE (readout finishes sooner) + less chemical-shift artifact (fat's Hz gap covers fewer pixels). At 3T, FLASH leans to higher BW and recovers SNR from the field surplus |

**Artifacts & pitfalls —** No refocusing: susceptibility hotspots drop out, worse at 3T. Flow is direction-dependent — through-plane inflow bright (TOF; mimics enhancement), in-plane flow saturated dark by the short TR, pulsatile CSF dephased — a trap in both directions. Opposed-phase fat–water rims masquerade as lesions. Geometric fidelity is FLASH's own virtue — isotropic 3D, no turbo blur, short TE at high bandwidth — and skipping fat sat preserves it by keeping fat–water boundaries clean; that combination is why stereotactic protocols use FLASH 3D without fat suppression.

**Used in this vault —** Everywhere fast T1 is the need, with the extras varying by job: thin-slice high-res 2D T1 (post-contrast brain pairs, orbit, larynx, enteroclysis mucosal work), dynamic 3D T1 (breast), and geometric fidelity where pixel positions must be trusted (stereotactic FLASH 3D for neuronavigation and radiosurgery planning). Free-breathing in-/opposed T1 in the liver protocols uses its single-shot cousin (entry 3).

---

## 2. VIBE — 3D spoiled GRE (the breath-hold T1 workhorse)

**What it is —** FLASH-3D retuned for the body — the same spoiled-GRE physics as entry 1, but with TR pushed to the floor through bundled acceleration and fat suppression built in, so a fat-suppressed T1 volume fits one breath-hold and can be re-acquired every few seconds. The abdomen/pelvis/post-contrast-brain T1 workhorse — set a FLASH-3D to TR ~3.5 ms + SPAIR + CAIPIRINHA + multiphase timing and you have built one.

**Contrast & good for —** Fat-suppressed T1 wherever enhancement must outshine fat; multiphasic imaging (arterial → portal → delayed) and dynamic contrast runs, re-acquired every few seconds. Wherever you need "T1 in one breath-hold, repeatedly," this is it.

- **Physics deep-dive — how VIBE differs from FLASH: the same engine, retuned.**

    - The identical part first, because it dissolves most of the confusion: VIBE *is* FLASH-3D. There is no new mechanism anywhere in VIBE. What differs is the *packaging*: the parameters are pushed to one extreme purpose, and the tools to do it are bundled into the product.

    - **TR pushed to the floor: 3–7 ms, versus 10–20 ms for generic FLASH-3D.** A naive FLASH-3D at its usual TR takes minutes (scan time = TR × N_y × N_z). VIBE buys the difference with a bundled stack of three independent tools from three branches of physics, whose savings multiply: **CAIPIRINHA** (parallel imaging — coils unfold the aliasing undersampled in *both* phase-encode axes, ÷~4), **partial Fourier** (conjugate symmetry — synthesize the un-acquired half, ÷~1.3), and an **asymmetric echo** (read only part of the echo — shorter TE, hence shorter TR). GRAPPA sits in the stack only as the parallel-imaging fallback when a protocol opts out of CAIPIRINHA or the hardware lacks it. Together — R4 × ~1.3 × shorter TR — is exactly how the TR lands at 3–7 ms and the slab fits ~15–20 s. The physics of each trade is unchanged; VIBE simply pays it upfront as the price of the breath-hold. At TR this short the Ernst angle is only ~5–7°, so the 10–15° flip angle sits *above* Ernst — the same low-flip-angle T1 regime as entry 1's 3D corner, pushed further.

    - **Fat suppression built in — SPAIR or Dixon — and why it is the default.** VIBE's home territory is post-contrast body T1, and on T1 the brightest normal tissue is fat: retroperitoneal fat, omental fat, marrow all glow, and enhancing tumor must outshine them to be seen. Suppression is therefore not an option but the point of the sequence (with a secondary benefit at 3T: removing fat also removes its 440 Hz chemical-shift artifacts). The two mechanisms — and the token naming: `_fs` = **SPAIR** (adiabatic fat inversion, B₁-robust, uniform at 3T — plain CHESS-style Fat Sat is B₁-sensitive and largely retired in VIBE); `_dixon` = **Dixon** (the dual-echo computation from entry 1, which suppresses fat *and* hands you the IP/OP pair from the same acquisition). That pair is what answers the fat-side questions when they arise — hepatic steatosis (fat fraction, from Dixon's fat output) and intracellular fat (the adrenal-adenoma test on the IP/OP pair). Each flavor pays its own time price: Dixon's second echo per TR roughly doubles the TR — and with it the scan — while `_fs` adds only a smaller per-TR spectral prep; so plain fs-VIBE is the faster option when the IP/OP pair isn't needed.

    - **TE stays shortest for T1 purity — and Dixon always costs a little of it.** T1 weighting wants TE ~1.2–1.5 ms; Dixon's second (in-phase) echo always sits later (2.46 ms at 3T, 4.76 at 1.5T), so its images carry a small T2\* toll at either field. The field-dependent part is the first echo: free at 3T (opposed-phase ≈ the shortest echo), forced longer at 1.5T (2.38 ms). Modest in practice — T2\* eats only a few percent at 2.5–5 ms — but real, and the trade Dixon makes for its four outputs.

    - **Purpose-built for dynamics.** Because there is no refocusing pulse, the volume can be re-acquired every few seconds — arterial, portal, delayed phases from the same sequence run. This exists only in the GRE family, and VIBE is the productized version of it.

**Tunable choices —**

*Contrast & suppression*

| Knob | Typical value | Turning it… |
|---|---|---|
| Flip angle | 10–15° (TWIST variants 25°) | Above Ernst → T1 contrast; lower → less T1, more SNR |
| TR / TE | TR 3.3–6.7; TE ~1.2–1.5 ms | Shortest possible — speed and T1 purity |
| Fat suppression | SPAIR / Dixon / none | SPAIR robust at 3T; Dixon adds fat fraction + in/opp for free |
| Dixon mode | 2-point (water/fat/IP/OP) | The reason your liver/pancreas protocols read four contrasts from one series |

*Speed*

| Knob | Typical value | Turning it… |
|---|---|---|
| CAIPIRINHA | 2×2 (R4) typical | ~4× acceleration with lower g-factor penalty than plain GRAPPA |
| GRAPPA | p2–p3 | Fallback acceleration |
| Breath-hold strategy | single BH / multiple BH / non-BH (StarVIBE) | See file 08 motion section |

**Artifacts & pitfalls —** Breath-hold failures (→ StarVIBE); fat–water swap in Dixon mode (dark rims everywhere — recognize it, reshim, or reacquire at in-phase TE); ringing at vessel–tissue interfaces during the arterial phase from undersampling; through-plane wrap-around in 3D — cover generously or oversample partitions.

**Used in this vault —** The vault's multiphasic and DCE backbone: liver, pancreas, kidney and adrenal multiphasic work; post-contrast brain and orbit; pelvis and SI-joint T1; and DCE across the prostate, cervix, rectum, salivary and orbital protocols. Its flavors carry the vault's specific choices — Dixon as the body's fat-suppressed standard, CAIPIRINHA for brain speed, TWIST where multi-arterial-phase timing matters (entry 9), and StarVIBE as the non-breath-hold escape (entry 8).

---

## 3. Magnetization-Prepared GRE — TurboFLASH and MPRAGE / MP2RAGE

**What it is —** A FLASH readout *preceded by a magnetization-preparation pulse* — usually a 180° inversion (IR) or a saturation pulse — that stamps the contrast before the fast readout runs. Two clinical faces: **TurboFLASH** (2D, single-shot-ish, used free-breathing for in-/opposed T1 and for first-pass cardiac perfusion — file 06) and **MPRAGE** (3D, the T1 anatomical standard of neuroimaging), with **MP2RAGE** as its quantitative, B₁-immune upgrade.

**Contrast & good for —** T1 with inversion-prepared contrast: the 3D T1 anatomy/gray–white volume (MPRAGE — the reformat source), B₁-uniform T1 + quantitative T1 maps (MP2RAGE), and free-breathing in-/opposed-phase T1 (single-shot TurboFLASH, one prep per slice).

**How it runs (MPRAGE) —**

```
one inversion        TI wait        rapid multi-flip readout
180°                                α  α  α  α  α  α  α  ... (~100-150 pulses,
  ▀▄▄           |<---- TI ---->|      ▄▀ ▄▀ ▄▀ ▄▀ ▄▀ ▄▀ ▄▀     one k-space line each,
                                         └──── one segment ────┘    TR ~10 ms)
        ↑ GM near zero, WM recovered
then: recovery → new inversion → next segment … until the whole 3D volume is filled
```

- **Physics deep-dive — why prepare at all?**

    - In a plain short-TR FLASH, T1 contrast comes from the *steady state* of partial recovery — workable, but the contrast window is set by TR and flip angle together and is relatively shallow. A preparation pulse does something stronger: it **sets the entire longitudinal magnetization to a known, extreme state** (e.g. −M₀ after inversion), then the readout samples the magnetization *as it recovers through the contrast-rich window*. T1 contrast is now stamped by the *preparation*, not by TR — so the readout can be extremely fast (segmented FLASH or single shot) without destroying contrast.

    - For MPRAGE the logic runs: invert everything → wait TI ≈ 900 ms (1 mm isotropic, 3T standard: TI 900 / TR 2300 / TE ~3 / α 9°) → at that moment white matter and gray matter sit at very different points on their recovery curves (gray matter near zero, white matter well recovered). The readout is **not one excitation** — it is a rapid train of ~100–150 small-α pulses, one k-space line each, ~10 ms apart: one inversion feeds *many* acquisition flips, all sampling the still-prepared magnetization before recovery erases the contrast. That group is one segment — and since the whole 3D volume cannot be read in a single window, the inversion–segment block is repeated **hundreds of times**: one fresh 180° + TI per segment (each block TR_3D ~2000–2500 ms), with the segment count = total k-space lines ÷ lines per segment. Each segment re-creates the same TI window, so the GM/WM contrast is stamped identically into every part of the volume. One IR, many flips, repeated — the "MP" (magnetization-prepared) + "RAGE" (rapid gradient echo) architecture. This is also why the flip-angle trade above matters: those ~150 pulses all bite into the *same* prepared M_z, and keeping them small is what lets the last line still see the inversion-stamped contrast.

    - **Why MP2RAGE exists.** MPRAGE prescribes one flip angle, but what the tissue *receives* is α × (B₁_actual / B₁_nominal) — and B₁ is not uniform across the head, especially at 3T, where the RF wavelength in tissue (~13 cm) is comparable to head size and sets up dielectric standing waves: the delivered flip angle runs high in some regions and low in others. On top of that, receive-coil sensitivity adds a second spatial brightness pattern. Two hardware patterns superimposed on the anatomy — so the same tissue looks different in different head regions. MP2RAGE runs **two readouts at two different TIs after a single inversion** (Siemens standard ~TI₁ 700 / TI₂ 2500 ms, TR 5000, α₁ 4° / α₂ 5°), giving two images with different T1 weighting but *identical* B₁ and coil effects. The scanner then computes the **UNI image** — a nonlinear (algebraic) combination of the two — in which proton density, T2\*, receive-coil sensitivity and most B₁ effects mathematically cancel, leaving an image whose intensity depends almost purely on T1. The same two images feed a pixelwise T1 fit → **quantitative T1 map** alongside the anatomical image. Cost: longer TR (two readouts), sensitivity to subject motion between the two readouts.

- **Physics deep-dive — why TurboFLASH runs in/opposed as two separate acquisitions.**

    - A dual-echo GRE grabs both echoes after one excitation — two readouts back-to-back (TE 2.38 then 4.76 ms @1.5T) — which works when the TR window is long enough for two readouts, as in FLASH and VIBE (entry 1).

    - TurboFLASH has no such window: it is single-shot — after its prep pulse it fills all of k-space in one continuous pass, one line every ~3–5 ms, with one fixed TE. A second echo at a different TE would require pausing the shot, which the sequence cannot do.

    - So the only way to get both chemical-shift states is two runs: one with TE at opposed phase, one at in-phase, displayed side by side — and no Dixon combination, since the pair is read, not computed.

    - That trade is deliberate: you pay with two acquisitions and lose the water/fat computation, and in exchange you get TurboFLASH's single-shot motion immunity — exactly what the free-breathing liver protocols need, where multi-shot FLASH would ghost.

**Tunable choices —**

*Contrast — MPRAGE / MP2RAGE*

| Knob | Typical value | Turning it… |
|---|---|---|
| TI | MPRAGE ~800–1100 ms; MP2RAGE 700/2500 ms | The contrast window — where gray/white sit on the recovery curve |
| Inversion TR | MPRAGE 2000–2500 ms; MP2RAGE ~5000 | Must allow full recovery between inversions |
| Flip angles | MPRAGE ~9°; MP2RAGE 4°/5° | Kept small on purpose — the readout is a transient, not a steady state (Ernst doesn't apply). Each pulse trades signal per line (sin α) against eating the prepared M_z (cos α): too large and the inversion-stamped contrast erodes across the segment. MP2RAGE's smaller angles also keep its two readouts from disturbing each other's samples of the recovery curve |

*Contrast — TurboFLASH*

| Knob | Typical value | Turning it… |
|---|---|---|
| Prep | **180° inversion** per slice (T1 in/opposed work); **90° saturation**, tipped then spoiled to M_z = 0, for first-pass perfusion (file 06) | The prep stamps the contrast — one prep per slice, then the whole slice's k-space in a single shot |
| TI — inversion prep only | ~100–400 ms (T1 weighting) | The wait after the 180°: where tissues sit on the recovery-through-zero curve = that slice's T1 contrast. The 90° saturation arm uses TS instead (file 06) |
| TE | the fixed in/opposed chemical-shift values (2.38/4.76 ms @1.5T; 1.23/2.46 @3T) | The fat-detection pair — the reason this variant exists |

*Speed — MPRAGE / MP2RAGE*

| Knob | Typical value | Turning it… |
|---|---|---|
| Voxel | 1 mm isotropic typical | The reason it is the reformat source |
| Lines per segment | ~100–150 typical | The speed-vs-contrast-sharpness dial: larger segments → fewer inversion blocks → faster scan, but the later lines of each segment are sampled further past the TI, so the GM/WM contrast window smears across the segment; smaller segments → every line near the TI, contrast crisp, but more blocks → longer scan |

*Speed — TurboFLASH*

| Knob | Typical value | Turning it… |
|---|---|---|
| Slice readout | whole slice in one pass, one line every ~3–5 ms | Freeze-frame per slice — free-breathing capable, no breath-hold needed |
| Slice interval | full T1 recovery before the next slice's prep | Makes the sequence slow per slice — the accepted price of its motion immunity |

**Artifacts & pitfalls —** MPRAGE: B₁ intensity variation at 3T (the MP2RAGE reason); motion between inversion and readout ruins the volume (reacquire); blood that missed the inversion reads bright. MP2RAGE: longer scan; motion *between its two readouts* corrupts the fit; the UNI image looks quantitative but isn't literally a T1 map. TurboFLASH: the long single-shot readout blurs — accepted, since each slice is motion-free.

**Used in this vault —** Prepared T1 is the vault's 3D anatomical standard (MPRAGE coronal as the reformat source), its B₁-robust quantitative upgrade in epilepsy work (MP2RAGE), its free-breathing single-shot form in liver/pancreas in-/opposed T1, and its saturation-recovery cousin carries cardiac first-pass perfusion (file 06).

---

## 4. Balanced SSFP — TrueFISP

**What it is —** The third GRE regime: instead of spoiling or ignoring the leftover transverse magnetization, the gradients are **completely balanced every TR** (zero net area on every axis), so the transverse signal from previous TRs is *fully preserved* and adds coherently into the next one. Siemens name: TrueFISP.

**Contrast & good for —** The balanced steady state scales with **T2/T1**: fluid and blood have long T2, so they shine against an intermediate background — the fastest bright-fluid/bright-blood contrast in MRI. Uses: bright-fluid and bright-blood surveys and localizers, **cine** function (file 06), and non-contrast MRA (NATIVE — file 05); also the fastest route to a bright-CSF myelogram-like image, at 1.5T especially, where a TSE equivalent would take minutes.

**How it runs —**

```
FLASH ends a TR by SPOILING the leftovers (destroying them).
TrueFISP ends a TR by REWINDING them — every gradient lobe is
followed by its exact mirror, net area zero on every axis.

one TR (TrueFISP):
RF:        α°                                     α°
            ▀▄                                     ▀▄
Gx(read):    ▁▂▃▄▅▆█▆▅▄▃▂▁                        net area 0
             └─ dephase ─┴─ readout ─┴─ rewind ─┘
Gy(phase):   ▁▂▃▄▅▆█▆▅▄▃▂▁                        net area 0
             └─ phase-encode ─┴─ exact reverse ─┘
signal:                             ✦
                    echo at TE = TR/2, automatically
```

- **Physics deep-dive — the two-pool recycle, and why it bands.**

    - **The frame.** z is the reservoir (magnetization parked there makes no signal); the α pulse pivots vectors **around the x-axis**; rotating +z around x lands fresh magnetization on **−y** — the signal direction, where every echo forms. Three directions, one machine.

    - **The α pulse does three things at once** — and this mixing *is* the sequence. (1) It tips a fresh sin α slice of the z-reservoir into −y (brand-new signal). (2) It acts on the old transverse pool too: the cos α fraction **stays transverse** (recycled). (3) The sin α fraction of that pool is pivoted **back into z** (returned to the reservoir). FLASH deliberately destroys the leftovers before they can meet the next pulse; TrueFISP deliberately feeds them into it.

    - **Balanced gradients — a trip out and back.** The encoding gradients open the fan; the readout closes it into the echo at TE = TR/2 (which is why the echo time is automatic, not chosen); the *rewinder* lobes — exact opposites of the encoding — close the fan again. End of TR: the transverse pool sits back at −y, phase-coherent, minus only its T2 decay. In a perfectly on-resonant voxel the pool is exactly where the next pulse wants it.

    - **The recycle loop.** Everything circulates between two pools:

      ```
              T1 recovery (1−e^(−TR/T1))
                     │
        ┌────────────▼────────────┐
        │     z reservoir         │◄────────────┐
        └────────────┬────────────┘             │
        α tips sin α → fresh signal            │ sin α return:
                     ▼                          │ the pulse pivots part of
        ┌─────────────────────┐                 │ the old pool back to z
        │  −y transverse pool  │────────────────┘
        └─────────────────────┘
        cos α survives the pulse; T2 decay drains it per TR;
        rewinders keep it coherent at −y for the next pulse
      ```

    - **Steady state = the balance of these flows** — the z pool is refilled by T1 recovery plus the sin α return, as fast as the α pulse spends it; the transverse pool is refilled by the fresh tip plus cos α survival, as fast as T2 drains it. Solving that balance gives the signal equation, and the T2/T1 ratio in it is the whole contrast story: long-T2 tissue (fluid, blood) loses almost nothing per TR, so its recycle runs near full efficiency → bright; short-T2 tissue bleeds its pool dry → dark.

      ```
      S ∝ M₀ · sin α / (1 + cos α + (T1/T2)·(1 − cos α))      (on-resonance form)
      ```

    - **Off-resonance: the pool stops arriving at −y.** The rewinders undo *gradient* phase, but a spin off-resonance by Δf also drifts by δ = 2π·Δf·TR per TR — time-based phase no gradient can touch. The pool therefore arrives at the next pulse at angle δ from −y. Decompose it: the cos δ projection still points along −y (recyclable), while the sin δ projection lies **along x — on the pivot axis itself** — where the rotation cannot move it (the same spectator geometry as CPMG). The recycle machine only ever sees cos δ of the pool.

    - **The collapse at δ = 180°.** The pool arrives at **+y — backwards**. Its surviving part now points opposite the fresh signal, so every TR the recycle *subtracts* instead of adds — the machine cancels itself and the voxel goes black. (At a band, TrueFISP has accidentally become FLASH: the recycle turned into a perfect spoiler.)

      ```
      δ (arrival angle)     0°        ±90°       180°
      cos δ                +1          0         −1
      recycle              full     nothing     anti-aligned →
      result               bright    dim        dark band
      ```

    - **From phase error to bands in the image.** Every voxel's brightness is set by its arrival error δ = 2π·Δf·TR: δ near 0 recycles fully (bright), δ = 180° destroys the recycle (black). Two knobs feed δ — TR (shorter = smaller error) and the field (steeper inhomogeneity = larger Δf). Bands exist at fixed frequencies (the nulls repeat every 1/TR), and a perfectly linear field would map them to evenly spaced stripes; a rapidly changing field instead *packs* them — it sweeps Δf through more nulls per centimeter, compressing the dark zones into denser, thinner lines (thickness = black-zone width ÷ field gradient). That black-zone width is set by the tissue: long T2 recovers from the null quickly (narrow black — thin dark lines over fluid), short T2 limps back (broad black — conspicuous dark swaths over muscle), so T2 decides how conspicuous the dark is against the bright. (With the standard alternating-phase RF scheme, the bright passbands sit at ±1/(2·TR) and on-resonance is itself a dark band — the scanner's center-frequency setting places the tissue of interest inside a passband.)

    - **Practical consequences.** Short TR does two favors at once: it shrinks every voxel's δ *and* pushes the nulls apart (spacing = 1/TR) until the anatomy's off-resonance range fits inside one bright zone — no null crosses the tissue at all. Shimming flattens Δf for the same end. Fat and water are intrinsically separated in frequency (3.5 ppm: 220 Hz at 1.5T, 440 Hz at 3T), and both must sit inside the ±1/(2·TR) passband to be bright and clean. At 1.5T a short-TR passband (±143 Hz at TR 3.5 ms) holds both peaks at once when the center frequency is set midway between them (±110 Hz each) — so fat sat is optional. At 3T the 440 Hz shift is wider than the window itself: tune to water and fat falls into a neighboring band (dark or erratically bright), and no center frequency can serve both — hence fat suppression at 3T. Flip angle is capped by SAR, not physics: ~70° at 1.5T, ~35–45° at 3T.

    - **Two family relations, worth separating.** Mechanically, TrueFISP's α pulse is SPACE's pulse: the same triple mixing — cos α stays transverse, sin α parks to z, fresh z is tipped — the "partial restore every TR" (file 02, entries 4 and 7). But for the weakness, contrast with the refocusing-pulse world: CPMG and SPACE both reverse off-resonance phase with their 180°-ish pulses, so static errors cancel at every echo; TrueFISP's α pulse is a pure rotation that reverses nothing — the error accumulates, TR after TR, and that accumulation is exactly what banding looks like.

**Tunable choices —**

*Steady state*

| Knob | Typical value | Turning it… |
|---|---|---|
| TR | ~2.5–3.5 ms (shortest possible) | Shorter = wider band spacing, less banding — the master knob |
| Flip angle | 1.5T 50–80°; 3T 35–45° (SAR cap) | Toward 90° → brighter fluid and more T2/T1 contrast |
| TE | = TR/2 automatically | Fixed by the balanced design |
| Shim | localized volume shim | The difference between a clean image and bands through the heart/bowel |

*Suppression & readout flavor*

| Knob | Typical value | Turning it… |
|---|---|---|
| Fat suppression | Fat Sat/SPAIR at 3T; often none at 1.5T | At 3T fat's chemical shift alone can band it |

**Artifacts & pitfalls —** Banding (above), and its bright companion: wherever the field sweeps rapidly across an interface, the frequency profile paints a dark line and a bright line together — a bright rim at a boundary is the profile's peak, not enhancement (it needs the steep sweep; a gentle field change just varies brightness). SAR cap at 3T; *not* T1-weighted — never use TrueFISP where you need T1 contrast. Blood stays bright only while flow is laminar: turbulent jets destroy the recycle's coherence and appear as dark voids — flow physics, not anatomy (and clinically useful in cine).

**Used in this vault —** Bright-fluid localizers and 2D bowel-motility loops (single-slice, breath-held cine) in the abdomen; cardiac planning localizers and all the cine work (file 06); TrueFISP cine loops of the thorax; and the readout behind NATIVE non-contrast renal MRA (file 05). The real-time CS variant is the cine rescue when gating fails.

---

## 5. Multi-Echo GRE — MEDIC

**What it is —** One excitation, then **3–6 gradient echoes read back-to-back**, all carrying the *same* phase-encode step and combined into **one k-space line**. Siemens name: MEDIC (multi-echo data image combination).

**How it runs —**

```
RF        α°
           ▀▄
G_read      ▁▂▃▄▅▆█▆▅▄▃▂▁  ▁▂▃▄▅▆█▆▅▄▃▂▁  ▁▂▃▄▅▆█▆▅▄▃▂▁   (monopolar: each echo
             └─dephase─┴─echo₁─┴─rewind─┴─dephase─┴─echo₂─┴─ …      its own readout pair)
signal          ✦₁              ✦₂              ✦₃
                └─────────── averaged into ONE k-space line ───────────┘
G_phase     ▁▂▃▄▅▆█▆▅▄▃▂▁   (one phase-encode step per TR — same for all echoes)
TR         |<------------------------- TR ------------------------->|
```

**Contrast & good for —** T2\*-family contrast with **SNR of an average of echoes**: the echoes are acquired at slightly different TEs and averaged (or summed with weights), which raises SNR while keeping the bright-CSF/myelographic character of GRE at short-to-medium effective TE. Classic uses: **cord gray–white contrast**, small-joint cartilage.

- **Physics deep-dive — why spend all echoes on one line, and why the flow compensation.**

    - **One line per excitation, still.** A single α pulse per TR, and all 3–6 echoes carry the *same* phase-encode step — they are averaged into one k-space line, not spread over many. The deliberate contrast with TSE: one 90° there produces N echoes that fill N different lines (turbo factor — the speed trick); MEDIC spends its N echoes on the *same* line and harvests their average instead. Same geometry, opposite trade: TSE converts echoes into speed, MEDIC converts them into SNR (√N-class gain from the averaging).

    - **Why MEDIC exists — SNR compensation for long TE.** The job is a bright-CSF, gray–white cord view, and T2-style contrast needs the effective TE long enough (~20–30 ms) that solid tissue decays while CSF (enormous T2\*) stays bright — TSE-T2 fails here anyway, because pulsatile CSF washes out in its long train (file 02). But single-echo GRE at that TE is SNR-poor — T2\* decay has eaten most of the signal. MEDIC's answer: read 3–6 near-free echoes around that TE after one excitation and average them into one k-space line — the noise averages down and buys the SNR back, effective TE ≈ train mean. Formally it stays T2\*-weighted; the T2 look is CSF's long T2\* against tissue's short one.

    - **Why there is no blur.** TSE blur happens because its echoes fill *different* k-space lines at different decay times — a decaying envelope across k-space blurs the image (file 02). MEDIC puts all its echoes into one line, so every line of k-space gets the same averaged weighting — no envelope, no blur. The trade is time, not sharpness: one line per TR, and no 180° train, so no TSE-class SAR either.

    - **Flow handling: short TE is the main protection; monopolar readouts are themselves readout-axis flow compensation.** The cord survives on the short effective TE (~20–30 ms): flow of any kind has almost no time to dephase (~1 mm of travel at 5 cm/s in 25 ms) — the opposite of TSE's long train, which hands pulsatile CSF hundreds of milliseconds to wash out and ghost (file 02). The monopolar design *is* a compensation scheme: each echo owns its dephase–readout pair, so each echo's first moment M₁ is nulled — velocity compensation along the readout axis, echo by echo. That serves flow along the readout direction; through-plane flow (the dominant CSF motion in cord axials) is covered only by the short TE.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Number of echoes | 3–6 | More = more SNR, longer minimum TR |
| Effective TE | ~20–30 ms (weighted mean) | Shorter → less T2\* blur, less bright-CSF; longer → more T2\* character |
| Echo spacing | short (limited by readout time) | Keeps echoes inside the usable T2\* window |

**Artifacts & pitfalls —** T2\* decay across the train smears edges if the echo spacing grows; sensitivity to off-resonance at the skull base/chest; not a quantitative sequence (that is the next entry).

**Used in this vault —** Cord axials — the one niche where MEDIC replaces TSE-T2 (pulsatile CSF would wash out in its train) — and one MSK job chosen for its own virtues: an isotropic 3D wrist volume, where the bright-fluid contrast and echo-averaged SNR serve thin-slice cartilage detail.

---

## 6. T2\* Mapping (multi-echo GRE relaxometry)

**What it is —** The quantitative sibling of MEDIC: a GRE readout at **many echoes with a *monoexponential* decay model fitted pixelwise** to produce a T2\* (or R2\* = 1/T2\*) map instead of an image.

**Contrast & good for —** Quantitative tissue iron: T2\* shortens as iron content rises (ferritin/hemosiderin are locally paramagnetic). Clinical anchors: **cardiac iron** (thalassemia — T2\* < 20 ms is abnormal, < 10 ms severe) and **hepatic iron** (multi-echo GRE with R2\* thresholds), plus research applications (MS, Parkinson). Contrast = a number that tracks iron, comparable across scanners.

- **Physics deep-dive — why many echoes, and what can corrupt the fit.**

    - **The measurement.** As in MEDIC, one excitation produces a train of echoes at increasing TEs, all sharing the same phase-encode step (same voxel at every TE) — but each echo is stored to its own image instead of averaged. The output is twofold: the **raw TE images** (each progressively more T2\*-weighted; they serve as source and QC) and the fitted **color-coded map, milliseconds per pixel**, from the voxel-wise fit across them. Iron shortens T2\* (locally paramagnetic), so the fitted number tracks iron content — comparable across scanners.

    - **Sampling the curve: three rules.** One T2\* value mathematically needs two points, but a trustworthy fit needs the whole curve sampled: several echoes (products use 8–14); the **first echo as short as possible** — if the first TE is too long, the short-T2\* tissue you care about (the iron-laden one) has already decayed away before sampling begins; and the **last echo beyond the expected T2\*** — stop too early and the fit extrapolates the tail from noise, overestimating T2\*.

    - **The fit.** S(TEᵢ) = S₀·e^(−TEᵢ/T2\*); plot ln(S) against TE: a straight line whose slope is −1/T2\* — T2\* in hand.

    - **Corruption 1 — fat's beat.** A voxel containing both fat and water has two components precessing at different frequencies. As TE advances, the fat component rotates against the water one, and the combined magnitude *oscillates* on top of the decay — a wiggle the monoexponential fit can't describe, biasing the number. Fix: fat suppression, or multi-peak fat modeling (which is why liver R2\* quantification models fat explicitly).

    - **Corruption 2 — short TR.** Keep TR long enough for recovery: too short, and the whole train's amplitude is T1-saturated (the tail sinks into noise) and leftover transverse from the previous TR can leak into the later echoes as stimulated echoes — either way the tail is unreliable and the fit is biased.

    - **And why the readout must be monopolar.** All echoes must be read with the same gradient polarity: bipolar readouts reverse the fat–water phase accrual every other echo, turning the beat into an unmodelable zig-zag. Monopolar keeps the beat monotonic — and therefore fit-able.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Echo count / spacing | 8–14 echoes; first TE shortest possible; last TE ≥ expected T2\* | The sampling of the decay curve (above) |
| TR | long (≥5×T1 of interest) | Kills T1 contamination of later echoes |
| Flip angle | 50–60° | Trade SNR vs T1 leakage |
| Fat handling | none (heart) / suppression or fat modeling (liver) | The liver needs it; the heart usually does not |
| Inline map | T2StarMap / R2\* map on | Scanner fits and displays the map automatically |

**Artifacts & pitfalls —** Bipolar-readout bias and T1 contamination at short TR (both above); fat's beat in the liver. In the heart, each voxel's decay is assembled across heartbeats from different tissue positions — dark-blood prep removes the worst offender, the bright moving blood (file 06). And the fit always measures tissue + field: a residual shim gradient dephases across the voxel and reads as iron (a ~20 Hz spread can halve a 20 ms myocardial T2\*; one reason cardiac T2\* is 1.5T-only).

**Used in this vault —** Cardiac 10-echo and liver 14-echo T2\* protocols (iron quantification, e.g. thalassemia screening and follow-up) and inline T2\*-map series for the heart and liver.

---

## 7. SWI — Susceptibility-Weighted Imaging

**What it is —** A high-resolution **3D fully flow-compensated spoiled GRE** whose *phase* information is used as a second contrast channel: a high-pass-filtered phase mask multiplies the magnitude image, and the result is displayed as thin minimum-intensity projections (mIP).

**Contrast & good for —** Anything that perturbs the local field: **deoxyhemoglobin/hemosiderin (microbleeds, DAI), calcium, iron deposits, and venous anatomy** (veins are dark because of deoxyhemoglobin). Clinical: microbleed screening (CAA, hypertension), trauma, cavernomas, hemorrhagic metastases, calcified lesions, and venous mapping around lesions.

- **Physics deep-dive — why magnitude alone is not enough, and what the phase mask adds.**

    - A susceptibility source (iron, deoxyhemoglobin, calcium) shifts the local Larmor frequency, so spins around it accumulate phase *and* lose signal (T2\*). On a magnitude image, small sources are invisible — the signal loss needs a whole voxel of affected tissue, and veins/microbleeds are smaller than that. But the **phase** is sensitive to much smaller perturbations: a voxel adjacent to a susceptibility source carries a phase offset even when its magnitude is untouched.

    - The pipeline, in four steps:

    - 1. **High-pass filter the phase image.** The phase image is free — the angle of each voxel's complex signal, a field map (φ = γ·ΔB·TE) — but raw phase is dominated by slow, global variations (B₀ error, shim, coil geometry) that dwarf the local effects; the high-pass removes the background so only the fine, local field bends remain.
    - 2. Build a **mask** from the filtered phase (0 where abnormal, 1 where normal).
    - 3. Multiply the mask into the magnitude, raised to a power m ≈ 3–4 — darkening the abnormal voxels.
    - 4. Display via **mIP** over 8–10 mm — a *minimum* projection (the targets are dark; the mirror of TOF's MIP), turning scattered dark dots into continuous veins and conspicuous microbleeds.

      ```
      one 3D GRE acquisition (complex data)
              ├──► MAGNITUDE image — the usual T2*-weighted GRE
              └──► PHASE image — each voxel's angle (a field map)
                       │ high-pass filter: drop the slow background
                       ▼
                  filtered phase — only fine, local field bends remain
                       │ abnormal phase → 0, normal → 1
                       ▼
                  phase mask (0–1)
                       │ multiply, raised to a power m ≈ 3–4
                       ▼
              SWI = magnitude × mask^m     (susceptibility voxels darkened)
                       │ mIP over 8–10 mm slabs
                       ▼
              the display: dark veins, dark microbleeds
      ```

    - **What comes out — four series, four jobs.** The phase never appears *inside* the processed SWI image (there it exists only as the mask — multiplication, not addition), but it survives as its own series. Siemens sends: **mIP** — the workhorse display (dark veins, punctate foci; microbleed count and distribution: lobar favors CAA, deep favors hypertension; venous anomalies and abnormal draining veins); **magnitude** — the raw anatomy, used to verify that a dark mIP spot is a real parenchymal focus and not a vessel cross-section or air-interface susceptibility; **phase** — the identification map (calcium vs hemorrhage); and the **processed SWI** volume itself, the mIP's source.

    - **The sign convention, and the paradox it explains.** Paramagnetic sources (iron, deoxyhemoglobin) make nearby spins precess *faster*, diamagnetic (calcium) *slower* — opposite phase directions, and that sign is the identification marker (Siemens' left-handed convention: paramagnetic bright on the processed phase, calcium dark — the opposite of right-handed systems, so know yours). On the magnitude image both are dark regardless: the darkness comes from the field *gradient* around the source, which dephases the voxel whatever the shift's sign (T2\* blooming) — magnitude alone cannot tell calcium from hemorrhage. The mask multiplication then sharpens what magnitude started: SWI = magnitude × mask^m, mask ≈ 1 at normal phase and ramping toward 0 for strong shifts, m ≈ 3–4 making the suppression steep (0.5³ = 0.125) — phase-abnormal voxels darkened severalfold on top of their intrinsic T2\* loss. The dark image shows *where*; the phase map shows *what*.

    - **Why fully flow-compensated, all three axes — and why it's fixed, not a knob.** The phase map must carry only susceptibility: flowing blood accrues velocity phase (φ = γ·M₁·v) on any axis whose first moment isn't nulled, polluting the phase and ghosting the magnitude. M₁ is therefore nulled on readout, phase-encode and slice-select alike — through-plane flow dominates in a 3D slab, so one axis is not enough. It is built into the product rather than offered as a choice, because the sequence is pointless without it; the cost (longer minimum TE from the extra lobes) is absorbed by the deliberately long TE, and only the acceleration moment M₂ remains uncompensated.

    - TE choice follows the same logic as T2\* mapping: long enough that susceptibility has developed (≈ **20 ms at 3T, ≈ 40 ms at 1.5T**), because the effect scales with field strength.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| TE | ~20 ms (3T) / ~40 ms (1.5T) | Longer = more susceptibility contrast, more signal loss |
| Resolution | 0.5–1 mm 3D partitions | Small sources need small voxels |
| Display | magnitude / phase / SWI / mIP (Siemens outputs all four) | mIP for reading vessels & microbleeds; phase for calcium vs hemorrhage |

**Artifacts & pitfalls —** Phase-wrap and filter artifacts at the brain edge; anything ferromagnetic (implants, dental work, air–bone interfaces) obliterates nearby signal; calcium vs hemorrhage needs the phase image and knowledge of your vendor's convention; mIP hides T1-bright structures — always read the source magnitude too.

**Used in this vault —** The epilepsy protocol (3D SWI axial), and as a named add-on for microbleed/hemorrhage screening in the plain and contrast brain protocols.

---

## 8. StarVIBE — Radial VIBE

**What it is —** VIBE re-plumbed with a **radial (stack-of-stars) k-space trajectory**: each TR reads one "spoke" through k-space center; consecutive spokes are rotated by the **golden angle (~111.25°)**, which never repeats an orientation.

**Contrast & good for —** The same T1 dynamic contrast as VIBE, but **free-breathing**: liver/pancreas multiphasic and delayed phases, enteroclysis, post-contrast head-and-neck and pelvis in patients who cannot hold their breath. Motion robustness is the entire point.

- **Physics deep-dive — why radial spokes beat cartesian lines under motion.**

    - **What a spoke is.** One TR produces one echo = one spoke: a single **diameter line** through k-space center (both ±k halves at once) — a *line*, not a filled sector. A diameter at angle θ is the same line as at θ+180°, so the spoke orientations only need to span 180° to cover the whole disk; the disk is filled by many diameters at many angles.

    - **The mechanism is averaging, not correction — this is what separates it from BLADE.** BLADE acquires full strips and *estimates and corrects* each blade's motion retrospectively (file 02). StarVIBE acquires single spokes and never tries to fix anything: each spoke is a few-ms snapshot, so every spoke samples a different instant of the breathing cycle, and the reconstruction simply averages them all. Motion becomes mild blur instead of ghosts — tolerance by averaging, no detection, no correction.

    - **The golden angle (~111.25°) — the orientation step between successive diameters.** Spoke n sits at θ_n = n × 111.25° (mod 180°) — the "most irrational" angle, chosen so consecutive spokes spread as evenly as possible: no two orientations ever coincide, and *any* window of consecutive spokes covers the circle near-uniformly.

    - **How the 3D works — a stack of stars.** k-space is organized as a cylinder: kx-ky sampled radially (the spokes), kz sampled cartesian (the partitions, swept sequentially). Each spoke-column runs one angle through all partitions, then rotates to the next angle; every partition shares the same angular pattern.

    - **Why arbitrary windows work — the center is sampled at every moment.** In cartesian imaging the center lines are acquired at specific times (hence CE-MRA's centric ordering). Radial has no such moment: *every* spoke passes through the center, so every TR contributes a fresh center sample. Any window of consecutive spokes therefore contains its own complete center plus a near-uniform periphery (the golden-angle property) — the ingredients of a full image, at whatever moment you choose. Two retrospective tricks follow. **Dynamic framing:** slide a window of N consecutive spokes along the time axis — each window is one frame, so the continuously acquired data becomes a multiphasic series with no breath-hold gaps, and the arterial phase is always inside some window (data exists at every moment). **Respiratory sorting:** bin spokes by the bellows/navigator position at acquisition — each bin still has uniform angular coverage, so each bin reconstructs a respiration-frozen image. One acquisition, three ways to slice it: all spokes (averaged static image), time windows (dynamic series), breathing bins (motion-frozen).

    - **What is adjustable, and the costs.** Each spoke has zero angular width — the knob is the spoke *count* (more spokes = finer angular sampling, less streaking, longer scan), not the golden-angle step, which is fixed in the product. Radial needs ~π/2× more spokes than cartesian lines for equal nominal resolution (the circle-vs-square redundancy, as in BLADE), and the reconstruction is gridding-based — streaks appear if too few spokes are used or the gradients are miscalibrated.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Spokes (per partition/time frame) | set by protocol | More = SNR and less streak; fewer = faster frames |
| Flip angle / TR/TE | as VIBE (α 10–15°, TR ~2.8–3.5 ms) | Same T1 logic as entry 2 |
| Fat suppression | SPAIR (product standard) | Spectral fat sat is compatible with radial readout |
| Temporal framing | continuous dynamics + arbitrary phases | Free-breathing arterial/portal/delayed from one run |
| CS combination | GRASP-VIBE (radial + compressed sensing) | Extra acceleration for DCE at the cost of iterative recon |

**Artifacts & pitfalls —** Radial streaks from extreme motion or too few spokes; slight blur (accepted); gridding demands good gradient calibration — misplaced samples streak (cartesian's grid is built-in, so it never faces this); and one frame costs ~1.57× a cartesian VIBE's — the price of continuity: wins for long dynamic loops (no breath-hold gaps), loses for one quick breath-hold shot.

**Used in this vault —** Three categories of free-breathing T1 jobs. The non-breathhold dynamics: multiphasic liver/pancreas and hepatobiliary delayed phases. The motion-immune T1s: MRCP-adjacent T1, enteroclysis, post-contrast head-and-neck, a generic pelvis option. And interventional work: the in-/opposed pair for localization.

---

## 9. TWIST — View-Sharing Time-Resolved GRE

**What it is —** A 3D spoiled GRE that **re-samples only the center of k-space on every frame** and reuses (shares) the periphery from neighboring frames — trading a little spatial detail for a temporal resolution of ~1–3 s per frame. Siemens: TWIST (time-resolved angiography with interleaved stochastic trajectories); the vault also runs it on VIBE-Dixon for multiphasic liver.

**Contrast & good for —** T1-dynamic *time series*: contrast arriving and washing through vessels and organs. Time-resolved MRA/MRV (AVM, dural fistula, pelvic congestion, gonadal vein), and **multi-arterial-phase liver imaging** (catching pure arterial frames despite variable circulation times).

- **Physics deep-dive — what "sharing the periphery" actually sacrifices.**

    - k-space center = contrast and SNR; periphery = edges and resolution. In a dynamic study the contrast changes frame to frame while the anatomy (edges) barely does — so TWIST splits each frame's sampling into two regions of the **phase-encode/partition plane** (ky-kz; the readout direction is always fully sampled):

    - **Region A — the center, measured every frame.** The central ~15–30% carries the contrast, which changes frame to frame — so it is re-measured completely each time.

    - **Region B — the periphery, divided into random subsets.** The remaining lines, which carry mostly static edge information, are shuffled into a pseudo-random sequence and divided into chunks (e.g., ~20% each). Each frame measures all of A plus the *next chunk* of B, then advances — the subsets are iterated round-robin, so after one full cycle every B line has been freshly measured once.

    - **The missing lines are borrowed (view-sharing).** A B line not measured in this frame is filled from the most recent frame that did measure it — frame N's periphery may be "N−2's periphery", harmless while the anatomy is static, which is exactly the situation during a contrast pass. The randomness matters: regular skipping would alias into structured ghosts; an incoherent subset spreads the sharing error as benign, noise-like artifacts.

    - **The gain, and the price.** Frame time falls from "full k-space at TR" to "A + one B-chunk at TR" — roughly 2–3× alone, up to ~12× combined with GRAPPA. The price: if the patient moves (or bowel peristalses) between frames, the borrowed periphery and the fresh center disagree → ghosting/edge blur. In the liver-TWIST-Dixon variant the same logic runs per phase (arterial frames at ~5 s, then PVP, delayed…), with Dixon fat suppression.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| Region A size | 15–30% of k-space | Larger A = fresher contrast, slower frames |
| Region B sampling | 10–30% of periphery per frame | Higher = less sharing, faster refresh, slower frames |
| Frame interval | 1.2–3.2 s (with GRAPPA down to ~1 s) | The product of the above two choices |
| Readout flavor | plain TWIST / TWIST-Dixon / TWIST-VIBE | Dixon adds fat-suppressed multiphasic (liver) |
| k-space ordering | stochastic interleave within B | Prevents regular undersampling artifacts |

**Artifacts & pitfalls —** Ghosting when anatomy moves across shared frames; center-periphery mismatch if contrast arrives *during* a frame; temporal resolution is real but *not* true "cine" — do not quantify fast physiology from TWIST frames; vein–artery overlap if the frame rate misses the pure arterial window (read the series, not one frame).

**Used in this vault —** Time-resolved cerebral MRV/AVM (head, with ePAT), dynamic facial AVM, EC/IC bypass flow dynamics, pelvic MRV (May-Thurner-type congestion), gonadal-vein tracking in undescended-tests work, and the multiphasic hepatic/pancreatic arterial-phase series on VIBE-Dixon.

---

## 10. SR-TurboFLASH — Saturation-Recovery First-Pass Perfusion

**What it is —** A TurboFLASH readout preceded by a **90° saturation pulse** instead of an inversion — repeated every heartbeat to track a contrast bolus's first pass through the myocardium (cardiac — detailed in file 06).

**Contrast & good for —** T1 shortening by gadolinium during first pass = **myocardial perfusion** (stress vs rest ischemia detection).

**How it runs —**

```
each heartbeat (ECG-triggered, diastolic):

RF:       90°(sat)  spoil            α  α  α  α … (TurboFLASH readout)
           ▄▀       ▄▄▄              ▄▀ ▄▀ ▄▀ ▄▀
M_z:        ──► 0              |<── saturation time ~100 ms ──>|
recovery:                            M_z = M₀·(1 − e^(−t/T1))
                          └─ brighter = shorter T1 ─┘
repeat every heartbeat through the bolus → the dynamic series
```

- **Physics deep-dive — why saturation, and what the bolus does.**

    - **Saturation gives a monotonic readout of T1.** The 90° + spoiler wipes M_z to zero — no sign flip, no null — and recovery from zero is the simplest curve: M_z = M₀·(1 − e^(−t/T1)). After a fixed delay (the saturation time, ~100 ms), brightness is a clean readout of T1: shorter T1 has recovered further, so it is brighter. The alternative, inversion, folds through zero (magnitude non-monotonic) and demands a precise TI — fragile for a prep that must fire every heartbeat with wandering R-R intervals.

    - **The per-beat loop and the bolus.** Each heartbeat: saturate → wait the fixed delay → TurboFLASH-read the slice(s) → repeat through the bolus passage. Gadolinium shortens T1 in perfused tissue → those segments brighten during the first pass; ischemic segments receive little contrast and stay dark — the first-pass deficit is the diagnostic image.

    - **Why stress and rest.** At rest, a ~50% stenosis can look normal. Under vasodilator stress, healthy territories increase flow several-fold while the stenosed one cannot — the deficit appears only under stress. Deficit at stress with normal rest = reversible ischemia; deficit in both = scar (correlate with LGE — file 06).

**Tunable choices —** (full table in file 06: slice count per beat, prep time, stress/rest pairing, contrast dose/rate.)

**Artifacts & pitfalls —** Dark-rim artifacts at the subendocardium (susceptibility at the blood–muscle interface, partial-volume of dark blood); arrhythmia breaks the per-beat timing; stress imaging needs the patient's heart rate elevated — motion and rate limit the readout.

**Used in this vault —** Cardiac stress/rest perfusion (file 06 for details); the magnetization-prepared logic also underlies the free-breathing in/opp TurboFLASH in the liver protocols (entry 3).

---

## Family summary

| Sequence | Regime | Contrast | Speed character | Standout physics risk |
|---|---|---|---|---|
| FLASH 2D/3D | spoiled | T1 (or T2* at long TE) | short TR | T2* loss at susceptibility |
| VIBE | spoiled 3D | T1 | breath-hold/dynamic | fat–water swap (Dixon) |
| TurboFLASH / MPRAGE / MP2RAGE | prepared | T1 (prep-stamped) | fast readout | B₁ variation (MPRAGE) |
| TrueFISP | balanced | T2/T1, bright fluid | very short TR | off-resonance banding |
| MEDIC | spoiled multi-echo | T2*/bright CSF | one excitation, N echoes | T2* edge blur |
| T2* mapping | spoiled multi-echo | quantitative R2*/T2* | N echoes + fit | T1/fat contamination of fit |
| SWI | spoiled 3D + phase | susceptibility | long TE needed | phase convention, wrap |
| StarVIBE | radial spoiled | T1 | free-breathing | streaks, blur |
| TWIST | spoiled + view-share | T1 dynamic | 1–3 s frames | shared-periphery ghosts |
| SR-TurboFLASH | prepared (SR) | T1 first-pass | per heartbeat | per-beat timing |

---

**Key sources** — Siemens Healthineers (MAGNETOM World protocols; StarVIBE, TWIST brochure, syngo MR; CS cardiac cine); mriquestions.com: [spoiling](https://www.mri-q.com/spoiling---what-and-how.html), [Ernst angle](https://ratio.mriquestions.com/optimal-flip-angle.html), [in/out phase](https://www.s.mriquestions.com/in-phaseout-of-phase.html), [TrueFISP](https://www.s.mriquestions.com/true-fispfiesta.html), [multi-echo GRE](https://ca.mriquestions.com/multi-echo-gre.html), [iron T2*](https://ratio.mriquestions.com/iront2-mapping.html); SWI physics (UCSD SWI course; Reichenbach); papers: Breuer CAIPIRINHA (MRM 2006), TWIST validation (Invest Radiol 2010); Radiopaedia: [TWIST](https://radiopaedia.org/articles/twist-time-resolved-angiography-with-interleaved-stochastic-trajectories-1).

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — 10 gradient-echo entries |
