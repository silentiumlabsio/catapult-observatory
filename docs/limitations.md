# Limitations

Catapult Observatory documents unsupported capabilities clearly.

## Driver Limitations

The current Marvell Linux driver exposes:

- Managed mode
- Access-point mode
- P2P client mode
- P2P group-owner mode

It does not expose monitor mode in the current environment.

## Unavailable Measurements

The current adapter and driver do not provide:

- Raw Channel State Information
- Per-subcarrier amplitude
- Per-subcarrier phase
- Per-antenna CSI
- Raw beamforming feedback
- Passive 802.11 management-frame capture

## Sensing Limitations

The system cannot honestly claim:

- Person identification
- Body-pose reconstruction
- Exact room coordinates
- Reliable direction from a single link
- Through-wall imaging
- True RF imaging
- Exact distance without specialized calibration and hardware

## Environmental Limitations

RSSI is affected by:

- Multipath propagation
- Walls and furniture
- Device orientation
- Reference-device movement
- Nearby networks
- Client power saving
- Traffic cadence
- Radio interference

## WSL2 Limitations

The USB device may need to be reattached after:

- Windows reboot
- WSL shutdown
- USB reset
- Driver reset
- Device unplug and reconnect

The dashboard may remain inactive until `mlan0` is restored.

## Project Scope

Catapult Observatory is a proof of concept and research platform.

It should not be treated as:

- A certified intrusion-detection system
- A medical sensor
- A safety-critical occupancy detector
- A law-enforcement tracking tool
- A replacement for professional RF equipment
