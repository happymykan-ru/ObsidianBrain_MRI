# Kidney (Dedicated Renal MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-05 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-kidney level.
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** End-expiration breath-holds preferred.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both kidneys | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_tse_fs_tra_mbh` | Axial | True axial | Both kidneys. Upper pole → lower pole | **None** | Multi breath-hold |
| 3 | `t2_tse_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Both kidneys | **None** | Breath-hold |
| 5 | `t1_vibe_dixon_cor_bh` | Coronal | True coronal | Both kidneys + renal vessels | **None** | Breath-hold |
| 6 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 7 | `t1_vibe_twist_dixon_tra_pre` | Axial | Copy Slice from #4 | — | **None** | Breath-hold |


### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency — verify post-contrast FOV matches pre-contrast #7. Standard dose, 2 mL/s | — | — | — |
| 8 | `t1_vibe_twist_dixon_tra_AP` | Axial | Copy Slice from #7 | Both kidneys | **None** | Breath-hold. Fixed delay 30 s |
| 9 | `t1_vibe_twist_dixon_tra_PVP` | Axial | Copy Slice from #7 | — | **None** | Breath-hold, 20 s after #8 |
| 10 | `t1_vibe_twist_dixon_cor_PVP` | Coronal | Copy Slice from #5 | Both kidneys + renal vessels | **None** | Breath-hold, after #9 |
| 11 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #7 | Both kidneys | **None** | Free breathing |
| 12 | `t1_vibe_twist_dixon_tra_delay` | Axial | Copy Slice from #7 | — | **None** | Breath-hold, ~3–5 min |
| 13 | `t1_vibe_twist_dixon_cor_delay` | Coronal | Copy Slice from #5 | Both kidneys + renal vessels | **None** | Breath-hold, after #12 |


---

## 3. Sequence Rationale

### Core Strategy

Dedicated renal MRI characterizes a known or suspected renal mass (cyst, RCC, angiomyolipoma, oncocytoma, urothelial tumour) and stages local extent (perinephric invasion, renal vein/IVC thrombus, nodal disease). The protocol is essentially a liver protocol adapted for renal FOV, with the coronal plane added for surgical anatomy and a delayed phase for excretory/collecting system assessment.

**Key differences from `liver_routine.md`:**

- **Single arterial phase** — no 5-phase TWIST. Renal enhancement is cortically dominant on AP with subsequent parenchymal equilibration; a single well-timed arterial capture is sufficient.
- **Coronal plane is essential** — the kidneys are paired retroperitoneal organs best profiled coronally. Pre-contrast Dixon coronal establishes the baseline; PVP and delayed coronals assess renal vein/IVC involvement and the collecting system.
- **TrueFISP included** — renal artery, renal vein, and IVC patency for surgical planning. Renal cell carcinoma has a predilection for venous invasion; tumour thrombus extending into the renal vein or IVC changes staging and surgical approach.
- **Delayed phase** — RCC washout kinetics and the collecting system/ureter. Urothelial tumours enhance on delayed images (filling defects in the contrast-opacified collecting system). The excretory phase also provides a functional MR urogram.
- **DWI included** — RCC is cellular (restricted diffusion). DWI also detects nodal and liver metastases.
- **Coverage is renal** — both kidneys from upper pole to lower pole. The adrenal glands are included incidentally superiorly.

---

### Pre-Contrast

