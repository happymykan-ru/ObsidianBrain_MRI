# EC/IC Bypass (Extracranial-Intracranial Bypass MRI)

**Version:** 1.0 | **Date:** 2026-07-22 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink). Fixed injection rate: 2 mL/s. TWIST timing depends on a predictable bolus — variable injection rates shift the bolus arrival relative to the dynamic frames. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_p3` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `TOF_3D_multi-slab` | Axial | ∥ AC-PC line | Whole brain + STA in scalp | **Superior** (venous flow) |
| — | **Contrast** | — | — | — | — |
| 4 | `TWIST_sag_dynamic` | Sagittal | ∥ midline | Whole head including scalp | **None** |
| 5 | `TOF_3D_multi-slab_C` | Axial | Copy Slice from #3 | — | **Superior** |
| 6 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |

*#4: Inject contrast after 1st measurement at 2 mL/s. Fixed rate is essential — TWIST timing depends on a predictable bolus.*

---

## 3. Sequence Rationale

### Core Strategy

EC/IC bypass connects the superficial temporal artery (STA) to an MCA branch to bypass an occluded ICA or proximal MCA. Imaging answers two questions: is the bypass patent, and does flow go the right direction. Anatomy (TOF) + flow dynamics (TWIST) together answer both.

**`t2_tse_tra_p3` (#1)**
Core axial T2 anatomy. Reference plane. Shows established infarction territory, surgical changes, and provides parenchymal context. p3 shortens acquisition.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. Matched to post-contrast (#6) for enhancement comparison and subtraction.

**`TOF_3D_multi-slab` (#3)**
Pre-contrast TOF MRA. Shows the native arterial anatomy: the occluded ICA/MCA, collateral filling, and the STA donor vessel. Coverage is extended to whole brain including the STA as it runs through the scalp — standard TOF coverage clips the donor vessel outside the skull. Sat band superior to suppress venous signal.

**Contrast**
Standard dose IV gadolinium. TWIST (#4) captures the first-pass bolus. Post-contrast TOF (#5) follows.

**`TWIST_sag_dynamic` (#4)**
Time-resolved MRA, sagittal source. This is the key bypass patency sequence. Sequential frames (~1–3 s each) show contrast flowing from the STA (scalp) → anastomosis → MCA branches. Antegrade flow (STA → MCA) = patent bypass. Retrograde flow (MCA filling from collaterals, STA not contributing) = bypass is occluded or stenosed. Standard TOF shows the anatomy; TWIST shows whether blood actually moves through it. Sagittal source covers the whole head including the scalp where the STA runs. For full TWIST acquisition details, see `cerebral_angiogram(no_brain_request).md`.

**`TOF_3D_multi-slab_C` (#5)**
Post-contrast TOF MRA. Gadolinium shortens blood T1, increasing the signal of slow flow in the STA and small-calibre MCA branches — post-contrast TOF is more sensitive for the bypass graft than pre-contrast TOF alone. Also shows enhancing tissue near the anastomosis (post-surgical change vs infection). Same extended coverage as pre-contrast TOF (#3).

**`t1_fl2d_tra_C` (#6)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map. Covers the brain for any post-operative complication (infarction, haemorrhage, infection).

---

## 4. How This Differs from Standard cerebral_angiogram

Standard cerebral angiogram is designed to find vascular pathology. EC/IC bypass imaging is designed to assess a known surgical conduit.

- **No FLAIR, no DWI:** The brain parenchyma has already been fully characterized on prior scans. This is a focused assessment of the bypass, not a diagnostic brain study. T2 suffices for new infarction or surgical change.

- **TWIST instead of post-contrast brain VIBE/MPR:** The dynamic information (flow direction, patency) is the diagnostic endpoint. VIBE/MPR for brain enhancement is not needed — this is not a tumour follow-up.

- **Post-contrast TOF added:** Pre-contrast TOF shows native anatomy; post-contrast TOF amplifies slow flow in the small-calibre bypass graft and STA.

- **Extended coverage on TOF:** Whole brain + STA in scalp. Standard angiogram TOF clips the donor vessel — the STA runs outside the skull.

- **TWIST sagittal for whole-head coverage:** Unlike AVM TWIST where the question is intracranial, here the flow path runs from the scalp (STA) → skull (craniotomy) → brain (MCA). Sagittal captures the entire extracranial-to-intracranial course in one dataset.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **Coverage** — STA included in the scalp on TOF (#3, #5) and TWIST (#4)? | Donor vessel runs outside the skull. If the STA is clipped by the FOV or sat band, extend coverage laterally to include the scalp surface |
| **TWIST (#4)** — contrast present? STA → anastomosis → MCA flow visible? | If no flow in STA: confirm IV injection. If STA fills but MCA does not: confirm anastomosis is inside the FOV |
| **Post-contrast** — contrast present? | Confirm intravascular enhancement on TOF (#5) and FLASH (#6) |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-22 | — | Initial — 6 sequences (TOF + TWIST for bypass patency) |
