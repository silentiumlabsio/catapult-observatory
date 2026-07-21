# Hardware

## Original Module

Catapult Observatory is built around a USB wireless module originally used in hotel television systems.

The module uses the Marvell 88W8997 wireless platform.

## Confirmed Hardware Characteristics

The hardware provides:

- 2×2 802.11ac Wi-Fi
- 2.4 GHz and 5 GHz support
- 20, 40, and 80 MHz channel-width capability
- Bluetooth and Bluetooth Low Energy support
- USB 2.0 host connection
- Integrated antenna design

## Current Linux Interfaces

When attached successfully to WSL2, the module exposes:

- A Wi-Fi interface, typically `mlan0`
- A Bluetooth HCI controller, typically `hci0`

## Why the Hardware Was Interesting

The module was designed for a narrow embedded deployment, but it still contained a capable Wi-Fi and Bluetooth chipset.

The project explored how much useful functionality could be recovered and repurposed through:

- Kernel configuration
- USB/IP passthrough
- Wireless-driver integration
- Access-point services
- BlueZ integration
- Local software development

## What the Hardware Can Support in This Project

- Local Wi-Fi access point
- Connected-station telemetry
- Bluetooth discovery
- Device inventory
- RSSI-based signal analysis
- Performance testing
- Wi-Fi and Bluetooth coexistence experiments

## What the Current Driver Does Not Expose

- Monitor mode
- Raw CSI
- Per-antenna CSI phase
- Passive 802.11 frame capture
- Exact physical positioning

These limitations are documented instead of hidden.
