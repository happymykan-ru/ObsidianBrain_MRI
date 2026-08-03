# Primovist (Hepatobiliary Contrast Liver MRI)

**Version:** 1.0 | **Date:** 2026-08-03 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Body matrix coil anteriorly + spine array
- **Laser Landmark:** Centre of body coil (mid-liver, ~xiphoid level)
- **Verbal Instructions:** Same as `liver_routine.md`. End-expiration preferred. Consistent breath-hold depth across all sequences.
- **IV Access:** Minimum 20G (pink). Injection rate: 2 mL/s. Primovist dose: 0.1 mL/kg. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 1 | `t2_haste_cor_mbh` | Coronal | True coronal | A/P: anterior abdominal wall → posterior liver margin. Whole liver | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t1_vibe_dixon_tra_bh` | Axial | True axial | Whole liver | **None** | Breath-hold |
| 3 | `t1_vibe_twist_dixon_tra_pre` | Axial | Copy Slice from #2 | — | **None** | Breath-hold |

### Post-Contrast — Dynamic Phases

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| — | **Contrast** | — | Check FOV consistency — verify post-contrast FOV matches pre-contrast #3. Primovist, 2 mL/s | — | — | — |
| 4 | `t1_vibe_twist_dixon_tra_bh_art_5phase` | Axial | Copy Slice from #3 | Whole liver | **None** | Breath-hold. Fixed delay 30 s |
| 5 | `t1_vibe_twist_dixon_tra_PVP` | Axial | Copy Slice from #3 | — | **None** | Breath-hold, 20 s after #4 |
| 6 | `t1_vibe_twist_dixon_tra_Delayed_2min` | Axial | Copy Slice from #3 | — | **None** | Breath-hold, ~2 min |
| 7 | `t1_vibe_twist_dixon_tra_Delayed_5min` | Axial | Copy Slice from #3 | — | **None** | Breath-hold, ~5 min |

*Dynamic phases are identical to liver_routine.md — arterial, PVP, delayed 2 min, delayed 5 min. TWIST view-sharing, water-only image used. See liver_routine.md for full rationale.*

### Post-Contrast — Hepatobiliary Phase Waiting Period (fill with T2 sequences)

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 8 | `t2_tse_fs_tra_mbh` | Axial | Copy Slice from #2 | Whole liver | **None** | Multi breath-hold |
| 9 | `t2_tse_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 10 | `t2_heavy_tse_fs_tra_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 11 | `t2_haste_fs_tra_p2_mbh` | Axial | Copy Slice from #2 | — | **None** | Multi breath-hold |
| 12 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |
| 13 | `ep2d_diff_b50_300_800_tra` | Axial | Copy Slice from #2 | Whole liver | **None** | Free breathing |

*T2 sequences and DWI are acquired during the ~15 min gap between the delayed 5 min phase (#7) and the hepatobiliary phase (#14). This fills the waiting period efficiently — the total scan time is similar to liver_routine despite the additional hepatobiliary phase.*
*These sequences are identical to their counterparts in liver_routine.md — see that protocol for full rationale.*

### Post-Contrast — Hepatobiliary Phase

| # | Series | Plane | Angulation | Coverage | Sat Band | Breath-Hold |
|---|--------|-------|------------|----------|----------|-------------|
| 14 | `t1_vibe_twist_dixon_tra_hepatobiliary` | Axial | Copy Slice from #3 | Whole liver | **None** | Breath-hold, ~20 min post-injection |

*#14: Hepatobiliary phase. Functioning hepatocytes take up Primovist via OATP transporters — the liver parenchyma is brightly enhancing. Lesions without functioning hepatocytes (metastasis, most HCCs, adenoma) appear dark against the bright liver.*

---

## 3. Sequence Rationale

### Core Strategy

Primovist (gadoxetate disodium) is a hepatobiliary contrast agent with dual properties: early post-contrast phases (arterial, PVP, delayed) behave like a standard extracellular agent for enhancement pattern assessment; the late hepatobiliary phase (~20 min) shows hepatocyte function — functioning hepatocytes take up the contrast via OATP1B1/1B3 transporters and excrete it into bile.

The key difference from `liver_routine.md` is workflow: the T2 sequences are deferred to the post-contrast period, filling the ~15-minute gap between the delayed 5 min phase and the hepatobiliary phase (~20 min). This keeps total scan time efficient — the patient is not idle during the hepatobiliary uptake period.

**Pre-contrast is lean:** only the essential sequences that must be pre-contrast are acquired — T2 HASTE coronal survey, T1 Dixon for fat assessment, and the TWIST pre-contrast baseline. All other T2 and DWI sequences are post-contrast.

---

### Pre-Contrast

**`t2_haste_cor_mbh` (#1)**
Same as liver_routine.md.

**`t1_vibe_dixon_tra_bh` (#2)**
Same as #6 in liver_routine.md — non-TWIST Dixon for clean fat assessment (in/opposed phase, water-only, fat-only).

**`t1_vibe_twist_dixon_tra_pre` (#3)**
Same as #8 in liver_routine.md — pre-contrast TWIST baseline. Water-only image only.

---

### Post-Contrast — Dynamic Phases

**#4–#7:** Arterial 5-phase, PVP, delayed 2 min, delayed 5 min — identical to liver_routine.md. See that protocol for full enhancement pattern rationale (HCC washout, haemangioma filling, FNH persistent enhancement, etc.).

Primovist dose is 0.1 mL/kg — the contrast volume is smaller than standard extracellular agents. This produces a tighter bolus; the arterial timing may be slightly earlier, though the fixed 30 s delay is still adequate. The lower volume also means less dense portal venous and delayed enhancement compared to a full-dose extracellular agent, but the diagnostic patterns (washout, enhancement kinetics) are the same.

---

### Post-Contrast — Hepatobiliary Phase Waiting Period

**#8–#13:** T2 sequences and DWI — identical to their counterparts in liver_routine.md. See that protocol for individual sequence rationale. They are acquired after the delayed 5 min phase, during the ~15 minute waiting period for hepatobiliary uptake. This is purely a workflow efficiency measure — the sequences themselves are unchanged.

---

### Hepatobiliary Phase

**`t1_vibe_twist_dixon_tra_hepatobiliary` (#14)**
T1 VIBE TWIST Dixon axial, ~20 min post-injection. This is the defining sequence of the Primovist protocol.

Primovist is taken up by functioning hepatocytes via OATP1B1/1B3 transporters on the sinusoidal membrane and excreted into bile canaliculi via MRP2. Maximum liver parenchymal enhancement occurs at ~15–25 min post-injection. The liver appears brightly enhancing.

Lesion behaviour in the hepatobiliary phase:

- **FNH:** OATP-positive → iso- or hyperintense to liver. FNH contains functioning hepatocytes with preserved OATP expression. This is the key differentiator from adenoma. A lesion that is arterially hyperenhancing and iso/hyperintense on hepatobiliary phase = FNH.
- **Hepatocellular adenoma:** OATP-negative (most subtypes) → hypointense. Inflammatory adenomas may show mild uptake but are generally dark. The HNF1A-mutated subtype is diffusely hypointense.
- **HCC:** Variable. Well-differentiated HCC may retain OATP expression → iso- or hyperintense. Moderately/poorly differentiated HCC loses OATP → hypointense. A hypointense nodule on hepatobiliary phase in a cirrhotic liver is suspicious for HCC. The combination of arterial hyperenhancement, PVP washout, and hepatobiliary phase hypointensity has high specificity for HCC.
- **Metastasis:** OATP-negative → hypointense. The bright liver background dramatically improves conspicuity of small metastases compared to extracellular agents. The hepatobiliary phase is the most sensitive sequence for detecting liver metastases.
- **Cyst/haemangioma:** No hepatocytes → hypointense. These were already characterized on T2 and dynamic phases.
- **Biliary excretion:** Contrast in the bile ducts provides a functional MRCP — biliary anatomy, leaks, and obstruction can be assessed.

**Timing:** ~20 min post-injection. In patients with normal liver function, 10–15 min may be sufficient. In cirrhotic patients with impaired hepatocyte function, uptake is slower — 20 min is the standard minimum; longer delays (30–40 min) may improve contrast if the 20 min image shows poor parenchymal enhancement.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Hepatobiliary timing** — Liver parenchyma brightly enhancing at 20 min? Bile ducts containing contrast? | If liver is poorly enhancing: hepatocyte function is impaired (cirrhosis, cholestasis, high bilirubin). Extend the delay to 30–40 min. If bile ducts are not visible at 20 min: this is normal — biliary excretion may take longer. Re-image if biliary assessment is critical |
| **Post-contrast** — Contrast present on arterial phase? | If absent: check IV line, confirm injection. Primovist volume is small — a tight, complete bolus is essential |
| **Breath-hold / FOV** — Same considerations as liver_routine.md | See liver_routine.md Alerts |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-03 | — | Initial — 14 sequences (T2 deferred to post-contrast, hepatobiliary phase at ~20 min). Primovist hepatobiliary protocol |
