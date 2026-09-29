# Aorta (Aortic MRI)

**Version:** 1.0 | **Date:** 2026-09-27 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first.
- **Coil:** Body matrix coils anteriorly + spine array.
- **Laser Landmark:** Sternal notch (thorax-only studies); xiphoid (whole-aorta studies).
- **Gating setup:** Pulse trigger (PPU) on a finger or toe for the bright-blood (trufi) series — check the waveform before starting. ECG leads only when the quantification layer is needed (cine + flow, coarctation work).
- **Breath-Hold Coaching:** End-inspiratory, consistent, kept small — the mask and post-contrast acquisitions must match in depth.
- **IV Access (contrast studies):** Right antecubital vein, 18–20 G [Confirm gauge]. Right arm is the rule — left-arm contrast crosses the arch origins via the left brachiocephalic vein.
- **eGFR:** Check before contrast — threshold 30.

---

## 2. Decision Pathway

Every aorta study is assembled by answering five questions in order — the toolkit (§3) is the reference for whatever each answer adds.

**First: is the region the arch, or the lower aorta?** This decides the geometric family — and with it the entire planning cascade, because the localizer planes exist to aim the target plane:

- **Arch question** → the sagittal-oblique family: the cor and tra build the candy-cane (the tra passes the plane through both aortas, the cor tilts it along the long axis); the obl sag is the long-axis view and hands its center to the fl3d slab, which follows in the same plane.
- **Whole-run question** — thoracoabdominal extent, the renal origins, the iliac bifurcation — → the coronal family: the coronal and sagittal show the vessel's course in two long-axis views, and from them the tilt is taken — the axial stack is angled to **true transverse** (perpendicular to the aortic axis), and the fl3d follows as **true coronal** along the aortic axis (the aorta is left of the spine in the thorax, midline below, so the slab follows the vessel rather than the body).

**Second: is the question about the flowing lumen only, or also about the wall?** Lumen-only questions — aneurysm size, follow-up, arch morphology — are answered by bright-blood sequences alone. A wall question — intramural hematoma, aortitis, dissection flap — must add the black-blood HASTE, because the wall is invisible to bright-blood imaging, and the dark-blood T1, which dates the hematoma. The wall's transverse plane is core; the longitudinal plane is added on demand. The pairing rule follows: each plane's blood contrast serves that plane's question — the wall planes get black-blood (robust to flow state), the flow planes get bright-blood (flow-sensitive), and the transverse plane carries both, because that is where the diagnosis is made.

**Third: is contrast given — and what does it need to show?** Three questions, each with its own sequences:

- **The lumen at its peak** — aneurysm anatomy, branch origins, the flap and the true/false-lumen flow in one timed pass → the timing tool + the fl3d block (pre, 1st pass, 2nd pass).
- **The wall's behavior** — aortitis, periaortic tissue → the T1 pair: the post-contrast T1 against the pre-contrast T1 already added by the wall question — enhancement is the difference between the two (a bright wall on the post alone may be methemoglobin, which glows without any contrast). No timing, no angio.
- **The time course** — whatever fills or changes late: a dissection false lumen, an aneurysm sac, thrombus, an endoleak → a cheap late look, the delayed post-contrast T1; or, when the time course itself is the diagnosis (endoleak, differential true/false-lumen enhancement), the time-resolved series, which sees every frame a single late T1 would miss.

The standard dissection study combines them: aortogram + delayed T1. If contrast is not possible, the study is the plain lumen-plus-wall survey.

**Fourth: how much of the aorta must be seen?** Confirm with the radiologist whether the **renal arteries** must be included and whether the **cardiac chambers** must be included; the answers set the field of view and decide whether the 2D series need **Composing** — two overlapping stations stitched into one long image covering arch → bifurcation. Only 2D series can compose; a 3D slab cannot. Known or suspected pathology below the diaphragm always means yes to the renal level; a purely thoracic question allows thorax-only coverage, the shorter, simpler study.

