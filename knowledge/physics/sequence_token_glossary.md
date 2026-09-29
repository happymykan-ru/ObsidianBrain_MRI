# Sequence Token Glossary — Vault → Generic Type

**Version:** 1.0 | **Date:** 2026-09-08

The reverse index connecting the general knowledge files to the protocol tokens. Every sequence family that appears anywhere in `/protocols/` maps to its generic type, its physics entry, and the body regions that use it. The general rule for reading a token — `weighting_family_fatsat_plane` plus suffixes (`_p2` GRAPPA, `_C` contrast, `_bh/_mbh/_trig` breathing, `_dyn`, `_iso`, `_cs4/6`, `_sms`) — is in the hub: [[pulse_sequences]].

Physics references: [[02_spin_echo_family]] · [[03_gradient_echo_family]] · [[04_epi_and_diffusion]] · [[05_angiography_and_flow]] · [[06_cardiac_sequences]] · [[07_spectroscopy_and_functional]] · [[08_options_and_parameters]]

| Token pattern | Generic type | Physics | Regions using it |
|---|---|---|---|
| `t1_se_*` | Conventional spin echo | 02 §1 | Head & Neck, MSK, Head |
| `t2_tse_*`, `t1_tse_*`, `pd_tse_*`, `pd+t2_tse_*`, `t2_heavy_tse_*` | TSE 2D (incl. dual-echo PD+T2, heavy T2) | 02 §2 | all nine regions |
| `t2_tse_tra_3_echos_*` | 3-echo TSE (PD/inter/T2 in one train) | 02 §2 | Head (paediatric) |
| `t2_tse_flair*`, `t2_tse_dark_fluid*`, `t2_dark_fluid*`, `t2_flair_fs*` | FLAIR | 02 §3 | Head, Head & Neck |
| `t2_stir*`, `t2_tirm*`, `t2_tirm_15_db*`, `stir_tse*` | STIR / TIRM (incl. dark-blood) | 02 §3 | Head & Neck, MSK, Spine, Pelvis, Cardiac |
| `dir_space_*` | DIR (double inversion recovery) | 02 §3 | Head |
| `t2_space*`, `pd_space*`, `t1_space*`, `t2_tse3d*`, `t2_spc*` | 3D TSE / SPACE | 02 §4 | Head, Spine, Abdomen, Pelvis, MSK, Head & Neck, Breast |
| `t2_haste*`, `t2_heavy_haste*`, `haste_localizer` | HASTE (single-shot TSE) | 02 §5 | Abdomen, Head & Neck, Pelvis, Intervention |
| `t2_blade*`, `t1_blade*`, `pd_blade*`, `t2_fblade*`, `t2_dark_fluid_blade*` | BLADE (incl. fastBLADE) | 02 §6 | Head, Abdomen, Spine, MSK, Intervention |
| `t1_tse_r*`, `t1_se_r*`, `t2_tseR*`, `t2_tseR*` | Restore / driven equilibrium | 02 §7 | Head (pituitary/IAM), Head & Neck, Spine, Pelvis |
| `t2_haste_diff*` | Non-EPI DWI (HASTE-DWI) | 02 §8 | Head & Neck (IAM — 1.5T) |
| `t1_fl2d*`, `t1_fl3d*`, `t2_fl2d*` | FLASH (spoiled GRE 2D/3D) | 03 §1 | Head, Head & Neck, MSK, Breast |
| `t1_vibe*` (incl. `_dixon`, `_fs`, `CAIPIRINHA`, `_dyn`) | VIBE (3D spoiled GRE) | 03 §2 | all except Intervention |
| `t1_mprage*`, `t1_mp2rage*`, `t1_tfl*`, `tfl13*` | Magnetization-prepared GRE (MPRAGE/MP2RAGE/TurboFLASH) | 03 §3 | Head, Abdomen, Cardiac |
| `t2_trufi*`, `cine_tfi*`, `cine_tf2d13*`, `cine_trufi*`, `trufi_*`, `native_truefisp*` | Balanced SSFP (TrueFISP) | 03 §4 | Cardiac, Abdomen, Intervention |
| `t2_me2d*`, `t2_me3d*` | MEDIC (multi-echo GRE) | 03 §5 | Spine, MSK |
| `fl2d5_*echo*`, `fl2d1_*echo*`, `T2StarMap*` | T2* mapping | 03 §6 | Cardiac, Abdomen |
| `t2_swi3d*` | SWI | 03 §7 | Head |
| `t1_starvibe*` | StarVIBE (radial VIBE) | 03 §8 | Abdomen, Head & Neck, Pelvis, Intervention |
| `TWIST*`, `twist_*`, `t1_vibe_twist_dixon*` | TWIST (view-sharing) | 03 §9 | Head, Abdomen, Pelvis, Head & Neck |
| `dynamic_tfl_sr*` | SR-TurboFLASH first-pass perfusion | 03 §10 / 06 §6 | Cardiac |
| `resolve_diff*`, `resolve_diffusion*`, `resolve_3scan_trace*`, `resolve_4scan_trace*` | Readout-segmented EPI DWI (RESOLVE) | 04 §2 | Head, Head & Neck, Breast, Pelvis |
| `ep2d_diff*` | Single-shot EPI DWI | 04 §2 | Abdomen, Head |
| `ep2d_diff_sms_mddw*` | DTI (SMS) | 04 §3 | Head |
| `ep2d_perf*` | DSC perfusion (incl. Diamox pairs) | 04 §4 | Head |
| `ep2d_pace_moco*`, `gre_field_mapping` | BOLD fMRI (+field map) | 04 §5 | Head |
| `ep2d_tra_hemo` | EPI T2* hemorrhage screen | 04 §6 | Head |
| `TOF_3D*`, `TOF_fl3d*` | TOF MRA | 05 §1 | Head, Head & Neck |
| `flow_*_retro_bh_ao` (VENC 150/400) | Phase-contrast flow (cine PC) | 05 §2 / 06 §2 | Cardiac |
| `angio3d_*`, `care_bolus*`, `test_bolus*` | CE-MRA | 05 §3 | Abdomen, Head & Neck |
| `native_truefisp_*` | NATIVE (non-contrast bSSFP MRA) | 05 §4 | Abdomen |
| `TWIST_HEAD*`, `twist_pelvis*` | Time-resolved MRA/MRV | 05 §5 | Head, Pelvis |
| `t2_space*_MRCP/ERCP`, `t2_tse3d*_MRCP/ERCP`, MRU/myelography/sialogram tokens | Hydrography (heavy-T2 3D) | 05 §6 | Abdomen, Spine, Head & Neck |
| `cine_*` (all) | Cine bSSFP | 06 §1 | Cardiac |
| `t1_map_*`, `t1map_*` (native/stress/post-C) | T1 mapping (MOLLI) | 06 §3 | Cardiac |
| `t2_map_trufisp*` | T2 mapping | 06 §4 | Cardiac |
| `fl2d5_10echo_heart`, `T2StarMap_8echo*` | Cardiac T2* mapping | 06 §5 | Cardiac |
| `de_overview_tfi*`, `de_trufi_overview_*_psir_fb`, `de_high-res_tfl*`, `ti_scout*` | LGE (TrueFISP overviews — magnitude + PSIR + TI scout) | 06 §7 | Cardiac |
| `csi_slaser_135` | MRS (sLASER CSI) | 07 §1 | Head |

**Notes —**
- Head = `protocols/Head Aug 2025` + related; "all nine" = Abdomen, Breast, Cardiac, Head, Head & Neck, Intervention, MSK, Pelvis, Spine.
- Cardiac T2\* (`fl2d5_10echo`) and liver T2\* (`fl2d1_14echo`) are the same physics (03 §6) applied to different organs.
- Tokens not listed here (e.g. scout/localizer tokens, `_bc` cryo variants of listed families) are variants of their listed family — the suffix meaning table in the hub decodes them.

---

**Version Control**

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-08 | — | Initial — full vault token coverage |
