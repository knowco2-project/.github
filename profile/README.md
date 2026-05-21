<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/knowco2-project/.github/main/profile/knowco2-logo-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/knowco2-project/.github/main/profile/knowco2-logo-light.svg">
    <img
      alt="knowco2 logo"
      src="https://raw.githubusercontent.com/knowco2-project/.github/main/profile/knowco2-logo-light.svg"
      width="240"
    >
  </picture>
</p>

<h1 align="center">knowco2</h1>

<p align="center">
  Open-source hardware and software for portable CO₂ monitoring and indoor air quality.
</p>

<p align="center">
  <!-- OSHWA UID badge — add after certification is approved -->
  <!-- <a href="https://certification.oshwa.org/USXXXXXX.html"><img alt="OSHWA Certified" src="https://img.shields.io/badge/OSHWA-USXXXXXX-blue"></a> -->
  <a href="https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE"><img alt="Docs license: CC-BY-SA-4.0" src="https://img.shields.io/badge/docs-CC--BY--SA--4.0-lightgrey"></a>
  <a href="https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE-HARDWARE"><img alt="Hardware license: CERN-OHL-S-2.0" src="https://img.shields.io/badge/hardware-CERN--OHL--S--2.0-orange"></a>
  <a href="https://spdx.org/licenses/MIT.html"><img alt="Firmware license: MIT" src="https://img.shields.io/badge/firmware-MIT-green"></a>
  <a href="https://github.com/knowco2-project/firmware-releases/releases"><img alt="Latest firmware release" src="https://img.shields.io/github/v/release/knowco2-project/firmware-releases?label=firmware&color=00d68f"></a>
  <a href="https://knowco2.com"><img alt="Website" src="https://img.shields.io/badge/website-knowco2.com-00b4d8"></a>
</p>

---

## Overview

knowco2 is an open-source CO₂ monitor built around low-cost, widely available microcontrollers and sensors. The firmware runs on CircuitPython and is designed to be readable, hackable, and straightforward to extend. All hardware design files, firmware, and documentation are released under open licenses.

This repository is the central hub for hardware files, firmware, and documentation.

---

## Open source hardware certification