**Fifth: is there a stenosis or gradient to quantify?** The coarctation question — add the cine (the stenosis as a dynamic event, plus the aortic-valve screen: a bicuspid valve accompanies coarctation in roughly half of cases) and the PC flow pair (ascending-aorta reference + stenosis peak velocity → gradient).

**In one glance:**

| If… | Then… |
|---|---|
| Arch is the question | obl sagittal family (candy-cane long axis) — otherwise coronal family (plain sag long axis) |
| Wall in question (IMH, aortitis, flap) | add haste tra + dark-blood T1 (longitudinal haste on demand) |
| Contrast for aortogram | add timing + fl3d pre / 1st pass / 2nd pass |
| Contrast for wall enhancement | add vibe fs C — paired with the pre-contrast T1 (enhancement = the difference) |
| Contrast for dynamics (endoleak, slow filling) | add the dynamic series — replaces the passes |
| Renals / heart must be covered | FOV extends; 2D series compose |
| Slow filling (false lumen, sac) | add vibe fs C to the aortogram set |
| Stenosis / gradient (coarctation) | add cine + PC flow (VENC 150, step-up 400) |

---

## 3. The Toolkit — what each sequence type is for

Reference for the sequences chosen in §2.

- **Bright-blood — `t2_trufi` (TrueFISP).** Blood bright, everything else gray — the *lumen* family: diameters, the arch silhouette, the flap as a dark line across the bright column. Pulse-triggered so the pulsating aorta stays sharp. Three roles: the **coronal** is the cheap first localizer (free breathing), the **axial** is the planning parent, and the **long-axis view** profiles the vessel in one plane — sagittal oblique (the candy-cane) when the arch is the question, plain sagittal when the whole vertical run is the question. The long-axis view is also the planning parent of the fl3d (its center is copied to the slab).

- **Black-blood — the wall family (`t2_haste` + `t1_tse_db`).** The same effect — lumen dark, **wall bright**, the only sequences that show the wall (the intramural hematoma crescent, wall thickening, the flap against the dark lumen) — achieved by two different mechanisms:
    - **`t2_haste` (single-shot TSE) — the detector.** Dark by **flow void** (fails when flow is slow). T2 sees the hematoma at **any age** (a bright crescent from day one); single-shot, free breathing — the fast whole-run screen. **Transverse is the core plane** (the wall in cross-section); the longitudinal plane is on demand — obl sagittal in arch studies, coronal in whole-run studies.
    - **`t1_tse_db` (T1 TSE, long axis) — the dater and the profile view.** Dark by **double-inversion preparation**. T1-bright only once methemoglobin forms (subacute) — it stages what the haste found, in the obl sagittal long axis. Pre-contrast; chosen when the wall is the *target*, not just a screening item.

- **T1 — `t1_vibe_fs` (fat-suppressed, axial).** The bright-blood T1 workhorse — the screen and the enhancement pair:
    - **Alone (pre-contrast)** — the IMH age detector in cross-section. Methemoglobin is T1-bright without any contrast — and contrast would only confound it — so in non-contrast studies this is the whole T1 story.
    - **As a matched pair (pre + post, same geometry)** — the pre is the baseline, the post is the **delayed layer**: the late look after the first pass, showing where contrast has *accumulated* (the slow-filling false lumen, the aneurysm sac) rather than where it flowed — and **wall enhancement**: gadolinium leaking through an inflamed, permeable wall (aortitis). Enhancement is the difference between the pair — a wall bright already on the pre is methemoglobin, not inflammation.

- **Angio — `fl3d` (3D spoiled GRE).** The contrast platform for the *aortogram*: gadolinium makes the lumen blaze, timing decides the rest (§6). Three uses of the same sequence: `pre` (the subtraction mask, geometry copied exactly to the post), `1st pass` (the arterial phase), `2nd pass` (venous/delayed — filling-defect confirmation: a true stenosis persists on both passes, a timing artifact disappears).

