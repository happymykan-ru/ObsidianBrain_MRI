# Kidney Non-Breath-Hold (Free-Breathing Renal MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-09-29 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the mid-kidney level.
- **Laser Landmark:** Midway between xiphoid and umbilicus
- **Verbal Instructions:** Breathe quietly and regularly throughout the entire exam — no breath-holds are required. The sequences are motion-robust (single-shot HASTE, BLADE, radial StarVIBE) and are designed to be acquired during free breathing.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_non-bh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior abdominal wall. Both kidneys | **Superior oblique** over heart | Free breathing |
| 2 | `t2_haste_fs_tra_non-bh` | Axial | True axial | Both kidneys. Upper pole → lower pole | **None** | Free breathing |
| 3 | `t2_fblade_fs_tra_p3_non-bh` | Axial | Copy Slice from #2 | — | **None** | Free breathing |
| 4 | `t1_tfl_in-phase_tra_non-bh` | Axial | True axial | Both kidneys | **None** | Free breathing |
| 5 | `t1_tfl_opp-phase_tra_non-bh` | Axial | Copy Slice from #4 | — | **None** | Free breathing |
| 6 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 7 | `t1_starvibe_fs_cor_non-bh_pre-C` | Coronal | True coronal | Both kidneys + renal vessels | **None** | Free breathing |

*#2–#3: Two fat-suppressed T2 axials acquired together — HASTE FS = maximally motion-robust (single-shot per slice); BLADE FS = higher SNR and sharper tissue contrast (multi-shot, needs a regular breathing rhythm). If the BLADE is degraded, the HASTE FS keeps the study diagnostic.*
*#4–#5: T1 TFL (TurboFLASH) — single-shot T1 per slice. In-phase and opposed-phase acquired separately.*
*#7: Coronal pre-contrast baseline — single measurement.*

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency — verify post-contrast FOV matches pre-contrast #4/#7. Standard dose, 2 mL/s. Inject after the 1st measurement of #8 | — | — | — |
| 8 | `t1_starvibe_fs_tra_non-bh_dynamic_C` | Axial | Copy everything from #4 | Both kidneys | **None** | Free breathing. Multiple consecutive measurements over ~3 min. 1st measurement = pre-contrast baseline — contrast injected after it |
| 9 | `t1_starvibe_fs_cor_non-bh_post_C` | Coronal | Copy everything from #7 | Both kidneys + renal vessels | **None** | Free breathing, after #8 |
| 10 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #4 | Both kidneys | **None** | Free breathing |
| 11 | `t1_starvibe_fs_tra_non-bh_delay_C` | Axial | Copy everything from #4 | — | **None** | Free breathing, ~3–5 min post-injection |
| 12 | `t1_starvibe_fs_cor_non-bh_delay_C` | Coronal | Copy everything from #7 | Both kidneys + collecting system | **None** | Free breathing, after #11 |

*#8: StarVIBE has a stack-of-stars radial acquisition — motion-robust, free breathing. Multiple consecutive measurements over ~3 min: 1st measurement = baseline/mask, contrast injected, remaining measurements capture the corticomedullary → nephrographic passage. No separate pre-contrast axial acquisition needed.*
*#11–#12: Excretory/delayed phase with the same StarVIBE acquisition — axial then coronal, matching the BH protocol's delayed pair.*

---

## 3. Sequence Rationale

### Core Strategy

This protocol is the free-breathing alternative to `kidney.md` for patients who cannot breath-hold (dyspnoea, poor compliance, language barrier). Same clinical purpose — characterize a known or suspected renal mass and stage local extent — with the same phase logic (pre-contrast → corticomedullary → nephrographic → excretory), but every sequence is motion-robust and acquired during free breathing.

**What replaces what (vs `kidney.md`):**

- **Pre-contrast**
    - **T2 axials** — the fat-suppressed breath-hold multi-shot TSE becomes a two-sequence pair, both axial: single-shot HASTE FS for motion robustness — lowest SNR and softest tissue contrast, but independent of breathing — plus BLADE FS for SNR and tissue contrast, which needs a regular breathing rhythm to avoid blurring. The non-fat-suppressed T2 axial is dropped — no free-breathing replacement; the axial in-phase T1 serves as the non-fat-suppressed anatomical reference.
    - **T1 in/opposed phase axials** — the 3D breath-hold Dixon becomes two separate 2D single-shot TFL acquisitions, one per echo. TFL gives up VIBE's SNR, spatial resolution and Dixon capability in exchange for motion robustness.
- **Post-contrast** — Dixon is no longer used; every acquisition becomes StarVIBE FS, split by plane:
    - **Axial** — the timed TWIST multiphase (pre / arterial / PVP) becomes a single continuous StarVIBE FS dynamic run (~3 min), the pre becoming its first measurement and serving as the mask; the delayed TWIST Dixon becomes a single StarVIBE FS axial measurement at ~3–5 min. StarVIBE trades TWIST's temporal resolution for radial motion robustness.
    - **Coronal** — the pre-contrast VIBE Dixon and the post-contrast TWIST VIBE Dixon (PVP and delayed) all become the same StarVIBE FS coronal, acquired three times: pre-contrast baseline, PVP, and delayed.

