---
name: Integration report
about: Report a working (or non-working) BMS-EV controller + battery + inverter integration
title: '[Integration] Battery model + Inverter model'
labels: integration-report
assignees: ''
---

## Configuration

- **Battery pack:** (make, model, capacity, year of manufacture, generation if relevant — e.g. "Tesla Model 3 LR NCA 75 kWh, 2020")
- **Hybrid inverter:** (make, exact model, AC power, phase — e.g. "SOFAR HYD 10KTL-3PH")
- **BMS-EV controller firmware version:** (from the label or web UI — e.g. "15.0.14")
- **Controller hardware revision:** (from the label — e.g. "HW3.1")
- **Installation date:** YYYY-MM-DD

## Location

- **Country:** 
- **Climate:** (indoor conditioned, indoor unconditioned, garage, outdoor enclosure, etc.)

## Battery health at commissioning

- **State of Health (SoH):** % (measured via UDS/OBD, LeafSpy, TeslaFi, ScanMyTesla, Torque Pro or similar)
- **How measured:**
- **Battery age at install:** _years since first delivery_

## Solar / PV setup

- **PV size:** kWp
- **Inverter grid code applied:** (VDE-AR-N 4105 / G98 / G99 / CEI 0-21 / other)

## What worked immediately

## What required troubleshooting

## Current runtime data

- **Days in operation:** 
- **Total energy throughput:** kWh
- **Uptime:**  %

## Photos (optional)

Drag and drop photos of:
- Enclosure showing pack + controller + inverter
- Wiring
- Web UI screenshot showing pack telemetry
- Grafana / Home Assistant dashboard (if any)

## Consent

- [ ] I consent to BMS-EV publishing this integration in the [Compatibility Matrix](https://docs.bms-ev.com/compatibility/) as a **Customer verified** pairing, with the technical fields above (no personal data)
- [ ] I do not consent — this report is for private support only
