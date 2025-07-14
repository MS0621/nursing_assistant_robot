# 🏥 Nursing Assistant Autonomous Robot System  

## 1. 📌 Project Overview

To address the excessive workload and burnout of nurses in hospital settings, we developed an autonomous robotic system that automates **medication delivery** and **vital sign monitoring**.

The system consists of **two TurtleBot4 robots** working cooperatively to perform logistics and patient interaction tasks across the **pharmacy and ward areas** in a hospital-like environment.

### System Architecture
<img width="920" alt="image" src="https://github.com/user-attachments/assets/9201e11e-0466-4b7a-8aae-bde2ca33f71c" />

### Node Architecture
<img width="1177" alt="image" src="https://github.com/user-attachments/assets/a5c84d87-49c2-4d37-9e85-74c5bc908902" />

### System flow
<img width="393" alt="image" src="https://github.com/user-attachments/assets/0e439a5b-1d56-4238-9ec0-7aecfa4f4423" />

---

## 2. ⚙️ Features and Functionalities

### ✅ Autonomous Navigation & Obstacle Avoidance
- SLAM-based navigation using ROS 2 Nav2
- Robust operation in complex environments like hospital corridors and rooms
- Dynamic obstacle detection (e.g. humans) with auto-stop and resume
  
<img width="479" alt="image" src="https://github.com/user-attachments/assets/b3056a58-d3fa-4957-845c-b18cc0670b8c" />

![project_map_real_2](https://github.com/user-attachments/assets/47fe3ec7-21e5-4fe4-877c-a25964b2c0be)



### ✅ Object and Patient Detection
- Real-time detection of medical items (Tylenol, bandages, etc.) using YOLOv8 and YOLOv11

  ![250627_YOLO turn](https://github.com/user-attachments/assets/025b827b-0cea-40c9-8565-37c37f36c835)

- Patient identification using ArUco markers and face detection

  ![face](https://github.com/user-attachments/assets/c7c89e95-f906-4512-b23b-c57c82a9576b)

- 3D localization via depth-based position estimation and TF2 transforms

  ![250627_marker turn](https://github.com/user-attachments/assets/f3ea4790-9497-4c3c-9367-df301f5fd89a)


### ✅ Contactless Vital Sign Monitoring
- rPPG-based estimation of heart rate, SpO2, and blood pressure

 < What is rPPG? >

rPPG is a non-contact method for measuring vital signs using a standard RGB camera. Based on the principles of traditional PPG, it detects subtle changes in facial skin color caused by blood volume variations to estimate physiological signals.

  1. Remote and non-invasive heart rate monitoring

  2. Analyzes minute skin tone changes from facial video

  3. Can measure: heart rate, heart rate variability (HRV), oxygen saturation, respiratory rate, stress levels, blood pressure, and skin temperature

- Integrated with face tracking and signal enhancement filters

[Comparison of rPPG-based Oxygen Saturation Measurement Performance by Face Area with Simple Signal Processing.pdf](https://github.com/user-attachments/files/21120109/Comparison.of.rPPG-based.Oxygen.Saturation.Measurement.Performance.by.Face.Area.with.Simple.Signal.Processing.pdf)



### ✅ Cloud-Based Robot Communication
- MQTT messaging over EMQX Cloud for stable multi-robot coordination

  <img width="379" alt="image" src="https://github.com/user-attachments/assets/c6ff258c-b111-43d3-be72-e0dd564d2fff" />
- Decentralized task assignment and rendezvous point logic(Using amcl_pose/pose/position/x,y topic)
![녹음 2025-07-08 194028](https://github.com/user-attachments/assets/c9592713-b85c-4ec3-b4cc-932662d9f80e)




  


### ✅ Integrated GUI Control Panel
- Real-time logistics requests and monitoring
- Visual display of robot status, positions, and vital signs


---

## 3. 🧠 Tech Stack

| Category        | Technologies Used |
|----------------|-------------------|
| **Robot Platform** | TurtleBot4, ROS 2 Humble, Nav2 |
| **Vision System**  | OAK-D Camera, YOLOv8/YOLOv11, OpenCV |
| **Communication**  | MQTT, EMQX Cloud |
| **AI / Algorithms**| rPPG, Face Detection, KCF Tracker, CHROM, TF2 |
| **Development Env.** | Ubuntu 22.04, Python3, RViz2, Roboflow |
| **Collaboration** | GitHub, Google Docs, Presentation Tools |

<img width="727" alt="image" src="https://github.com/user-attachments/assets/82cc495a-b436-4a73-a29b-a479adc2bb34" />


---

## 4. 🌟 Outcomes & Impact

- Successfully demonstrated a full **autonomous robotic pipeline** for hospital logistics and patient interaction
- Integrated navigation, object recognition, face detection, and vital sign estimation into one real-time system
- Cloud-based structure ensures **scalability and reliability** for large-scale hospital deployment
- Enables nurses to focus on specialized medical tasks by **offloading repetitive labor**
- Provides a **foundational model for smart hospital infrastructure**

---

## 5. 🎥 Demo

- ▶️ [Demo Video] (https://drive.google.com/file/d/1XalQhJVQs6HRULGkdsYCedEdJGqS83Y0/view?usp=sharing)

---
