# GrainGuard Edge Node V1

Telemetry-only ESP32 starter firmware. It does not control a fan, heater, auger or other actuator.

## Tested design target

- ESP32 DevKit V1 / ESP32-WROOM-32
- SHT31 ambient temperature and relative humidity breakout
- SCD40 CO2 sensor in a protected, sampled headspace chamber
- DS18B20 temperature probe placed in a representative grain-mass location
- USB Serial JSON Lines at 115200 baud
- Nordic UART Service (NUS) BLE notifications

The sketch has been prepared against the listed Arduino libraries, but must be compiled against the exact installed board core and library versions before flashing. No physical board or sensor has been tested as part of this source-package build.

## Libraries

Install using Arduino Library Manager:

1. Adafruit SHT31 Library
2. Sensirion I2C SCD4x (current `SensirionI2cScd4x` API) and its Sensirion Core dependency
3. OneWire
4. DallasTemperature
5. ArduinoJson (version 7 compatible)
6. NimBLE-Arduino (2.x API for ESP32)

Select an ESP32 Dev Module board and the correct serial port. Build and inspect compile warnings before flashing.

## Wiring reference

| Module | ESP32 pin | Notes |
|---|---:|---|
| I2C SDA (SHT31 + SCD40) | GPIO 21 | Shared I2C bus; confirm addresses |
| I2C SCL (SHT31 + SCD40) | GPIO 22 | Shared I2C bus |
| DS18B20 data | GPIO 4 | 4.7 kΩ pull-up to 3.3 V is normally required |
| Common ground | GND | Common reference |
| Sensor supply | 3V3 / breakout VIN as specified | Check the exact module documentation first |

SHT31 commonly uses address 0x44; SCD40 uses 0x62. Confirm with an I2C scanner. Some breakout boards accept 5 V at VIN while bare sensor devices do not. ESP32 GPIOs are not 5 V tolerant. Never connect an unverified 5 V output to an ESP32 pin.

## Grain moisture

V1 intentionally emits `grain_moisture_pct: null`. Do not connect a generic soil-moisture probe and label its output as grain moisture. Use a crop-calibrated grain moisture meter or laboratory method and enter its value in the app with method, crop, moisture basis, sample ID and meter/calibration details. A future hardware integration requires a documented interface and crop-specific calibration.

## Placement

- Place SHT31 in a shaded, ventilated enclosure measuring store air, away from direct sunlight, rain and fan discharge.
- Place DS18B20 at a documented depth and location within the grain mass. A single probe cannot represent a large bin; use several locations for a serious pilot.
- Place SCD40 in a protected headspace sampling enclosure designed to avoid dust and condensation. Record airflow and sampling configuration. It is a trend sensor, not a mycotoxin detector.
- Keep electronics, exposed connectors and mains equipment physically separated from grain dust and operators.

## Safety

No fan relay or actuator output exists in this version. Do not add automatic aeration based on ambient RH alone. Any later actuator design requires a crop-specific equilibrium-moisture model, independent fail-safe review, electrical protection, operator override and controlled validation.

## Upstream API references

- Sensirion SCD4x Arduino library and current example: https://github.com/Sensirion/arduino-i2c-scd4x
- Adafruit SHT31 library: https://github.com/adafruit/Adafruit_SHT31
- NimBLE-Arduino API: https://h2zero.github.io/NimBLE-Arduino/
- DallasTemperature library: https://github.com/milesburton/Arduino-Temperature-Control-Library

## V1.1 physical build documents

- `ASSEMBLY-GUIDE-V1.1.md` — wiring, safe assembly and acceptance tests
- `BOM-AND-TEST-CHECKLIST.md` — bill of materials and commissioning checklist
- `../docs/FIELD-PILOT-PROTOCOL.md` — first controlled field pilot
- `../docs/KNOWN-LIMITATIONS-V1.1.md` — limitations and safety boundaries
