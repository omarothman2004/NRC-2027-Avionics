# NRC-2027-Avionics
This repository houses the payload telemetry electronics for UH Rocketry Club, as part of my team's entry for the 2027 UK National Rocketry Competition (NRC). 
# 🚀 NRC 2027 Avionics & Flight Computer Payload

![Build Status](https://img.shields.io/badge/KiCad-v10.0.8-blue)
![Platform](https://img.shields.io/badge/Hardware-Teensy%204.1-orange)
![License](https://img.shields.io/badge/License-MIT-green)


Designed and maintained by the **UH Rocketry Team**.

---

## 📌 System Architecture

The core electronics suite is built around a single-board **Teensy 4.1 (ARM Cortex-M7 @ 600 MHz)** powering real-time sensor polling, long-range RF transmission, and auxiliary recovery diagnostics.

### Primary Hardware Modules
* **Flight Processing Unit:** PJRC Teensy 4.1
* **Barometric Pressure & Altitude:** Bosch BMP390L ($I^2C$ `0x77`)
* **Inertial Measurement Unit (IMU):** MPU-6050 6-DOF ($I^2C$ `0x68`)
* **GPS Tracking:** u-blox NEO-M8N (UART `Serial1`)
* **Communication:** HopeRF RFM95W 868 MHz LoRa Transceiver (SPI0 + `DIO0`)
* **Power Regulation:** Microchip MIC5219-3.3 LDO (3.7V LiPo to $+3.3\text{V}$)
* **Rocket Alerts:** WS2812B RGB Status LED + Transistor-Driven 90dB Recovery Buzzer
* **Safety Isolation:** 2-Pin Arming Header / Jumper Circuit

---

## 📁 Repository Organization

| Directory | Description |
| :--- | :--- |
| `hardware/` | KiCad 9 schematic files, PCB layout, symbol libraries, and BOM spreadsheets. |
| `firmware/` | PlatformIO / C++ source code for sensor loops, data parsing, and telemetry transmission. |
| `docs/` | Presentation slides for Preliminary Design Review (PDR), sensor datasheets, and NRC rules. |
| `ground-station/` | Receiver scripts and serial monitor parsing tools for ground control tracking. |

---

## ⚡ Hardware Features & Enhancements (vs 2026 Baseline)
- **High-Frequency Motion Tracking:** Integrated 6-DOF IMU for acceleration and roll-rate diagnostics during motor burn.
- **Battery Monitoring:** Resistor divider network routing live supply voltage to Teensy ADC pin (`A0`).
- **Keyed Power Isolation:** External arming header to prevent battery drain and premature ejection power-ups.
- **Microsecond Data Sync:** Optional GPS `TIMEPULSE` (PPS) routing for atomic-clock synchronized telemetry logs.

---

## 🛠 Setup & Testing

### Prerequisites
* **KiCad 10.0+** (for editing PCB and schematic files)
* **VS Code + PlatformIO** or **Arduino IDE** with Teensyduino installed
* **TinyGPS++** & **RadioLib** libraries for standalone testing

### Quick Hardware Verification
1. Flash `firmware/test/imu_i2c_scan_test` to verify $I^2C$ address recognition (`0x77` BMP390, `0x68` MPU-6050).
2. Run `firmware/test/gps_standalone_test` outside with open sky access to verify satellite lock (9600 baud).

---

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.
