# Undescended Testes (Cryptorchidism Localization MRI with Contrast)

**Version:** 1.0 | **Date:** 2026-08-06 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, feet-first
- **Coil:** Body matrix coil anteriorly + spine array. The undescended testis may be anywhere from the renal hilum to the inguinal canal — coverage must span the abdomen and pelvis.
- **Laser Landmark:** Umbilicus (mid-abdomen, covering renal hilum through inguinal region)
- **Verbal Instructions:** Shallow breathing throughout.
- **IV Access:** 22G (blue) at 1 mL/s is adequate. Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

### Pre-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| 1 | `t2_haste_cor_p3_mbh` | Coronal | True coronal | Abdomen + pelvis. Renal hilum → symphysis pubis | **Superior oblique** over heart | Multi breath-hold |
| 2 | `t2_tse_tra_pelvis` | Axial | True axial | Pelvis. Iliac crest → perineum | **None** | Free breathing |
| 3 | `t2_tse_sag_pelvis` | Sagittal | True sagittal | Pelvis. L/R: both inguinal canals | **None** | Free breathing |
| 4 | `t1_tse_dixon_tra_pelvis` | Axial | Copy Slice from #2 | Pelvis. Iliac crest → perineum | **None** | Free breathing |
| 5 | `t1_tse_dixon_cor_pelvis` | Coronal | Copy Slice from #1 | Abdomen + pelvis. Renal hilum → symphysis pubis | **None** | Free breathing |
| 6 | `t2_trufi_cor_non-bh` | Coronal | Copy Slice from #1 | — | Copy Sat from #1 | Free breathing |

*#1: T2 HASTE coronal — whole abdomen survey. The undescended testis could be anywhere from the renal hilum (retroperitoneal) to the inguinal canal; the entire migration path must be surveyed.*  
*#2–#3: T2 TSE axial + sagittal pelvis — the most common location is the inguinal canal. High-resolution pelvic survey.*  
*#4–#5: T1 TSE Dixon axial + coronal — pre-contrast baseline. TSE avoids susceptibility at the inguinal region. *  

### Post-Contrast

| # | Series | Plane | Angulation | Coverage | Sat Band | Breathing |
|---|--------|-------|------------|----------|----------|-----------|
| — | **Contrast** | — | Check FOV consistency. Standard dose | — | — | — |
| 7 | `twist_pelvis_venogram_C` | Coronal | TWIST angiography. Coronal slab covering the IVC, gonadal veins, and inguinal canals | Renal hilum → symphysis pubis | **None** | Shallow breathing. Multiple phases over ~3 min. Inject contrast after 1st measurement |
| 8 | `t1_tse_dixon_tra_pelvis_C` | Axial | Copy Slice from #4 | Pelvis | **None** | Breath-hold |
| 9 | `t1_tse_dixon_cor_pelvis_C` | Coronal | Copy Slice from #5 | Abdomen + pelvis | **None** | Breath-hold |

*#7: TWIST pelvis venogram — The venous drainage pattern helps localize the undescended testis.*  
*#8–#9: Post-contrast T1 axial + coronal. Enhancing testicular parenchyma confirms the undescended testis is present and viable (enhancement = perfusion).*  

---

## 3. Sequence Rationale

### Core Strategy

Undescended testis (cryptorchidism) localization is an **anatomical localization and viability assessment**, not a pathological screening. The clinical questions are: where is the testis, and is it viable? Once the testis is located and confirmed perfused, management proceeds to orchidopexy or orchidectomy. If pathology is present (tumour, inflammation), it would be characterized on `testes.md` after orchiopexy brings the testis into the scrotum.

The undescended testis may be anywhere along its embryological migration path — from the retroperitoneum (renal hilum level) through the inguinal canal to the scrotum. The protocol uses a large-FOV survey (HASTE coronal entire abdomen+pelvis), high-resolution pelvic sequences, a TWIST venogram to track the testicular vein and confirm testicular identity, and post-contrast T1 to confirm viability.


