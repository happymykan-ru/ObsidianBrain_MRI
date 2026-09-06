# Cryoablation (MR-Guided Cryoablation)

**Version:** 1.0 | **Date:** 2026-09-06 | **Scanner:** [Confirm model]

---

## 1. Patient Positioning & Registration

- **Registration — always head-first supine:** regardless of the patient's physical position on the table, the exam is **always registered as head-first supine** — so the image orientation is always the same as what the radiologist sees when inserting the needle inside the bore.
- **Position:** per target organ — **prone** for kidney cryoablation, **supine** for others (e.g., endometriosis) — the registration remains head-first supine in every case
- **Coil:** **Bore coil (BC)** — the bore-integrated coil keeps the patient's skin accessible for needle work.
- **Laser Landmark:** the skin marking is done via the green lab laser — see the skin-marking procedure.

---

## 2. Procedure Overview

**What it is:** MR-guided cryoablation destroys a tumor by freezing — under image guidance, needles are placed into the tumor percutaneously, and the cryo-probes freeze it in controlled cycles. The MRI does four jobs at once: it finds and characterizes the tumor, plans the needle paths, drives the needles in under real-time imaging, and displays the **ice ball** as it forms — frozen tissue is a signal void on the images, so the ablation zone can be watched until it covers the tumor with a margin.

**Why MRI:** real-time soft-tissue contrast — the tumor and the critical structures around it stay visible while the needle advances; the ice ball is directly visible as a signal void; no ionizing radiation.

The step-by-step flow is the Workflow Overview below.

---

## 3. Workflow Overview

**The procedure flows as one chain — each phase hands the geometry to the next:**

