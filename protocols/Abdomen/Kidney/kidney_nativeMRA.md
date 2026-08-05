# Kidney Native MRA (Non-Contrast Renal MRA)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the renal arteries (~L1 level).
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** T2 HASTE coronal: shallow breathing (not breath-hold). For the NATIVE TrueFISP: breathe quietly and regularly — the acquisition is respiratory-triggered and follows the breathing cycle.
- **IV Access:** Not required — non-contrast protocol.
- **Patient Preparation — Triggering setup:**
  - **Respiratory trigger (PERU):** Connect the PERU (peripheral trigger unit) cable to the Siemens ECG gating device port. Position the respiratory bellows around the upper abdomen (over the diaphragm). Confirm the respiratory waveform is displayed on the physiology monitor with clear end-expiration plateaus.
  - **ECG trigger:** Attach ECG electrodes per standard Siemens cardiac gating setup (white, green, red, black leads placed along the cardiac axis, starting from the sternal notch and extending toward the left lower chest. Adjust until the R-wave is >1 mV on the physiology display). An adequate R-wave amplitude (>1 mV) and a clean trace without artefact are essential — the NATIVE TrueFISP acquisition is gated to each R peak. Poor ECG signal degrades triggering and the acquisition is non-diagnostic.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_shallow_breathing_p2` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both kidneys | **Superior oblique** over heart | Shallow breathing |
| 2 | `t2_tse_fs_tra_p2_mbh` | Axial | True axial | Both kidneys. Upper pole → lower pole | **None** | Multi breath-hold |
| 3 | `t2_tse_tra_p2_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t1_vibe_dixon_tra_p4_bh` | Axial | True axial | Both kidneys | **None** | Breath-hold |
| 5 | `native_truefisp_resp_trig_tra` **or** `native_truefisp_nav_ECG_tra` | Axial | True axial. Slab covering the aorta and both renal arteries | Aorta (above renal origins) → distal renal arteries | **None** | Respiratory triggered **or** navigator-gated, ECG-triggered |

*#1: Shallow breathing — not breath-hold.*  
*#2–#3: T2 TSE pair — same as kidney.md.*  
*#4: T1 VIBE Dixon axial — in/opposed phase for fat and intrinsic T1 signal. Same as kidney.md.*  
*#5: NATIVE TrueFISP — non-contrast renal MRA. Two triggering options: respiratory (PERU) or ECG (navigator).*  

---

## 3. Sequence Rationale

### Core Strategy

This is a **non-contrast** renal artery MRA for patients who cannot receive gadolinium (renal impairment, eGFR contraindication, NSF risk). NATIVE TrueFISP (Siemens' non-contrast MRA sequence) is a 3D balanced SSFP acquisition — blood is inherently bright from T2/T1 contrast without requiring contrast injection. The clinical question is renovascular: is there renal artery stenosis? No mass characterization is performed — the T2 and T1 sequences are purely anatomical survey.

**Key differences from `kidney_CeMRA.md`:**

- **No contrast** — NATIVE TrueFISP replaces the entire CeMRA pipeline (mask, bolus tracking, arterial acquisition, subtraction).
- **No post-contrast T1** — no dynamic or nephrographic phase. Mass characterization is not the goal.
- **No DWI, no TrueFISP vessel scout** — the NATIVE TrueFISP is the MRA and vessel assessment.
- **HASTE coronal is shallow breathing** — not breath-hold. This is a renal patient population; breath-hold compliance may be limited.
- **T1 VIBE Dixon is p4 accelerated** — higher parallel imaging factor to shorten breath-hold.

---

### Sequence Details

**T2 survey (#1–#3):** Same kidney screen as `kidney.md` but without contrast considerations. The T2 pair identifies renal size, position, cysts, and any incidental mass. No dedicated coronal T1 for surgical planning — the protocol is focused on the arteries.

**T1 VIBE Dixon (#4):** In/opposed phase for fat and intrinsic T1 signal. p4 parallel imaging keeps the breath-hold short.

**NATIVE TrueFISP (#5):** A 3D balanced SSFP slab covering the aorta and both renal arteries. Blood is bright from the inherent T2/T1 contrast of fully refocused SSFP — arterial inflow enhances the signal; stationary tissue is saturated. The acquisition is inherently motion-sensitive (SSFP requires short TR and is intolerant of motion), so triggering is essential.

Two triggering options:

- **Respiratory trigger (PERU):** Connect the PERU (peripheral trigger unit) to the Siemens ECG gating device. A respiratory bellows or navigator detects the breathing cycle and acquires data only at end-expiration. The patient breathes freely; the acquisition is gated.
- **ECG trigger (navigator ECG):** The acquisition is gated to the cardiac cycle. Renal artery flow is pulsatile — systolic phase maximizes arterial inflow enhancement (fast flow); diastolic phase minimizes flow artefacts and provides more consistent vessel signal. The navigator corrects for respiratory motion simultaneously. ECG triggering is more accurate but requires reliable ECG signal; respiratory triggering (PERU) is simpler and adequate for most patients.

**Choice:** Respiratory trigger is the default — simpler setup, adequate for most patients. ECG trigger when cardiac gating is needed (arrhythmia, pulsatile flow artefacts on prior imaging) or when respiratory pattern is erratic and navigator gating alone is insufficient.

**Why triggering is needed:** Unlike 2D TrueFISP (single slice in milliseconds — effectively motion-insensitive), NATIVE TrueFISP is a 3D volume with two phase-encode directions and takes several minutes. Respiratory motion and cardiac pulsation produce severe ghosting in both phase-encode directions without gating. The SSFP contrast mechanism itself is not vulnerable — the 3D acquisition is just slow enough for motion to matter.

**Why axial, not coronal:** The renal arteries arise from the anterior aortic wall and course posteriorly to the hila — the A/P direction. An axial slab puts the renal arteries in-plane (readout direction), giving maximum spatial resolution where it counts. A coronal slab would make the vessels through-plane, relying on slice resolution (typically coarser). CeMRA uses coronal because the contrast gives high SNR in any plane — NATIVE TrueFISP lacks that SNR headroom and benefits from the narrower S/I axial slab (fewer slice-encode steps, shorter acquisition).

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both kidneys and renal arteries in the NATIVE slab? Aorta from above renal origins to below? | Accessory renal arteries arise below the main origins — if the slab ends too high, an accessory artery is missed |
| **NATIVE image quality** — Renal arteries bright, background dark? No motion artefact? | If arteries are dark: the SSFP contrast may be failing — check shim and frequency adjustment. If motion artefact: the triggering may be irregular — check respiratory bellows/navigator signal or ECG lead placement |
| **T1 Dixon** — In/opposed phase diagnostic despite p4 acceleration? | Higher parallel imaging reduces SNR. If non-diagnostic: reduce acceleration factor |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 5 sequences. Non-contrast NATIVE TrueFISP renal MRA. Two triggering options: respiratory (PERU) or ECG (navigator). No contrast, no DWI |