**Key differences from `testes.md`:**

- **Large FOV — abdomen + pelvis** — the undescended testis may be anywhere from the renal hilum to the scrotum. Testes protocol is small-FOV scrotum only.
- **TWIST pelvis venogram** — the testicular vein (gonadal vein) drains the testis and its course leads to the undescended testis. Time-resolved venous imaging tracks the vein from the testis through the inguinal canal and retroperitoneum. Testes protocol does not need venography.
- **No STIR** — inflammation assessment is not needed (anatomical localization and viability, not pathology screening).
- **No dedicated scrotal sequences** — the scrotum is empty (or contains the contralateral normal testis only). The target is the undescended testis along the migration path.
- **T1 TSE Dixon (not VIBE)** — the undescended testis is small and often lies in the inguinal canal adjacent to bowel. TSE is less susceptible to the air-soft tissue interface than VIBE, avoiding artefact that could obscure a small enhancing nodule.

---

### Pre-Contrast

**T2 HASTE coronal (#1):** Whole abdomen + pelvis survey. The embryological migration path of the testis is from the urogenital ridge (renal hilum) through the retroperitoneum, into the inguinal canal, and down to the scrotum. The undescended testis could be anywhere along this path — the HASTE coronal surveys the entire route in one view. The undescended testis is a small T2-intermediate oval structure.

**T2 TSE axial + sagittal pelvis (#2, #3):** The most common location is the inguinal canal (80% of undescended testes). High-resolution pelvic T2 in two planes profiles the canal and the external ring.

**T1 TSE Dixon axial + coronal (#4, #5):** Pre-contrast baseline. The primary purpose is the water-only (fat-suppressed) image — the undescended testis sits in retroperitoneal or inguinal fat. Without FS, the enhancing testis post-contrast (#8, #9) is isointense to bright fat and can be invisible.

**T2 TrueFISP coronal (#6):** Vessels bright without contrast. The testicular vein and pampiniform plexus are identified — their course guides the search for the undescended testis. Free-breathing, motion-insensitive.

---

### Post-Contrast

**TWIST pelvis venogram (#7):** Time-resolved TWIST angiography in the coronal plane. The clinical need: an atrophic undescended testis may be morphologically indistinguishable from a lymph node, collapsed bowel, or other soft tissue on T2 alone — a small oval T2-intermediate structure in the retroperitoneum or inguinal canal has several possible identities. The testicular vein (gonadal vein) drains the testis and runs alongside it — if the testis is present, the vein is present and leads directly to it. The TWIST venogram tracks the gonadal vein from its drainage (right → IVC at L2, left → left renal vein) caudally to the testis. If the vein ends blindly without reaching a testis, the testis is absent (anorchia) or completely atrophic with no venous drainage. The TWIST also shows the testicular parenchymal blush on later phases — enhancement confirms viability, distinguishing a viable undescended testis from an atrophic remnant that does not enhance.

**T1 TSE Dixon axial + coronal (#8, #9):** Post-contrast T1. Enhancing testicular parenchyma confirms the undescended testis is perfused and viable. A non-enhancing testis suggests atrophy or infarction.

---

## 4. Alerts

| Check | Improve |
|---|---|
| **Coverage** — Entire migration path from renal hilum to inguinal canal surveyed? | If the intra-abdominal testis (at the renal hilum) is missed: the undescended testis is reported as absent — incorrect. The HASTE coronal (#1) must include the renal fossae |
| **TWIST venogram** — Testicular vein identified? Leads to the undescended testis? | If the vein is not visualized: the testis may be atrophic (vein is small or absent). The T1 post-contrast (#8, #9) should still show enhancing testicular tissue |
| **Contrast** — Undescended testis enhances? | If non-enhancing: the testis is atrophic or infarcted — this changes management (orchidectomy vs orchidopexy) |

---

## 5. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-08-06 | — | Initial — 9 sequences. Large-FOV abdomen+pelvis survey. TWIST venogram for testicular vein tracking. Pre/post T1 for viability |
