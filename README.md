# Arduino Smart Soil Moisture Sensor & Automated Irrigation Controller

Traditional irrigation systems often waste large amounts of water due to rigid, timer-based schedules. This project uses an Arduino Uno combined with a soil moisture sensor and a relay module to monitor root-zone hydration in real-time and dynamically trigger a water pump only when soil moisture drops below a set threshold.

Welcome to the repository for my automated soil moisture monitoring system! I built and simulated this project in Tinkercad Circuits as part of my computer engineering portfolio to explore embedded systems, sensor integration, and real-world resource management.
System Components

Arduino Uno R3: The central microcontroller processing sensor data and controlling system logic.

Soil Moisture Sensor: Measures the electrical conductivity of the soil to determine water content.

Relay Module: Acts as an electrically operated switch to safely drive higher-voltage actuators like a water pump.

Visual & Serial Feedback: Integrated LEDs and the Arduino Serial Monitor provide real-time status updates.

Block Programming Logic

The system runs on a continuous loop using Tinkercad's block code:

Data Acquisition: Reads the analog value from the soil moisture sensor connected to pin A0.

Data Logging: Prints the current moisture reading to the Serial Monitor.

Decision Making (Threshold Logic):

If the soil moisture value falls below 100 (indicating dry soil), the Arduino sets digital pin 8 to HIGH, activating the relay and pump.

Otherwise, it keeps pin 8 LOW to conserve water and energy.

Engineering Reflections & Lessons Learned

While building and debugging this circuit, I ran into a crucial hardware lesson regarding electrical limits:

The Pin D7 Power Mistake: Initially, I wired the power pin of the soil moisture sensor directly to digital pin D7 and set it HIGH in my code to power the sensor. The Tinkercad simulator immediately flagged a warning:
Current through I/O pin(s) D7 (28.6 mA) exceeds the recommended maximum of 20.0 mA. This may reduce the usable lifetime of the Arduino.

How I Fixed It:

I learned that digital I/O pins on microcontrollers are designed for signaling and communication, not for supplying continuous power to external hardware modules. Drawing $28.6\text{ mA}$ exceeds the safe $20\text{ mA}$ limit of the ATmega328P pins and risks damaging the chip over time.

To fix this, I re-routed the sensor's power wire directly to the dedicated 5V power supply pin on the Arduino board. This provides a stable, independent power source for the sensor without straining any digital I/O pins, keeping the microcontroller safe and efficient!

🔮 Future Improvements

Add an I2C 16x2 LCD display to show live moisture percentages directly on the hardware setup.

Implement hysteresis to prevent the pump from rapidly toggling on and off right at the threshold boundary.

Transition the block code into standard C++ Arduino code to prepare for more advanced firmware development.
