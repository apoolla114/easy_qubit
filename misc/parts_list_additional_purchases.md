# Additional purchases (base apparatus only)

Parts **not** on your existing team list (Arduino, ADF4351, amps, SMA, antenna PCB/wire, diamond, magnet, Quarton laser, **CAX183**, BPW34, both filters, OPA381, TIA PCB, passives, safety glasses, 3D-printed mounts).

These are **Thorlabs optomechanics** that **replace the three 3D-printed mounts** and implement the [physical layout](diagrams/parts_diagram.md). No March extensions (no KM100, MW switch, HW-KIT2, second filter, etc.).

**Prices:** Thorlabs **USD list price** from [thorlabs.com](https://www.thorlabs.com) product pages (checked **Oct 2026**). Tax and shipping are extra. Combine **CAX183** on the same Thorlabs order you already planned—do **not** duplicate CAX183 here.

---

## Thorlabs — order table

| Qty | Item | Thorlabs P/N | Unit price (USD) | Line total (USD) | Link |
|-----|------|--------------|------------------|------------------|------|
| 1 | Aluminum breadboard 4″ × 6″ × 1/2″ | **MB4** | $52.34 | $52.34 | [MB4](https://www.thorlabs.com/item/MB4) |
| 3 | Post holder, L = 2″ | **PH2** | $9.58 | $28.74 | [PH2](https://www.thorlabs.com/item/PH2) |
| 3 | Clamping fork, 1.24″ slot (for breadboard) | **CF125** | $10.36 | $31.08 | [CF125](https://www.thorlabs.com/item/CF125) |
| 3 | Optical post, L = 4″ | **TR4** | $7.14 | $21.42 | [TR4](https://www.thorlabs.com/item/TR4) |
| 1 | Large V-clamp (Quarton laser module) | **VC3C** | $48.31 | $48.31 | [VC3C](https://www.thorlabs.com/item/VC3C) |
| 1 | Lens mount, SM05 internal/external threads | **LMR05S** | $30.63 | $30.63 | [LMR05S](https://www.thorlabs.com/item/LMR05S) |
| 1 | SM05 lens tube, 1″ thread depth (filter stack) | **SM05L10** | $17.47 | $17.47 | [SM05L10](https://www.thorlabs.com/item/SM05L10) |
| 1 | SM05 retaining ring (second filter; tube includes one) | **SM05RR** | $4.63 | $4.63 | [SM05RR](https://www.thorlabs.com/item/SM05RR) |
| 1 | Lens mount (filter stack base on post) | **LMR05** | $18.18 | $18.18 | [LMR05](https://www.thorlabs.com/item/LMR05) |
| 1 | 90° construction post (detector / wire PCB mount) | **TR3C** | $14.00 | $14.00 | [TR3C](https://www.thorlabs.com/item/TR3C) |
| 1 | Spanner wrench for SM05 retaining rings | **SPW603** | $30.54 | $30.54 | [SPW603](https://www.thorlabs.com/item/SPW603) |

| | **Thorlabs list subtotal** | | | **$297.34** | |

---

## Not purchased (use your existing list)

Already covered by your BOM: microcontroller, ADF4351, power supply, 2× TQP3M9009, attenuator, SMA hardware, microwave PCB + Burke wire, diamond, magnet, Quarton laser, **CAX183**, BPW34, RG630, 5CGA-630, OPA381, photodiode/TIA PCB, R/C/wire/perfboard, safety glasses.

---

## Lab / hardware (not on either list)

| Item | Notes |
|------|--------|
| **Six 1/4″-20 cap screws** | Mount **CF125** forks to **MB4** (typically **1/2″** length); often in optics lab—buy locally (~**$5–10**) if missing. |
| **8-32 setscrew** | Post into **PH2** (usually included with posts/holders). |

---

## Assembly mapping (replaces 3D prints)

| Former 3D print | Thorlabs build |
|-----------------|----------------|
| Laser mount | **VC3C** on **TR4** + **PH2** + **CF125** on **MB4** |
| Focusing lens holder | **LMR05S** on second post line; **CAX183** (your order) |
| Diamond / filters / PD holder | **LMR05** + **SM05L10** + **SM05RR** + filters + diamond; **TR3C** for detector PCB |

Full BOM: [parts_list.md](parts_list.md).
