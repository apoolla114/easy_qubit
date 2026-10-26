# Additional purchases (base apparatus only)

Parts **not** on your existing team list. These **Thorlabs** items **replace the three 3D-printed mounts** ([physical layout](diagrams/parts_diagram.md)). **CAX183** stays on your list—do not duplicate here.

**Prices:** Thorlabs USD **list** (Oct 2026); tax/shipping extra.

---

## Recommended — **1-post cart (~$150** list)

One vertical post holds **CAX183** ([LMR05S](https://www.thorlabs.com/item/LMR05S)) and the **filter stack** ([LMR05](https://www.thorlabs.com/item/LMR05) + [SM05L10](https://www.thorlabs.com/item/SM05L10)) at different heights on the same axis. **Quarton** sits on the **MB4** with a **lab clamp** (no **VC3C**). **Detector / MW PCBs** screw to **MB4** with standoffs. **No spanner in cart**—borrow **SPW603** / **SPB05** or tighten **SM05RR** carefully by hand.

| Qty | Item | P/N | Unit (USD) | Line (USD) | Link |
|-----|------|-----|------------|------------|------|
| 1 | Breadboard 4″ × 6″ | **MB4** | $52.34 | $52.34 | [MB4](https://www.thorlabs.com/item/MB4) |
| 1 | Post holder, L = 2″ | **PH2** | $9.58 | $9.58 | [PH2](https://www.thorlabs.com/item/PH2) |
| 1 | Clamping fork | **CF125** | $10.36 | $10.36 | [CF125](https://www.thorlabs.com/item/CF125) |
| 1 | Optical post, L = 4″ | **TR4** | $7.14 | $7.14 | [TR4](https://www.thorlabs.com/item/TR4) |
| 1 | Lens mount (CAX183) | **LMR05S** | $30.63 | $30.63 | [LMR05S](https://www.thorlabs.com/item/LMR05S) |
| 1 | Lens mount (filter base) | **LMR05** | $18.18 | $18.18 | [LMR05](https://www.thorlabs.com/item/LMR05) |
| 1 | SM05 lens tube (both filters) | **SM05L10** | $17.47 | $17.47 | [SM05L10](https://www.thorlabs.com/item/SM05L10) |
| 1 | Extra SM05 retaining ring | **SM05RR** | $4.63 | $4.63 | [SM05RR](https://www.thorlabs.com/item/SM05RR) |

| | **1-post subtotal** | | | **$150.33** | |

Use **PH2** sliding to set lens vs filter height; **TR4** gives room for two **SM05** mounts on one line.

---

## Alternate — **2-post cart (~$176** list)

If laser steering and the filter stack need **independent** height (side-by-side on **MB4**), add a second post line—still **no VC3C**, **no spanner**.

| Qty | Item | P/N | Unit (USD) | Line (USD) | Link |
|-----|------|-----|------------|------------|------|
| 1 | (same **MB4**, **LMR05S**, **LMR05**, **SM05L10**, **SM05RR** as 1-post cart) | | | $123.25 | |
| 2 | Post holder **PH2** | **PH2** | $9.58 | $19.16 | [PH2](https://www.thorlabs.com/item/PH2) |
| 2 | Clamping fork **CF125** | **CF125** | $10.36 | $20.72 | [CF125](https://www.thorlabs.com/item/CF125) |
| 2 | Optical post, L = 2″ | **TR2** | $6.31 | $12.62 | [TR2](https://www.thorlabs.com/item/TR2) |
| | **2-post subtotal** | | | **$175.75** | |

About **$25** more than the 1-post cart (second post line instead of one **TR4**).

---

## Lowest cash — **SM05 block only (~$72** list)

If the lab loans **MB4** (or any 6″×6″ breadboard) **plus** one post/holder/fork set **and** a laser clamp:

| Qty | Item | P/N | Line (USD) | Link |
|-----|------|-----|------------|------|
| 1 | LMR05S | | $30.63 | [LMR05S](https://www.thorlabs.com/item/LMR05S) |
| 1 | LMR05 | | $18.18 | [LMR05](https://www.thorlabs.com/item/LMR05) |
| 1 | SM05L10 | | $17.47 | [SM05L10](https://www.thorlabs.com/item/SM05L10) |
| 1 | SM05RR | | $4.63 | [SM05RR](https://www.thorlabs.com/item/SM05RR) |
| | **Subtotal** | | **$70.91** | |

Align with advisor: “purchased Thorlabs” may mean this block + documented lab loan for the plate and posts.

---

## Borrow from EECS lab (instead of buying)

| Item | List $ | Notes |
|------|--------|--------|
| **VC3C** laser V-clamp | $48.31 | Any **cylindrical clamp** / post ring for Quarton OD |
| **SPB05** or **SPW603** | $31.14 / $30.54 | Filter install; lab optics kit usually has one |
| **MB4 + PH2 + CF125 + TR\*** | up to ~$79 | See **SM05-only** tier above |
| **TR3C** | $14.00 | Optional: vertical PCB beside stack—else standoffs on **MB4** |

---

## Layout (1-post recommended)

```text
MB4
├── Lab clamp + Quarton (on board) ──beam──►  TR4/PH2: LMR05S→CAX183 ──► LMR05→SM05L10→filters→diamond
└── Detector PCB + wire-launch on MB4 (standoffs)
```

## Layout (2-post alternate)

```text
MB4
├── Post A: lab clamp + Quarton, LMR05S + CAX183
└── Post B: LMR05 → SM05L10 → filters → diamond; detector on MB4
```

---

## Optional add-ons (only if needed after alignment)

| Qty | Item | P/N | Unit (USD) | Why add | Link |
|-----|------|-----|------------|---------|------|
| 1 | SM05 spanner bit | **SPB05** | $31.14 | No lab wrench; install **SM05RR** without scratching filters | [SPB05](https://www.thorlabs.com/item/SPB05) |
| 1 | Large V-clamp (laser) | **VC3C** | $48.31 | No suitable lab clamp for Quarton | [VC3C](https://www.thorlabs.com/item/VC3C) |
| 1 | Third post line | **TR2** + **PH2** + **CF125** | $26.25 | Split laser vs lens on separate posts | [TR2](https://www.thorlabs.com/item/TR2) |
| 1 | 90° construction post | **TR3C** | $14.00 | Prefer PCB vertical beside stack | [TR3C](https://www.thorlabs.com/item/TR3C) |
| 1 | Full spanner wrench | **SPW603** | $30.54 | Easier than **SPB05** for tight rings | [SPW603](https://www.thorlabs.com/item/SPW603) |

---

## Previous full cart (reference — **$297.34**)

3× post lines, **TR4**, **VC3C**, **TR3C**, **SPW603** — use only if reduced layouts fail or advisor requires three independent heights.

<details>
<summary>Full 11-line table (click to expand)</summary>

| Qty | P/N | Line (USD) |
|-----|-----|------------|
| 1 | MB4 | $52.34 |
| 3 | PH2 | $28.74 |
| 3 | CF125 | $31.08 |
| 3 | TR4 | $21.42 |
| 1 | VC3C | $48.31 |
| 1 | LMR05S | $30.63 |
| 1 | SM05L10 | $17.47 |
| 1 | SM05RR | $4.63 |
| 1 | LMR05 | $18.18 |
| 1 | TR3C | $14.00 |
| 1 | SPW603 | $30.54 |
| | **Total** | **$297.34** |

</details>

---

## Not purchased (your existing list)

Arduino, ADF4351, power supply, 2× TQP3M9009, attenuator, SMA, microwave PCB + wire, diamond, magnet, Quarton, **CAX183**, BPW34, RG630, 5CGA-630, OPA381, TIA PCB, passives, safety glasses.

---

## Hardware

**Two** 1/4″-20 cap screws (for **1× CF125**), ~1/2″ length — lab or hardware store (~**$3**). Add two more if you use the **2-post** cart.

Full BOM: [parts_list.md](parts_list.md).
