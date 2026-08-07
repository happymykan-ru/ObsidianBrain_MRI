# Shoulder (Routine Shoulder MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-07 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Patient slightly oblique towards the affected side (supported by sandbags behind the contralateral torso) to bring the shoulder closer to the magnet isocentre for improved B0 homogeneity and SNR.
- **Coil:** Dedicated shoulder coil or flex coil centred over the glenohumeral joint.
- **Laser Landmark:** Coracoid process — palpate just inferior to the lateral clavicle.
- **Immobilization:** Place a mattress over the affected shoulder and strap with a restrainer to eliminate respiratory motion. The affected hand is placed in external rotation and secured by sandwiching between two soft pads — external rotation aligns the supraspinatus tendon in the coronal oblique plane; internal rotation pulls it anteriorly and makes it harder to profile.
- **Breathing:** Shallow breathing — respiratory motion transmits to the shoulder.
- **IV Access:** 20G (pink) in the contralateral arm. Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `pd_tse_fs_tra_shoulder` | Axial Oblique | ∥ supraspinatus course (⟂ glenoid fossa) — planned from coronal scout | AC joint → below axillary recess (quadrilateral space). Medial: enough to include glenoid; lateral: beyond greater tuberosity | **None** |
| 2 | `pd_tse_cor` | Coronal Oblique | ∥ supraspinatus tendon (⟂ glenoid fossa) — planned from axial #1 | Subscapularis/anterior → infraspinatus/posterior. Medial: glenoid fossa; lateral: greater tuberosity | **None** |
| 3 | `t2_tse_fs_cor` | Coronal Oblique | Copy Slice from #2 | Copy coverage from #2 | **None** |
| 4 | `t2_tse_fs_sag` | Sagittal Oblique | ⟂ coronal oblique (∥ glenoid fossa) — planned from axial #1 | Medial glenoid neck → lateral deltoid. Coracoid → scapular spine | **None** |
| 5 | `t1_tse_sag` | Sagittal Oblique | Copy Center from #4 | Copy coverage from #4. 4 mm slice thickness | **None** |

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| — | **Contrast** | — | Standard dose. Inject at 2 mL/s. | — | — |
| 6 | `t1_tse_fs_sag_C` | Sagittal Oblique | Copy Slice from #4 | Copy coverage from #4 | **None** |
| 7 | `t1_tse_fs_tra_C` | Axial Oblique | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 8 | `t1_tse_fs_cor_C` | Coronal Oblique | Copy Slice from #2 | Copy coverage from #2 | **None** |

---

## 3. Plane Positioning

All planes are relative to the glenohumeral joint, not true anatomical axes:

