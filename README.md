# SMD133-to-AX5202P

Adapter PCB from the SMD133 mapper IC to the MMC3 AX5202P.

Several cartridge projects are designed for the AX5202P, but that chip is hard to find, whereas the SMD133 is easier to obtain. This board lets you use the SMD133 in those projects.

Russian version: [`README.ru.md`](README.ru.md)

## Jumper configuration

### `K5K7`

The **K5K7** jumper (on SMD133A the corresponding pin is labeled **K5K6**, on SMD133B — **K5K7**) selects which **additional** register block is active on the SMD133.

- If the jumper is **closed**, the range `$5000–$5005` is used.
- If the jumper is **open** (left open), the range depends on the SMD133 variant:
  - SMD133A → `$6000–$6005`
  - SMD133B → `$7000–$7005`

**Note:** With the jumper open, the chip’s internal pull-down holds the pin to GND. If you want to drive this signal from an external source (for example, from the cartridge PCB), solder to the matching pad on the board and do not bridge the jumper. A closed jumper, conversely, pulls the pin to VCC.  
If you are not planning to experiment with the SMD133, the simplest approach is to leave the jumper unsoldered — this does not affect MMC3 mapper operation.

### `CPU_A1` and `CPU_A12`

The AX5202P does not have these pins, but the SMD133 does.  
These jumpers let you either bring in external address-line signals (for example, from the cartridge PCB) or tie them to ground.

- **Close the jumpers** — the corresponding SMD133 pins are forced to GND. This yields behaviour close to authentic MMC3.
- **Leave them open** — you can feed `CPU_A1` and `CPU_A12` from external circuitry by soldering to the jumper pads.

**Important:** It is not recommended to leave these pins floating (connected neither to ground nor to an external signal). In theory this could lead to unpredictable mapper behaviour, although no one has deliberately verified this.

### `WRAM +CE` and `WRAM WE`

These are **normally closed** jumpers:

- `WRAM +CE` is pulled to `VCC`.
- `WRAM WE` is shorted to the `CPU_RW` signal.

This wiring reproduces AX5202P behaviour, so it is recommended to leave the jumpers as-is.  
If you want to experiment — cut the corresponding jumper.

## License

This project is licensed under **CERN Open Hardware Licence Version 2 – Permissive** (`CERN-OHL-P-2.0`).  
See `LICENSE` for details.

SPDX-License-Identifier: `CERN-OHL-P-2.0`
