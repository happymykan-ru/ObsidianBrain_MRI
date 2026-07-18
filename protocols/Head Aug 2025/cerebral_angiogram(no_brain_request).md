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
RESOLVE DWI with GRAPPA ×2. 3 orthogonal directions averaged to trace. Acute ischaemia detection — essential in an angiogram protocol to identify territory already infarcted vs tissue at risk. RESOLVE reduces susceptibility distortion at skull base.

**`TOF_3D_multi-slab` (#4)**
3D time-of-flight MR angiography, multi-slab acquisition. The primary diagnostic sequence. Sequential thin slabs are acquired perpendicular to arterial flow to maximise inflow enhancement — fresh unsaturated spins entering each slab appear bright against saturated stationary tissue. Multi-slab reduces saturation effects that degrade single-slab TOF over long travel distances. Sat band placed **superior** to suppress venous flow signal descending from above, keeping the TOF arterial-dominant.

*Coverage:* Image position is copied at the circle of Willis level. Slab spans **carotid siphon → above corpus callosum** (~60–80 mm), typically across 3–4 overlapping thin 3D slabs (~20–30 mm each, ~25% overlap). Inferior boundary must capture the full carotid siphon curve and vertebrobasilar junction — cutting too high misses dissection and aneurysm at the petrous-cavernous junction. Superior boundary captures the distal ACA (pericallosal, callosomarginal) and MCA candelabra. Slab overlap <25% causes horizontal dark bands at slab junctions (venetian blind artefact).

**Contrast**
Standard dose IV gadolinium. Target ~5 min delay before post-contrast T1 (#5).

**`t1_fl2d_tra_brain_C` (#5)**
Post-contrast 2D FLASH axial. Matches pre-contrast baseline (#2) for enhancement comparison. Post-contrast T1 is included because vascular pathology (vasculitis, tumour encasement, aneurysm wall enhancement) may not be visible on TOF alone.

---

## 4. Pathology-Based Variations

- **Aneurysm screening:** TOF is the primary sequence. If aneurysm is suspected and TOF quality is limited (slow flow, large aneurysm with turbulent dephasing), add post-contrast MRA
- **Dissection:** TOF with fat saturation through the neck if cervical dissection is suspected. Intramural haematoma on T1 FS neck is the key finding
- **Vasculitis:** Post-contrast T1 (#5) is essential — vessel wall enhancement is the primary finding. Consider adding high-resolution T1 FS post-contrast through the circle of Willis
- **AVM / fistula:** Consider adding t2_fl2d (T2* FLASH) post-contrast for venous anatomy
- **Large vessel occlusion (stroke):** DWI (#3) + TOF (#4) provide the core acute stroke workup — territory and vessel status

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack if any sequence is short |
| **TOF** — venous contamination? (sigmoid/transverse sinus bright) | Confirm superior sat band is placed. If venous signal persists, extend or reposition sat band |
| **TOF** — slab boundary artefact? (horizontal dark lines at slab junctions) | Increase slab overlap to ≥25%. If severe, consider single-slab TOF with reduced coverage |
| **TOF** — coverage adequate? Carotid siphon through pericallosal ACA? | Reposition if siphon cut inferiorly or distal ACA missing superiorly |
| **`resolve_3scan_trace_p2`** — true restriction vs T2 shine-through on ADC? | Document true restriction. If distorted at skull base: flip phase-encode (A>>P → P>>A) |
| **`resolve_3scan_trace_p2`** — water peak centred and narrow? | Re-shim if water peak broad or shifted |
| **`t1_fl2d_tra_brain_C`** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection, repeat if extravasation suspected |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-18 | — | Initial — 5 sequences (TOF + basic brain) |
