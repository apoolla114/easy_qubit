# Parts reference (stashed from parts_list.md)

Everything that is **not** in the current order: optional / later purchases, lab- and Burke-supplied items, budget scenarios, design notes, checklist, and exclusions. The current order is in [parts_list.md](parts_list.md).

**Apparatus:** Ensemble NV **CW ODMR** · **December cash target:** ~**$500–550** (lab/Burke items excluded) · **P0 checkout ref.:** ~**$572** (team, Oct 2026, before **MB4** + **QLM-1125**). Full-program budget: branch **`budget-800-stretch`**.

**Diagram:** [diagrams/parts_diagram.md](diagrams/parts_diagram.md) · **Diagram (costs):** [diagrams/parts_diagram_cost.md](diagrams/parts_diagram_cost.md) · **Goals:** [goals.md](goals.md) · **Add-on cart (vs original team list):** [parts_list_additional_purchases.md](parts_list_additional_purchases.md)

**Legend:** **P0** = December assembly · **P1** = after bring-up · **P2** = March stretch · **Given/Lab** = no team cash

Prices are **list USD (Oct 2026)**; add **~10–15% + shipping**. Order through **course / 159A** when required.

---

## Laser assembly fasteners (not included)

All parts below are **imperial** (1/4″-20 and 8-32) and **mate correctly** on **MB4 + TR1 + LMR7 + CL5A + QLM-1125**. Thorlabs does **not** ship breadboard screws with **MB4**, **CL5A**, **TR1**, or **LMR7**.

