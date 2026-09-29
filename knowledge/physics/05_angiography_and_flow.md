# Angiography & Flow

**Version:** 1.0 | **Date:** 2026-09-08

Everything in this file makes **blood (or fluid) the contrast agent** instead of tissue. The four ways MRI sees vessels:

1. **Time of flight (TOF)** — flowing blood is *unsaturated* and therefore bright against saturated static tissue.
2. **Phase contrast (PC)** — moving spins accumulate phase in a bipolar gradient; the phase measures velocity.
3. **Contrast-enhanced (CE-MRA)** — gadolinium makes blood T1-short → bright on a T1 sequence, with the whole game being *k-space timing* (catch the arterial phase).
4. **Bright-fluid 3D (NATIVE, and the hydrography cousins MRCP/MRU)** — balanced steady states or heavy-T2 3D make static or slow fluid bright without contrast.

The non-trivial physics concentrates in two places: **why flowing spins look different from static ones** (TOF, PC — entry 1, 2) and **why the timing of k-space center decides a CE-MRA's quality** (entry 3). Both repay careful reading.

Values throughout are recommended typical ranges — your protocols win where they conflict.

---

## 1. TOF — Time-of-Flight MRA

**What it is —** A fast spoiled GRE (2D or 3D) with *short TR*, run so that static tissue saturates while **fresh blood flowing into the slab stays unsaturated and bright**. Tokens: `TOF_3D_multi-slab`, `TOF_fl3d`, with CS variants.

**Contrast & good for —** Non-contrast arterial anatomy: circle of Willis, carotid bifurcations, and (with care) distal vessels. The vault's neurovascular and radiosurgery work uses 3D TOF as the standard non-invasive angiogram.

- **Physics deep-dive — the inflow effect, from the ground up.**

    - A GRE with short TR and moderate flip angle (see file 03, entry 1) drives *stationary* spins toward a steady state with little signal: each pulse tips the recovered magnetization, and with short TR there is little recovery between pulses — they are **saturated** (dark). Now consider blood: it spends only a short time inside the imaging slab before flowing out. A blood spin that entered the slab *after* the previous pulse arrives **fully relaxed** (unsaturated, full M₀). The next RF pulse tips it, and it emits maximum signal — **inflow enhancement**. Contrast law:

      ```
      Arterial signal  ∝ (1 − e^(−TR/T1_blood)) × (freshness: how much unsaturated blood entered per TR)
      Static tissue    → saturated toward zero
      ```

    - This is why TOF is a *T1- and flow-dependent* sequence and why it has characteristic failure modes: **slow flow** (spins sit in the slab long enough to become saturated → distal small vessels and slow collaterals disappear — worst in-plane flow, where blood travels *along* the slice rather than through it); and **turbulence** at stenoses (random motion in the readout gradients dephases signal — a dark gap that mimics occlusion).

    - The 3D version needs one more trick. A 3D slab is thick; blood crossing a *large* slab spends many TRs inside it and saturates before reaching the distal end — the very vessels you want to see. Two countermeasures, both used in your vault protocols:

    - **Multiple thin slabs (MOTSA)** — several overlapping thin 3D slabs instead of one thick one; blood re-enters unsaturated at each slab. The overlap regions are re-measured; the scanner keeps the best center partitions, avoiding the "venetian-blind" banding at slab boundaries.
    - **TONE (ramped flip angles)** — the flip angle *increases along the flow direction* (e.g. 20°→40° into the slab): proximal spins see small angles (stay fresh), distal spins see larger angles (their partially saturated magnetization is tipped harder) — flattening the signal along the slab.

    - And the venous problem: in the circle of Willis, venous blood flows *out of* the imaging volume toward the jugulars — but inflow enhancement works for any fresh blood entering the slab, including veins at the slab's far edge. A **traveling saturation band** placed on the venous side (superior, for the circle of Willis) pre-saturates that blood before it enters — killing venous signal.

    - Display is by **MIP** (maximum intensity projection): the brightest voxel along each ray — which, in a saturated-background angiogram, is the vessel lumen.

**Tunable choices —**

*Contrast & flow*

