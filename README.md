#Smart Room Energy Management 


Tech: PIR sensor, LDR, relay module, ESP8266.

Campus use: Reduce energy waste in empty classrooms.

##Goal: Automatically turn ON/OFF lights and fans based on student presence and light intensity.
Use Case: Saves electricity in empty classrooms.

Key Features:

PIR sensor detects human motion.

LDR sensor checks room brightness.

ESP32 sends data to Firebase.

Dashboard shows real-time classroom status (ON/OFF).

Hardware:

ESP32

PIR Sensor

LDR Sensor

Relay Module (for lights/fans)

Firebase (for real-time data)

# 1. Hardware Components
| component  | quqntity |      Outcome(Purpose) |
| :---         |     :---:      |     :---:      | 
|  ESP32       |       1        |Main microcontroller with Wi-Fi|
| PIR sensor    | 1|             Detects motion (presence of people)|
|LDR           | 1 |             Measures brightness| 
| Relay Module| 1–2|  Controls lights/fans|
|LED bulb / small fan| 1 | Simulated classroom devices|
|Jumper wires + breadboard| 5/10| Connections|


#2. Circuit Connections

#PIR Sensor:

VCC → 5V

GND → GND

OUT → GPIO 13 (for example)

#LDR Sensor:

One leg → 3.3V

Other leg → Analog pin (A0 / GPIO 34) + resistor (to GND)

#Relay:

VCC → 5V

GND → GND

IN → GPIO 26

Output → Controls bulb/fan circuit

# 3. Software Tools

Arduino IDE (with ESP32 board installed)

Firebase Realtime Database

Blynk / Firebase Dashboard (optional UI)

# 4. Code Structure (Concept Overview)

#include <WiFi.h>
#include <FirebaseESP32.h>

#define PIR_PIN 13
#define LDR_PIN 34
#define RELAY_PIN 26

// Firebase credentials
#define FIREBASE_HOST "your-project.firebaseio.com"
#define FIREBASE_AUTH "your-firebase-secret"
#define WIFI_SSID "Your_WiFi"
#define WIFI_PASSWORD "Your_Password"

FirebaseData firebaseData;

void setup() {
  Serial.begin(115200);
  pinMode(PIR_PIN, INPUT);
  pinMode(LDR_PIN, INPUT);
  pinMode(RELAY_PIN, OUTPUT);

  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Firebase.begin(FIREBASE_HOST, FIREBASE_AUTH);
}

void loop() {
  int motion = digitalRead(PIR_PIN);
  int lightLevel = analogRead(LDR_PIN);

  // Logic: turn ON if motion detected and dark
  if (motion == HIGH && lightLevel < 1000) {
    digitalWrite(RELAY_PIN, HIGH);
    Firebase.setString(firebaseData, "/classroom/status", "ON");
  } else {
    digitalWrite(RELAY_PIN, LOW);
    Firebase.setString(firebaseData, "/classroom/status", "OFF");
  }

  delay(2000);
}

# 5. Firebase Database Structure Example
{
  "classroom": {
    "status": "ON",
    "motion": "1",
    "lightLevel": "820"
  }
}

# 6. Future Improvements

Add temperature/humidity (DHT11) sensors.

Create a web dashboard to view classroom status.

Integrate Telegram/Email alert when devices are ON for too long

