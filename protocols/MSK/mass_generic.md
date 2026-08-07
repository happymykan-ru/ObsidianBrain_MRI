# Mass — Generic (Musculoskeletal Tumour Protocol)

**Version:** 1.0 | **Date:** 2026-08-07 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Depends on region. The mass must be centred in the magnet isocentre.
- **Coil:** Smallest surface coil that covers the mass with adequate margin. Flex coil for extremities; wrist coil for hand/wrist; knee coil for distal thigh/proximal calf; body matrix + spine array for pelvis, proximal thigh, chest wall, or shoulder girdle.
- **Laser Landmark:** Centre of the palpable mass. If non-palpable, at the anatomical level indicated on the referral or prior imaging.
- **Skin Markers:** Place two oil-based fiducial markers at the margins of the patient-indicated mass (proximal and distal, or medial and lateral). The markers are visible on all sequences and confirm that the imaged mass corresponds to the clinical finding.
- **Immobilization:** Sandbags, foam padding, and tape as needed to eliminate motion. The region must not shift between sequences — misregistration between pre- and post-contrast sequences invalidates subtraction.
- **IV Access:** 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_cor` / `t2_stir_sag` | Coronal or Sagittal (Long Axis) | Parallel to the long axis of the involved compartment. Choose coronal or sagittal — whichever best profiles the mass along its full length | Mass + entire involved compartment. At least 5 cm margin beyond the mass in all directions. Include joint above and below if within FOV limits | **None** |
| 2 | `t1_tse_dixon_cor` / `t1_tse_dixon_sag` | Copy from #1 (Long Axis) | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `t1_tse_tra` | Axial | Perpendicular to long axis of compartment | Copy coverage. Mass + compartment in cross-section | **None** |
| 4 | `t2_tse_fs_tra` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| — | **Contrast** | — | Standard dose. Inject at 2 mL/s. | — | — |
| 5 | `t1_vibe_tra_dyn_C` *(post-op only)* | Axial | Copy Slice from #3 | Mass only. Tight FOV for temporal resolution | **None** |
| 6 | `t1_tse_dixon_cor_C` / `t1_tse_dixon_sag_C` | Copy from #1 (Long Axis) | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 7 | `t1_fs_tse_tra_C` | Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |

---

## 3. Sequence Rationale

### Core Strategy

This is a **generic template** — it adapts to any anatomical region by adjusting FOV, coil positioning, and slice prescription to the specific compartment. The sequence selection is fixed because each sequence serves a defined role that applies universally to musculoskeletal mass characterization.

Three layers:

- **Fluid detection** — STIR long axis (#1): screen for the mass. Oedema, cystic/necrotic components, peritumoural reaction.
- **Anatomical definition** — T1 Dixon long axis (#2), T1 TSE tra (#3), T2 FS tra (#4): compartment of origin, margins, relationship to neurovascular bundle and bone, intrinsic tissue composition (fat, haemorrhage, matrix).
- **Enhancement characterization** — T1 Dixon long C (#6) for subtraction; T1 FS TSE tra C (#7) for primary enhancement assessment; dynamic VIBE (#5) if post-op.

### Why STIR/Dixon in the long plane, spectral FS in the axial?

The plane assignment follows from each sequence's role, not from any physics constraint tied to the plane itself.

**T2 side:** The long-axis plane (#1) screens joint-to-joint across a large FOV — B0 varies across that span (skin folds, bony contours, joints). STIR is immune to this; it suppresses fat uniformly regardless. The axial plane (#4) covers a single cross-sectional slab through muscle — a smaller, more homogeneous region where spectral FS is more likely to hold up, and it returns higher SNR for the surgical-detail plane.

**T1 side:** Dixon is in the long axis (#2, #6) because opposed-phase (microscopic fat detection) is a characterization tool — you want it profiling the full mass. The non-FS T1 TSE in the axial plane (#3) is about haemorrhage detection and compartmental anatomy — fat is deliberately left bright as natural contrast, so Dixon offers no advantage. The post-contrast FS TSE axial (#7) uses spectral FS because TSE + spectral FS gives the highest SNR for the reporting reference image — when B0 is homogeneous in that slab.

**In practice:** if B0 is poor (metal, skin folds, surgical scar), swap spectral FS to STIR or Dixon for T2, Dixon for T1 post-contrast. The choices above are the default, not a rule.

---

### Pre-Contrast

**T2 STIR (#1):** The **mass detection sequence** in the long-axis plane. Muscle is T2-intermediate, fat is suppressed dark, oedema/fluid is bright — the mass is conspicuous. Profiles the full craniocaudal (or anteroposterior) extent, relationship to the joints above and below, and guides the axial plane prescription (#3, #4).

**T1 TSE Dixon (#2):** The **pre-contrast anatomical reference**, in the same long-axis plane as #1. Four contrasts from one acquisition:

- **Water-only:** Mass profiled against dark fat — the pre-contrast mask for the subtraction sequence (#6).
- **Opposed-phase:** Detects **microscopic intralesional lipid** — signal dropout relative to in-phase indicates intracellular fat (liposarcoma, lipid-rich metastases such as renal cell, adrenal rest tumour). Macroscopic fat is obvious on all sequences; microscopic fat is only apparent on opposed-phase.
- **In-phase:** Standard T1 anatomy. Bone marrow, muscle, and fat in their normal signal relationship.

**T1 TSE axial (#3):** Non-fat-saturated T1 in the cross-sectional plane. Three roles:

- **Compartments:** Fat between muscle groups delineates fascial boundaries — the mass's compartment of origin is best defined where fat is bright.
- **Subacute haemorrhage:** Methaemoglobin is T1-bright on non-FS sequences. On fat-saturated sequences it is indistinguishable from enhancing tissue or fluid — the non-FS T1 is the definitive reference for intrinsic T1 signal.
- **Bone marrow:** Normal marrow is T1-bright (fatty). Marrow replacement by tumour is T1-dark — the most sensitive pre-contrast sign of bone involvement.

**T2 TSE FS axial (#4):** The **cross-sectional anatomical plane** — the surgical planning plane. Fat-suppressed T2 defines the mass, its internal matrix (solid vs cystic vs necrotic), and peritumoural oedema. Assesses circumferential margins, neurovascular bundle relationship, and bone cortical contact.

---

### Post-Contrast

**T1 VIBE axial dynamic (#5) — post-op only:** Multiple consecutive acquisitions to capture enhancement kinetics. Temporal resolution ≤15 s per measurement. Inject at start.

For a primary mass, the question is "does it enhance?" — the static post-contrast sequences (#6, #7) answer this. Post-operatively, everything enhances to some degree: granulation tissue, scar, seroma, and residual/recurrent tumour all show some enhancement. The dynamic distinguishes them by their enhancement curve:

- **Type 1 (progressive):** Gradual increasing enhancement — post-surgical granulation tissue, benign fibrosis.
- **Type 2 (plateau):** Rapid uptake then plateau — cellular benign or intermediate-grade lesions.
- **Type 3 (washout):** Rapid arterial enhancement with early washout — recurrent high-grade sarcoma, hypervascular metastases.
- **Type 4 (no enhancement):** Seroma, haematoma, necrotic tumour.

Only needed when there has been prior surgery and the clinical question is recurrence vs post-surgical change. Skip for primary mass assessment.

**T1 TSE Dixon long axis post-contrast (#6):** The **subtraction sequence**. Dixon water-only is acquired pre (#2) and post (#6) with identical geometry — subtraction (post − pre) removes all intrinsic T1 signal, leaving only true enhancement. Essential when the mass is intrinsically T1-bright (haemorrhage, protein, fat) and enhancement would otherwise be ambiguous. Water-only also shows enhancing tumour against uniformly dark fat along the full craniocaudal extent and any skip lesions.

**T1 FS TSE axial (#7):** The **primary enhancement sequence** — the highest-SNR, highest-detail static post-contrast image. This is the cross-sectional surgical plane and the sequence the radiologist reports from for enhancement assessment (margins, neurovascular bundle, bone).

---

## 4. Adjustment Strategies

### Coverage & Set-and-Go

Coverage must include at least **5 cm beyond the enhancing tumour margin** in all directions. For the long-axis plane include the joint above and below where FOV permits — skip lesions and peritumoural oedema track along the compartment.

When the required craniocaudal coverage exceeds what a single station can acquire, use **set-and-go** (multi-station):

- **Standard bore (60 cm):** Set-and-go needed beyond [Confirm] mm
- **Long bore (70 cm):** Set-and-go needed beyond [Confirm] mm

**Overlap:** 30–40 mm for the long-axis plane (#1, #2, #5); 0 mm for the axial plane (#3, #4, #6).

**Steps:**
1. No-tilt true plane
2. Set overlap
3. Set and go
4. Couple stacks
5. Tilt plane

Parameter changes must be applied to **all slabs** individually — adjusting FOV, resolution, or fat sat on one slab does not automatically propagate. Manually update each slab.

When copying slice geometry from pre-contrast to post-contrast sequences: use **copy across multiple steps** and also copy the **phase encoding direction** — this ensures identical geometry and matching distortion between the mask and the post-contrast sequences for subtraction.

### Resolution

Pixel size (mm) = FOV (mm) ÷ matrix. Phase pixel = base resolution × (100 ÷ phase %).

**Base resolution** (frequency-encode direction, mm):
- Hand, wrist, foot: ≤0.5
- Forearm, calf, upper arm: 0.5–0.7
- Thigh, shoulder girdle: 0.7–1.0
- Pelvis, buttock, chest wall: 0.8–1.2

**Phase resolution** (% of base):
- Set to 75–85% across all regions. Saves scan time; the SNR gain offsets the slightly rectangular pixel.

**Slice thickness** (mm):
- Hand, wrist, foot: 2–3
- Forearm, calf, upper arm: 3–4
- Thigh, shoulder girdle: 4–5
- Pelvis, buttock, chest wall: 5–6

**Slice gap** (% of slice thickness):
- Small masses near critical structures (nerve, vessel): 0–10
- All others: 10–20

**Post-contrast:**
- **T1 FS TSE (#7):** may reduce phase resolution by 5–10% from the pre-contrast standard to compensate for the fat sat pulse time penalty while maintaining coverage and scan time.
- **T1 Dixon (#5):** keep geometry identical to the pre-contrast Dixon (#2) — same FOV, matrix, resolution, slice thickness, and gap. Any mismatch breaks the subtraction.

### Fat Saturation Strategy

**Weak fat sat for pre-contrast, strong for post-contrast.** Pre-contrast: gentle suppression preserves SNR and avoids accidental water suppression — fat just needs to be darker than oedema for detection. Post-contrast: fat must be completely black — any residual fat signal at the tumour margin can mimic enhancement or mask it.

**SPAIR** (spectrally-selective adiabatic inversion recovery) replaces standard spectral FS when B1 homogeneity is in question. The adiabatic pulse is B1-insensitive — uniform fat suppression where standard spectral FS would be patchy. Cost: slightly longer and higher SAR.

SPAIR helps in regions prone to **B1** inhomogeneity (poor RF transmit uniformity): shoulder girdle/axilla, pelvis/buttock, chest wall, and large-FOV thigh — especially with body matrix coil at 3T. 

SPAIR does **not** fix **B0** problems (skin folds, scars, joints, metal). For B0-compromised sites: fall back to STIR for T2, Dixon for T1.

### Phase Encoding Direction

1. *Reduce flow artifact:* align phase with the vessel so the ghost stays on the vessel, not across adjacent anatomy. *(Long axis: phase H/F — major vessels run craniocaudally, ghost stays on the vessel track.)*
2. *Not overlap area of interest:* the ghost must not land on the mass or critical structures.
3. *No wrapping:* the FOV must contain all anatomy in the phase direction. If anatomy extends beyond the FOV, add phase oversampling or swap direction.
4. *Shortest dimension:* all else equal, phase-encode along the shorter FOV dimension for fewer steps.

**Note:**
- Subtraction pair: phase direction must match — copy with geometry.
- In-plane rotation: consider rotating the FOV slightly so the phase-encode ghost falls outside the mass rather than through it, if the anatomy and coverage permit.

### Sat Band & Flow Compensation

Both reduce pulsation artifact — sat band for vessels outside the stack, flow comp for vessels inside. They address different populations and do not cancel each other.

**Sat band** saturates inflowing spins before they enter the stack. Blood arrives dark → no signal → no pulsation ghost. Also prevents bright contrast-laden inflow from being mistaken for enhancement at the tumour margin.

- **Parallel H:** single sat band superior to the stack. Suppresses arterial inflow from above (proximal → distal flow). Sufficient for most extremity masses where inflow is unidirectional.
- **Parallel H + F:** sat bands both superior and inferior. Use at junctional regions (shoulder, hip/pelvis) where vessels converge from multiple directions, or when large draining veins below the stack carry contrast-laden blood back into the FOV from below.

**Flow compensation** rephases moving spins already within the FOV, correcting the phase errors that produce pulsation ghosts along the phase-encode direction. Side effects: vessels become brighter (reduced flow void) and minimum TE increases. The brighter signal has a diagnostic benefit — a bright branching tubular structure is clearly a vessel; a dark flow void can be mistaken for necrosis.

- **Slice direction** (through-plane flow): axial slices. Major extremity vessels run perpendicular to the axial plane — flow comp rephases blood passing through each slice. Reliable in all regions including junctions.
- **Read direction** (in-plane flow): coronal and sagittal slices. Vessels run within the plane along the compartment — flow comp rephases blood moving along the vessel during readout. Reliable in straight extremities (forearm, calf, upper arm, thigh) where vessels follow the compartment. Less reliable at junctional regions (shoulder, pelvis) where vessel geometry is complex.

**When to use which:**

- **Neither:** no significant vessels near or within FOV. Small superficial mass, distal, very small FOV.
- **Sat band only (H or H+F):** major inflow artery near the stack edge, but internal vessels not creating problematic ghosting. Mid-forearm mass with a single feeding artery and clean image.
- **Flow comp only (slice or read):** no major inflow outside, but small internal arteries creating ghosts. Hand, wrist, foot, ankle — small distal masses.
- **Both (sat band + flow comp):** major inflow outside AND internal pulsation both contributing. Thigh, pelvis, shoulder girdle, upper arm — proximal/junctional masses.
- **Junctional long plane exception:** at the shoulder or pelvis in the long-axis plane, skip read flow comp — vessel geometry is too complex for it to be reliable. Rely on H+F sat band instead.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — At least 5 cm margin? Joint above and below included? Oil markers cut through by a slice? | Extend the stack if the mass is clipped. Ensure at least one slice passes through each oil marker to confirm the imaged mass corresponds to the clinical finding |
| **FOV & parameter consistency** — FOV, resolution, and signal settings consistent? | Copying slices transfers only geometry (position, angulation, slice count) — it does not copy FOV, matrix, or other parameters. Manually set these before copying slices. Also copy phase encoding direction |
| **Fat sat on post-contrast T1 (#7)** — Is fat saturation enabled? | Easily forgotten. Check the first image: subcutaneous fat must be dark and soft-tissue contour should be well-defined. If fat is bright, fat sat is off — stop and re-run with fat sat enabled |
| **TR of post-contrast T1 (#7)** — TR within acceptable T1 range after auto-lengthening? | TR auto-lengthens post-contrast to fit all slices with fat sat. Check it stays within: 500–800 ms at 1.5T, 600–900 ms at 3T. If TR exceeds this, T1 contrast degrades — add concatenation instead of letting TR drift further. 
| **Pre-contrast check** — Radiologist reviewed pre-contrast images? | Show pre-contrast images to the radiologist before injecting. Confirm planes, coverage, and image quality are sufficient. Once contrast is in, you cannot go back to change the pre-contrast sequences |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-07 | — | Initial — 6 sequences (+1 optional). STIR long axis + T1 Dixon long axis + T1 non-FS axial + T2 FS axial. T1 Dixon long C + T1 FS TSE axial C post-contrast. Dynamic VIBE optional for post-op. Generic MSK mass template with adjustment strategies |
