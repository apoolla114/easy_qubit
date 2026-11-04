## Apparatus diagram (team design)

Hybrid of **CW ODMR** from Zhang et al., *Little bits of diamond* ([Am. J. Phys. 86, 225 (2018)](https://doi.org/10.1119/1.5023389)) with **automated MW** (ADF4351 + microcontroller) and **compact detection** from Mariani et al. ([AIP Advances 12, 065321 (2022)](https://doi.org/10.1063/5.0089161)).

**BOM:** [../parts_list.md](../parts_list.md) · **Goals:** [../goals.md](../goals.md)

Two views of the same apparatus:


| View           | Section                               | Use when                                     |
| -------------- | ------------------------------------- | -------------------------------------------- |
| **Conceptual** | [below](#conceptual-signal--function) | Physics, reports, “what does this block do?” |
| **Physical**   | [below](#physical-build--layout)      | Assembly, Thorlabs mounts, bench layout      |
| **Costs**      | [parts_diagram_cost.md](parts_diagram_cost.md) | Budget, orders, per-block $                  |


### Cross-reference (conceptual ↔ physical)


| Conceptual role                     | Physical where it lives                                            |
| ----------------------------------- | ------------------------------------------------------------------ |
| Microcontroller + ADC + USB logging | **Bench** — CTL module; USB to PC                                  |
| Synthesizer (set MW frequency)      | **Bench** — ADF4351                                                |
| Amplifier (attenuator optional)     | **Bench/table** — TQP3M9009; SMA coax to Burke antenna             |
| MW antenna (RF → B₁)                | **Holder** — Burke PCB + SMA female (supplied)                     |
| 520 nm pump + focus                 | **Laser assembly** — Quarton + CAX183                              |
| NV sample + B₀                      | **Holder** — diamond + magnet                                      |
| Filter stack (PL band)              | **Holder** — RG630, 5CGA-630 in stack                              |
| Photodiode + TIA                    | **Holder** — **BPW34** on filters; **F5** breakout + **OPA381** under PD on **MB4** |
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
        ATT["Attenuator\n(optional — defer)"]
        ANT["Burke MW antenna\n(PCB + SMA → B₁ at NVs)"]
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
    SYN -->|CW microwave| AMP --> ATT --> ANT
    ANT -.->|B₁| DIA

    SRC --> LNS -->|520 nm| DIA
    MAG -.->|B₀| DIA

    DIA -->|PL 600–800 nm| FILT --> PD --> TIA
    TIA -->|analog voltage| CTL
```



→ Physical placement of these blocks: [Physical build](#physical-build--layout)

---



## Physical (build & layout)

**Three things you assemble / wire:** laser assembly, sample holder (optics + Burke antenna), bench/table RF + microcontroller (SMA chain).

```mermaid
flowchart TB
    PC["PC"]

    subgraph BENCH ["Bench/table — RF & microcontroller (SMA chain, no breadboard)"]
        CTL["Microcontroller\n(on-chip ADC)"]
        SYN["ADF4351 module"]
        AMP["MW amp(s) TQP3M9009"]
        ATT["RF attenuator\n(optional)"]
        COAX["SMA coax"]
        CTL -->|SPI| SYN
        SYN --> AMP --> ATT --> COAX
    end

    subgraph LASERASM ["Laser assembly — Thorlabs MB4 breadboard"]
        BOARD["MB4 breadboard\n(4″ × 6″)"]
        QLM["Quarton QLM-1125\n2-axis laser mount"]
        LASER["Quarton 520 nm module\n(built-in driver & collimation)"]
        POST_L["Lens post\nTR1 → MB4"]
        L2["CAX183 in LMR7"]
        BOARD --- QLM --- LASER
        BOARD --- POST_L --- L2
        LASER --> L2
    end

    subgraph HOLDER ["Sample holder — contact stack on detector (Mariani-style)"]
        direction TB
        DIA["Diamond (top face — BurkeLab)"]
        LP1["RG630"]
        LP2["5CGA-630"]
        PD["BPW34 photodiode"]
        BRK["Stargazer breakout\nOPA381 TIA — screws to MB4"]
        ANT["Burke MW antenna\n(PCB + SMA female)"]
        MAG["Permanent magnet\n(on or near holder)"]
        DIA --> LP1 --> LP2 --> PD --> BRK
    end

    PC <-->|USB| CTL
    COAX -->|SMA to antenna| ANT
    ANT -.->|RF near sample| DIA
    L2 -.->|520 nm beam down| DIA
    MAG -.->|B₀| DIA
    BRK -->|shielded wire to bench| CTL
```



→ What each block *does*: [Conceptual](#conceptual-signal--function)

### What each subassembly is


| Build unit         | Parts inside                                                                       | How it connects                                                                            |
| ------------------ | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Laser assembly** | Quarton in **QLM-1125**, base held to **MB4** by 2× **CL5A**; CAX183 in **LMR7** on **TR1** screwed into **MB4** | Lens height is fixed (~38 mm center) until **PH1 + CF125** are added — see [parts_list_reference.md](../parts_list_reference.md#lens-post-ph1--cf125-deferred) |
| **Sample holder**  | RG630 + 5CGA-630 + diamond on **BPW34**; **F5** Stargazer breakout (**OPA381**) on **MB4** under PD; **Burke antenna** | Optional **SM05** cage + **TR1.5** / **TR3C** in [reference](../parts_list_reference.md) |
| **MW bench**       | ADF4351, amp(s), optional att, **SMA coax** on table                               | **Synth → amp → (att) → coax → Burke antenna**; CTL **USB** to PC; lab PSUs              |




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
      │  BPW34  │  ← active area under filters
      ├─────────┤
      │ F5 PCB  │  ← Stargazer breakout; **OPA381** (8-VSSOP) + TIA passives; standoffs to **MB4**
      └─────────┘
   Burke MW antenna (SMA) ── RF near diamond / PL region
```



### Build & bring-up order

1. **Detector** — solder **OPA381** (+ **F6** passives) to **F5** breakout (8-VSSOP / 0.65 mm pad side); mount board to **MB4**; wire **BPW34** to TIA input; verify output (no diamond yet).
2. **Holder** — stack filters on **BPW34**; diamond on top; mount **Burke antenna** near sample; add magnet.
3. **Laser assembly** — align beam on diamond top face.
4. **Bench RF** — synth → amp → (att if needed) → **SMA coax** → Burke **SMA female**; **low power** first.
5. **Microcontroller** — SPI frequency sweeps + ADC readout; log PL vs frequency.



### Electrical notes

- **ADC** is inside the microcontroller; detector PCB provides **voltage** to an analog input.  
- Match **ADF4351 SPI logic** (often 3.3 V) to CTL I/O.  
- Short **shielded** run from detector PCB to bench CTL; scope optional on TIA out for lab debug only.
- Quarton housing is at **+V** (not ground) — keep it insulated from the **MB4** and posts.



### December target

Assembled **three subassemblies** + CW ODMR PoC — see [goals.md](goals.md).