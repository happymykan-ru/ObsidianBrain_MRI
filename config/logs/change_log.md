# MRI Brain — Change Log

## 2026-07-18 Session

| File | Status | Change |
|------|--------|--------|
| `/protocols/Head Aug 2025/plain_brain.md` | ✅ Complete | Initial protocol created — 5 sequences (t2_tse_tra, t1_mprage_cor, MPR reformat, t2_tse_flair_tra, resolve_diffusion_tra) |
| `/protocols/Head Aug 2025/plain_brain.md` | ✅ Revised | Removed breathing, added copy slice/copy center, added sat band placement, condensed to single table |
| `/protocols/Head Aug 2025/contrast_brain.md` | ✅ Complete | Initial protocol created — 7 sequences (3 pre, DWI fills delay, 3 post-contrast) |
| `/protocols/Head Aug 2025/fast_brain.md` | ✅ Complete | Initial protocol created — 10 sequences (accelerated p2/p3, EPI hemo, multi-plane post-contrast) |
| `/protocols/Head Aug 2025/fast_brain.md` | ✅ Rewritten | Split into ultra-fast only (all ~20 s, 9 sequences) — standard TSE + FLASH + EPI |
| `/protocols/Head Aug 2025/blade_brain.md` | ✅ Complete | New protocol — 8 sequences (BLADE T2/T1/FLAIR + RESOLVE DWI, motion-robust) |
| `/protocols/Head Aug 2025/cerebral_angiogram+brain.md` | ✅ Complete | Initial — 9 sequences (TOF MRA + brain, FLASH 2D instead of MPRAGE pre-contrast) |
| `/protocols/Head Aug 2025/cerebral_angiogram(no_brain_request).md` | ✅ Complete | Initial — 5 sequences (focused TOF + basic brain, detailed TOF coverage rationale) |
| `/protocols/Head Aug 2025/IAM+brain.md` | ✅ Complete | Initial — 9 sequences (T2 SPACE IAM + full brain ± contrast) |
| `/protocols/Head Aug 2025/IAM(no_brain_request).md` | ✅ Complete | Initial — 7 sequences (focused IAM, T2 SPACE + T1 TSE FS targeted) |
| `/protocols/Head Aug 2025/orbit.md` | ✅ Complete | Initial — 6 sequences + 2 optional (STIR, Dixon, TSE-only, dynamic VIBE, oblique sagittal) |
| `/protocols/Head Aug 2025/pituitary.md` | ✅ Complete | Initial — 6 sequences (TSE-only, dynamic coronal, fat sat post-contrast) |
| `/protocols/Head Aug 2025/pituitary+brain.md` | ✅ Complete | Initial — 10 sequences (full brain + targeted pituitary) |
| `/protocols/Head Aug 2025/epilepsy.md` | ✅ Complete | Initial — 10 sequences (MP2RAGE, SWI, coronal oblique hippocampal, FLAIR) |
| `/protocols/Head Aug 2025/MS.md` | ✅ Complete | Initial — 10 sequences (DIR SPACE replaces FLAIR, orbit screening, post-contrast DWI delay) |
| `/protocols/Head Aug 2025/Brain/` | ✅ Reorganized | All 14 brain protocols moved into `Brain/` subdirectory |
| `/protocols/Head Aug 2025/NS/brain+viewing_wand.md` | ✅ Complete | Initial — 7 sequences (FLASH 3D sagittal for neuronavigation, no fat sat for geometric accuracy) |
| `/protocols/Head Aug 2025/NS/EC_IC_bypass.md` | ✅ Complete | Initial — 6 sequences (TOF + TWIST for bypass patency, extended STA coverage) |
| `/protocols/Head Aug 2025/NS/diamox.md` | ✅ Complete | Initial — 8 sequences + optional TOF (Diamox-challenged DSC ×2, cerebrovascular reserve mapping) |
| `/protocols/Head Aug 2025/RT/X-knife_SRS.md` | ✅ Complete | Initial — 2 branches (Tumor: 5 seq; AVM: 5 seq). FLASH 3D sagittal, T2 SPACE, geometric accuracy priority |
| `/protocols/Head Aug 2025/Brain/fMRI.md` | ✅ Complete | Initial — 13 sequences (7 fMRI paradigms, DTI 20-dir SMS, field map, standard brain) |
| `/protocols/Head Aug 2025/Paed/paed_brain.md` | ✅ Complete | Initial — 2 age pathways (<2yr + >2yr), multi-echo T2 for immature brain, FLAIR >1yr only |
| `/protocols/Head Aug 2025/Paed/paed_orbit.md` | ✅ Complete | Initial — 5 sequences + retinoblastoma variation (T2 SPACE, oblique sagittal, brain screening) |
| `/protocols/Head Aug 2025/Paed/paed_pit.md` | ✅ Complete | Initial — 6 sequences (age-adapted: SE vs TSE sagittal, dynamic >6yr only) |
| `/protocols/Head Aug 2025/Head & Neck/All head and neck/NP.md` | ✅ Complete | Initial — 7 sequences (StarVIBE, lower neck Dixon, 4-scan DWI, skull base → clavicles) |
| `/protocols/Head Aug 2025/Head & Neck/All head and neck/NP_for_IMRT.md` | ✅ Complete | Initial — 8 sequences (straight axial for IMRT planning, two DWI acquisitions, pre-contrast coronal oblique) |
| `/protocols/Head & Neck/All head and neck/oral_cavity.md` | ✅ Complete | Initial — 8 sequences + variations (Ca tongue sagittal, larynx Dixon) |
| `/protocols/Head & Neck/All head and neck/oral_cavity_for_IMRT.md` | ✅ Complete | Initial — 11 sequences (straight axial, split OC/neck DWI, pre-contrast neck STIR/T1 SE, T2 Dixon coronal, separate lower neck Dixon) |
| `/protocols/Head & Neck/All head and neck/oral_cavity_for_IMRT.md` | ✅ Revised | v1.1 corrections: DWI OC includes skull base, StarVIBE includes vertex + can tilt, VIBE OC starts ventricles, neck/lower neck can tilt |
| `/protocols/Head & Neck/All head and neck/salivary_glands.md` | ✅ Complete | Initial — 9 sequences (DCE, MPR). Two coverage options (parotid-only, all salivary glands) |
| `/protocols/Head & Neck/All head and neck/TM_joint.md` | ✅ Complete | Initial — 5 sequences (dual-echo PD+T2 sagittal, open-mouth PD sagittal, coronal ± contrast). Double oblique sagittal, 2 mm slices |
| `/protocols/Head & Neck/All head and neck/brachial_plexus.md` | ✅ Complete | Initial — 7 sequences (TIRM, fast Dixon throughout, coronal + separate R/L axials + sagittals). C1 → manubrium coverage, head & neck + body coils |
| `/protocols/Head & Neck/Brain & Carotid CeMRA/CeMRA.md` | ✅ Complete | Initial — 14 sequences over 3 phases (brain pre, CeMRA, brain post). TOF + Care Bolus CeMRA in a single contrast injection. Table shifts LOC→ISO→LOC |
| `/protocols/Abdomen/Liver/liver_routine.md` | ✅ Complete | Initial — 13 sequences (HASTE, TSE ± FS, heavy T2, T1 VIBE Dixon, TrueFISP, TWIST Dixon art 5-phase, PVP, delayed, DWI b50/300/800). Multiphasic liver with fixed delay timing |
| `/protocols/Abdomen/Liver/liver_non-bh.md` | ✅ Complete | Initial — 10 sequences (HASTE T2, T1 TFL in/opp, StarVIBE dynamic, DWI, StarVIBE delayed). Free-breathing alternative to liver_routine.md |
| `/protocols/Abdomen/Liver/primovist.md` | ✅ Complete | Initial — 14 sequences (T2 deferred to post-contrast to fill hepatobiliary wait, hepatobiliary phase at ~20 min). Primovist hepatobiliary protocol |
| `/protocols/Abdomen/Liver/primovist_non-bh.md` | ✅ Complete | Initial — 13 sequences (HASTE, TFL, BLADE, StarVIBE dyn + 5/10/20 min). Free-breathing Primovist protocol |
| `/protocols/Abdomen/MRCP/MRCP.md` | ✅ Complete | Initial — 8 sequences (T2 liver screen + T2 SPACE 3D MRCP + 2 thin-slab HASTE projections). Non-contrast ductal protocol |
| `/protocols/Abdomen/MRCP/MRCP_non-bh.md` | ✅ Complete | Initial — 11 sequences. Free-breathing variant: liver_non-bh BLADE screen + MRCP core. Thin slabs respiratory-triggered; 3T FS variant |
| `/protocols/Abdomen/Pancreas/pancreas.md` | ✅ Complete | Initial — 12 sequences. Pancreas-only FOV. TrueFISP coronal. Optional ERCP sequence. Dynamic phases per liver_routine. No delayed 5 min |
| `/protocols/Abdomen/Pancreas/pancreas_non-bh.md` | ✅ Complete | Initial — 9 sequences. Free-breathing pancreas. HASTE T2, TFL trig, StarVIBE dynamic. SPACE ERCP dropped |
| `/protocols/Abdomen/Adrenal/adrenal.md` | ✅ Complete | Initial — 9 sequences. Adrenal-only FOV. Chemical shift primary, dynamics simplified (single AP + PVP axial/coronal) |
| `/protocols/Abdomen/Kidney/kidney.md` | ✅ Complete | Initial — 13 sequences. Renal FOV. Coronal plane + delayed phase + DWI. Single arterial phase. TrueFISP for vascular assessment |
| `/protocols/Abdomen/Kidney/kidney_CeMRA.md` | ✅ Complete | Initial — 9 sequences. CeMRA + single nephrographic T1. Two pathways: Care Bolus or Test Bolus. No multiphasic dynamics, no DWI |
| `/protocols/Abdomen/Kidney/kidney_nativeMRA.md` | ✅ Complete | Initial — 5 sequences. Non-contrast NATIVE TrueFISP renal MRA. Two triggering options: respiratory (PERU) or ECG. No contrast, no DWI |
| `/protocols/Abdomen/Kidney/kidney_MRU.md` | ✅ Complete | Initial — 17 sequences. Split-FOV upper/lower. T2 SPACE + Angio3D excretory phases (2/5/10/15 min). Whole urinary tract from kidneys to bladder |
| `/protocols/Abdomen/Kidney/renal_volume.md` | ✅ Complete | Initial — 5 sequences (×2 kidneys). Oblique coronal, sagittal, and axial for renal volumetry. Non-contrast |
| `/protocols/Abdomen/Enteroclysis/enteroclysis.md` | ✅ Complete | Initial — 16 sequences. TrueFISP cine motility + Buscopan ×2 + split-FOV abdomen/pelvis + arterial/PVP. FL2D coronal post-contrast |
| `/protocols/Pelvis/Male Pelvis/prostate.md` | ✅ Complete | Initial — 8 sequences. Oblique axial/coronal per prostate wall. DWI b=50/500/1500. DCE with 2 baseline measurements. T2 SPACE sagittal 3D |
| `/protocols/Pelvis/Male Pelvis/FIA.md` | ✅ Complete | Initial — 6 sequences. Oblique axial/coronal per anal canal. T2 STIR + T1 TSE + delayed post-contrast T1 Dixon. 2 min delay |
| `/protocols/Pelvis/Male Pelvis/CA_rectum.md` | ✅ Complete | Initial — 11 sequences. Oblique T2 aligned to tumour. Low rectal tumour addendum for anal sphincter. DWI b=50/800 |
| `/protocols/Pelvis/Female Pelvis/fibroid.md` | ✅ Complete | Initial — 9 sequences. T2 in 3 planes + DWI + delayed post-contrast T1 in 3 planes. 2 min delay for fibroid enhancement |
| `/protocols/Pelvis/Female Pelvis/Ca_cervix_or_corpus.md` | ✅ Complete | Initial — 17 sequences (4 optional). Oblique T2 per cervical canal/endometrial stripe. DCE sagittal + subtraction. Whole pelvis DWI. Optional abdominal screen |
| `/protocols/Pelvis/Female Pelvis/brachytherapy_pre-OT.md` | ✅ Complete | Initial — 11 sequences. Head-first treatment position, vaginal gel, 2 mm true axial T2. DWI b=1500. True axial + oblique for CT fusion |
| `/protocols/Pelvis/Female Pelvis/brachytherapy_with_applicator.md` | ✅ Complete | Initial — 4 sequences. Applicator in situ, sequential oblique planning from localizers. Non-contrast verification |
| `/protocols/Pelvis/Female Pelvis/urethral_diverticulum.md` | ✅ Complete | Initial — 8 sequences. T2 in 3 planes + delayed post-contrast T1 + post-micturition imaging. 60 s contrast delay |
| `/protocols/Pelvis/Female Pelvis/incontinence.md` | ✅ Complete | Initial — 7 sequences. T2 in 3 planes + T2 SPACE + pre/post T1 Dixon. Pelvic floor anatomical protocol |
| `/protocols/Pelvis/Female Pelvis/endometriosis.md` | ✅ Complete | Initial — 7 sequences. T2 sagittal primary + axial + SPACE + DWI + pre/post T1. Sagittal + axial post-contrast |
| `/protocols/Pelvis/Female Pelvis/generic_pelvis.md` | ✅ Complete | Initial — 7 sequences. Gender-neutral general-purpose pelvic screening. StarVIBE post-contrast. Two pathology variations (O-RADS, pelvic venous) |
| `/protocols/Pelvis/Male Pelvis/testes.md` | ✅ Complete | Initial — 8 sequences. T2 coronal primary + STIR axial. Small-FOV scrotal protocol. Pre/post T1 Dixon |
| `/protocols/Pelvis/Male Pelvis/undescended_testes.md` | ✅ Complete | Initial — 9 sequences. Large-FOV abdomen+pelvis. TWIST venogram for testicular vein. Pre/post T1 for viability |
| `/protocols/Pelvis/Male Pelvis/penis.md` | ✅ Complete | Initial — 11 sequences. T2 short/long axis + STIR in two planes. Dynamic sagittal post-contrast for plaque activity (Peyronie's). Wide-FOV pelvic survey pre/post. |
| `/protocols/MSK/mass_generic.md` | ✅ Complete | Initial — 7 sequences (6+1 optional). STIR long axis + T1 Dixon long axis + T1 non-FS axial + T2 FS axial. T1 Dixon long C + T1 FS TSE axial C. Dynamic VIBE optional post-op. Adjustment strategies for FOV, resolution, fat sat, phase encoding, sat band & flow comp |
| `/protocols/MSK/shoulder.md` | ✅ Complete | Initial — 8 sequences. PD FS axial + PD coronal + T2 FS cor + T2 FS sag 3mm + T1 sag 4mm. Three-plane T1 FS post-contrast. All planes oblique to glenohumeral joint |
| `/protocols/MSK/knee.md` | ✅ Complete | Initial — 9 sequences (+1 variation). T2 FS sag SMS + 3D PD SPACE CS6 iso + MPR + T1 SE axial + dual-echo PD+T2 FS axial + PD FS coronal. Three-plane T1 FS post-contrast. ACL reconstruction variation with oblique coronal |
| `/protocols/MSK/hip.md` | ✅ Complete | Initial — 5 sequences. T1 cor + T2 FS cor + PD FS sag + T2 Dixon axial + T1 oblique axial (FAI). Non-contrast hip protocol |
| `/protocols/MSK/hip_prosthesis.md` | ✅ Complete | Initial — 6 sequences + contrast. T1 TSE cor SEMAC-15 + T2 TIRM cor SEMAC-10 + T2 TIRM tra SEMAC-8 + T1 TSE tra SEMAC-8, pre/post IV gadolinium, matched-geometry subtraction pairs. Metal artifact reduction (WARP) hip arthroplasty protocol |
| `/protocols/MSK/hip_prosthesis.md` | ✅ Revised | Coronal prescribed oblique ∥ femoral stem long axis (≈ true coronal, tilts for bowed/flexed femur or varus/valgus stem); coverage "why" consolidated into a single shared rationale for both planes |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Complete | Initial — 23 workflow steps. TrueFISP surveys + pseudo-localizer cascade + retro cine (3C/4C/2C/LVOT) + aortic flow VENC 150 + native T1 map + adenosine stress (stress T1 map at peak, stress perfusion, rest perfusion) + SA volumetry + TI scout + DE overviews (4C/2C/SAX/TrueFISP PSIR FB) + high-res FS SAX LGE |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Restructured | v1.1 — workflow overview + dose ledger up front, series table split into phase sub-tables, planning & rationale on the same phase timeline, alerts split pre-stress/stress/post-stress |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Restructured | v1.2 — coverage & planning folded into the sequence rationale; each phase carries its own planning (cascade in Phase 0, cine rules in Phase 1, stack planning in Phases 2 & 5) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.3 — coronal thorax scout marked "plain only" (plain-study sequence); rationale entry removed, row kept in series table |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.4 — sequence rationale re-keyed to protocol sequence names, numbers kept as secondary references |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.5 — phantom `t1_map_positioning` removed; `dynamic_tfl_sr_tpat_sax` (#11) is the positioning/verification run copied by T1 maps and perfusion. Renumbered 23 → 22 sequences |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.6 — #11 role corrected: quick multislice SAX sweep (perfusion format, no contrast) used to place SAB/SAM/SAA — not a 3-slice acquisition |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.7 — #11 purpose stated explicitly: positioning acquisition for T1 map + perfusion stack (localization only). #13 corrected to true pre-contrast baseline with 10 serial measurements |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Restructured | v1.8 — Phase 2 overview-first: what this phase does (geometry → baseline state → perfusion baseline + design rule), then per-sequence entries with nested sub-bullets, condensed T1-mapping explanation in `t1_map` |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.9 — slice placement detailed under #11: levels set on the positioning sweep using the systolic phase of the 4C and 2C cines as long-axis reference (SAB below annulus/LVOT, SAM papillary level, SAA distal to papillary tips) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.10 — systolic-phase rationale: by end-systole the annulus is at its most apical position, so the basal slice placed below it never has the valve enter the plane |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.11 — 5(6)3 generalized into a(b)c sampling notation; RR-specific decision details removed |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.12 — R heart-rate dependence stated: recovery heartbeat count increases as RR interval decreases |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.13 — Phase 3 workflow: water bolus + auto pause, base BP + 180 s countdown (BP @150/90 s), radiologist review, response check (BP↓≥10 or HR↑≥10 → last BP @20 s + cuff deflated / else step-up 60 s), all BP logged |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.14 — stress T1 map timing corrected to 30 s countdown (before the 20 s last BP) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.15 — adequacy response check moved before the stress T1 map: decision after 90 s BP + radiologist review, map acquired only after adequacy confirmed (or step-up) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.16 — Phase 3 timing titles unified to "countdown s (+real s)" format |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.17 — titles explicit "countdown __s (+real s)"; internal paragraph references left unchanged |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.18 — Phase 4 sequence explicit: 6 min wait → dose 2 injection → rest perfusion starts immediately with the injection |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.19 — Phase 4 rationale as bullets (wait → dose 2 → restC); double dose (0.2 mmol/kg) split into three doses stated in dose ledger and Phase 4 |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.20 — Phase 5 timing: 3rd dose immediately before volumetry; DE images ~7 min after the 3rd dose, volumetry fills the wait |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.21 — Phase 5 details: EF volumetry (diastolic planning, whole-ventricle coverage), TI scout at thickest myocardium (uniform dark, no dark rim), DE overviews prospective-gated with full-wall coverage and gradual TI increase |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Restructured | v1.22 — Phase 5 split into Part 1 SAX Volumetry vs Part 2 Late Gadolinium Enhancement with separate rationale blocks |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.23 — terminology corrected: "late gadolinium equilibrium" → "late gadolinium enhancement (LGE)" |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.24 — volumetry mechanism added: Simpson's disk summation, EDV/ESV, EF formula; coverage rules tied to disk integrity |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.25 — DE overviews as sub-bullets (prospective gating); high-res FS SAX = optional 2D after radiologist consult on PSIR, TI set, slice-by-slice toward apex; differences vs overviews/PSIR stated |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.26 — high-res DE name confirmed as `de_hires_tfl_fs_sax` (TurboFLASH); transient `tlf` variant reverted |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.27 — high-res DE renamed `de_high-res_tfl_fs_sax` per protocol card wording |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.28 — "how it differs" bullets enriched: mechanism → resulting image difference → what they look for (vs DE overviews and vs PSIR) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.29 — comparison restructured into nested sub-bullets: Mechanism / Result / What they look for per comparison |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.30 — Q&A added: why both DE overviews and PSIR are needed (opposite failure modes, division of labour), placed before the how-it-differs comparisons |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.31 — "why both DE overviews and PSIR" moved after the high-res entry and restyled to the same bullet + 4-space sub-bullet structure as the how-it-differs section |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.32 — Q&A bullets condensed: "why both" 5 → 3 sub-bullets, how-it-differs trimmed, key content preserved |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.33 — false negative / false positive labels restored; "What they look for" restored to full wording in both comparisons |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.34 — physics correction: too-short TI nulls the subendocardial tissue itself (earlier null point from gadolinium-shortened T1) → scar dark (false negative), not blood-pool nulling |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.35 — "why both" actor tightened to "the infarct itself that nulls"; TI-scout dark-rim wording kept as original (blood pool nulling + interface partial volume, per user) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.36 — TI-scout dark rim completed: rim = interface voxels partial-volumed between nulled blood pool and myocardium |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.37 — comparison headings de-confused ("How the high-res series differs…"); ambiguous "it"/"this series" replaced |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.38 — pre-stress alerts reordered (caffeine → Gd dose/eGFR → contrast line → ECG → breath-hold → VENC); emergency-equipment row moved to top of Stress phase |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.39 — total Gd dose alert: double-dose rationale + eGFR < 30 → consult radiologist (dose adjustment / Gadovist) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.40 — contrast-line alert: correct gauge, R side contrast / L side adenosine, BP cuff off the adenosine side |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.41 — ECG alert: choose the lead with the cleanest R wave for gating |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.42 — sequence names fixed: stress_C / rest_C (C separate, capitalized) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.43 — stress-phase alert: "Perfusion start" → "Perfusion breath-hold" (shallow, held as long as possible, then normal breathing) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.44 — post-stress alert reframed as "Myocardial nulling": check on DE + high-res series, normal nulling TI ≈ 300 ms, re-scout if shifted |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.45 — post-stress wrap-around check added: increase FOV if wrapping appears |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.46 — full-document audit: countdown-30s timing unified in Core Strategy + response check |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.47 — **D**otaram restored to total-Gd alert (contrast agent, not a typo) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.48 — workflow overview rewritten as natural-language phase bullets |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.49 — workflow overview as a compact two-column step table (one line per phase) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.50 — workflow overview step table converted to bullet-point variant |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.51 — workflow overview finalized: Phase 0–5 arrow-chain bullets with inline stress branch |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.52 — workflow overview: best of both — Phase labels + terse arrows with (#) refs + italic stress branch |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.53 — caffeine withdrawal split into its own preparation bullet; contraindication screen lists only true contraindications |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.54 — caffeine back in the contraindication screen as the contraindicating condition (not withdrawn ≥12–24 h) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.55 — breath-hold corrected to end-inspiration; small consistent breath-holds (not oversized); table #1 → BH (end-insp) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.56 — long-breath-hold coaching added: perfusion = one long hold; when unable, shallow normal breathing, never re-breath-hold |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.57 — IV access: eGFR threshold stated (above 30) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.58 — bullet retitled "eGFR check" (was "IV Access for Contrast") |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.59 — dose ledger: all three contrast doses at 4 ml/s (Phase 4 + Phase 5 table rows harmonized too) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.60 — double dose unit updated to 0.4 ml/kg |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.61 — dose ledger: Dotaram/Gadovist concentration note (0.4 ml/kg ↔ 0.2 mmol/kg; halve volume if Gadovist) |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.62 — total dose reverted to 0.2 mmol/kg, note removed |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Revised | v1.63 — total dose 0.2 mmol/kg with concentration note restored |
| `/protocols/Cardiac/cardiac_stress.md` | ✅ Finalized | Version history consolidated to a single 1.0 initial-build row (all iterations considered the first build) |
| `/protocols/Cardiac/cardiac_non-stress.md` | ✅ Complete | Initial version — 18 workflow steps. Rest CMR: axial localizer + pseudo-cascade + retro cines + flow VENC 150 + native T1 + T2 map + single-dose contrast 2 ml/s + SA volumetry + LGE block (TI scout, overviews, PSIR FB, T1 seg FS SA). No stress arm — equivalent sequences condensed with references to cardiac_stress.md |
| `/protocols/Cardiac/myocarditis.md` | ✅ Complete | Initial version — 23 workflow steps. Non-stress base + myocarditis channels: T2 TIRM 15-slice dark-blood SA stack, early enhancement block (EGE optional + early TI scout + early PSIR 3-plane), PSIR overviews both phases, high-res FS SAX |
