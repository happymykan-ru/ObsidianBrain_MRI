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
