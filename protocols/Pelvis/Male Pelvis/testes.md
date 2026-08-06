# Testes (Scrotal / Testicular MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. Small FOV centred on the scrotum. Alternatively, a small ultraflex coil may be placed directly over the scrotum for higher SNR.
- **Laser Landmark:** Symphysis pubis
- **Immobilization:** Towel or padding under the scrotum to elevate and support the testes — reduces motion from respiration and keeps the testes at a consistent position. A folded towel between the thighs may help separate the scrotum from the medial thighs.
- **Verbal Instructions:** Shallow breathing throughout.
- **IV Access:** 22G (blue) at 1 mL/s is adequate — no dynamic timing. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_tse_cor` | Coronal | True coronal | Scrotum + both testes + spermatic cords to the external inguinal ring | **None** | Free breathing |
| 2 | `t2_space_sag_p2` | Sagittal | True sagittal | Scrotum + both testes. L/R: both hemiscrotums | **None** | Free breathing |
| 3 | `t2_tse_tra` | Axial | True axial | Scrotum + both testes + spermatic cords to the external inguinal ring | **None** | Free breathing |
| 4 | `t2_stir_tse_tra` | Axial | Copy Slice from #3 | — | **None** | Free breathing |
| 5 | `t1_vibe_dixon_tra` | Axial | Copy Slice from #3 | Scrotum + both testes | **None** | Breath-hold |
| 6 | `t1_vibe_dixon_cor` | Coronal | Copy Slice from #1 | Scrotum + both testes | **None** | Breath-hold |


### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose. No specific delay required | — | — | — |
| 7 | `t1_vibe_dixon_tra_C` | Axial | Copy Slice from #5 | Scrotum + both testes | **None** | Breath-hold |
| 8 | `t1_vibe_dixon_cor_C` | Coronal | Copy Slice from #6 | Scrotum + both testes | **None** | Breath-hold |


---

## 3. Sequence Rationale

### Core Strategy

Testicular MRI characterizes scrotal pathology when ultrasound is equivocal: testicular mass (seminoma vs non-seminomatous germ cell tumour), orchitis, infarction, torsion, or trauma. The protocol uses high-resolution T2 in three planes with STIR for uniform fat suppression, supplemented by pre/post-contrast T1 for enhancement assessment.

**Sequence order:** T2 first — the primary diagnostic contrast. T1 Dixon after — pre-contrast baseline and fat assessment. Post-contrast T1 in two planes.

---

### Pre-Contrast

**T2 TSE coronal (#1):** The primary anatomical plane. Both testes are profiled side-by-side — symmetric size, signal, and contour are assessed. The tunica albuginea is a thin T2-dark line surrounding the testis. The epididymis (head, body, tail) is T2-intermediate. A testicular mass is typically T2-hypointense relative to the bright testicular parenchyma. The coronal plane also profiles the inguinal canals for associated pathology (hernia, cord lipoma).

**T2 SPACE sagittal (#2):** 3D T2 with isotropic resolution. MPR provides reformatted views of each hemiscrotum in any plane. Each testis is profiled sagittally — the epididymis is posterior and the tunica vaginalis is assessed for hydrocele.

**T2 TSE axial (#3):** Orthogonal plane. The spermatic cord (vas deferens, testicular vessels) is tracked through the inguinal canal to at least the external inguinal ring. Cord involvement by tumour or inflammation tracking proximally must be identified. The relationship of a mass to the tunica albuginea (intratesticular vs extratesticular) is confirmed axially.

**T2 STIR axial (#4):** Uniform fat suppression. The scrotum has multiple air-skin interfaces (between the scrotal wall, thighs, and perineum) where chemical FS would fail patchily due to B0 inhomogeneity. STIR, being inversion-recovery-based, is immune to this. STIR is primarily for inflammation: orchitis and epididymo-orchitis appear as diffuse T2-hyperintensity — the oedema is brightest on STIR against dark suppressed fat. STIR also shows extratesticular inflammatory spread into the scrotal wall and spermatic cord. Tumour characterization relies on the non-FS T2 (#1, #3) and post-contrast enhancement; STIR supplements by identifying associated inflammatory change.

**T1 VIBE Dixon axial + coronal (#5, #6):** Pre-contrast baseline. Intrinsic T1-hyperintensity — haemorrhage (trauma, torsion), proteinaceous content, or fat (cord lipoma — signal dropout on opposed phase).

---

### Post-Contrast

**T1 VIBE Dixon axial + coronal (#7, #8):** Post-contrast T1. Normal testicular parenchyma enhances symmetrically. Asymmetric decreased enhancement suggests torsion (absent perfusion), segmental infarction, or an ischaemic tumour. A solid testicular mass enhances (seminoma enhances avidly and uniformly; non-seminomatous tumours enhance heterogeneously with necrosis). Orchitis shows diffuse increased enhancement. The coronal plane allows side-by-side comparison of testicular enhancement.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Positioning** — Scrotum elevated and supported? Both testes at the same level? | If the scrotum is compressed between the thighs: the testes are displaced asymmetrically — comparison is unreliable. Use a towel under the scrotum to elevate |
| **Coverage** — Both testes included? Spermatic cord covered to at least the external inguinal ring (pubic tubercle level)? | The external inguinal ring is at the pubic tubercle — just superior and lateral to the pubic symphysis, where the cord exits the canal to enter the scrotum. If the cord is clipped below this: proximal cord involvement is missed. Extend through the canal to the internal ring if cord pathology is suspected |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 8 sequences. T2 coronal primary + STIR axial. Small-FOV scrotal protocol. Pre/post T1 Dixon |
