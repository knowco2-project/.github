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
  <a href="https://github.com/knowco2-project/firmware-releases/releases"><img alt="Latest firmware release" src="https://img.shields.io/github/v/release/knowco2-project/firmware-releases?label=firmware&color=00d68f"></a>
  <a href="https://knowco2.com"><img alt="Website" src="https://img.shields.io/badge/website-knowco2.com-00b4d8"></a>
  <a href="https://cloud.knowco2.com"><img alt="Cloud portal" src="https://img.shields.io/badge/cloud-cloud.knowco2.com-1a1a2e"></a>
</p>

---

## Overview

knowco2 is an open-source CO₂ monitor built around low-cost, widely available microcontrollers and sensors. The firmware runs on CircuitPython and is designed to be readable, hackable, and straightforward to extend. The cloud backend, iOS app, and enclosure designs are all open alongside it.

This organization is the central hub for firmware releases, hardware files, documentation, and support resources.

---

## Supported hardware

**Microcontroller**
- Adafruit Feather ESP32-S3 Reverse TFT *(primary)*
- Other ESP32-S3 boards with adaptation

**Power**
- USB-C, 5 V 1 A
- Works with any USB-C power source: wall adapters, power banks, laptop ports, and phones (using a USB-C to USB-C cable or male-to-male USB-C adapter)

**Sensors**
| Sensor | Measurement | Interface | Notes |
|--------|-------------|-----------|-------|
| Sensirion SCD4x (SCD40, SCD41) | CO₂, temperature, humidity | I²C | Primary |
| Sensirion SCD30 | CO₂, temperature, humidity | I²C | Supported |

Additional sensor support is intended to be straightforward to add. The firmware abstracts sensor reads behind a consistent interface.

---

## Repositories

