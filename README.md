# Phial

A small (~22 mm diameter, round) battery-powered Bluetooth LE sensor board from
Golioth. Rev B.

> **Status:** pre-release cleanup for open-hardware (OSHW) publication.
> Items marked **[UNKNOWN]** below need confirmation before this README is
> final. Everything else was verified against the design files in this repo.

## Hardware summary (Rev B)

| Subsystem | Part / details | Notes |
|-----------|----------------|-------|
| Main SoC  | Nordic nRF54L15-QFAA | Rev B moved from nRF52 BGA to nRF54L15 DFN |
| PMIC      | Nordic nPM2100 (NPM2100-CAAA-R) | not populated on built boards — see Hardware status |
| IMU       | ST LIS2DH12 | 3-axis accelerometer, I2C |
| Microphone| ST MP34DT05TR-A | PDM MEMS mic |
| Audio out | Raltron RDTE-4.000-3030-NS1 | electromagnetic transducer (buzzer) |
| BLE antenna | Taoglas WLA.04 | 2.4 GHz chip antenna |
| NFC       | Taoglas FXC.24.A flex antenna | nets NFC1/NFC2 |
| Display/UI| 16x 0201 LED ring (Kingbright APG0201SEC-TT) | |
| Buttons   | Panasonic EVP-AWED4A + C&K KMS221G | [UNKNOWN] confirm both populated on Rev B |
| Battery   | CR2032 coin cell (HF1N holder) | [UNKNOWN] role of 112TR contact / alternate battery options |
| Debug     | SWD via Tag-Connect | alignment pins on paste layer |

**[UNKNOWN]** The schematic also references an nRF52840-CKAA-F-R (WLCSP) symbol
and a BME280. It is unclear whether these are an alternate/deprecated variant,
DNP on Rev B, or planned future population. Needs a pass against the Rev B BOM.

## Hardware status (Rev B)

- **The only boards ever built were assembled without the nPM2100.** A
  zero-ohm resistor selects the function and bypasses that section of the
  circuit, so the built variant runs without the Nordic PMIC.
- Consequence: the nPM2100 power path (battery management via VINT/VOUT) is
  designed but **never exercised on hardware** — treat it as unvalidated
  until a PMIC-populated build is made and tested.
- Further validation history not captured in this repo [UNKNOWN].

## Design files

- KiCad 9 project. **Note:** project files are currently named
  `pilulith.*` (the project's former codename). They are being renamed to
  `phial.*` as part of the release cleanup — see the cleanup checklist.
- 6-layer board, 0.8464 mm thick, ENIG finish, JLC06081H (2116/7628) stackup.
- `input/` — local symbol/footprint/3D sources and reference art.
- `pilulith.pretty/` (to be renamed) — project footprints, including Golioth
  and Orleon logo art footprints.

## Manufacturing outputs

**[UNKNOWN / TODO]** Gerbers, drill files, pick-and-place and BOM exports are
not yet committed or attached to a release. The BOM currently lives in
schematic symbol properties (last touched in commit `e64fb58`). A fabrication
package will be attached to a GitHub Release before publication.

## Firmware

Firmware lives in a separate repo: [golioth/phial-fw](https://github.com/golioth/phial-fw)
(currently private).

## License

Hardware in this repository is released under the **CERN Open Hardware
Licence v2 — Permissive (CERN-OHL-P)**. The LICENSE file is being added as
part of the release cleanup. Documentation and artwork are covered by the
same license unless noted otherwise.

Note: `input/art/` contains vendor reference images (Nordic, JLCPCB stackups,
Taoglas antenna drawings) that are **not** covered by this license and may be
replaced with links before publication — see the cleanup checklist.

## Credits

Designed by Chris Gammell at Golioth.
