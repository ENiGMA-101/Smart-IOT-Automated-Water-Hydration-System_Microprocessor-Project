# Smart IoT Automated Water Hydration System (ESP32)

An ESP32-based automated plant hydration (irrigation) system that monitors environmental and soil conditions and controls a water pump and a protective shed/cover. It integrates with **Blynk IoT** for live monitoring, manual control, and event notifications.

## Features

- **Soil moisture monitoring** (capacitive analog sensor)
- **Water tank level monitoring** (HC-SR04 ultrasonic distance sensor)
- **Temperature & humidity monitoring** (DHT sensor)
- **Rain detection** (digital rain sensor)
- **Automatic pump control** using sensor logic + safety cutoff
- **Servo-controlled shed/cover** that closes automatically when it’s raining
- **Blynk IoT dashboard**
  - Live sensor telemetry
  - Manual pump ON/OFF override
  - Manual servo angle control
  - Event logs (pump started/stopped)

## Hardware Components

- ESP32 development board
- HC-SR04 Ultrasonic Sensor (water level distance)
- DHT sensor (configured as **DHT11** in code; can be changed if using DHT22)
- Capacitive Soil Moisture Sensor (analog)
- Rain Sensor (digital, active-low)
- Servo motor (shed/cover)
- 2-channel low-trigger relay module (pump control uses 1 channel)
- Water pump + tubing
- Power supply suitable for pump + ESP32 (with common ground)

## Pin Mapping (ESP32)

| Module | Signal | ESP32 Pin |
|---|---:|---:|
| Ultrasonic | TRIG | 22 |
| Ultrasonic | ECHO | 23 |
| DHT | DATA | 4 |
| Soil Moisture | AO | 34 |
| Rain Sensor | DO | 15 |
| Servo | PWM | 12 |
| Relay (Pump) | IN | 21 |
| Status LED | LED | 2 |

## How It Works (Control Logic)

Every 5 seconds the ESP32:
1. Reads:
   - Tank distance (cm) from ultrasonic sensor
   - Temperature (°C) and humidity (%) from DHT
   - Raw soil moisture ADC value
   - Rain sensor digital state
2. Sends readings to Blynk virtual pins.
3. Controls the shed servo:
   - **Raining → CLOSE** (default close angle: 90°)
   - **Not raining → OPEN** (default open angle: 0°)
   - If you manually move the servo from Blynk, it stops auto-control until reset/restart.
4. Controls the pump:
   - If **tank is low**, pump is disabled and forced OFF.
   - Otherwise, pump turns ON when:
     - Soil is dry **AND**
     - (Temperature is high **OR** Humidity is low)
     - AND there is no manual override active
   - Pump runs for a fixed duration (**10 seconds**) then turns OFF automatically.

## Thresholds (Current Code Defaults)

You can tune these in `ProjectCode.ino`:

- `TEMP_THRESHOLD = 30.0 °C`
- `HUMIDITY_THRESHOLD = 40.0 %`
- `SOIL_THRESHOLD_RAW = 2000` (higher raw value means “drier” for many sensors)
- `WATER_LEVEL_DISTANCE_THRESHOLD = 12.0 cm`  
  (distance > threshold indicates tank is low, depending on your tank geometry)
- `PUMP_RUNTIME_MS = 10000` (10 seconds)

## Blynk Setup

The sketch uses Blynk IoT with these virtual pins:

| Blynk Virtual Pin | Purpose |
|---|---|
| V0 | Temperature |
| V1 | Soil raw value |
| V2 | Water distance (cm) |
| V3 | Rain status |
| V4 | Pump control (button) |
| V5 | Servo angle (slider) |
| V6 | Humidity |

### Notes
- You must create a Blynk Template and match the **Template ID / Auth Token**.
- The code currently contains Wi‑Fi credentials and a Blynk token directly in the sketch. For safety, rotate these if the repo is shared.

## Software Requirements

- Arduino IDE (or PlatformIO)
- ESP32 board support installed
- Libraries:
  - `WiFi.h` (ESP32 core)
  - `BlynkSimpleEsp32.h` (Blynk library)
  - `DHT.h` (Adafruit DHT sensor library)
  - `ESP32Servo.h`

## How to Run

1. Open `ProjectCode.ino` in Arduino IDE.
2. Install required libraries.
3. Update:
   - Wi‑Fi SSID/password
   - Blynk template/auth values
   - Sensor type if needed (DHT11 vs DHT22)
4. Select your ESP32 board + COM port.
5. Upload to ESP32.
6. Open Serial Monitor at **115200 baud** to view debug logs.
7. Use the Blynk app/web dashboard to monitor and control the system.

## Project Files

- `ProjectCode.ino` — main ESP32 firmware (sensors, control logic, Blynk)
- `Smart_IOT_Automated_Water_Hydration_System_Microprocessor_Project.pdf` — project documentation/report
- `LICENSE` — MIT License

## Safety & Reliability Tips

- Use a proper power supply for the pump and isolate/relay appropriately.
- Ensure **common ground** between ESP32 and relay input side (as required by your relay module).
- Consider adding:
  - Pump dry-run protection (flow sensor or current sensing)
  - Debounce/filtering for noisy sensors
  - Calibration mapping for soil sensor (raw → % moisture)

## License

MIT License (see `LICENSE`).
