# SMD133-to-AX5202P

Adapter PCB from the SMD133 mapper IC to the MMC3 AX5202P.

Several cartridge projects are designed for the AX5202P, but that chip is hard to find, whereas the SMD133 is easier to obtain. This board lets you use the SMD133 in those projects.

Russian version: [`README.ru.md`](README.ru.md)

## Jumper configuration

### `K5K7`

The **K5K7** jumper and the identically named SMD133 pin (on earlier SMD133 revisions — **K5K6**) set the address range used for cartridge configuration.  
Inside the SMD133 there is an internal pull-down to GND, therefore:

- If the jumper is **open** (left disconnected), the standard MMC3 range `$5000–$5005` is used.
- If the jumper is **closed**, the range depends on the SMD133 variant:
  - SMD133A → `$6000–$6005`
  - SMD133B → `$7000–$7005`

### `CPU_A1` and `CPU_A12`

The AX5202P does not have these pins, but the SMD133 does.  
If you need authentic (original) MMC3 behaviour — short these jumpers.  
There is a theory that everything may still work the same as on the AX5202P without them.

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
