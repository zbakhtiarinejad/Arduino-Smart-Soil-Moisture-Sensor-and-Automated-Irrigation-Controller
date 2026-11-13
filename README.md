# Arduino Smart Soil Moisture Sensor & Automated Irrigation Controller

Traditional irrigation systems often waste large amounts of water due to rigid, timer-based schedules. This project uses an Arduino Uno combined with a soil moisture sensor and a relay module to monitor root-zone hydration in real-time and dynamically trigger a water pump only when soil moisture drops below a set threshold.
<img width="1087" height="631" alt="Screenshot 2026-11-12 163202" src="https://github.com/user-attachments/assets/8979c2f8-2528-400f-b216-6bda90829292" />

## Overview
This repository contains an automated soil moisture monitoring and smart irrigation system built and simulated in Tinkercad Circuits. The project demonstrates embedded systems fundamentals, analog-to-digital conversion, and relay-actuated control logic designed to optimize water conservation.


## System Architecture

| Component | Function |
| :--- | :--- |
| **Arduino Uno R3** | Central microcontroller processing sensor signals and executing control logic. |
| **Soil Moisture Sensor** | Measures volumetric water content via variable electrical resistance. |
| **Relay Module** | Acts as an isolated electronic switch to control higher-power actuators. |
| **Visual Indicators** | LEDs and the Serial Monitor provide live telemetry and system status feedback. |

## Firmware and Control Logic

The system continuously acquires data and applies real-time threshold decisions:

* **Data Acquisition:** Reads analog values from the soil moisture sensor connected to analog pin `A0`.
* **Telemetry:** Streams live readings to the Arduino Serial Monitor for debugging and performance tracking.
* **Actuation Logic:**
  * If moisture falls below the critical threshold ($< 100$), digital pin `8` is driven **HIGH**, activating the relay and pump circuit.
  * Otherwise, digital pin `8` remains **LOW** to conserve water and resources.

## Engineering Lesson: Pin Current Limits and Circuit Safety

During the development and testing phase of this circuit, an important hardware limitation was encountered regarding microcontroller pin specifications:

### The Issue
Initially, the power supply wire of the soil moisture sensor was connected directly to digital pin `D7` and set to `HIGH` in the firmware. The Tinkercad simulator triggered an immediate hardware warning:

> *Current through I/O pin(s) D7 ($28.6\text{ mA}$) exceeds the recommended maximum of $20.0\text{ mA}$. This may reduce the usable lifetime of the Arduino.*

### The Resolution
Digital I/O pins on microcontrollers like the ATmega328P are designed for logic signaling and data communication, not for supplying continuous operating current to external hardware modules. Drawing $28.6\text{ mA}$ exceeds the safe $20\text{ mA}$ per-pin threshold and risks thermal degradation of the chip.

To resolve this, the sensor power wire was re-routed to the dedicated **5V power supply pin** on the Arduino board. This draws stable power directly from the onboard voltage regulator, protecting the digital I/O pins and ensuring reliable long-term hardware operation.

## Future Enhancements
* **LCD Display Integration:** Add an I2C 16x2 display to render real-time moisture telemetry directly on the physical hardware setup.
* **Hysteresis Implementation:** Introduce software hysteresis to eliminate rapid relay chattering near the threshold boundary.

## Recent Updates
The firmware has been successfully upgraded from visual block-based programming to native Arduino C++ source code, improving code readability, execution control, and alignment with professional embedded engineering standards.

