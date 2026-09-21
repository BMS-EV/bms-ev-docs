# Changelog

All notable changes to BMS-EV documentation and public data are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and BMS-EV controller firmware versions follow [Semantic Versioning](https://semver.org/).

## Public API (docs.bms-ev.com/data/) — canonical dataset

- **[batteries.json](https://docs.bms-ev.com/data/batteries.json)** — 73 EV battery pack variants
- **[inverters.json](https://docs.bms-ev.com/data/inverters.json)** — 56 hybrid inverter variants
- **[compatibility.json](https://docs.bms-ev.com/data/compatibility.json)** — 3,815 pre-configured combinations

## Controller firmware — current: 16.5.0

The BMS-EV Controller ships pre-flashed with firmware 16.5.0 (September 2026). Each unit is compiled and flashed for a specific battery + inverter pair before shipping.

### 16.5.0 (September 2026) — current
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
- Added "Current firmware: 16.5.0" to meta-info on all 59 documentation pages

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

### 2026-09-18 (P0 + P1 - audit v4 closeout)
- **P0.1** Compliance: Article 47 -> Article 77 (Digital Battery Passport, applicable from 18 February 2027 per Regulation EU 2023/1542). Article 47 defines the due-diligence chapter scope, not the passport itself. Fixed on /compliance/ and /second-life-battery/regulations/
- **P0.2** Safety: "CE marking transferability" replaced with the actual mechanism under Reg 2023/1542 Art. 45 (repurposing/remanufacturing operator obligations) and Art. 77 (Digital Battery Passport). Regulatory status of the repurposed battery must be assessed for the specific product and economic operator
- **P0.3** Getting Started: Nissan Leaf and Renault Zoe classification corrected - HV whole pack (~350-360 V) is the primary route; module-reconfigured 48 V LV bank is a separate DIY route (not the default)
- **P0.4** Tesla + SOFAR integration: 4.05 V/cell taper threshold now correctly split by chemistry - NCA/NMC packs use ~4.05 V/cell taper, LFP packs use ~3.45 V/cell taper (3.65 V max). Applying NCA threshold to LFP under-utilises the pack; applying LFP threshold to NCA risks over-charge
- **P0.5** Tesla + SOFAR: added per-variant compatibility table (Model 3 LR NCA / SR+ NCA / SR+ LFP / Highland LR) with chemistry, topology, voltage, firmware and verification status
- **P0.6** Compatibility Matrix: reworded from "every row tested" to accurate verification level breakdown. Added Verification levels section documenting Field tested / Bench tested / Protocol verified / Engineering validated
- **P0.7** Inverters page: neutralised marketing language - "premium tier" and "best price/performance" replaced with factual descriptions
- **P0.8** Safety cooling: universal "safe at 0.3 C" replaced with pack-specific engineering recommendation subject to validation
- **P0.9** Safety: "All original EV BMSes implement cell balancing" softened to "Many EV BMS architectures implement cell balancing; strategy and thresholds are manufacturer- and pack-specific"
- **P0.10** IMD thresholds (500 Ω/V warning, 100 Ω/V trip) presented as BMS-EV design thresholds, not universal industry standard
- **P1.11** Megger 500/1000 V - added explicit warning: do not apply insulation-test voltage unless OEM permits that test voltage and configuration
- **P1.12** Safety enclosure specs (1.5 mm steel, 60 min fire, 200 cm2 vent, H2/CO 500 ppm) - each marked as BMS-EV engineering recommendation with source/jurisdiction context
- **P1.13** EN 62619 sect 8 enclosure - marked as BMS-EV engineering interpretation
- **P1.14** ASIL C/D universal claim removed - replaced with "functional-safety frameworks such as ISO 26262; applicable ASIL classification is manufacturer- and function-specific"
- **P1.15** "factory BMS holds manufacturer safety certificates" replaced with "original battery pack was developed and validated as part of the vehicle OEM safety architecture"
- **P1.16** CAN 125 kbps K-line replacement categorical claim softened
- **P1.20** Homepage 70-90 percent capacity claim now sourced (Recurrent Auto 2025, Geotab 2023) with variability disclaimer
- **P1.21** Getting Started prices - full methodology added: sample size, sources, country, date range, VAT/shipping treatment, nominal vs usable capacity basis
- **P1.23** Compliance EN 62619 "interoperability" replaced with "applicable safety requirements of industrial secondary lithium battery systems; applicability to complete reused ESS depends on system architecture and conformity assessment"
- **P1.24** Safe-language audit - marketing terms like "safest way", "safer than", "guarantees safety" replaced with neutral technical language (retains, provides, monitors, limits, fails open, is designed to, was validated)

### 2026-09-19 (audit v5 P0 closeout — 18 blockers resolved)
- P0-1 Tesla Model 3 LFP operating voltage unified to 265-387 V (was 212-383 V in 3 places, mathematically inconsistent with LFP cell 2.5 V minimum)
- P0-2 Nissan Leaf CAN bus corrected to 500 kbps (was 250 kbps in one place on can-bus page)
- P0-3 Renault Zoe Gen2 (ZE50) chemistry corrected in header table: LG Chem NCM 712 pouch (not CATL LFP as previously stated) + Gen1 41 kWh voltage unified to 360 V nominal
- P0-4 Stellantis eCMP cell config unified to 108s2p across page (was 96s in body)
- P0-5 + P0-6 Hyundai/Kia E-GMP: removed unsupported 216s / 587 V claim (mathematically impossible 216x3.63=784V) and unsupported 96s regional variant claim (no public teardown source); large-pack claims flagged NEEDS VERIFICATION
- P0-7 Tesla Model 3 contactor architecture unified: the Tesla OEM BMS owns contactor and precharge sequencing internally, BMS-EV signals via CAN only. Removed 3 contradictory statements on the same page.
- P0-8 VW MEB CAN IDs 0x1A5555xx flagged NEEDS VERIFICATION (extended 29-bit format not documented in public MEB teardowns)
- P0-9 Nissan Leaf CAN IDs relabeled as telemetry frames + wake-frame reference added with dalathegreat source link
- P0-10 Shop bms-ev.com page 168016: all "80+ battery" and "60+ inverter" references replaced with canonical 73 battery profiles / 56 hybrid inverter variants (5 replacements)
- P0-11 Shop: "batteries themselves are automotive-grade with certification" universal safety claim replaced with per-standard OEM validation description + system-level ESS compliance disclaimer
- P0-12 SOFAR HYD channel count split per model: 5/6/8KTL = 1 channel; 10/15/20KTL = 2 channels, per official SOFAR datasheet V5.2 2024
- P0-13 Deye SUN HP3 DC input range unified per model across pages: 5-25K = 160-700 V (datasheet 2023-07-24); 29.9-50K = 160-800 V (approved battery list DY-HV(160-800)-028)
- P0-14 SOFAR HYD DC range corrected to 180-800 V (was 180-750 V on 2 pages, per SOFAR datasheet)
- P0-15 ISO 26262 ASIL C/D blanket claim softened: per-function classification varies by OEM and safety goal
- P0-16 Structured data JSON-LD (TechArticle + Product + Dataset) added to 20 authority pages (11 battery + 9 inverter)
- P0-17 batteries.csv (74 lines) and inverters.csv (57 lines) generated on docs.bms-ev.com/data/, GitHub repos synced
- P0-18 Sitemap.xml lastmod refreshed to 2026-09-19 across all URLs
- llms.txt updated with canonical CSV links section

### 2026-09-19 (audit v5 P1 closeout - 12 items)
- P1-1 Alternatives page rewritten: removed all five "time to working system" estimates for third-party projects (Battery-Emulator, Batrium, Orion BMS 2, SimpBMS, REC BMS) and the "hours, not weeks" / "No 500-hour bring-up" framing. Replaced the comparison row with three objective attributes (firmware pre-configured y/n, cell-tap wiring required y/n, source code public y/n). Added primary-source links for every listed project and a vendor-authored-comparison disclosure note.
- P1-2 Marketing superlatives removed across 24 pages: "most widely available", "most abundant", "most accessible", "best-engineered", "unusually well suited", "one of the cleanest", "most popular", "most economical", "most stable", "first mass-produced", "better than any other", "best value", "best fit", "best balance", "cheapest", "widest". Each replaced with a factual or sourced statement.
- P1-3 Part number data surfaced via new /part-numbers/ page generated from compatibility.csv
- P1-4 New authority page /batteries/bmw-ix-i4/ for the BMW Gen5 eDrive family (iX, i4, i5, i7). Per-model voltages sourced (iX xDrive40 ~330 V; i4 ~430 V nominal, 400-477 V band) rather than a single platform figure. Unverified fields explicitly marked NEEDS VERIFICATION.
- P1-6 New /case-studies/ page: Kia EV6 + SOFAR HYD 15KTL documented as the one field-verified deployment with PV Magazine Deutschland coverage, plus the full list of 22 battery + inverter pairs in production deployment (17 battery families). Unit counts and customer locations deliberately omitted per customer confidentiality.
- P1-7 New /research/ page: field-data programme methodology, 18-field data schema, anonymisation policy (no identifiers, climate zone not country, month granularity, minimum subgroup size 5), declared limitations including self-selection bias and vendor-run-study conflict of interest. No dataset published yet - methodology only.
- P1-8 New /part-numbers/ page generated from compatibility.csv: 42 of 73 battery profiles have a documented OEM part number family; the other 31 are explicitly marked NEEDS VERIFICATION rather than guessed.
- P1-9 12 new integration guides created for previously uncovered battery families: Renault Zoe x 4 inverters, Stellantis e-CMP x 3, MG 4 x 3, BYD Atto 3 x 2. Each carries verified inverter DC windows, pack architecture, contactor architecture and family-specific limitations.
- P1-10 Safety page: BMW i3 R1234yf refrigerant cooling separated from glycol-water cooled packs (Tesla, MEB, E-GMP, Audi e-tron). Different failure modes and different stationary-reuse options.
- P1-11 Safety page: cell absolute protection trip (around 4.25 V NMC/NCA, 3.65 V LFP) explicitly separated from charge taper threshold (around 4.05-4.20 V NMC/NCA, 3.45 V LFP), with a warning not to configure an inverter using a protection figure as a charge target.
- P0-13 follow-up: 11 further Deye "160-500 V" references corrected across nissan-leaf-deye and vw-meb. The SG04LP1/SG04LP3 families were also mislabelled as HV - they are 48 V low-voltage products and are now shown as such.
- Solis battery window corrected from 90-500 V to 120-500 V on 3 pages per solisinverters.com datasheet.
- "300+ controllers delivered" now states the counting basis: cumulative across all sales channels since 2024 (webshop, marketplaces, direct and B2B/distributor), because webshop order history alone does not reflect that total.
- llms.txt: DIY BMS comparison neutralised (removed "50-500 hours of configuration", "faster to install (hours vs weeks)", "safer (manufacturer safety certificates preserved)"), replaced with an architectural description.

### 2026-09-19 (inverter DC window verification pass)
- SolaX X3-Hybrid G4 confirmed at 120-800 V from the official solaxpower.com datasheet (text-extracted, not inferred). Corrected 90-800 V references on 5 pages.
- SolaX X1-Hybrid G4 corrected from 90-500 V to 80-480 V per SolaX support documentation. The official X1 datasheet PDF is a scanned image with no extractable text, so the support-article figure is cited rather than a guessed value.
- FoxESS H3 Smart corrected from 90-500 V to 80-500 V per fox-ess.com.
- Remaining Deye SG04LP1/SG04LP3 references corrected: these are 48 V low-voltage products, previously shown with HV battery windows.

### 2026-09-19 (audit round 6 - Deye phase/voltage + Tesla LFP topology)

P0 - corrected against official manufacturer datasheets (text-extracted, not inferred):
- **Deye SG01HP3-EU-AM2 is THREE-PHASE, not single-phase.** The datasheet title reads "Three Phase Hybrid Inverter", Grid Type is "Three Phase" and output is 3L/N/PE 220/380, 230/400 Vac. Docs previously listed the whole 5-20 kW range as 1P. Source: datasheet_sun-(5-25)k-sg01hp3-eu_230724_en.pdf
- **Deye AM2 battery voltage is 160-700 V, not 160-500 V.** Corrected in the direct answer, the DC-range list and the FAQ.
- **Deye AM2 model list corrected**: the range is 5/6/8/10/12/15/20/25 kW. Docs listed a non-existent 16K and omitted 15K and 25K.
- **Deye battery current separated from PV MPPT current.** The table column previously showed "2x 15 A" in a way that could be read as a battery-port limit. Battery current is 30 A (5/6/8K), 37 A (10/12K), 50 A (15/20/25K), one battery input. PV figures (2 MPP trackers, 150-850 V, 20+20 / 26+20 / 26+26 A) are now stated separately with an explicit note.
- **Deye BM3/BM4 has TWO battery inputs (50+50 A)**, not one - corrected, and the dual-pack FAQ answer updated accordingly.
- **Tesla Model 3 SR+ LFP topology corrected.** 106s1p means exactly 106 prismatic CATL BTF0 cells (161 Ah, 3.2 V), arranged as 2x 25s1p + 2x 28s1p modules. Docs previously stated "~3300 cells", "parallel count varies 26-32P" and "CATL 2170 cylindrical" - all three were wrong, apparently carried over from the cylindrical NCA architecture. Pack is 55 kWh total / 49.8 kWh usable at 339.2 V nominal. Sources: batterydesign.net Tesla LFP teardown; ScienceDirect cell teardown.
- **"All four Model 3 pack variants" replaced** with an explicit per-variant list including topology, on both the SOFAR and GoodWe integration pages.
- **Contactor architecture unified as pack-specific.** The safety responsibility table previously stated "Yes - 12 V coil driver" for BMS-EV contactor drive, while the Tesla page correctly stated the OEM BMS owns the sequence. A new section explains that OEM-sequenced packs (Tesla, E-GMP, BMW, Zoe via CMM) run the sequence in their own BMS and BMS-EV only requests it over CAN, whereas reconfigured-module builds need BMS-EV to sequence an external precharge circuit. Getting Started updated to match.

P1:
- "Every EV battery pack is designed as a floating (IT) system" softened to "Most high-voltage EV battery packs", with an instruction to verify the topology per pack.
- IMD threshold: "must alarm below 100 ohm/V (per IEC 61557-8)" replaced. 100 ohm/V is stated as the BMS-EV supported-system threshold; IEC 61557-8 is described as covering IMD device requirements, with the applied threshold a system design decision.
- Safety cable/fuse table marked "Illustrative engineering examples only - not installation instructions and not universal specifications", with cable cells shortened and a single cable-standard note below (H1Z2Z2-K for new work; PV1-F not recommended; H07RN-F is an AC cable).
- Porsche Taycan (J1) and Hyundai/Kia E-GMP split into separate table rows - they are different platforms with different voltages.
- Getting Started "standard practice" replaced with jurisdiction- and insurer-dependent wording.
- Compliance "may lawfully be repurposed for stationary storage" replaced with a framework statement plus the national requirements that also apply.
- Homepage life claim split into Observed (fleet studies) and Modelled (BMS-EV projection with stated duty assumptions), linking to /research/.
- compatibility.json and compatibility.csv: 1507 rows with verification_type in_catalog or empty are now explicitly engineering_validated. The dataset meta publishes the four-class vocabulary, definitions and per-class counts (2 field_verified, 2306 protocol_verified, 1507 engineering_validated).
- Kia EV6 806 V full-charge figure marked as calculated (192 x 4.2 V) rather than measured, on both the case study and the E-GMP battery page.
