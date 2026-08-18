# Hip Prosthesis (Hip Arthroplasty MRI — Metal Artifact Reduction + Contrast)

**Version:** 1.0 | **Date:** 2026-08-18 | **Scanner:** [Confirm 1.5T/3T — 1.5T preferred for metal imaging]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first. Legs neutral or slight internal rotation, symmetrical. Pillow under the knees for comfort — this population is often elderly and in pain.
- **Coil:** Body matrix coil anteriorly + spine array posteriorly — same as the routine hip. Centre over the affected hip joint.
- **Laser Landmark:** Greater trochanter of the affected side — palpate at the widest point of the lateral hip.
- **Immobilization:** Strap both feet together and place sandbags beside the legs. Motion control matters more than in the routine protocol — the pre/post pairs must not shift, or the subtraction breaks.
- **IV Access:** Required — IV gadolinium.
- **Implant Safety:** Confirm the implant is MR conditional and document it before scanning [Confirm institute policy].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_cor_semac15_hip` | Oblique Coronal | ∥ femoral stem long axis — planned from axial localizer (≈ true coronal in neutral positioning) | FOV: Iliac crest → below stem tip (≈5 cm distal to stem tip). Slice coverage: anterior femoral cortex → posterior femoral cortex | **None** |
| 2 | `t2_tirm_cor_semac10_hip` | Oblique Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `t2_tirm_tra_semac8_hip` | True Axial | ⟂ femoral shaft axis — planned from coronal #1 | Above acetabular roof → below stem tip | **None** |
| 4 | `t1_tse_tra_semac8_hip` | True Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |
| — | **Contrast** | — | IV gadolinium [Confirm dose/rate] | — | — |
| 5 | `t1_tse_tra_semac8_hip_C` | True Axial | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 6 | `t1_tse_cor_semac15_hip_C` | Oblique Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |

---

## 3. Coverage & Plane Planning

**Oblique Coronal (∥ femoral stem long axis)**
- **Coverage:** Slice direction A→P: anterior femoral cortex → posterior femoral cortex — the stack sweeps the entire cup and stem through their full AP depth. FOV S→I: iliac crest → below the stem tip (≈5 cm distal to the tip).
- **Angulation:** Slice box aligned ∥ femoral stem long axis. In neutral positioning this is ≈ true coronal — the shaft runs vertically in the coronal plane — but the stack must be tilted to the stem axis when the femur is bowed, the hips are flexed (knee pillow), or the stem sits varus/valgus: the stem then leaves the coronal plane and a straight stack cuts it obliquely.

**True Axial**
- **Coverage:** Slice direction S→I: above acetabular roof → below stem tip — the same S→I window as the coronals.
- **Angulation:** ⟂ femoral shaft axis, sections the stem in true cross-section, orthogonal to the coronal pair (planes parallel and perpendicular to the implant axis).

**Why**
- The bone-implant interface is the target. The coronal profiles it along the implant's length — cup, calcar (classic proximal osteolysis site), modular junction, stem tip; the axial profiles it around the full circumference per level (medial, lateral, anterior, posterior) and maps the posterior soft tissues — sciatic nerve, gluteal compartment — and pseudotumor.
- Both planes extend below the stem tip — tip osteolysis, tip fracture, and distal loosening hide below it. Proximal extension to the iliac crest keeps the gluteal origins and iliopsoas.
- Angulation keeps the stem in the plane it is assessed in: coronal ∥ stem stays in-plane along its length; axial ⟂ shaft keeps a circular cross-section — a tilted stack smears the interface.

**Unilateral focus:** Centre the affected hip. Both hips in the FOV is ideal for side-by-side comparison, but SEMAC factors carry a large time penalty — [Confirm institute practice on bilateral coverage].

---

## 4. Sequence Rationale

### Core Strategy

The routine hip protocol answers: labrum, cartilage, FAI morphology, marrow. The arthroplasty protocol answers: periprosthetic osteolysis, adverse local tissue reaction (ALTR / pseudotumor), infection, aseptic loosening, periprosthetic fracture, and residual tendon damage — all around a metal implant that distorts the field and defeats normal fat suppression. Everything in this protocol is shaped by the metal.

### How this differs from the standard hip protocol — and why

**The planes shrink from four to two.** The routine hip runs coronal, sagittal, axial, and oblique axial (the FAI plane) — the sagittal profiles the labral ring and the oblique axial measures the alpha angle on the native femoral neck. The arthroplasty protocol runs coronal and axial only: the labrum and the native femoral head-neck junction are gone, so both planes have no target left. The questions move to the periprosthetic bone and soft tissue interfaces, which two orthogonal planes survey adequately.

**The fat suppression method changes from Dixon / spectral FS to TIRM.** Both spectral fat saturation and Dixon depend on field homogeneity — both fail in the steep B0 gradients around metal. TIRM nulls fat by inversion recovery, which is independent of B0 homogeneity, and is the only FS method that survives next to an implant.

**The post-contrast sequence becomes non-FS T1 pre/post pairs.** The routine protocol's post-contrast sequence is FS T1 — fat-saturated T1 cannot be run near metal. Instead, matched-geometry non-FS T1 pairs (pre and post) are acquired and enhancement is extracted by subtraction.

**Every sequence gains metal artifact reduction.** The routine protocol has none. Here every sequence runs SEMAC (15/10/8) for through-plane correction plus VAT and high readout bandwidth for in-plane correction — together the WARP package.

**Coverage extends below the stem tip.** The routine protocol covers iliac crest → lesser trochanter. The arthroplasty protocol must survey the whole implant: osteolysis and fracture occur along the full stem and at the tip, so coverage runs iliac crest → below the stem tip.

**The protocol becomes contrast-enhanced.** The routine hip is non-contrast. Here IV gadolinium is used because infection, ALTR, and the loosening membrane are enhancement questions.

### SEMAC factor logic

- SEMAC adds phase encoding along the slice direction to correct through-plane slice distortion; correction strength and scan time both scale with the number of encoding steps.
- **Coronal SEMAC-15:** the slice direction (A→P) crosses the curved anterior/posterior surfaces of the cup and stem — through-plane field gradients are at their worst here, and the coronal is the primary interface plane.
- **Axial SEMAC-8:** the slice direction runs parallel to the stem long axis. The field gradients around a long cylinder are radial — i.e., in-plane — where VAT + high readout bandwidth do the work. Fewer steps keep the scan short.
- **TIRM coronal SEMAC-10:** TIRM + SEMAC is the longest sequence in the protocol; 10 steps instead of 15 keeps it within a practical scan time while retaining adequate through-plane correction.

### Pre-Contrast

**T1 TSE coronal SEMAC-15 (#1):** The **anatomy and interface baseline**. T1 without FS gives the sharpest implant-bone margins: the cup-acetabulum interface, the stem-femur interface, and the calcar region. Normal marrow stays T1-bright, so the intermediate-signal fibrous membrane of osteolysis stands out against it. Non-FS is not a choice — spectral FS fails near metal. This sequence is also the subtraction baseline for #6.

**T2 TIRM coronal SEMAC-10 (#2):** The **fluid-sensitive coronal**. TIRM is the fat-suppression method that survives metal: inversion recovery nulls fat independent of B0 homogeneity, where spectral FS and Dixon both degrade. It shows joint effusion, periprosthetic fluid collections, osteolysis (fluid-bright), the cystic/solid pseudotumor of ALTR, marrow edema around the stem (stress reaction or infection), and abductor tendon tears.

**T2 TIRM axial SEMAC-8 (#3):** The **fluid-sensitive axial**. Cross-sections through the stem and cup show the periprosthetic membrane around the full circumference. Posterior soft tissues — sciatic nerve, gluteal compartment — and pseudotumor extent are assessed here. SEMAC-8: the axial slice direction is along the stem axis, so distortion is mostly in-plane (see SEMAC factor logic).

**T1 TSE axial SEMAC-8 (#4):** The **axial anatomy and marrow counterpart** to #3 — and the subtraction baseline for #5. Same geometry as #3, so anatomy and fluid sit side by side.

**Contrast:** IV gadolinium — the prosthesis questions are enhancement questions: periprosthetic joint infection (enhancing synovium, sinus tract, abscess), ALTR (enhancing inflammatory pseudotumor), aseptic loosening (enhancing fibrous membrane at the interfaces). [Confirm dose/rate.]

### Post-Contrast

**T1 TSE axial SEMAC-8 C (#5):** Post-contrast **axial first** — the enhancing membrane is best profiled in cross-section around the stem/cup circumference, and enhancement fades with time. Subtraction versus #4 removes the T1-bright fat that cannot be spectrally suppressed, isolating true enhancement.

**T1 TSE coronal SEMAC-15 C (#6):** Post-contrast coronal — enhancement along the length of the cup and stem interfaces, the abductor tendons, and the iliopsoas. Subtraction versus #1.

---

## 5. Pathology-Based Variations

**Suspected periprosthetic fracture**
- Add a sagittal `t1_tse_sag_semac8_hip` along the femoral shaft — a fracture line along the anterior/posterior cortex is best profiled sagittally.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Implant documentation & SAR** — MR conditional confirmed and label conditions read? | Check the implant's static field limit and SAR limit. Run in **Normal mode only — never First Level** (the label limit matches Normal mode's 2 W/kg ceiling) and watch the SAR display: SEMAC re-excites each slice ~31× and TIRM adds inversion pulses, making this the RF-heavy pair. If SAR is exceeded, reduce flip angle / lengthen TR rather than accept First Level |
| **Coverage: Stem tip included** — Coronal and axial FOV extend below the tip? | Tip osteolysis, tip fracture, and distal loosening hide below the tip. If the stack stops at the lesser trochanter (routine hip habit), the distal stem is missed |
| **SEMAC + VAT (WARP)** — factors set, in-plane correction active? | Add SEMAC steps when through-plane distortion persists — curved/smeared interfaces or signal pile-up beyond the implant margins; reduce when scan time is prohibitive (time ∝ 2×steps+1). Add readout BW when in-plane artifact or VAT blur remains at the margins. VAT auto-active — never switch off: SEMAC alone corrects only through-plane |
| **Motion** — Pre/post pair moved between scans? | SEMAC + TIRM are long scans in a painful elderly population; motion breaks the subtraction — re-acquire the moved sequence |
| **R/L labelling** — Correct side labelled on all sequences? | Unilateral exam — a wrong side label misattributes pathology |
| **Scanner field strength** — 1.5T preferred | Metal artifact is smaller at 1.5T than 3T (less susceptibility, lower SAR). At 3T expect more pronounced artifact despite SEMAC |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-18 | — | Initial — 6 sequences + contrast. T1 TSE cor SEMAC-15 + T2 TIRM cor SEMAC-10 + T2 TIRM tra SEMAC-8 + T1 TSE tra SEMAC-8, pre/post IV gadolinium, matched-geometry subtraction pairs |
