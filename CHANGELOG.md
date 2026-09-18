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

### 2026-09-18 (full external verification pass — second review)
- Full audit of docs against manufacturer datasheets and community reverse-engineering sources
- **Renault Zoe Gen2 ZE50** chemistry corrected: LG Chem LGX E78 NCM 712 pouch cells (not CATL LFP as previously stated), per pushevs.com teardown
- **Stellantis eCMP** (Peugeot e-208, Opel Corsa-e, Citroën) cell configuration corrected: 108s2p (not 96s), 356–448 V operating range, per dalathegreat Battery-Emulator wiki teardown
- **GoodWe** DC voltage ranges corrected against official goodwe.com datasheets:
  - EH single-phase: 85–460 V DC (was 100–450 V)
  - ET three-phase: 200–800 V DC (ET/ET-LV) or 200–865 V DC (ETC G2) — was 180–600 V
- **SolaX X3 Hybrid G4** DC range corrected: 120–800 V DC (was 90–800 V), per solaxpower.com/x3-hybrid-g4 datasheet
- **Fronius GEN24 Plus** communication protocol corrected: **Modbus RTU RS485 via RJ45** (NOT CAN as previously stated). Emulates BYD HVS/M (2020-25) battery model. Voltage range: up to 450 V (Primo single-phase) or up to 700 V (Symo three-phase), per dalathegreat Battery-Emulator Fronius wiki
- **SMA Sunny Boy Storage 3.7/5.0/6.0** corrected: this is a **high-voltage DC-coupled battery inverter** (100–550 V DC, 360 V rated) per sma.de datasheet — NOT a 48 V LV inverter as previously stated. Only the older SBS 2.5 was LV
- **Sungrow SH5.0–10RT** corrected: 150–600 V DC (was 160–560 V), per en.sungrowpower.com datasheet
- **Solis S6-EH1P** high-voltage corrected: 120–500 V DC (was 90–500 V), per solisinverters.com datasheet
- **FoxESS H1/H3** corrected: 80–500 V DC (was 90–500 V), per fox-ess.com datasheet
- **Deye SUN HP3** battery voltage range corrected — CRITICAL FIX:
  - SUN-5K to 25K SG01HP3-EU-AM2: **160–700 V DC** (per Deye datasheet_sun-(5-25)k-sg01hp3-eu_230724_en.pdf)
  - SUN-29.9K to 50K SG01HP3-EU-BM3/BM4: **160–800 V DC** (per Deye approved battery list DY-HV(160-800)-028)
  - Previous documentation stated 160–500 V DC which was incorrect. This changes E-GMP + Deye compatibility: 77.4 kWh packs (peak ~806 V) can pair with Deye 29.9–50K models at max SoC ~95 %
- **Tesla CAN message IDs** corrected against dalathegreat Battery-Emulator TESLA-BATTERY.cpp source code:
  - Previous docs listed 0x132, 0x212, 0x352 (with wrong content), 0x312, 0x2A2, 0x102 — several of these were incorrect
  - Actual frame set: 0x20A (contactors), 0x212 (BMS state, isolation), 0x229 (heartbeat), 0x252 (regen/discharge power), 0x292 (SoC), 0x2D2 (min/max cell V + current limits), 0x312 (thermal), 0x332 (brick V), 0x352 (energy metrics NOT cell V), 0x392 (module type/mass), 0x3D2 (lifetime counters), 0x2B4 (DCDC voltages) — with source-code link added
- **Nissan Leaf CAN IDs** corrected: 0x1DC is **charge/discharge current limits** (not voltage/temperature as previously stated); 0x5BC added for SoH/temperatures; 0x5C0 corrected to cell voltage groups (multiplexed) not just pack temperature. Source: My Nissan Leaf forum + Dala Battery-Emulator project
- Hyundai/Kia + Deye compatibility table updated to reflect corrected Deye voltage ranges (77.4 kWh E-GMP now compatible with Deye 29.9–50K SG01HP3 with SoC limit)


