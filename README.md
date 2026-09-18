# BMS-EV Documentation

**Technical documentation for BMS-EV controllers** — enabling complete electric vehicle battery packs from Tesla, BMW, Nissan, Volkswagen, Hyundai, Kia, Renault, Stellantis, BYD, MG, Ford, Volvo, Polestar and others to be reused as **stationary home energy storage** with hybrid solar inverters.

> **Full docs:** [docs.bms-ev.com](https://docs.bms-ev.com/) · **Shop:** [bms-ev.com](https://bms-ev.com/) · **Contact:** office@bms-ev.com

---

## What is BMS-EV?

BMS-EV is a controller platform that:

- **Retains the original vehicle BMS** — cell balancing, protection, and thermal management continue to be handled by the manufacturer's own safety architecture
- **Wakes and keeps the BMS alive** outside the vehicle via emulated ECU signals
- **Translates CAN protocol** from the vehicle's native format to the hybrid inverter's expected protocol (Pylontech, BYD Battery-Box, native Deye/SolaX/Sungrow/GoodWe, SMA BAT-CAN, Fronius Solar Battery, KOSTAL Smart Battery)
- **Controls contactors and precharge** sequencing for high-voltage packs

```
┌────────────────────┐    ┌────────────────────┐    ┌────────────────────┐
│   EV battery pack  │    │  BMS-EV Controller │    │  Hybrid inverter   │
│   Original BMS ──► │CAN │  Protocol bridge ──►│CAN │  Reads SOC, V, I,  │
│   (Tesla, BMW,     │    │                    │    │  T, limits         │
│    VW MEB, etc)    │    │                    │    │  (Deye, SOFAR,     │
│                    │    │                    │    │   GoodWe, SMA...)  │
└────────────────────┘    └────────────────────┘    └────────────────────┘
```

## Coverage

| Metric | Value |
|--------|-------|
| **EV battery pack variants supported** | 72 |
| **Hybrid inverter models supported** | 56 |
| **Pre-configured combinations** | 3,815 |
| **Controllers delivered** | 300+ (since 2024) |
| **Shop languages** | 26 |

## Quick Links

### Documentation
- 📊 [**Compatibility Matrix**](https://docs.bms-ev.com/compatibility/) — 73 battery pack variants × 56 inverter variants, filter by voltage range and CAN protocol
- 🚀 [**Getting Started**](https://docs.bms-ev.com/getting-started/) — how EV battery reuse works, what to buy
- 🔒 [**Safety Architecture**](https://docs.bms-ev.com/safety/) — HV isolation, precharge, HVIL, standards
- 💡 [**Alternatives**](https://docs.bms-ev.com/alternatives/) — BMS-EV vs Battery-Emulator, Batrium, Orion BMS 2, SimpBMS, REC
- 📜 [**Compliance**](https://docs.bms-ev.com/compliance/) — CE, RoHS, EU Batteries Regulation 2023/1542

### Battery Reference Pages
- [Tesla Model 3 / Model Y](https://docs.bms-ev.com/batteries/tesla-model-3/) — 50/60/75/82 kWh, NCA/LFP
- [Tesla Model S / Model X](https://docs.bms-ev.com/batteries/tesla-model-s/) — 60/75/85/90/100 kWh, NCA
- [BMW i3](https://docs.bms-ev.com/batteries/bmw-i3/) — 22/33/42 kWh (60/94/120 Ah), NMC
- [Nissan Leaf](https://docs.bms-ev.com/batteries/nissan-leaf/) — 24/30/40/62 kWh, NMC
- [Volkswagen MEB](https://docs.bms-ev.com/batteries/vw-meb/) — 48-82 kWh (ID.3/ID.4/Skoda Enyaq/Audi Q4/Cupra Born/Ford Explorer)
- [Hyundai/Kia E-GMP](https://docs.bms-ev.com/batteries/hyundai-kia-egmp/) — 58.2/72.6/77.4 kWh (Ioniq 5/6, EV6, EV9)
- [Renault Zoe](https://docs.bms-ev.com/batteries/renault-zoe/) — 22/41/52 kWh (Gen1 NMC, Gen2 LFP)
- [Stellantis CMP](https://docs.bms-ev.com/batteries/stellantis-cmp/) — Peugeot, Citroen, Opel, Fiat, Toyota Proace Electric
- [BYD Atto 3 / Yuan Plus](https://docs.bms-ev.com/batteries/byd-atto-3/) — 50/60 kWh Blade LFP
- [MG 4](https://docs.bms-ev.com/batteries/mg-4/) — 51/64 NMC, 77 LFP Trophy
- [Ford Mustang Mach-E](https://docs.bms-ev.com/batteries/ford-mustang-mach-e/) — 68/88/98 kWh
- [All 73 battery pack variants](https://docs.bms-ev.com/batteries/)

### Inverter Reference Pages
- [Deye SUN HP3](https://docs.bms-ev.com/inverters/deye/) — 5-50 kW hybrid, single- and three-phase
- [SOFAR HYD](https://docs.bms-ev.com/inverters/sofar/) — 3-20KTL-3PH
- [GoodWe](https://docs.bms-ev.com/inverters/goodwe/) — EH, ET, ES, EHB, BH, BT, A-ES families
- [SolaX](https://docs.bms-ev.com/inverters/solax/) — X1 Hybrid, X3 Hybrid G4, X3-Ultra
- [SMA](https://docs.bms-ev.com/inverters/sma/) — Sunny Boy Storage, Sunny Boy Smart Energy, Sunny Tripower X
- [Fronius](https://docs.bms-ev.com/inverters/fronius/) — Primo/Symo Gen24 Plus, Verto Plus
- [Sungrow](https://docs.bms-ev.com/inverters/sungrow/) — SH RS/RT/T series
- [Solis](https://docs.bms-ev.com/inverters/solis/) — RHI, S5, S6 series
- [FoxESS](https://docs.bms-ev.com/inverters/foxess/) — H1/AC1, H3/AC3, H3 Smart/Pro
- [All 56 inverters](https://docs.bms-ev.com/inverters/)

### Popular Integration Guides

| Battery | Compatible inverters |
|---------|---------------------|
| **Tesla Model 3/Y** | [SOFAR](https://docs.bms-ev.com/integrations/tesla-model-3-sofar/), [Deye](https://docs.bms-ev.com/integrations/tesla-model-3-deye/), [GoodWe](https://docs.bms-ev.com/integrations/tesla-model-3-goodwe/), [SolaX](https://docs.bms-ev.com/integrations/tesla-model-3-solax/), [SMA](https://docs.bms-ev.com/integrations/tesla-model-3-sma/), [Fronius](https://docs.bms-ev.com/integrations/tesla-model-3-fronius/), [Sungrow](https://docs.bms-ev.com/integrations/tesla-model-3-sungrow/), [Solis](https://docs.bms-ev.com/integrations/tesla-model-3-solis/), [FoxESS](https://docs.bms-ev.com/integrations/tesla-model-3-foxess/), [Kostal](https://docs.bms-ev.com/integrations/tesla-model-3-kostal/) |
| **BMW i3** | [Deye](https://docs.bms-ev.com/integrations/bmw-i3-deye/), [SOFAR](https://docs.bms-ev.com/integrations/bmw-i3-sofar/), [GoodWe](https://docs.bms-ev.com/integrations/bmw-i3-goodwe/), [SolaX](https://docs.bms-ev.com/integrations/bmw-i3-solax/), [SMA](https://docs.bms-ev.com/integrations/bmw-i3-sma/), [Fronius](https://docs.bms-ev.com/integrations/bmw-i3-fronius/) |
| **Nissan Leaf** | [Deye](https://docs.bms-ev.com/integrations/nissan-leaf-deye/), [SOFAR](https://docs.bms-ev.com/integrations/nissan-leaf-sofar/), [GoodWe](https://docs.bms-ev.com/integrations/nissan-leaf-goodwe/), [SolaX](https://docs.bms-ev.com/integrations/nissan-leaf-solax/) |
| **VW MEB** | [Deye](https://docs.bms-ev.com/integrations/vw-meb-deye/), [SOFAR](https://docs.bms-ev.com/integrations/vw-meb-sofar/), [GoodWe](https://docs.bms-ev.com/integrations/vw-meb-goodwe/), [SMA](https://docs.bms-ev.com/integrations/vw-meb-sma/) |
| **Hyundai/Kia E-GMP** | [Deye](https://docs.bms-ev.com/integrations/hyundai-kia-deye/) |

### Second-Life Battery Knowledge Center
- [How it works](https://docs.bms-ev.com/second-life-battery/how-it-works/) — step-by-step guide, architecture diagram, power flow states
- [Cost breakdown](https://docs.bms-ev.com/second-life-battery/cost/) — €4000-8000 for 40-90 kWh, ROI analysis, TCO 10-year
- [Regulations](https://docs.bms-ev.com/second-life-battery/regulations/) — EU Batteries Regulation 2023/1542, national grid codes (DE/FR/IT/ES/NL/PT/BE/PL/UK), fire safety
- [EV Battery BMS explained](https://docs.bms-ev.com/second-life-battery/ev-battery-bms/) — factory BMS vs BMS-EV vs DIY BMS
- [CAN Bus Communication](https://docs.bms-ev.com/second-life-battery/can-bus/) — protocol translation, message IDs, timing

## Common Questions

### Can a Tesla Model 3 battery be used for home energy storage?

**Yes.** A complete Tesla Model 3 or Model Y battery pack can be reused as stationary energy storage with a compatible hybrid inverter (SOFAR HYD, Deye SUN HP3, GoodWe EH/ET, SolaX X3 Hybrid G4, SMA Sunny Tripower Smart, Fronius Symo Gen24 Plus, Sungrow SH RT). The original Tesla BMS is retained; a BMS-EV controller communicates with it over CAN (500 kbps) and translates the data to the hybrid inverter's expected protocol (typically Pylontech-derived, BYD Battery-Box, or a native protocol).

### Which controller connects a Tesla battery to a Deye inverter?

**BMS-EV Controller pre-configured for Tesla Model 3/Y + Deye SUN-(5-20)K-SG01HP3-EU-AM2** (single-phase 5–20 kW) or **SUN-(29.9-50)K-SG01HP3-EU-BM3** (three-phase 29.9–50 kW). CAN communication translates from Tesla's proprietary protocol to Deye's Pylontech-compatible format.

### Is BMS-EV safe? Does it replace the original vehicle BMS?

**BMS-EV does not replace the vehicle's battery management system.** The original BMS continues to handle cell balancing, over/undervoltage protection, thermal management, and contactor safety. The BMS-EV controller sits alongside the original BMS on the CAN bus, waking it, reading its data, and re-encoding it for the hybrid inverter. This preserves the manufacturer's engineered safety architecture — a critical advantage over DIY BMS replacements.

### How does BMS-EV differ from open-source alternatives?

| | BMS-EV | Battery-Emulator | Batrium | Orion BMS 2 | SimpBMS |
|---|---|---|---|---|---|
| Model | Commercial | Open source | Commercial | Aftermarket | Open source |
| Hardware | Dedicated | Multiple options | Dedicated LV | Universal EV | Universal |
| Original BMS retained | ✅ Yes | ✅ Yes | ❌ Replaced | ❌ Replaced | ❌ Replaced |
| Pre-configured | ✅ Yes (per pair) | Manual config | Manual config | 50+ hours config | 500+ hours dev |
| Warranty | 2 years | Community | 2 years | 2 years | None |
| Support | Manufacturer | Community | Manufacturer | Manufacturer | Community |
| Retail price | €500 | Free (DIY hw) | €800-1500 | €700-1200 | Free (DIY hw) |
| Time to working system | Hours | Days-weeks | Weeks | Weeks | Months |

Full comparison: [docs.bms-ev.com/alternatives/](https://docs.bms-ev.com/alternatives/)

## Data

- **[compatibility.csv](compatibility.csv)** — machine-readable database of 3,815 pre-configured battery × inverter combinations shipping today
- **[docs.bms-ev.com/sitemap.xml](https://docs.bms-ev.com/sitemap.xml)** — full sitemap
- **[docs.bms-ev.com/llms.txt](https://docs.bms-ev.com/llms.txt)** — LLM-friendly documentation index

## Contributing

Found an integration missing from the matrix? A battery generation we don't document? [Open an issue](https://github.com/BMS-EV/bms-ev-docs/issues) or contact office@bms-ev.com.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

Documentation licensed under [MIT License](LICENSE).

Product firmware and hardware designs are proprietary. BMS-EV Controller is a commercial product available at [bms-ev.com](https://bms-ev.com/).

## Contact

- **Shop:** https://bms-ev.com/
- **Documentation:** https://docs.bms-ev.com/
- **Email:** office@bms-ev.com
- **WhatsApp:** +48 506 112 993
- **Company:** Clima Boost Jakub Lipiński, Kościuszki 70A, 55-330 Lutynia, Poland (NIP: PL5971544886)

---

<sub>Featured in [PV Magazine Deutschland](https://www.pv-magazine.de/) · July 2026</sub>
