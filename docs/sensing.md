# RSSI and Spatial Sensing

## Overview

Catapult Observatory includes experimental sensing features based on station telemetry exposed by the Marvell Wi-Fi driver.

This is not raw CSI sensing.

## Available Measurements

The driver can expose measurements such as:

- RSSI
- Average signal level
- Inactivity time
- Received bytes and packets
- Transmitted bytes and packets
- Failed transmissions
- Transmission rate
- MCS information

## Single-Link Sensing

A single stationary reference device creates one radio path between the access point and the client.

The sensing engine evaluates:

- Short-term RSSI variation
- Medium-term variation
- Signal span
- Baseline deviation
- Change persistence
- Traffic freshness
- Feature agreement
- Endpoint movement

## Why Active Traffic Matters

When a client is idle, station telemetry may update too slowly for useful sensing.

Controlled active traffic helps keep measurements fresh.

## Motion Lens

Motion Lens is a visualization layer for signal-derived activity.

It can display:

- Movement onset
- Sustained disturbance
- Decay
- Confidence
- Data quality
- Temporal echoes

The moving shape is a signal-activity proxy, not a body model.

## Multi-Link Spatial Sensing

Several stationary clients can create multiple radio paths.

The spatial engine compares the disturbance pattern across these links and can estimate a probable calibrated zone.

Possible outputs include:

- Probable activity zone
- Zone likelihood
- Link disturbance strength
- Zone transition
- Measurement confidence
- Coverage quality

## Calibration

A useful calibration process includes:

1. Record an empty-room baseline.
2. Keep all reference devices stationary.
3. Record consistent movement in each zone.
4. Repeat each zone several times.
5. Validate with blind test runs.
6. Reject or recalibrate weak links.

## Limitations

RSSI-based sensing is strongly affected by:

- Device placement
- Walls
- Furniture
- Multipath propagation
- Background traffic
- Client power saving
- Nearby wireless activity
- Reference-device movement

Results are probabilistic and experimental.