- **Dynamic — `twist` (time-resolved).** Repeated 3D frames every ~1–3 s with no timing required: the contrast *movie*. It replaces the timed passes entirely and carries its own pre-contrast baseline, so no separate mask is needed. Included when the time course is the diagnosis — endoleak, slow sac filling, differential true/false-lumen enhancement.

- **Quantification — cine + PC flow.** ECG-retrospective-gated — the cardiac toolkit enters here: `trufi_cine_retro` shows the aorta through the cardiac cycle (the coarctation jet, pulsatility); PC flow through-plane measures velocity — at the ascending aorta (the reference) and at the stenosis (peak velocity → Bernoulli gradient). VENC 150, step-up to 400 for high-velocity jets (physics: file 05, entry 2).

- **Timing — `care_bolus_sag` / `testbolus_tra`.** The two tools that place k-space center on the arterial peak (§6).

---

## 4. Sequence List

| Series | Category | Include when |
|---|---|---|
| `t2_trufi_cor` (non-bh) | bright-blood, planning | Always — first localizer |
| `t2_trufi_tra` | bright-blood, planning | Always — axial planning parent |
| `t2_trufi_obl_sag` (arch) / `t2_trufi_sag` (whole run) | bright-blood, long axis | Always — the long-axis lumen view + fl3d planning parent |
| `t2_haste_tra` | black-blood, transverse | Wall question |
| `t2_haste_obl_sag` / `t2_haste_cor` | black-blood, longitudinal | Wall question, on demand — obl sag (arch) or cor (whole run) |
| `t1_tse_db_obl_sag` | T1, dark-blood, long axis | Wall question — the wall/IMH anatomy sequence, pre-contrast |
| `t1_vibe_fs_tra_bh` | T1 FS, axial | Wall question — the IMH-age T1; the pre of the matched pair when enhancement is asked |
| `care_bolus_sag` (or `testbolus_tra`) | timing | Contrast for aortogram |
| `fl3d pre` | angio | Contrast for aortogram |
| `fl3d 1st pass C` | angio | Contrast for aortogram |
| `fl3d 2nd pass C` | angio | Contrast for aortogram — optional (filling-defect confirmation; dissection hands this job to the delayed T1) |
| `twist_cor` (dynamic) | time-resolved angio | Filling dynamics — replaces the timed passes, carries its own baseline |
| `t1_vibe_fs_tra_bh_C` | T1 FS, axial | The delayed layer — slow filling (false lumen, sac) or wall enhancement, judged against its pre |
| `trufi_cine_retro_obl_sag` | cine | Stenosis / gradient question |
| `trufi_cine_retro_aortic_valve` | cine | Stenosis found — bicuspid valve screen |
| `flow_150_tp_retro_bh` (AO / stenosis) | PC flow | Stenosis found — reference + peak velocity → gradient |

*Site note:* the dissection protocol's `fl3d_cor_dynC` maps to the 1st-pass row if it is the timed angio, or to the dynamic row if it is a true time-resolved series — confirm on the console.

---

## 5. The Standard Studies

The usual answers to the five questions produce the named protocols — each is simply a ticked subset of the list above:

- **Contrast aorta (thoracic)** — region: arch · wall: yes · contrast: aortogram · coverage: thorax (per radiologist). = planning + long axis (obl sag) + haste tra + dark-blood T1 + care bolus + fl3d obl sag pre/1st/2nd. The *lumen study of the arch*.
- **Plain aorta (whole aorta)** — region: whole run · wall: yes · contrast: none · coverage: whole aorta. = planning + long axis (plain sag) + composed haste tra/cor + composed trufi tra/cor + vibe fs tra (IMH age). The *wall study without contrast*.
- **Dissection** — region: whole run · wall: yes · contrast: aortogram + delayed T1 · coverage: whole aorta. = planning + long axis (plain sag) + composed haste cor/tra + composed trufi tra + vibe fs tra (pre) + care bolus + fl3d cor pre/dynC + vibe fs tra C. The *complete study*.
- **Coarctation** — the thoracic contrast study + quantification: cine obl sag; if the stenosis is found, cine of the aortic valve + PC flow at the ascending aorta and at the stenosis. The *six-layer study*.

