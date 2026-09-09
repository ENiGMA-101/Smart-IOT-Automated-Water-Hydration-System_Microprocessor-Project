<div align="center">

# 💧 Smart IoT Automated Water Hydration System

### 🌱 Intelligent Plant Hydration & Environmental Monitoring using ESP32 + Blynk IoT

<p>
  <img src="https://img.shields.io/badge/ESP32-IoT-000000?style=for-the-badge&logo=espressif" alt="ESP32">
  <img src="https://img.shields.io/badge/C%2B%2B-Arduino-00599C?style=for-the-badge&logo=cplusplus" alt="C++">
  <img src="https://img.shields.io/badge/Blynk-IoT-23C48E?style=for-the-badge" alt="Blynk">
  <img src="https://img.shields.io/badge/Embedded-Systems-6C63FF?style=for-the-badge" alt="Embedded Systems">
  <img src="https://img.shields.io/badge/Project-Microprocessor-orange?style=for-the-badge" alt="Academic Project">
</p>

<p>
  <strong>
    An ESP32-powered smart hydration system that monitors soil,
    water level, temperature, humidity and rain conditions,
    then automatically controls irrigation while providing
    real-time IoT monitoring through Blynk.
  </strong>
</p>

<p>
  <a href="#-project-overview">Overview</a> •
  <a href="#-features">Features</a> •
  <a href="#-how-it-works">How It Works</a> •
  <a href="#-system-architecture">Architecture</a> •
  <a href="#-hardware">Hardware</a> •
  <a href="#-software">Software</a> •
  <a href="#-setup">Setup</a> •
  <a href="#-contributors">Contributors</a>
</p>

</div>

---

## 🎬 Project Overview

<!--
Add your project GIF here.

Recommended:
assets/project-demo.gif
-->

<div align="center">

### 🚀 Live Project Demonstration

<!-- Add GIF here -->

</div>

<br>

<!--
Add your project video here later.

You can use:
- YouTube thumbnail
- GitHub video
- MP4 hosted externally
-->

<div align="center">

### 🎥 Hardware Demonstration

<!-- Add your video here -->

</div>

---

## 📌 Project Overview

The **Smart IoT Automated Water Hydration System** is an ESP32-based
smart irrigation and environmental monitoring project designed to
automatically manage plant hydration according to real-time
environmental and soil conditions.

The system combines multiple sensors with automated decision-making,
a water pump, a servo-controlled protective cover, and **Blynk IoT**
to create a connected smart hydration solution.

The ESP32 continuously monitors:

- 🌡️ Temperature
- 💧 Humidity
- 🌱 Soil moisture
- 🚰 Water tank level
- 🌧️ Rain condition

Based on these readings, the system can automatically:

- Control the water pump
- Prevent pumping when the water tank is low
- Open or close the protective shed
- Respond to environmental conditions
- Send live sensor information to Blynk
- Allow manual control through the IoT dashboard

---

# ✨ Features

| Feature | Description |
|---|---|
| 🌱 Soil Monitoring | Measures soil moisture using a capacitive sensor |
| 🚰 Water Level Monitoring | Measures tank level using HC-SR04 |
| 🌡️ Temperature Monitoring | Reads environmental temperature |
| 💧 Humidity Monitoring | Measures environmental humidity |
| 🌧️ Rain Detection | Detects rainfall using a digital rain sensor |
| 💦 Automatic Irrigation | Controls the water pump according to conditions |
| 🛑 Low Water Protection | Prevents pump operation when tank level is low |
| 🏠 Smart Protective Cover | Servo automatically closes during rain |
| 📱 Blynk IoT | Remote monitoring and control |
| 🔄 Manual Override | Allows manual pump and servo control |
| 📊 Live Telemetry | Sends sensor data to Blynk |
| 🔔 Event Monitoring | Tracks pump start/stop events |
| ⚡ ESP32 Control | Central embedded controller |

---

# 🧠 Core Concept

```text
                   ┌──────────────────────┐
                   │       ESP32          │
                   │   Main Controller    │
                   └──────────┬───────────┘
                              │
        ┌─────────────────────┼──────────────────────┐
        │                     │                      │
        ▼                     ▼                      ▼
 ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
 │ Soil Sensor │       │ DHT Sensor  │       │ Rain Sensor │
 └──────┬──────┘       └──────┬──────┘       └──────┬──────┘
        │                     │                      │
        └─────────────────────┼──────────────────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │ Decision Making  │
                    │   & Monitoring   │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              │                             │
              ▼                             ▼
       ┌──────────────┐              ┌──────────────┐
       │ Water Pump   │              │ Servo Cover  │
       └──────────────┘              └──────────────┘
              │                             │
              └──────────────┬──────────────┘
                             ▼
                    ┌──────────────────┐
                    │    Blynk IoT     │
                    │ Dashboard / App  │
                    └──────────────────┘
