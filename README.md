# Catapult Observatory

<p align="center">
  <img src="docs/images/catapult-overview.png"
       alt="Catapult Observatory project overview"
       width="920">
</p>

<p align="center">
  <strong>A repurposed hotel-TV wireless module transformed into a local Wi-Fi, Bluetooth, RSSI-sensing, and wireless-assessment platform.</strong>
</p>

<p align="center">
  Built by <strong>SilentiumLabs</strong>
</p>

---

## Overview

Catapult Observatory began with a specialized USB wireless module originally designed for hotel television systems.

The module is based on the **Marvell 88W8997** Wi-Fi and Bluetooth platform. Rather than leaving it limited to its original embedded use case, I rebuilt the surrounding software environment and developed a complete local wireless research and assessment platform around it.

This was not a plug-and-play project.

The build required:

- A custom WSL2 Linux kernel
- USB/IP passthrough from Windows into Kali Linux
- Marvell Wi-Fi and Bluetooth driver integration
- Wi-Fi access-point configuration
- DHCP, local DNS, routing, and NAT
- BlueZ-based Bluetooth support
- Local telemetry collectors
- RSSI-based sensing engines
- Experimental multi-link spatial sensing
- Local assessment, evidence, and reporting workflows
- A browser-based control and visualization dashboard

The result is **Catapult Observatory**, a proof-of-concept platform for local wireless visibility, device assessment, signal-behavior analysis, and hardware experimentation.

---

## Table of Contents

