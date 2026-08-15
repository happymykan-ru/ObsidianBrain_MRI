# SI Joint (Sacroiliac Joint MRI — with Contrast)

**Version:** 1.0 | **Date:** 2026-08-15 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Arms by the torso — no need to raise the arms above the head, so head-first is fine. Adjust body position so the sacrum is centred in the magnet.
- **Coil:** Body coil anteriorly + spine array posteriorly.
- **Laser Landmark:** Anterior superior iliac spine / sacral level.
- **IV Access:** Required for this contrast protocol — 20G (pink), standard dose, saline flush [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_dixon_cor_si_joint` | Coronal | ∥ sacral axis (through both SI joints) — planned from axial localizer; ∥ sacral long axis on sagittal | Anterior to sacrum → posterior to sacrum. L5 → coccyx | **Superior + Anterior** |
| 2 | `t1_space_cor_si_joint` | Coronal | Copy Slice from #1 | Copy coverage from #1. Isotropic voxels for MPR | **Superior + Anterior + Posterior** |
| 3 | `t1_vibe_fs_cor_si_joint` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **Superior + Anterior** |
| 4 | `t2_tse_fs_tra_si_joint` | Axial | ⟂ sacral axis — planned from sagittal #1 | Above SI joint → below SI joint. Both joints included | **Superior + Anterior** |
| 5 | `t1_tse_tra_si_joint` | Axial | Copy Slice from #4 | Copy coverage from #4 | **Superior + Anterior** |
| — | **Contrast** | — | Standard dose. | — | — |
| 6 | `t1_tse_fs_tra_si_joint_C` | Axial | Copy Slice from #4 | Copy coverage from #4 | **Superior + Anterior** |
| 7 | `t1_tse_fs_cor_si_joint_C` | Coronal | Copy Slice from #1 | Copy coverage from #1 | **Superior + Anterior** |

---

## 3. Coverage & Plane Planning

**Coronal (oblique coronal)**
- **Coverage:** Slice direction A→P: anterior to the sacrum (presacral soft tissues) → posterior to the sacrum (sacral canal, posterior joint margin). FOV S→I: L5 → coccyx, iliac wings included laterally.
- **Planning:** The SI joints are not true coronal structures — each faces ~45° anterolaterally. The coronal is rotated along the sacral axis (through both SI joints) on the axial localizer, and tilted parallel to the sacral long axis on the sagittal. This puts both joints in the same slice, profiling the full joint — iliac side, joint space, sacral side — from top to bottom. L5 must be in the FOV: ankylosing spondylitis begins at the lumbosacral junction.

**Axial**
- **Coverage:** Slice direction S→I: above the SI joint → below it. Both joints in FOV.
- **Planning:** Perpendicular to the sacral axis, each slice cross-sections the joint — the cartilaginous portion (synovial, upper two-thirds) and the ligamentous portion (syndesmosis, lower third) in profile. Both joints are midline structures and appear in the same slice for side-by-side comparison.

**Sat band placement:** most sequences use **superior + anterior** bands. The superior band saturates the inflowing blood of the aorta, IVC, and iliac vessels — flow ghosts from these vessels propagate inferiorly across the SI joints. The anterior band saturates the bowel and abdominal wall — peristalsis and respiratory motion ghost directly over the sacrum. The **SPACE coronal** gets **superior + anterior + posterior**: the 3D acquisition phase-encodes in two directions, so posterior motion sources (rectum, gluteal vessels) ghost along the second axis too and must be saturated as well.

**Phase-encode direction [Confirm]:** coronal PE = R/L, axial PE = A/P. Set PE so motion ghosts propagate away from the joints, and along the short FOV axis where possible for rectangular FOV time savings. The sat bands kill the *source* signal, so no ghosts propagate in any direction.

---

## 4. Sequence Rationale

### Core Strategy

The SI joint protocol assesses active sacroiliitis — the hallmark MRI findings are bone marrow edema (periarticular, best on fluid-sensitive sequences), erosions (subchondral bone loss), and contrast enhancement of the joint space and subchondral marrow (active inflammation). The referral population is predominantly young adults with suspected spondyloarthropathy.

The coronal plane carries the fluid survey (T2 Dixon), the 3D anatomy reference (T1 SPACE), and a fast FS T1 (VIBE). The axial plane pairs T1 with T2 FS — the joint cross-section. Post-contrast T1 FS in both planes completes the enhancement assessment.

### Pre-Contrast

**`t2_tse_dixon_cor_si_joint` (#1):** The **fluid-survey coronal**. Answers: is there bone marrow edema — the defining finding of active sacroiliitis? Periarticular edema on the iliac and sacral sides is bright on the water-only image. Dixon is chosen because the pelvis has challenging B0 homogeneity (bowel gas, presacral soft tissues) — Dixon's fat-water separation is robust where spectral FS fails. The coronal along the sacral axis profiles the full joint extent in one view.

**`t1_space_cor_si_joint` (#2):** The **erosion and anatomy sequence**. 3D T1 SPACE isotropic — thin continuous slices through the joint. Erosions (subchondral cortical breaks with marrow signal extending into them) and joint space morphology are assessed on the non-FS T1: dark cortex against bright marrow fat gives the sharpest bone margins. Isotropic voxels allow MPR through the obliquely oriented joint in any plane. Fat left bright: fatty marrow adjacent to the joint is the reference tissue.

**`t1_vibe_fs_cor_si_joint` (#3):** The **fast FS T1 sequence**. VIBE is a fast 3D gradient echo — free-breathing with averaging, motion-tolerant without breath-hold cooperation. Fat saturation does three jobs:
- **Cartilage conspicuity:** the SI joint's hyaline cartilage is only 2–4 mm — against suppressed (dark) marrow fat it stands out along the whole joint surface. Cartilage thinning, erosion into cartilage, and joint-space narrowing become measurable.
- **Sharp subchondral plate:** fat sat removes the chemical-shift blur at the marrow-cartilage interface, sharpening the cortical margins — the erosion (cortical break) assessment asset.
- **Pannus pre-contrast:** inflammatory pannus is intermediate-bright against suppressed fat, visible as a bright rim along the joint surface before contrast.

The structural complement to the edema view (Dixon) and the marrow view (SPACE).

**`t2_tse_fs_tra_si_joint` (#4):** The **fluid-sensitive cross-section**. The axial plane profiles the cartilaginous and ligamentous portions of the joint — marrow edema and joint fluid in cross-section. FS makes periarticular edema bright against dark fat. Bilateral comparison in the same slice.

**`t1_tse_tra_si_joint` (#5):** The **anatomy cross-section**. Non-FS T1 for the sharpest cortical and subchondral detail — erosions and joint space assessment. Paired with the T2 FS axial (#4): same cross-sections in two contrasts, anatomy and fluid side by side.

### Post-Contrast

**`t1_tse_fs_tra_si_joint_C` (#6):** Enhancement in cross-section — enhancing joint space and subchondral marrow indicate active inflammation. Active sacroiliitis enhances avidly; chronic inactive disease does not.

**`t1_tse_fs_cor_si_joint_C` (#7):** Enhancement along the full joint extent.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — SI joint included in all sequences? | Check every sequence — if the joint is clipped on any series, that contrast/plane's assessment is lost |
| **Coronal angulation** — Both SI joints in the same coronal slice, rotation less than 45°? | Keep rotation under 45° — beyond it the slice flips to sagittal/axial classification: series naming, PACS orientation, and slice graphics all go wrong |
| **L5 inclusion** — L5 vertebra in the coronal FOV? | Ankylosing spondylitis begins at the lumbosacral junction — if L5 is clipped, early disease is missed |
| **Wrap artifact** — Aliasing on the T1 SPACE? |  Confirm slab oversampling sufficient and no wrapping onto the SI joint |
| **Ghosting** — Ghosts over the SI joints? | If ghosting appears, check that the anterior sat band covers the full abdominal wall (skin through bowel) — a band over the bowel alone leaves the moving abdominal wall unsuppressed |
| **Post-contrast** — Contrast given, enhancement visible? | Active sacroiliitis enhances. Confirm true enhancement — enhancing joint space and subchondral marrow |


---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-15 | — | Initial — 8 sequences (+ contrast). T2 Dixon cor + T1 SPACE cor + T1 VIBE FS cor + T2 FS axial + T1 axial. Post-contrast: T1 FS axial + T1 FS coronal. SI joint protocol with contrast |
