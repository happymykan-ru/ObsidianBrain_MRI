# GBM DSC (Glioblastoma Protocol with Perfusion and Spectroscopy)

**Version:** 1.0 | **Date:** 2026-07-20 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 18G (green). DSC perfusion requires a tight contrast bolus — 4 mL/s injection rate demands an 18G, well-sited IV, preferably in the ACF (short catheter, low resistance). Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_tse_dark-fluid_tra` | Axial | Copy Slice and Sat from #1 | — | — |
| 4 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 5 | `ep2d_perf_C` | Axial | Copy Slice from #1 | Foramen magnum → vertex | **None** |
| 6 | `t1_vibe_fs_cor_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 7 | `MPR` | Sag+Ax | — | Whole brain | — |
| 8 | `t1_fl2d_tra_C` | Axial | Copy Slice from #1 | — | **None** |
| 9 | `csi_slaser_135` | [Confirm plane] | [Confirm] | [Confirm VOI placement] | **None** |

*#5: Dynamic DSC perfusion. Inject contrast at 4 mL/s after the 10th measurement for a tight bolus.*
*#9: MR Spectroscopy — multi-voxel CSI with sLASER localization at TE 135.*

---

## 3. Sequence Rationale

### Core Strategy

GBM imaging has three questions beyond standard tumour assessment: is it recurrence or treatment effect, what is the tumour's vascularity, and what is the metabolic profile. Standard anatomical sequences provide the baseline; DSC perfusion distinguishes recurrence from radiation necrosis; MRS characterizes tumour metabolism.

**`t2_tse_tra` (#1)**
Core axial T2 anatomy. Reference plane. T2 shows peritumoural oedema, mass effect, and midline shift.

**`t1_fl2d_tra` (#2)**
Pre-contrast T1 baseline. Matched to post-contrast (#8) for enhancement comparison and subtraction. Pre-contrast T1 hyperintensity suggests haemorrhage within the tumour — common in GBM.

**`t2_tse_dark-fluid_tra` (#3)**
CSF-suppressed T2 FLAIR. Non-enhancing tumour infiltration along white matter tracts is best seen on FLAIR — GBM extends far beyond the enhancing margin. FLAIR defines the full tumour extent.

**`resolve_3scan_trace_tra_p2` (#4)**
RESOLVE DWI. The cellular component of GBM restricts diffusion (ADC dark) while peritumoural oedema facilitates diffusion (ADC bright). DWI before perfusion ensures the ADC map is not contaminated by contrast leakage which can alter diffusion signal.

**Contrast — DSC Perfusion (#5)**
Gadolinium at 4 mL/s. The DSC perfusion sequence captures the first-pass bolus through the brain. Post-perfusion contrast recirculates and provides enhancement for the subsequent anatomical T1 sequences (#6–#8).

**`ep2d_perf_C` (#5)**
EPI 2D dynamic susceptibility contrast perfusion. EPI acquires whole-brain images every ~1–2 seconds. The first 10 measurements establish the baseline T2* signal. Contrast injected at 4 mL/s after measurement 10 — at this concentration in brain capillaries, gadolinium is a T2* contrast agent. The bolus causes signal drop proportional to cerebral blood volume. The signal-time curve is converted to a concentration-time curve and then to an rCBV (relative cerebral blood volume) map.

*Why perfusion for GBM?* Recurrence has high rCBV (angiogenesis, leaky vessels). Radiation necrosis has low rCBV (vascular damage, no angiogenesis). rCBV > 1.75 suggests recurrence; rCBV < 1.0 suggests necrosis. This distinction determines whether the patient gets repeat surgery or steroids.

*Why 4 mL/s?* DSC requires a tight, compact bolus. A slow injection smears the bolus across many measurements, flattening the signal drop and underestimating rCBV. 4 mL/s through a 20G gives a sharp bolus with clear peak.

*Why 10th measurement?* Enough baseline frames to characterize the pre-contrast signal with good SNR, but not so many that scan time is wasted before the bolus arrives.

**`t1_vibe_fs_cor_C` (#6)**
3D T1 post-contrast coronal with fat saturation. Enhancing GBM margin — irregular, thick, nodular rim enhancement is characteristic. Coronal is the money plane for callosal and periventricular tumour extension.

**`MPR` (#7)**
Multiplanar reconstruction from post-contrast VIBE (#6). Sagittal and axial reformatted views.

**`t1_fl2d_tra_C` (#8)**
Post-contrast 2D FLASH axial. Identical geometry to pre-contrast (#2) — subtract for enhancement map. New enhancement beyond the resection cavity margin is the hallmark of recurrence.

**`csi_slaser_135` (#9)**
CSI (Chemical Shift Imaging) with sLASER localization at TE 135. Multi-voxel spectroscopy acquires a grid of spectra across the lesion — this captures the metabolic heterogeneity of GBM (enhancing rim vs necrotic core vs peritumoural oedema).

*Why sLASER?* Semi-LASER uses adiabatic refocusing pulses — less sensitive to B1 inhomogeneity than PRESS. GBM often sits near the skull vertex or sinuses where B1 is uneven; sLASER gives more reliable shimming and cleaner spectra.

*Why TE 135?* At intermediate echo time, the lactate doublet is inverted (below baseline) making it clearly distinguishable from lipid. GBM metabolic profile: elevated choline (cell membrane turnover), decreased NAA (neuronal loss), elevated lactate (anaerobic glycolysis in the hypoxic tumour core). Normal brain is fully aerobic — no lactate. Lactate also appears in radiation necrosis (tissue breakdown). The distinction comes from choline: elevated choline + lactate = tumour; low choline + lactate = necrosis. The choline/NAA ratio correlates with tumour grade.

---

## 4. Clinical Applications of Perfusion and Spectroscopy

- **Post-treatment (recurrence vs radiation necrosis):** DSC perfusion (#5) is the key sequence — rCBV distinguishes the two. MRS (#9) adds complementary data: elevated choline favours recurrence; lipid/lactate without choline elevation favours necrosis.
- **Pre-operative planning:** MRS (#9) defines the metabolic extent — choline elevation often extends beyond the enhancing margin, guiding surgical targets. FLAIR (#3) defines non-enhancing infiltration.
- **Pseudoprogression (early post-treatment increase in enhancement):** DSC rCBV is low in pseudoprogression (treatment-related inflammation, not tumour). True progression shows elevated rCBV.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **IV access** — 18G in ACF, well-sited, patent? | DSC requires 4 mL/s. Test flush before starting. If resistance felt: replace IV |
| **Coverage** — vertex to foramen magnum on all axials? | Adjust slice stack |
| **DSC (#5)** — baseline signal stable through first 10 measurements? | If baseline is drifting (patient motion, poor shim): re-acquire. Unstable baseline makes rCBV unreliable |
| **DSC (#5)** — dark blood visible on inline display during bolus passage? | Watch the inline EPI images: when the bolus arrives, vessels should go dramatically dark (T2* signal loss). If no darkening seen: check IV, confirm injection was delivered, check for extravasation |
| **MRS (#9)** — shim successful? Water linewidth adequate? | If linewidth >15 Hz at half-maximum: re-shim. Poor shim blurs metabolite peaks and makes choline/NAA ratio unreliable |
| **Post-contrast** — contrast present? Confirm intravascular enhancement | If absent: check IV line. DSC will also show no bolus |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-20 | — | Initial — 9 sequences (DSC perfusion + MRS) |