- [Project Status](#project-status)
- [From This to This](#from-this-to-this)
- [Why This Build Was Difficult](#why-this-build-was-difficult)
- [Custom Kernel Work](#custom-kernel-work)
- [System Architecture](#system-architecture)
- [Core Components](#core-components)
- [Wi-Fi Intelligence](#wi-fi-intelligence)
- [Bluetooth Intelligence](#bluetooth-intelligence)
- [RSSI-Based Sensing](#rssi-based-sensing)
- [Motion Lens](#motion-lens)
- [Spatial Lab](#spatial-lab)
- [IoT and Firmware Assessment](#iot-and-firmware-assessment)
- [Performance Laboratory](#performance-laboratory)
- [Assessment, Evidence, and Reporting](#assessment-evidence-and-reporting)
- [Local Processing and Privacy](#local-processing-and-privacy)
- [Project Images](#project-images)
- [Hardware and Driver Limitations](#hardware-and-driver-limitations)
- [Responsible Use](#responsible-use)
- [Documentation](#documentation)
- [Source Availability](#source-availability)

---

## Project Status

| Area | Status |
|---|---|
| Custom WSL2 kernel | Operational in the lab environment |
| USB/IP attachment | Operational |
| Marvell Wi-Fi interface | Operational when attached to WSL2 |
| Wi-Fi access point | Operational |
| Bluetooth controller | Operational |
| Local dashboard | Operational |
| Wi-Fi station telemetry | Operational |
| Bluetooth discovery and inventory | Operational |
| RSSI movement sensing | Experimental |
| Multi-link zone sensing | Experimental |
| Device-behavior analysis | Prototype |
| IoT and firmware comparison workflows | Prototype |
| Raw CSI | Not exposed by the current driver |
| Monitor mode | Not exposed by the current driver |

> **Important:** Catapult Observatory does not claim to identify people, reconstruct body pose, see through walls, or calculate exact physical coordinates. Its sensing features are based on measurable RSSI and station-telemetry changes exposed by the current driver.

---

## From This to This

### Original hardware

A USB wireless module designed for a narrow embedded use case:

- Marvell 88W8997 chipset
- 2×2 802.11ac Wi-Fi
- 2.4 GHz and 5 GHz operation
- Bluetooth and Bluetooth Low Energy
- USB 2.0 host interface
- Limited original software environment

<p align="center">
  <img src="docs/images/hardware-module.jpg"
       alt="Original Catapult Marvell wireless module"
       width="700">
</p>

### Rebuilt platform

A local research and assessment platform supporting:

- Wi-Fi client visibility
- Bluetooth discovery and inventory
- Signal and traffic history
- RSSI-based disturbance sensing
- Experimental multi-link zone sensing
- Performance measurements
- IoT assessment workflows
- Firmware before-and-after comparisons
- Evidence storage
- Findings and reporting
- Local-only processing

---

## Why This Build Was Difficult

The original hardware was not designed as a general-purpose Linux research adapter.

The work included:

1. Identifying the hardware and chipset
2. Building a custom WSL2 Linux kernel
3. Enabling the required USB, wireless, Bluetooth, and networking support
4. Passing the USB device from Windows into WSL2 with `usbipd-win`
5. Bringing the Marvell Wi-Fi and Bluetooth interfaces online
6. Creating a stable access-point stack
7. Building recovery scripts and persistent system services
8. Collecting only the telemetry the driver actually exposes
9. Designing signal-processing and visualization layers
10. Separating measured facts from experimental inference
11. Documenting unsupported capabilities instead of hiding them

---

## Custom Kernel Work

The standard WSL2 environment did not expose everything required to use the adapter as intended.

I built and deployed a custom Linux kernel:

```text
Linux 6.18.35.2-silentium-usb3+
```

The custom environment was configured for:

- WSL2 USB passthrough
- USB/IP support
- Marvell wireless hardware
- Wi-Fi access-point operation
- Bluetooth HCI support
- Linux routing and firewall features
- systemd-managed local services

The adapter is attached from Windows into Kali Linux using `usbipd-win`.

Once attached, the primary Wi-Fi interface appears inside Linux as:

```text
mlan0
```

The Bluetooth side appears as a Linux HCI controller, typically:

```text
hci0
```

---

## System Architecture

```mermaid
flowchart TD
    A[Windows Host] --> B[usbipd-win]
    B --> C[Custom WSL2 Linux Kernel]

    C --> D[Marvell Wi-Fi Interface]
    C --> E[Bluetooth HCI Interface]

    D --> F[Wi-Fi Access Point]
    F --> G[DHCP / Local DNS / NAT]

    D --> H[Telemetry Collector]
    E --> I[BlueZ Discovery and Inventory]

    H --> J[RSSI Sensing Engine]
    H --> K[Spatial Sensing Engine]
    H --> L[Assessment and Evidence Services]
    I --> L

    J --> M[Catapult Observatory Dashboard]
    K --> M
    L --> M
```

All primary processing and storage remain local.

---

## Core Components

### Windows host layer

- Windows
- WSL2
- `usbipd-win`
- USB attachment and recovery
- Browser access to the local dashboard

### Linux platform layer

- Kali Linux under WSL2
- Custom Linux kernel
- systemd services
- Marvell Wi-Fi driver
- Bluetooth HCI and BlueZ
- NetworkManager
- dnsmasq
- nftables

### Catapult application layer

- Python
- Flask
- JavaScript
- HTML and CSS
- SQLite
- Server-Sent Events
- Local JSON state snapshots
- systemd-managed background engines

---

## Wi-Fi Intelligence

Catapult Observatory can organize supported Wi-Fi station telemetry, including:

- Connected-client inventory
- Signal strength
- Average signal measurements
- Received and transmitted bytes
- Packet counters
- Client inactivity
- Transmission rate
- MCS information
- Failed transmissions
- Latency and jitter measurements
- Connection history
- Endpoint-change observations

The platform is designed to show what was actually measured rather than inventing unsupported values.

---

## Bluetooth Intelligence

The Bluetooth workspace uses Linux BlueZ services to provide:

- Nearby-device discovery
- Address-type classification
- Device-name inventory
- Pairing status
- Bonding status
- Trust status
- Connection status
- Service UUID inventory
- Advertisement history
- Privacy-exposure observations
- Read-only GATT inspection for approved devices
- Wi-Fi and Bluetooth coexistence testing

---

## RSSI-Based Sensing

Catapult Observatory includes experimental movement and radio-disturbance sensing using measurements exposed by the Wi-Fi driver.

The sensing engine analyzes:

- RSSI variation
- Signal span
- Short-term change
- Medium-term change
- Baseline deviation
- Measurement persistence
- Traffic freshness
- Feature agreement
- Endpoint movement

Possible states include:

```text
QUIET
BUILDING
DISTURBANCE
MOVEMENT
SUSTAINED ACTIVITY
SETTLING
ENDPOINT SHIFT
LOW QUALITY
```

The visualization represents signal-derived activity. It does not claim to display a physical person or exact location.

---

## Motion Lens

Motion Lens converts sensing measurements into a live visual representation of radio-path activity.

It includes:

- Motion-volume visualization
- Radio-path field visualization
- Temporal disturbance history
- Movement onset and decay
- Confidence indicators
- Data-quality indicators
- Session holding
- Frame export
- Full-screen visualization

Visual intensity is reduced when measurement quality or confidence is low.

<p align="center">
  <img src="docs/images/motion-lens.png"
       alt="Catapult Observatory Motion Lens"
       width="920">
</p>

---

## Spatial Lab

Spatial Lab combines measurements from multiple stationary Wi-Fi clients.

Each reference device creates a separate radio path between itself and the Catapult access point.

With several calibrated reference devices, the platform can estimate:

- Probable activity zone
- Zone likelihood
- Movement transitions
- Per-link disturbance strength
- Coverage quality
- Measurement confidence
- Reference-device movement
- Session history

These results are probabilistic zone estimates, not exact physical coordinates.

<p align="center">
  <img src="docs/images/spatial-lab.png"
       alt="Catapult Observatory Spatial Lab"
       width="920">
</p>

---

## IoT and Firmware Assessment

The platform supports controlled assessment workflows for owned or authorized devices.

Example workflow:

```text
Device Baseline
      ↓
Firmware Before Snapshot
      ↓
Firmware Update
      ↓
Firmware After Snapshot
      ↓
Service, privacy, and behavior comparison
```

The comparison workflow can record changes involving:

- Local services
- Network destinations
- Connection behavior
- Signal behavior
- Bluetooth exposure
- Performance measurements
- Privacy observations

---

## Performance Laboratory

Supported performance tests include:

- Client latency
- Packet loss
- Jitter
- DNS resolution time
- TCP connection time
- Device-by-device comparison
- Wi-Fi-only baseline
- Bluetooth coexistence testing

Unsupported measurements are marked unavailable instead of being estimated.

---

## Assessment, Evidence, and Reporting

Catapult Observatory includes local workflows for:

- Scope records
- Authorized assets
- Service validations
- Bluetooth validations
- Findings
- Evidence storage
- Evidence hashing
- Assessment timelines
- CSV exports
- JSON exports
- Printable reports

---

## Local Processing and Privacy

The platform may store supported metadata such as:

- Wireless station counters
- DHCP lease information
- Network connection metadata
- Bluetooth observations
- Performance measurements
- Sensing sessions
- Assessment evidence

It is not designed to collect:

- Passwords
- Credentials
- Decrypted HTTPS content
- Private messages
- Transferred files
- Application payload contents

No cloud processing is required for the core platform.

---

## Project Images

### Project overview

<p align="center">
  <img src="docs/images/catapult-overview.png"
       alt="Catapult Observatory project overview"
       width="920">
</p>

### Dashboard overview

The dashboard combines platform state, wireless throughput, Bluetooth observations, DNS metadata, assessment controls, and local activity history.

<p align="center">
  <img src="docs/images/dashboard-overview.png"
       alt="Catapult Observatory dashboard overview"
       width="920">
</p>

### Intelligence Hub

The Intelligence Hub combines local Wi-Fi and Bluetooth observations, behavior-model status, review items, and device activity into one workspace.

<p align="center">
  <img src="docs/images/intelligence-hub.png"
       alt="Catapult Observatory Intelligence Hub"
       width="920">
</p>

### Signals workspace

The Signals workspace visualizes supported Wi-Fi and Bluetooth measurements, signal strength, range estimates, RF information, latency, and collector status.

<p align="center">
  <img src="docs/images/signals-workspace.png"
       alt="Catapult Observatory Signals workspace"
       width="920">
</p>

### Bluetooth workspace

The Bluetooth workspace provides BlueZ-based discovery, controller management, pairing-state visibility, inventory, and read-only inspection workflows.

<p align="center">
  <img src="docs/images/bluetooth-workspace.png"
       alt="Catapult Observatory Bluetooth workspace"
       width="920">
</p>

### Sensing Studio status

<p align="center">
  <img src="docs/images/sensing-studio-status.png"
       alt="Catapult Observatory Sensing Studio status"
       width="920">
</p>

### Disturbance waterfall

<p align="center">
  <img src="docs/images/sensing-studio-waterfall.png"
       alt="Catapult Observatory disturbance waterfall"
       width="920">
</p>

> All public screenshots were sanitized to obscure device names, MAC addresses, Bluetooth identities, and other identifying information.

---

## Hardware and Driver Limitations

The current adapter and Linux driver expose managed, access-point, and P2P operation.

They do not expose:

- Monitor mode
- Raw Channel State Information
- Per-antenna CSI phase data
- Passive 802.11 frame capture
- Exact physical positioning
- Body-pose reconstruction
- Person identification
- True RF imaging

Catapult Observatory therefore does not claim to see people through walls or determine exact room coordinates.

Its sensing features use measurable RSSI and station-telemetry changes.

---

## What This Project Is Not

Catapult Observatory is not presented as:

- A certified intrusion-detection system
- A medical sensor
- A safety-critical occupancy detector
- A person-identification system
- A law-enforcement tracking platform
- A replacement for calibrated professional RF equipment

It is a proof of concept and engineering research platform.

---

## Responsible Use

Catapult Observatory is intended for:

- Hardware experimentation
- Owned-device testing
- Authorized wireless research
- IoT evaluation
- Local network assessment
- Educational use

Testing should only be performed on devices, hardware, and networks you own or are explicitly authorized to assess.

---

## Repository Structure

```text
catapult-observatory/
├── README.md
├── SECURITY.md
├── .gitignore
└── docs/
    ├── architecture.md
    ├── hardware.md
    ├── kernel-build.md
    ├── sensing.md
    ├── limitations.md
    ├── privacy-and-responsible-use.md
    └── images/
        ├── catapult-overview.png
        ├── hardware-module.jpg
        ├── dashboard-overview.png
        ├── intelligence-hub.png
        ├── signals-workspace.png
        ├── bluetooth-workspace.png
        ├── motion-lens.png
        ├── spatial-lab.png
        ├── sensing-studio-status.png
        └── sensing-studio-waterfall.png
```

---

## Documentation

- [Architecture](docs/architecture.md)
- [Hardware](docs/hardware.md)
- [Custom Kernel and WSL2 Integration](docs/kernel-build.md)
- [RSSI and Spatial Sensing](docs/sensing.md)
- [Limitations](docs/limitations.md)
- [Privacy and Responsible Use](docs/privacy-and-responsible-use.md)
- [Security Policy](SECURITY.md)

---

## Author

**Silentium**  
Founder, SilentiumLabs

GitHub: [silentiumlabsio](https://github.com/silentiumlabsio)

---

## Security Contact

Please do not publish sensitive evidence, credentials, private device identifiers, or suspected vulnerabilities in a public issue.

Security contact:

```text
Silentiumlabsio@gmail.com
```

See [SECURITY.md](SECURITY.md) for the responsible-disclosure policy.

---

## Source Availability

The full Catapult Observatory application remains private.

No open-source license is currently granted. Unless otherwise stated, the project design, interface, documentation, branding, and private source code remain the property of SilentiumLabs.

Copyright © 2026 SilentiumLabs. All rights reserved.