### 2026-09-18 (later same day — external verification pass)
- Kia EV6 77.4 kWh voltage corrected: ~697 V nominal / ~480–806 V operating range (per batterydesign.net teardown, 192s2p SK Innovation NMC pouch cells) — previous 523 V nominal was incorrect for 77.4 kWh (523 V applies to 58.2 kWh RWD variant only)
- Kia EV6 + SOFAR HYD 15KTL case study clarified: max SoC limited to ~95 % (pack ~790 V) to stay safely below SOFAR 800 V DC ceiling
- Tesla Model 3 SR+ LFP voltage refined: ~340 V nominal (3.2 V/cell × 106s, per batterydesign.net) instead of 345 V
- VW MEB pack configurations corrected: 55 kWh = 96s2p (8 modules × 12 cells), 61 kWh = 108s2p (9 modules × 12 cells), 82 kWh = 96s3p (12 modules × 24 cells, 8s3p per module) — per batterydesign.net teardown; previous 77-82 kWh = 108s label was incorrect
- SOFAR HYD 5-20KTL-3PH battery input clarified: **two independent battery channels** (25 A each, ~10 kW each) that can accept separate battery banks or be paralleled — not a single input as previously stated
- Deye BYD HVS support ceiling clarified: 512 V max per BYD compatibility list, therefore E-GMP 697 V packs cannot use Deye SUN HP3 family (SOFAR HYD is the practical route)
- Life projection methodology footer added to 6 pages: cites Preger et al. 2020, Recurrent 2025 fleet data, Geotab 2023 EV battery health report
- Technical author/reviewer/revision metadata added to all 59 documentation pages
- Cable specification clarified: H1Z2Z2-K solar cable (IEC 62930 / EN 50618) recommended; PV1-F noted as older standard not recommended for new installations


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


### 2026-09-18 (P0 fixes from ChatGPT audit review #3)
- **compatibility.csv schema v2.0**: added 9 new provenance fields per row:
  - status, verification_type: field_verified / protocol_verified / in_catalog
  - verification_date, battery_part_number, battery_revision
  - inverter_firmware_min, bms_ev_firmware_min, hardware_revision
  - source, notes
- **Kia EV6 + Sofar HYD 3-20KTL-3PH** marked as field_verified with PV Magazine July 2026 reference
- **541 rows marked protocol_verified** across Tesla, BMW i3, BMW iX/i4-i7, Nissan Leaf, VW MEB, Renault Zoe Gen1/Gen2, Peugeot e-208, Opel Corsa-e, Citroen e-C4 - sources: dalathegreat Battery-Emulator, openinverter.org, batterydesign.net, pushevs.com, My Nissan Leaf forum, LeafSpy
- **3273 rows remain in_catalog** - BMS-EV firmware supports the pair via protocol translation but no field/protocol source attached yet
- **WP blog corrections**: 25 translations of Complete BMS Guide for Tesla Model 3/Y/S received technical corrections note - Pylontech LV vs BYD HVS/Pylontech HV per inverter, Tesla generic voltage/cell-count/balance simplifications flagged, HV connector specs, commissioning per-system rather than universal 10-20A/30min rules
- **34 translations of DIY 30 kWh Tesla Modules** received architectural distinction note - complete OEM pack vs reconfigured modules
- **About + Safety Architecture pages (10 translations)** received clarification - automotive OEM validation is NOT stationary ESS validation - installer responsible for IEC 60364-7-712, VDE-AR-N 4105, NFPA 855, UL 9540 compliance
- **WP page 168016**: 80+ battery types marketing overstatement -> 73 battery profiles (68 OEM EV pack variants + 5 DIY BMS profiles) with docs link

### 2026-09-18 (P1 completion - full audit closeout)
- compatibility.csv v2.1: enriched with 40+ battery part numbers and revisions across Tesla, BMW, Nissan, MEB, Zoe, Stellantis, Kia, BYD, Chevrolet Bolt, Ford, Rivian, Porsche, Volvo, Polestar, MG and more
- field_verified count doubled: 1 to 2 - added Nissan Leaf 40 kWh + SOFAR HYD from PV Magazine July 2026 installation
- protocol_verified count: 541 to 2306 - added part numbers + revisions to every pair with an open-source teardown or documented CAN protocol source
- in_catalog remaining: 3273 to 1507 - less-documented battery models
- battery_part_number populated: 0 to 2308 rows - 60.5 percent of dataset now has explicit OEM part numbers
- Sources section added to 20 authority pages: 11 battery + 9 inverter authority pages on docs.bms-ev.com now have h2 id=sources table with Parameter / Value / Source rows referencing batterydesign.net, dalathegreat/Battery-Emulator, openinverter.org, pushevs.com, manufacturer datasheets and BMS-EV production field data
- 462 WP blog posts across 26 languages received the Technical corrections audit 2026-09-18 note covering commissioning current, commissioning time, HV connector requirements, cable sizing, cell voltage/SoC/balance simplifications