| Knob | Typical value | Turning it… |
|---|---|---|
| TR / TE | TR 20–25 ms; TE shortest (~3–4 ms) | Short TR saturates background harder but saturates slow blood sooner; shortest TE reduces turbulence dephasing |
| Flip angle | ~20° (15–25°) | Higher = more background saturation + more inflow saturation — a balance |
| Slabs (MOTSA) | multiple thin slabs, 25–50% overlap | Thinner slabs = fresher blood; more overlap = longer scan |
| TONE ramp | ~20–40% ramp for 1–2 slabs | Flattens signal along the slab for distal vessels |
| Traveling saturation band | superior to slab (arterial circle) | Kills venous inflow |
| Voxel | 0.5–0.8 mm | Small vessels need small voxels; SNR is the limit |

*Speed*

| Knob | Typical value | Turning it… |
|---|---|---|
| CS / GRAPPA | cs factor or p2 | Time cut; CS-TOF in the vault's planning protocols |

**Artifacts & pitfalls —** Slow-flow saturation (missed distal/slow vessels — the #1 false negative); turbulent dephasing at stenoses (false *occlusion*); venetian-blind banding if MOTSA overlap is wrong; in-plane flow vessels vanish (flow parallel to the slice — angulate slices perpendicular to the vessel); background fat can stay bright (fat suppression helps); patient motion ruins the MIP before it ruins the source.

**Used in this vault —** 3D TOF of the circle of Willis (multi-slab) in the neurovascular and radiosurgery protocols; post-coiling follow-up (FLASH-3D TOF); compressed-sensing TOF in planning variants. Time-of-flight is the non-contrast workhorse of the head; the renal/abdominal non-contrast work uses NATIVE instead (entry 4).

---

## 2. Phase-Contrast Flow (PC)

**What it is —** A GRE sequence in which a **bipolar gradient pair** makes moving spins accumulate a phase proportional to their velocity; two interleaved acquisitions (flow-encoded + flow-compensated reference) are subtracted so that only *velocity-dependent* phase remains.

**Contrast & good for —** Two jobs. **Flow quantification:** through-plane PC measures velocity across a vessel and integrates it — mL/s, net flow per beat, regurgitant fraction, shunt ratio, CSF flow. **Non-contrast angiography:** the velocity map is inherently vessel-only — stationary tissue contributes zero phase — so the 3D speed map MIP-renders into a complete vessel tree (rotational PC MRA), and the low-VENC version is a common non-contrast **MRV** (dural sinuses, slow flow); because the map is signed, it also shows flow *direction*, which magnitude-only TOF cannot.

- **Physics deep-dive — how a gradient measures velocity, and what VENC means.**

    - **The complete sequence, in one TR.** PC is an ordinary gradient echo with one extra ingredient — the bipolar pair — and it is run twice: once flow-encoded, once flow-compensated:

      ```
      Acq A — flow-encoded:

      RF:      ▄▀▄
      Gss:     ▄▀▄   ▄▄▄▄▄▄  █▄▄▄▄▄▄
               exc  └──bipolar──┘
      Gpe:         ▁
      Gro:                 ▄▀ ▁▂▃▄▅▆▇
      echo:                   ▁▂▃▄▅▆▇█

      Acq B — flow-compensated:

      RF:      ▄▀▄
      Gss:     ▄▀▄   (balanced — no velocity sensitivity)
      Gpe:         ▁
      Gro:                 ▄▀ ▁▂▃▄▅▆▇
      echo:                   ▁▂▃▄▅▆▇█

      reconstruct both → two complex images → subtract phases → velocity map
      ```

    - **Two kinds of phase — a slope the FT measures, and an offset it passes through.** Every gradient stamps phase; the difference is whether the phase *grows along k*. k itself is the trajectory's position-sensitivity setting (the running gradient total, γ·∫G dt); the imaging gradients (phase-encode blips, readout) give each voxel a phase that grows with k at a rate set by its position:

      ```
      imaging: φ(k) = k · x
      (phase GROWS along k — the FT measures the slope, and
      that slope is the position: the "frequency" in k-space)
      ```

      The bipolar is a gradient too, but a round trip: its equal-opposite lobes stamp +k₀·x then −k₀·x — exact cancellation for a stationary spin, while a moving spin receives the stamps at different places and keeps only the residue:
      
      ```
      stationary:  +k₀·x − k₀·x = 0        
      moving:  k₀·(x₁ − x₂) = γ·M₁·v
      ```

      What survives is a **fixed offset**, φ = γ·M₁·v — no k, zero slope along k, which the FT passes through as the pixel's phase.

    - **How the phase is recovered — subtraction as complex division.** The receiver records two quadrature channels, so every pixel reconstructs as a complex number z = m·e^(iφ): its magnitude is the anatomy, its angle atan2(Q, I) is the phase. The subtraction happens pixel by pixel, as a **complex division** of the two images:

      ```
      z_A / z_B  =  m·e^(i·(φ_bg + φ_v)) / m·e^(i·φ_bg)  =  e^(i·φ_v)

      Δφ  =  angle(z_A) − angle(z_B)  =  φ_v  =  γ · M₁ · v
      ```

      Dividing complex values divides the magnitudes — which are identical (both acquisitions show the same anatomy), so they cancel to 1 — and **subtracts the angles**. Everything the two acquisitions share (B₀, eddy currents, coil, geometry) sits in φ_bg and vanishes; only the velocity phase survives. The scanner calibrates the pair so a chosen velocity, **VENC**, produces exactly 180° of phase:

      ```
      v = (VENC / π) · Δφ
      ```

      The background suppresses itself: stationary tissue divides out to zero phase, so phase-contrast is inherently background-free — its "contrast" is pure velocity. (The wrap back into ±180° is exactly where VENC aliasing will live.)

    - **The VENC rule.** Choose VENC just above the fastest expected velocity: too low, fast spins wrap past ±180° (**aliasing** — the lumen flips direction mid-systole, like a clock hand passing 12); too high, all velocities produce small phases while velocity noise scales as VENC (velocity SNR ∝ v/VENC).

    - **The three geometries — what the encoding axis does to the image.**

        - **2D through-plane.** The slice cuts the vessel in cross-section; the bipolar runs along the slice axis. Every lumen pixel carries the through-plane velocity, so the vessel appears as a **uniform direction-coded disk** — toward-viewer bright, away dark — and stationary tissue sits at gray. This is the quantitative mode: integrate the disk per phase → flow curve → mL/beat.

        - **2D in-plane.** The vessel lies within the slice; the bipolar runs along the read or phase axis. The vessel appears **bright along one encoded direction and dark along the opposite** — flow direction at a glance — but vessels running perpendicular to the encoded axis carry no velocity component along it and vanish, and pixels mix vessel with wall, so nothing can be quantified.

        - **3D.** The acquisition is a slab with two phase-encode axes — a volume, not a slice; that is *spatial* encoding, and the velocity encoding is a separate choice. With a **single encoding axis**, only that one flow component is measured and perpendicular vessels drop out. The complete vessel tree needs **three-direction encoding (the 4-point method)** — the bipolar run along x, y, and z, plus one compensated reference, four acquisitions per phase — giving every voxel the full velocity vector; its **speed** √(vₓ²+v_y²+v_z²) is independent of vessel orientation, so all vessels render bright in MIP projections, rotating in space. Lowering VENC to venous speeds aliases the fast arterial flow into incoherence — the same volume becomes an **MRV**.

    - **Cine-PC.** The identical bipolar pair is fired repeatedly, each repetition landing at a different part of the cardiac cycle; the ECG stamp sorts the repetitions into phase bins (segmented, retrospective gating — file 06), so every point of the cardiac cycle gets its own velocity map and the flow curve spans systole to diastole; temporal resolution = 2 × TR × views-per-segment.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| VENC | arterial ~150 (aorta 130–200; step-up 400 for stenosis); venous ~10–20 (MRV); CSF 5–15 | The master knob — aliasing vs velocity noise (above) |
| Encoding direction | through-plane (quantify) vs in-plane (visualize) | What the measurement means |
| Temporal resolution | TR × views-per-segment (~30–60 ms) — cardiac-gated cine only | Finer = better flow curve, longer scan |
| Reference strategy | interleaved flow-encoded + compensated | The subtraction that removes background |

**Artifacts & pitfalls —** Aliasing (see above — if the aorta shows inverted velocities in systole, reacquire at higher VENC); partial-volume at the vessel wall (contours placed too generously include slow edge flow); through-plane motion of the vessel itself; eddy-current offsets (background phase must be subtracted with static-tissue correction); turbulent flow at stenoses has *random* phase — it dephases, and the measurement underestimates true velocity there.

**Used in this vault —** Aortic flow (VENC 150, with step-up to 400 available for high-velocity jets) in the cardiac protocols — full context in file 06. The same physics quantifies CSF flow where implemented in neuro protocols.

---

## 3. CE-MRA — Contrast-Enhanced MRA

**What it is —** A 3D T1-weighted spoiled GRE run *during* the arterial phase of a gadolinium bolus: contrast shortens blood T1 (~1200 → ~100 ms) so the arterial lumen is maximally bright while the background stays dark, and the scan is timed so that **k-space center is sampled exactly while the arteries are brightest**. Tokens: `angio3d_cor_*` with the Care Bolus / Test Bolus pairs that time it.

**Contrast & good for —** High-resolution arterial anatomy where TOF cannot reach or would take too long: renal arteries (with breath-hold and/or respiratory triggering), carotids, aortogram, run-off — and, in the vault, delayed-phase excretory urography after contrast.

- **Physics deep-dive — why CE-MRA is a timing problem, and which ordering to pick.**

    - Contrast makes blood bright easily. The difficulty is that the bolus passes: arteries peak, then veins light up ~5–10 s later, and once the *veins* are bright the arterial image is ruined (overlap). Since a 3D CE-MRA takes ~20 s to acquire, you cannot simply "scan during the arterial phase" — you must decide **which seconds of k-space get the arterial phase**, and the answer is the center:

      ```
      k-space center  →  image contrast (brightness of arteries)
      k-space edges   →  sharpness only
      ```

    - So the acquisition order matters more than the scan time:

    - **Centric / elliptical-centric ordering** (center sampled first) — the arterial phase is captured in the first ~1–3 s; the rest of the scan fills the edges, which can safely happen while veins are bright (they add detail, not brightness). That is why centric tolerates a slow scan and a late trigger; its one fatal direction is starting too early — center before arrival → Maki artifact (below). Breath-hold failure is destructive only at the start. This is the ordering of every first-pass arterial phase (renal, carotid, arch, runoff).

    - **Linear ordering** (center mid-scan, at ~T_acq/2) — the image contrast becomes the average of the whole scan, so the arterial peak must land mid-scan and the bolus must last the entire acquisition; timing errors are tight in both directions, and veins brighten the center too — full venous contamination. Breath-hold failure is destructive whenever the center is due. It survives only where the contrast has stopped moving: the venous/delayed second pass (confirming filling defects, venous anatomy), the 2/5/10/15-minute excretory phases, equilibrium-phase MRV.

    - The general rule: **transient signal state → centric (grab it early); stable signal state → linear (average it)** — ordering only matters while the bolus is moving; on a plateau it stops being a physics decision.

- **Physics deep-dive — bolus timing: the two tools and the delay equation.**

    - The bolus is a **slug, not a spike**: its front arrives at the vessel and its concentration peaks halfway through the slug's own length. All timing math reduces to putting k-space center on that peak. The vault's protocols use both Siemens tools:

    - **Care Bolus** — a real-time 2D monitoring acquisition (one image per second) at the target vessel; the diagnostic 3D **starts when the bolus is seen** (auto-threshold on an ROI, or the radiographer triggers by eye). One injection, no math, and it adapts to the patient's actual circulation — the default whenever a monitorable vessel exists. Its forgiveness is arithmetic, not luck: triggering at arrival costs ~3–4 s of breath-hold command + sequence start, then ~2 s more to k-space center, which lands the center at arrival + ~5 s ≈ arrival + T_inj/2 ≈ **the peak** (for a typical 10-s injection) — the latencies cancel against the slug's half-length. Costs: someone must watch, and the vessel must be large enough to monitor.

    - **Test Bolus** — a tiny (1–2 mL) pre-injection at the diagnostic rate runs a single-slice dynamic series at the vessel; the measured curve gives the time-to-peak T_p, and the diagnostic scan starts at a calculated delay:

      ```
      delay = T_p + (V_inj / R) / 2 − T_center

      T_p       = time-to-peak of the test bolus ≈ arrival time of the full bolus's front (the test slug is ~1 s long, so its peak marks the front)
      V_inj / R = diagnostic injection volume ÷ rate = the injection duration T_inj (20 mL at 2 mL/s → 10 s); the slug peaks halfway through its own arrival, hence the ÷ 2
      T_center  = time from scan start to k-space center, set by the ordering: ~1–3 s with elliptical-centric (center first), ≈ half the scan with linear
      ```

    - In plain words: the test slug is so short that its peak marks the *arrival* of the front; the full slug peaks later, halfway through its own injection; and T_center is subtracted so the scan starts that much before the target — k-space center lands on the peak. (The formula is a starting point: a full bolus travels a little faster than a 1 mL test spike, so the real peak may run a few seconds early — the arterial plateau absorbs the error.)

    - **Started too early → Maki artifact**: k-space center sampled before the bolus arrives — edges sharp, center dark — a bright ring that mimics vessel narrowing. **Started too late** → venous contamination (jugulars/renal veins overlap the arteries on MIPs). Both are the price of mistiming; the whole toolset above exists to avoid them.

**The injection & sequence design —**

- **Injection —** right arm (antecubital vein — shortest path to the arch). Left arm is a fallback, not an error: the left brachiocephalic vein crosses the anterior mediastinum directly over the arch-vessel origins, so dense venous contrast overlies the region of interest in arch/carotid studies — obscuring or mimicking origin lesions; fields below the thorax are unaffected, and a saline flush washes the vein out quickly.
- **Sequence —** the base is a **3D spoiled GRE (FLASH, file 03)**: shortest TR/TE, flip angle ~25–40°, thin partitions, breath-hold where possible, and fat suppression or subtraction for background. MIP display follows the acquisition.

**By territory —** arrival times are orders of magnitude, not constants — cardiac output, age and disease move them by tens of seconds:

- **Aorta**
    - **Slab —** coronal, oblique along the arch; whole aorta: one long sagittal-oblique slab if a single breath-hold covers the run, otherwise a two-station moving-table bolus chase (thorax → abdomen)
    - **Cover —** arch study: ascending aorta → proximal descending, all great-vessel origins included (an origin stenosis is the classic missed lesion); whole aorta: arch → iliac bifurcation
    - **Monitor —** transverse, through the ascending aorta at the arch
    - **Timing —** arrival 10–20 s; breath-hold commanded just before the trigger (the thoracic aorta moves with the diaphragm); too late and the SVC/azygos brighten over the arch. Chase: trigger once — station 2's timing is station 1 + the table move (the bolus travels meanwhile), centric ordering absorbing the error; outrunning the bolus gives an empty station 2, lagging gives venous contamination. Trap: aneurysm sacs fill slowly and swirl — incomplete filling on the arterial phase is physiology, not a dissection flap (add a delayed phase when sac morphology matters).

- **Pulmonary**
    - **Slab —** coronal
    - **Cover —** pulmonary trunk → hilar branches
    - **Monitor —** transverse, through the pulmonary trunk
    - **Timing —** arrival 4–8 s — the fastest, tightest window, compounded by breath and cardiac motion

- **Renal**
    - **Slab —** coronal, oblique along the aorta
    - **Cover —** above the celiac origin → distal renal arteries — long enough for accessory renals (donor work's classic miss: a lower-pole accessory near the iliac level)
    - **Monitor —** transverse, at the celiac/renal level; the vault's practice: visual Care Bolus through the renal arteries, or a Test Bolus at the descending aorta above the origins
    - **Timing —** arrival 15–25 s; renal veins + IVC light up ~7–10 s after the peak — the breath-hold and the small T_center keep the window

- **Runoff (periphery)**
    - **Slab —** coronal stations — aortoiliac → thigh → calf (moving table for the chase)
    - **Cover —** aorta → ankles, three stations
    - **Monitor —** Care Bolus at the distal aorta (chase trigger); a Test Bolus at the popliteal for calf-specific timing
    - **Timing —** calf arrival 30–60+ s, highly variable and often asymmetric in PAD. Three strategies: (1) **bolus chase** — ~7–15 s per station; risks: outrunning the slow leg, venous contamination at the calf, motion between mask and contrast (immobilize the legs); (2) **dual injection** — a second half-dose timed to the calf via the popliteal test bolus; (3) **TWIST at the calf** — no timing at all (entry 5). (No runoff protocol in the vault yet — this block is general knowledge.)

**Tunable choices —**

*Timing*

| Knob | Typical value | Turning it… |
|---|---|---|
| Trigger | Care Bolus (auto/visual threshold) vs Test Bolus (calculated delay) | One injection and no math vs a measured delay — test bolus costs ~2 mL extra contrast and setup time |
| k-space ordering | centric (arterial) vs linear (plateau phases) | Sets T_center — the tolerance against mistiming (choice rule above) |
| Delay | T_p + (V_inj/R)/2 − T_center | The number that makes or breaks the study (decoded above) |

*Acquisition*

| Knob | Typical value | Turning it… |
|---|---|---|
| TR/TE/FA | TR ~3.8–4.4 ms; TE ~1.3–1.6; FA ~25° | Shortest-TR T1 GRE — see file 03 |
| Partitions / voxel | thin (≤1.5 mm) for MIP quality | Resolution = SNR = acquisition time |
| Breath-hold vs trigger | BH (renal/carotid) or respiratory-triggered | Motion management per territory (file 08) |
| Phases | arterial, then venous/delayed as needed | The vault's excretory phases 2/5/10/15 min after the angio |

**Artifacts & pitfalls —** Maki artifact (started too early); venous contamination (started too late, or slow scan with linear ordering); patient motion between bolus tracking and scan; breathing during the acquisition (→ triggering); background enhancement on delayed phases (interstitial contrast — fine for urography, bad for arteries); contrast dose and injection rate directly set the width of the arterial window.

**Used in this vault —** Renal and carotid CE-MRA (Care Bolus / Test Bolus pairs per protocol), and the same 3D GRE platform run as delayed *excretory urography* (2/5/10/15-minute phases) in the MR-urography protocols — a good reminder that "the sequence" doesn't know what phase of contrast you are imaging; the *timing* defines the study.

---

## 4. NATIVE — Non-Contrast MRA (TrueFISP)

**What it is —** Siemens' non-contrast angiographic family: **NATIVE TrueFISP** uses ECG-triggered 3D balanced SSFP with a spatially selective inversion pulse — fresh arterial blood enters bright while the surrounding static tissue is nulled by the inversion. Tokens: `native_truefisp_resp_trig_tra`, `native_truefisp_nav_ECG_tra`. (NATIVE SPACE, the peripheral systolic/diastolic subtraction variant, exists as a product but is not in this vault.)

**Contrast & good for —** **Renal arteries** and other abdominal/neck vessels *without gadolinium* — the protocol of choice when contrast is contraindicated (severe renal failure, NSF risk, pregnancy). Compared with TOF it tolerates slow flow far better (the nulling does not depend on the blood saturating) and it is a true 3D bright-blood technique.

- **Physics deep-dive — the three ingredients and why each is there.**

    - NATIVE TrueFISP combines three mechanisms, each solving a problem the others cannot:

    - 1. **3D balanced SSFP readout** (file 03, entry 4) — bright blood by T2/T1 in laminar flow, with the short-TR robustness that TrueFISP gives. But on its own it shows *veins as brightly as arteries* and all the static fluid too.
    - 2. **Spatially selective inversion pulse** — a thick slab is inverted (including the target vessel); during the wait **TI (~250–1200 ms)** the inverted static tissue recovers toward zero — and the readout occurs when it is nulled. Blood that *flows into the slab after the inversion* was never inverted → full signal. This is the same inflow logic as TOF, but the background suppression comes from **T1 nulling, not saturation** — so it works for slower flow than TOF (blood needs only to traverse the distance between the inversion slab edge and the imaging slab within TI, not to survive a short-TR saturation regime).
    - 3. **ECG triggering + respiratory gating** — the acquisition is timed to **diastole** (maximal arterial inflow, minimal pulsatile motion) and gated to the respiratory cycle via a **navigator on the right diaphragm dome (PACE acceptance ±3 mm)** — free-breathing but frozen at end-expiration.

    - The contrast direction is set by the *order of the two slabs*: invert upstream of the imaging volume and inflowing arterial blood (which comes from upstream) is bright; veins flowing the other way were inverted too and stay dark at their null time. Fat is suppressed spectrally (SPAIR-class) because fat's T1 is close to the null regime and would otherwise stay bright.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| TI | 250–1200 ms (inflow-dependent) | Longer = more inflow time, more T1 recovery of background — a balance set by flow speed |
| Trigger | ECG, diastolic window | Brightest inflow, least motion |
| Respiratory gate | navigator ±3 mm (PACE) | Free-breathing sharpness |
| Flip angle / TR | ~90°; shortest TR | TrueFISP regime (file 03) |
| Fat suppression | SPAIR-class | Keeps fat out of the null window |

**Artifacts & pitfalls —** Navigator failure (irregular breathing → prolonged scan, blur); arrhythmia perturbs the diastolic timing; slow or turbulent flow still dephases (TrueFISP turbulence); the technique is territory-specific — it shines for renal arteries, less so for tortuous distal vessels; TI must be re-tuned if the protocol moves between 1.5T and 3T (T1 changes).

**Used in this vault —** Renal non-contrast MRA (respiratory-triggered and navigator-ECG variants) for patients with contraindicated contrast — e.g. impaired renal function.

---

## 5. Time-Resolved TWIST MRA/MRV

**What it is —** The angiography application of TWIST view-sharing (physics in file 03, entry 9): rapid repeated 3D frames (~1–3 s) capturing contrast arriving, filling arteries, then veins — no bolus timing required because *every* phase is captured. Tokens: `TWIST_*` cerebral/head/neck/pelvis.

**Contrast & good for —** Studies where *dynamics* are the diagnosis: AVMs and dural fistulas (arterial feeders → nidus → venous drainage timing), cerebral venous studies, pelvic congestion (May-Thurner), gonadal-vein localization in cryptorchidism work. Also the rescue when a single-phase CE-MRA cannot be timed reliably — unknown or highly variable circulation (PAD calf, pulmonary, restless patients) — at the cost of spatial resolution versus a dedicated high-res CE-MRA (entry 3).

**Physics — the file-03 story in one paragraph.** Each frame re-measures only the central ~15–30% of k-space (region A — where the contrast lives) and reuses the periphery from adjacent frames (region B — where the anatomy lives). Frame time drops to ~1–3 s. The diagnostic content is a *movie* of contrast phases; the caveat is that the periphery lags one frame, so anything moving fast (patient motion, peristalsis) ghosts.

**Tunable choices —** (region A/B sizes, frame interval, GRAPPA combination — file 03, entry 9) plus display by subtraction/MIP of selected frames.

**Artifacts & pitfalls —** Ghosting with motion across shared frames; frame rate insufficient for true arteriovenous timing (artery and vein both bright in one frame → cannot separate); lower spatial resolution than a dedicated high-res CE-MRA.

**Used in this vault —** Cerebral AVM and MRV (head, ePAT), facial AVM dynamics, EC/IC bypass flow, pelvic MRV for congestion/May-Thurner, and gonadal-vein tracking in undescended-testis protocols.

---

## 6. Hydrography — MRCP · MRU · Myelography · Sialography

**What it is —** Not one sequence but a *clinical application class* built on the heavy-T2 sequences of file 02 (3D SPACE or thin-slab HASTE): static fluid (bile, urine, CSF, saliva) is maximally bright and everything else dark — an "MR photograph of the fluid column." Tokens: `t2_space_*_MRCP/ERCP/MRU`, `t2_haste_*_thin_slab_*`.

**Contrast & good for —**

| Application | Fluid | Question |
|---|---|---|
| MRCP | bile | Stones, strictures, ductal anatomy, ERCP planning |
| MR urography | urine | Obstruction level, hydronephrosis, post-transplant |
| MR myelography | CSF | Root sleeve avulsions, CSF leak |
| MR sialography | saliva | Duct stones/strictures (e.g. Sjögren) |

**Physics — why heavy T2 sees fluid and nothing else.** With TR effectively infinite and TE ~ 600–1000 ms (3D SPACE) or ~60–100 ms effective in thin-slab HASTE, signal = S₀·e^(−TE/T2): only *very long-T2* substances survive — static fluid (T2 = seconds) is bright; parenchyma (T2 ~ 50–100 ms) has fully decayed; blood (flowing or short-T2) is dark. Static-fluid imaging therefore needs no contrast and no subtraction — the contrast is the T2 filter itself. Two acquisition styles, each with a purpose:

- **3D SPACE slab** — one isotropic heavy-T2 volume covering the ducts; reconstructed as **MIPs in any plane** (and thin-slice source for problem-solving). Respiratory-triggered for the biliary tree (the ducts move with breathing).
- **Thin-slab 2D HASTE projections** — a single thick slab (~20–40 mm) positioned along the duct, acquired in a breath-hold: the "projection MRCP" that resolves overlapping ducts and stones against the background of the 3D volume. (Coronal oblique along the biliary axis, sagittal oblique variants in the vault.)

Fluid motion is the enemy of both: *flowing* fluid (e.g. urine jets from the ureteric orifices, bowel content) dephases and can mimic filling defects — which is why the protocols sometimes add an anti-peristaltic agent for the bowel and why "static" is the operative word.

**Tunable choices —**

| Knob | Typical value | Turning it… |
|---|---|---|
| TE / effective TE | 3D SPACE very long; HASTE 60–100 ms eff. | Heavier T2 = cleaner fluid, longer scan/blur |
| Respiratory control | trigger (3D) vs breath-hold (thin slab) | Both exist in the vault — see above |
| Slab orientation & thickness | along the duct of interest | Oblique coronal for biliary; sagittal for the distal ureter |
| Fat suppression | none (fluid only) or FS for duct-in-fat work | Pure-fluid imaging usually runs without it |

**Artifacts & pitfalls —** Flow voids mimicking stones (urine jets, bile flow — compare adjacent slabs); bowel overlap (suppress motility); breathing blur on the 3D volume (trigger); stones below resolution or impacted at the ampulla (thin-slab HASTE + source images beat MIP alone — always read the source); metal (stents, clips) voids.

**Used in this vault —** MRCP as both 3D triggered volume and breath-hold thin-slab projections (including the ERCP-planning variant); MR urography as triggered isotropic 3D plus the delayed-phase contrast series (entry 3); MR myelography (sagittal, fat-suppressed); MR sialography (oblique, fat-suppressed) for duct pathology.

---

## Family summary

| Technique | Blood contrast mechanism | Needs contrast? | Quantifies? | Weakness |
|---|---|---|---|---|
| TOF | inflow (unsaturated blood) | no | no | slow flow, turbulence |
| Phase contrast | velocity phase (bipolar gradients) | no | **yes** (velocity/flow) | VENC tuning, turbulence |
| CE-MRA | T1 shortening of blood | yes | no | timing (k-space center) |
| NATIVE TrueFISP | inversion-null + balanced SSFP inflow | no | no | navigator/ECG dependence |
| TWIST MRA | T1 + view-sharing dynamics | yes | no | spatial resolution, ghosts |
| Hydrography | heavy-T2 static fluid | no | no | fluid *motion* mimics disease |

---

**Key sources** — Siemens Healthineers (syngo NATIVE; Care Bolus; TWIST brochure; MAGNETOM World MRCP/MRU protocols); mriquestions.com: [TOF MRA](https://www.s.mriquestions.com/time-of-flight-mra.html), [MOTSA](https://www.s.mriquestions.com/motsa.html), [VENC](https://ratio.mriquestions.com/what-is-venc.html), [view ordering in MRA](https://ww.mriquestions.com/view-ordering-in-mra.html), [timing the bolus](https://ratio.mriquestions.com/timing-the-bolus.html); SCMR 2020 flow protocols (JCMR); Radiopaedia: [velocity encoding](https://radiopaedia.org/articles/velocity-encoding), [TWIST](https://radiopaedia.org/articles/twist-time-resolved-angiography-with-interleaved-stochastic-trajectories-1); papers: Lotz PC review (AJR 2002).

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — TOF/PC/CE-MRA/NATIVE/TWIST/hydrography |
