# GrainGuard V1.1 — Known Limitations

- One DS18B20 measures one point; grain stores have spatial gradients.
- SHT31 ambient RH is not grain moisture content.
- SCD40 CO2 trends are not a validated mould, insect or aflatoxin diagnosis.
- Firmware emits grain moisture as null by design.
- Sensor data must be calibrated and compared with reference methods.
- Ventilation advice must abstain without crop-specific EMC data and independently measured grain moisture.
- Firmware has no fan, heater or auger actuation.
- BLE/USB and website ingestion require testing with the actual board, browser, phone/PC and breakouts.
- No field trial, food-safety validation, regulatory approval or certification is claimed.
