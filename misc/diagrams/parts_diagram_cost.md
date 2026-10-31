## Apparatus diagram — with costs (team design)

Same layout as [parts_diagram.md](parts_diagram.md). **Line format:** `role, part / MPN, ext $` (list USD). **$0** = BurkeLab, EECS lab, or team stock unless noted.

**BOM detail:** [../parts_list.md](../parts_list.md) · **No-cost views:** [parts_diagram.md](parts_diagram.md)

| View | Section |
|------|---------|
| **Conceptual** | [below](#conceptual-signal--function-costs) |
| **Physical** | [below](#physical-build--layout-costs) |

**Pricing scope:** P0 parts you **buy** (1× MW amp; attenuator **deferred**; no custom wire-launch PCB; no PCB-mount SMA). **MB4** from lab (not in Thorlabs cart). Team checkout reference: **Amazon ~$102**, **program ~$572** (Oct 2026, incl. tax/shipping on some vendors).

---

## Conceptual (signal & function) — costs

```mermaid
flowchart TB
    subgraph CTRL ["Control & acquisition — section total $0"]
        CTL["microcontroller, Uno / Nucleo, $0"]
        PC["PC, existing, $0"]
        CTL <-->|USB| PC
    end

    subgraph MW ["Microwave — section total $27"]
        SYN["synthesizer, ADF4351 module, $23"]
        AMP["amplifier, TQP3M9009, $4"]
        ATT["attenuator, optional defer, $0"]
        ANT["Burke MW antenna, PCB + SMA female, $0"]
    end

    subgraph OPT ["Optical pump — section total $28"]
        SRC["520 nm source, Quarton VLM-520-74, $28"]
        LNS["focus lens, CAX183, $0 in Thorlabs cart"]
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
    SYN -->|CW microwave| AMP --> ATT --> ANT
    ANT -.->|B₁| DIA

    SRC --> LNS -->|520 nm| DIA
    MAG -.->|B₀| DIA

    DIA -->|PL 600–800 nm| FILT --> PD --> TIA
    TIA -->|analog voltage| CTL
```

| Section | Subtotal (USD) |
|---------|----------------|
| Control & acquisition | **0** |
| Microwave (purchased) | **27** |
| Optical pump (Amazon laser only) | **28** |
| Sample | **0** |
| Detection | **83** |
| **Conceptual subassemblies (excludes Thorlabs mechanics & safety)** | **138** |

*Attenuator (~$16) omitted — add only if power is too high. **CAX183** ($16) is in the Thorlabs subtotal below.*

---

## Physical (build & layout) — costs

Thorlabs lines match [thorlabs_cart_p0.csv](../thorlabs_cart_p0.csv) (no **MB4**). MW chain on bench/table via **SMA coax** (lab or Amazon **M4**); **Burke antenna** at holder.

```mermaid
flowchart TB
    PC["PC, existing, 0"]

    subgraph BENCH ["Bench — RF & microcontroller — section total $27"]
        CTL["microcontroller, Uno / Nucleo, $0"]
        SYN["synthesizer, ADF4351 module, $23"]
        AMP["MW amp, TQP3M9009, $4"]
        COAX["SMA coax, lab / Amazon, $0"]
        CTL -->|SPI| SYN
        SYN --> AMP --> COAX
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

    subgraph HOLDER ["Sample holder — section total $191"]
        DIA["diamond, BurkeLab chip, $0"]
        LP1["filter, SCHOTT RG630, $37"]
        LP2["filter, Newport 5CGA-630, $38"]
        SM05["filter stack, SM05L10 + SM05RR + LMR05, $40"]
        DETPCB["detector perfboard, lab BPW34 + OPA381, $8"]
        ANT["Burke MW antenna, PCB + SMA female, $0"]
        MAG["magnet, lab Nd disk, $0"]
        POST_H["post lines ×2, PH2 + CF125 + TR4 each, $54"]
        TR3C["detector post optional, Thorlabs TR3C, $14"]
        DIA --> LP1 --> LP2 --> DETPCB
        SM05 --- LP1
        TR3C --- DETPCB
    end

    PC <-->|USB| CTL
    COAX -->|SMA male to female| ANT
    ANT -.->|RF near sample| DIA
    L2 -.->|520 nm beam down| DIA
    MAG -.->|B₀| DIA
    DETPCB -->|shielded wire to bench| CTL
```

| Build unit | Subtotal (USD) | Notes |
|------------|----------------|--------|
| **Bench** | **27** | ADF4351 + 1× amp; CTL + coax at $0 (lab); no breadboard for RF |
| **Laser assembly** | **150** | Quarton + CAX183 + VC3C + LMR05S + one post line |
| **Sample holder** | **191** | Filters + SM05 stack + detector ICs + TR3C + two post lines; Burke antenna $0 |
| **Physical subassemblies** | **368** | Excludes safety glasses ($23); **MB4** lab loan for posts |

---

## Overall (P0 team purchase)

| Category | Ext $ |
|----------|-------|
| Purchased MW + optics modules + filters + detector ICs (no Thorlabs) | **138** |
| Thorlabs optomechanics + CAX183 ([cart CSV](../thorlabs_cart_p0.csv), no MB4) | **~231** |
| Laser safety glasses (Walmart O3) | **23** |
| **Overall P0 list (before tax/shipping)** | **~392** |

| Removed vs earlier BOM | Savings (list) |
|------------------------|----------------|
| **MB4** (lab breadboard) | ~52 |
| **M3** attenuator (defer) | ~16 |
| **M5** PCB-mount SMA (on Burke antenna) | ~9 |
| **M6** custom wire-launch PCB (Burke antenna) | ~15 |

Add **~10–15% + shipping**; optional **SPW603** spanner (+$13–37) and **2nd TQP3M9009** (+$4) not included. **Amazon wishlist (MW + laser):** team checkout **~$102** (Oct 2026).

Full vendor tables: [parts_list.md](../parts_list.md#orders-by-vendor).

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
   Burke MW antenna (SMA), $0 · SM05/LMR05/TR3C/mechanics in holder subtotal
```

### Microwave cable chain (purchased path)

```text
ADF4351 → TQP3M9009 → [attenuator if needed] → SMA coax → Burke antenna (SMA female)
```
