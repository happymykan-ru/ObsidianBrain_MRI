# TM Joint (Temporomandibular Joint MRI ± Contrast)

**Version:** 1.0 | **Date:** 2026-08-02 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil (no dedicated TMJ surface coils available)
- **Laser Landmark:** External auditory canal (tragus) — the TMJ sits directly anterior to the EAC. Centring here positions the joint at isocentre.
- **Immobilization:** Foam padding
- **Verbal Instructions:** For closed-mouth sequences: rest teeth together gently — do not clench. Clenching contracts the lateral pterygoid muscle and alters condyle position. For open-mouth sequences: a folded gauze bite block (~2–3 cm) is placed between the incisors. Rest teeth gently on the gauze; do not bite down actively. Remain completely still — the open-mouth position is uncomfortable and difficult to hold. Breathe quietly.

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t1_tse_cor_2mm_closed` | Coronal (true) | ⟂ hard palate | Both TMJs (see rationale) | **None** |
| 2 | `pd+t2_tse_sag_2mm_closed` | Sagittal Oblique (double) | ∥ mandibular ramus on coronal → ∥ condylar long axis on axial (≈ ∥ mandibular ramus on axial). Separate L/R | Single TMJ per side. Small FOV (~12–15 cm) | **None** |
| 3 | `pd_tse_sag_2mm_open` | Sagittal Oblique (double) | **New localizer** with mouth open. Same double oblique principle. Separate L/R | Single TMJ per side. Same as #2 | **None** |
| — | **Contrast** | — | — | — | — |
| 4 | `t1_tse_cor_fs_2mm_closed` | Coronal (true) | Copy Slice from #1 | — | **None** |
| 5 | `t1_tse_sag_fs_2mm_closed` | Sagittal Oblique (double) | Copy Slice from #2. Separate L/R | — | **None** |

*#2: PD+T2 is a dual-echo TSE acquisition — early echo = PD, late echo = T2. Both contrasts from one scan.*
*#3: Mouth opened with gauze bite block (~2–3 cm). New localizer is required because the condyle translates anteriorly out of the fossa; the closed-mouth prescription planes no longer apply. PD only (single echo) — shorter scan while the patient holds the open position.*
*All sagittal sequences are prescribed separately for left and right TMJs — the condylar angle differs between sides.*
*All sequences use 2 mm slice thickness — highest resolution of any head and neck protocol.*
*#4, #5: Contrast indicated for suspected synovitis, inflammatory arthritis, or post-surgical assessment. For routine internal derangement without suspicion of inflammation, contrast may be omitted.*

---

## 3. Sequence Rationale

### Core Strategy

TMJ imaging assesses the disc-condyle relationship. The primary clinical question is internal derangement: is the disc displaced, and does it recapture on mouth opening? The disc is fibrocartilaginous — low signal on all sequences. The protocol is built around **PD-weighted sagittal oblique** as the workhorse sequence: PD provides the optimal contrast between the dark disc and intermediate-signal surrounding tissues (lateral pterygoid muscle, bilaminar zone, joint fluid). T2 identifies joint effusion. Open-mouth views test disc recapture. The coronal plane assesses medial/lateral disc displacement and condylar morphology.

---

**`t1_tse_cor_2mm_closed` (#1)**
T1 TSE true coronal, both TMJs. Pre-contrast anatomical reference.

The true coronal plane profiles:
- **Condylar head morphology** — flattening, osteophytes, subchondral cysts (osteoarthritis). Both condyles on one image for direct comparison.
- **Medial/lateral disc displacement** — while most disc displacements are anterior or anterior-medial (best seen sagittally), pure lateral or medial displacement is assessed coronally. The disc should sit atop the condyle like a cap.
- **Joint space symmetry** — unilateral joint space narrowing suggests degenerative change.
- **Lateral pterygoid muscle** — atrophy or asymmetry (chronic disuse from protective splinting).

T1 provides the bone and soft tissue baseline for post-contrast comparison (#4).

**Coverage:** The coronal stack extends beyond the immediate joint space. Superiorly, it must include the entire glenoid fossa and articular eminence — the fossa forms the roof of the joint and its thin bone can be eroded in inflammatory arthritis or fractured in trauma. The middle cranial fossa floor directly above the fossa should also be visible. Inferiorly, coverage extends well below the condylar neck to include the mandibular ramus past the sigmoid notch — the lateral pterygoid muscle inserts on the anterior condylar neck and pterygoid fovea, and its full inferior attachment must be seen. Anterior-posterior: from the articular eminence to posterior to the mastoid process, ensuring the entire condyle and fossa are captured in all patients regardless of condylar position. Both TMJs must be fully included in a single acquisition.

---

**`pd+t2_tse_sag_2mm_closed` (#2, L/R)**
PD+T2 dual-echo TSE, double oblique sagittal. This is the **primary diagnostic sequence** for TMJ internal derangement. Two echoes are acquired from one scan: PD (early echo) and T2 (late echo).

**Double oblique prescription:** On the coronal scout, align the slice plane parallel to the mandibular ramus. On the axial scout, rotate the plane parallel to the long axis of the condyle (the condyle is angulated ~15–25° from the coronal plane, with the medial pole more posterior). In practice, aligning parallel to the mandibular ramus on the axial scout is roughly equivalent — the ramus follows the same posteromedial orientation as the condylar axis and is a larger, easier landmark to sight. This gives a true sagittal view of the condyle and disc — a straight sagittal would cut the condyle obliquely and misrepresent disc position.

**PD (early echo):** Disc morphology. The fibrocartilaginous disc is low signal; surrounding tissues (lateral pterygoid, bilaminar zone, joint fluid) are intermediate signal. The posterior band of the disc should sit at approximately the 12 o'clock position relative to the condylar head. Anterior disc displacement: the disc is positioned anterior to 12 o'clock. The bilaminar zone (retrodiscal tissue, posterior attachment of the disc) is stretched in anterior displacement.

**T2 (late echo):** Joint effusion — bright signal in the superior or inferior joint compartment. A trace of fluid is physiological; a large effusion suggests capsulitis, internal derangement, or inflammatory arthritis. T2 also helps distinguish acute disc displacement (effusion present, disc morphology preserved) from chronic disc displacement (no effusion, disc may be deformed or perforated).

**Coverage:** Single TMJ, small FOV (~12–15 cm) centred on the condyle. Performed separately for left and right.

---

**`pd_tse_sag_2mm_open` (#3, L/R)**
PD TSE double oblique sagittal, mouth open. A **new localizer** is acquired with the mouth open (gauze bite block in place), and the double oblique prescription is repeated on the new scouts.

With mouth opening, the condyle translates anteriorly out of the glenoid fossa onto the articular eminence — the condyle position and slice geometry change, and the closed-mouth prescription planes are no longer valid.

PD only (single echo) — shorter acquisition than the dual-echo closed-mouth sequence, important because the patient must hold the open position still.

**The key diagnostic question: disc recapture.**

- **Normal:** The disc remains interposed between the condyle and the articular eminence throughout opening. The thin intermediate zone of the disc sits at the condyle-eminence interface.
- **Anterior disc displacement WITH recapture:** The disc is anteriorly displaced in the closed-mouth position (#2). On opening, the condyle translates forward and the disc reduces (returns) to its normal position between the condyle and eminence. Often associated with a clicking sound (the disc reducing and displacing).
- **Anterior disc displacement WITHOUT recapture:** The disc remains anteriorly displaced even with the mouth fully open. The condyle translates forward but the disc does not reduce — the condyle articulates directly with the bilaminar zone or the posterior band of the displaced disc. This is more severe: mouth opening is typically limited (no translation), there is no click (the disc is locked anteriorly), and progression to osteoarthritis is common. Surgical intervention (arthroscopy, arthroplasty, discectomy) is more likely.

**Practical note:** The gauze bite block must be thick enough (~2–3 cm) to achieve adequate condylar translation but not so thick that the patient cannot hold it. If opening is limited due to pain or mechanical block, note the maximum opening achieved.

---

**Contrast**
Standard dose IV gadolinium. Indicated for suspected synovitis, inflammatory arthritis (rheumatoid arthritis, juvenile idiopathic arthritis), or post-surgical assessment. For routine internal derangement without suspicion of inflammation, contrast may be omitted — the pre-contrast sequences (#1–#3) are diagnostic for disc position.

---

**`t1_tse_cor_fs_2mm_closed` (#4)**
T1 TSE FS true coronal, post-contrast. Matched geometry to #1.

Enhancing synovium indicates synovitis/capsulitis — the normal synovium is a thin, barely perceptible line; thickened, avidly enhancing synovium is pathological. In inflammatory arthritis (RA, JIA), enhancing pannus destroys the disc and cartilage. Both TMJs on one image allow side-to-side comparison of synovial enhancement.

**Coverage:** Matches #1.

---

**`t1_tse_sag_fs_2mm_closed` (#5, L/R)**
T1 TSE FS double oblique sagittal, post-contrast. Matched geometry to #2.

The disc itself is fibrocartilaginous and **does not normally enhance** — it is avascular. Enhancement within the disc suggests:
- **Discitis / inflammatory change** — rare, but seen in severe inflammatory arthritis where pannus invades the disc substance.
- **Post-surgical granulation tissue** — after discectomy or arthroplasty, enhancing tissue in the joint space may be post-surgical scar or recurrent disc tissue. The distinction is difficult and requires correlation with symptoms.

The bilaminar zone (retrodiscal tissue, posterior to the disc) is **normally vascular and enhances** — this is the posterior attachment of the disc and should not be mistaken for pathology. In anterior disc displacement, the bilaminar zone is stretched anteriorly into the joint space and its normal enhancement is pulled forward with it.

**Coverage:** Matches #2. Separate L/R.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both TMJs on coronal? Sagittal FOV centred on each condyle? | Reposition if TMJ clipped |
| **Double oblique** — Sagittal plane parallel to mandibular ramus (coronal) and condylar long axis (axial)? | If plane is straight sagittal (not oblique), the condyle will be cut obliquely — disc position will appear artefactually displaced. Re-plan with double oblique |
| **Open mouth** — Condyle translated out of the fossa onto the articular eminence? | If condyle not translated: gauze too thin or patient unable to open (note maximum opening in report) |
| **Motion** — Open-mouth sequence: patient holding still? | The open position is uncomfortable — motion is common. If degraded: the closed-mouth sagittal (#2) and coronal (#1) are more robust; the open-mouth view is the most likely to fail. Re-acquire if non-diagnostic |
| **Post-contrast** — Contrast present? Check the bilaminar zone on sagittal FS (#5) — it is normally vascular and should enhance. | If absent: check IV line, confirm injection. The bilaminar zone enhances normally — do not mistake this for pathological synovial enhancement |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-02 | — | Initial — 5 sequences (dual-echo PD+T2 sagittal, open-mouth PD sagittal, coronal ± contrast) |
