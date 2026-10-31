# Project goals

**Apparatus:** Ensemble NV **continuous-wave optically detected magnetic resonance (CW ODMR)** — prove the BurkeLab diamond and our MW/optical/readout chain on the **December PoC** budget (see [parts_list.md](parts_list.md)). Full-program budget notes: git branch **`budget-800-stretch`**.

**Diagram:** [diagrams/parts_diagram.md](diagrams/parts_diagram.md) (conceptual + physical) · **Parts:** [parts_list.md](parts_list.md)

---

## Design rationale (vs *Little bits of diamond*)

We started from Zhang et al. (*Am. J. Phys.* 86, 225 (2018)) and changed four areas:

| Topic | Original (*Little bits*) | Our design |
|-------|--------------------------|------------|
| **Microwave** | VCO + ramp (manual / FG sweep) | **ADF4351** + **microcontroller** — automated SPI frequency sweeps |
| **Laser** | 532 nm lab laser + microscope | **520 nm Quarton module** (driver + collimation) + **CAX183** focus lens |
| **Detection** | Epifluorescence + LP/SP + PDA36A + scope/DMM | **Diamond on RG630 + 5CGA-630 + BPW34 + OPA381 TIA** → **CTL ADC** (scope optional) |
| **MW at sample** | ~5 mm wire on **custom PCB** + SMA | **Burke antenna** (PCB + **SMA female**); **synth → amp → (att) → coax → antenna** |

Physics goal unchanged: **PL vs MW frequency** near ~2.87 GHz (with **magnet** for splittings).

---

## Timeline

### December — basic apparatus (~$500 spend target)

**Deliverables**

- [ ] Thorlabs optomechanics on **MB4**: laser clamp, **CAX183** mount, **SM05** filter stack + detector post  
- [ ] Optical path: laser → focus → diamond → filters → PD → TIA → **CTL**  
- [ ] MW path: CTL → ADF4351 → amp(s) → *(att if needed)* → SMA coax → **Burke antenna**  
- [ ] Firmware: set ADF4351 frequency; log TIA voltage vs frequency  
- [ ] **PoC:** stable PL; **best-effort CW ODMR dip** (contrast not guaranteed on first alignment)

**Success criteria (minimum)**

- Visible / digitized **NV photoluminescence** with filters in place  
- Reproducible **frequency sweep** without manual tuning knob  
- Documented **geometry** (wire–diamond distance, magnet placement)

**Fallback (Burke / course)**

- **Assembly complete** with optical and MW paths wired and characterized separately  
- Qualitative MW effect on PL (even if sweep is noisy)

### January–March — extensions

Build on December hardware; order depends on what failed in PoC.

| Priority | Extension | Purpose |
|----------|-----------|---------|
| 1 | Alignment + software (averaging, background subtract) | Improve ODMR visibility without new parts |
| 2 | Second amp / attenuator tuning | Stronger or safer **B₁** at wire |
| 3 | **MW switch** + pulsed firmware | Pulsed MW ODMR; path toward Rabi / T₁ (stretch) |
| 4 | Laser gating (if laser allows) | Sync with MW pulses |
| 5 | Loop antenna PCB (Mariani-style) | Repeatable MW coupling vs wire-only |
| 6 | Integrator readout (IVC102) | Closer to Mariani et al.; likely beyond budget unless lab stocks parts |

**March stretch (not required for PoC)**

- Pulsed sequences, better contrast, coherence-style experiments  
- Full [parts_diagram_arduino_paper.md](parts_diagram_arduino_paper.md) apparatus  

**Out of scope for this budget / timeline**

- Single-NV confocal microscopy  
- Full isolator + driver-amp chain as in Mariani Table I  

---

## What the apparatus can do

**December (CW PoC)**

- Confirm **ensemble NV** PL through the compact stack  
- **CW ODMR:** fluorescence vs **automated** MW frequency sweep (~2.7–3.1 GHz)  
- **Qualitative Zeeman:** shift features with **permanent magnet**  
- USB **data logging** for reports  

**With March extensions**

- **Pulsed MW** spectroscopy (if switch added)  
- Better SNR / contrast; possible stepping stone to pulsed ODMR normalization  
- Still **not** single-spin or full quantum control without major optics/control upgrades  

---

## Open questions (BurkeLab)

- Intended **wire length and shape** (straight ~5 mm vs coil)?  
- Recommended **distance** from wire to diamond / PL collection region?  
- Existing **PCB footprint** or mechanical drawing we should match?  
- Sample orientation (**[111]** alignment) with provided magnet?

---

## Budget summary

| Phase | Target spend | Notes |
|-------|--------------|--------|
| December core | ≤ ~500 | See [parts_list.md](parts_list.md); lab/Burke reduce cash |
