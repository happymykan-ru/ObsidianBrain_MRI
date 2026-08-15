# Spine (Cervical / Thoracic / Lumbar — Non-Contrast with Contrast Option)

**Version:** 1.0 | **Date:** 2026-08-15 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first. Legs slightly elevated on a pillow wedge to flatten lumbar lordosis and reduce discomfort if necessary. Arms at the sides.
- **Coil:**
  - **C spine:** Both anterior and posterior head and neck coil.
  - **T and L spine:** Posterior head and neck coil only (for the whole body localizer).
- **Laser Landmark:**
  - **C spine:** Mid neck.
  - **T and L spine:** Sternal notch — for the whole spine sagittal localizer, from which the regional sagittal is planned.
- **Immobilization:** Soft padding on either side of the head to prevent movement.
- **Patient preparation:**
  - **C spine:** Instruct the patient not to swallow during the acquisition — swallowing motion is the dominant C-spine artifact.
  - **T spine:** Shallow breathing — respiratory motion transmits to the thoracic spine.
- **IV Access:** Only if contrast is indicated — 20G (pink), injection rate 2 mL/s, standard dose, saline flush [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Region | Angulation | Coverage | Sat Band |
|---|--------|-------|--------|------------|----------|----------|
| 1 | `t2_tse_dixon_sag_spine` | Sagittal | All | True sagittal — planned from whole spine sagittal localizer and coronal localizer | C: Foramen magnum → T2/T3. T: C7 → L1. L: T12 → S3 | **Anterior** |
| 2 | `t1_tse_sag_spine` | Sagittal | All | Copy Slice from #1 | Copy coverage from #1 | **Anterior** |
| 3 | `t2_me2d_tra_spine` (C, T) / `t2_tser_tra_spine` (L) | Axial | All | ∥ disc space — planned from sagittal #1 | Per disc level of interest. Through the neuroforamina bilaterally | **Anterior** |
| 4 | `t1_tse_tra_spine` (C, T) / `t1_tse_sms_tra_spine` (L) | Axial | All | ∥ disc space — planned from sagittal #1 | Per disc level of interest. Through the neuroforamina bilaterally | **Anterior** |

### Post-Contrast (when contrast is indicated)

| # | Series | Plane | Region | Angulation | Coverage | Sat Band |
|---|--------|-------|--------|------------|----------|----------|
| 5 | `t1_tse_fs_sag_spine_C` | Sagittal | All | Copy Slice from #1 | Copy coverage from #1 | **Anterior** |
| 6 | `t1_tse_fs_tra_spine_C` (C, T) / `t1_tse_sms_fs_tra_spine_C` (L) | Axial | All | Copy from #4 | Copy coverage from #4 | **Anterior** |

---

## 3. Coverage & Plane Planning

### Sagittal (all regions)

**Coverage — at least include:**
- **C spine:** Coverage: foramen magnum → T2/T3. The C7-T1 junction must be included — the most common site of missed cervical disc pathology is at the junction. Centre the slab at C4 — the midpoint of the coverage, keeping both ends within the most homogeneous region of the coil. If field inhomogeneity appears at the shoulders: adjust the shim strategy from "standard neck" to "standard" and manually tighten the shim box.
- **T spine:** C7 → L1. Include the T12-L1 junction.
- **L spine:** T12 → S3. Include the entire sacrum and the distal thecal sac.

**Why:** The sagittal plane is the survey plane — cord signal, vertebral alignment, disc height and hydration, vertebral body marrow, and CSF all assessed in one long-axis view. 

### Axial (per region)

**Coverage — what you plan:**
- **C spine:** Single slab, C2 → T1. The entire cervical spine fits in one stack.
- **T and L spine:** Blocks cut at the levels of pathology, each angled to its disc space. When whole spine coverage is intended, split into two slabs:
  - **T spine:** one slab above the diaphragm, one below. Increase averages on the below-diaphragm slab — it moves with breathing, and the extra averages suppress respiratory ghosting.
  - **L spine:** two slabs, upper and lower, each aligned to its disc spaces.
- FOV through the neuroforamina bilaterally — the exiting nerve roots must be seen.

**Why:** The axial plane cross-sections the spinal canal, cord/cauda equina, and neuroforamina. The disc-nerve root relationship is only assessable in axial. Angling parallel to the disc (not perpendicular to the vertebral body) gives a true cross-section of the disc-canal interface — where herniation occurs.

---

## 4. Sequence Rationale

### Core Strategy

The spine protocol assesses the cord/conus/cauda equina, the discs (degeneration, herniation), the neuroforamina (stenosis), the vertebral bodies (marrow — metastases, infection, fracture), and the canal (stenosis). One sagittal Dixon pair provides both fluid-sensitive and anatomical coverage in all three regions. The axial sequences differ by region: C and T spine use a T2 MEDIC (me2d) for cord and foraminal contrast and a T1 TSE for foraminal fat detail; L spine uses T2 TSE Restore and T1 with SMS acceleration — the cauda equina region tolerates SMS and benefits from the speed.

### Pre-Contrast

**`t2_tse_dixon_sag_spine` (#1):** The **fluid-survey sagittal** for all regions. Answers: is there a disc herniation, cord compression, cord edema (myelopathy), canal stenosis, or abnormal CSF? Four images, each with a pathological use:
- **In-phase:** Routine T2 anatomy — the general morphological reference.
- **Opposed-phase:** Microscopic fat detection in vertebral marrow — signal dropout indicates residual fat (benign marrow lesions, hemangioma); absent dropout suggests fat-replacing pathology (malignant infiltration).
- **Water-only:** The fat-suppressed T2 workhorse — CSF, cord edema, disc herniation, and canal compromise maximally bright against dark fat.
- **Fat-only:** Fatty marrow distribution.
Dixon is chosen over spectral FS because spectral FS fails where the spine B0 is inhomogeneous — the shoulders at the C-T junction and the lung interfaces in the thoracic spine. 

**`t1_tse_sag_spine` (#2):** The **marrow and alignment sequence**. Answers: is the vertebral marrow normal? Non-FS T1 — normal marrow is T1-bright; replacement by metastases, infection, or fracture edema is T1-dark. This is the most sensitive sequence for marrow pathology and the earliest sign of marrow infiltration. Disc heights and vertebral alignment are assessed. The T1 sagittal also serves as the pre-contrast mask for the post-contrast FS sagittal.

**T2 axial (#3):** The **canal and foraminal cross-section**. Answers: is the canal or foramen compromised, and by what? The axial plane is the only cross-section of the disc-canal interface — disc herniation, cord compression (C/T), cauda equina compromise (L), and foraminal stenosis are assessed here.
- **C and T spine — `t2_me2d_tra_spine` (MEDIC):** Multi-echo gradient echo combines multiple echoes for high SNR with bright CSF and excellent cord gray-white contrast. The cord is the primary target, and MEDIC's bright CSF without flow voids shows the canal and foramina clearly.
- **L spine — `t2_tseR_tra_spine` (TSE Restore):** Below L1-L2 there is no cord, only the cauda equina. Restore's driven-equilibrium pulse maintains bright CSF with high SNR at shorter TR — the target is the nerve roots in the thecal sac and foramina, where bright CSF and root visualization are the priority.

**T1 axial (#4):** The **foraminal fat sequence**. Answers: is the foramen stenosed? The neuroforamen is the tunnel between two adjacent pedicles — bounded by pedicles above and below, vertebral body/disc anteriorly, and facet joint posteriorly. Inside, the exiting nerve root runs through epidural fat. On non-FS T1, that fat is the bright halo surrounding the dark nerve root ("dark dot in a bright ring"). Foraminal stenosis effaces the fat plane first — the root sits against bone with no surrounding fat. The sharpest foraminal assessment.
- **C and T spine — `t1_tse_tra_spine`:** T1 TSE.
- **L spine — `t1_tse_sms_tra_spine`:** Same contrast with SMS (simultaneous multi-slice) acceleration.

### Post-Contrast

**`t1_tse_fs_sag_spine_C` (#5):** Answers: is there enhancing pathology — metastases, infection (discitis/osteomyelitis), post-operative granulation? Enhancing tissue appears bright against dark fat along the whole sagittal extent. Compare against the pre-contrast T1 sagittal (#2).

**`t1_tse_fs_tra_spine_C` (#6, C/T) / `t1_tse_sms_fs_tra_spine_C` (#6L, L):** Enhancement localization in cross-section — epidural vs intradural, foraminal involvement, paraspinal extension.

---

### Q&A: Why does only the L spine use SMS?

SMS (simultaneous multi-slice) excites several slices at once with a multiband RF pulse; the coils separate them using their different sensitivity profiles. Scan time drops by the multiband factor — but not for free:

- **SNR penalty:** Signal drops roughly by √MB (multiband factor), plus an SMS-specific g-factor that varies with coil geometry. MB2 costs ~30% SNR before the g-factor.
- **Slice leakage:** Residual signal from simultaneously excited slices ghosts into each other. In the lumbar spine, where slices are thick and separated by the normal slice gap, leakage stays sub-conspicuous.
- **Motion sensitivity:** Each shot now encodes several slices, so patient motion contaminates several levels at once instead of one.

Why this trade-off is acceptable on the **lumbar T1 axial** only:

- **The question is high-contrast.** T1 foraminal assessment is bright fat vs dark nerve root — the highest-contrast question in the spine protocol. The SNR penalty barely registers on that interface.
- **T1 TSE has SNR to spend.** Short TE means high baseline signal; the sequence starts from a surplus, unlike the T2 Restore axial, which starts closer to the margin.
- **Two slabs.** Lumbar axials are upper and lower blocks — the time savings are real and directly felt by the patient. C-spine axials are single small blocks that are already fast.
- **The lumbar canal has no cord.** Slice leakage or ghosting lands on CSF and roots, not on the delicate cord-canal interface. C and T axials keep conventional TSE precisely because the cord is the target — its contrast is subtler, and artifacts there can simulate or mask myelopathy.

---

## 5. Pathology-Based Variations

**Paraspinal mass**
- Add `t2_tirm_cor_spine` (T2 STIR coronal, planned from the sagittal) & `t1_tse_fs_cor_spine_C` post-contrast. The coronal plane profiles the craniocaudal extent and relationship to the paraspinal muscles, pleura, and adjacent organs. STIR makes the mass and edema maximally conspicuous against suppressed fat, and its fat suppression stays uniform despite the B0 variation across the large FOV. Post-contrast answers the enhancement pattern — solid/homogeneous (cellular tumor), peripheral with central non-enhancement (necrosis or abscess), non-enhancing (cystic/necrotic) — separating cellular from necrotic/cystic masses and flagging infection. It also separates enhancing tumor from surrounding edema and makes small enhancing deposits conspicuous. A single post-contrast suffices — subtraction is only needed when the mass is T1-bright pre-contrast (hemorrhage, fat, proteinaceous content); the pre-contrast T1 sagittal serves as the reference.

**Acute trauma**
- Replace the Dixon sagittal with `t2_tse_sag_spine` + `t2_tirm_sag_spine` (T2 + T1 + STIR sagittal trio). STIR's mixed T1+T2 contrast makes marrow edema more conspicuous than pure T2 weighting — edema has both T1 and T2 prolongation, and STIR sums both mechanisms. Bone bruise and subtle fracture edema are the question. Trauma patients move and arrive uncomfortable — STIR has no phase dependency to corrupt. The opposed-phase image is irrelevant here. Axials stay per region.

**Whole-spine screening (known malignancy, suspected metastases)**
- Replace the regional sagittals with composing whole-spine series: `t1_tse_sag_whole_spine_COMP`, `t2_tse_sag_whole_spine_COMP`, and `t2_tirm_sag_whole_spine_COMP`, C1 → sacrum. T1 is the most sensitive sequence for vertebral marrow replacement; T2 gives the anatomical reference; STIR makes any accompanying edema conspicuous across the full extent. Dixon's opposed-phase is not needed here: it answers "is this marrow lesion benign or malignant?", but the malignancy is already known — the question is mapping extent, not characterizing an incidental lesion. STIR also holds up better across the multi-station B0 variation of a composed acquisition.

**Cervical radiculopathy / foraminal stenosis**
- Add `t2_tse_obl_sag_spine` — oblique sagittal, one stack per side (R and L). Planned from the axial localizer: rotate the sagittal stack ~45–55° off the midline, following the foraminal axis on that side. The cervical nerve roots exit anterolaterally at ~45° to the sagittal plane — the oblique stack cuts each foramen perpendicular to the nerve root course, giving a true cross-section of the root inside each foramen, lined up from C2-C3 to C7-T1. Coverage: unilateral skin margin → just past the midline (includes the full foramen and the lateral canal where the root enters).

**C1/C2 subluxation / craniocervical junction assessment**
- Add `t2_space_sag_cs6_iso_spine` — 3D T2 SPACE isotropic sagittal. Thin continuous slices through C0–C2 with MPR reformats along the dens axis — the atlanto-dental interval and craniocervical relationships are assessed in any plane. For atlantoaxial instability: rheumatoid arthritis pannus, os odontoideum, trauma.

**Suspected CSF leak**
- Add `t2_space_sag_fs_spine` — 3D T2 SPACE sagittal with fat saturation (MR myelography). Heavily T2-weighted: CSF is hyperintense; extradural fluid collections, CSF tracking along nerve roots, and meningeal diverticula are seen against suppressed background. Fat saturation is essential — without it, epidural fat and CSF are indistinguishable on heavily T2 contrast. Cover the suspected region, or the whole spine if the leak site is unknown.

---

## 6. Technique Variations

**Metal (post-instrumentation)** — three toolboxes:

  - *STIR & T2 TSE swap:* replace Dixon with `t2_tirm_sag_spine`. Dixon's phase-based water-fat separation breaks down near metal (water-fat swap); TIRM suppresses fat by inversion and is immune to the B0 distortion.
  - *WARP:* replace with `t2_tse_sag_WARP_spine` and other available WARP variants. Siemens' metal-artifact reduction package — combines high bandwidth (shrinks in-plane distortion), VAT (view angle tilting — cancels in-plane displacement), and SEMAC (extra slice-direction phase encoding — corrects through-plane pile-up). SEMAC is one technique; WARP is the bundle that contains it.
  - *High bandwidth adjustments:* crank receiver bandwidth on the remaining sequences, add averages to recover the SNR cost.

**Motion (uncooperative patient, respiratory)** — four toolboxes:

  - *Fast Dixon:* shrinks the inter-echo window, so the Dixon survives minor movement. Does nothing for ghosting.
  - *BLADE:* `t2_blade_sag_spine`, `t1_blade_sag_spine`. Corrects in-plane rotation and translation shot-to-shot — the anti-ghosting tool.
  - *T2 + T2 STIR replacement:* `t2_tse_sag_spine` + `t2_tirm_sag_spine`. Removes Dixon's phase dependency — STIR's fat suppression is motion-immune. Does not correct ghosting by itself.
  - *Reduced phase resolution:* shorter shots, less motion per shot. Costs detail — the last lever.

Escalation by severity:
1. **Mild:** Fast Dixon alone.
2. **Moderate:** T2/T2 STIR pair +/- BLADE sagittals. BLADE kills the ghosting; the STIR pair keeps fat suppression intact under the motion that remains.
3. **Severe:** The above plus reduced phase resolution. A low-resolution diagnostic scan beats a high-resolution non-diagnostic one. Keep axials conventional TSE, reduced resolution, ready to repeat.

**CSF flow artifacts (C/T spine)**
  - CSF pulsation shows two signatures on T2 sagittals: **flow voids** — dark signal gaps in the thecal sac where CSF jets dorsal to the cord (upper cervical); and **pulsation ghosts** — ghost replicas of the cord/canal along the phase-encode direction overlaid on the vertebral bodies, which can simulate cord lesions or intradural masses. Recognize the repeat-pattern at TR spacing.
  - Apply read flow compensation on the **T2 sagittals** (rephases constant-velocity flow, kills most voids and ghosts — usually on by default; confirm). T1 sagittals do not need flow comp — CSF is dark anyway, ghosts are inconspicuous, and flow comp costs minimum TE for no gain.

---

## 7. Alerts

| Check | Improve |
|---|---|
| **Axial slab overlap** — When more than one axial slab is used, do the slabs overlap? | A gap between slabs leaves an unscanned disc level. Make the slabs overlap by at least one slice so no level falls between them |
| **Fat-water swap / signal loss** — Any region with poor shimming? | Poor B0 homogeneity causes regional signal loss and Dixon water-fat swap. Check every sagittal, with special attention to the C7-T1 junction — the shoulders make it the most shim-challenged region and the most common site of missed cervical disc disease. Re-shim (standard shim mode, tighten the shim box) or swap to TIRM |
| **Axial angulation and slice position** — Slice cuts through the point of maximal stenosis? | Angle the axial block to pass through the point of maximal canal or foraminal stenosis on the sagittal — a block that misses this level underestimates or misses the compression |
| **Flow artifacts** — CSF flow voids or pulsation ghosts on sagittals? | Dark signal gaps in the thecal sac or ghost replicas of the cord along the phase-encode direction can simulate cord lesions. Confirm read flow comp is on for T2 sagittals; re-check if ghosts overlap the cord |
| **Post-contrast** — Contrast given, enhancement visible? | Confirm the injection went in and enhancing tissue is seen before completing the exam.|

---

## 8. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-15 | — | Initial — C/T/L combined. T2 Dixon sag + T1 sag. C/T: T2 MEDIC axial + T1 axial. L: T2 TSE Restore axial + T1 SMS axial. Post-contrast: T1 FS sag + T1 FS axial (L: SMS) |
