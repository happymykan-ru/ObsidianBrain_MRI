# Liver Routine (Multiphasic Liver MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first (feet-first if scanner layout requires)
- **Coil:** Body matrix coil anteriorly + spine array. Centre the body coil over the liver.
- **Laser Landmark:** Centre of body coil (mid-liver, approximately at the xiphoid level)
- **Immobilization:** Positioning aids as needed
- **Verbal Instructions:** Breath-hold commands are essential — coach the patient before starting. End-expiration is preferred (more reproducible diaphragm position across breath-holds). If the patient has poor breath-hold compliance, use end-inspiration. The patient must hold at the same depth for each acquisition — inconsistent breath-hold depth causes slice misregistration between sequences, degrading lesion comparison and subtraction.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_tse_fs_tra_mbh` | Axial | True axial | Whole liver | **None** | Multi breath-hold |
| 3 | `t2_tse_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 4 | `t2_heavy_tse_fs_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 5 | `t2_haste_fs_tra_p2_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 6 | `t1_vibe_dixon_tra_mbh` | Axial | True axial | Whole liver | **None** | Multi breath-hold |
| 7 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 8 | `t1_vibe_twist_dixon_tra_pre` | Axial | True axial | Whole liver | **None** | Breath-hold |

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | **Check FOV consistency** — verify post-contrast FOV matches pre-contrast #8. Standard dose, 2 mL/s | — | — | — |
| 9 | `t1_vibe_twist_dixon_tra_bh_art_5phase` | Axial | Copy Slice from #8 | Whole liver | **None** | Breath-hold. Fixed delay 30 s post-injection |
| 10 | `t1_vibe_twist_dixon_tra_PVP` | Axial | Copy Slice from #8 | — | **None** | Breath-hold, 20 s after #9 |
| 11 | `t1_vibe_twist_dixon_tra_Delayed_2min` | Axial | Copy Slice from #8 | — | **None** | Breath-hold, ~2 min post-injection (50 s after #10) |
| 12 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #8 | Whole liver | **None** | Free breathing |
| 13 | `t1_vibe_twist_dixon_tra_Delayed_5min` | Axial | Copy Slice from #8 | — | **None** | Breath-hold, ~5 min post-injection |

---

## 3. Sequence Rationale

### Core Strategy

Multiphasic liver MRI characterizes focal liver lesions by their enhancement pattern across arterial, portal venous, and delayed phases. The differential of a liver lesion — cyst, haemangioma, FNH, adenoma, HCC, metastasis — is determined by how it enhances and washes out relative to liver parenchyma. T2 signal (with and without fat saturation, heavily T2-weighted) and DWI (ADC value) narrow the pre-contrast differential. The dynamic phases then confirm: arterial hyperenhancement with portal venous washout = HCC; arterial hyperenhancement with persistent enhancement = FNH; progressive centripetal filling = haemangioma; rim enhancement with persistent central low signal = metastasis.

---

### Pre-Contrast

