## Apparatus diagram — with costs (team design)

Same layout as [parts_diagram.md](parts_diagram.md). **Line format:** `role, part / MPN, ext $` (list USD, Oct 2026). **$0** = BurkeLab, EECS lab, or team stock unless noted.

**BOM detail:** [../parts_list.md](../parts_list.md) · **No-cost views:** [parts_diagram.md](parts_diagram.md)

| View | Section |
|------|---------|
| **Conceptual** | [below](#conceptual-signal--function-costs) |
| **Physical** | [below](#physical-build--layout-costs) |

**Pricing scope:** P0 parts you **buy** (Scenario B — full Thorlabs Tier 1, both filters, 1× amp). Ranges in BOM (e.g. 2× amp) are not shown here.

---

## Conceptual (signal & function) — costs

```mermaid
flowchart TB
    subgraph CTRL ["Control & acquisition — section total $0"]
        CTL["microcontroller, Uno / Nucleo, $0"]
        PC["PC, existing, $0"]
        CTL <-->|USB| PC
    end

    subgraph MW ["Microwave — section total $42"]
        SYN["synthesizer, ADF4351 module, $23"]
        AMP["amplifier, TQP3M9009, $4"]
        ATT["attenuator, SMA fixed, $0"]
        DEL["wire delivery, JLC wire-launch PCB + Burke wire, $15"]
    end

    subgraph OPT ["Optical pump — section total $44"]
        SRC["520 nm source, Quarton VLM-520-74, $28"]
        LNS["focus lens, Thorlabs CAX183, $16"]
    end

    subgraph SAMPLE ["Sample — section total $0"]
        DIA["NV diamond, BurkeLab chip, $0"]
        MAG["static B₀, lab magnet, $0"]
    end

    subgraph DET ["Optical → electrical — section total $83"]
        FILT["filters, SCHOTT RG630 + Newport 5CGA-630, $75"]
        PD["photodiode, BPW34S-Z, $4"]
        TIA["TIA, OPA381AIDGKR, $4"]
    end

    CTL -->|program f_MW| SYN
    SYN -->|CW microwave| AMP --> ATT --> DEL
    DEL -.->|B₁| DIA

    SRC --> LNS -->|520 nm| DIA
    MAG -.->|B₀| DIA

    DIA -->|PL 600–800 nm| FILT --> PD --> TIA
    TIA -->|analog voltage| CTL
```

| Section | Subtotal (USD) |
|---------|----------------|
| Control & acquisition | **0** |
| Microwave | **42** |
| Optical pump | **44** |
| Sample | **0** |
| Detection | **83** |
| **Conceptual subassemblies (excludes bench mechanics & safety)** | **169** |

*Conceptual blocks omit Thorlabs breadboard/posts/clamps ($267 list for T1–T10) and laser safety glasses ($23). Those appear in the physical view and overall total.*

---

## Physical (build & layout) — costs

Thorlabs lines follow [parts_list.md](../parts_list.md) Tier 1 cart; **MB4** is counted under **Bench**; laser and holder posts are split per [subassembly table](parts_diagram.md#what-each-subassembly-is).

```mermaid
flowchart TB
    PC["PC, existing, 0"]

    subgraph BENCH ["Bench — RF, microcontroller, breadboard — section total $79"]
        CTL["microcontroller, Uno / Nucleo, $0"]
        SYN["synthesizer, ADF4351 module, $23"]
        AMP["MW amp, TQP3M9009, $4"]
        ATT["RF attenuator, lab SMA, $0"]
        COAX["SMA coax, lab / Amazon RG316, $0"]
        MB4["breadboard, Thorlabs MB4, $52"]
        CTL -->|SPI| SYN
        SYN --> AMP --> ATT --> COAX
    end

    subgraph LASERASM ["Laser assembly — section total $150"]
        LASER["520 nm module, Quarton VLM-520-74, $28"]
        L2["focus lens, CAX183 in LMR05S, $16"]
        VC3C["laser clamp, Thorlabs VC3C, $48"]
        POST_L["post line, PH2 + CF125 + TR4, $27"]
        LMR05S["lens mount, LMR05S, $31"]
        LASER --> L2
        VC3C --- LASER
        POST_L --- LMR05S
    end

    subgraph HOLDER ["Sample holder — section total $206"]
        DIA["diamond, BurkeLab chip, $0"]
        LP1["filter, SCHOTT RG630, $37"]
        LP2["filter, Newport 5CGA-630, $38"]
        SM05["filter stack, SM05L10 + SM05RR + LMR05, $40"]
        DETPCB["detector PCB, BPW34S-Z + OPA381, $8"]
        TR3C["detector post, Thorlabs TR3C, $14"]
        WPCB["wire-launch PCB, JLCPCB 2-layer, $15"]
        WIRE["copper wire, BurkeLab 40 µm, $0"]
        MAG["magnet, lab Nd disk, $0"]
        POST_H["post lines ×2, PH2 + CF125 + TR4 each, $54"]
        DIA --> LP1 --> LP2 --> DETPCB
        WPCB --> WIRE
        SM05 --- LP1
        TR3C --- DETPCB
    end

    PC <-->|USB| CTL
    COAX -->|SMA to holder| WPCB
    WIRE -.->|RF current near top face| DIA
    L2 -.->|520 nm beam down| DIA
    MAG -.->|B₀| DIA
    DETPCB -->|shielded wire to bench| CTL
```

| Build unit | Subtotal (USD) | Notes |
|------------|----------------|--------|
| **Bench** | **79** | MB4 + ADF4351 + 1× amp; CTL/coax/attenuator at $0 (lab) |
| **Laser assembly** | **150** | Quarton + CAX183 + VC3C + LMR05S + one post line |
| **Sample holder** | **206** | Both filters + SM05 stack + detector ICs + wire PCB + TR3C + two post lines |
| **Physical subassemblies** | **435** | Excludes safety glasses ($23) |

---

## Overall (P0 team purchase)

| Category | Ext $ |
|----------|-------|
| Conceptual/detection + RF + optics ICs & modules (no Thorlabs mechanics) | 169 |
| Thorlabs optomechanics T1–T10 (incl. split above) | 267 |
| Laser safety glasses (Walmart O3) | 23 |
| **Overall P0 list (Scenario B)** | **~459** |

Add **~10–15% + shipping**; optional **SPW603** spanner (+$13) and **2nd TQP3M9009** (+$4) not included. Full vendor tables: [parts_list.md](../parts_list.md#orders-by-vendor).

### Stack (top → bottom) — line items

```text
  [ laser beam from above ]
           ↓
      ┌─────────┐
      │ Diamond │  sample, BurkeLab, $0
      ├─────────┤
      │  RG630  │  filter, SCHOTT RG630, $37
      ├─────────┤
      │ 5CGA-630│  filter, Newport 5CGA-630, $38
      ├─────────┤
      │  BPW34  │  photodiode, BPW34S-Z, $4
      │ OPA381  │  TIA, OPA381AIDGKR, $4
      └─────────┘
   wire PCB, 15 · Burke wire, 0 · SM05/LMR05/TR3C/mechanics in holder subtotal
```
