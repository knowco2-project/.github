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
  <a href="LICENSE"><img alt="Docs license: CC-BY-SA-4.0" src="https://img.shields.io/badge/docs-CC--BY--SA--4.0-lightgrey"></a>
  <a href="LICENSE-HARDWARE"><img alt="Hardware license: CERN-OHL-S-2.0" src="https://img.shields.io/badge/hardware-CERN--OHL--S--2.0-orange"></a>
  <a href="firmware/LICENSE"><img alt="Firmware license: MIT" src="https://img.shields.io/badge/firmware-MIT-green"></a>
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

| Component | License |
|-----------|---------|
| Documentation | [CC-BY-SA-4.0](LICENSE) — Creative Commons Attribution-ShareAlike 4.0 |
| Hardware design files | [CERN-OHL-S-2.0](LICENSE-HARDWARE) — CERN Open Hardware Licence Strongly Reciprocal v2 |
| Firmware / software | [MIT](firmware/LICENSE) |

<!-- Replace the placeholder below with your OSHWA UID after approval -->
<!-- OSHWA Certification: [USXXXXXX](https://certification.oshwa.org/USXXXXXX.html) -->

---

## Repository structure

```
knowco2/
├── README.md              — This file
├── LICENSE                — CC-BY-SA-4.0 (documentation)
├── LICENSE-HARDWARE       — CERN-OHL-S-2.0 (hardware design files)
├── hardware/
│   ├── pcb/               — Schematic and PCB design files
│   ├── enclosure/         — 3D enclosure design files
│   └── bom/               — Bill of materials
├── firmware/
│   ├── LICENSE            — MIT (firmware)
│   └── circuitpython/     — CircuitPython firmware source
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
| Sensirion SCD4x (SCD40, SCD41) | CO₂, temperature, humidity | I²C | Primary |
| Sensirion SCD30 | CO₂, temperature, humidity | I²C | Supported |

Full bill of materials: [hardware/bom/bom.csv](hardware/bom/bom.csv)

---

## Hardware files

Design files are in [hardware/](hardware/). See [hardware/README.md](hardware/README.md) for format details and sourcing notes.

- **PCB / schematic:** [hardware/pcb/](hardware/pcb/) — KiCad source files, Gerbers, PDF schematic
- **Enclosure:** [hardware/enclosure/](hardware/enclosure/) — STEP, STL, and source files
- **BOM:** [hardware/bom/bom.csv](hardware/bom/bom.csv)

---

## Firmware

Firmware source is in [firmware/circuitpython/](firmware/circuitpython/). Pre-built releases are available on the [firmware-releases](https://github.com/knowco2-project/firmware-releases/releases) page as `.py` files ready to drop onto the device.

**Updating firmware**

- **Over the local network (recommended):** navigate to `http://knowco2-XXXX.local/update` in a browser and upload the new firmware file directly — no USB required.
- **Via USB:** hold the middle button (B) while powering on until the screen blinks. The `CIRCUITPY` drive mounts and you can replace `code.py` directly.
- **CircuitPython itself:** double-tap reset to enter the UF2 bootloader (`FTHRS3BOOT`), then drag a `.uf2` file onto the drive.

---

## Assembly

Step-by-step assembly instructions: [docs/assembly.md](docs/assembly.md)

**Required tools**
- Soldering iron (optional — if using headers)
- USB-C cable for initial flashing
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
- Automatic Self-Calibration (ASC) is enabled by default. The sensor tracks the lowest CO₂ level over time and uses that as the fresh-air baseline (~400 ppm). First adjustments appear after ~2 days; calibration settles within 7–9 days. See [docs/calibration.md](docs/calibration.md) for full details.
- For immediate recalibration, take the device outdoors, wait for it to stabilize, then trigger Forced Recalibration (FRC) from the settings portal with a reference of 400 ppm.

**Display not updating**
- Press the middle button (B) to cycle display modes
- A watchdog reboot will occur automatically if the firmware hangs

---

## Resources

- **Getting started:** [knowco2.com/getting-started.html](https://knowco2.com/getting-started.html)
- **Calibration guide:** [docs/calibration.md](docs/calibration.md) · [knowco2.com/calibration.html](https://knowco2.com/calibration.html)
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
| Documentation, guides, this README | CC-BY-SA-4.0 | [LICENSE](LICENSE) |
| Hardware design files (PCB, enclosure, BOM) | CERN-OHL-S-2.0 | [LICENSE-HARDWARE](LICENSE-HARDWARE) |
| Firmware and software | MIT | [firmware/LICENSE](firmware/LICENSE) |

All licenses are [OSHWA-approved](https://www.oshwa.org/sharing-best-practices/made-with-creative-commons/) for open source hardware projects.
