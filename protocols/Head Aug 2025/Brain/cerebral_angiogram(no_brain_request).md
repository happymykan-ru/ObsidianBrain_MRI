# Cerebral Angiogram (No Brain Request)

**Version:** 1.0 | **Date:** 2026-07-18 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `resolve_3scan_trace_p2` | Axial | Copy Slice from #1 | — | **None** |
| 4 | `TOF_3D_multi-slab` | Axial | ∥ AC-PC line | Carotid siphon → above corpus callosum | **Superior** (venous flow) |
| — | **Contrast** | — | — | — | — |
| 5 | `t1_fl2d_tra_brain_C` | Axial | Copy Slice from #1 | — | **None** |

---

## 3. Sequence Rationale

This is a focused protocol for intracranial arterial imaging. Brain sequences are included for anatomical reference and to rule out concurrent parenchymal pathology, but TOF is the primary diagnostic sequence.

**`t2_tse_tra_brain` (#1)**
Core T2 axial brain anatomy. Reference plane for the protocol. Provides parenchymal context for vascular findings — e.g., territory of an occluded vessel on TOF can be correlated with established infarction on T2.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast 2D FLASH axial. Baseline T1 reference for post-contrast comparison (#5). No sat band: short TR has no slack.

**`resolve_3scan_trace_p2` (#3)**
RESOLVE DWI with GRAPPA ×2. The DWI-TOF pair answers the core acute stroke question: what's already dead vs what's at risk. Infarcted core shows restricted diffusion (bright on DWI, dark on ADC) — this tissue is dead regardless of intervention. The TOF (#4) shows the vessel occlusion. When DWI shows a small lesion but TOF shows a large vessel occlusion, the mismatch is tissue at risk (penumbra) — still salvageable if the vessel is reopened. When DWI already matches the full vascular territory, the infarct is complete and intervention may not change outcome. RESOLVE reduces susceptibility distortion at skull base.

**`TOF_3D_multi-slab` (#4)**
3D time-of-flight MR angiography, multi-slab acquisition. The primary diagnostic sequence. Sequential thin slabs are acquired perpendicular to arterial flow to maximise inflow enhancement — fresh unsaturated spins entering each slab appear bright against saturated stationary tissue. Multi-slab reduces saturation effects that degrade single-slab TOF over long travel distances. Sat band placed **superior** to suppress venous flow signal descending from above, keeping the TOF arterial-dominant.

*Coverage:* Image position is copied at the circle of Willis level. Slab spans **carotid siphon → above corpus callosum** (~60–80 mm), typically across 3–4 overlapping thin 3D slabs (~20–30 mm each, ~25% overlap). Inferior boundary must capture the full carotid siphon curve and vertebrobasilar junction — cutting too high misses dissection and aneurysm at the petrous-cavernous junction. Superior boundary captures the distal ACA (pericallosal, callosomarginal) and MCA candelabra. Slab overlap <25% causes horizontal dark bands at slab junctions (venetian blind artefact). If the lesion or vessel of interest is not fully covered (e.g., high ICA stenosis extending extracranially, distal ACA/MCA pathology), either increase slices per slab or switch to an EC/IC bypass TOF protocol with larger coverage.

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before post-contrast T1 (#5).

**`t1_fl2d_tra_brain_C` (#5)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast baseline (#2) — subtract for pure enhancement map. Post-contrast T1 is included because vascular pathology (vasculitis, tumour encasement, aneurysm wall enhancement) may not be visible on TOF alone.

---

## 4. Pathology-Based Variations

- **Post-coiling:** The post-coiling protocol replaces most of the standard angiogram sequences. Coil mass changes the diagnostic question entirely — before coiling: "is there an aneurysm?"; after coiling: "is it completely occluded? Any neck remnant? Parent vessel compromise?" The coil mass creates severe susceptibility artefact on standard TOF, and post-contrast brain sequences are needed to assess for procedural complications.

  Post-coiling sequences:
  - `t2_tse_tra_brain`
  - `t1_fl2d_tra`
  - `TOF_fl3d_tra` *(pre-contrast — FLASH 3D TOF, less susceptible to coil artefact than multi-slab)*
  - Contrast
  - `TOF_fl3d_tra_C` *(post-contrast, high bandwidth — penetrates coil susceptibility to show residual flow in the aneurysm neck or sac)*
  - `t1_vibe_fs_cor_C` + `MPR`
  - `t1_fl2d_tra_C`

  Key differences from the standard angiogram: pre-contrast TOF switches to FLASH 3D (less susceptibility than multi-slab near the coil). Post-contrast TOF with high bandwidth is the key sequence — it sees past the coil dropout to confirm occlusion or detect residual filling. A full post-contrast brain block (VIBE + MPR + FLASH) is added to assess for procedural complications (ischaemia, haematoma). RESOLVE DWI is omitted — the coil susceptibility would degrade it beyond diagnostic value.

- **Dissection:** Add `t1_tse_fs_tra` through the neck (skull base → C2–C3, 2–3 mm slices). 
    - *Coverage:* The V3 segment is most vulnerable at C1–C2 — exiting the C2 foramen and looping around the C1 lateral mass before piercing the dura, head rotation maximally stretches the vessel here. Skull base captures the V3–V4 junction at dural penetration. C2–C3 inferiorly captures V2 just before the mobile segment. No need below C3 — lower dissections are rare. 
    - *Plane:* Axial, parallel to cervical disc spaces. The vertebral artery runs vertically — true perpendicular cuts show the intramural haematoma as a crisp bright crescent. Any tilt elongates it into a smear indistinguishable from lumen. Spin echo avoids the flow-void and susceptibility artefacts that degrade GRE at the transverse foramina.

- **AVM / fistula:** Add `TWIST_HEAD_ePAT2×3`. Time-resolved MRV capturing dynamic contrast passage — arterial feeders → nidus → early venous drainage in sequential frames (~1–3 s per frame, ePAT ×3).
    - *Plane:* **Sagittal** 3D source for general AVM/fistula — most efficient for whole-head coverage with the fewest slabs. Covers all potential feeders (ICA, ECA, vertebral) and drainers. Consider **coronal** source if the target is specifically the transverse sinus (e.g., transverse-sigmoid dural fistula) — the transverse sinus runs laterally, so a coronal source profiles it in-plane for better spatial resolution along the sinus axis.
    - *Coverage:* Whole skull — temporal bone to temporal bone, vertex to skull base. Include the ECA territory (scalp, meninges) as these are common feeders in dural fistulae.
    - *Timing:* Acquired immediately post-contrast during the first-pass bolus. Start the TWIST acquisition — the first measurement serves as the pre-contrast mask. Inject contrast after the 1st measurement frame with no pause. Subsequent frames track the bolus through arterial → capillary → venous phases.
    - *Contrast:* Use the CeMRA contrast injection protocol (including saline bolus and pause after flush) but at **standard** brain contrast dose — not the CeMRA double-dose. The time-resolved nature of TWIST compensates for the lower dose.
    - *Key finding:* Early venous drainage — veins filling on the same frame as arteries or within 1–2 frames. Normal venous filling should be 4–6 seconds delayed from arterial peak.

- **Vasculitis:** Post-contrast T1 (#5) is essential — vessel wall enhancement is the primary finding. Consider adding high-resolution T1 FS post-contrast through the circle of Willis

---

## 5. Alerts

| Check | Improve |
|---|---|
| **TOF Lesion Coverage** — lesion/vessel of interest fully covered? | If not: increase slices/slab or switch to EC/IC bypass TOF with larger coverage |
| **TOF Anatomical Coverage** — coverage adequate? Carotid siphon through pericallosal ACA? | Reposition if siphon cut inferiorly or distal ACA missing superiorly |
| **TOF** — venous contamination? (sigmoid/transverse sinus bright) | Confirm superior sat band is placed. If venous signal persists, extend or reposition sat band |
| **TOF** — slab boundary artefact? (horizontal dark lines at slab junctions) | Increase slab overlap to ≥25%. If severe, consider single-slab TOF with reduced coverage. Check source images — dark lines can mimic stenosis or occlusion on MIP |
| **`t1_fl2d_tra_brain_C`** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection, repeat if extravasation suspected |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 5 sequences (TOF + basic brain) |
