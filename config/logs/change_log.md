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
