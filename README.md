# 🤖 ESP32 Object Tracking Arm

A low-cost robotic arm built with an **ESP32**, **Python**, and **OpenCV** that can be controlled manually through a web interface or autonomously detect and pick up coloured objects using computer vision.

This project was built to explore the intersection of **embedded systems**, **robotics**, **computer vision**, and **wireless communication** while keeping the hardware affordable and accessible.

---

## Features

- 🎮 Web-based manual control hosted directly on the ESP32
- 📷 Real-time object detection using OpenCV
- 🔴 Detects red and blue objects
- 🤖 Automatic robotic arm movement
- 📡 Wi-Fi communication between computer and ESP32
- ⚙️ Servo motor control with smooth movement
- 🧮 Basic inverse kinematics for positioning
- 💰 Built using inexpensive, widely available components

---

# Project Overview

The robotic arm has two operating modes.

### Manual Mode

The ESP32 hosts its own web server, allowing any phone or computer connected to the same network to control:

- Base rotation
- Shoulder
- Elbow
- Gripper

No additional software is required—only a web browser.

---

### Autonomous Mode

A webcam continuously monitors the workspace.

Python and OpenCV detect coloured objects and determine their position within the camera frame.

The detected coordinates are converted into servo angles and transmitted to the ESP32, which moves the robotic arm to pick up the object.

The communication between the computer and ESP32 is performed over Wi-Fi using WebSockets (or Serial in the alternate implementation).

---

# System Architecture

```
                 Webcam
                    │
                    ▼
        Python + OpenCV Detection
                    │
         Detect object coordinates
                    │
                    ▼
        Inverse Kinematics Calculation
                    │
      WebSocket / Serial Communication
                    │
                    ▼
                ESP32 Controller
                    │
            Servo Motor Commands
                    │
                    ▼
              Robotic Arm Motion
```

---

# Hardware

| Component | Quantity |
|------------|----------|
| ESP32 Development Board | 1 |
| SG90/MG90S Servo Motors | 4 |
| Robotic Arm Kit | 1 |
| External 5V Power Supply | 1 |
| Jumper Wires | As needed |
| USB Cable | 1 |
| Webcam | 1 |

---

# Software

### Arduino

Libraries used:

- ESPAsyncWebServer
- AsyncTCP
- ESP32Servo

### Python

Packages:

```bash
pip install opencv-python
pip install websocket-client
pip install numpy
pip install pyserial
```

---

# Repository Structure

```
ESP32-Robotic-Arm/
│
├── esparm2.ino
├── esparm7.ino
├── robot_vision_control.py
├── OpenCV code red color tracking.py
├── README.md
│
├── images/
│   └── robotic_arm.jpg
│
└── demo/
    └── Robot Arm trial 12.mp4
```

---

# How It Works

## 1. Object Detection

OpenCV processes frames from a webcam.

Objects are detected using HSV colour thresholds.

The largest detected contour is selected and its centre point is calculated.

---

## 2. Motion Planning

The detected coordinates are mapped into servo angles.

The project uses basic inverse kinematics to estimate:

- Shoulder angle
- Elbow angle

The base servo rotates according to the object's horizontal position.

---

## 3. Communication

Python sends servo positions to the ESP32 using:

- WebSockets
- Serial communication (alternate version)

The ESP32 receives commands and updates each servo.

---

## 4. Gripping

Once the arm reaches the object:

1. Open gripper
2. Move into position
3. Close gripper
4. Return to neutral
5. Release object

---

# Challenges

This project involved much more than simply assembling a robotic arm.

Some of the biggest challenges included:

- Tuning OpenCV colour detection for different lighting conditions
- Preventing false object detections
- Synchronizing multiple servo motors
- Learning inverse kinematics for arm positioning
- Establishing reliable communication between Python and the ESP32
- Balancing movement speed with positioning accuracy

Each improvement introduced new problems, requiring many rounds of testing and debugging before the system behaved reliably.

---

# Future Improvements

- Object recognition using a trained AI model instead of colour detection
- Live camera feed embedded in the web interface
- Automatic path planning
- Depth estimation for improved positioning
- Gesture-based control
- Mobile application
- ROS integration
- Higher torque digital servos

---

# Lessons Learned

This project taught me how multiple engineering disciplines come together in robotics.

Rather than relying on a single programming language or framework, I combined embedded programming, computer vision, networking, and mathematics into one system.

More importantly, I learned that successful robotics projects depend on continuous testing and iteration. Every subsystem worked independently before eventually becoming part of a larger integrated solution.

---

# Built With

- ESP32
- Arduino IDE
- Python
- OpenCV
- WebSockets
- HTML/CSS/JavaScript
- C++

---

## Author

**Harsh Desai**

If you have any questions or suggestions, feel free to open an issue or reach out!