- **Axial oblique:** planned from the coronal scout, perpendicular to the glenoid fossa. Coverage: AC joint → below axillary recess (quadrilateral space). Medial enough to include the glenoid; lateral to skin margin.
- **Coronal oblique:** planned from the axial oblique (#1), parallel to the supraspinatus tendon (~ perpendicular to the glenoid fossa). Coverage: subscapularis anteriorly → infraspinatus posteriorly; medial enough to include the full supraspinatus belly; lateral to skin margin.
- **Sagittal oblique:** planned from the axial oblique (#1), perpendicular to the coronal oblique and parallel to the glenoid fossa. Coverage: medial glenoid neck → lateral deltoid (just past humeral head); FOV includes anterior & posterior skin margin (coracoid → scapular spine).

---

## 4. Sequence Rationale

### Core Strategy

The shoulder protocol assesses the rotator cuff — tendinopathy, partial/full-thickness tears, and muscle atrophy (Goutallier grading) — plus the labrum, biceps anchor, glenohumeral ligaments, AC joint, and subacromial/subdeltoid bursa. All planes are oblique to the glenohumeral joint; true anatomical planes distort the cuff and labrum.

PD exists for anatomy, not pathology detection. In sports MSK, the anatomy *is* the pathology — a 2 mm partial-thickness supraspinatus tear, a frayed labrum, a delaminating articular cartilage defect. These structures are a few millimeters thick and need the highest possible SNR to resolve crisply. PD gives that: short TE, high signal, sharp tissue boundaries. With FS, the dark tendon/cartilage stands against intermediate-bright fluid — enough contrast to see the tear, and the anatomical clarity is what lets you grade it. 

T2 FS then adds maximum fluid sensitivity for tears, edema, and bursitis — the pathology workhorse where conspicuity matters more than anatomical detail. Non-fat-sat PD and T1 are kept for muscle quality and marrow assessment. Three-plane T1 FS post-contrast completes the protocol for synovium, labral, and cuff enhancement.

---

### Pre-Contrast

**PD TSE FS axial (#1):** The axial oblique plane shows the glenoid labrum face-on — anterior, posterior, and superior (biceps anchor) — plus the biceps tendon in the bicipital groove, the glenohumeral ligaments, and the joint recesses. PD with FS gives high-SNR anatomy with fluid made bright: a labral tear appears as fluid signal entering the labral substance, and a joint effusion distends the recesses. This sequence also provides the reference plane for prescribing the coronal and sagittal obliques.

**PD TSE coronal (#2):** The coronal oblique plane profiles the supraspinatus tendon in its long axis, from the supraspinous fossa origin to the greater tuberosity insertion. Fat is left bright (no FS): fatty atrophy of the supraspinatus and infraspinatus muscle bellies is graded on non-fat-sat sequences where T1-bright fat streaks within intermediate muscle signal are directly visible (Goutallier classification). AC joint osteophytes appear as T2-dark projections impinging on the underlying supraspinatus.

**T2 TSE FS coronal (#3):** Same coronal oblique plane as #2, now with T2 and fat saturation for maximum fluid sensitivity. A full-thickness cuff tear appears as fluid signal traversing the tendon from articular to bursal surface; a partial tear shows fluid on one side only. The tear site, mediolateral size, and retraction distance from the greater tuberosity are measured here. Subacromial/subdeltoid bursitis and bone marrow edema are maximally conspicuous against dark fat.

**T2 TSE FS sagittal 3 mm (#4):** The sagittal oblique plane provides cross-sections through all four cuff tendons at a single slice: supraspinatus (superior), infraspinatus (posterosuperior), teres minor (posteroinferior), and subscapularis (anterior). This plane answers which tendon is torn, the cross-sectional area of the tear, and the mediolateral position of the retracted stump. 3 mm slices for fine tendon detail.

**T1 TSE sagittal 4 mm (#5):** Non-fat-saturated T1 in the same sagittal oblique plane — the muscle quality reference. Fatty atrophy appears as T1-bright streaks replacing normal intermediate muscle signal (Goutallier grade). Normal bone marrow is T1-bright; marrow replacement is T1-dark. The acromial shape (type I–III) and the coracoacromial arch are profiled. 4 mm slices — muscle quality does not require tendon-level resolution.

---

### Post-Contrast

**T1 TSE FS sagittal (#6):** Sagittal oblique post-contrast — cross-sections through the capsule, labrum, and cuff tendons. Enhancing synovium indicates synovitis or adhesive capsulitis (thickened enhancing capsule). Contrast entering a labral tear or filling a paralabral cyst confirms the tear. Post-surgical granulation tissue at a cuff repair site enhances. This is the highest-yield post-contrast plane for the labrum and capsular insertion.

**T1 TSE FS axial (#7):** Axial oblique post-contrast — the labrum face-on and the biceps tendon sheath in cross-section. Enhancing tendon sheath: tenosynovitis. Enhancing anterior or posterior labral substance: labral tear. Humeral avulsion of the glenohumeral ligament (HAGL) shows enhancement at the humeral attachment. The axillary recess may show enhancing capsule (capsulitis) or non-enhancing loose bodies.

**T1 TSE FS coronal (#8):** Coronal oblique post-contrast — the supraspinatus tendon in long axis. Intrasubstance enhancement within the tendon suggests a partial tear or post-repair granulation. Enhancing subacromial/subdeltoid bursa: bursitis. Enhancing AC joint: synovitis or osteoarthritis.

---

## 5. Motion Artifact Variation — BLADE

If breathing artifacts degrade the image despite shallow breathing instruction and immobilization, replace all conventional TSE sequences with BLADE (PROPELLER) equivalents:

- `pd_blade_fs_tra_shoulder`
- `pd_blade_cor`
- `t2_blade_fs_cor`
- `t2_blade_fs_sag`
- `t1_blade_sag`

Post-contrast T1 FS sequences remain conventional TSE where possible (they are short and acquired quickly), but may also be swapped to BLADE if motion persists.

**Trade-off:** BLADE oversamples the k-space centre with rotating blades, making it robust to motion — ghosting and blurring from patient movement are markedly reduced. The cost is slightly lower SNR, longer scan time, and a characteristic mild blurring from blade interpolation. For gross pathology (full-thickness cuff tear, bursitis, marrow edema, muscle atrophy grading) BLADE is adequate. For fine anatomical detail — subtle labral fraying, small partial-thickness articular-surface tears, delaminating cartilage — conventional TSE is superior because the sharper tissue boundaries matter. Use BLADE only when motion would otherwise render the conventional sequences non-diagnostic.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **Plane obliquity** — Axial truly ⟂ glenoid? Coronal truly ∥ supraspinatus? | True axial/coronal/sagittal cut obliquely through the cuff and labrum — partial tears and labral separation are missed. Verify on the axial oblique that the glenoid is profiled face-on and the coronal is prescribed parallel to the supraspinatus tendon |
| **Sagittal slice thickness** — `t2_tse_fs_sag` (3 mm) and `t1_tse_sag` (4 mm) not copying slices? | Different slice thickness breaks copy slice — the slice positions will misalign. Use **copy center** instead: same FOV center and angulation, set slice thickness independently |
| **Arm position** — Neutral/slight external rotation? | Internal rotation pulls the supraspinatus anteriorly — the coronal oblique cuts it obliquely, making the tendon appear artefactually thickened or torn. Check the bicipital groove position on the axial: if anterior, the arm is internally rotated |
| **Post-contrast** — Contrast given? Enhancing tissue visible on all three planes? | Enhancement can be subtle (mild capsulitis, small labral tear, post-surgical granulation). Acquire sagittal first (highest yield for labrum and capsule), then axial, then coronal. Check that enhancing tissue is truly enhancement, not intrinsic T1 signal — compare with pre-contrast `t1_tse_sag` |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-07 | — | Initial — 8 sequences. PD FS axial + PD coronal + T2 FS cor/sag 3mm + T1 sag 4mm. Three-plane T1 FS post-contrast. Oblique planes to glenohumeral joint |
