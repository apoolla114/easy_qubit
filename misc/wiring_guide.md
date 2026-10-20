## Wiring (verify the pins against UM3115, the NUCLEO-H563ZI user manual, and the module's silkscreen)

```mermaid
flowchart LR
  subgraph nucleo [NUCLEO-H563ZI]
    PA5["PA5 SPI1_SCK (D13)"]
    PB5["PB5 SPI1_MOSI (D11)"]
    PD14["PD14 GPIO out (D10)"]
    CEpin["GPIO out (e.g. D9)"]
    LDpin["GPIO in (e.g. D8)"]
    GNDn[GND]
    V5[5V]
  end
  subgraph adf [ADF4351 module]
    CLK
    DAT
    LE
    CE
    LD
    GNDa[GND]
    PWR["DC in 5V"]
  end
  PA5 --> CLK
  PB5 --> DAT
  PD14 --> LE
  CEpin --> CE
  LD --> LDpin
  GNDn --- GNDa
  V5 --> PWR
```
- Connect the grounds together. If the module has a 3V3 header pin, do **not** also feed it from the Nucleo while the DC jack is powered.
- MISO isn't used, because the ADF4351 can't be read back. You can optionally route MUXOUT to a GPIO input instead.
