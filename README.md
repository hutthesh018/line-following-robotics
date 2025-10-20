
# Smart Line-Following Obstacle-Avoiding Robot with OLED Display

## Overview:
This project is a **Smart Line Follower Robot** enhanced with **Obstacle Detection**, **OLED Display Interface**, and **Button Control**.
Built using an **Arduino UNO (or Nano)**, this robot can **follow a black line**, **detect and avoid obstacles**, and **display real-time information** on an OLED screen.
The system includes both **manual and serial command controls**, allowing the robot to be started, stopped, or restarted via **button press** or **serial input**.

##  Features:
*  **Line Following** using dual IR sensors.
*  **Obstacle Detection** using Ultrasonic Sensor (HC-SR04).
*  **OLED Display (SSD1306)** for live status updates.
*  **Manual ON/OFF and Restart Buttons** for easy control.
*  **Buzzer Alert** when an obstacle is detected.
*  **Motor Speed Control** using PWM.
*  **Serial Commands** (`start`, `stop`, `restart`, `quit`).

## Components Required:

| Component                   | Quantity | 
| --------------------------- | -------- |
| Arduino UNO / Nano          | 1        |
| L293D / L298N Motor Driver  | 1        |
| DC Gear Motors              | 2        |
| IR Line Sensors             | 2        |
| Ultrasonic Sensor (HC-SR04) | 1        |
| OLED Display (SSD1306, I2C) | 1        |
| Push Buttons                | 2        |
| Buzzer                      | 1        |
| Power Supply                | 1        |
| Jumper Wires, Breadboard    | -        |


## Circuit Connection:

### **Motor Driver (L293D / L298N)**
* **Left Motor:**
  * IN1 → Arduino **Pin 2**
  * IN2 → Arduino **Pin 3**
  * ENA → Arduino **Pin 4** *(PWM for speed)*
* **Right Motor:**
  * IN3 → Arduino **Pin 5**
  * IN4 → Arduino **Pin 6**
  * ENB → Arduino **Pin 7** *(PWM for speed)*
* **Motor Power (VCC):** 9V or Battery +
* **Motor Driver GND:** Connect to Arduino **GND**
* **Motor Output Pins (OUT1, OUT2, OUT3, OUT4):** Connect to Left and Right DC motors

### **Line Sensors (IR Sensors)**
* **Left IR Sensor OUT → Arduino Pin 8**
* **Right IR Sensor OUT → Arduino Pin 9**
* **VCC of both sensors → 5V (from Arduino)**
* **GND of both sensors → GND (common ground)**

### **Ultrasonic Sensor (HC-SR04)**
* **VCC → 5V**
* **GND → GND**
* **TRIG → Arduino Pin 10**
* **ECHO → Arduino Pin 11**

### **OLED Display (SSD1306 I2C)**
* **VCC → 3.3V or 5V (depending on model)**
* **GND → GND**
* **SDA → Arduino A4**
* **SCL → Arduino A5**

### **Buttons**
* **ON/OFF Button → Arduino Pin 13**
  * One leg → Pin 13
  * Other leg → GND
* **Restart Button → Arduino A0**
  * One leg → A0
  * Other leg → GND

###  **Buzzer**
* **Positive (+) → Arduino Pin 12**
* **Negative (–) → GND**

### **Power Supply**

* **9V Battery or 7.4V Li-ion pack → Motor Driver VCC**
* **Arduino VIN → Same Battery + (through motor driver’s 5V out or direct)**
* **All Grounds (GND) must be connected together** → *(Arduino, Sensors, Motor Driver, OLED, Battery)*

## Working Principle:
1. **Startup Phase:**
   * OLED displays "Ready" and waits for the user to press the ON button.
2. **Line Following:**
   * Robot follows the black line using two IR sensors.
   * Left/right motor speeds are adjusted based on sensor inputs.
3. **Obstacle Detection:**
   * Ultrasonic sensor measures distance ahead.
   * If obstacle < 20 cm → robot stops, buzzer beeps, and OLED shows "Obstacle!".
4. **Restart/Stop Control:**
   * Press ON/OFF button or send command through Serial Monitor.
   * Press Restart button to continue operation.


## Serial Commands:
You can control the robot using the Arduino Serial Monitor
| Command   | Function              |
| --------- | --------------------- |
| `start`   | Starts line following |
| `stop`    | Stops robot           |
| `restart` | Resumes after stop    |
| `quit`    | Stops and exits loop  |


## OLED Display Messages:
| Status    | Message on OLED              |
| --------- | ---------------------------- |
| Idle      | `Ready` / `Press ON`         |
| Running   | `Running` / `Line Following` |
| Obstacle  | `Obstacle!` / `XX cm`        |
| Restarted | `Restarted` / `Resuming`     |
| Stopped   | `Stopped` / `Press ON`       |


## How to Use:
1. Upload the sketch to your Arduino board.
2. Power up the system and ensure OLED displays “Ready.”
3. Place the robot on a **black line over white surface**.
4. Press **ON/OFF** button or send `start` command.
5. The robot will start following the line.
6. Place an obstacle in front to test ultrasonic detection.
7. Press **Restart** or send `restart` to resume.

## License
This project is open-source and free for educational use.
Developed for academic and prototype demonstration purposes.


