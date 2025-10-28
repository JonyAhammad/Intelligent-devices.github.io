# 🌟 Smart Classroom Energy Management System (IoT + Firebase + ESP32)

## 📘 Project Overview
The **Smart Classroom Energy Management System** automatically controls classroom lights and fans based on **motion detection** and **ambient light levels**.  
It helps reduce energy waste by turning off devices when no one is in the room and updates the **real-time status** to **Firebase Cloud** for monitoring.

---

## 🎯 Objectives
- Detect human presence using a PIR sensor.
- Measure room brightness using an LDR sensor.
- Automatically control lights/fans through a relay module.
- Upload live data (status, brightness, motion) to Firebase.
- Build a real-time dashboard to monitor classroom energy usage.

---

## 🧰 Components Used

| Component | Quantity | Description |
|------------|-----------|-------------|
| ESP32 Board | 1 | Main microcontroller with Wi-Fi |
| PIR Sensor (HC-SR501) | 1 | Detects motion/presence |
| LDR (Light Dependent Resistor) | 1 | Measures brightness |
| 10kΩ Resistor | 1 | For LDR voltage divider circuit |
| Relay Module (1/2 Channel) | 1 | Controls bulb or fan |
| Bulb/Fan (5V or 220V) | 1 | Output load |
| Jumper Wires | — | For connections |
| Breadboard | 1 | For prototyping |
| USB Cable | 1 | For ESP32 programming |
| (Optional) DHT11/DHT22 | 1 | Temperature & humidity monitoring |

---

## ⚙️ Circuit Connections

### 🟢 PIR Sensor (HC-SR501)
| PIR Pin | ESP32 Pin |
|----------|-----------|
| VCC | 5V |
| GND | GND |
| OUT | GPIO 13 |

### 🟡 LDR Sensor (with 10kΩ Resistor)
| LDR Pin | ESP32 Pin |
|----------|-----------|
| One leg → 3.3V | — |
| Other leg → GPIO 34 (Analog Input) | — |
| 10kΩ Resistor between LDR output and GND | — |

### 🔵 Relay Module
| Relay Pin | ESP32 Pin |
|------------|-----------|
| VCC | 5V |
| GND | GND |
| IN | GPIO 26 |

💡 *Relay output terminals (COM and NO) connect to your device (bulb or fan).*

---

## ⚡ Circuit Diagram (Text Layout)
+3.3V -----> [ LDR ] ----┬----> GPIO 34
|
[10kΩ]
|
GND

PIR Sensor: OUT -> GPIO 13, VCC -> 5V, GND -> GND
Relay IN -> GPIO 26, VCC -> 5V, GND -> GND

# Tools & Libraries Used

Arduino IDE

FirebaseESP32 Library (by Mobizt)

WiFi.h (built-in ESP32 library)

Firebase Realtime Database

ESP32 DevKit Boar

[IoT Project Diagram](images/A_detailed_digital_schematic_diagram_illustrates_a.png)
<img width="1536" height="1024" alt="ChatGPT Image Oct 29, 2025, 12_50_56 AM" src="https://github.com/user-attachments/assets/644556e9-bcc0-42a1-862c-0a7fcafbfec7" />


# If You Don’t Use ESP32 / ESP8266

ESP32 and ESP8266 are popular because they combine microcontroller + Wi-Fi, but if you remove them, you’ll need two things instead:

A regular microcontroller (like Arduino Uno)

A separate Wi-Fi module (to send data to the cloud or mobile app)
