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
  <a href="https://github.com/knowco2-project/knowco2-firmware/releases"><img alt="Latest firmware release" src="https://img.shields.io/github/v/release/knowco2-project/knowco2-firmware?label=firmware&color=00d68f"></a>
  <a href="https://knowco2.com"><img alt="Website" src="https://img.shields.io/badge/website-knowco2.com-00b4d8"></a>
</p>

---

## Overview

knowco2 is an open-source CO₂ monitor built around low-cost, widely available microcontrollers and sensors. The firmware runs on CircuitPython and is designed to be readable, hackable, and straightforward to extend. Hardware design files, firmware, integrations, and documentation are released under open licenses.

This organization is the central hub for knowco2 hardware files, firmware, integrations, and documentation.

---

## Open source hardware certification

This project is designed to comply with the [Open Source Hardware Definition v1.0](https://www.oshwa.org/definition/) from the Open Source Hardware Association (OSHWA).

**knowco2 OSHWA certification: pending** — UID will be added here once approved.

| Component | License |
|-----------|---------|
| Documentation | [CC-BY-SA-4.0](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE) — Creative Commons Attribution-ShareAlike 4.0 |
| Hardware design files | [CERN-OHL-S-2.0](https://github.com/knowco2-project/knowco2-hardware/blob/main/LICENSE-HARDWARE) — CERN Open Hardware Licence Strongly Reciprocal v2 |
| Firmware / software | [MIT](https://github.com/knowco2-project/knowco2-firmware) |

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
|------|------------|----------|
| [knowco2-hardware](https://github.com/knowco2-project/knowco2-hardware) | Public | Open hardware files, enclosure CAD, BOM, assembly docs |
| [knowco2-firmware](https://github.com/knowco2-project/knowco2-firmware) | Public | CircuitPython firmware source, pre-built releases, and changelogs |
| [knowco2-hacs](https://github.com/knowco2-project/knowco2-hacs) | Public | Home Assistant / HACS integration for KnowCO2 |

**knowco2-hardware structure:**

```text
knowco2-hardware/
├── LICENSE                — CC-BY-SA-4.0 (documentation)
├── LICENSE-HARDWARE       — CERN-OHL-S-2.0 (hardware design files)
├── pcb/                   — PCB/module notes and mechanical references
├── enclosure/             — 3D enclosure design files (STEP, STL, reference images)
├── bom/                   — Bill of materials (bom.csv)
└── docs/
    ├── assembly.md        — Assembly instructions
    └── calibration.md     — Sensor calibration guide