**Key differences from `liver_non-bh.md`:**

- **Coronal T1 — pre-contrast, post-contrast, delayed** — the kidney protocol needs the coronal plane for the renal vein/IVC and the collecting system; liver non-bh has no coronal T1 in any phase and stays axial after contrast.
- **T2 axial block** — both FS T2 axials are always acquired, with no A/B variant choice: FS T2 is the core lesion-characterization sequence for a renal mass, so the HASTE + BLADE pair runs in every patient instead of branching the protocol by breathing pattern; no heavy T2 either — no MRCP-type sequence is needed for the kidney.

---

### Pre-Contrast

**`t2_haste_cor_non-bh` (#1)**
T2 HASTE coronal. Single-shot TSE — each slice acquired in <1 second, independent of breathing. Coronal survey of both kidneys and the retroperitoneum. Superior oblique sat band over the heart suppresses cardiac ghosting into the upper abdomen.

**`t2_haste_fs_tra_non-bh` (#2)**
T2 HASTE FS axial. Single-shot per slice — each slice independent of breathing. Primary lesion detection: a renal mass is T2-hyperintense against the intermediate-signal parenchyma. Lowest SNR of the T2 family but maximally motion-robust.

**`t2_fblade_fs_tra_p3_non-bh` (#3)**
T2 BLADE (PROPELLER) FS axial. Multi-shot with rotating k-space blades — higher SNR and sharper tissue contrast than HASTE. Motion between blades causes blurring, not ghosting. Requires a regular breathing rhythm.

Why both: the FS T2 distinguishes simple cyst (very T2-bright, thin wall) from solid lesion (intermediate T2 signal) — the core T2 characterization of a renal mass. BLADE is the quality acquisition; HASTE is the guarantee. If the patient's breathing degrades the BLADE, the HASTE FS still diagnoses.

**`t1_tfl_in-phase_tra_non-bh` (#4)**
T1 TurboFLASH (TFL) in-phase axial. TFL is a 2D single-shot spoiled gradient echo — each slice acquired in <1 s, free breathing. Unlike VIBE (3D, breath-hold, Dixon-capable), TFL is 2D single-shot: lower SNR, thicker slices, no Dixon support — in-phase and opposed-phase must be acquired as two separate sequences. The benefit is motion robustness. In-phase TE (~4.8 ms at 1.5T, ~2.4 ms at 3T) — water and fat signals add constructively: higher SNR, preserved fat planes. Assesses kidney morphology and intrinsic T1-hyperintensity (blood products in haemorrhagic cyst or RCC). Doubles as the non-fat-suppressed anatomical reference, since the BH protocol's non-FS T2 is dropped.

**`t1_tfl_opp-phase_tra_non-bh` (#5)**
T1 TurboFLASH opposed-phase axial. Matched geometry to #4 but at the opposed-phase TE (~2.4 ms at 1.5T, ~1.2 ms at 3T). Signal dropout confirms intracellular lipid — clear cell RCC (the most common renal malignancy) may show dropout, though less reliably than adrenal adenoma. Angiomyolipoma contains macroscopic fat — bright on T1, drops on fat-suppressed rather than on opposed-phase.

**`t2_trufi_cor_non-bh` (#6)**
T2 TrueFISP coronal. Very short TR — essentially motion-insensitive. Blood is bright without contrast. Renal arteries, renal veins, and IVC: renal artery stenosis, tumour thrombus, accessory renal arteries for surgical planning. Unchanged from the BH protocol — already acquired free-breathing there.

**`t1_starvibe_fs_cor_non-bh_pre-C` (#7)**
T1 StarVIBE FS coronal, single pre-contrast measurement. Radial acquisition — motion-robust. Replaces the coronal VIBE Dixon pre of the BH protocol. Baseline for the coronal post-contrast comparison (renal vein/IVC, collecting system) and coronal anatomical reference.

---

### Post-Contrast

**`t1_starvibe_fs_tra_non-bh_dynamic_C` (#8)**
T1 StarVIBE FS axial, multiple consecutive measurements over ~3 minutes. Replaces the breath-hold TWIST arterial + PVP phases of the BH protocol.

StarVIBE uses a stack-of-stars radial k-space acquisition — the centre of k-space is sampled with every radial spoke, making it inherently motion-robust. Respiratory motion during free breathing produces radial streaks rather than coherent phase-encode ghosts.

**Workflow:** The first measurement is the pre-contrast baseline (mask). Contrast is injected after the 1st measurement completes. Subsequent measurements are acquired back-to-back over ~3 minutes, capturing the entire enhancement passage — corticomedullary, nephrographic, and early delayed — without timing sensitivity. Temporal resolution is lower than TWIST, but no breath-hold is needed.

**Phase identification:** Review the measurements for the corticomedullary phase — cortex brightly enhancing, medulla still dark, renal vein not yet enhancing. If the medulla is already enhancing, the scan is in the nephrographic phase and corticomedullary contrast is lost. Mass enhancement patterns:

- **Clear cell RCC (hypervascular):** Brightly enhancing on corticomedullary — the most common renal malignancy.
- **Papillary RCC (hypovascular):** Hypoenhancing relative to cortex — better seen on nephrographic.
- **Oncocytoma:** Hypervascular with central stellate scar (enhances on delayed).
- **Angiomyolipoma:** Variable enhancement depending on the vascular component.

**`t1_starvibe_fs_cor_non-bh_post_C` (#9)**
T1 StarVIBE FS coronal, acquired after the dynamic series (late nephrographic). The coronal plane profiles the renal vein and IVC along their long axis — enhancing tissue within the vein lumen = tumour thrombus (changes staging from T1 to T3a/b). On axial the vein is cut piecemeal in cross-section, so the extent of thrombus is ambiguous; on coronal it is unmistakable. Also coronal anatomy for surgical planning.

**`ep2d_diff_b50_300_800_tra` (#10)**
DWI, single-shot EPI — same as the BH protocol, free breathing with signal averaging. b=50, 300, 800. Renal cell carcinoma is cellular → restricted diffusion (ADC dark); cyst is fluid → facilitated diffusion (ADC bright). Also provides a screen for nodal and liver metastases.

**`t1_starvibe_fs_tra_non-bh_delay_C` (#11)**
T1 StarVIBE FS axial, single measurement ~3–5 min post-injection. Excretory phase — two purposes, same as the BH protocol:

- **RCC washout:** Clear cell RCC washes out relative to renal parenchyma — the delayed phase confirms the washout pattern.
- **Collecting system:** Contrast has excreted into the calyces, renal pelvis, and ureter — the collecting system is bright. A urothelial tumour appears as a filling defect or enhancing mural nodule.

**`t1_starvibe_fs_cor_non-bh_delay_C` (#12)**
T1 StarVIBE FS coronal, acquired after the axial delayed. The coronal plane at the excretory phase captures the collecting system and ureter along their length in a single view — the functional MR urogram equivalent. An intrarenal collecting system, ureteric filling defect, or obstructed/duplicated system is read here, not on the axial. Same logic as `kidney.md`, where the delayed phase is the only phase acquired in both planes.

---

### Why No Non-Fat-Suppressed T2

T2 does a different job in each organ, which is why `kidney.md`'s non-FS T2 axial has no counterpart here.

In the liver it is a **characterization** tool: the lesion differential is wide, and the FS/non-FS pair adds a fat-versus-fluid axis the FS image alone cannot give.

In the kidney it is a **detection** tool: one clean FS T2 answers the cyst-versus-solid question, and everything downstream is carried by enhancement kinetics, DWI and the T1 pair. The non-FS T2's other two roles are already spoken for:

- **Fat** — macroscopic fat (angiomyolipoma) and intracellular lipid (clear cell RCC) are read on the in-phase/opposed-phase TFL pair and the FS StarVIBE.
- **Fat planes** — the liver's segments are defined by fat-containing fissures (falciform ligament, ligamentum venosum, gallbladder fossa, porta hepatis), which is what makes the non-FS T2 a resection-planning tool there. The kidney has no fat-defined segmental surgical anatomy, and its perinephric planes read on T1.

The cost is real but small: perinephric fat invasion (T3a) and the fat-versus-fluid call now rest on the FS T2 plus the in-phase T1. Against that, the breath-hold protocol got this sequence for one breath-hold; free-breathing it is a full acquisition, and this protocol spends its second T2 axial slot on a BLADE FS — buying motion robustness in the sequence that carries the diagnosis rather than a complementary contrast.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Both kidneys from upper pole to lower pole on all sequences? | Free breathing causes respiratory excursion — the kidneys move with the diaphragm. Prescribe stacks slightly wider than the anatomical extent. The right kidney is normally lower than the left |
| **In/opp-phase TE** — Echo times correct? 1.5T: OP ~2.4 ms / IP ~4.8 ms. 3T: OP ~1.2 ms / IP ~2.4 ms. In-phase image: no dark rim at organ borders? | If the in-phase echo shows a dark rim (India ink) at fat–water interfaces, the echo is not truly in-phase — the TE has shifted. Do not adjust bandwidth or TE — either changes the echo timing and breaks the in/opposed phasing |
| **BLADE FS** — Breathing regular? | Irregular breathing blurs the BLADE FS — rely on the HASTE FS (#2) for lesion characterization |
| **Dynamic phase** — Corticomedullary phase captured: cortex brightly enhancing, medulla dark? | If cortex is not yet enhancing: the phase is too early. If medulla is already enhancing: nephrographic — corticomedullary contrast is lost |
| **Post-contrast** — Contrast present? | If absent: check IV line, confirm injection. A non-contrast study is non-diagnostic for RCC characterization |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-29 | — | Initial — 12 sequences. Free-breathing alternative to kidney.md. HASTE + BLADE FS T2, TFL in/opp, StarVIBE cor pre/post + dynamic + axial/coronal delayed, TrueFISP, DWI |
