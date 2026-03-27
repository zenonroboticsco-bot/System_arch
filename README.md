# 🤖 Robin Robot — System Architecture

<div align="center">

![Platform](https://img.shields.io/badge/Platform-NVIDIA%20Jetson%20Orin%20NX-76b900?style=for-the-badge&logo=nvidia&logoColor=white)
![ROS2](https://img.shields.io/badge/ROS2-Humble-22314E?style=for-the-badge&logo=ros&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flutter](https://img.shields.io/badge/App-Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)

**Interactive social robot — face recognition · voice AI · vision scanning · autonomous navigation**

</div>

---

## 📁 Repository Structure

```
robin-robot/
│
├── 📂 system_arch/          ← Robot system — ROS2 nodes, architecture diagrams
│   ├── README.md            ← Full technical documentation
│   ├── screenshots/         ← Diagram preview images
│   └── diagrams/            ← All .drawio source files
│
└── 📂 app/                  ← Flutter control app
    └── README.md            ← App user manual & panel guide
```

---

## ⚡ What Robin Does

| | Feature | Tech |
|---|---------|------|
| 🎤 | Wake word → voice commands | OpenWakeWord + Vosk STT (offline) |
| 👤 | Face recognition + greeting | dlib CNN + SQLite |
| 📷 | Vision scanning (OCR, ID, scene) | Zenon Vision AI API |
| 🧠 | LLM question answering | Zenon AIHIVE-LLMDSTXT |
| 🏃 | 40+ pre-built motions | Dynamixel + DDSM400 wheels |
| 👁️ | Person following | YOLOv8 TensorRT |
| 😊 | Animated face expressions | PyQt5 SVG |
| 📱 | Mobile / desktop control app | Flutter + FastAPI |

---

## 📖 Documentation

- **[System Architecture →](system_arch/README.md)** — ROS2 nodes, data flow, all diagrams
- **[App User Manual →](app/README.md)** — Flutter app guide, voice commands, panels

---

<div align="center">
Built on <strong>NVIDIA Jetson Orin NX</strong> · ROS2 Humble · Ubuntu 22.04
</div>
