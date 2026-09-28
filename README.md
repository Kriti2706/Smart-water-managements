# 🌊 ESP32 Smart Water Management & Monitoring System

An automated, IoT-ready water management prototype built on an ESP32 microcontroller that dynamically monitors water storage levels using an HC-SR04 ultrasonic sensor, manages automated pump relay actuation, provides live telemetry on an I2C OLED display, and supports tactile manual override control.


## 📌 Project Overview

The system continuously monitors reservoir water levels in real time using high-frequency non-contact ultrasonic distance profiling.

When the liquid depth crosses the configured threshold levels:
Low Level Threshold:  < 20% (Trigger Pump ON)
High Level Threshold: >= 90% (Trigger Pump OFF)
the system:

1. Detects low water storage capacity.
2. Engages the relay to start the water pump.
3. Continuously streams real-time level percentages to the SSD1306 OLED display.
4. Illuminates diagnostic indicator LEDs to reflect active pump status.
5. Monitors high-level cutoffs to prevent reservoir overflow.
6. Automatically disengages the pump relay once the tank is safely filled.
7. Permits immediate operator intervention via a tactile manual override button.

---

## ⚙️ Main Features

* 💧 Non-contact ultrasonic liquid depth measurement
* 📈 Real-time water capacity calculation and volume percentage mapping
* ⚡ Autonomous relay-driven pump control (Anti-dry-run & overflow protection)
* 📺 Crisp 0.96" SSD1306 I2C OLED live telemetry display
* 🔘 Dedicated manual override push-button for emergency control
* 🟢 Real-time LED status diagnostics (Normal, Pumping, Alert)
* ⏱️ Non-blocking sensor polling and high-speed telemetry refresh
* 🌐 Built and verified with complete Wokwi virtual schematic simulation

---

## 🧩 Hardware Components

| Component | Purpose |
| :--- | :--- |
| ESP32 | Main micro-controller & control processing |
| HC-SR04 Ultrasonic Sensor | Non-contact liquid level & depth detection |
| 5V Relay Module | Automated AC/DC water pump switching |
| 0.96" I2C OLED (SSD1306) | Live local telemetry and state display |
| Push Button | Manual pump override control |
| Status LEDs (Green/Red) | Visual system operational status |
| Jumper Wires & Breadboard | System interconnects |
| Power Supply (5V/3.3V) | Core electronics power |

---
 ## 🔌 Pin Connections

### HC-SR04 Ultrasonic Sensor

| Ultrasonic Sensor | ESP32 |
| :--- | :--- |
| VCC | 5V |
| GND | GND |
| TRIG | GPIO 5 |
| ECHO | GPIO 18 |

### SSD1306 I2C OLED Display

| OLED Pin | ESP32 |
| :--- | :--- |
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |
I²C address used: 0x3C### Relay & Actuation

| Relay Pin | ESP32 |
| :--- | :--- |
| VCC | 5V |
| GND | GND |
| IN (Signal) | GPIO 4 |

### Manual Override Push Button

| Button Pin | ESP32 |
| :--- | :--- |
| Terminal 1 | GPIO 19 |
| Terminal 2 | GND |

*Note: The button utilizes the ESP32 internal pull-up resistor (`INPUT_PULLUP`).*

---

## 🧠 Water Level Calculation Logic

The HC-SR04 sensor measures the time of flight for ultrasonic sound pulses:Sound Speed = 0.0343 cm/µs
Distance (cm) = (Duration × 0.0343) / 2
Water depth and percentage are determined against the total tank depth:Water Depth = Total Tank Height - Measured Distance
Percentage (%) = (Water Depth / Max Tank Depth) × 100
### Automation & State MachineWater 

Percentage < 20%

↓
 Relay ON (Pump Starts)

↓

Status LED: Active / Filling

Water Percentage >= 90%

↓
 Relay OFF (Pump Stops)

↓
Status LED: Full / Standby

---

## 🔔 Manual Override Architecture

To ensure manual flexibility and maintenance safety, manual switching bypasses automatic thresholds without requiring a system restart.

When the button is pressed:
Button Pressed

↓

Toggle Current Pump State

↓

Update OLED Display to "MANUAL OVERRIDE"

↓

Lock Auto-Switching Until Released / Reset

---

## 🧪 Module Testing

Each hardware block was verified individually before combined integration:

* **OLED Test:** Runs I2C communication sweeps and tests screen buffer drawing.
* **Ultrasonic Distance Sweep:** Verifies sensor distance repeatability with millimeter accuracy.
* **Relay Actuation Test:** Confirms dynamic switching and protection against coil inductive kickback.
* **Button Debounce Verification:** Validates debounce logic to eliminate spurious pump switching signals.

---

## 📁 Repository Structure

```text
ESP32-Smart-Water-Management/
├── README.md
├── sketch.ino
├── diagram.json
├── wokwi-project.txt
├── docs/
│   ├── circuit-diagram.png
│   └── architecture-flowchart.png
└── LICENSE
⚠️ Prototype Disclaimer
This project is an academic simulation and prototyping system designed for water management automation.
In production environments dealing with mains AC high-voltage pump motors, opto-isolated relay modules, proper thermal heatsinking, contactor relays, and industrial IP67-rated waterproof ultrasonic sensors must be used in compliance with regional electrical safety standards.
