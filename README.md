# HawkEyeX – Intelligent Face Tracking & Laser Alignment System

<div align="center">
  <img 
    src="https://github.com/Madxfury/HawkEyeX/blob/9ba00148177d6d373603b8aa30fc2598ebdf2a63/Assets/HawkeyeX_Logo.png"
    alt="HawkEyeX Logo"
    height="200"
    style="margin-bottom: 6px;"
  />
  
  <br />
  <h3><i>{From Vision to Motion : Closing the AI–Hardware Loop}</i></h3>
</div>

<br />

**HawkEyeX** is a real-time **computer vision–driven robotic tracking system** that detects a human face from a live camera feed and **physically responds** by aligning a laser pointer using a dual-axis servo mechanism controlled by an Arduino.

Unlike software-only demos, HawkEyeX demonstrates how **visual intelligence can be translated into precise, low-latency physical motion**, a core challenge in robotics, autonomous systems, and embodied AI.

---

## 🧩 Problem Statement

Most introductory computer vision projects focus on **detection only**  drawing bounding boxes on a screen.

However, real-world AI systems must answer a harder question:

> **How do we convert perception into reliable, real-time action in the physical world?**

Key challenges include:
- Translating pixel-space coordinates into mechanical movement  
- Maintaining low latency for real-time tracking  
- Synchronizing software intelligence with hardware actuation  
- Ensuring stable motion without oscillation or jitter  

**HawkEyeX** addresses these challenges by building a closed-loop system that connects **vision → control logic → embedded hardware → physical response**.

---

## 📸 System Visuals

### 🎥 Live Face Tracking Interface
<p align="center">
  <img src="https://github.com/Madxfury/HawkEyeX/blob/2fc014daadd29d3e705ca5c425f19dd98e96d7ff/Assets/CV_Face_Traking_Interface.jpg" width="700"/>
</p>

### 🏗️ System Architecture
<p align="center">
  <img src="https://github.com/Madxfury/HawkEyeX/blob/8427df59fa6e839b9ccff417e20e44e016d338b1/Assets/System_Architecture.png" width="800"/>
</p>

### 🔌 Hardware Setup
<p align="center">
  <img src="https://github.com/Madxfury/HawkEyeX/blob/9deebe8c58ec1ae34593a4f8185c1b8b1a6a8458/Assets/Hardware_setup.jpg" width="600"/>
</p>

---

## 🌟 Key Capabilities

### 👁️ Real-Time Face Detection
- Live video capture using OpenCV  
- Face detection via Haar Cascade / cvzone FaceDetector  
- Robust detection under moderate lighting conditions  

### 🎯 Physical Face Tracking
- Face centroid calculation for each frame  
- Pixel displacement mapped to servo angles  
- Continuous pan–tilt motion to maintain alignment  

### ⚡ Low-Latency Closed Loop
- End-to-end response time: **~100–150 ms**
- Continuous feedback loop (not event-based)
- Stable tracking without abrupt jumps  

### 🔗 Seamless Software–Hardware Integration
- Python ↔ Arduino communication via PyFirmata  
- Hardware abstraction using StandardFirmata  
- Clean separation between perception and actuation  

---

## 🏗 System Architecture (Detailed)

HawkEyeX follows a **two-layer architecture**, inspired by real-world robotics systems.

### 1️⃣ Vision & Control Layer (Python)
- Captures live frames from webcam  
- Detects face and computes center coordinates  
- Normalizes pixel position relative to frame size  
- Interpolates face position into servo angles  
- Sends commands via serial communication  

### 2️⃣ Actuation Layer (Arduino)
- Receives servo angle commands  
- Controls two servo motors:
  - **X-axis** (horizontal pan)
  - **Y-axis** (vertical tilt)
- Laser pointer mounted on Y-axis tracks face in real time  

---

## 🛠 Tech Stack

### Software
- Python  
- OpenCV  
- cvzone  
- NumPy  
- PyFirmata  
- Arduino IDE  

### Hardware
- Arduino Uno R3  
- 2× Servo Motors (Pan & Tilt)  
- Laser Module  
- USB Webcam  
- Jumper wires & power supply  

---

## ⚙️ Core Control Logic

To ensure smooth and resolution-independent motion, face coordinates are mapped to servo angles using linear interpolation:

```python
servoX = np.interp(face_x, [0, frame_width], [180, 0])
servoY = np.interp(face_y, [0, frame_height], [180, 0])
```
## 🔌 Hardware Connections

<div align="center">

<table>
  <tr>
    <th>Component</th>
    <th>Arduino Pin</th>
  </tr>
  <tr>
    <td>Servo (X-axis)</td>
    <td>Pin 9</td>
  </tr>
  <tr>
    <td>Servo (Y-axis)</td>
    <td>Pin 10</td>
  </tr>
  <tr>
    <td>Laser Module</td>
    <td>Mounted on Y-axis servo</td>
  </tr>
</table>

</div>

<p align="center">
  <sub><b>Note:</b> Arduino must be flashed with <b>StandardFirmata</b> before running the Python code.</sub>
</p>


---

### 🚀 Prerequisites
- Python 3.x
- Arduino IDE
- USB Webcam
- Arduino Uno (with StandardFirmata uploaded)
## 🚀 Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/Madxfury/HawkEyeX.git
cd HawkEyeX
```
### 2️⃣ Install Dependencies
```bash
pip install opencv-python numpy cvzone pyfirmata
```
### 3️⃣ Configure Serial Port
```bash
port = "COM11"  # Update based on your system
```
### 4️⃣ Run the Tracker
```bash
python facetracking.py
```
## 🎥 Working Demo

📎 **Live Hardware Demo**  
https://drive.google.com/file/d/1mSrebXJIhjzprI4NYx8MaNPxpr59gtvd/view

---

## 📊 Observed Results

- Accurate face detection and tracking  
- Stable servo response without oscillation  
- Reliable laser alignment  
- Best performance with a single face in view  

---

## 🌍 Applications

- Human-following robots. 
- Autonomous camera tracking systems  
- Smart surveillance platforms  
- Interactive AI installations  
- Attention-aware human–machine interfaces  

---

## 🔮 Future Roadmap

- [ ] Deep learning–based detection (YOLO / DNN)
- [ ] Multi-face prioritization logic
- [ ] PID-based servo smoothing
- [ ] Wireless control (ESP32 / Wi-Fi / Bluetooth)
- [ ] Object tracking beyond faces
---

<div align="center">
  <sub><i>Built with</i></sub> <sub><b>❤️</b></sub> <sub><i> by Sanskar</i></sub>
</div>
