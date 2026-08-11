# Wrist (Routine Wrist MRI — Non-Contrast)

**Version:** 1.0 | **Date:** 2026-08-11 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** "Superman" — supine, head-first. Place a dedicated large pillow overhead. The wrist and hand coil sits on top of the pillow, arm extended above the head. Hand supinated (palm up), fingers spread with a small soft pad between them to fill dead space and minimize motion. Place a mattress or soft pad under the elbow for support.
- **Coil:** Dedicated hand and wrist coil. Centre over the radiocarpal joint line — palpate the gap between the distal radius and the proximal carpal row.
- **Laser Landmark:** Radiocarpal joint line.
- **Immobilization:** Cover the wrist coil with a mattress and secure with a strap.
- **IV Access:** Not required for this non-contrast protocol. [Confirm — add IV if contrast is indicated for specific clinical question.]

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_tra_wrist` | Axial | ∥ radiocarpal joint line — planned from coronal localizer | Proximal to distal radioulnar joint → carpometacarpal joints. Radial styloid to ulnar styloid in FOV | **None** |
| 2 | `t2_tse_fs_tra_wrist` | Axial | Copy Slice from #1 | Copy coverage from #1 | **None** |
| 3 | `t1_tse_cor_wrist` | Coronal | ∥ long axis of carpus (scaphoid-lunate-capitate axis) — planned from axial #1 | Dorsal skin margin → volar skin margin | **None** |
| 4 | `pd_tse_fs_cor_wrist` | Coronal | Copy Slice from #3 | Copy coverage from #3 | **None** |
| 5 | `t2_me3d_cor_wrist` | Coronal | Copy Slice from #3 | Copy coverage from #3. Isotropic voxels for MPR | **None** |
| 6 | `t2_tse_fs_sag_wrist` | Sagittal | ∥ radius shaft (⟂ radiocarpal joint line) — planned from axial #1 | Radial styloid → ulnar styloid | **None** |

---

## 3. Plane Positioning

All planes share the same FOV: proximal to distal radioulnar joint (DRUJ) → carpometacarpal (CMC) joints. Proximal to the DRUJ captures the extensor tendons at their musculotendinous junction; to the CMC joints captures the full carpus including the carpometacarpal articulations.

- **Axial:** parallel to the radiocarpal joint line (the line connecting the volar and dorsal rims of the distal radius), planned from the coronal localizer. This compensates for the ~10–15° volar tilt of the distal radius — a perpendicular-to-shaft axial cuts obliquely through the carpal tunnel and carpal bones. Slice coverage: proximal to DRUJ → CMC joints. The axial plane cross-sections the carpal tunnel (median nerve, flexor tendons), extensor compartments, and DRUJ — the only plane where all structures are seen simultaneously.

- **Coronal:** parallel to the long axis of the carpus (scaphoid-lunate-capitate axis) on the axial plane. Slice coverage: dorsal skin margin → volar skin margin (must include the flexor tendons, transverse carpal ligament, median nerve, and palmar extrinsic ligaments anteriorly). The coronal plane profiles the triangular fibrocartilage complex (TFCC), intrinsic ligaments (scapholunate, lunotriquetral), and carpal bones in long axis. Aligning to the carpal axis — not the radius — keeps the carpus in true coronal despite its natural ulnar tilt.

- **Sagittal:** perpendicular to both the axial and coronal planes. Slice coverage: radial styloid → ulnar styloid. The sagittal plane profiles carpal alignment (capitolunate and scapholunate angles), flexor tendons in long axis, and the median nerve.

---

## 4. Sequence Rationale

### Core Strategy

The wrist protocol assesses the TFCC (tear, degeneration, ulnar-sided wrist pain), intrinsic ligaments (scapholunate and lunotriquetral tears), carpal tunnel (median nerve, flexor tendons, space-occupying lesions), extensor compartments (tenosynovitis), and carpal bones (avascular necrosis [AVN] — scaphoid, lunate/Kienböck's disease; fractures; marrow edema). The structures are millimetre-scale — the scapholunate ligament is ~2 mm, the TFCC disc proper is ~2–3 mm. SNR and resolution drive the sequence selection.

The axial plane pairs T1 with T2 FS — anatomy and fluid side by side in the cross-section plane. The coronal plane carries three sequences: T1 for marrow and bone alignment, PD FS for the highest-SNR ligament and TFCC detail, and a 3D T2 isotropic acquisition with MPR that replaces dedicated 2D sagittal anatomy and provides thin reformats through the TFCC and intercarpal ligaments. T2 FS sagittal completes the protocol for carpal alignment and flexor tendons.

---

### Pre-Contrast

**T1 TSE axial (#1):** The **anatomy cross-section sequence**. Non-FS T1 gives the sharpest margins in the only plane where all structures are seen simultaneously — carpal tunnel contents (median nerve, flexor tendons, transverse carpal ligament), extensor compartments, and DRUJ. Dark median nerve stands out against T1-bright fat; a compressed or swollen nerve is directly visible. The extensor retinaculum and DRUJ ligaments are seen in cross-section. Normal carpal bone marrow is T1-bright; marrow replacement (AVN, contusion, fracture) is T1-dark.

**T2 TSE FS axial (#2):** The **fluid-sensitive counterpart** to #1, in the same axial plane. T2 with FS makes tenosynovitis of the extensor and flexor tendon compartments maximally conspicuous. Joint effusion, ganglion cysts, DRUJ synovitis, and marrow edema are bright against dark fat. Paired with the T1 axial, the same cross-sections are seen in two contrasts — T1 for structure and marrow, T2 FS for fluid.

**T1 TSE coronal (#3):** The **carpal anatomy and marrow sequence**. Non-FS T1 profiles the carpal bones, intercarpal and carpometacarpal joints, and the DRUJ. Sharp cortical margins for fracture line and bone alignment assessment. T1-bright marrow in the scaphoid and lunate is essential — AVN of the scaphoid (proximal pole after fracture) and lunate (Kienböck's disease) first appear as T1-marrow signal loss. The coronal plane is where carpal bone alignment and intercarpal relationships are assessed.

**PD TSE FS coronal (#4):** The **TFCC and ligament detail sequence**. The TFCC (articular disc, meniscus homologue, ulnocarpal ligaments, extensor carpi ulnaris [ECU] subsheath) and the intrinsic interosseous ligaments (scapholunate, lunotriquetral) are 2–3 mm thick fibrocartilaginous structures. PD gives the highest SNR — the TFCC disc proper and the scapholunate ligament have T2 values of ~30–40 ms; PD's short TE captures signal before T2 decay, maximizing boundaries between the dark fibrocartilage and intermediate-bright surrounding tissue. FS provides fluid conspicuity for TFCC full-thickness tears (fluid crossing the disc) and intrinsic ligament disruptions. The coronal plane profiles these structures in long axis.

**T2 3D coronal isotropic (#5):** The **isotropic 3D sequence** — one acquisition that replaces dedicated 2D sagittal anatomy and provides reformats through the TFCC and intercarpal ligaments at any plane. Coronal acquisition: the carpus is wider (mediolateral) than deep (anteroposterior), making the coronal slab the shortest dimension and minimizing scan time. Thin continuous slices with no gap — a partial TFCC tear or small scapholunate ligament perforation that falls between 2D slices is captured. MPR gives sagittal and axial reformats inline without additional scan time.

**T2 TSE FS sagittal (#6):** The **carpal alignment and tendon sequence**. The sagittal plane profiles the capitolunate and scapholunate angles for carpal instability assessment. The flexor tendons and median nerve are seen in long axis. T2 FS provides fluid sensitivity for marrow edema at the carpal bones, intercarpal joint effusion, and flexor tenosynovitis. A single sagittal sequence is sufficient — anatomy coverage is complemented by the coronal T1 (#3) and the 3D MPR (#5).

---

## 5. Pathology-Based Variations

**Suspected pigmented villonodular synovitis (PVNS) / tenosynovial giant cell tumor (TGCT)**
- Add `t2_fl2d_tra_wrist` — T2 FLASH 2D axial gradient echo. PVNS/TGCT deposits hemosiderin in the synovium; gradient echo (T2*) makes hemosiderin bloom — the susceptibility artifact causes signal dropout in the synovial mass, which is the diagnostic hallmark. Conventional TSE sequences are less sensitive to this blooming.

---

## 6. Alerts

| Check | Improve |
|---|---|
| **R/L labeling** — Correct side confirmed on all sequences? | The wrist is unilateral — a mislabeled side can lead to a wrong-site report |
| **TFCC coverage** — Full TFCC from radial attachment to ulnar styloid? | TFCC tears at the ulnar attachment (foveal or styloid) are the most common — if the FOV clips the ulnar side, the most clinically relevant tear site is missed |
| **3D coverage** — Entire carpus covered? MPR not truncated? | If the 3D slab is too narrow, reformatted edges are clipped. Confirm coverage from dorsal to volar skin margin and DRUJ to CMC joints |
| **Carpal tunnel** — Median nerve clearly seen on axial T1? | Carpal tunnel syndrome is a common referral. Confirm the median nerve is visible from the DRUJ level through the carpal tunnel to the CMC level. Assess for nerve flattening, increased T2 signal, and bowing of the flexor retinaculum |

---

## 7. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-11 | — | Initial — 6 sequences. T1 axial + T2 FS axial + T1 coronal + PD FS coronal + T2 3D isotropic coronal + T2 FS sagittal. Non-contrast wrist protocol |
