# Adrenal (Dedicated Adrenal MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-adrenal level (T12–L1).
- **Laser Landmark:** Xiphoid or slightly below
- **Verbal Instructions:** End-expiration breath-holds preferred.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both adrenals + kidneys | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Both adrenals | **None** | Breath-hold |
| 3 | `t2_tse_fs_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t2_tse_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 5 | `t1_vibe_dixon_cor_bh` | Coronal | True coronal | A/P: covering both adrenals + kidneys | **None** | Breath-hold |
| 6 | `t1_vibe_twist_dixon_tra_pre` | Axial | Copy Slice from #2 | — | **None** | Breath-hold |

*#2: T1 VIBE Dixon axial — in/opposed phase. Sequenced early (before T2 TSE) because chemical shift is the primary diagnostic tool for adrenal lesions. In/opp phase must be acquired pre-contrast.*  
*#3–#4: T2 TSE pair — FS for lesion detection, non-FS for anatomical reference.*  
*#5: T1 VIBE Dixon coronal — pre-contrast coronal baseline. Adrenals profiled in relation to renal vessels and IVC.*  
*#6: Pre-contrast TWIST baseline — water-only image.*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency — verify post-contrast FOV matches pre-contrast #6. Standard dose, 2 mL/s | — | — | — |
| 7 | `t1_vibe_twist_dixon_tra_AP` | Axial | Copy Slice from #6 | Both adrenals | **None** | Breath-hold. Fixed delay 30 s |
| 8 | `t1_vibe_twist_dixon_tra_PVP` | Axial | Copy Slice from #6 | — | **None** | Breath-hold, 20 s after #7 |
| 9 | `t1_vibe_twist_dixon_cor_PVP` | Coronal | Copy Slice from #5 | — | **None** | Breath-hold, after #8 |

*#7: Single arterial phase — no 5-phase TWIST. The adrenal enhancement pattern is binary (adenoma = rapid wash-in/wash-out; metastasis/phaeochromocytoma = progressive enhancement). A single well-timed arterial capture is sufficient.*  
*#8–#9: PVP axial + coronal. The coronal PVP assesses IVC invasion and renal vein involvement.*  

---

## 3. Sequence Rationale

### Core Strategy

Dedicated adrenal MRI characterizes an indeterminate adrenal nodule found on CT. The primary clinical question: is this an adenoma or a metastasis (or phaeochromocytoma, or adrenocortical carcinoma)? The answer is determined by **chemical shift imaging** (intracellular lipid detection on in/opposed phase Dixon) — not by dynamic enhancement pattern, which is the key discriminator in liver.

**Key differences from `liver_routine.md`:**

- **Chemical shift is the primary tool, not dynamics.** Adrenal adenoma contains intracellular lipid → signal dropout on opposed phase. Metastasis does not. A lipid-rich adenoma is diagnosed on the pre-contrast Dixon alone — contrast is confirmatory, not primary. The dynamic phases are therefore simplified: single arterial phase (no multi-phase TWIST), PVP axial + coronal, no delayed phases.
- **Coronal plane is essential.** The adrenals sit atop the kidneys and the coronal plane profiles their craniocaudal extent, relationship to the upper pole, renal vessels, and IVC. Pre-contrast Dixon coronal establishes the baseline; post-contrast PVP coronal assesses IVC invasion.
- **No heavy T2, no TrueFISP, no DWI.** Adrenal characterization does not need these — T2 signal is non-specific (both adenoma and metastasis can be T2-intermediate).
- **Coverage is adrenal-focused.** Small FOV covering both glands from the diaphragmatic crus to the renal hilum.
- **Dixon sequenced early (#2).** In/opposed phase must be pre-contrast (contrast alters the phase relationship). Acquired before the T2 TSE pair to capture the cleanest possible chemical shift data.

---

### Pre-Contrast

**T2 HASTE coronal (#1):** Coronal survey — whole abdomen coverage for screening. Both adrenals, kidneys, and upper retroperitoneum.

**T1 VIBE Dixon axial (#2):** The **most important sequence** in the protocol. In/opposed phase — signal dropout on opposed phase = intracellular lipid = adenoma. The degree of dropout can be quantified (signal intensity index). A lesion that drops >20% on opposed phase relative to in-phase is an adenoma. Metastasis, phaeochromocytoma, and adrenocortical carcinoma do not contain intracellular lipid and do not drop signal. Sequenced early because contrast would alter the phase relationship and invalidate the chemical shift assessment.

**T2 TSE axial (#3–#4):** T2 pair — FS for lesion detection, non-FS for anatomical reference. Adrenal lesions are mildly T2-hyperintense; the T2 signal helps distinguish phaeochromocytoma (markedly T2-hyperintense — "light bulb" sign) from adenoma (mildly hyperintense).

**T1 VIBE Dixon coronal (#5):** Pre-contrast coronal baseline. Profiles the adrenal glands, kidneys, renal vessels, IVC, and any mass effect. The coronal plane is essential for surgical planning — the adrenal veins drain to the left renal vein (left) and IVC (right); tumour thrombus extending into these vessels changes management.

**T1 TWIST pre (#6):** Pre-contrast baseline for dynamic phases. Water-only image.

---

### Post-Contrast

**Arterial phase (#7):** Single arterial acquisition (no 5-phase TWIST). Adenoma enhances rapidly and washes out — by the PVP, the adenoma may already be isointense and less conspicuous. The arterial phase confirms the rapid wash-in. Single phase is sufficient because the enhancement pattern is binary (wash-in/wash-out = adenoma vs progressive = metastasis/phaeochromocytoma) — there is no need to capture multiple sub-phases for peak detection.

The optimal adrenal arterial window: aorta is brightly opacified, the adrenal gland enhances avidly, but the renal cortex is still dark (contrast has not yet reached the renal parenchyma). If the renal cortex is already enhancing, the scan is approaching PVP — the adenoma may have already washed out. A single arterial acquisition gives no second chance; the fixed 30 s delay must be correct.

**PVP axial (#8) + coronal (#9):** Adenoma washes out on PVP — appears hypointense or isointense relative to the enhancing adrenal parenchyma. Metastasis and phaeochromocytoma enhance progressively — brighter on PVP than arterial. The coronal PVP assesses:
- **IVC invasion:** Enhancing tumour within the IVC lumen suggests adrenocortical carcinoma or renal cell carcinoma.
- **Renal vein involvement:** Left adrenal vein drains to the left renal vein.
- **Bilateral involvement:** Phaeochromocytoma can be bilateral (MEN2, VHL).

No delayed phase is needed — adrenal washout is complete by PVP, and progressive enhancement of metastasis/phaeochromocytoma is already evident by PVP.

---

## 4. Variations

- **Non-breath-hold:** Borrow the free-breathing techniques from `liver_non-bh.md` and `pancreas_non-bh.md` (HASTE, TFL, StarVIBE). Specifically add:
  - `t2_blade_fs_tra_3mm_trig` — respiratory-triggered BLADE for small-FOV adrenal T2. BLADE's rotating blades provide motion-robust lesion detection; triggering improves slice-to-slice consistency on the small adrenal target.
  - `t1_tfl_in-phase_cor_3mm` / `t1_tfl_opp-phase_cor_3mm` — respiratory-triggered coronal T1 in/opposed phase. Replaces T1 VIBE Dixon coronal (#5); separate acquisitions at different TE.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both adrenals from crus to renal hilum on all sequences? | Reposition if clipped. The right adrenal is higher and more difficult to see than the left; the left adrenal extends more inferiorly to the renal hilum |
| **Chemical shift** — Opposed phase shows signal dropout in the lesion relative to in-phase? | If no dropout: adenoma is not excluded (lipid-poor adenoma, ~30% of adenomas). The dynamic phases then become the primary tool — rapid wash-in/wash-out supports adenoma. If the lesion was previously characterized on CT with washout: MRI may still show dropout |
| **Arterial phase** — Aorta bright, adrenal enhancing, renal cortex dark? | If renal cortex is already enhancing: the scan is approaching PVP. Single acquisition — no second chance |
| **Post-contrast** — Contrast present? | If absent: check IV line, confirm injection. The dynamic phases are secondary to chemical shift, so a non-contrast study may still be diagnostic if the Dixon shows clear dropout |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 9 sequences. Adrenal-only FOV. Chemical shift primary, dynamics simplified (single AP + PVP axial/coronal) |
