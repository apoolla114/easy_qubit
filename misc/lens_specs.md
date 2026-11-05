# Optical component specifications

Every lens, filter, and the photodiode in the build, plus the lens from the Mariani reference design for comparison. Parts list: [parts_list.md](parts_list.md) · Layout: [diagrams/parts_diagram.md](diagrams/parts_diagram.md)

**Optical path:** Quarton VLM-520-74 (laser diode → built-in collimating lens) → **CAX183** focusing lens (in **LMR7** on **TR1**) → diamond → **RG630** → **5CGA-630** → **BPW34S** photodiode.

| Part | Role | In our build? |
|------|------|---------------|
| Quarton built-in lens | Collimates the 520 nm diode inside the module | Yes (comes with **O1**) |
| [CAX183](https://www.thorlabs.com/item/CAX183) | Focuses the collimated beam onto the diamond | Yes (**O2**) |
| [CAY033](https://www.thorlabs.com/item/CAY033) | Collimator L1 in Mariani et al. (bare PLT3 510 diode) | No — reference only |
| [SCHOTT RG630, Edmund 16-420](https://www.edmundoptics.com/p/schott-rg630-125mm-dia-1mm-thick-colored-glass-longpass-filter/44313/) | Absorptive long-pass: blocks 520 nm pump, passes NV PL | Yes (**F1**) |
| [Newport 5CGA-630](https://www.newport.com/p/5CGA-630) | Interference (reflective) long-pass: blocks 520 nm pump, passes NV PL | Yes (**F2**) |
| [ams OSRAM BPW 34 S](https://ams-osram.com/products/photodetectors/photodiodes/osram-dil-smt-bpw-34-s) | Detects NV PL (600–800 nm) | Yes (**F3**) |

**Detector stack (Mariani-style):** diamond on **RG630** (1.0 mm) on **5CGA-630** (1.1 mm) on **BPW34S**, which puts the diamond ≈ 2.1 mm above the photodiode.

---

## 1. Quarton VLM-520-74 LPA built-in collimating lens

Integrated in the laser module; not removable or adjustable. Quarton publishes beam specs, not lens prescriptions — **focal length, NA, and coating are not published**.

Source: [VLM-520-74 series datasheet](https://media.ic-find.com/datasheets/af28896ff085fc418b65c4188570139d.pdf)

| Spec | Value |
|------|-------|
| Lens type | Aspherical **glass** collimating lens |
| Output aperture | **Ø4.3 mm** |
| Beam shape | Ellipse |
| Beam divergence (half angle) | **< 0.6 mrad** |
| Spot size at 10 m | < 7 mm |
| Beam alignment (pointing vs housing axis) | < 3° |
| Wavelength | 505–530 nm (520 nm nominal) |
| Output power (LPA) | < 4 mW, Class IIIa |
| Operating temp. (spot size spec held) | −20 to +60 °C |
| Storage temp. | −40 to +85 °C |

**Module context:** Ø6.5 mm × 26 mm bronze housing, 2.8 g, 3–6 VDC, < 200 mA, onboard APC driver. **Housing is at VDD (+)** — insulate it from metal mounts.

**Notes for alignment**
- The < 3° beam alignment spec means the beam can exit up to ~3° off the housing axis, which walks the beam ~1 mm sideways per ~20 mm of travel. Since the CAX183 aperture is only Ø4.3 mm, check that the beam is actually centered on the lens rather than trusting the mount.
- Because the beam is elliptical, the focused spot will be elliptical too.

---

## 2. Thorlabs CAX183 — focusing lens (O2)

Molded plastic plano-convex asphere (Philips design), uncoated. It was designed as a **diode-laser collimator**; we use it in reverse, focusing a collimated beam.

Sources: [Thorlabs CAX183](https://www.thorlabs.com/item/CAX183) · [Thorlabs plastic aspheres specs](https://www.thorlabs.us/NewGroupPage9_PF.cfm?Category_ID=141&Guide=10&ObjectGroup_ID=16) · [Manufacturer datasheet (PDF)](https://www.tme.com/Document/5d9686e041937ae0930dbce682295f35/CAX183.pdf)

| Spec | 670 nm (design) | 785 nm |
|------|-----------------|--------|
| Effective focal length | **18.15 mm** | 18.33 mm |
| Back focal length (with 0.25 mm BK7 window) | 17.51 mm | 17.69 mm |
| Free working distance | **16.30 mm** | 16.48 mm |

| Spec | Value |
|------|-------|
| Numerical aperture | **0.12** |
| Clear aperture | **Ø4.3 mm** |
| Outer diameter | **Ø6.28 mm** |
| Center thickness | 1.09 mm |
| Surfaces | Mono-aspheric (one aspheric surface, one flat) |
| Material | Polycarbonate |
| AR coating | None (≈ 90% transmission) — AR-coated version is [CAX183-A](https://www.thorlabs.com/item/CAX183-A) (400–700 nm, $35) |
| Laser window correction | 0.25 mm N-BK7, 0.55 mm from source |
| Wavefront error, RMS (at design λ) | 0.030λ on axis · 0.035λ total |
| Optical tolerance | 0.1 mm |
| Field radius | 0.3 mm |
| Surface quality | 80-50 scratch-dig |
| Operating temp. | −10 to 75 °C |
| Storage temp. | −25 to 100 °C |
| Price (list) | $15.64 |

**Mount:** [LMR7](https://www.thorlabs.com/item/LMR7) (Ø7 mm bore, also secures Ø6.35 mm, ≤ 4.0 mm thick) with the included **SM7RR** retaining ring. Optical center ≈ 38 mm above **MB4** on **TR1**.

### Behavior at 520 nm (estimates, not datasheet values)

Specs above are at 670/785 nm. Polycarbonate's refractive index is higher at 520 nm (≈ 1.593 vs ≈ 1.579 at 670 nm), so the lens is slightly stronger in green:

| Quantity | Estimate at 520 nm | How |
|----------|--------------------|-----|
| Focal length | ≈ **17.7 mm** | \( f \propto 1/(n-1) \): 18.15 × 0.579 / 0.593 |
| Working distance (flat face → focus) | ≈ **15.9 mm** | 16.30 mm shortened by the same ~0.4 mm |
| Effective NA with Quarton beam | ≈ 0.12 | Quarton Ø4.3 mm aperture ≈ CAX183 Ø4.3 mm clear aperture |
| Focused spot diameter | **~5–20 µm** | Upper bound from divergence: \( 2 f \theta \approx 2 \times 17.7\ \text{mm} \times 0.6\ \text{mrad} \approx 21\ \mu\text{m} \); lower bound near the diffraction limit for a ~2–4 mm beam |

Practical consequences:
- **Focus at ~16 mm, not 18 mm**, from the lens's flat face. The [PH1 + CF125](parts_list_reference.md#lens-post-ph1--cf125-deferred) slide exists for this adjustment.
- The Quarton beam roughly fills the lens's clear aperture, so there's little margin. Center the beam on the lens or the edges will clip.
- **Orientation:** put the convex (aspheric) side toward the laser and the flat side toward the diamond, which reverses its collimator use.
- The lens is corrected for a 0.25 mm glass window on the focus side. We have no window there, which adds a little spherical aberration, but that is negligible at NA 0.12.
- Plastic lens: the datasheet warns that **mechanical lock-mounting can distort it**. Tighten the SM7RR ring only finger-snug.

---

## 3. Thorlabs CAY033 — Mariani reference collimator (not purchased)

In Mariani et al. (2022), this lens collimated the bare PLT3 510 diode before the CAX183. We don't need it because the Quarton module has its own collimating lens. It's listed here only to compare with the paper ([diagrams/parts_diagram_arduino_paper.md](diagrams/parts_diagram_arduino_paper.md)).

Source: [Manufacturer datasheet (PDF)](https://static.chipdip.ru/lib/003/DOC036003390.pdf)

| Spec | 670 nm | 785 nm (design) |
|------|--------|-----------------|
| Effective focal length | 3.30 mm | 3.32 mm |
| Back focal length (with 0.25 mm BK7 window) | 2.08 mm | 2.10 mm |
| Free working distance | 1.98 mm | 2.00 mm |

| Spec | Value |
|------|-------|
| Numerical aperture | 0.40 |
| Clear aperture | Ø2.7 mm |
| Outer diameter | Ø7.40 mm |
| Center thickness | 3.05 mm |
| Surfaces | Bi-aspheric |
| Material | Acrylic (PMMA) |
| Coating | AR @ 785 nm (≈ 95% transmission at 785 nm) |
| Wavefront error, RMS max | 0.040λ on axis · 0.065λ total |
| Operating / storage temp. | 5 to 65 °C / −25 to 70 °C |

---

## Lens side-by-side

| | Quarton built-in | CAX183 | CAY033 (ref.) |
|---|---|---|---|
| Role | Collimate | Focus | Collimate |
| Material | Glass | Polycarbonate | Acrylic |
| Focal length | Not published | 18.15 mm (≈ 17.7 mm @ 520 nm) | 3.32 mm |
| NA | Not published | 0.12 | 0.40 |
| Aperture | Ø4.3 mm (output) | Ø4.3 mm (clear) | Ø2.7 mm (clear) |
| Coating | Not published | None | AR 785 nm |
| Output | < 0.6 mrad half-angle, elliptical | ~5–20 µm spot (est.) | — |

---

## 4. SCHOTT RG630 colored-glass long-pass — Edmund 16-420 (F1)

Absorptive filter: the glass itself absorbs short wavelengths, so blocking does not depend on the angle of the incoming light.

Sources: [Edmund 16-420](https://www.edmundoptics.com/p/schott-rg630-125mm-dia-1mm-thick-colored-glass-longpass-filter/44313/) · [Drawing (PDF)](https://www.edmundoptics.eu/ViewDocument/prnt_16420.pdf) · [1 mm transmittance curve (PDF)](https://www.edmundoptics.eu/ViewDocument/curv_16420.pdf) · [SCHOTT RG630 glass datasheet (PDF)](https://www.edmundoptics.ca/ViewDocument/schott-rg630-longpass-datasheet-en.pdf)

| Spec | Value |
|------|-------|
| Diameter | **Ø12.50 ± 0.2 mm** |
| Thickness | **1.00 ± 0.1 mm** |
| Cut-on (50% internal transmittance) | **630 ± 6 nm** (SCHOTT spec at 3 mm reference thickness) |
| Stopband limit (internal transmittance 10⁻⁵) | 540 nm (at 3 mm) |
| Passband limit (internal transmittance 0.94) | 710 nm (at 3 mm) |
| Reflection factor \(P_d\) | 0.92 (two-surface reflection loss ≈ 8%; external T = 0.92 × internal T) |
| Refractive index \(n_d\) | 1.52 |
| Coating | Uncoated |
| Surface quality | 60-40 scratch-dig |
| Parallelism | ≤ 3 arcmin |
| Cut-on temperature coefficient | 0.14 nm/K |
| Density | 2.65 g/cm³ |
| Transformation temp. | 527 °C |
| Price (list) | $37 |

**What 1 mm thickness means:** SCHOTT guarantees the edge values at **3 mm**, but ours is **1 mm**. Internal transmittance scales as \( \tau_{1\,\text{mm}} = \tau_{3\,\text{mm}}^{1/3} \), so the following are estimates, not datasheet values:
- At 540 nm, \( (10^{-5})^{1/3} \approx 0.02 \), or about **OD 1.7**. At 520 nm it blocks more strongly than that, but this filter alone is **not enough** to block the pump. That's why the stack includes the 5CGA-630.
- The 50% point moves a little shorter than 630 nm, and the edge is less steep. Use the 1 mm curve linked above.

---

## 5. Newport 5CGA-630 colored-glass-alternative long-pass (F2)

All-dielectric interference filter. Despite the name, it is **not** colored glass. It reflects the blocked band, so 520 nm light bounces back up toward the diamond instead of being absorbed. Its edge is much steeper than the RG630's.

Sources: [Newport 5CGA-630](https://www.newport.com/p/5CGA-630) · [Newport CGA catalog (PDF)](https://api.p1.mks.com/medias/sys_master/resources/h02/ha2/9954229977118/CAT-11091%20Colored%20Glass%20Alternatve%20Filters%20Catalog/CAT-11091-Colored-Glass-Alternatve-Filters-Catalog.pdf)

| Spec | Value |
|------|-------|
| Diameter | **Ø12.7 mm** (0.500 ± 0.005″) |
| Thickness | **1.1 ± 0.1 mm** |
| Clear aperture | ≥ 90% of diameter (film to the edge), > 11.43 mm |
| Cut-on (50% transmittance, normal incidence) | **630 ± 6 nm** |
| 90% transmittance reached by | ≤ 650 nm |
| OD 5 blocking from | ≥ 595 nm down to **200 nm** |
| Pass-band transmittance | ≥ 90% typical, out to 2500 nm |
| Effective index \(n_e\) | 1.74 |
| Surface quality | 80-50 scratch-dig |
| Laser damage threshold | ≥ 1 J/cm² (532 nm, 10 ns, 20 Hz) |
| Operating temp. | −100 to 400 °C |
| Cleaning | Acetone or IPA on lens tissue, non-abrasive |
| Price (list) | $38 |

**Angle sensitivity (estimate):** For an interference filter, the cut-on moves to shorter wavelengths as the angle of incidence \(\theta\) increases: \( \lambda(\theta) \approx \lambda_0 \sqrt{1 - (\sin\theta / n_e)^2} \). With \(\lambda_0\) = 630 nm and \(n_e\) = 1.74:

| Angle of incidence | Cut-on (est.) |
|--------------------|---------------|
| 0° | 630 nm |
| 20° | ≈ 618 nm |
| 30° | ≈ 603 nm |
| 45° | ≈ 576 nm |
| 60° | ≈ 546 nm |

The diamond emits PL in every direction, and scattered pump light reaches the filter at steep angles. Above ~60°, this filter's 520 nm blocking falls off. The RG630 is absorptive, so it doesn't have this problem. That's why the two filters are stacked.

---

## Filter side-by-side

| | RG630 (F1) | 5CGA-630 (F2) |
|---|---|---|
| Type | Absorptive colored glass | Dielectric interference (reflective) |
| Diameter × thickness | Ø12.5 × 1.0 mm | Ø12.7 × 1.1 mm |
| Cut-on (50%) | 630 ± 6 nm (3 mm ref.) | 630 ± 6 nm |
| Blocking at 520 nm | ≳ OD 1.7 (est., 1 mm) | ≥ OD 5 (normal incidence) |
| Edge steepness | Gradual | Steep (~595 → 650 nm, OD 5 → 90% T) |
| Angle dependence | None | Cut-on shifts blue at high angles |
| Pass-band T | ≈ 0.92 × internal | ≥ 90% |

---

## 6. ams OSRAM BPW 34 S photodiode — BPW-34-S-Z (F3)

Silicon PIN photodiode in a surface-mount DIL plastic package. We run it in **photovoltaic mode (0 V bias)** into the **OPA381** TIA.

Sources: [ams OSRAM product page](https://ams-osram.com/products/photodetectors/photodiodes/osram-dil-smt-bpw-34-s) · [Datasheet (PDF)](https://look.ams-osram.com/m/1f206a499ac1f0b2/original/BPW-34-S.pdf) · [DigiKey BPW-34-S-Z](https://www.digikey.com/en/products/detail/ams-osram-ag/BPW-34-S-Z/1893856)

**Characteristics** (T_A = 25 °C, typical unless noted)

| Spec | Value |
|------|-------|
| Radiant sensitive area | **7.02 mm²** (**2.65 × 2.65 mm**) |
| Peak sensitivity wavelength | **920 nm** (current datasheet; older revisions list 850 nm) |
| Spectral range (10% of peak) | 420–1120 nm (older revisions: 400–1100 nm) |
| Spectral sensitivity of chip @ 850 nm | **0.62 A/W** |
| Quantum yield @ 850 nm | 0.90 electrons/photon |
| Half angle | ± 60° |
| Dark current (V_R = 10 V) | 2 nA typ, ≤ 30 nA max |
| Capacitance (V_R = 0 V, 1 MHz) | **72 pF** |
| Rise / fall time (V_R = 5 V, 50 Ω, 850 nm) | 20 ns / 20 ns |
| Photocurrent (1000 lx Std. Light A, V_R = 5 V) | 80 µA typ (**-Z** bin: ≥ 55 µA) |
| Short-circuit current (1000 lx, 0 V) | 80 µA |
| Open-circuit voltage (1000 lx) | 365 mV typ, ≥ 300 mV |
| Forward voltage (I_F = 100 mA) | 1.3 V |
| NEP (V_R = 10 V, 850 nm) | 0.041 pW/√Hz |
| Specific detectivity D* | 6.5 × 10¹² cm·√Hz/W |
| Temp. coefficient of I_SC | +0.18 %/K |
| Temp. coefficient of V_O | −2.6 mV/K |

**Maximum ratings**

| Spec | Value |
|------|-------|
| Reverse voltage | 32 V |
| Power dissipation | 150 mW |
| Operating / storage temp. | −40 to 100 °C |
| ESD (HBM) | 2 kV |
| Package (L × W × H) | ≈ 6.45 × 3.85 × 1.15 mm, reflow-solderable |

**Notes for our design**
- **Fit:** The 2.65 mm square active area is fully covered by both Ø12.5 mm filters, so filter alignment over the chip isn't critical.
- **Responsivity at our wavelengths (estimates from the relative-sensitivity curve, not datasheet values):** ≈ 0.45–0.5 A/W across the NV PL band (650–800 nm), and ≈ 0.25–0.3 A/W at 520 nm. Silicon responds well to green, so any pump light that leaks through the filters adds directly to the signal.
- **TIA stability:** At 0 V bias, the 72 pF junction capacitance sits on the OPA381 input. Size the feedback capacitor using the [OPA381 datasheet](https://www.ti.com/product/OPA381) photodiode-capacitance guidance.
- **Dark current:** It's specified at 10 V reverse bias. In photovoltaic mode (0 V) it is much lower, so dark current isn't a concern for us.
