# Smart-water-managements
ESP32-based Smart Water Management System featuring automated pump control via relay, ultrasonic level sensing, OLED status display, and indicator LEDs. Includes Wokwi simulation diagram and firmware.

Unmonitored water storage systems frequently suffer from pump dry-running, electrical inefficiencies, and water overflow. To solve this, the Smart Water Management System provides closed-loop control over liquid reservoirs using an ESP32 microcontroller, continuously sampling water depth via an ultrasonic sensor and presenting live telemetry on an I2C OLED display.
The firmware processes data through threshold logic to automatically regulate the pump relay, preventing dry-running and overflow while eliminating manual intervention. For flexible operation, the circuit integrates tactile pushbuttons for manual override along with indicator LEDs for real-time status diagnostics.
Key Features:
 * Automated Level Detection: High-accuracy distance sensing using an HC-SR04 ultrasonic module.
 * Intelligent Pump Actuation: Relay-switched pump control to eliminate manual intervention and water wastage.
 * Live Telemetry: 0.96 inch I2C OLED display indicating real-time water percentage and pump status.
 * Manual Override and Indicators: Dedicated pushbuttons for emergency control and multi-color LEDs for instant status diagnostics.
 * Wokwi Simulation: Ready-to-run virtual schematic (diagram.json) for quick hardware-free testing.
   
