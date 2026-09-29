# Spectroscopy & Functional MRI

**Version:** 1.0 | **Date:** 2026-09-08

This file holds the vault's two non-imaging "contrast" methods: **MRS** — which turns the chemical shift of protons into a *spectrum* of metabolites rather than an image of water — and **ASL**, the non-contrast perfusion technique, which is not yet implemented in any vault protocol (it appears only as a named alternative in the Diamox protocol) and is therefore treated as reference knowledge rather than an in-vault workhorse.

MRS deserves care: the single voxel or CSI grid replaces the image-encoding game with *localization* — making sure the spectrum comes only from the tissue you want — and every parameter choice (TE, voxel size, suppression) directly reshapes the peaks you read.

Values throughout are recommended typical ranges — your protocols win where they conflict.

---

## 1. MRS — Magnetic Resonance Spectroscopy (sLASER CSI)

**What it is —** Instead of imaging, the signal is read out as a **spectrum**: the different chemical environments of protons (in water, fat, NAA, choline, creatine, lactate…) precess at slightly different frequencies — the **chemical shift** — and after a water-suppressed, localized acquisition, a Fourier transform of the FID yields peaks at each metabolite's frequency. The vault runs **multivoxel CSI with sLASER localization at TE 135** (`csi_slaser_135`).

**Contrast & good for —** Metabolite *concentrations* and ratios in a defined tissue volume: in the brain, **NAA** (neuronal marker — falls in tumor, epilepsy, neurodegeneration), **choline** (membrane turnover — rises in tumor), **creatine** (relatively stable reference), **lactate** (anaerobic metabolism — rises in tumor, ischemia, mitochondrial disease). TE 135 additionally *inverts* lactate, separating it from the lipid signal that otherwise hides it. Clinical uses: brain tumor grading/treatment follow-up, epilepsy lateralization, metabolic disease.

