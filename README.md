
# ESP32-Based Autonomous Obstacle Avoidance Robot

An ESP32-based autonomous robot that uses an HC-SR04 ultrasonic sensor mounted on an SG90 servo motor for real-time obstacle detection and left/right path scanning. The ESP32 processes sensor readings and controls the L298N motor driver to navigate around obstacles. Powered by two lithium batteries, with an LM2596 buck converter supplying regulated 5V to the ESP32, ultrasonic sensor, and servo motor.

---

## 📑 Table of Contents

1. [Key Features](#-key-features)
2. [Hardware Required](#-hardware-required)
3. [Working Principle](#-working-principle)
4. [Wiring Guide](#-wiring-guide)
5. [Software Installation](#-software-installation)
6. [Troubleshooting](#-troubleshooting)

---

## 🚀 Key Features

- Real-time obstacle detection using HC-SR04 ultrasonic sensor.
- Servo-based left and right path scanning.
- Automatic direction selection based on measured distance.
- Dual DC motor control using L298N motor driver.
- Adjustable obstacle detection threshold and motor speed.
- Regulated 5V power supply using LM2596 buck converter.

## 🔧 Hardware Required

| Component | Quantity |
|---|---:|
| ESP32 Dev Module | 1 |
| HC-SR04 Ultrasonic Sensor | 1 |
| SG90 Servo Motor | 1 |
| L298N Motor Driver | 1 |
| LM2596 Buck Converter | 1 |
| DC Geared Motors | 2 |
| Front Wheels | 2 |
| Rear Caster Wheel | 1 |
| Robot Chassis | 1 |
| Lithium Batteries (2500mAh, 3.4V each) | 2 |
| Jumper Wires | As required |

## ⚙️ Working Principle

1. The ESP32 continuously reads the distance from the HC-SR04 ultrasonic sensor.
2. If the detected distance is greater than 20 cm, the robot moves forward.
3. If an obstacle is detected within 20 cm, the motors stop.
4. The servo rotates the ultrasonic sensor towards the left (150°) and right (30°).
5. The ESP32 measures and compares the distances in both directions.
6. The robot turns towards the direction with greater available clearance.
7. The process repeats continuously for autonomous navigation.

## 🔌 Wiring Guide

### 1. ESP32 to L298N Motor Driver

| ESP32 GPIO | L298N Pin |
|---|---|
| GPIO 32 | ENA |
| GPIO 25 | IN1 |
| GPIO 26 | IN2 |
| GPIO 33 | ENB |
| GPIO 27 | IN3 |
| GPIO 14 | IN4 |

### 2. ESP32 to HC-SR04

| HC-SR04 | ESP32 |
|---|---|
| VCC | 5V |
| GND | GND |
| TRIG | GPIO 5 |
| ECHO | GPIO 19 (through voltage divider) |

**Note:** Use a voltage divider on the HC-SR04 ECHO output to reduce its 5V signal to a safe 3.3V level for the ESP32.

### 3. ESP32 to Servo Motor

| Servo Wire | Connection |
|---|---|
| Orange (Signal) | GPIO 18 |
| Red (VCC) | 5V |
| Brown/Black (GND) | GND |

### 4. Power Supply Connections

- Two lithium batteries connected in series supply power to the L298N motor driver's input and LM2596 buck converter input.
- The LM2596 output is adjusted to 5V.
- Regulated 5V is supplied to the ESP32 VIN/5V input, HC-SR04 and servo motor.
- All circuit grounds must be connected together (common ground).

**Important:** Verify the buck converter output is 5V using a multimeter before connecting the ESP32 and other components.

## 💻 Software Installation

### 1. Arduino IDE Setup

1. Download and install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Open Arduino IDE and go to **File → Preferences**.
3. Add the ESP32 board package URL under Additional Boards Manager URLs:

   `https://dl.espressif.com/dl/package_esp32_index.json`

4. Navigate to **Tools → Board → Boards Manager**.
5. Search for ESP32 and install the ESP32 board package.
6. Select **Tools → Board → ESP32 Arduino → ESP32 Dev Module**.
7. Select the appropriate COM port.

### 2. Required Libraries

Install the following library through **Sketch → Include Library → Manage Libraries**:

- `ESP32Servo` – Servo motor interfacing and positioning.

### 3. Uploading the Code

1. Download or clone this repository.
2. Open the Arduino source file in Arduino IDE.
3. Ensure the ESP32 board and COM port are selected correctly.
4. Connect the ESP32 through USB.
5. Click **Verify** to compile the program.
6. Click **Upload** to flash the code onto the ESP32.
7. Disconnect USB and power the robot through its battery supply.

## 🛠️ Troubleshooting
Troubleshooting and Root-Cause Analysis
- Raspberry Pi Pico header soldering issue: Incorrect soldering alignment prevented proper board connections. Switched to an ESP32 development board with pre-soldered headers.
- IR sensor calibration issue: The IR sensor modules did not provide reliable black-and-white surface detection for lane following. Suspected improper calibration and inconsistent sensor readings. Changed the project approach to obstacle avoidance.
- Buck converter damage: Accidentally reversed the battery polarity while connecting the 7.4 V battery to the LM2596 input, damaging the converter. Replaced the buck converter.
- ESP32 damage: Accidentally connected the ESP32 power supply to the wrong breadboard position, causing an incorrect connection between the 5 V and GND pins. The board stopped accepting firmware uploads and had to be replaced.
- Servo motor failure: Hot glue entered the servo's internal gear mechanism while mounting the HC-SR04 sensor, causing it to jam. Replaced the servo motor.
- Incorrect motor direction: During obstacle-avoidance testing, the robot turned in the opposite direction to the intended movement. Checked the motor connections and corrected the wiring at the motor driver outputs.
- Power supply verification: Measured the LM2596 output using a multimeter after disconnecting the load and verified that it provided the required 5 V output.
## 🔄 Adjustable Parameters

The following parameters can be modified in the source code:

| Parameter | Default Value | Function |
|---|---:|---|
| STOP_DISTANCE | 20 cm | Obstacle detection threshold |
| MOTOR_SPEED | 200 | Motor PWM speed (0–255) |
| Left Scan Angle | 150° | Ultrasonic sensor left position |
| Right Scan Angle | 30° | Ultrasonic sensor right position |
| Left Turn Delay | 2500 ms | Left turning duration |
| Right Turn Delay | 1500 ms | Right turning duration |

Turning delays should be calibrated according to the actual robot movement.

## 📷 Project Demonstration

Add your robot photographs, circuit diagram and working demonstration video here.

---

## 👨‍💻 Technologies Used

- Microcontroller: ESP32
- Programming Language: Embedded C++ (Arduino framework)
- Development Environment: Arduino IDE
- Communication: GPIO and PWM
- Sensors: Ultrasonic distance sensing

---

**Project Type:** Embedded Systems | Robotics | Autonomous Navigation