- **Phase 0 — Localization:** HASTE (#1) finds the target
- **Phase 1 — Table reset:** the rough lesion location is set as the table isocenter → **ISO → FIX**
- **Phase 2 — Planning imaging:** HASTE (#2) + BLADE tra/sag (#3–4) ± StarVIBE in/out (#5–6, optional)
- **Phase 3 — Needle planning:** needle path(s) planned on the BLADE images → pixel lens marks the x, y, z
- **Phase 4 — Skin marking:** the coordinates transfer to the patient — out by 1002 + z → x/y at the lab laser → mark → back → laser off
- **Phase 5 — Needle insertion:** **ISO** → BEAT interactive (#7) → BLADE re-check (#8) → next needle
- **Phase 6 — Cryoablation:** freeze cycles with BLADE ice-ball monitoring (#9–11)
- **Phase 7 — Send:** BLADE tra & sag at pre / 1st / 2nd / post cryo

---

## 4. Imaging Series

### Phase 0 — Initial Localization

| # | Series | Plane | Purpose | Breathing |
|---|--------|-------|---------|-----------|
| 1 | `haste_localizer` | Axial | Initial scout — locate the target region | BH |

### Phase 1 — Table Reset

| # | Series | Action |
|---|--------|--------|
| — | **Reset table position** | Find the target lesion on #1 → reset the table position → change table mode from **ISO to FIX** |

### Phase 2 — Planning Imaging (new table position)

| # | Series | Plane | Purpose | Breathing |
|---|--------|-------|---------|-----------|
| 2 | `haste_localizer` | Axial | Localizer at the new table position | BH |
| 3 | `t2_fblade_tra_bc` | Axial | T2 BLADE axial — planning + needle-path planning | FB (motion-robust) |
| 4 | `t2_fblade_sag_bc` | Sagittal | T2 BLADE sagittal — planning + needle-path planning | FB (motion-robust) |
| 5 | `t1_starvibe_tra_in-phase_bc` | Axial | T1 StarVIBE in-phase — optional, when indicated | FB |
| 6 | `t1_starvibe_tra_out-phase_bc` | Axial | T1 StarVIBE out-phase — optional, when indicated | FB |

### Phase 3 — Needle Planning

| # | Series | Action |
|---|--------|--------|
| — | **Pixel lens** | The radiologist plans the needle insertion on the BLADE images (#3–4) and uses the pixel lens to mark the position (x, y, z) of the needle insertion site |

### Phase 4 — Skin Marking

| # | Series | Action |
|---|--------|--------|
| — | **Skin mark (lab laser)** | Full procedure in the skin-marking section: table out by 1002 + z → x/y at the lab laser → skin mark → table back by the same amount → laser off |

### Phase 5 — Needle Insertion

| # | Series | Plane | Purpose | Breathing |
|---|--------|-------|---------|-----------|
| 7 | `beat_interactive` | 3 slices, 2 planes / 2 slices, 1 plane | Real-time interactive guidance during puncture — preset selected per radiologist requirement | — |
| 8 | `t2_fblade_tra_bc` + `t2_fblade_sag_bc` | Ax + Sag | Re-check after each needle insertion — then re-insert the next needle under BEAT interactive | FB |

### Phase 6 — Cryoablation

| # | Series | Plane | Purpose | Breathing |
|---|--------|-------|---------|-----------|
| 9 | `t2_fblade_tra_bc` + `t2_fblade_sag_bc` | Ax + Sag | 1st cryoablation — ice ball monitoring | FB |
| 10 | `t2_fblade_tra_bc` + `t2_fblade_sag_bc` | Ax + Sag | 2nd cryoablation — ice ball monitoring | FB |
| 11 | `t2_fblade_tra_bc` + `t2_fblade_sag_bc` | Ax + Sag | Post cryoablation | FB |

### Phase 7 — Send

- The final sequences to send: `t2_fblade_tra_bc` + `t2_fblade_sag_bc` at **pre** (#3–4), **1st cryoablation** (#9), **2nd cryoablation** (#10), **post cryoablation** (#11).

---

## 5. Skin Marking Procedure (Lab Laser)

1. **Pixel lens coordinates:** the radiologist marks the needle insertion site on the console and reads off its position (x, y, z) — the z is the table coordinate, **H(+ve) = head-ward, F(−ve) = foot-ward** of the red-laser isocenter.
2. **Laser geometry:** the distance from the red (internal) laser to the green **lab laser** = **1002** mm of table movement (centre → lab laser).
3. **The principle:** move the table out by **1002 + the z coordinate** — the lab laser's z (= 0) then corresponds exactly to the z of the MR-imaged lesion. *Example: needle site at **H50** → 1002 + 50 = **1052** mm.*
4. **Move the table out by that amount** — toward the lab laser.
5. At the lab laser, enter the **x and y** offsets — **+x = right, −x = left** — and mark the skin there.
6. **Move the table back inward by the same amount.**
7. **Turn the laser off** — a switched-on laser causes image artifact. The table stays in **FIX** mode for the skin-marking procedure.

---

## 6. Sequence Rationale

**Why the bore coil:** the bore-integrated coil leaves the patient's skin exposed for the puncture — the standard anterior body-array coils would cover the needle entry site.

**`haste_localizer` (#1–2):** single-shot T2 scout — fast localization of the target for the table reset; repeated after the reset because the table geometry has changed.

**`t2_fblade_tra_bc` / `t2_fblade_sag_bc` (#3–4) — the workhorse pair:** **fastBLADE** — Siemens' accelerated redesign of BLADE (their PROPELLER — periodically rotated overlapping blades). Two roles:
    - **Planning:** the radiologist plans the needle path(s) on the axial + sagittal pair.
    - **Monitoring:** the needle and the growing ice ball are both **signal voids** — the repeated BLADE runs track each needle's position and the ice ball against the tumor margin.

**Why fastBLADE is faster — and why cryoablation is its home:**
    - **The blade anatomy:** BLADE fills k-space in rotating rectangular strips (blades) of parallel lines; each blade is one TSE echo train. Scan time = blades × TR, and the blade count needed is ≈ π × matrix / (2 × strip width) — so **wider blades = fewer blades = shorter scan**.
    - **Why standard BLADE stays slow:** within a blade, later echoes decay with T2 — a wide blade's outer lines are acquired on the dim late echoes, giving a sagging amplitude profile → blur/streaking. With fixed 180° trains the only cure is narrow blades — hence many blades and the long scan time.
    - **The fastBLADE fix:** EPG-designed variable flip-angle trains compensate the T2 decay, keeping the received signal flat across the whole train — the blade width is no longer capped by decay, so fewer blades cover k-space; the VFA trains also cut SAR, and the optimized RF/SPAIR pulses shorten each TR. Motion robustness is untouched — it comes from the rotating-blade architecture, not the flip angles.
    - **Why it is rare outside cryoablation:** the sequence is new and niche — diagnostic protocols either breath-hold (standard TSE) or grab speed (HASTE / DL reconstruction), so BLADE-family demand is small. Cryoablation is the one workflow with no substitute: the patient is free-breathing and moving, and the repeated re-checks (#8) and ice-ball runs (#9–11) must be fast *and* diagnostic — the single setting where fast + motion-robust + fat-suppressed T2 must come together.

**`t1_starvibe_tra_in-phase_bc` / `t1_starvibe_tra_out-phase_bc` (#5–6) — optional chemical-shift pair:** a free-breathing 3D dataset acquired at in- and out-of-phase echo times, for when the lesion needs fat characterization:
    - **When indicated:** lipid-containing tumors — clear cell RCC (the main kidney cryo target) and adrenal adenomas — lose signal on the out-of-phase image, confirming the target identity and defining the tumor margin against the surroundings.
    - **Secondary read:** after ablation the ablation zone turns T1-bright (blood products) — the pair separates that from true fat.
    - **Rib check:** as a 3D dataset it reformats along the planned needle trajectory, so ribs lying in the puncture path are seen and avoided at planning.

**`beat_interactive` (#7) — real-time needle guidance:** **BEAT IRTTT** — Siemens' interactive real-time imaging mode for interventions: a continuously acquired fast gradient-echo loop (balanced SSFP) refreshes at several frames per second, and the operator repositions the imaging planes live on the fly to follow the needle — which reads as a dark susceptibility void against the bright tissue. The tip is tracked **manually by eye** as it advances. The table mode is switched back to **ISO** for the interactive phase (FIX is held through planning and skin marking). Two presets, chosen per radiologist requirement:
    - **3 slices / 2 planes:** three slice positions across two orthogonal planes — the needle is seen from two directions at once, so its depth and oblique trajectory are unambiguous; the cost is frame rate — the per-plane update slows.
    - **2 slices / 1 plane:** two slice positions in a single plane — the fastest refresh, for tracking a rapidly advancing needle; the cost is spatial context — a needle deviating out of that plane is missed.

### Cryotherapy — the freeze cycles and the ice ball

**The ice ball — why frozen tissue is a signal void:**
    - **Freezing removes the signal source:** every pixel is fed by mobile water protons; when tissue freezes, the water crystallises and the protons lock into the ice lattice — the frozen volume simply stops being MR-visible.
    - **The T2 collapse:** relaxation in ice drops to microseconds — the transverse signal dies instantly after excitation, long before any readout — so no weighting recovers it (T1/T2/PD all read black) and the void is absolute.
    - **The margin renders crisp:** ice and liquid water differ in susceptibility, so the ice-ball boundary carries its own dark rim — the edge between the void and the unfrozen tissue stays sharp.
    - **Why this is the ideal monitor:** the dark region is not an artifact blooming around an object — it *is* the frozen tissue itself, so the void's boundary maps the ablation zone in real time as it grows. After thawing, the water re-mobilises and the signal returns — the post-cryo runs show the dead, edematous zone, no longer void.
    - **The margin pearl:** the lethal isotherm (−20 to −40 °C) sits a few millimetres **inside** the visible ice-ball edge — the outermost rim of the black ball is frozen but not necessarily dead, so the ball must cover the tumor **plus a few mm**.

**Why the freeze is repeated (freeze–thaw–freeze):** one cycle does not kill reliably — each phase kills by a different mechanism, and the protocol stacks them:
    - **Freeze:** ice forms inside the cells (lethal to their membranes) and outside them — water is drawn out of the cells by osmosis, so the cells dehydrate, shrink and tear.
    - **Thaw:** the ice melts and water floods back into the damaged, dehydrated cells — an osmotic shock on top of the mechanical damage; the injured microvessels also shut down and thrombose.
    - **Second freeze:** the already-damaged, now-ischemic tissue freezes again — intracellular ice is more extensive and the kill is completed. Two cycles make the lethal zone far more reliable than one.

**Active vs passive thaw:**
    - **Passive thaw:** the probe stops cooling and the tissue rewarms on its own from surrounding body heat — slow and uncontrolled.
    - **Active thaw:** the system heats the probe (helium gas / electric) to thaw the ice ball quickly and controllably — a shorter cycle time, and the fast melt adds to the osmotic injury.

**The gases — why argon freezes and helium thaws:** the cryo-probe runs on the Joule–Thomson effect — a high-pressure gas expanding through the probe tip changes temperature, and the direction depends on the gas:
    - **The mechanism:** expanding gas molecules do work against their mutual **attraction** — paid from their kinetic energy, so the gas cools; counteracting this, at high pressure the molecules are crowded and repelling, so expansion releases energy and warms. Each gas has an **inversion temperature** — below it, expansion cools; above it, expansion warms.
    - **Argon — the freeze:** argon's inversion temperature is ≈ 723 K — far above room temperature, so room-temperature argon cools on expansion: it drops below its boiling point (−186 °C), partially liquefies, and the boiling liquid absorbs a huge amount of latent heat from the tissue around the needle — tip temperatures around −160 to −190 °C. The ice ball grows.
    - **Helium — the thaw:** helium's inversion temperature is ≈ 45 K — far *below* room temperature, so expanding helium **warms** (its intermolecular attraction is the weakest of any gas — the same property that makes liquid helium hard to liquefy). The warm gas heats the needle — the active thaw.
    - **Why the design matters:** one needle, two gas lines, no moving parts — the freeze–thaw–freeze protocol is switched by changing the gas feed, which is why the cycles are fast and controllable.

**Skin protection — warm water:** for superficial targets the ice ball can reach the skin and freeze it (a cold injury at the puncture site and along the surface). **Warm water** is placed over the skin during the freeze to keep the skin above freezing while the deep ice ball grows.

---

## 7. Alerts

| Check | Improve |
|---|---|
| **Registration** — always registered head-first supine, regardless of physical position? | The image orientation must match what the radiologist sees when inserting the needle inside the bore — never register by physical position |
| **Table reset & mode** — target lesion found, table position reset, mode ISO → FIX? | FIX locks the geometry for the skin-marking procedure; switch back to ISO for the BEAT interactive phase |
| **Skin-mark movement** — table out by 1002 + z (e.g., H50 → 1052), back by the same amount? | A wrong table movement projects the mark onto the wrong skin point |
| **x/y signs at the lab laser** — +x right, −x left? | A sign error mirrors the mark across the laser centre |
| **Laser off** — laser switched off before scanning? | A switched-on laser causes image artifact |
| **Needle loop** — BLADE re-check after each needle, BEAT interactive before each re-insertion? | Each needle position must be confirmed before the next is placed |
| **Ice ball** — monitored on the BLADE runs during each cryo cycle? | The ice ball must cover the tumor margin **plus a few mm** (the lethal isotherm sits inside the visible edge) — verify on the 1st and 2nd cryo runs |
| **Send list** — BLADE tra & sag at pre / 1st cryo / 2nd cryo / post cryo sent? | The four timepoint sets are the procedure record |

---

## 8. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-06 | — | Initial build — MR-guided cryoablation workflow. Head-first-supine registration rule + HASTE localization + table reset (ISO→FIX) + planning pair (T2 BLADE tra/sag, bore coil) + optional T1 StarVIBE in/out phase + pixel-lens needle planning + lab-laser skin marking (table out by 1002 + z; H50 example → 1052; +x right / −x left) + BEAT interactive needle guidance + BLADE re-check loop + cryo monitoring (1st/2nd/post) + send list (BLADE tra/sag ×4 timepoints) |