- **Physics deep-dive — the four mechanisms, in the order a spectrum is built.**

    - **1. Chemical shift — why metabolites have different frequencies.** Electrons shield nuclei: protons in different molecules experience slightly different effective B₀ and precess at slightly different frequencies. The shifts are tiny — a few parts per million (ppm) of the Larmor frequency (at 3T, 1 ppm = 128 Hz) — but resolvable. The spectrum plots signal vs ppm, with water at 4.7 ppm. The clinical peaks: choline ~3.2, creatine ~3.0, NAA ~2.0, lactate ~1.33 ppm (a *doublet* — see below), lipids ~0.9–1.5.

    - **2. Localization — the CSI and sLASER story.** A spectrum from the whole head would be dominated by scalp fat and useless. Localization confines the signal:

    - **Single-voxel** (PRESS/STEAM/sLASER): three orthogonal slice-selective pulses excite only the box-shaped intersection voxel (the classic 90°–180°–180° scheme of PRESS). Simple, robust, one region at a time.
    - **CSI (chemical shift imaging, the vault's choice):** a slab is excited and *phase-encoded in two dimensions without a readout gradient* — a grid of voxels ("multivoxel"), each yielding its own spectrum. CSI gives spatial coverage (lesion + contralateral normal for comparison) at the cost of voxel bleed (point-spread function) between grid elements and longer scan time.

    - **sLASER** is the modern localization choice because of a subtlety called **chemical-shift displacement error (CSDE)**: the slice-selective pulses in PRESS/STEAM are frequency-selective, and since metabolites differ in frequency, each metabolite's "voxel" is shifted spatially relative to the others — at 3T with PRESS this displacement is ~11.6 %/ppm, meaning the lactate voxel can be a centimeter away from the NAA voxel inside a large grid element! **sLASER uses adiabatic full-passage refocusing pulses** (which define their slice by amplitude modulation, insensitive to frequency offset) reducing CSDE to ~2 %/ppm — the reason the vault's 3T multivoxel runs sLASER rather than PRESS.

    - **3. Water and lipid suppression — what you must kill to see metabolites.** Water is ~10,000× more concentrated than the metabolites of interest; without suppression its huge peak and tails swamp the spectrum. **CHESS/WET** (frequency-selective saturation of the water line before the localization) or VAPOR-type schemes handle water; **OVS (outer-volume saturation)** — saturation bands around the volume of interest — kills the skull/scalp lipid signal that no amount of frequency selection can remove (lipid is *inside* the excited slab edge).

    - **4. TE choice — the lactate inversion.** Lactate is a J-coupled spin system: its two protons split each other's resonance into a **doublet**, and the *phase of that doublet evolves with TE*. At short TE (~30 ms) the doublet is upright but sits under the lipid peak (lipids at 0.9–1.3 ppm overlap it). At TE 135–144 ms (= 1/J, J ≈ 7 Hz), the doublet has evolved to *inverted* — a clear downward doublet at 1.33 ppm, separated from the (still upright) lipid baseline. That is the entire point of the vault's TE 135: **see lactate as an inverted doublet below the lipid hump**. TE 30 gives the most metabolites (more peaks, better SNR) but a messier lactate region; TE 270 restores upright lactate at further SNR cost.

**Quality gates before reading any spectrum:** shim quality — the water peak's full width at half maximum should be ≤ ~0.1 ppm (~6 Hz @1.5T, ~13 Hz @3T); broad peaks mean bad shim and unreliable ratios. Voxel placement must avoid lipid (skull, scalp), hemorrhage, and CSF (partial volume dilutes all metabolites).

**Tunable choices —**

*Localization & coverage*

| Knob | Typical value | Turning it… |
|---|---|---|
| Method | sLASER (vault, 3T-robust) vs PRESS/STEAM | CSDE — the sLASER advantage (above) |
| Single-voxel vs CSI | CSI multivoxel (vault) vs single voxel | Coverage vs voxel bleed / time |
| Voxel size | ~8 cm³-class (2×2×2 cm) single; CSI grid elements similar | Bigger = SNR; smaller = less partial volume, more time |

*Spectral content*

| Knob | Typical value | Turning it… |
|---|---|---|
| TE | 30 (max metabolites) vs **135–144 (lactate inversion)** vs 270 | What the spectrum shows (above) |
| Water suppression | CHESS/WET-class | Mandatory — see above |
| OVS bands | around VOI | Kills skull/scalp lipid |
| Shim | interactive + 3D shim; FWHM ≤ 0.1 ppm | The quality gate — never read a bad shim |

*Timing & volume*

| Knob | Typical value | Turning it… |
|---|---|---|
| Averages | ≥8 (single-voxel); CSI as grid requires enough | SNR ∝ √averages — MRS is SNR-starved |
| TR | 1500–2000 ms typical | Longer = less T1 saturation of metabolites, slower |

**Artifacts & pitfalls —** Lipid contamination (voxel too close to skull — the #1 practical failure); bad shim (broad peaks — unreadable); water suppression failure (huge water peak, baseline roll); motion during the long acquisition; voxel bleed in CSI (a lesion "present" in the adjacent normal voxel); partial volume with CSF dilutes peaks; TE-135 lactate is inverted — read it as a *downward* doublet, not an artifact (a classic misread); ratios (Cho/Cr, NAA/Cr) are the robust currency, not absolute values.

**Used in this vault —** Multivoxel CSI with sLASER localization at TE 135 for brain-tumor (GBM-class) metabolic assessment — choline/NAA elevation mapping and lactate detection.

---

## 2. ASL — Arterial Spin Labeling

**What it is —** Perfusion imaging that **uses magnetically labeled arterial blood water as the endogenous tracer**: inflowing blood is "tagged" by an RF pulse, then imaged after a delay long enough for it to reach the tissue; subtracting a control (untagged) image leaves signal proportional to perfusion. No contrast injection. **Status: NOT in this vault's protocols** — it appears only as a named alternative in the Diamox cerebrovascular-reserve discussion — so this entry is reference knowledge.

**Contrast & good for —** Quantitative cerebral blood flow (CBF, mL/100 g/min) without gadolinium: stroke/perfusion assessment, moyamoya, dementia workup, tumor perfusion in patients with renal failure, and the very population the Diamox protocol serves when contrast is contraindicated.

- **Physics deep-dive — labeling, waiting, and subtracting.**

    - **Labeling.** A spatially selective inversion (or saturation) pulse is applied to arterial blood *upstream* of the imaging slab — typically the neck (pCASL, the current standard: a long train of small pulses, "pseudo-continuous," labels a thick column of flowing blood over ~1–2 s). The labeled blood is now magnetically distinguishable: it has been inverted while everything in the imaging slab has not.

    - **The wait (label delay / PLD or TI).** The scanner waits while labeled blood travels through the arterial tree into the capillaries — typically **PLD ~1.5–2 s** (longer for slow flow/older patients — but too long and the label decays: T1 of blood ~1.6 s @3T washes the tag out with a time constant of T1, so the achievable SNR is fundamentally T1-limited).

    - **The subtraction.** A second acquisition without labeling (control) is otherwise identical — same T1, same coils, same static tissue. Subtract: everything static cancels, and only the labeled blood that *arrived during the delay* remains → signal ∝ CBF:

      ```
      ΔM = 2 · M₀_blood · f · T1 · e^(−PLD/T1) · (tissue delivery terms)      f = CBF
      ```

    - Quantification needs the equilibrium blood magnetization M₀ (a separate calibration image) and knowledge of the arterial transit time — the reason ASL reports absolute CBF while DSC (file 04) usually reports relative values. The whole acquisition is repeated many times and averaged: each label–control pair yields a weak signal (~1% of M₀), so 3–5 minutes of averaging is normal.

    - **Why not just use it everywhere DSC is used?** ASL is non-invasive and repeatable (no bolus timing, no preload, no leakage correction — the DSC T1-leakage problem of file 04 simply does not exist), but it is SNR-poor, sensitive to *arterial transit time* (in slow-collateral disease the tag may not arrive within the delay → false low CBF in tissue that is actually perfused — exactly the population the Diamox study targets!), and has lower spatial resolution than DSC. The two are complementary: DSC for tumor hemodynamics, ASL where contrast is unwanted or repeatability matters.

**Tunable choices —** (label duration, PLD/TI, labeling scheme pCASL vs PAS, averages — the field is evolving; these are pending vendor-specific implementations.)

**Artifacts & pitfalls —** Transit-time artifact (slow flow → tag arrives late → false low CBF — use longer PLD); motion between label/control pairs; the label *inverts* — any static tissue accidentally labeled (e.g. by imperfect labeling-plane geometry) appears as a bright artifact; low SNR (averaging is the only real cure); field-strength dependence (3T is markedly better: longer blood T1 and higher SNR).

**In this vault —** Not yet implemented; named in the Diamox protocol as the alternative perfusion method when contrast is contraindicated. File this entry under reference knowledge.

---

## Key sources — mriquestions/Radiopaedia MRS methodological consensus (europepmc 7179569); Siemens Healthineers: 3D CSI option, syngo MR Spectro; MRS consensus papers (water/lipid suppression PMC8569948); ASL: Alsop et al. consensus (MRM 2015), Radiopaedia ASL.

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — MRS + ASL entries |
