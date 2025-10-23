# Intelligent-devices


Project Overview: "ParkPal" - Smart Parking Timer
A device that tracks your parking time and sends phone notifications before your parking session expires.

🛠 Required Components & Tools
Hardware Components:
ESP32 Microcontroller (has built-in WiFi & Bluetooth) - ~$5-10

OLED Display (0.96") - to show remaining time - ~$3-5

Rotary Encoder or Buttons - for setting time - ~$2

Buzzer - for local alerts - ~$1

Breadboard & Jumper Wires - ~$5

USB Power Bank - to power the system in your car

Total Cost: ~$15-25

Software & Services:
Arduino IDE (free)

Blynk IoT Platform (free tier) - for phone notifications

IFTTT (If This Then That) - optional for advanced notifications

**Step-by-Step Implementation**
Phase 1: Basic Setup & Hardware
Circuit Connections:

 **ESP32 → OLED Display (I2C: SDA=21, SCL=22)
ESP32 → Rotary Encoder (CLK=18, DT=19, SW=23)
ESP32 → Buzzer (Pin 15)**

**Basic Code Structure:**
**
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <BlynkSimpleEsp32.h>

// Parking timer variables
unsigned long parkingStartTime = 0;
unsigned long parkingDuration = 7200; // 2 hours in seconds (10 min for testing)
bool timerActive = false;

void setup() {
  // Initialize display
  // Connect to WiFi
  // Initialize Blynk
}

void loop() {
  // Check rotary encoder for time setting
  // Update display with remaining time
  // Check if alert should be sent
  Blynk.run();
}
**

**Phase 2: Time Setting Interface**
How it works:

Rotate encoder to set hours (1-4 hours)

Press encoder to start timer

OLED shows: "Parking: 2H 00M" and countdown

**Phase 3: Smart Notifications**
Using Blynk for Alerts:

**
void checkParkingTime() {
  unsigned long elapsed = millis() - parkingStartTime;
  unsigned long remaining = parkingDuration - elapsed;
  
  // 15-minute warning
  if (remaining <= 900 && remaining > 895) { // 15 minutes = 900 seconds
    Blynk.logEvent("parking_alert", "15 minutes remaining!");
    tone(buzzer, 1000, 1000); // Beep
  }
  
  // 5-minute final warning
  if (remaining <= 300 && remaining > 295) { // 5 minutes
    Blynk.logEvent("parking_alert", "5 minutes left! Move your car!");
    tone(buzzer, 2000, 2000); // Longer beep
  }
  
  // Time expired
  if (remaining <= 0 && timerActive) {
    Blynk.logEvent("parking_alert", "PARKING TIME EXPIRED!");
    tone(buzzer, 3000, 5000); // Continuous alert
    timerActive = false;
  }
}
**
** Mobile App Setup
Blynk App Configuration:**
Download Blynk App (iOS/Android)

Create project with ESP32 template

Add "Notification" widget

Get Auth Token for your code

*What you'll see on your phone:*
🏎️ Parking Alert!
15 minutes remaining on your parking session
Location: [optional GPS coordinates]
Time started: 10:00 AM

**Enclosure & Final Design**
Create a car-friendly device:

3D-print a small case

Use suction cup to mount on windshield

Power via car USB port or power bank

User Interface:
┌──────────────┐
│ 🅿️ PARK PAL  │
│ Time: 2H 00M │
│ ▲ START  ▼   │
└──────────────┘

##***Implementation Plan (2-3 Weeks)***
**Week 1: Foundation**
Order components

Setup Arduino IDE with ESP32

Test OLED display with basic text

Connect to WiFi

**Week 2: Core Functionality**
Implement rotary encoder time setting

Create countdown timer logic

Setup Blynk account and basic notifications

Week 3: Polish & Testing
Design enclosure

Test in car environment

Create presentation materials

Add bonus features (see below)

** Bonus Features to Impress**
GPS Auto-Detection - automatically starts timer when you park

Multiple Time Presets - 30min, 1h, 2h, 4h buttons

Location Memory - remembers where you parked

Weather Alerts - warns if rain is coming

Battery Saver - deep sleep when not active