---

## 6. Bolus Timing — Care Bolus (default) / Test Bolus (alternative)

General bolus physics (slug concept, delay equation, k-space ordering): `knowledge/physics/05_angiography_and_flow.md`, entry 3.

**Dose ledger**

| When | What | Rate | Purpose |
|---|---|---|---|
| Care Bolus timing | full dose, no test injection | 2 mL/s | monitored in real time at the AVOT |
| Test Bolus timing (alternative) | 1–2 mL | 2 mL/s + saline flush | measure transit time T_p |
| Main injection | **1.5× standard dose** [Confirm 0.15 mmol/kg] | 2 mL/s | long slug → wide arterial window, forgiving timing |

**Workflow** — pre mask → start Care Bolus monitoring → inject → trigger → 1st pass → 2nd pass.

**Care Bolus (default)**

- Monitoring plane: **sagittal through the aortic outflow tract (AVOT)** — coronal is the fallback when a suitable sagittal plane cannot be found.
- Inject the full dose; watch the slice in real time; **start the fl3d when contrast reaches the AVOT**.
- The trigger is deliberately upstream of the arch: the trigger latency + breath-hold command + T_center consume exactly the time the bolus front needs to round the arch, so k-space center lands on the arch/descending peak. The 1.5× dose at 2 mL/s makes a long slug, which widens the arterial window and makes this early trigger forgiving.
- The AVOT plane doubles as the **venous-reflux check**: the left ventricle is visible — verify LV enhancement before triggering (distinguishes true arterial inflow from reflux up the SVC/brachiocephalic veins — SVC obstruction, high CVP, same-side AV fistula).
- **The couch will move after the trigger** (the monitoring slice and the fl3d slab may sit at different table positions) — give the breath-hold command ~1 s in advance so the patient is holding when the table stops.

**Test Bolus (alternative)**

- `testbolus_tra` through the ascending aorta at the arch; inject 1–2 mL at 2 mL/s + saline flush; the dynamic series gives the time-to-peak T_p.
- Start the fl3d at

  ```
  delay = T_p + (V_inj / R) / 2 − T_center
  ```

  measured from the start of the full injection (T_p ≈ arrival of the front; (V/R)/2 = half the injection duration; T_center ≈ 2 s for elliptical-centric ordering).

**Pitfalls** — started too early → Maki artifact (bright ring, dark lumen); started too late → SVC/azygos bright over the arch; aneurysm sacs fill slowly and swirl — incomplete sac filling on the arterial phase is physiology, not a dissection flap (add a delayed phase when sac morphology matters); breath-hold failure moves the thoracic aorta and ruins the arch.

---

## 7. Alerts & Important Considerations

| Check | Improve |
|---|---|
| **Pulse waveform** — PPU trace clean and regular before the bright-blood series? | Reposition the sensor; a poor trigger leaves pulsation ghosting on the trufi series |
| **Coverage** — renal level and cardiac chambers confirmed with the radiologist? | The answers set the FOV before any series is planned |
| **Composing** — stitched series cover arch → bifurcation without a gap? | Reposition the stations |
| **Mask ↔ post geometry** — fl3d pre copied exactly to the post, same breath-hold depth? | Any mismatch becomes dark rings on the subtracted MIP |
| **Care Bolus plane** — sagittal through the AVOT (coronal fallback)? | A bad plane makes the trigger unreliable |
| **LV check** — left ventricle enhanced before triggering? | Reflux up the SVC/brachiocephalic veins mimics arterial filling |
| **Couch move** — breath-hold commanded ~1 s before the trigger? | The table repositions after the trigger; the patient must already be holding |
| **Contrast** — right arm? eGFR checked? gauge adequate for 2 mL/s? | Use the largest available line; left arm only as fallback |
| **Quantification** — ECG trace clean before the cine and flows? | Retrospective gating is useless with a poor trigger |

---

## 8. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-22 | — | Initial — decision-first: five-question pathway (region first), toolkit reference, single sequence list, four standard studies |
