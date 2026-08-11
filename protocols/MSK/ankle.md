# Ankle (Routine Ankle MRI — Non-Contrast)

**Version:** 1.0 | **Date:** 2026-08-11 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first. Adjust body position so the affected leg is centred in the magnet. Foot in neutral or slight plantarflexion — dorsiflexion tenses the tendons and can mask tenosynovitis; excessive plantarflexion relaxes the ligaments and can obscure a partial tear.
- **Coil:** Dedicated foot and ankle coil. Place a blue incontinent sheet over the coil for hygiene. Centre over the tibial plafond (ankle joint line).
- **Laser Landmark:** Ankle joint line, just inferior to the medial malleolus.
- **Immobilization:** Place soft pads within the foot and ankle coil to pad any empty space. Place a mattress over both feet and ankles and secure with a strap.
- **IV Access:** Not required for this non-contrast protocol. [Confirm — add IV if contrast is indicated for specific clinical question.]

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `pd+t2_tse_fs_sag_ankle` | Sagittal | ∥ tibial plafond (ankle joint line) — planned from axial localizer | Medial malleolus → lateral malleolus. FOV: above tibial plafond → plantar calcaneus | **None** |
| 2 | `pd_space_sag_p4_ankle` | Sagittal | Copy Slice from #1 | Copy coverage from #1. Isotropic voxels for MPR | **None** |
| 3 | `MPR` | Coronal + Axial | Reformatted from #2 | — | — |
| 4 | `t1_tse_tra_ankle` | Axial | ∥ tibial plafond — planned from sagittal #1 | Above tibiofibular syndesmosis → base of 5th metatarsal. Both malleoli in FOV | **None** |
| 5 | `t2_tse_fs_tra_ankle` | Axial | Copy Slice from #4 | Copy coverage from #4 | **None** |
| 6 | `pd_tse_fs_cor_ankle` | Coronal | ∥ intermalleolar line (bimalleolar axis) — planned from axial #4 | Navicular anteriorly → past posterior border of talus. FOV: above tibial plafond → plantar calcaneus | **None** |

---

## 3. Coverage & Plane Planning

**Sagittal**

- **Coverage:** Slice direction: medial malleolus → lateral malleolus. FOV: above tibial plafond (myotendinous junction of the deep flexors) → plantar skin margin (plantar fascia).
- **Why:** The sagittal plane profiles the talar dome cartilage from anterior to posterior — osteochondral lesions (OCL) are most commonly anterolateral and posteromedial, and sagittal is the primary cartilage survey plane. The Achilles tendon and plantar fascia are seen in long axis. Malleolus-to-malleolus coverage ensures both medial and lateral ligament complexes are swept through.

**Axial**

- **Coverage:** Slice direction S→I: above tibiofibular syndesmosis → base of 5th metatarsal. FOV: navicular anteriorly; remainder to skin margin. Angulation: parallel to the tibial plafond — a true axial cuts the joint obliquely, distorting ligament cross-sections.
- **Why:** The axial plane is the ligament and tendon cross-section plane — ATFL, CFL, PTFL, deltoid components, syndesmosis, and all tendons (peroneals, flexors, extensors) are seen in short-axis. Extending above the syndesmosis captures the AITFL and interosseous membrane — high ankle sprains are missed if coverage stops at the joint line. Extending to the base of the 5th metatarsal captures the peroneus brevis insertion — same inversion injury mechanism as ATFL tears; avulsion fractures and tendinopathy at this site are missed if the stack stops at the calcaneus. Anterior FOV to the navicular includes the extensor tendons (tibialis anterior, EHL, EDL) — anterior ankle impingement and extensor tenosynovitis are assessed here.

**Coronal**

- **Coverage:** Slice direction: navicular → past posterior border of talus. FOV: above tibial plafond → plantar skin margin. Angulation: parallel to the intermalleolar line (bimalleolar axis).
- **Why:** The coronal plane is the long-axis view of the deltoid ligament (medial) and lateral ligament complex — these run superior-inferior and are profiled in full length here. The weight-bearing talar dome cartilage is seen in cross-section. Parallel to the bimalleolar axis ensures both malleoli and their attached ligaments are in the same plane, not tilted out. Posterior margin stops at the posterior talus — everything behind this (PTFL, os trigonum, Achilles, calcaneus) is assessed on sagittal and axial; extending further posterior adds scan time with no diagnostic yield in this plane.

---

## 4. Sequence Rationale

### Core Strategy

The ankle protocol assesses the ligaments (ATFL, CFL, PTFL, deltoid complex, syndesmosis), the talar dome cartilage (osteochondral lesions), the tendons (peroneals, flexors, extensors, Achilles), and the plantar fascia. Planes are aligned to the ankle joint, not true anatomical axes — a true sagittal cuts through one malleolus only; an oblique alignment following the joint line captures both.

The sagittal plane carries two sequences: a dual-echo PD+T2 FS for anatomy-and-fluid in one plane, and a 3D PD SPACE isotropic acquisition with MPR that replaces dedicated 2D coronal and axial anatomy sequences. The axial plane pairs a non-FS T1 with a FS T2 — anatomy and fluid side by side, same cross-section, same logic as the hip coronal pair. PD FS coronal completes the protocol for collateral ligaments and weight-bearing cartilage.

