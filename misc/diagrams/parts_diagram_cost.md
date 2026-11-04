## Apparatus diagram — with costs

Parts we are buying now, placed where they go in the build. **Node format:** `role, part, $` (list USD). **$0** = BurkeLab, EECS lab, or team stock. Order details: [../parts_list.md](../parts_list.md).

```mermaid
flowchart TB
    PC["PC, existing, $0"]

    subgraph BENCH ["Bench — RF & microcontroller — $36"]
        CTL["microcontroller, Uno / Nucleo, $0"]
        SYN["synthesizer, ADF4351 module, $23"]
        AMP["MW amp, TQP3M9009, $4"]
        COAX["SMA coax, RG316 male–male, $9"]
        CTL -->|SPI| SYN
        SYN --> AMP --> COAX
    end

    subgraph LASERASM ["Laser assembly — $167"]
        BOARD["breadboard 4″×6″, Thorlabs MB4, $52"]
        CL5A["base hold-down, 2× Thorlabs CL5A, $11"]
        QLM["laser mount, Quarton QLM-1125, $32"]
        LASER["520 nm module, Quarton VLM-520-74, $28"]
        POST_L["lens post, TR1 into MB4, $6"]
        LMR7["lens mount, Thorlabs LMR7, $22"]
        L2["focus lens, CAX183, $16"]
        BOARD --- CL5A --- QLM --- LASER
        BOARD --- POST_L --- LMR7 --- L2
        LASER --> L2
    end

    subgraph HOLDER ["Sample holder — $92"]
        DIA["diamond, BurkeLab chip, $0"]
        LP1["filter, SCHOTT RG630, $37"]
        LP2["filter, Newport 5CGA-630, $38"]
        PD["photodiode, BPW34, $4"]
        BRK["detector PCB, Stargazer 8-VSSOP breakout, $9"]
        TIA["TIA, OPA381, $4"]
        ANT["MW antenna, Burke PCB + SMA female, $0"]
        MAG["magnet, lab Nd disk, $0"]
        DIA --> LP1 --> LP2 --> PD --> BRK
        BRK --- TIA
    end

    SAFETY["laser safety glasses, Walmart, $23"]

    PC <-->|USB| CTL
    COAX -->|SMA| ANT
    ANT -.->|RF near sample| DIA
    L2 -.->|520 nm| DIA
    MAG -.->|B₀| DIA
    BRK -->|shielded wire| CTL
```

| Block | $ |
|-------|---|
| Bench | 36 |
| Laser assembly | 167 |
| Sample holder | 92 |
| Safety glasses | 23 |
| **Total (list, before tax/shipping)** | **318** |
