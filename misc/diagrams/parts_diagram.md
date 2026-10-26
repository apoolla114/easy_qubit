## Apparatus diagram (team design)

Hybrid of **CW ODMR** from Zhang et al., *Little bits of diamond* ([Am. J. Phys. 86, 225 (2018)](https://doi.org/10.1119/1.5023389)) with **automated MW** (ADF4351 + microcontroller) and **compact detection** from Mariani et al. ([AIP Advances 12, 065321 (2022)](https://doi.org/10.1063/5.0089161)).

**BOM:** [../parts_list.md](../parts_list.md) · **Goals:** [../goals.md](../goals.md)

Two views of the same apparatus:


| View           | Section                               | Use when                                     |
| -------------- | ------------------------------------- | -------------------------------------------- |
| **Conceptual** | [below](#conceptual-signal--function) | Physics, reports, “what does this block do?” |
| **Physical**   | [below](#physical-build--layout)      | Assembly, Thorlabs mounts, bench layout      |


### Cross-reference (conceptual ↔ physical)


| Conceptual role                     | Physical where it lives                                            |
| ----------------------------------- | ------------------------------------------------------------------ |
| Microcontroller + ADC + USB logging | **Bench** — CTL module; USB to PC                                  |
| Synthesizer (set MW frequency)      | **Bench** — ADF4351                                                |
| Amplifier / attenuator              | **Bench** — TQP3M9009, att, SMA coax                               |
| Wire delivery (RF → B₁)             | **Holder** — wire-launch PCB + Burke wire                          |
| 520 nm pump + focus                 | **Laser assembly** — Quarton + CAX183                              |
| NV sample + B₀                      | **Holder** — diamond + magnet                                      |
| Filter stack (PL band)              | **Holder** — RG630, 5CGA-630 in stack                              |
| Photodiode + TIA                    | **Holder** — detector PCB (bottom of stack)                        |
| Oscilloscope                        | **Lab only** — optional probe on TIA output (not in PoC data path) |


---



## Conceptual (signal & function)

**Measurement:** CW laser on → sweep **MW frequency** → NV photoluminescence (PL) changes at resonance → log **PL vs f** via microcontroller ADC.

```mermaid
flowchart TB
    subgraph CTRL ["Control & acquisition"]
        CTL["Microcontroller\nSPI + on-chip ADC"]
        PC["PC\nfirmware, plots, logs"]
        CTL <-->|USB| PC
    end

    subgraph MW ["Microwave — manipulate electron spin"]
        SYN["Frequency synthesizer\n(ADF4351)"]
        AMP["Power amplifier\n(TQP3M9009)"]
        ATT["Attenuator\n(limit power & reflections)"]
        DEL["Thin-wire delivery\nRF current → B₁ at NVs"]
    end

    subgraph OPT ["Optical — pump NV ensemble (CW)"]
        SRC["520 nm source\n(spin init & PL readout)"]
        LNS["Focus lens\n(concentrate pump light)"]
    end

    subgraph SAMPLE ["Sample"]
        DIA["NV diamond"]
        MAG["Static magnetic field B₀\n(Zeeman splitting)"]
    end

    subgraph DET ["Optical → electrical"]
        FILT["Long-pass filters\n(RG630 + 5CGA-630)"]
        PD["Photodiode\nPL → photocurrent"]
        TIA["Transimpedance amp\n(OPA381: I → V)"]
    end

    CTL -->|program f_MW| SYN
    SYN -->|CW microwave| AMP --> ATT --> DEL
    DEL -.->|B₁| DIA

    SRC --> LNS -->|520 nm| DIA
    MAG -.->|B₀| DIA

    DIA -->|PL 600–800 nm| FILT --> PD --> TIA
    TIA -->|analog voltage| CTL
```



→ Physical placement of these blocks: [Physical build](#physical-build--layout)

---



## Physical (build & layout)

**Three things you fabricate / wire:** laser assembly, sample holder, bench RF + microcontroller.

```mermaid
flowchart TB
    PC["PC"]

    subgraph BENCH ["Bench — RF & microcontroller (wired on plate / breadboard)"]
        CTL["Microcontroller\n(on-chip ADC)"]
        SYN["ADF4351 module"]
        AMP["MW amp(s) TQP3M9009"]
        ATT["RF attenuator"]
        COAX["SMA coax"]
        CTL -->|SPI| SYN
        SYN --> AMP --> ATT --> COAX
    end

    subgraph LASERASM ["Laser assembly — Thorlabs MB4 post + VC3C clamp"]
        LASER["Quarton 520 nm module\n(built-in driver & collimation)"]
        L2["CAX183 in LMR05S"]
        LASER --> L2
    end

    subgraph HOLDER ["Sample holder — Thorlabs post + SM05 filter stack"]
        direction TB
        DIA["Diamond (top face — BurkeLab)"]
        LP1["RG630"]
        LP2["5CGA-630"]
        DETPCB["Detector PCB\nBPW34 + OPA381 TIA"]
        WPCB["Wire-launch PCB\n(SMA jack + pads)"]
        WIRE["40 µm Cu wire (BurkeLab)"]
        MAG["Permanent magnet\n(on or near holder)"]
        DIA --> LP1 --> LP2 --> DETPCB
        WPCB --> WIRE
    end

    PC <-->|USB| CTL
    COAX -->|SMA to holder| WPCB
    WIRE -.->|RF current near top face| DIA
    L2 -.->|520 nm beam down| DIA
    MAG -.->|B₀| DIA
    DETPCB -->|shielded wire to bench| CTL
```



→ What each block *does*: [Conceptual](#conceptual-signal--function)

### What each subassembly is


| Build unit         | Parts inside                                                                       | How it connects                                                                            |
| ------------------ | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Laser assembly** | **VC3C** + Quarton on **TR/PH**; **LMR05S** + CAX183 on second post              | Aim at **top** of diamond; height on **MB4**                                               |
| **Sample holder**  | **SM05L10** + RG630 + 5CGA-630; diamond on tube face; **DETPCB** on **TR3C**; wire PCB | **SMA coax** to wire PCB; **shielded** analog to CTL                                       |
| **Bench plate**    | **MB4** or separate plate: CTL, ADF4351, amp(s), attenuator, coax                  | **USB** to PC; lab PSUs; common ground with analog                                         |




### Stack (top → bottom on the holder)

```text
  [ laser beam from above ]
           ↓
      ┌─────────┐
      │ Diamond │  ← top face illuminated
      ├─────────┤
      │  RG630  │
      ├─────────┤
      │ 5CGA-630│
      ├─────────┤
      │  BPW34  │  ← same PCB as OPA381 (TIA)
      │ OPA381  │
      └─────────┘
   wire PCB + µm wire ── near diamond / PL region
```



### Build & bring-up order

1. **Detector PCB** — solder BPW34 + OPA381; verify TIA output (no diamond yet).
2. **Holder** — stack filters on PCB, fix diamond on top; attach wire-launch PCB; solder Burke wire; add magnet.
3. **Laser assembly** — align beam on diamond top face.
4. **Bench RF** — synth + amp + att + coax to holder; **low power** first (wire ≠ 50 Ω load).
5. **Microcontroller** — SPI frequency sweeps + ADC readout; log PL vs frequency.



### Electrical notes

- **ADC** is inside the microcontroller; detector PCB provides **voltage** to an analog input.  
- Match **ADF4351 SPI logic** (often 3.3 V) to CTL I/O.  
- Short **shielded** run from detector PCB to bench CTL; scope optional on TIA out for lab debug only.



### December target

Assembled **three subassemblies** + CW ODMR PoC — see [goals.md](goals.md).