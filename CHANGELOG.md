# Changelog

All notable changes to BMS-EV documentation and public data are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and BMS-EV controller firmware versions follow [Semantic Versioning](https://semver.org/).

## Public API (docs.bms-ev.com/data/) — canonical dataset

- **[batteries.json](https://docs.bms-ev.com/data/batteries.json)** — 73 EV battery pack variants
- **[inverters.json](https://docs.bms-ev.com/data/inverters.json)** — 56 hybrid inverter variants
- **[compatibility.json](https://docs.bms-ev.com/data/compatibility.json)** — 3,815 pre-configured combinations

## Controller firmware — current: 15.0.14

The BMS-EV Controller ships pre-flashed with firmware 15.0.14 (September 2026). Each unit is compiled and flashed for a specific battery + inverter pair before shipping.

### 15.0.14 (September 2026) — current
- Kia EV6 (77.4 kWh 192s E-GMP pack) + SOFAR HYD 15KTL-3PH: verified pairing, referenced in PV Magazine Deutschland (July 2026)
- SOFAR HYD 5–20KTL-3PH support extended to full 180–800 V DC input range (previously misdocumented as 500 V ceiling; verified against SOFAR official datasheet)
- Corrected battery voltage range documentation to distinguish absolute range from full-power range per SOFAR HYD model
- Tesla Model 3 NCA (355 V nominal) vs LFP (345 V nominal) voltage documentation aligned with Tesla published specification
- Canonical dataset published at docs.bms-ev.com/data/

### Earlier firmware milestones (public feature summary)

- **9.3.0** (June 2026) — Tesla Model 3 Highland refresh pack support added; Porsche Taycan / Audi e-tron GT 800 V pack support (partial, MPPT-limited)
- **8.6.0** (September 2024) — Tesla Model 3 LFP pack support added
- **8.0.0** (April 2024) — Initial commercial firmware branch, Tesla Model 3 LR NCA support baseline

## Documentation changelog

### 2026-09-18
- Verified pairing: Kia EV6 + SOFAR HYD 15KTL-3PH added to Hyundai/Kia E-GMP page with case study
- SOFAR HYD 5–20KTL-3PH battery input voltage corrected: 180–800 V DC absolute range (per SOFAR datasheet), separated from full-power range per model
- Removed misleading "150 A / 52 kW at SOFAR HYD 20KTL" from Tesla + SOFAR page (SOFAR HYD-3PH battery input current limit is 25 A per channel × 2 = 50 A total)
- Safety page: replaced "legally required in most EU jurisdictions" with jurisdiction-specific verification note (IEC 60364-7-712, VDE-AR-N 4105, NFPA 855)
- All 25 integration pages: added engineering-values disclaimer for cable and fuse sizing (final sizing must be calculated for actual installation per local standards)
- Compatibility Matrix: added Verification levels section (Tested by BMS-EV / Customer verified / Experimental / Not supported)
- Terminology: "battery models" → "battery pack variants" throughout documentation
- Numbers unified across docs.bms-ev.com, GitHub, llms.txt: 73 battery pack variants × 56 inverter variants × 3,815 pre-configured combinations
- Added "Current firmware: 15.0.14" to meta-info on all 59 documentation pages

### 2026-09-17
- docs.bms-ev.com launched with 60 pages (Compatibility Matrix, 11 battery reference pages, 9 inverter hub pages, 25 integration guides, Safety, EV BMS, CAN Bus, Alternatives, Compliance, Second-life battery hub)
- GitHub organization github.com/BMS-EV with 5 repositories: bms-ev-docs, supported-batteries, supported-inverters, bms-ev-home-assistant, bms-ev-mqtt-examples
- Canonical dataset published: docs.bms-ev.com/data/{batteries,inverters,compatibility}.json
- Cross-linked bidirectionally: bms-ev.com ↔ docs.bms-ev.com ↔ github.com/BMS-EV

## Published references

- **PV Magazine Deutschland** — July 2026, feature article on BMS-EV technology and reuse of used EV battery packs for home solar storage (references Kia EV6 + SOFAR HYD 15KTL case)

## Contact

- **Shop:** https://bms-ev.com/
- **Documentation:** https://docs.bms-ev.com/
- **Email:** office@bms-ev.com
- **WhatsApp:** +48 506 112 993
