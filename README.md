# 🤖 Autonomous Obstacle-Avoidance Robot

An autonomous three-wheeled robotic vehicle built on the Arduino platform.

The robot continuously scans its environment using a servo-mounted ultrasonic sensor. It uses non-blocking asynchronous logic to process spatial data in real time, adjust motor speed using Pulse Width Modulation (PWM), and dynamically navigate around obstacles.

---

## 📋 Features

### ⚡ Asynchronous Processing
Built entirely without `delay()` loops (except for minimal microsecond sensor pulses), allowing the robot to maintain a highly responsive main loop.

### 🎚️ Dynamic Speed Control
Uses hardware PWM to drive two independent DC motors smoothly for precise speed control.

### 🔄 Pan-and-Scan Navigation
When an obstacle is detected, the robot:

1. Stops
2. Rotates the ultrasonic sensor left and right using a servo motor
3. Compares available distances
4. Chooses the clearest path
5. Turns accordingly

### 🔘 Hardware Kill Switch
A physical toggle button using Arduino's internal pull-up resistor can instantly enable or disable autonomous operation.

### 🔋 Unified Power Distribution
A shared battery system safely supplies high current to the motor driver while simultaneously powering the Arduino.

---

# 🛠️ System Architecture & Pin Map

| Component | Arduino Pin | Function |
|-----------|-------------|----------|
| Ultrasonic Trigger | D12 | Digital Output |
| Ultrasonic Echo | D11 | Digital Input |
| Servo Signal | D10 | PWM Output |
| L298N ENA | D9 | PWM Output (Left Motor Speed) |
| L298N IN1 | D8 | Left Motor Direction |
| L298N IN2 | D7 | Left Motor Direction |
| L298N ENB | D5 | PWM Output (Right Motor Speed) |
| L298N IN3 | D4 | Right Motor Direction |
| L298N IN4 | D3 | Right Motor Direction |
| Toggle Button | D2 | Input Pull-up |

---

# 🔌 Power Distribution

```text
      [ Battery Pack (7.4V - 11.1V) ]
                 │
         ┌───────┴────────┐
         │                │
         ▼                ▼
     [ Switch ]      [ L298N Motor Driver ]
                             │
                             │ (5V Output)
                             ▼
                       [ Arduino Uno ]
                             │
                             ▼
                    [ Sensors & Servo ]
```

---

# 🚀 Getting Started

## Prerequisites

- Arduino IDE (v1.8.x or newer)
- `Servo.h` library (built into Arduino IDE)

---

## 📦 Hardware Requirements

- 1× Arduino Uno R3 (or compatible board)
- 1× L298N Dual H-Bridge Motor Driver
- 1× HC-SR04 Ultrasonic Sensor
- 1× SG90 Servo Motor
- 1× 3-Wheel Robot Chassis
- 2× DC Geared Motors
- 1× SPST Toggle Switch
- 1× 7.4V–11.1V Li-ion Battery Pack

---

# 💻 Installation

## Clone the Repository

```bash
git clone https://github.com/yourusername/autonomous-obstacle-robot.git
```

## Upload the Code

1. Open `src/autonomous_robot.ino` in Arduino IDE.
2. Wire all components according to the pin map.
3. Connect the Arduino to your computer via USB.
4. Select:

- **Tools → Board → Arduino Uno**
- **Tools → Port → Your COM Port**

5. Click **Upload**.

---

# ⚙️ How It Works

```text
          [ Start ]
               │
               ▼
        (Button ON?)
          │      │
         No      Yes
          │       │
          ▼       ▼
   [ Stop Motors ] [ Read Distance ]
                           │
                  Distance < 25 cm?
                     │          │
                    No         Yes
                     │          │
                     ▼          ▼
          [ Move Forward ]   [ Stop ]
                                 │
                                 ▼
                  [ Scan Left & Right ]
                                 │
                                 ▼
                   [ Compare Distances ]
                                 │
                                 ▼
                   [ Turn Best Direction ]
```

---

# 🔮 Future Scope

## 🍃 Sustainability & Energy Efficiency

### Regenerative Braking Emulation

Optimize H-bridge braking sequences to reduce inertial energy loss during sudden stops.

### Solar Power Integration

Mount flexible photovoltaic panels on top of the chassis to supplement battery charging during outdoor operation.

### Deep Sleep Mode

Use watchdog timers to place the microcontroller and sensors into low-power mode when idle.

---

## 🧠 Advanced Navigation & Intelligence

### PID Motor Control

Integrate wheel encoders and PID algorithms to maintain straight-line motion regardless of battery voltage fluctuations.

### SLAM Integration

Replace the ultrasonic scanner with LiDAR or depth cameras for simultaneous localization and mapping.

### IoT Telemetry

Upgrade to ESP32 for wireless transmission of sensor data and environmental maps.

---

# 📄 License

This project is licensed under the MIT License.

Feel free to use, modify, and distribute this project.

---

## ⭐ If you found this project useful, consider giving it a star.
