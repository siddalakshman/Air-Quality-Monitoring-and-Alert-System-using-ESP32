# PROJECT REPORT
# ESP32-Based Air Quality Monitoring and Alert System

**Project Domain:** Embedded Systems and IoT  
**Microcontroller:** ESP32  
**Sensor:** MQ-2 Gas Sensor  
**Development Platform:** Wokwi Simulator  
**Programming Language:** Arduino C++  
**Department:** Electronics and Communication Engineering

---

## 1. ABSTRACT

The ESP32-Based Air Quality Monitoring and Alert System is an embedded systems project designed to monitor gas and smoke-related sensor readings and generate automatic warnings when predefined thresholds are exceeded. The system uses an ESP32 microcontroller to process analog readings from an MQ-2 gas sensor. Based on the measured values, it provides visual indications through green, yellow, and red LEDs and activates a buzzer when the configured alert threshold is reached. The project is developed and tested using the Wokwi online simulator, allowing the circuit and software to be evaluated without physical hardware. It demonstrates sensor interfacing, analog-to-digital conversion, conditional logic, and audible alert generation. The prototype is intended for educational purposes and does not provide calibrated air-quality measurements.

## 2. INTRODUCTION

Air quality monitoring is important for understanding environmental conditions and identifying potentially hazardous gas or smoke levels. Embedded systems provide a practical way to collect sensor readings and respond automatically when measurements exceed predefined limits.

This project uses the ESP32 microcontroller as the main processing unit and an MQ-2 sensor as the input device. The program continuously reads sensor values, evaluates the readings against predefined thresholds, and activates the appropriate indicators.

The project is implemented in Wokwi, a browser-based electronics simulator. This approach allows the functionality to be developed and tested before physical hardware is assembled.

## 3. PROBLEM STATEMENT

Manual observation cannot continuously monitor changing sensor conditions. A simple automated system is therefore useful for demonstrating continuous monitoring and threshold-based warning generation.

The proposed system reads sensor data, classifies the readings into different status levels, and provides visual and audible alerts when necessary.

## 4. OBJECTIVES

The main objectives are:

- To interface an MQ-2 gas sensor with an ESP32.
- To read analog sensor values using the ESP32 ADC.
- To classify readings into normal, moderate, and alert conditions.
- To indicate status using three LEDs.
- To generate an audible warning using a buzzer.
- To display sensor readings through the Serial Monitor.
- To simulate and test the system using Wokwi.

## 5. HARDWARE AND SOFTWARE REQUIREMENTS

### 5.1 Components

| Component | Quantity | Function |
|---|---:|---|
| ESP32 DevKit | 1 | Main controller |
| MQ-2 gas sensor | 1 | Gas/smoke-related sensing |
| Green LED | 1 | Normal status |
| Yellow LED | 1 | Moderate status |
| Red LED | 1 | Alert status |
| Buzzer | 1 | Audible warning |
| 220 Ω resistors | 3 | LED current limiting |
| Jumper wires | As required | Circuit connections |

### 5.2 Software

- Wokwi ESP32 Simulator
- Arduino C++
- ESP32 Arduino Core 3.x
- Serial Monitor

## 6. SYSTEM ARCHITECTURE

The system follows a sensor-controller-alert architecture.

**System flow:**

```text
       MQ-2 GAS SENSOR
              |
              v
       ESP32 ANALOG INPUT
           GPIO 34
              |
              v
       SENSOR VALUE PROCESSING
              |
              v
       THRESHOLD COMPARISON
              |
       +------+------+ 
       |      |      |
       v      v      v
     NORMAL MODERATE ALERT
       |      |      |
       v      v      v
     GREEN  YELLOW   RED
      LED    LED     LED
                      |
                      v
                    BUZZER

       SENSOR STATUS
              |
              v
        SERIAL MONITOR
```

## 7. PIN CONFIGURATION

| Component | ESP32 Pin |
|---|---|
| MQ-2 Analog Output | GPIO 34 |
| Green LED | GPIO 18 |
| Yellow LED | GPIO 19 |
| Red LED | GPIO 23 |
| Buzzer Positive | GPIO 25 |
| MQ-2 VCC | VIN/5V in the simulated circuit |
| MQ-2 GND | GND |
| LED Cathodes | GND |
| Buzzer Negative | GND |

Each LED is connected through a current-limiting resistor.

**Hardware precaution:** MQ-2 modules may produce analog output voltages that exceed the ESP32's safe input voltage. For a physical implementation, verify the output range and use suitable voltage conditioning where necessary.

