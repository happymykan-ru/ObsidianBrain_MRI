# Elbow (Routine Elbow MRI — Non-Contrast)

**Version:** 1.0 | **Date:** 2026-08-11 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Oblique the body towards the affected side, supported by a mattress behind the contralateral torso — this brings the elbow closer to the magnet isocentre for improved B0 homogeneity and SNR. Arm at the side, forearm supinated (palm up).
- **Coil:** Ultraflex coil wrapped around the elbow and secured with a strap. Centre over the humeroulnar joint line — palpate the gap between the olecranon and the distal humerus.
- **Laser Landmark:** Humeroulnar joint line.
- **Immobilization:** Place a triangular support over the palm and secure with straps to maintain supination and prevent motion. Sandbags alongside the arm.
- **IV Access:** Not required for this non-contrast protocol. [Confirm — add IV if contrast is indicated for specific clinical question.]

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_stir_cor_elbow` | Coronal | ∥ humeral epicondylar line (trans-epicondylar axis) — planned from axial localizer | Anterior to capitellum → posterior to olecranon fossa. FOV: above humeral epicondyles → below radial tuberosity | **None** |
| 2 | `t1_tse_dixon_cor_elbow` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `pd_tse_fs_cor_elbow` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 4 | `t1_tse_tra_elbow` | Axial | ∥ humeroulnar joint line — planned from coronal #1 | Above humeral epicondyles → below radial tuberosity. Both epicondyles in FOV | **None** |
| 5 | `t2_tse_fs_tra_elbow` | Axial | Copy Slice from #4 | Copy coverage from #4 | **None** |
| 6 | `t2_stir_sag_elbow` | Sagittal | ∥ humeral shaft (⟂ trans-epicondylar line) — planned from axial #4 | Medial epicondyle → lateral epicondyle. FOV: above humeral epicondyles → below radial tuberosity | **None** |

---

## 3. Plane Positioning

All planes share the same FOV: above humeral epicondyles → below radial tuberosity. Above the epicondyles captures the common flexor and extensor origins — medial epicondylitis (golfer's elbow) and lateral epicondylitis (tennis elbow) are missed if the FOV stops at the joint line. Below the radial tuberosity captures the biceps tendon insertion.

- **Coronal:** plane parallel to the humeral epicondylar line (trans-epicondylar axis), planned from the axial localizer (if epicondyles not covered in the anatomical axial localizer, repeat). Slice coverage: anterior to capitellum → posterior to olecranon fossa. Both epicondyles must appear on the same coronal slice at the joint level — a tilted coronal foreshortens the ulnar collateral ligament (UCL) and common flexor/extensor origins.

- **Axial:** parallel to the humeroulnar joint line, planned from the coronal (#1). Slice coverage: above humeral epicondyles → below radial tuberosity. The axial plane is the cross-section where all ligaments, tendons, and the ulnar nerve are seen simultaneously.

- **Sagittal:** parallel to the humeral shaft (perpendicular to the trans-epicondylar line), planned from the axial (#4). Slice coverage: medial epicondyle → lateral epicondyle. The sagittal profiles the biceps tendon, triceps tendon, and joint recesses in long axis.

---

## 4. Sequence Rationale

### Core Strategy

The elbow protocol assesses the collateral ligaments — ulnar collateral ligament (UCL) and lateral collateral ligament (LCL) complex — the common flexor and extensor origins (medial and lateral epicondylitis), the biceps and triceps tendons, the articular cartilage, and the ulnar nerve. The elbow is the most off-isocentre joint — with the arm at the side or above the head, B0 homogeneity is poor. STIR and Dixon are used for the fluid-sensitive sequences where spectral FS would fail; PD FS is kept for the highest-SNR tendon detail.

The coronal plane carries three sequences — a T2 STIR for fluid survey, a T1 Dixon for anatomy and marrow (two contrasts in one acquisition), and a PD FS for the sharpest ligament and tendon detail. The axial plane pairs T1 with T2 FS — anatomy and fluid side by side in the only plane where all structures are seen in cross-section. T2 STIR sagittal completes the protocol for the biceps and triceps tendons in long axis.

---

### Pre-Contrast

**T2 STIR coronal (#1):** The **fluid-survey coronal**. T2 makes joint effusion, collateral ligament tears, and marrow edema maximally conspicuous. STIR is chosen over spectral FS because the elbow is off-isocentre — STIR provides robust, uniform fat suppression independent of B0 homogeneity. The coronal plane profiles the UCL and LCL complex in long axis, the common flexor and extensor origins, and the radiocapitellar joint.

**T1 TSE Dixon coronal (#2):** The **anatomy-and-marrow sequence** — two contrasts in one acquisition. The in-phase image is a non-FS T1: sharp cortical and trabecular bone margins, bright fatty marrow, dark ligaments against fat. The water-only image is a FS T1: marrow replacement and soft-tissue detail without fat signal. Dixon provides robust fat-water separation where spectral FS would be degraded off-isocentre, and replaces what would otherwise be two separate sequences (T1 non-FS + T1 FS). Same coronal plane as #1 for direct comparison.

**PD TSE FS coronal (#3):** The **tendon-and-ligament detail sequence**. PD gives the highest SNR for thin structures — the UCL anterior band is 2–3 mm thick, the common extensor and flexor origins are millimetre-scale. PD's short TE and high signal yield the sharpest boundaries between dark tendon/ligament and intermediate-bright surrounding tissue. FS provides sufficient fluid conspicuity for tears. The coronal plane is where these structures are seen in long axis — this is the sequence to measure UCL tear size and grade epicondylitis.

**T1 TSE axial (#4):** The **anatomy cross-section sequence**. Non-FS T1 provides the sharpest ligament margins in the only plane where all structures are seen simultaneously — UCL, LCL complex, biceps tendon, triceps tendon, common flexor and extensor in short-axis. The ulnar nerve is assessed in the cubital tunnel: T1-bright fat surrounds the dark nerve; scarring or compression displaces or effaces this fat plane. Normal marrow is T1-bright; marrow replacement (contusion, stress fracture) is T1-dark.

**T2 TSE FS axial (#5):** The **fluid-sensitive counterpart** to #4, in the same axial plane. T2 with FS makes fluid in torn ligaments, tenosynovitis, joint effusion, and marrow edema maximally conspicuous. Paired with the T1 axial (#4), the same cross-sections are seen in two contrasts — T1 for structure and marrow, T2 FS for fluid. This is the same "anatomy + fluid side by side" logic as the hip and ankle T1/T2 FS pairs.

**T2 STIR sagittal (#6):** The **biceps-and-triceps sequence**. The sagittal plane is the long-axis view of the biceps tendon (anterior) descending to the radial tuberosity and the triceps tendon (posterior) inserting on the olecranon. The anterior and posterior joint recesses are profiled for effusion. The coronoid and olecranon are seen in profile. T2 STIR provides robust fluid sensitivity — same STIR rationale as #1. Single sagittal sequence: anatomy is covered by #2 (T1 Dixon coronal) and #4 (T1 axial); this sequence only needs to provide fluid sensitivity in this plane.

---

## 5. Q&A

**How to align planes when the elbow cannot be fully extended?**

- **Sagittal** — unaffected. Flexion is sagittal-plane motion; the humerus, joint, and forearm remain in-plane. Plan along the humeral shaft as usual.
- **Coronal** — most affected. The forearm bends out of the humeral coronal plane. Priority: align to the humeral epicondylar line to keep the common extensor and flexor origins in true long axis — these are the most common injury sites. Accept that distal insertions will be obliqued.
- **Axial** — intermediate. Split the angle equally between humeral shaft and forearm (perpendicular to the bisector). The bisector gives the best cross-section at the joint level, where the ligaments, tendons, and ulnar nerve matter most.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **R/L labeling** — Correct side confirmed on all sequences? | The elbow is unilateral — a mislabeled side can lead to a wrong-site report |
| **B0 homogeneity** — Fat suppression unreliable? | The elbow is off-isocentre — spectral FS may fail, producing geographic bright patches that mimic edema. Improve shimming first; if still non-diagnostic, replace PD/T2 FS with PD/T2 Dixon |
| **Coronal alignment** — Truly parallel to the epicondylar line? | A tilted coronal foreshortens the UCL and common flexor/extensor origins. Confirm both epicondyles are visible on the same coronal slice at the joint level |
| **UCL coverage** — Full UCL from medial epicondyle to sublime tubercle? | The anterior band inserts on the sublime tubercle of the ulna — if the FOV clips the medial ulna, the UCL insertion is missed and a partial tear at the insertion cannot be excluded |
| **Biceps tendon insertion** — Radial tuberosity in FOV on all planes? | The biceps tendon inserts on the radial tuberosity, distal to the joint line. If coverage stops at the joint, the most common site of biceps tendon rupture is missed |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-11 | — | Initial — 6 sequences. T2 STIR cor + T1 Dixon cor + PD FS cor + T1 axial + T2 FS axial + T2 STIR sag. Non-contrast elbow protocol |