---

### Pre-Contrast

**PD+T2 TSE FS sagittal (#1):** The **dual-echo sagittal survey**. PD (short TE, high SNR) gives sharp ligament and tendon anatomy — the Achilles tendon, plantaris, and deep flexors in long axis. T2 (long TE) makes fluid maximally bright. FS is essential: Kager's fat pad and marrow would otherwise obscure fluid at the talar dome. Two contrasts, one scan time. The sagittal plane profiles the talar dome from anterior to posterior — osteochondral lesions, subchondral marrow edema, and joint effusion are assessed here.

**PD SPACE sagittal P4 isotropic (#2):** The **primary anatomy sequence** — one 3D acquisition that replaces dedicated 2D coronal and axial anatomy scans. While #1 answers *is there fluid?*, this answers *what does the structure look like?* PD is chosen over T2 for higher SNR and shorter TE, giving sharper anatomical detail and cleaner MPR reformats. FS is not applied: fat provides essential tissue contrast — the dark ligaments and tendons stand out against bright fat. The sagittal acquisition plane is the shortest slab dimension (M-L), minimising scan time, while profiling the talar dome and Achilles in their primary axis. Isotropic voxels allow reformatting in any plane at near-source resolution.

**MPR (#3):** Coronal and axial reformats from the 3D PD SPACE (#2), reconstructed inline without additional scan time.

**T1 TSE axial (#4):** The **anatomy and marrow sequence** in the axial plane. Non-FS T1 leaves fat bright — dark ligaments (ATFL, CFL, PTFL, deltoid, syndesmosis) stand out against bright fat with the sharpest possible margins. T1 is the most sensitive sequence for marrow: normal talar and tibial marrow is T1-bright; marrow replacement (OCL bed, contusion, stress fracture) is T1-dark. The axial plane is the only cross-section where all ligaments and tendons are seen simultaneously in short-axis.

**T2 TSE FS axial (#5):** The **fluid-sensitive counterpart** to #4, in the same axial plane. T2 with FS makes fluid in torn ligaments, tenosynovitis, joint effusion, and marrow edema maximally conspicuous. Paired with the T1 axial (#4), the same cross-sections are seen in two contrasts — T1 for structure and marrow, T2 FS for fluid. This is the same "anatomy + fluid side by side" logic as the hip T1/T2 FS coronal pair.

**PD TSE FS coronal (#6):** The **collateral ligament and cartilage sequence**. The coronal plane is the long-axis view of the deltoid ligament (medial) and lateral ligament complex — these run superior-inferior and are profiled in full length here. The weight-bearing talar dome cartilage is seen in cross-section — osteochondral lesion depth and subchondral marrow edema are measured in this plane. PD is chosen over T2 for higher SNR — the collateral ligaments are thin, linear structures that need signal for crisp margins, not extra fluid sensitivity. FS makes subchondral marrow edema bright beneath OCLs and distinguishes cartilage from adjacent joint fluid.

---

## 5. Q&A: Sagittal Alignment

**Sagittal alignment — foot long axis vs perpendicular to intermalleolar line?**

Align the sagittal to the foot's long axis, not perpendicular to the intermalleolar line. The foot naturally sits in ~15° external rotation relative to the bimalleolar axis — forcing the sagittal perpendicular to the intermalleolar line cuts obliquely through the talar dome and the Achilles tendon, the two structures you most need in true long axis. The talar dome is profiled best along the dorsiflexion/plantarflexion arc, which follows the foot. Aligning to the foot also keeps the Achilles from origin to insertion in-plane.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Axial coverage** — Above the syndesmosis included on axials? | High ankle sprains (AITFL, interosseous membrane) are missed if the axial stack stops at the joint line. Confirm coverage extends above the tibiofibular syndesmosis on both axials |
| **Coronal angulation** — #6 truly parallel to the intermalleolar line? | If the coronal is tilted, one malleolus and its attached ligaments are out of plane — the deltoid or lateral complex appears foreshortened or absent. Confirm both malleoli are visible on the same coronal slice at the joint level |
| **3D SPACE coverage** — Entire ankle covered? MPR not truncated? | If the 3D slab is too small, reformatted edges are clipped. Confirm coverage from medial to lateral malleolus and above tibial plafond to plantar calcaneus |
| **Achilles and plantar fascia** — Both fully included in the sagittal FOV? | A tight FOV clips the Achilles insertion or plantar fascia origin. Confirm the entire calcaneus is inside the FOV on sagittal sequences |
| **R/L labeling** — Correct side confirmed on all sequences? | The ankle is unilateral — a mislabeled side can lead to a wrong-site report. Verify the correct side is annotated on every sequence before sending |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-11 | — | Initial — 6 sequences. Dual-echo PD+T2 FS sag + 3D PD SPACE sag + MPR + T1 axial + T2 FS axial + PD FS coronal. Non-contrast ankle protocol |