| Joint | Parts | Fastener | Included with purchase? |
|-------|--------|----------|-------------------------|
| **Board → lens post** | **TR1** bottom ↔ **MB4** tapped hole | **1/4″-20 cap screw** from **under** the board up into the post (board is 1/2″ thick; **3/8″–1/2″** thread length is typical, e.g. Thorlabs **SH25S050**) | No — buy or borrow |
| **Post → lens mount** | **LMR7** base ↔ **TR1** top | **8-32** screw into post top: remove **TR1**’s removable 8-32 setscrew, seat **LMR7** on post, tighten with **8-32 cap screw** (~**1/2″** long) through **LMR7** base, **or** reuse the post setscrew if it engages the mount (5/64″ hex) | **Setscrew only** on **TR1**; **8-32 cap screw** usually **not** included with **LMR7** |
| **Lens in mount** | **CAX183** in **LMR7** | **SM7RR** retaining ring (torque with **SPW207** / **SPW801** or careful hand-tight) | **SM7RR** **included** with **LMR7** |
| **Board → QLM base** | **CL5A** ×2 ↔ **MB4** | **1/4″-20 cap screw** + **washer** (Thorlabs **W25S050**) through clamp into board hole — [CL5A](https://www.thorlabs.com/item/CL5A) docs | No |
| **QLM → laser module** | **VLM-520-74** in **QLM-1125** | Plastic clamp screws in QLM kit | **Yes** (Quarton) |
| **QLM base → board** | Ø4.5 mm holes in QLM base | **Does not** match **MB4** 1/4″-20 grid — use **CL5A**, not cap screws through QLM holes | N/A |

**Rough count for laser line only:** **2×** 1/4″-20 cap + washer (**CL5A**) + **1×** 1/4″-20 cap (**TR1**) + **1×** 8-32 cap or setscrew (**LMR7**–**TR1**) ≈ **4 screws + 2 washers**. If you add deferred sample posts (**TR1.5**, **TR3C**), budget **two more** 1/4″-20 caps from below **MB4** — see [below](#sample-holder-posts-tr15--tr3c-deferred).

**Tools:** 3/16″ hex (1/4″-20 cap), 5/64″ hex (8-32 on posts/mounts).

---

## Lens post: PH1 + CF125 (deferred)

**Not in the current Thorlabs cart.** The lens line is **LMR7 + TR1** screwed into **MB4** — cheaper and enough for a first mechanical build while the sample is a **low stack on the detector PCB** (no sample posts).

**Why add them later (~$19 list):**

| Part | Role |
|------|------|
| **[PH1](https://www.thorlabs.com/item/PH1)** post holder | Grips **TR1** and lets you **slide the post up/down** to match the filter stack optical center (~54 mm) and the **QLM-1125** beam (~49–55 mm). With **TR1** alone, lens center is only ~38 mm (1″ post + LMR7 height). |
| **[CF125](https://www.thorlabs.com/item/CF125)** clamping fork | Bolts **PH1** to **MB4** with a **slotted foot** so you can **slide the whole lens post sideways** — sets **~16 mm** working distance (CAX183 focus to diamond) and centers the lens under the laser without picking a new breadboard hole. |

**When to order:** After the **MB4** layout is wired; if the fixed **TR1** height cannot be aligned to the stack/laser, or focus requires sliding along the beam axis.

**Lab alternative:** Borrow **PH1 + CF125** (or any post holder + fork) from the optics lab for bring-up before buying.

---

## SM05 filter cage: LMR05 + SM05L10 + SM05RR (deferred)

**Not in the current Thorlabs cart.** P0 matches Mariani et al.: **RG630** and **5CGA-630** sit on the **BPW34** active area, **diamond** on top (~2 mm above the PD in their layout). No Thorlabs tube or rings — contact / gravity with careful handling (Kapton, light tape, or a small bezel — see [checklist](#pre-order-checklist)).

**Why we had SM05 in an earlier BOM:**

| Part | Role if ordered later |
|------|------------------------|
| **[LMR05](https://www.thorlabs.com/item/LMR05)** | SM05-threaded base; threads **SM05L10**; can bolt to **MB4** or sit on the PCB |
| **[SM05L10](https://www.thorlabs.com/item/SM05L10)** | Lens tube holds **both** Ø12.5 mm filters with retaining rings |
| **[SM05RR](https://www.thorlabs.com/item/SM05RR)** | Extra ring (tube often ships with one) for the second filter |

**When to order:** Filters **shift or scratch** in the bare stack; you want a fixed clear aperture and repeatable stack height; or advisor wants purchased Thorlabs retention for the filter pair.

**List cost if added:** ~**$40** (**LMR05** ~$18 + **SM05L10** ~$17 + **SM05RR** ~$5, Oct 2026 list). Install **SM05RR** with lab **SPW603** / **SPB05** or hand-tight — see optional row below.

---

## Sample holder posts: TR1.5 + TR3C (deferred)

**Not in the current Thorlabs cart.** P0 sample holder is a **low contact stack** on **BPW34** with **F5** breakout on **MB4** (standoffs). No optical posts for the sample line.

**Why we had posts in an earlier BOM:**

| Part | Role if ordered later |
|------|------------------------|
| **[TR1.5](https://www.thorlabs.com/item/TR1.5)** (1.5″ post) | Screws **LMR05** into **MB4** so the filter stack center sits ~**54 mm** above the board (1.5″ + LMR05 optical height) — matches **QLM-1125** beam height (~49–55 mm) without sliding the lens post. |
| **[TR3C](https://www.thorlabs.com/item/TR3C)** (90° construction post) | Holds the detector **PCB vertical** beside the stack; alternative to **standoffs** on **MB4**. |

**When to order:** If a **low stack** on the PCB cannot be illuminated/focused with **TR1 + LMR7** (even with **PH1 + CF125**), or you want the filter line at breadboard post height for side-by-side alignment with the laser post.

**List cost if added:** ~**$27** (**TR1.5** ~$6 + **TR3C** ~$21, Oct 2026 list).

---

## Optional / conditional / later purchases

| ID | Item | Qty | MPN | Vendor | Unit $ | Phase | When to buy | Link |
|----|------|-----|-----|--------|-------|-------|-------------|------|
| — | Post holder, L=1″ (lens) | 1 | PH1 | Thorlabs | 9 | P0 defer | See [above](#lens-post-ph1--cf125-deferred) | [PH1](https://www.thorlabs.com/item/PH1) |
| — | Clamping fork (lens) | 1 | CF125 | Thorlabs | 10 | P0 defer | See [above](#lens-post-ph1--cf125-deferred) | [CF125](https://www.thorlabs.com/item/CF125) |
| — | Optical post, L=1.5″ (filter stack) | 1 | TR1.5 | Thorlabs | 6 | P0 defer | See [sample holder posts](#sample-holder-posts-tr15--tr3c-deferred) | [TR1.5](https://www.thorlabs.com/item/TR1.5) |
| — | Construction post (detector) | 1 | TR3C | Thorlabs | 21 | P0 defer | See [sample holder posts](#sample-holder-posts-tr15--tr3c-deferred) | [TR3C](https://www.thorlabs.com/item/TR3C) |
| T7 | SM05 lens tube (filter stack) | 1 | SM05L10 | Thorlabs | 17 | P0 defer | See [SM05 filter cage](#sm05-filter-cage-lmr05--sm05l10--sm05rr-deferred) | [SM05L10](https://www.thorlabs.com/item/SM05L10) |
| T8 | SM05 retaining ring (extra) | 1 | SM05RR | Thorlabs | 5 | P0 defer | With **SM05L10** | [SM05RR](https://www.thorlabs.com/item/SM05RR) |
| T9 | Lens mount (filter stack base) | 1 | LMR05 | Thorlabs | 18 | P0 defer | With **SM05L10** | [LMR05](https://www.thorlabs.com/item/LMR05) |
|----|------|-----|-----|--------|--------|-------|-------------|------|
| T11 | Spanner wrench (SM05RR) | 1 | SPW603 | Thorlabs | 13 | P0 | Only if **T7–T9** ordered; else N/A | [SPW603](https://www.thorlabs.com/item/SPW603) |
| T12 | Kinematic mount | 1 | KM100 | Thorlabs | 64 | P1 | After bring-up | [KM100](https://www.thorlabs.com/item/KM100) |
| T13 | Hardware kit | 1 | HW-KIT2 | Thorlabs | 15 | P1 | If lab has no screws | [HW-KIT2](https://www.thorlabs.com/item/HW-KIT2) |
| M2 | 2nd MW amplifier | 1 | TQP3M9009 | Amazon | 4 | P1 | Recommended build; weak MW | [Team wishlist](https://www.amazon.com/hz/wishlist/ls/1HXJ4O5ZYQING?ref_=wl_share) |
| M3 | RF attenuator | 1 | Fixed SMA (10–20 dB) | Amazon | 16 | P1 | Only if MW power too high | — |
| M8 | MW switch | 1 | HMC284 SPDT module | Amazon | 15–22 | P1 | Pulsed MW | [Example listing](https://www.amazon.com/HMC284-Switch-Reflective-Isolation-Control/dp/B0DZHNS5HY) |
| F6 | TIA passives | 1 | R/C per OPA381 datasheet | DigiKey | 5 | P0 | If lab cannot supply | [OPA381 datasheet](https://www.ti.com/product/OPA381) |
| M9 | 50 Ω SMA termination | 1 | 132360 or equiv. | DigiKey | 3 | P1 | Optional | [132360 SMA termination](https://www.digikey.com/en/products/filter/rf-termination/742?s=132360) |

**MW chain:** synthesizer → amplifier → *(optional attenuator)* → SMA coax → **Burke antenna (SMA female)**.

---

## Supplied (no purchase)

### BurkeLab

| ID | Item | Qty | Phase | Notes |
|----|------|-----|-------|-------|
| M6 | MW antenna assembly | 1 | P0 | PCB + **SMA female** + wire; team connects with SMA coax |
| S1 | NV diamond sample | 1 | P0 | On contact filter stack (top face lit) |

### EECS lab / team

| ID | Item | Qty | Phase | Notes |
|----|------|-----|-------|-------|
| C1 | Microcontroller | 1 | P0 | Uno or Nucleo — [wiring_guide](diagrams/wiring_guide.md) |
| C2 | USB A–B cable | 1 | P0 | |
| H1 | 1/4″-20 cap screws + setscrews | ~4–5 | P0 | Cap screws for 2× **CL5A** (+ **CF125** if added); cap/setscrew for **TR1** into **MB4** (+ **TR1.5** / **TR3C** if deferred posts added) |
| — | Custom detector PCB layout | 0 | P0 | Optional; P0 uses purchased **F5** Stargazer breakout + **F3**/**F4** |
| F7 | Permanent magnet | 1 | P0 | Zeeman split |
| P1 | Bench power supplies | — | P0 | MW, laser, CTL |
| P2 | Oscilloscope | 0 | — | Debug only |

---

## Budget summary

| Scenario | What’s included | Est. team spend |
|----------|-----------------|-----------------|
| **A — December minimum** | P0; **1×** amp; Thorlabs P0 cart | **~$318** list (+ tax/ship → **~$350–370**) |
| **B — December recommended** | P0; **2×** amp (+$4); full P0 cart | **~$322** list (+ tax/ship) |
| **C — P1 add-ons** | B + switch, KM100, extra amp, att. | See P1 rows; totals in branch `budget-800-stretch` |
| **D — ~$300 cash** | Core RF + optics + **one** filter + **minimal** Thorlabs; **heavy lab loan** | **~$250–320** out of pocket |

**Not in budget (defer):** RF isolator ($100+), IVC102 integrator, TQP7M9103 driver.

### Scenario D — ~$300 out-of-pocket (what has to give)

The **current [parts_list.md](parts_list.md) P0 cart** is **~$318 list** (laser-line Thorlabs **~$107**, both filters, Amazon RF/laser/**M4** coax/**F5** breakout, DigiKey, glasses). Tax/shipping adds on top unless the course absorbs shipping.

**To cut below ~$300 list**, defer performance items:

| Defer from P0 cart | Saves (list) |
|--------------------|--------------|
| **F2** Newport **5CGA-630** (RG630 only) | ~38 |
| **O3** safety glasses (lab loan) | ~23 |
| **O2** **CAX183** (collimated module only; harder focus) | ~16 |
| **T7–T9** SM05 cage (already deferred — bare stack) | — |

*Scenario D is a planning sketch; use **parts_list.md** totals for the live order.*

| Must come from **EECS lab / advisor** (not in $300) | |
|-----------------------------------------------------|--|
| Breadboard + **3×** post / holder / fork (replaces MB4, PH2, CF125, TR4) | ~$130 value |
| Laser clamp (replaces **QLM-1125**) — any clamp that holds **Ø6.5 mm** | ~$32 value |
| LMR7 + lens post line | ~$49 value |
| Magnet, passives, PSU, scope | |
| Safety glasses if not purchased | ~$23 value |
| Burke: diamond + wire | |

| Defer past $300 build | Risk |
|-----------------------|------|
| **5CGA-630** (second filter) | More green leak; noisier PL |
| **2nd TQP3M9009** | Weaker MW → harder ODMR |
| **QLM-1125, KM100, MW switch** | Harder alignment; no pulsed MW |
| **SM05 cage (T7–T9)** | Bare filter stack may shift; add ~$40 if needed |

**Realistic December goal at $300:** assembled **CW** path, **PL on ADC**, automated **frequency sweep**; ODMR dip is **best effort** (alignment + MW coupling), not guaranteed.

---

## Design choices

1. **Thorlabs** mounts on a purchased **MB4** — not 3D-printed; MW bench uses SMA only.
2. **Laser:** Quarton **QLM-1125** on **MB4** (2× **CL5A**). **CAX183** in [LMR7](https://www.thorlabs.com/item/LMR7) on **TR1** screwed into **MB4**. Optional **PH1 + CF125** on the lens line — [deferred](#lens-post-ph1--cf125-deferred).
3. **Sample (Mariani-style):** [F1](https://www.edmundoptics.com/p/schott-rg630-125mm-dia-1mm-thick-colored-glass-longpass-filter/44313/) + [F2](https://www.newport.com/p/5CGA-630) + diamond on **BPW34** (**F3**); **F5** Stargazer 8-VSSOP breakout on **MB4** under the PD with **OPA381** (**F4**) + **F6** passives. Optional **SM05** cage — [deferred](#sm05-filter-cage-lmr05--sm05l10--sm05rr-deferred); optional posts **TR1.5** + **TR3C** — [deferred](#sample-holder-posts-tr15--tr3c-deferred).
4. **December:** 1× amp if tight; 2× recommended.
5. **CTL on-chip ADC** only; no scope purchase.

---

## Order waves

**Wave 1 (P0):** everything in [parts_list.md](parts_list.md); Burke **M6** antenna + **S1** diamond.

**Wave 2 (P1):** M8, M9, T12, extra M2, T13.

**Wave 3 (P2):** Loop antenna PCB, integrator — [stretch diagram](diagrams/parts_diagram_arduino_paper.md).

---

## Pre-order checklist

- [x] **Quarton OD** = Ø6.5 mm (datasheet) → **QLM-1125** (Ø6–12.5 mm); VC3C minimum is Ø6.6 mm
- [x] **CAX183** (Ø6.28 mm, 1.09 mm CT) fits **LMR7** (Ø7 mm, also secures Ø6.35 mm; ≤4.0 mm thick)
- [x] **QLM-1125** base: Ø35 mm, 6 mm thick, Ø4.5 mm holes (not 1/4″-20) → 2× **CL5A** clamps
- [x] **QLM-1125** beam height ~49–55 mm (Quarton photos) → P0 uses **low stack on PCB**; add **TR1.5** or **PH1 + CF125** if beam cannot hit diamond
- [ ] Focus/align laser (**TR1** ~38 mm lens center) onto low stack; add **PH1 + CF125** and/or **TR1.5** if needed — [deferred sections](#lens-post-ph1--cf125-deferred)
- [ ] Quarton housing is at **+V** — insulate (e.g. Kapton) where it touches metal
- [ ] **SM7RR** ring (LMR7) uses **SPW207** / **SPW801**, not **SPW603** — tighten by hand or borrow
- [ ] **F5:** solder **OPA381AIDGKR** (8-VSSOP, 0.65 mm) on **MSOP/VSSOP** pad side of [Stargazer 492](https://www.amazon.com/gp/product/B07R5QR9P3); **BPW34** above stack — wire or short SMT bridge to TIA input
- [ ] **CTL** SPI levels vs [ADF4351](https://www.analog.com/en/products/adf4351.html) module
- [ ] **M4** coax length/plugs: synth → amp → Burke **SMA female** (male–male **RG316**)
- [ ] Diamond retention on **filter stack** (contact mount: Kapton ring, light tape, or small bezel — Mariani uses gravity on stacked filters)

---

## Explicitly excluded

| Item | Reason |
|------|--------|
| VCO + ramp (*Little bits*) | ADF4351 + CTL |
| Epifluorescence microscope | Contact filter stack on PD (Mariani) |
| 3D-printed mounts | Thorlabs Tier 1 |
| VC3C V-clamp (was **T5**) | Min Ø6.6 mm; Quarton is Ø6.5 mm → **QLM-1125** (**O4**) |
| LMR05S lens mount | Ø1/2″ optics; CAX183 is Ø6.28 mm → **LMR7** |
| External ADC | CTL ADC |
| IVC102 (base build) | TIA PoC |
| PCB-mount SMA (**M5**) | On Burke antenna |
| Custom wire-launch PCB (JLC) | Burke **M6** antenna |
| RF attenuator (**M3**) | Defer unless power too high |

---

## References

- Zhang et al., *Am. J. Phys.* **86**, 225 (2018) — [doi:10.1119/1.5023389](https://doi.org/10.1119/1.5023389)
- Mariani et al., *AIP Advances* **12**, 065321 (2022) — [doi:10.1063/5.0089161](https://doi.org/10.1063/5.0089161)
