# GrainGuard — Adaptive Grain Preservation Platform

**Research prototype V1.0 | GitHub Pages-ready | Single-file front end + ESP32 firmware + optional Supabase**

GrainGuard explores a crop-aware grain-storage monitoring and decision-support system. It captures grain-mass temperature, ambient temperature/relative humidity and protected headspace CO2 trends, records crop and batch context, and provides conservative storage-condition indicators. A ventilation planner can evaluate a crop-specific equilibrium-moisture-content (EMC) table only when one is supplied and reviewed by a qualified specialist.

> **Important:** GrainGuard V1 is not a food-safety certification system, mycotoxin detector or autonomous grain aeration controller. It does not determine whether grain is safe to eat, sell or store. No fan/actuator output is implemented. The website's demo readings are synthetic and labelled.

## Contents

```text
.
├── index.html
├── README.md
├── LICENSE
├── SECURITY.md
├── CONTRIBUTING.md
├── .nojekyll
├── .github/workflows/pages.yml
├── assets/
│   └── grainguard-system.svg
├── hardware/
│   ├── GrainGuard_ESP32.ino
│   ├── README.md
│   ├── PROTOCOL.md
│   └── BOM.md
├── supabase/
│   ├── schema.sql
│   └── README.md
├── docs/
│   ├── 48-HOUR-HACKATHON-PLAN.md
│   ├── ARCHITECTURE.md
│   ├── INSTITUTIONAL-DEPLOYMENT.md
│   ├── OPERATOR-GUIDE.md
│   ├── ORIGINALITY-SCREEN.md
│   ├── RESEARCH-AND-LIMITATIONS.md
│   └── VALIDATION-PROTOCOL.md
└── .github/workflows/pages.yml
```

## Website features

- Dashboard and batch inventory
- USB Serial and BLE telemetry interfaces
- Separate physical, manual, laboratory and demo data labels
- ESP32 device status and JSONL telemetry parser
- Storage-condition indicators with visible evidence
- Crop guide references (historic FAO contextual figures, not regulatory limits)
- Crop-specific EMC table import and bilinear interpolation within the validated table domain; no extrapolation
- Ventilation decision support that refuses to advise with missing inputs; advisory only
- Open-Meteo geocoding and current weather integration
- Local-first storage, CSV and JSON export, print report
- Optional Supabase Auth and RLS-protected cloud tables
- Validation register, research dossier, potential partner pathways and limitations
- GitHub Pages Actions workflow

## Publish on GitHub Pages

1. Download/extract the release ZIP.
2. Upload the **contents** of the `grainguard-github` folder to the root of a GitHub repository (keep all folders).
3. Open repository **Settings → Pages**.
4. Set **Build and deployment → Source** to **GitHub Actions**.
5. Push to the `main` branch. The included workflow deploys `index.html` and the static files.

Hardware APIs such as Web Serial and Web Bluetooth generally require a secure context (HTTPS) and supported browser. USB Serial works best on Chromium desktop. Web Bluetooth is supported in compatible Chromium browsers, including many Android Chrome versions, but not all browsers/devices.

## Hardware quick start

See `hardware/README.md` and `hardware/BOM.md`. The target is ESP32 DevKit V1 with SHT31 ambient T/RH, SCD40 headspace CO2 and DS18B20 grain temperature. The sketch emits newline-delimited JSON over USB Serial and Nordic UART Service BLE.

V1 leaves `grain_moisture_pct` null by design. Use a crop-calibrated grain meter or laboratory method, then enter the result in the app. Do not treat generic soil probes or ambient RH as grain moisture.

## Optional Supabase integration

Run `supabase/schema.sql` in the Supabase SQL Editor. Then open **Settings & integrations** in the website and enter your project URL and anon/publishable key. Create or sign in with a Supabase Auth account.

Never embed a Supabase `service_role` or secret key in this static website. RLS must remain enabled. The supplied policies restrict records to the signed-in user; multi-organisation deployments need additional membership/role controls and a privacy review.

## Weather integration

Weather location lookup and current conditions use Open-Meteo public endpoints. Forecast data is contextual and must not be used as a substitute for on-site ambient sensors or validated EMC input.

## Research position

Grain monitoring, grain moisture/temperature sensing, storage alerts and automated aeration already exist commercially. Bin-Sense is one example: https://www.binsense.com/products/. GrainGuard does not claim those capabilities as novel. The technical hypothesis worth testing is a conservative, crop-specific EMC-aware intervention gate combined with condition trends, explicit uncertainty and refusal to issue a recommendation when critical information is missing.

See `docs/RESEARCH-AND-LIMITATIONS.md` and `docs/VALIDATION-PROTOCOL.md` before using outputs externally.

## External references

- FAO post-harvest losses: https://www.fao.org/4/x5065e/x5065E05.htm
- FAO storage fundamentals: https://www.fao.org/4/x5065e/x5065E04.htm
- FAO controlled ventilation: https://www.fao.org/4/x5065e/x5065E0a.htm
- FAO fungi and mycotoxins: https://www.fao.org/4/x5065e/x5065E0c.htm
- Bin-Sense existing product benchmark: https://www.binsense.com/products/
- Open-Meteo API: https://open-meteo.com/en/docs
- Supabase JS and RLS: https://supabase.com/docs/reference/javascript/installing

## Development status

This package is a source release prepared for prototype development. The HTML/JavaScript can be syntax-checked and deployed statically, but the ESP32 firmware must be compiled against installed library versions and tested on actual hardware. Sensor calibration, field trials, EMC table validation, institutional approval, food-safety testing and patent review remain outstanding.

## License

MIT for the original source code in this repository. Third-party libraries, sensor modules, standards and cited materials retain their own licenses/terms. The MIT license is not a certification or warranty of the physical instrument.

## Physical build and validation

- [Assembly guide](hardware/ASSEMBLY-GUIDE-V1.1.md)
- [Bill of materials and checklist](hardware/BOM-AND-TEST-CHECKLIST.md)
- [Field pilot protocol](docs/FIELD-PILOT-PROTOCOL.md)
- [Known limitations](docs/KNOWN-LIMITATIONS-V1.1.md)
