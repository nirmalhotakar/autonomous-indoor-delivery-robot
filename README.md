# AI-Enabled Autonomous Indoor Delivery Robot

This repository contains the source code and complete hardware configuration for an autonomous indoor delivery robot. Designed with a multi-tier split-architecture model, the system leverages a Raspberry Pi 4 Model B for high-level artificial intelligence tasks (facial recognition), an ESP32 subsystem for voice processing, and communicates wirelessly to an Arduino microcontroller handling real-time locomotion, sensor fusion, and obstacle avoidance.

## Core Features

*   **Multimodal Biometric Security:** Locks the system in vision-scanning mode until an authorized person is recognized via OpenCV and face embeddings.
*   **Phonetic Voice Dispatch:** Uses speech recognition on the ESP32 voice subsystem to parse vocal commands and assign destination targets.
*   **Wireless Command Transmission:** High-level controller connects via the HC-05 Bluetooth module to dispatch discrete movement instructions.
*   **Sensor-Fused Grid Navigation:** Combines an MPU-6050 6-DOF IMU and a LIS2MDL 3-axis magnetometer with a tuned PID controller for drift-compensated straight-line trajectory tracking.
*   **Creep-and-Lock Turning Algorithm:** Implements multi-stage angular velocity throttling down to minimum motor PWM to ensure 90-degree turns without inertial overshoot or wheel slip.
*   **Obstacle Avoidance:** Uses an MG90S servo-actuated HC-SR04 ultrasonic scanner to detect blockages, execute lateral detour waypoints, and return smoothly to the planned trajectory.

---

## Hardware Components & Bill of Materials

Based on the full hardware assembly, the following components are required:

### 1. High-Level AI & Vision
*   **Main Processor:** Raspberry Pi 4 Model B
*   **Camera:** Logitech Webcam (for facial detection and recognition pipeline)

### 2. Voice Chatbot Subsystem (ESP32)
*   **Controller:** ESP32 Controller Unit
*   **Audio Input:** INMP441 MEMS Microphone Module
*   **Audio Output:** MAX98357A Mono Amplifier & Small Speaker
*   **Display:** I2C OLED Display

### 3. Processing & Low-Level Control
*   **Microcontroller:** Arduino Uno R3
*   **Motor Shield:** L293D Motor Drive Shield (driving multi-wheel DC BO motor configuration)
*   **Wireless Communication:** HC-05 Module
*   **Logic Level Shifter:** Logic Level Converter

### 4. Sensors & Navigation
*   **Magnetometer:** LIS2MDL 3-Axis Digital Magnetic Field Sensor (I2C)
*   **Gyroscope & Accelerometer:** MPU-6050 6-Axis Motion Tracking Sensor (I2C)
*   **Ultrasonic Sensor:** HC-SR04 Ultrasonic Sensor
*   **Servo Mechanism:** MG90S Servo Motor (for sweeping the ultrasonic sensor)
*   **Speed / Odometry:** LM393 Speed Sensor Module
*   **Mounting:** Laser-Cut MDF Sensor Mount

### 5. Chassis & Power Distribution
*   **Chassis:** 6-Wheel Robotic Chassis with yellow-hub Wheels and DC BO Motors (Pairs)
*   **Motor Power Supply:** 12V 1.3Ah Lead-Acid Battery
*   **Compute Power Supply:** 20000mAh Power Bank

---

## Software Architecture

*   **`final_voice_and_command.py`:** Main Python program coordinating face verification, speech-to-text recognition, authorization lookup, and Bluetooth command broadcasting.
*   **`college_A_B_final.ino`:** Arduino firmware featuring MPU-6050 + LIS2MDL sensor fusion, creep-and-lock turn regulation, PID motor adjustments, and active grid waypoint tracking.
*   **`n_e_w_s_with_obstacle_avoidance.ino`:** Arduino navigation routine with integrated sweeping servo ultrasonic obstacle avoidance and lateral path recovery.

---

## Authorship & Authorization Parameters
*   **Lead Developer:** Nirmal
*   **Authorized Deployment Targets:** Nirmal, Chaitra, Rutu (Configured in Python biometric dictionary).
