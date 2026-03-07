# 🚀 Planet X Rover

An ESP32-based autonomous rover with environmental sensing, obstacle avoidance, and a live web control dashboard.

---

## Features

- **Live Web Dashboard** — control the rover and view all sensor data from any device connected to its WiFi
- **Motor Control** — forward, backward, left, right and stop via web interface
- **Auto Mode** — rover drives itself and stops automatically when an obstacle is detected
- **Obstacle Avoidance** — HC-SR04 ultrasonic sensor detects objects closer than 20cm
- **Environmental Sensors** — temperature, humidity (DHT11) and pressure (BMP280)
- **LCD Display** — 16x2 I2C LCD shows distance and sensor readings
- **Physical Buttons** — three buttons to display temperature, humidity and pressure on the LCD
- **Serial Monitor Output** — all sensor data printed every 2 seconds over USB

---

## Hardware Required

| Component | Quantity |
|-----------|----------|
| ESP32-WROOM-32 | 1 |
| L293D Motor Driver | 1 |
| DC Motors | 2 |
| HC-SR04 Ultrasonic Sensor | 1 |
| DHT11 Temperature & Humidity Sensor | 1 |
| BMP280 Pressure Sensor | 1 |
| 16x2 I2C LCD Display (0x27) | 1 |
| Push Buttons | 3 |
| AA Battery Pack (4x or 6x AA) | 1 |

---

## Pin Wiring

### Motor Driver (L293D)

| L293D Pin | ESP32 GPIO |
|-----------|------------|
| EN1,2 (pin 1) | GPIO 32 |
| IN1 (pin 2) | GPIO 25 |
| IN2 (pin 7) | GPIO 26 |
| IN3 (pin 10) | GPIO 19 |
| IN4 (pin 15) | GPIO 23 |
| EN3,4 (pin 9) | GPIO 33 |
| VCC1 (pin 16) | 3.3V |
| VCC2 (pin 8) | Battery + |
| GND (pins 4,5,12,13) | ESP32 GND + Battery - |
| OUT1 (pin 3) | Motor A wire 1 |
| OUT2 (pin 6) | Motor A wire 2 |
| OUT3 (pin 11) | Motor B wire 1 |
| OUT4 (pin 14) | Motor B wire 2 |

### Sensors & Display

| Component | ESP32 GPIO |
|-----------|------------|
| DHT11 Data | GPIO 4 |
| HC-SR04 TRIG | GPIO 5 |
| HC-SR04 ECHO | GPIO 18 |
| LCD SDA | GPIO 21 |
| LCD SCL | GPIO 22 |
| BMP280 SDA | GPIO 21 |
| BMP280 SCL | GPIO 22 |

> LCD, BMP280 share the same I2C bus (GPIO 21 + 22)

### Buttons

| Button | ESP32 GPIO |
|--------|------------|
| Temperature | GPIO 15 |
| Humidity | GPIO 2 |
| Pressure | GPIO 17 |

---

## Libraries Required

Install these via Arduino IDE Library Manager:

- `LiquidCrystal_I2C`
- `DHT sensor library` by Adafruit
- `Adafruit BMP280 Library`
- `Adafruit GFX Library`
- `WiFi` (built into ESP32 board package)
- `WebServer` (built into ESP32 board package)

---

## How to Use

### Upload
1. Open `PlanetXRover.ino` in Arduino IDE
2. Select board: **ESP32 Dev Module**
3. Select the correct COM port
4. Click Upload

### Connect to Web Dashboard
1. Power on the rover
2. On your phone or laptop, go to **WiFi Settings**
3. Connect to **`PlanetXRover`**
4. Password: **`rover1234`**
5. Open a browser and go to **`192.168.4.1`**

### Web Dashboard Controls
- **Arrow buttons** — hold to move, release to stop
- **Speed slider** — adjust motor speed (min 60% to ensure motors start)
- **Auto Mode toggle** — switches between manual control and autonomous driving
- **Sensor cards** — live readings updated every 2 seconds automatically

### Physical Buttons
- **Press once** — shows that sensor reading on the LCD
- **Press same button again** — clears back to distance display
- **Press different button** — switches to that reading

---

## I2C Device Addresses

| Device | Address |
|--------|---------|
| LCD | 0x27 |
| BMP280 | 0x76 |

---

## Notes

- Power the motors from a **4x AA or 6x AA battery pack** — a standard 9V block battery does not supply enough current to run motors
- All GND connections (ESP32 GND and battery negative) must be connected together on the L293D
- If a motor spins the wrong direction, swap its two output wires on the L293D — no code change needed
- Serial Monitor runs at **115200 baud** and prints all sensor data every 2 seconds

---

## Project Structure

```
PlanetXRover/
└── PlanetXRover.ino
```

---

## License

MIT License — free to use, modify and share.