This project is designed to comply with the [Open Source Hardware Definition v1.0](https://www.oshwa.org/definition/) from the Open Source Hardware Association (OSHWA).

**knowco2 OSHWA certification: pending** — UID will be added here once approved.

| Component | License |
|-----------|---------|
| Documentation | [CC-BY-SA-4.0](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE) — Creative Commons Attribution-ShareAlike 4.0 |
| Hardware design files | [CERN-OHL-S-2.0](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE-HARDWARE) — CERN Open Hardware Licence Strongly Reciprocal v2 |
| Firmware / software | [MIT](https://spdx.org/licenses/MIT.html) |

The primary components used in knowco2 are themselves OSHWA-certified open source hardware:

| Component | OSHWA UID |
|-----------|-----------|
| Adafruit Feather ESP32-S3 Reverse TFT | [US002502](https://certification.oshwa.org/us002502.html) |
| Adafruit SCD41 CO₂ Sensor Breakout | [US002089](https://certification.oshwa.org/us002089.html) |
| Sensirion SCD40 | [US002088](https://certification.oshwa.org/us002088.html) |
| Sensirion SCD30 | [US001081](https://certification.oshwa.org/us001081.html) |

<!-- Once approved, replace the pending note above with: -->
<!-- **OSHWA Certified:** [USXXXXXX](https://certification.oshwa.org/USXXXXXX.html) -->

---

## Repositories

| Repo | Visibility | Contents |
|------|-----------|----------|
| [knowco2-hardware](https://github.com/knowco2-project/knowco2-hardware) | Public | PCB files, enclosure, BOM, assembly docs |
| [firmware-releases](https://github.com/knowco2-project/firmware-releases) | Public | Pre-built firmware releases and changelogs |
| [.github](https://github.com/knowco2-project/.github) | Public | Org profile |

**knowco2-hardware structure:**
```
knowco2-hardware/
├── LICENSE                — CC-BY-SA-4.0 (documentation)
├── LICENSE-HARDWARE       — CERN-OHL-S-2.0 (hardware design files)
├── pcb/                   — Schematic and PCB design files
├── enclosure/             — 3D enclosure design files (STEP, STL, 3MF)
├── bom/                   — Bill of materials (bom.csv)
└── docs/
    ├── assembly.md        — Assembly instructions
    └── calibration.md     — Sensor calibration guide
```

---

## Supported hardware

**Microcontroller**
- Adafruit Feather ESP32-S3 Reverse TFT *(primary)*
- Other ESP32-S3 boards with adaptation

**Power**
- USB-C, 5 V 1 A
- Compatible with any USB-C source: wall adapters, power banks, laptop ports

**Sensors**

| Sensor | Measurement | Interface | Notes |
|--------|-------------|-----------|-------|
| Sensirion SCD41 | CO₂, temperature, humidity | I²C (0x62) | Primary |
| Sensirion SCD30 | CO₂, temperature, humidity | I²C | Supported |

Full bill of materials: [bom/bom.csv](https://github.com/knowco2-project/knowco2-hardware/blob/main/bom/bom.csv)

---

## Technical specifications

**CO₂ measurement (Sensirion SCD41)**

| Parameter | Value |
|-----------|-------|
| Range | 400–5000 ppm |
| Accuracy | ±(40 ppm + 5% of reading) |
| Interface | I²C at address 0x62 |

**Temperature measurement (Sensirion SCD41)**

| Parameter | Value |
|-----------|-------|
| Range | –10 to +60 °C |
| Accuracy | ±0.8 °C (at 15–35 °C) |

**Humidity measurement (Sensirion SCD41)**

| Parameter | Value |
|-----------|-------|
| Range | 0–95% RH |
| Accuracy | ±6% RH (at 15–35 °C, 20–65% RH) |

**Operating conditions**

| Parameter | Value |
|-----------|-------|
| Operating temperature | –10 to +60 °C (limited by SCD41) |
| Power input | 5 V via USB-C |
| Connectivity | 2.4 GHz Wi-Fi 802.11 b/g/n only (5 GHz not supported) |
| Bluetooth | BLE 5.0 |

**Microcontroller (Adafruit Feather ESP32-S3 Reverse TFT)**

| Parameter | Value |
|-----------|-------|
| Processor | ESP32-S3 dual-core Xtensa LX7 @ 240 MHz |
| Flash | 4 MB |
| PSRAM | 2 MB |
| Display | 1.14" IPS TFT, 240×135 px (ST7789) |

---

## Hardware files

Design files are in [knowco2-hardware](https://github.com/knowco2-project/knowco2-hardware). See the [hardware README](https://github.com/knowco2-project/knowco2-hardware/blob/main/README.md) for format details and sourcing notes.

- **PCB / schematic:** [pcb/](https://github.com/knowco2-project/knowco2-hardware/tree/main/pcb) — KiCad source files, Gerbers, PDF schematic
- **Enclosure:** [enclosure/](https://github.com/knowco2-project/knowco2-hardware/tree/main/enclosure) — STEP, STL, and source files
- **BOM:** [bom/bom.csv](https://github.com/knowco2-project/knowco2-hardware/blob/main/bom/bom.csv)

---

## Firmware

Firmware source is in [firmware/circuitpython/](firmware/circuitpython/). Pre-built releases are available on the [firmware-releases](https://github.com/knowco2-project/firmware-releases/releases) page as `.py` files ready to drop onto the device.

**Updating firmware**

- **Over the local network (recommended):** navigate to `http://knowco2-XXXX.local/update` in a browser and upload the new firmware file directly — no USB required.
- **Via USB:** hold the middle button (B) while powering on until the screen blinks. The `CIRCUITPY` drive mounts and you can replace `code.py` directly.
- **CircuitPython itself:** double-tap reset to enter the UF2 bootloader (`FTHRS3BOOT`), then drag a `.uf2` file onto the drive.

---

## Assembly

Step-by-step assembly instructions: [docs/assembly.md](https://github.com/knowco2-project/knowco2-hardware/blob/main/docs/assembly.md)

**Required tools**
- USB-C data cable (must support data transfer, not charge-only)
- Computer with a browser

**Quick start**
1. Flash the latest CircuitPython `.uf2` to the Feather board
2. Copy `code.py` and the `lib/` folder from the firmware release onto `CIRCUITPY`
3. Connect the SCD4x sensor via the I²C STEMMA QT / Qwiic connector (no soldering required)
4. Power on — the device will create a Wi-Fi access point named `knowco2-XXXX`
5. Connect to that network, visit `http://192.168.4.1`, and enter your Wi-Fi credentials

---

## Buttons

| Button | Location | Short press | Hold (~2 s) |
|--------|----------|-------------|-------------|
| A | Bottom | Toggle °C / °F | — |
| B | Middle | Cycle display mode (detailed → big CO₂ → graph) | — |
| C | Top | Toggle main screen / AP info screen | Switch between AP and Wi-Fi client mode |

---

## Integrations

**Local network (no account required)**

| Integration | How |
|-------------|-----|
| Home Assistant | MQTT — configure broker, port, credentials, and topic prefix in the settings portal |
| Any MQTT broker | Topics publish on `<prefix>/co2`, `/temp_c`, `/humidity` |
| Adafruit IO | Built-in Adafruit IO feed publishing |
| Grafana / InfluxDB | Poll `/data` or `/status` JSON endpoints, or subscribe via MQTT |
| Custom dashboards | HTTP JSON: `/status`, `/data`; CSV: `/export.csv` |
| OTA firmware updates | Browser-based update page at `/update` |

**Cloud (account required)**

| Integration | How |
|-------------|-----|
| knowco2 iOS app | Device management, history, real-time readings |
| knowco2 cloud portal | [cloud.knowco2.com](https://cloud.knowco2.com) |

---

## Troubleshooting

**Device won't connect to Wi-Fi**
- Check that your network is 2.4 GHz — 5 GHz is not supported
- Hold the top button (C) for ~2 seconds to switch back to AP mode, then connect to the device's own network and visit `http://192.168.4.1`

**CO₂ readings seem wrong**
- Allow ~60 seconds after power-on for the sensor to stabilize
- Automatic Self-Calibration (ASC) is enabled by default. The sensor tracks the lowest CO₂ level over time and uses that as the fresh-air baseline (~400 ppm). First adjustments appear after ~2 days; calibration settles within 7–9 days. See [docs/calibration.md](https://github.com/knowco2-project/knowco2-hardware/blob/main/docs/calibration.md) for full details.
- For immediate recalibration, take the device outdoors, wait for it to stabilize, then trigger Forced Recalibration (FRC) from the settings portal with a reference of 400 ppm.

**Display not updating**
- Press the middle button (B) to cycle display modes
- A watchdog reboot will occur automatically if the firmware hangs

---

## Resources

- **Getting started:** [knowco2.com/getting-started.html](https://knowco2.com/getting-started.html)
- **Calibration guide:** [docs/calibration.md](https://github.com/knowco2-project/knowco2-hardware/blob/main/docs/calibration.md) · [knowco2.com/calibration.html](https://knowco2.com/calibration.html)
- **CO₂ explainer:** [knowco2.com/co2-interactive.html](https://knowco2.com/co2-interactive.html)
- **Firmware releases:** [firmware-releases/releases](https://github.com/knowco2-project/firmware-releases/releases)
- **Issues & bug reports:** [open an issue](https://github.com/knowco2-project/knowco2/issues)
- **Contact:** [knowco2.com/contact.html](https://knowco2.com/contact.html)

---

## Project principles

- Accuracy over hype
- Privacy-first by design
- Low power, low operating cost
- Simple to build, simple to extend
- Fully open source

---

## Contributing

Issues, pull requests, and hardware experiments are welcome. If you're adapting the firmware for a different sensor or enclosure, opening an issue first is a good way to avoid duplicating work.

---

## License summary

| What | License | File |
|------|---------|------|
| Documentation, guides, this README | CC-BY-SA-4.0 | [LICENSE](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE) |
| Hardware design files (PCB, enclosure, BOM) | CERN-OHL-S-2.0 | [LICENSE-HARDWARE](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE-HARDWARE) |
| Firmware and software | MIT | [spdx.org/licenses/MIT](https://spdx.org/licenses/MIT.html) |

All licenses are [OSHWA-approved](https://www.oshwa.org/sharing-best-practices/made-with-creative-commons/) for open source hardware projects.