**`t2_haste_cor_mbh` (#1)**
T2 HASTE coronal. Single-shot TSE — each slice is acquired in <1 second, so even poor breath-holders produce diagnostic images. The coronal plane provides a survey of the whole liver, biliary tree, and relationship to diaphragm and adjacent organs. Rapid acquisition with minimal motion artefact makes this the ideal first sequence.

**Coverage:** A/P: anterior abdominal wall → posterior liver margin. Superior oblique sat band over the heart — suppresses cardiac motion artefact propagating into the liver dome.

The superior oblique sat band is placed over the heart on the coronal slice, angled to follow the cardiac apex. Cardiac motion during acquisition produces ghosting along the phase-encode direction; the liver dome sits directly below the heart and is the most vulnerable region.

---

**`t2_tse_fs_tra_mbh` (#2)**
T2 TSE axial with fat saturation. Lesion detection — T2-hyperintense lesions (cysts, haemangiomas, oedematous or necrotic tumours) stand out against the intermediate-signal, fat-suppressed liver parenchyma. FS also suppresses subcutaneous and intra-abdominal fat, reducing ghosting artefact across the phase-encode direction.

Multi breath-hold: the TSE acquisition is split across multiple breath-holds to cover the whole liver.

---

**`t2_tse_tra_mbh` (#3)**
T2 TSE axial without fat saturation. Matched geometry to #2 but no FS — the fat planes remain bright. Used as an anatomical reference: vessel margins, lymph nodes, and the tumour-liver interface are clearer without FS.

---

**`t2_heavy_tse_fs_tra_mbh` (#4)**
Heavily T2-weighted TSE FS axial (long TE). Only structures with very long T2 relaxation times remain bright — bile ducts, cysts, haemangiomas, and fluid collections. Solid lesions (HCC, metastasis) darken. This is effectively the axial MRCP-equivalent, separating truly fluid-filled lesions from solid T2-hyperintense lesions. A haemangioma remains bright on heavy T2; an HCC drops signal.

---

**`t2_haste_fs_tra_p2_mbh` (#5)**
T2 HASTE FS axial, p2 accelerated. Motion-robust backup to the T2 TSE FS (#2). If the patient cannot hold their breath consistently for the multi-breath-hold TSE (which requires reproducible diaphragm position across multiple breath-holds), the single-shot HASTE is more forgiving — each slice is independent, so inter-slice motion from inconsistent breath-holds is eliminated.

---

**`t1_vibe_dixon_tra_mbh` (#6)**
T1 VIBE Dixon axial, multi breath-hold. Non-TWIST acquisition — standard VIBE with full k-space sampling per breath-hold. Dixon provides water-only, fat-only, in-phase, and opposed-phase images.

This sequence provides clean Dixon water-fat separation (non-TWIST = no view-sharing compromise) and is the workhorse for pre-contrast T1 assessment:

- **In-phase + water-only pair:** Assess cirrhotic morphology — in-phase preserves fat planes for segmental anatomy, fissures, vessel margins, and volume changes (caudate hypertrophy, right lobe atrophy). Water-only suppresses perihepatic fat, crisply delineating the liver surface for nodularity. Both from the same acquisition so perfectly co-registered. In-phase also assesses intrinsic T1-hyperintensity (blood products, protein, melanin, copper) and iron deposition (haemochromatosis, siderosis — liver abnormally dark).
- **Opposed phase:** Signal dropout confirms intracellular lipid — diffuse steatosis (homogeneous signal loss throughout the liver), or intralesional fat (adenoma, well-differentiated HCC, angiomyolipoma, lipoma). The opposed-phase TE (~1.2 ms at 1.5T, ~1.1 ms at 3T) captures the fat-water phase cancellation.
- **Fat-only:** Distribution of macroscopic fat within a lesion or the liver.

This is a separate acquisition from the TWIST Dixon pre-contrast (#8) because TWIST view-sharing compromises Dixon water-fat separation quality.

**Coverage:** Whole liver.

---

**`t2_trufi_cor_non-bh` (#7)**
T2 TrueFISP (balanced SSFP) coronal, free breathing. TrueFISP has very short TR — effectively motion-insensitive, so no breath-hold is required. Blood and bile are bright without contrast. The coronal plane assesses:
- **Portal vein patency** — portal vein thrombosis is a contraindication to certain locoregional therapies and changes surgical planning
- **Hepatic veins** — patency and drainage pattern for surgical planning
- **IVC** — compression or tumour thrombus
- **Biliary tree** — dilated ducts are bright, providing a coronal MRCP-like view

---

**`t1_vibe_twist_dixon_tra_pre` (#8)**
T1 VIBE TWIST Dixon axial, pre-contrast. Only the water-only image is of interest — TWIST view-sharing compromises Dixon fat-water separation quality, so the in/opposed phase images are unreliable. Fat assessment is handled by the dedicated non-TWIST Dixon (#6). The water-only image provides a fat-suppressed T1 baseline for post-contrast enhancement comparison. Lesion T1 signal relative to liver parenchyma noted before contrast (T1-hyperintense = blood products, proteinaceous content, melanin, copper, fat).

---

### Post-Contrast

**Contrast check:** Before proceeding, confirm the post-contrast FOV and slice prescription match #8 exactly — any shift in position or FOV between pre and post makes enhancement comparison unreliable.

Standard extracellular gadolinium, 2 mL/s. Fixed delay timing.

All post-contrast T1 sequences use TWIST (Time-resolved angiography With Stochastic Trajectories), a view-sharing technique: the k-space centre (contrast-determining) is acquired more frequently than the periphery (detail-determining). This gives high temporal resolution (~3–5 s between phases) without losing spatial resolution. Only the water-only Dixon image is of interest — TWIST compromises water-fat separation.

**`t1_vibe_twist_dixon_tra_bh_art_5phase` (#9)**
Arterial phase, 5 TWIST phases in a single breath-hold. Fixed delay 30 s post-injection. Typical hepatic arterial enhancement: contrast arrives at the hepatic artery ~20–25 s after injection start, peaks at ~30–35 s. Five phases capture the entire arterial passage — from early arterial (hepatic artery only) through late arterial (portal vein starting to enhance). Only one phase is selected for reporting.

**Optimal arterial phase selection:** Portal vein enhanced (confirms bolus has transited the splanchnic circulation), hepatic veins not yet enhanced (contrast has not yet drained through the liver parenchyma). Too early = portal vein dark; too late = hepatic veins bright.

The arterial phase is the single most important sequence in liver MRI:
- **Arterial hyperenhancement** (lesion brighter than liver) = HCC, FNH, adenoma, hypervascular metastasis (NET, RCC, melanoma, breast). A lesion that is not arterially hyperenhancing is unlikely to be HCC.
- **Arterial hypoenhancement** = metastasis (colorectal, pancreatic), cyst, haemangioma (peripheral nodular enhancement).
- The 5 TWIST phases ensure at least one phase captures the peak arterial enhancement of any lesion — lesions enhance at slightly different times depending on their vascular supply.

**`t1_vibe_twist_dixon_tra_PVP` (#10)**
Portal venous phase. 20 s after #9 completes (~50–60 s post-injection). Typical portal venous enhancement peaks at ~60–70 s after injection start — contrast has transited the splanchnic circulation.

The portal vein and hepatic parenchyma are at peak enhancement. The liver is brightly and uniformly enhancing. Lesion behaviour in PVP:
- **Washout** (lesion darker than liver, having been brighter on arterial) = HCC. The portal tracts within the lesion do not retain contrast; the lesion appears hypointense against the enhancing liver background. Arterial hyperenhancement + PVP washout = LR-5 (definite HCC).
- **Persistent enhancement** (lesion remains iso/hyperintense to liver) = FNH, adenoma, haemangioma (peripheral filling). Benign lesions retain contrast in the portal venous phase because they have functional portal venous drainage.
- **Rim enhancement** = metastasis. The periphery enhances (viable tumour, inflamed desmoplastic reaction) while the centre remains hypointense (necrosis).
- **Progressive centripetal filling** = haemangioma. Nodular peripheral enhancement that fills inward toward the centre.

**`t1_vibe_twist_dixon_tra_Delayed_2min` (#11)**
Delayed phase, ~2 min post-injection (50 s gap after #10). Typical extracellular equilibrium at ~2–3 min — contrast has distributed from the intravascular space into the interstitial space.

Contrast has distributed through the extracellular space. Key findings:
- **Capsular enhancement** (pseudocapsule) — HCC may show a thin enhancing rim on delayed images, representing the fibrous capsule.
- **Progressive fill-in** — haemangiomas continue to fill centripetally. A haemangioma that has completely filled by this phase is indistinguishable from liver parenchyma (but clearly abnormal on T2 and arterial).
- **Persistent enhancement** — fibrotic tumours (cholangiocarcinoma, scirrhous HCC) retain contrast in the fibrous stroma and may appear more conspicuous on delayed than on PVP.

**`ep2d_diff_b50_300_800_tra` (#12)**
DWI, single-shot EPI, b=50, 300, 800. Free breathing with signal averaging.

Acquired during the delay between 2 min and 5 min. Free breathing — each TR provides one diffusion-weighted image; signal averaging over multiple TRs improves SNR. Single-shot EPI means each slice is acquired in one shot, so respiratory motion between slices is not problematic (unlike multi-shot).

- **b=50:** Low b-value suppresses capillary perfusion signal while preserving tissue signal. Used as the ADC baseline — functionally equivalent to b=0 but with vessel suppression, so perfusion does not contaminate the ADC calculation.
- **b=300:** Intermediate b-value — above the perfusion-sensitive range (perfusion dominates below b~200) but retaining higher SNR than b=800. Provides a third data point between b=50 and b=800 for a more accurate ADC curve fit.
- **b=800:** High b-value — strongly diffusion-weighted. Restricted diffusion (bright at b=800, dark on ADC) = cellular lesion (HCC, metastasis, lymphoma). Facilitated diffusion (dark at b=800, bright on ADC) = fluid content (cyst, haemangioma, necrotic tumour). Benign haemangiomas may still appear bright at b=800 due to T2 shine-through; the ADC map distinguishes this from true restriction by calculating the signal decay slope across all three b-values.
- **ADC:** Quantitative map calculated from all three b-values. T2 shine-through (bright at b=800 due to long T2, not restricted diffusion) is identified by a high ADC — the signal decays steeply between b-values because water diffuses freely. True restriction shows a shallow decay slope and low ADC (<1.0–1.2 × 10⁻³ mm²/s).

**`t1_vibe_twist_dixon_tra_Delayed_5min` (#13)**
Late delayed phase, ~5 min post-injection.

- **Haemangioma fill-in:** By 5 min, most haemangiomas have filled completely and are isointense to liver. Any non-filling component suggests thrombosis or fibrosis within the haemangioma.
- **Cholangiocarcinoma:** Delayed persistent enhancement — the fibrous stroma of cholangiocarcinoma retains contrast, making it appear brighter at 5 min than at PVP.
This phase assesses persistent enhancement and washout beyond the portal venous phase.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Breath-hold** — Patient able to hold for the post-contrast TWIST VIBE phases (#9–#11, #13)? | If poor compliance: increase parallel imaging factor, reduce phase resolution (partial Fourier), or reduce phase FOV (if liver fits). Test on pre-contrast TWIST (#8) first — if the patient holds successfully and the liver is fully covered, apply to all post-contrast phases |
| **FOV consistency** — Post-contrast FOV and slice prescription match pre-contrast #8? If FOV or coverage is increased, breath-hold should not be prolonged — compensate per the techniques above. Confirm on #8 first |
| **DWI coverage** — Whole liver covered? | DWI is free-breathing — respiratory motion shifts the liver dome during acquisition. Check whole liver is covered |
| **Post-contrast** — Contrast present? Confirm hepatic artery and portal vein enhancement on #8/#9 | If absent: check IV line, confirm injection. At 2 mL/s, extravasation is a risk — check the injection site before and during contrast delivery |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-03 | — | Initial — 13 sequences (HASTE, TSE ± FS, heavy T2, T1 VIBE Dixon, TrueFISP, TWIST Dixon arterial 5-phase, PVP, delayed 2 min + 5 min, DWI b50/300/800) |
