# Fibroid (Uterine Fibroid MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Centre over the uterus (mid-pelvis, ~2 cm above symphysis pubis).
- **Immobilization:** Pelvic binder.
- **Laser Landmark:** Centre of body coil
- **Verbal Instructions:** Shallow breathing throughout.
- **Buscopan:** Not required. The uterus is fixed by the broad ligament and uterosacral ligaments — bowel peristalsis does not significantly displace it, unlike rectal tumours or prostate (which sit directly against the moving rectal wall).
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. 20G (pink) at 2 mL/s if preferred. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_tse_sag` | Sagittal | True sagittal | Uterus + cervix + vagina. L/R: covering both ovaries and adnexae | **None** | Free breathing |
| 2 | `t2_space_sag_p2_iso` | Sagittal | Copy Slice from #1 | — | **None** | Free breathing |
| 3 | `t2_tse_tra` | Axial | True axial | Uterus + adnexae. S/I: iliac crest → perineum | **None** | Free breathing |
| 4 | `t2_tse_cor` | Coronal | True coronal | Uterus + adnexae. A/P: symphysis → sacrum | **None** | Free breathing |
| 5 | `resolve_diff_b50_800_tra` | Axial | Copy Slice from #3 | Uterus only | **A/P** (anterior + posterior skin margins) | Free breathing |
| 6 | `t1_vibe_dixon_tra_pre` | Axial | Copy Slice from #3 | Uterus + pelvic nodes | **None** | Breath-hold |

*#1: T2 TSE sagittal — primary anatomical plane. Endometrium, junctional zone, myometrium, and fibroid zonal anatomy.*  
*#2: T2 SPACE sagittal — 3D T2 with isotropic resolution. MPR for reformats in any plane.*  
*#3–#4: T2 TSE axial + coronal — orthogonal planes for fibroid mapping.*  
*#5: DWI b=50, 800 — restricted diffusion in cellular fibroids vs degenerated fibroids.*  
*#6: T1 VIBE Dixon axial — pre-contrast baseline. In/opposed phase for fat (lipoleiomyoma) and haemorrhagic degeneration (T1-bright).*  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. 1–2 mL/s (timing not critical). Delay 2 min before scanning | — | — | — |
| 7 | `t1_vibe_dixon_tra_C` | Axial | Copy Slice from #6 | Uterus + pelvic nodes | **None** | Breath-hold |
| 8 | `t1_vibe_dixon_cor_C` | Coronal | Copy Slice from #4 | Uterus + adnexae | **None** | Breath-hold |
| 9 | `t1_vibe_dixon_sag_C` | Sagittal | Copy Slice from #1 | Uterus + cervix | **None** | Breath-hold |

*#7–#9: Post-contrast T1 in all three planes, delayed 2 min. Fibroids enhance (smooth muscle tumours) — the 2 min delay allows contrast accumulation in the interstitial space of the fibroid. Enhances less than myometrium — fibroid appears hypointense relative to the brightly enhancing myometrium.*  

---

## 3. Sequence Rationale

### Core Strategy

Uterine fibroid MRI maps the number, size, and location of fibroids (leiomyomas) for treatment planning: myomectomy, uterine artery embolization, or MR-guided focused ultrasound (MRgFUS). The clinical question: how many fibroids, where are they (submucosal, intramural, subserosal), and are they viable (enhancing) or degenerated (non-enhancing, T2-dark)? T2 anatomy is the primary tool; contrast confirms viability; DWI adds cellularity assessment.

All sequences use true planes (not oblique to the uterus). The uterus varies in position — anteverted, retroverted, anteflexed — between patients and with bladder filling. True planes give standardized, reproducible views across serial scans for treatment monitoring. Unlike cervical or endometrial cancer staging — where oblique planes perpendicular to the cervical canal or endometrial stripe are essential for measuring depth of myometrial invasion and parametrial extension — fibroids are intramural masses. Their relationship to the endometrial cavity and serosal surface is clear on true orthogonal planes regardless of uterine version.

---

### Pre-Contrast

**T2 TSE sagittal (#1):** The primary anatomical plane for the uterus. Shows the endometrial stripe (T2-bright), junctional zone (T2-dark inner myometrium), and outer myometrium (T2-intermediate). Fibroids are well-circumscribed T2-hypointense masses — they are composed of densely packed smooth muscle cells and abundant collagen, which have short T2 relaxation times due to low free water content compared to the more vascular, fluid-rich myometrium. A submucosal fibroid distorts the endometrial cavity; an intramural fibroid is within the myometrium; a subserosal fibroid bulges from the outer uterine contour. The sagittal plane profiles the uterus, cervix, and vagina in one view.

**T2 SPACE sagittal (#2):** 3D T2 with isotropic resolution. MPR provides high-resolution reformats in any plane — useful for mapping multiple fibroids in orthogonal planes from a single acquisition. SPACE also gives a volumetric overview of the uterine size and shape.

**T2 TSE axial (#3) + coronal (#4):** Orthogonal planes for mapping each fibroid in three dimensions. The FIGO classification (0–7) requires accurate localization of the fibroid relative to the endometrial cavity and serosal surface — three planes ensure no fibroid is missed and each is correctly classified.

**DWI (#5):** b=50, 800. Cellular fibroids show restricted diffusion (bright at b=800, dark on ADC) due to dense smooth muscle cells. Degenerated fibroids (hyaline, cystic, or calcified degeneration) show facilitated diffusion (dark at b=800, bright on ADC). DWI helps distinguish the rare leiomyosarcoma from a benign fibroid — sarcoma shows markedly restricted diffusion (very dark ADC) and heterogeneous T2 signal, though no single feature is definitive. DWI also screens for incidental pelvic malignancy.

**T1 VIBE Dixon axial (#6):** Pre-contrast baseline. In/opposed phase for fat — lipoleiomyoma contains macroscopic fat (signal dropout on opposed phase). Haemorrhagic degeneration (infarction of a fibroid) appears T1-hyperintense on pre-contrast (blood products). Intrinsic T1 signal must be documented before contrast to distinguish from enhancement.

---

### Post-Contrast

**T1 VIBE Dixon (#7–#9):** Post-contrast T1 in all three planes, delayed 2 min. Fibroids are benign smooth muscle tumours — they enhance with contrast, but typically less than the surrounding myometrium. A viable fibroid enhances; a degenerated fibroid shows minimal or no enhancement. The 2 min delay allows contrast to accumulate in the interstitial space of the fibroid.

The enhancement pattern maps each fibroid for treatment planning:
- **Enhancing fibroid** = viable, perfused — suitable for embolization (the embolic agent targets the vascular supply) or MRgFUS (perfused tissue absorbs ultrasound energy)
- **Non-enhancing fibroid** = degenerated/infarcted — already non-viable; treatment not directed here
- **Submucosal enhancing fibroid** = candidate for hysteroscopic resection
- **Subserosal pedunculated enhancing fibroid** = candidate for laparoscopic myomectomy

The three-plane post-contrast coverage (axial + coronal + sagittal) maps every fibroid in 3D for procedural planning.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Entire uterus from fundus to cervix on all sequences? Adnexae included? | Reposition if clipped. A pedunculated subserosal fibroid can extend far from the uterine body — check that no fibroid is clipped at the edge of the FOV |
| **Post-contrast delay** — 2 min delay observed? | If scanned immediately after contrast: fibroid enhancement is incomplete, underestimating viability. The 2 min interstitial phase is optimal for fibroid-to-myometrium contrast |
| **DWI** — b=800 tumour conspicuity adequate? ADC map diagnostic? | Same DWI quality checks — see prostate.md. Fibroids are benign but DWI quality affects the ability to detect incidental malignancy |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 9 sequences. T2 in 3 planes + DWI + delayed post-contrast T1 in 3 planes. 2 min delay for fibroid enhancement |
