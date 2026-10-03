# 🔴 Autonomous Laser-Based Intrusion Detection System

An embedded security system that detects unauthorized entry by monitoring a laser beam. When the beam is interrupted, the system automatically triggers an alarm and alert indicators, with no manual operation needed.

![Status](https://img.shields.io/badge/status-prototype-orange)
![Language](https://img.shields.io/badge/language-Embedded%20C-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📌 Overview

A laser diode projects a narrow beam onto a light sensor (LDR / photodiode). In normal state the sensor receives the beam continuously. If an intruder crosses the path, the beam breaks, the sensor reading drops below a threshold, and the microcontroller instantly activates the alert system.

The system runs autonomously: it powers up, monitors continuously, and raises alerts on its own.

## ✨ Features

- Real-time intrusion detection using a laser beam
- Fully autonomous, continuous monitoring
- Instant buzzer and LED alert on beam break
- Adjustable detection threshold for different lighting conditions
- Low cost, low power, and easy to deploy
- Expandable with GSM/IoT modules for remote notifications

## 🧰 Hardware Components

| Component | Purpose |
|---|---|
| Microcontroller (Arduino / ESP32 / 8051) | Central processing unit |
| Laser diode module (650 nm) | Beam source |
| LDR / Photodiode | Beam detection |
| Buzzer | Audible alarm |
| LEDs (Red / Green) | Status indication |
| Resistors, breadboard / PCB | Circuit connections |
| 5V power supply | Power source |
| *(Optional)* GSM / Wi-Fi module | Remote alerts |

> Update this table to match the exact components you used.

## ⚙️ How It Works

```
 Laser Diode ───────── beam ─────────▶ LDR / Photodiode
                                              │
                                      Analog / Digital signal
                                              ▼
                                       Microcontroller
                                              │
                          ┌───────────────────┴───────────────────┐
                    Beam intact                              Beam broken
                   (Green LED ON)                    (Buzzer + Red LED ON)
```

1. The laser is aligned with the sensor.
2. The microcontroller continuously reads the sensor value.
3. If the value is above the threshold, the system is **SECURE**.
4. If the value drops below the threshold, the system flags an **INTRUSION** and triggers the alarm.

## 🔌 Circuit / Pin Configuration

| Module | Pin |
|---|---|
| Laser diode | D8 |
| LDR (analog) | A0 |
| Buzzer | D9 |
| Red LED | D10 |
| Green LED | D11 |

> Adjust pins according to your board and wiring.

## 💻 Sample Code

```c
#define LASER_PIN   8
#define LDR_PIN     A0
#define BUZZER_PIN  9
#define RED_LED     10
#define GREEN_LED   11
#define THRESHOLD   500   // calibrate for your environment

void setup() {
  pinMode(LASER_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  pinMode(GREEN_LED, OUTPUT);
  digitalWrite(LASER_PIN, HIGH);   // laser always ON
  Serial.begin(9600);
}

void loop() {
  int value = analogRead(LDR_PIN);
  Serial.println(value);

  if (value < THRESHOLD) {          // beam broken
    digitalWrite(BUZZER_PIN, HIGH);
    digitalWrite(RED_LED, HIGH);
    digitalWrite(GREEN_LED, LOW);
  } else {                          // beam intact
    digitalWrite(BUZZER_PIN, LOW);
    digitalWrite(RED_LED, LOW);
    digitalWrite(GREEN_LED, HIGH);
  }
  delay(50);
}
```

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/laser-intrusion-detection-system.git
   ```
2. **Build the circuit** as per the pin configuration above.
3. **Open** the code in Arduino IDE (or your preferred IDE).
4. **Calibrate** the `THRESHOLD` value using the Serial Monitor readings.
5. **Upload** the code to the board.
6. **Align** the laser with the sensor and power up the system.

## 🧪 Testing

- Beam intact: green LED on, buzzer off
- Hand or object crossing the beam: buzzer and red LED on
- Beam restored: system returns to secure state

## 🔮 Future Enhancements

- SMS / call alerts through a GSM module
- IoT dashboard and mobile notifications (ESP32 + cloud)
- Camera capture on intrusion
- Multi-beam grid for wider coverage
- Auto-alignment and self-calibration
- Modulated laser signal to avoid false triggers from ambient light

## ⚠️ Safety Note

Use only low-power (Class 1 / Class 2, under 5 mW) laser modules. Never point a laser at eyes or reflective surfaces.

## 📁 Project Structure

```
├── src/            # Source code
├── docs/           # Circuit diagram, report
├── images/         # Prototype photos
├── README.md
└── LICENSE
```

## 👩‍💻 Author

**Anushya Ramesh**
B.E. Electronics and Communication Engineering
Vivekanandha College of Engineering for Women, Tamil Nadu

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
