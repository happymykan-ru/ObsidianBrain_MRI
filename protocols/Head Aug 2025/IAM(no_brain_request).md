# IAM (Internal Auditory Meatus, No Brain Request)

**Version:** 1.0 | **Date:** 2026-07-19 | **Scanner:** [Confirm 1.5T/3T]

---

## 1. Patient Positioning & Coil Setup

- **Position:** Supine, head-first
- **Coil:** Head coil
- **Laser Landmark:** Glabella
- **Immobilization:** Foam padding between head and coil
- **IV Access:** 20G (pink) or 22G (blue). Injection rate: 2 mL/s (20G) or 1.5 mL/s (22G). Standard dose. Saline flush: [Confirm volume].

---

## 2. Imaging Series

| # | Series | Plane | Angulation | Coverage | Sat Band |
|---|--------|-------|------------|----------|----------|
| 1 | `t2_tse_tra_brain` | Axial | ∥ AC-PC line | Foramen magnum → vertex | **Inferior** (neck vessels) |
| 2 | `t1_fl2d_tra_brain` | Axial | Copy Slice from #1 | — | **None** |
| 3 | `t2_space_tra_iso_IAM` | Axial | ∥ AC-PC line | Upper medulla → mid-pons (~30–40 mm) | **None** |
| 4 | `resolve_3scan_trace_tra_p2` | Axial | Copy Slice from #1 | — | **None** |
| — | **Contrast** | — | — | — | — |
| 5 | `t1_vibe_fs_cor_brain_C` | Coronal | ⟂ AC-PC line | Frontal sinus → occipital pole | **Inferior** |
| 6 | `MPR` | Sag+Ax | — | Whole brain | — |
| 7 | `t1_tse_fs_tra_3mm_IAM_C` | Axial | Copy Slice from #3 | — | **None** |

---

## 3. Sequence Rationale

This is a focused IAM screening protocol. Brain sequences are minimal — enough for anatomical reference and basic parenchymal context. The diagnostic weight is on the IAM-targeted sequences (#3, #7).

**`t2_tse_tra_brain` (#1)**
Core axial T2 anatomy. Reference plane. Provides parenchymal context — brainstem or CPA pathology that mimics IAM symptoms.

**`t1_fl2d_tra_brain` (#2)**
Pre-contrast T1 baseline. FLASH 2D — matched geometry for post-contrast comparison and subtraction. No sat band.

**`t2_space_tra_iso_IAM` (#3)** — Primary Screening Sequence
3D T2 SPACE with isotropic resolution. CSF is bright, nerves and vessels dark (cisternographic effect) — the 7th/8th nerve complexes are visible against CSF. Vestibular schwannoma: CPA mass extending into or widening the IAM.

*Plane:* Axial source. Coronal reformat (not part of the standard sequence but recommended) — profiles the IAM in-plane, showing canalicular extension and cochlear relationship that axial alone can miss.

*Resolution:* Isotropic voxels essential (e.g., 0.6 mm). Slice thickness must equal in-plane resolution for diagnostic reformats — changing it breaks isotropy and degrades coronal views.

*Sequence choice:* SPACE (TSE-based 3D) avoids the susceptibility artefact that plagues GRE at the petrous apex (air cells → field inhomogeneity → signal dropout). TSE's 180° refocusing pulses correct for static field inhomogeneity.

*Coverage:* Upper medulla → mid-pons (~30–40 mm). The 7th/8th nerve travels ~10–15 mm from pontomedullary junction root entry zone through the CPA cistern into the IAM fundus. Inferior boundary captures the CPA cistern. Superior boundary at mid-pons captures the 5th nerve root entry zone. Centering on the bony IAM alone clips the cisternal segment where small tumours first appear.

*Slice oversampling (0%):* The small slab needs enough coverage for the full nerve course. Adding oversampling would either add scan time or force a smaller slab that clips anatomy. Wrap from outside the slab lands at the edges, away from the centrally-positioned IAMs — provided the slab is properly centred (see Alerts).

**`resolve_3scan_trace_tra_p2` (#4)**
RESOLVE DWI. Acute ischaemia, abscess. Less distortion at skull base vs single-shot EPI.

**Contrast**
Standard dose IV gadolinium. Post-contrast T1 brain (#5) runs first to allow sufficient enhancement time for the IAM sequence (#7). IAM tumour enhancement peaks slightly later than brain parenchyma.

**`t1_vibe_fs_cor_brain_C` (#5)**
3D T1 post-contrast coronal with fat saturation. Brain enhancement screening — skull base, meninges. Source data for MPR (#6). Placed before the IAM T1 to allow adequate delay for IAM tumour enhancement.

**`MPR` (#6)**
Multiplanar reconstruction from post-contrast VIBE (#5). Sagittal and axial views.

**`t1_tse_fs_tra_3mm_IAM_C` (#7)**
Diagnostic post-contrast T1 TSE with fat saturation, 3 mm slices through the IAMs. Vestibular schwannomas and meningiomas enhance avidly. TSE (not GRE) is essential at the petrous apex — 180° refocusing pulses correct for static field inhomogeneity from air-bone interfaces. GRE would bloom and obscure the IAM/CPA. Fat sat suppresses petrous marrow fat that can mask thin enhancing tumour along the canal. Matched geometry to T2 SPACE (#3) for side-by-side comparison.

---

## 4. Pathology-Based Variations

- **Facial nerve pathology:** Standard IAM coverage is sufficient — the facial nerve shares the same CPA → IAM course as the vestibulocochlear nerve. T2 SPACE (#3) traces the nerve from root entry zone through the IAM to the geniculate ganglion. Post-contrast T1 (#7) — normal facial nerve can enhance mildly at the geniculate ganglion; asymmetry is the key.
- **CPA mass:** Shift centre posteriorly and inferiorly — centre on the CPA cistern rather than the bony IAM. Extend coverage to lower medulla. The standard IAM slab centred on the porus acusticus will clip a CPA meningioma or epidermoid extending posteriorly into the cistern.

---

## 5. Alerts

| Check | Improve |
|---|---|
| **`t2_space_tra_iso_IAM` (#3)** — IAM centred in slab? Wrapped anatomy or signal falloff reaching the lesion? | 0% slice oversampling — wrap and edge signal decay land at slab edges. Confirm IAM/lesion sits well within the central safe zone. If near edge: extend slab or add 10–20% slice oversampling |
| **`t1_vibe_fs_cor_brain_C` (#5)** — contrast present? Confirm intravascular enhancement | If absent: check IV line, confirm injection |

---

## 6. Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-07-19 | — | Initial — 7 sequences (IAM targeted + basic brain) |