**T2 sequences (#1–#3):** Same logic as `liver_routine.md` but renal FOV. HASTE coronal survey (#1). T2 TSE FS (#2) = primary lesion detection — a renal mass is T2-hyperintense against the intermediate-signal parenchyma. T2 TSE non-FS (#3) = anatomical reference. The T2 pair distinguishes simple cyst (very T2-bright, thin wall) from solid lesion (intermediate T2 signal).

**T1 VIBE Dixon (#4–#5):** Axial + coronal. In/opposed phase — intracellular lipid in clear cell RCC (the most common renal malignancy) may show signal dropout, though less reliably than adrenal adenoma. Angiomyolipoma contains macroscopic fat (bright on T1, drops on fat-suppressed). Intrinsic T1-hyperintensity = blood products in haemorrhagic cyst or RCC. The coronal plane profiles the kidneys, renal hilum, and IVC for surgical anatomy.

**T2 TrueFISP (#6):** Renal arteries, renal veins, and IVC bright without contrast. Assesses:
- **Renal artery stenosis** — may coexist with renal mass or be an incidental finding
- **Renal vein/IVC patency** — tumour thrombus from RCC
- **Variant anatomy** — accessory renal arteries for surgical planning

**T1 TWIST pre (#7):** Pre-contrast baseline. Water-only image.

---

### Post-Contrast

**Arterial phase (#8):** Single arterial acquisition — the corticomedullary phase. Typical cortical enhancement peaks at ~25–35 s post-injection. The optimal timing: renal cortex is brightly enhancing, the medulla is still dark (not yet opacified), and the renal vein is not yet enhancing. Corticomedullary differentiation is maximal — cortex bright, medulla dark, sharply demarcated. If the medulla is already enhancing, the scan has reached the corticomedullary equilibrium phase and is approaching PVP — the hypervascular tumour-to-cortex contrast is lost. Mass enhancement pattern:
- **Clear cell RCC (hypervascular):** Brightly enhancing on arterial — the most common renal malignancy.
- **Papillary RCC (hypovascular):** Hypoenhancing relative to cortex — better seen on PVP.
- **Oncocytoma:** Hypervascular with central stellate scar (enhances on delayed).
- **Angiomyolipoma:** Variable enhancement depending on the vascular component.

**PVP (#9–#10):** The nephrographic phase — typical uniform parenchymal enhancement at ~70–90 s post-injection. Cortex and medulla are now isointense (corticomedullary differentiation is lost). The coronal PVP assesses renal vein and IVC for tumour thrombus — enhancing tissue within the vein lumen = venous invasion (changes staging from T1 to T3a/b).

**DWI (#11):** Same as `liver_routine.md`. Renal cell carcinoma is cellular → restricted diffusion (ADC dark). Cyst is fluid → facilitated diffusion (ADC bright). DWI helps distinguish solid from cystic lesions when T2 and enhancement are equivocal. Also provides a screen for nodal and liver metastases.

**Delayed phase (#12–#13):** The excretory phase — typical contrast excretion into the collecting system at ~3–5 min post-injection. Two purposes:
- **RCC washout:** Clear cell RCC washes out relative to renal parenchyma. The delayed phase confirms the washout pattern.
- **Collecting system:** Contrast has excreted into the calyces, renal pelvis, and ureter — the collecting system is bright. A urothelial tumour appears as a filling defect or enhancing mural nodule. This is the functional MR urogram equivalent.

---

**Why no dedicated T2 FS coronal, but a dedicated T1 coronal (pre + post):**

The T2 HASTE coronal (#1) provides coronal T2 survey — the axial TSE pair handles lesion characterization; a dedicated T2 TSE FS coronal would add nothing. T1 coronals are needed for two reasons: (1) the coronal plane profiles the renal vein and IVC along their long axis — an enhancing tumour thrombus extending into these vessels is unmistakable on coronal but ambiguous on axial, where the vein is cut piecemeal in cross-section; (2) on the delayed excretory phase, the coronal plane captures the entire collecting system and ureter in a single view — the equivalent of an IVU/urogram. Axial post-contrast assesses the mass; coronal T1 assesses the vessels, drainage, and collecting system.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both kidneys from upper pole to lower pole on all sequences? | Reposition if clipped. The right kidney is normally lower than the left |
| **Arterial phase** — Renal cortex brightly enhancing, corticomedullary differentiation visible? | If cortex is not yet enhancing: the arterial phase is too early. If medulla is already enhancing: the scan is approaching PVP — corticomedullary contrast is lost |
| **Post-contrast** — Contrast present? | If absent: check IV line, confirm injection. A non-contrast study is non-diagnostic for RCC characterization |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-05 | — | Initial — 13 sequences. Renal FOV. Coronal plane + delayed phase + DWI. Single arterial phase |
