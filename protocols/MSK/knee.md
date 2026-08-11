# Knee (Routine Knee MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-07 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first. Knee in the magnet isocentre. The joint should be in neutral rotation with the patella facing anteriorly — external or internal rotation distorts the cruciate ligament course on sagittal images.
- **Coil:** Dedicated knee coil or flex coil wrapped around the knee. Centre over the joint line — palpate the gap between the femoral condyles and tibial plateau.
- **Laser Landmark:** Joint line, just inferior to the patella.
- **Immobilization:** Sandbags alongside the leg to prevent motion. Pad the contralateral leg for comfort.
- **IV Access:** 20G (pink) in the contralateral arm. Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_fs_sms_sag_knee` | Sagittal Oblique | ∥ lateral femoral condyle long axis (∥ ACL course) — planned from axial localizer | Medial femoral condyle → lateral femoral condyle (entire joint). FOV includes patella to popliteal fossa | **None** |
| 2 | `pd_space_sag_cs6_iso_knee` | Sagittal Oblique | Copy Slice from #1 | Copy coverage from #1. Isotropic voxels for MPR | **None** |
| 3 | `MPR` | Coronal + Axial | Reformatted from #2 | — | — |
| 4 | `t1_se_tra_knee` | Axial Oblique | ⟂ coronal plane, ∥ tibial plateau — planned from sagittal #1 | Above patella → below tibiofibular joint. Joint line and menisci centred in the stack | **None** |
| 5 | `pd+t2_tse_fs_tra_knee` | Axial Oblique | Copy Slice from #4 | Copy coverage from #4 | **None** |
| 6 | `pd_tse_fs_cor_knee` | Coronal Oblique | ⟂ knee joint (⟂ tibial plateau) — planned from sagittal #1 | Half of patella anteriorly → popliteal fossa posteriorly | **None** |

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| — | **Contrast** | — | Standard dose. Inject at 2 mL/s. | — | — |
| 7 | `t1_tse_fs_sag_knee_C` | Sagittal Oblique | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 8 | `t1_tse_fs_tra_knee_C` | Axial Oblique | Copy Slice from #4 | Copy coverage from #4 | **None** |
| 9 | `t1_tse_fs_cor_knee_C` | Coronal Oblique | Copy Slice from #6 | Copy coverage from #6 | **None** |

---

## 3. Plane Positioning

All planes are aligned to the knee joint, not true anatomical axes:

- **Sagittal oblique:** aligned parallel to the long axis of the lateral femoral condyle on the axial view. The ACL originates at the posteromedial aspect of the lateral femoral condyle and inserts at the anteromedial tibial spine — it runs posterolateral to anteromedial, not straight sagittal. The lateral femoral condyle's long axis naturally follows this oblique course. Aligning the sagittal plane parallel to it profiles the ACL along its full length. A true sagittal cuts the ACL obliquely — it appears thinned or absent even when intact. Coverage: medial femoral condyle → lateral femoral condyle. FOV includes patella anteriorly to popliteal fossa posteriorly.

- **Axial oblique:** parallel to the tibial plateau on the coronal plane AND parallel to the meniscal plane (tibial articular surface) on the sagittal plane. This gives a true cross-section through the menisci — if tilted relative to either reference, the meniscus appears artefactually thickened from partial-volume averaging. Coverage: above patella → below tibiofibular joint; joint line centred in the stack.

- **Coronal oblique:** perpendicular to the knee joint (perpendicular to the tibial plateau). Coverage: half of patella anteriorly → popliteal fossa posteriorly.

---

## 4. Sequence Rationale

### Core Strategy

The knee protocol assesses the menisci (tears, degeneration, root avulsion), cruciate ligaments (ACL, PCL), collateral ligaments (MCL, LCL), articular cartilage, extensor mechanism, and bone marrow. Planes are aligned to joint-specific landmarks, not true anatomical axes — each plane is prescribed to profile the target structures without obliquity.

The 3D PD SPACE with compressed sensing is the centrepiece — one isotropic acquisition with MPR replaces dedicated 2D coronal and axial anatomy sequences. T2 FS sagittal provides the fluid-sensitive overview in the ACL plane. A true SE (non-turbo) T1 is kept for sharp meniscal morphology that TSE blurs. Dual-echo PD+T2 axial gives two contrasts from one scan. Three-plane T1 FS post-contrast completes the protocol for synovium, meniscal repair, and osteochondral enhancement.

---

### Pre-Contrast

**T2 TSE FS sagittal SMS (#1):** The sagittal plane profiles the ACL, PCL, and meniscal horns. T2 is chosen over PD here because the primary question is *is there fluid?* — T2's longer TE makes fluid maximally bright, and FS suppresses the abundant knee fat (Hoffa's pad, subcutaneous fat, marrow) that would otherwise obscure it. The ACL runs from the medial aspect of the lateral femoral condyle to the anterior tibial spine; the PCL runs from the lateral aspect of the medial femoral condyle to the posterior tibia. The meniscal horns are seen as dark triangles — fluid signal within the triangle extending to an articular surface is a tear. Bone marrow edema, joint effusion, and popliteal cysts are bright against dark fat.

**PD SPACE sagittal CS6 isotropic (#2):** The **primary anatomy sequence** — one 3D acquisition that replaces dedicated 2D coronal and axial anatomy scans. While #1 (T2 FS) answers *is there fluid?*, this sequence answers *what does the structure look like?* PD is chosen over T2 for higher SNR and shorter TE, giving sharper anatomical detail and cleaner MPR reformats. FS is not applied: fat provides essential tissue contrast — the dark meniscus and ligaments stand out against bright fat. The sagittal acquisition plane profiles the ACL and menisci along their primary axis. Isotropic voxels allow reformatting in any plane at near-source resolution — a meniscal tear confirmed in two orthogonal planes on MPR is real, not partial-volume artifact from a curved surface. Articular cartilage is assessed on thin reformats through the weight-bearing surfaces.

**MPR (#3):** Coronal and axial reformats from the 3D PD SPACE (#2), reconstructed inline without additional scan time.

**T1 SE axial (#4):** The **meniscal extrusion sequence**. The meniscus is short-T2 fibrocartilage — dark on T1 against bright fat. The question is whether it protrudes beyond the tibial margin, and by how much — that boundary must be razor-sharp to measure. TSE blurs short-T2 tissues; true SE preserves the crisp dark triangle. Fat is left bright as the measurement background, and the axial plane is the cross-section where extrusion is seen. Also shows parameniscal cysts and patellofemoral morphology (trochlear depth, patellar tilt). The sagittal and coronal planes are covered anatomically by the 3D PD SPACE MPR (#3); this fills the gap — the sharpest possible meniscal margin, in the one plane where extrusion is measured.

**PD+T2 TSE FS axial (#5):** The **side-by-side fluid-and-anatomy sequence**. The axial plane is the only cross-section where the medial and lateral compartments, joint recesses, and collateral ligaments can be compared within the same slice — symmetry is instantly assessed. FS is essential: the joint recesses and meniscal margins are surrounded by fat; without it, a small amount of fluid is invisible. PD and T2 are acquired together as a dual echo — PD (short TE) for sharp meniscal and ligament anatomy, T2 (long TE) for fluid conspicuity in tears and recesses. Two contrasts, one scan time.

**PD TSE FS coronal (#6):** The **collateral ligament and cartilage sequence**. The coronal plane is the long-axis view of the MCL and LCL — these ligaments run superior-inferior and are profiled in their full length here. The meniscal bodies are seen in cross-section (the mid-portion between the horns) — a radial tear through the meniscal body or a root avulsion at the tibial attachment is assessed. Articular cartilage thickness through the weight-bearing femoral condyles and tibial plateaus is measured in this plane. PD is chosen over T2 for higher SNR — the collateral ligaments are thin, linear structures that need signal for sharp margins, not extra fluid sensitivity. FS is essential because fat runs alongside the ligaments and would otherwise obscure their margins; with fat suppressed dark, the ligament stands out and any fluid tracking along a sprained or torn ligament is conspicuously bright.

---

### Post-Contrast

Contrast is used to answer three questions in the knee: is there synovitis (inflammatory, infective, or post-surgical), is a meniscal repair healing or re-torn (enhancing tissue at the repair site), and is there an osteochondral lesion with active inflammation at the bone-cartilage interface. T1 FS is the contrast mechanism in all three planes — enhancing tissue appears bright against dark fat.

**T1 TSE FS sagittal (#7):** The sagittal plane profiles the ACL, PCL, menisci, and synovium. Enhancing synovium indicates synovitis; enhancement within the meniscal substance or at a post-repair site suggests healing tissue or re-tear. Osteochondral lesions enhance at the bone-cartilage interface beneath the defect.

**T1 TSE FS axial (#8):** The axial plane cross-sections the patellofemoral compartment, medial and lateral joint recesses, popliteal fossa, and patellar/quadriceps tendons. Enhancing joint recesses indicate synovitis. Enhancing parameniscal soft tissue suggests a parameniscal cyst or post-surgical granulation. The patellar and quadriceps tendons are assessed for tendinopathy or post-repair enhancement.

**T1 TSE FS coronal (#9):** The coronal plane provides side-by-side comparison of the medial and lateral compartments, meniscal bodies and roots, and collateral ligaments. Enhancing meniscal root indicates root avulsion or healing after repair. Asymmetric compartment enhancement suggests unilateral synovitis.

---

## 5. ACL Reconstruction Variation — Oblique Coronal

When the indication is post-ACL reconstruction graft assessment, add an oblique coronal sequence to the pre-contrast set:

- `pd_tse_fs_cor_oblique_knee` — prescribed from the sagittal oblique (#1), parallel to the ACL graft course (perpendicular to the Blumensaat line). Coverage: femoral tunnel → tibial tunnel.

The standard coronal oblique (#6) parallels the posterior femoral condyles and is perpendicular to the tibial plateau — it cuts the graft obliquely. The oblique coronal parallels the graft itself, profiling the femoral tunnel, the full graft, and the tibial tunnel in one plane.

What the oblique coronal assesses that the standard planes may miss:

- **Tunnel position:** the femoral tunnel must be at the anatomical ACL footprint (posteromedial aspect of the lateral femoral condyle). A malpositioned femoral tunnel is the most common cause of graft failure. The oblique coronal shows the femoral tunnel entrance face-on; the sagittal oblique does not show medial-lateral offset.
- **Graft continuity:** the graft is seen from femoral tunnel to tibial tunnel in a single plane. A partially intact graft can appear absent on sagittal if the slice passes obliquely through it.
- **Tunnel osteolysis:** cystic widening around the tunnels precedes failure and is seen circumferentially in this plane.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Sagittal obliquity** — Sagittal plane truly parallel to the ACL? | A true sagittal cuts the ACL obliquely — it appears thinned or absent even when intact. Align with the lateral femoral condyle long axis. The ACL should appear on ≥2–3 consecutive sagittal slices; if visible on only one, the plane is off |
| **3D SPACE coverage** — Entire joint covered? MPR not truncated? | If the 3D slab is too small, reformatted edges are clipped. Confirm coverage from medial to lateral femoral condyles and patella to popliteal fossa. Check that MPR reformats are complete before moving on |
| **Meniscal root coverage** — Coronal plane includes the tibial root attachments? | Root avulsion is missed if coverage stops at the joint line. The coronal plane must extend far enough to include both the medial and lateral tibial root insertions |
| **Popliteal fossa coverage** — Posterior capsule and popliteal vessels included? | Baker's cyst and posterior capsule pathology are easily clipped if the FOV is too tight posteriorly. Confirm the popliteal fossa is within the FOV on all planes |
| **Patella coverage** — Patella and quadriceps tendon fully included? | Easily clipped on axial planes. Confirm full patella and quadriceps tendon insertion are within the FOV |
| **Slice consistency** — Slice thickness and gap uniform across all sequences in the same plane? | Different slice thickness / inconsistent gapping breaks copy slice |
| **Post-contrast** — All three planes acquired? Allow time for synovial enhancement? | Enhancement can be subtle. Acquire all three planes and allow ~3–5 min post-injection for synovial enhancement before starting. Check enhancing tissue against pre-contrast T1 SE (#4) to confirm it is true enhancement, not intrinsic T1 signal |
| **R/L labeling** — Correct side confirmed on all sequences? | The knee is unilateral — a mislabeled side can lead to a wrong-site report. Verify the correct side is annotated on every sequence before sending |
| **Metal artifact** — Prior ACL reconstruction with metallic fixation? | Metallic interference screws distort B0 — spectral FS may fail near the tunnels, producing geographic bright patches that mimic or mask pathology. Swap to STIR or Dixon for FS sequences if metal is present |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-07 | — | Initial — 9 sequences (+1 variation). T2 FS sag SMS + 3D PD SPACE CS6 iso + MPR + T1 SE axial + dual-echo PD+T2 FS axial + PD FS coronal. Three-plane T1 FS post-contrast. ACL reconstruction variation with oblique coronal |
