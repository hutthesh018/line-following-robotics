# Smart Line-Following Obstacle-Avoiding Robot with OLED Display

## Overview :
This project is a **Smart Line Follower Robot** built using an **ESP32**, enhanced with **Obstacle Detection**, **OLED Display Interface**, **4x4 Keypad Menu**, and **Button Control**.
The robot can:
* Follow a black line using dual IR sensors.
* Detect and avoid obstacles with an ultrasonic sensor.
* Display real-time status updates on an OLED screen.
* Be controlled via **push buttons**, **keypad menu**, or **serial commands**.
The system now supports **automatic pause when obstacles are detected** and **resuming via restart button** or keypad.

## Features:
1. **Line Following** using dual IR sensors.
2. **Obstacle Detection** using Ultrasonic Sensor (HC-SR04).
3. **OLED Display (SSD1306 I2C)** for live status updates:
   * `"Ready / Press ON"`
   * `"Starting Game"`
   * `"Running / Line Following"`
   * `"Obstacle Detected / XX cm"`
   * `"Game Ended / Press Restart"`
   * `"Resuming / Line Following"`
4. **Manual Control**: ON, OFF, Restart buttons.
5. **4x4 Keypad Menu** for selecting modes: Start, Stop, Restart, About.
6. **Buzzer Alert** when obstacle is detected.
7. **Motor Speed Control** via PWM.
8. **Serial Commands** supported: `start`, `stop`, `restart`, `quit`.

## 🛠️ Components Required
| Component                     | Quantity |
| ----------------------------- | -------- |
| ESP32 Development Board       | 1        |
| L293D / L298N Motor Driver    | 1        |
| DC Gear Motors                | 2        |
| IR Line Sensors               | 2        |
| Ultrasonic Sensor (HC-SR04)   | 1        |
| OLED Display (SSD1306, I2C)   | 1        |
| Keypad                        | 1        |
| Push Buttons                  | 3        |
| Buzzer                        | 1        |
| 7.4V Li-ion Pack / 9V Battery | 1        |
| Jumper Wires / Breadboard     | -        |


## Circuit Connection :

### Motor Driver (L293D / L298N)
* **Left Motor:** IN1 → GPIO 2, IN2 → GPIO 3, ENA → GPIO 4 (PWM)
* **Right Motor:** IN3 → GPIO 5, IN4 → GPIO 6, ENB → GPIO 7 (PWM)
* Motor Power VCC → Battery +
* GND → Common Ground
* OUT pins → Connect to DC motors

### Line Sensors
* Left IR OUT → GPIO 8
* Right IR OUT → GPIO 9
* VCC → 3.3V / 5V
* GND → GND

### Ultrasonic Sensor (HC-SR04)
* VCC → 5V
* GND → GND
* TRIG → GPIO 10
* ECHO → GPIO 11

### OLED Display (SSD1306 I2C)
* VCC → 3.3V
* GND → GND
* SDA → GPIO 21
* SCL → GPIO 22

### Keypad (only keys 1–4 used)
* Row Pins → GPIO 32, 33, 25, 26
* Column Pins → GPIO 27, 14, 12, 13
* Only keys 1 (Start), 2 (Stop), 3 (Restart), 4 (About) are functiona

### Push Buttons
* ON Button → GPIO 13 + GND
* OFF Button → GPIO A0 + GND
* Restart Button → GPIO A1 + GND

### Buzzer
* * → GPIO 12
* – → GND

### Power Supply
* 7.4V Li-ion / 9V Battery → Motor Driver VCC
* ESP32 VIN → Same Battery + (or through motor driver 5V output)
* Connect all GNDs together (ESP32, Sensors, Motor Driver, OLED, Battery)


## Working Principle:
1. **Startup Phase:**
   OLED shows `"Ready / Press ON"`; robot waits for ON button or keypad selection.
2. **Line Following:**
   Dual IR sensors detect the black line. Motor speeds adjust automatically.
3. **Obstacle Detection:**
   Ultrasonic sensor checks distance ahead. If < 20 cm:
   * Motors stop
   * Buzzer alerts
   * OLED shows `"Obstacle Detected"` → `"Game Ended / Press Restart"`
4. **Restart / Stop Control:**
   * **Restart Button** or keypad can resume operation.
   * **ON/OFF Buttons** or serial commands (`start`, `stop`, `restart`, `quit`) control robot.

##  Keypad Menu:
| Key | Function |
| --- | -------- |
| 1   | Start    |
| 2   | Stop     |
| 3   | Restart  |
| 4   | About    |


## OLED Display Messages:
| Status    | OLED Message               |
| --------- | -------------------------- |
| Idle      | Ready / Press ON           |
| Starting  | Starting Game              |
| Running   | Running / Line Following   |
| Obstacle  | Obstacle Detected / XX cm  |
| Stopped   | Game Ended / Press Restart |
| Restarted | Resuming / Line Following  |

## How to Use:
1. Upload ESP32 sketch.
2. Power the system; OLED displays **“Ready”**.
3. Place robot on black line.
4. Use **ON Button**, **Restart Button**, or **Keypad** to control.
5. Obstacle stops robot; restart resumes automatically.
6. Serial commands can also be used for control.

## License:
Open-source for **educational and prototype purposes**.

