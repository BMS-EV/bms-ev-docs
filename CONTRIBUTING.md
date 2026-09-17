# Contributing to BMS-EV Documentation

Thanks for wanting to help improve BMS-EV documentation.

## Types of contributions welcome

### 1. Report an integration that works (but isn't documented)

If you've successfully installed a BMS-EV controller with a battery + inverter combination that isn't in our [Compatibility Matrix](https://docs.bms-ev.com/compatibility/), please [open an issue](https://github.com/BMS-EV/bms-ev-docs/issues/new) with:

- Battery pack (make, model, kWh, year)
- Hybrid inverter (make, model, phase, kW)
- BMS-EV Controller firmware version
- Photos of installation (optional)
- Runtime data (SOC/SOH, throughput, uptime) if available

We'll verify and add to the matrix.

### 2. Report a compatibility issue

If a documented pairing doesn't work as expected in your setup, [open an issue](https://github.com/BMS-EV/bms-ev-docs/issues/new) with:

- Battery + inverter + firmware version
- Symptom (won't wake, wrong SOC, CAN timeout, contactor doesn't close, etc.)
- Error codes from BMS-EV controller
- CAN trace if available (Kvaser, PCAN, CANable dump)

### 3. Improve documentation

Documentation is in `/docs/` (Markdown source) and mirrored on [docs.bms-ev.com](https://docs.bms-ev.com/). Corrections, clarifications, and additional examples welcome via Pull Request.

### 4. Suggest new battery or inverter

Want us to add support for a new EV or inverter? [Open an issue](https://github.com/BMS-EV/bms-ev-docs/issues/new) with:

- Vehicle/inverter identification
- Availability on the used market (for batteries)
- Volume of interest (existing installer partners, community demand)

We prioritize based on real-world usage.

## Documentation standards

When submitting documentation changes:

- **Concrete data** — voltages, currents, kbps, CAN IDs, standard clause numbers
- **No marketing language** — "market-leading", "best-in-class" is out
- **Cite sources** — for manufacturer specs, cite the datasheet; for standards, cite the section
- **Tables for compatibility** — human-readable + machine-parseable
- **ASCII diagrams** for architecture — render in any text viewer

## What we don't accept

- **Firmware modifications** — controller firmware is proprietary
- **DIY hardware clones** — hardware design is proprietary
- **Reverse-engineered proprietary data** without manufacturer permission
- **Marketing claims about competitors** — factual comparison only ([alternatives page](https://docs.bms-ev.com/alternatives/))

## Contact

- **Issues:** https://github.com/BMS-EV/bms-ev-docs/issues
- **Email:** office@bms-ev.com
- **WhatsApp:** +48 506 112 993

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