| Repository | Description |
|------------|-------------|
| [firmware-releases](https://github.com/knowco2-project/firmware-releases) | Versioned firmware releases and changelogs |
| [.github](https://github.com/knowco2-project/.github) | Organization profile and shared configuration |

> Private repositories (cloud infrastructure, iOS app, Android app, hardware CAD) may be made public as development stabilizes.

---

## Apps

| Platform | Status |
|----------|--------|
| iOS (native Swift) | Available |
| Android | In development |

Both apps connect to the [knowco2 cloud](https://cloud.knowco2.com) for device management, historical data, and real-time readings.

---

## Integrations

knowco2 is designed to fit into the tools and workflows you already use, without requiring a cloud account for local features.

**Local network (no account required)**

| Integration | How |
|-------------|-----|
| Home Assistant | MQTT — configure broker, port, credentials, and topic prefix in the settings portal |
| Any MQTT broker (Mosquitto, Node-RED, etc.) | Same MQTT settings; topics publish on `<prefix>/co2`, `/temp_c`, `/humidity` |
| Adafruit IO | Built-in Adafruit IO publishing to named feeds |
| Grafana / InfluxDB | Poll the `/data` or `/status` JSON endpoints, or subscribe via MQTT |
| Custom dashboards / scripts | HTTP JSON endpoints: `/status`, `/data`; CSV download at `/export.csv` |
| OTA firmware updates | Browser-based update page at `/update` — no USB cable needed |

**Cloud (account required)**

| Integration | How |
|-------------|-----|
| knowco2 iOS app | Available now — device management, history, real-time readings |
| knowco2 Android app | In development |
| knowco2 cloud portal | [cloud.knowco2.com](https://cloud.knowco2.com) — web dashboard and device management |
| AI tools (Claude, Cursor, and others) | MCP (Model Context Protocol) server in development — query readings, trends, and alerts directly from your AI tools |

---

## Firmware releases

<!-- RELEASES_START -->
See the [firmware-releases](https://github.com/knowco2-project/firmware-releases/releases) page for all releases, changelogs, and downloadable `.uf2` / `.py` assets.
<!-- RELEASES_END -->

---

## Buttons

| Button | Location | Short press | Hold (~2 s) |
|--------|----------|-------------|-------------|
| A | Bottom | Toggle °C / °F | — |
| B | Middle | Cycle display mode (detailed → big CO₂ → graph) | — |
| C | Top | Toggle between main screen and AP info screen | Switch between AP and STA (Wi-Fi client) mode |

---

## Quick reference

**Device won't connect to Wi-Fi**
- Check that your network is 2.4 GHz — 5 GHz is not supported
- Hold the **top button (C) for ~2 seconds** to switch back into AP mode, then connect to the device's own Wi-Fi network and visit `http://192.168.4.1` to update credentials
- Once connected to your network, the portal is accessible at `http://knowco2-XXXX.local` — replace `XXXX` with the four-character ID shown on the device's AP info screen

**CO₂ readings seem wrong**
- Allow ~60 seconds after power-on for the sensor to stabilize
- **Automatic Self-Calibration (ASC)** is enabled by default and is the recommended long-term calibration method. The sensor tracks the lowest CO₂ level it sees over time and uses that as the fresh-air baseline (~400 ppm). For best results, expose the device to outdoor air for at least a few minutes periodically — this gives ASC a reliable reference point. First adjustments appear after ~2 days; the calibration settles within 7–9 days of normal use. See the [calibration guide](https://knowco2.com/calibration.html) for full details.
- If readings are consistently off and you want to recalibrate immediately, use **Forced Recalibration (FRC)**: take the device outdoors, wait for it to stabilize, then trigger recalibration from the settings portal with a reference value of 400 ppm
- Only disable ASC if the device is used in a continuously occupied or sealed space where CO₂ never drops to outdoor levels — in those environments ASC will drift low over time

**Display not updating**
- Press the middle button (B) to cycle through display modes
- A watchdog reboot will occur automatically if the firmware hangs

**Cloud not receiving data**
- Confirm the device HMAC key matches what's registered in the cloud portal
- Check that the device has a valid NTP time sync (required for HMAC signature validity)
- Review the serial output at 115200 baud for error messages

**Updating firmware or device files**

> **Caution:** Modifying files directly on the device can prevent it from booting if done incorrectly. Only do this if you know what you're changing, and keep a backup of the original files.

- **To update firmware over the local network** (recommended): with the device connected to your Wi-Fi, navigate to `http://knowco2-XXXX.local/update` in a browser. You can upload a firmware file directly from that page without connecting a USB cable.
- **To update device files via USB** (e.g. `code.py`, config): hold the **middle button (B)** while powering on and keep holding it until the screen blinks. The `CIRCUITPY` drive will mount on your computer and you can edit files directly.
- **To update CircuitPython itself**: double-tap the reset button quickly. The device enters the UF2 bootloader and mounts as `FTHRS3BOOT`. Drag a new `.uf2` file onto that drive to flash it.
- If the device is unresponsive after a file change, re-enter drive mode as above and restore the previous `code.py` from a [firmware release](https://github.com/knowco2-project/firmware-releases/releases).

---

## Resources

- **Getting started:** [knowco2.com/getting-started.html](https://knowco2.com/getting-started.html)
- **Calibration guide:** [knowco2.com/calibration.html](https://knowco2.com/calibration.html)
- **CO₂ explainer:** [knowco2.com/co2-interactive.html](https://knowco2.com/co2-interactive.html)
- **Repair & self-service:** [knowco2.com/#repair](https://knowco2.com/#repair)
- **Warranty:** [knowco2.com/warranty.html](https://knowco2.com/warranty.html)
- **Contact:** [knowco2.com/contact.html](https://knowco2.com/contact.html)
- **Cloud portal:** [cloud.knowco2.com](https://cloud.knowco2.com)
- **Firmware releases & changelogs:** [firmware-releases/releases](https://github.com/knowco2-project/firmware-releases/releases)
- **Issues & bug reports:** open an issue in the relevant repository

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