## 8. WORKING PRINCIPLE

The ESP32 initializes its input and output pins and configures the buzzer using the LEDC tone-generation interface. The MQ-2 sensor's analog output is read periodically using `analogRead()`.

The program compares the sensor value against two predefined thresholds.

- **Normal condition:** A reading below 1500 activates the green LED.
- **Moderate condition:** A reading from 1500 to 2499 activates the yellow LED.
- **Alert condition:** A reading of 2500 or above activates the red LED and generates a 2 kHz buzzer tone.

The current sensor value and corresponding status message are printed to the Serial Monitor every second.

The thresholds are selected for demonstration and software testing. They do not represent calibrated gas concentrations or official Air Quality Index values.

## 9. SOFTWARE IMPLEMENTATION

The firmware is developed in Arduino C++ for the ESP32.

The principal programming functions are:

| Function | Purpose |
|---|---|
| `analogRead()` | Reads the analog sensor value |
| `pinMode()` | Configures GPIO pins |
| `digitalWrite()` | Controls LED indicators |
| `ledcAttach()` | Configures the buzzer output |
| `ledcWriteTone()` | Generates or stops the buzzer tone |
| `Serial.print()` | Displays readings and status messages |
| `delay()` | Sets the sampling interval |

The code uses conditional statements to determine the system status and activate the corresponding outputs.

Refer to `sketch.ino` in this repository for the complete implementation.

## 10. TESTING AND EXPECTED RESULTS

The system can be tested in Wokwi by running the simulation and adjusting the virtual sensor input when supported.

| Test Condition | Expected LED | Buzzer | Expected Status |
|---|---|---|---|
| Reading below 1500 | Green | OFF | NORMAL |
| Reading from 1500 to 2499 | Yellow | OFF | MODERATE |
| Reading 2500 or above | Red | ON | ALERT |

### Testing Procedure

1. Open the Wokwi ESP32 project.
2. Start the simulation.
3. Open the Serial Monitor at 115200 baud.
4. Adjust the virtual sensor reading.
5. Observe the LED indicators and buzzer.
6. Verify that the displayed status corresponds to the configured thresholds.

These are expected results. Actual test observations should be recorded after running the simulation.

## 11. ADVANTAGES

- Low-cost educational implementation.
- No physical components required for initial simulation.
- Simple and understandable alert logic.
- Visual and audible warning mechanisms.
- Practical experience with ESP32 programming.
- Easy to extend with additional components and monitoring features.

## 12. LIMITATIONS

- The project uses demonstration thresholds rather than calibrated gas concentration limits.
- MQ-2 readings can be affected by multiple gases and environmental conditions.
- The system does not directly measure official AQI or PM2.5 concentrations.
- Simulation results do not establish the accuracy of physical hardware.
- The current design does not include cloud monitoring or historical data logging.

## 13. APPLICATIONS

Potential educational applications include:

- Gas and smoke detection demonstrations.
- Embedded systems laboratory projects.
- Sensor interfacing experiments.
- Automated warning systems.
- IoT prototype development.

The system is not a certified gas detector or life-safety device.

## 14. FUTURE SCOPE

The project can be improved by adding:

1. An LCD or OLED for displaying sensor readings.
2. A Wi-Fi dashboard for remote monitoring.
3. Timestamped data logging.
4. Notifications through an IoT platform.
5. Suitable calibrated sensors for specific air pollutants.
6. Physical prototype testing and comparison with a reference instrument.

## 15. CONCLUSION

The ESP32-Based Air Quality Monitoring and Alert System demonstrates how a microcontroller can process gas/smoke-related sensor readings and generate automatic visual and audible warnings. The project combines analog input, threshold comparison, GPIO control, buzzer tone generation, and serial reporting in a single embedded application.

Using Wokwi makes it possible to develop and test the program logic without purchasing hardware. The project provides a useful foundation for further study of embedded systems, sensor interfacing, and IoT applications. Future improvements could introduce calibrated sensors, wireless monitoring, and data logging to expand its functionality.

## 16. REFERENCES

1. Espressif Systems, ESP32 Arduino Core Documentation: https://docs.espressif.com/projects/arduino-esp32/en/latest/
2. Wokwi Online Simulator: https://wokwi.com/
3. Wokwi Documentation: https://docs.wokwi.com/

---

**Author:** Sidda Lakshman Kumar Naidu  
**Department:** Electronics and Communication Engineering

**Repository:** ESP32-Based Air Quality Monitoring and Alert System
