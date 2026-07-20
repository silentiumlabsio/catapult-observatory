# Catapult Observatory

<p align="center">
  <strong>A repurposed hotel-TV wireless module transformed into a local Wi-Fi, Bluetooth, RSSI-sensing, and device-intelligence platform.</strong>
</p>

<p align="center">
  Built under <strong>SilentiumLabs</strong>
</p>

---

## Overview

Catapult Observatory began with a specialized USB wireless module originally intended for hotel television systems.

The module is based on the Marvell 88W8997 Wi-Fi and Bluetooth platform. Instead of leaving it limited to its original purpose, I rebuilt the surrounding software environment and developed a complete local wireless research and assessment platform around it.

This was not a plug-and-play project.

The build required:

- A custom WSL2 Linux kernel
- USB/IP passthrough from Windows into Kali Linux
- Marvell wireless driver integration
- Wi-Fi access-point configuration
- Bluetooth support through BlueZ
- DHCP, DNS, routing, and NAT services
- Local telemetry collectors
- RSSI-based sensing engines
- Spatial sensing experiments
- Device behavior modeling
- A complete browser-based dashboard

The result is **Catapult Observatory**, a proof-of-concept platform for local wireless visibility, experimentation, device assessment, and telemetry analysis.

---

## From This

A USB wireless module designed for a narrow embedded use case:

- Marvell 88W8997 chipset
- 2×2 802.11ac Wi-Fi
- Bluetooth and BLE support
- USB 2.0 interface
- Limited original software environment

## To This

A complete local platform supporting:

- Wi-Fi client visibility
- Bluetooth discovery
- Device inventory
- Signal and traffic history
- RSSI-based movement sensing
- Experimental multi-link zone sensing
- Device behavior baselines
- IoT assessment workflows
- Firmware before-and-after comparisons
- Performance and coexistence testing
- Evidence storage
- Findings and reporting
- Local-only processing

---

## Custom Kernel Work

The standard WSL2 environment did not expose everything required to use the adapter as intended.

I built and deployed a custom Linux kernel:

```text
Linux 6.18.35.2-silentium-usb3+
