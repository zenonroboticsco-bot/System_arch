# 📱 Robin Robot — Control App

<div align="center">

![Flutter](https://img.shields.io/badge/Built%20with-Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)
![API](https://img.shields.io/badge/API-FastAPI%20port%208000-009688?style=flat-square)
![Languages](https://img.shields.io/badge/Languages-EN%20%7C%20FA%20%7C%20AR-orange?style=flat-square)
![Version](https://img.shields.io/badge/Manual-V%201.0-brightgreen?style=flat-square)

*Flutter mobile & desktop app — full control of Robin over Wi-Fi*

</div>

---

## 📋 Contents

- [Connect to Robot](#-connect-to-robot)
- [8 Panels Overview](#-8-panels-overview)
- [Robot Control](#1--robot-control)
- [Voice Commands](#2--voice-commands)
- [AI Chatbot](#3--ai-chatbot)
- [Motion Library](#4--motion-library)
- [Scan Mode](#5--scan-mode)
- [Camera](#6--camera)
- [Vision](#7--vision)
- [Audio](#8--audio)
- [All Voice Commands](#-all-voice-commands-quick-reference)
- [Troubleshooting](#-troubleshooting)

---

## 🔗 Connect to Robot

| | Requirement |
|-|------------|
| **Wi-Fi** | Same network as robot |
| **Robot IP** | `10.255.254.75` |
| **API Port** | `8000` |
| **Robot must be** | Powered on + `run.sh` running |

**Startup checklist:**
1. Power on Robin (button on back of head)
2. Wait **~45 seconds** for all ROS2 nodes to initialize
3. Open the app → Robot Control panel
4. Tap **Get State** — if status data appears, you're connected ✅

---

## 📐 8 Panels Overview

| # | Panel | Icon | What You Can Do |
|---|-------|------|-----------------|
| 1 | Robot Control | 🤖 | Start/shutdown, live status, face expressions |
| 2 | Voice Commands | 🎤 | Activate wake word, set language, view log |
| 3 | AI Chatbot | 💬 | Type or speak questions, LLM replies |
| 4 | Motion Library | 🏃 | 40+ motions in 6 categories, one-tap |
| 5 | Scan Mode | 🔍 | OCR · ID extraction · Auto-describe |
| 6 | Camera | 📷 | Power on/off, capture still image |
| 7 | Vision | 👁️ | Object tracking, YOLO detection |
| 8 | Audio | 🔊 | ReSpeaker control, audio playback |

---

## 1 🤖 Robot Control

The main hub — power, status, and face expressions.

### Power

| Button | Action |
|--------|--------|
| ▶ **START ROBOT** | Sends start command, all nodes activate |
| ⏹ **SHUTDOWN** | Confirmation dialog → graceful shutdown |

> ⚠️ Always use SHUTDOWN — cutting power abruptly can corrupt the face database.

### Live Status (refreshes every 15s)

| Field | Meaning |
|-------|---------|
| `mode` | idle · listening · tracking · executing |
| `face_expression` | Current face shown on robot display |
| `voice_active` | Whether wake word listener is running |
| `ai_phase` | Current AI pipeline phase |

### Face Expressions

Tap any button to instantly change the robot's face:

| Expression | Use Case |
|-----------|---------|
| 😄 HAPPY | Welcome / positive feedback |
| 😢 SAD | Error / negative response |
| 😠 ANGRY | Warning / denied action |
| 😮 SURPRISED | Unexpected event |
| 😐 NEUTRAL | Default idle state |

---

## 2 🎤 Voice Commands

Activates Robin's built-in wake word listener. Once active, say **"z bot"** then your command — you'll hear a beep confirming the wake word was detected.

### Language

| Code | Language | Notes |
|------|---------|-------|
| `en` | English | Default · best accuracy |
| `fa` | Farsi | Requires Vosk Farsi model on robot |
| `ar` | Arabic | Requires Vosk Arabic model on robot |

### Controls

- **BEGIN** — starts wake word detection
- **STOP** — stops listening
- **Language dropdown** — changes language before starting
- **Command log** — shows timestamped results of every command

---

## 3 💬 AI Chatbot

Direct conversation with Robin's LLM (Zenon AIHIVE-LLMDSTXT). All replies are ≤30 words.

### Text Chat
1. Type any question in the text field
2. Tap **Send** — robot replies in under 10 seconds
3. Full conversation appears in the scrollable log

### Voice Chat
1. Select language
2. Tap **BEGIN** — robot listens (no wake word needed here)
3. Speak your question naturally
4. Robot transcribes → sends to LLM → speaks reply via Piper TTS
5. Tap **STOP** to end

---

## 4 🏃 Motion Library

One-tap access to all pre-programmed robot movements in 6 expandable categories.

### Categories

| Category | Example Motions |
|----------|----------------|
| 🚶 Basic | forward · backward · turn left/right · stop |
| 🕺 Gestures | wave · dance · spin · charge |
| 😊 Face Orientation | face_me · face_front · face_left · face_right |
| 🎭 Expressions | happy · sad · surprised · neutral |
| 🔧 Utility | stand · reset |
| ⚡ Advanced | Multi-joint sequences |

### How to Run

1. Tap a category header to expand it
2. Tap any motion tile (shows emoji + name)
3. Spinner appears while motion runs
4. Status: **Running → Completed** (clears after 2s)

> ⚠️ Only one motion at a time. Tapping while running has no effect — wait for completion.

---

## 5 🔍 Scan Mode

Uses Zenon Vision AI to analyze the camera view. Robin speaks the result aloud.

### Scan Types

| Mode | Trigger | Result |
|------|---------|--------|
| **AUTO** | Continuous every 4s | Describes what Robin sees |
| **OCR** | "read text" | Reads all visible text |
| **ID** | "scan id" | Extracts Name · DOB · ID# · Expiry |
| **Scene** | "describe scene" | 2-sentence environment description |
| **OFF** | — | Stops continuous scanning |

### Quick Scan Buttons

| Button | Action |
|--------|--------|
| Scan OCR | Immediate one-shot text read |
| Scan ID | Immediate ID card extraction |
| Get Status | Fetch current scan mode status |
| Get Result | Fetch most recent scan result text |

### Face-Aware Scanning

When a known person is detected, Robin uses their name:
```
Without face:  "I see a person holding a paper"
With face:     "I see Robin holding a paper"
```

> 💡 **OCR tip:** Fill the frame with the document, good lighting, hold still for 2–3s.
> 💡 **ID tip:** Place the ID face-up, flat, within 30cm. Only clearly visible fields are extracted.

---

## 6 📷 Camera

Controls the CSI camera (IMX sensor, 21 Hz).

| Button | Action |
|--------|--------|
| Camera ON | Starts camera_publisher_node lifecycle |
| Camera OFF | Deactivates camera node |
| Capture Image | Saves a still frame |

> ⚠️ The camera starts automatically with `run.sh`. Only use this panel if the camera stopped unexpectedly.

---

## 7 👁️ Vision

On-demand YOLO detection and person-following.

### Object Tracking (Follow Mode)

| Button | Action |
|--------|--------|
| START TRACKING | Starts object_tracker + follower_ctrl via node_manager |
| STOP TRACKING | Deactivates both, robot returns to stand |

**Parameters:**
- Deadband: `0.07` — no movement if person is centered
- Speed: `10 RPM` per wheel
- Lost timeout: `400ms` — stops if target disappears

### YOLO Detection

| Button | Action |
|--------|--------|
| START DETECTION | Activates yolo_detector (YOLOv8 TensorRT) |
| STOP DETECTION | Deactivates yolo_detector |

- Detects up to 5 objects per frame at confidence > 0.5
- Say **"z bot, what do you see"** to hear the detection spoken aloud

---

## 8 🔊 Audio

Controls the ReSpeaker microphone array and audio playback.

### ReSpeaker

| Button | Action |
|--------|--------|
| ReSpeaker ON | Activates microphone_array_publisher_node |
| ReSpeaker OFF | Deactivates mic array |

The ReSpeaker provides:
- Sound direction (0–360°) — used by **face_me** command
- Microphone input for Vosk STT and wake word detection

### Audio Playback

1. Enter the full path to a WAV file on the robot
2. Tap **Play Audio**
3. Tap **List Audio Files** to browse available files

**Common audio files on the robot:**
```
/home/robin/robin_ws/audio_files/blip.wav              ← wake word beep
/home/robin/robin_ws/audio_files/beginningtracking.wav ← follow mode start
/home/robin/robin_ws/audio_files/trackingstopped.wav   ← follow mode end
```

---

## 🎤 All Voice Commands — Quick Reference

> Say **"z bot"** then any command below. Wait for the beep.

| Category | Say after "z bot" | What Happens |
|----------|------------------|-------------|
| **Movement** | go forward | Drives forward |
| | go back | Reverses |
| | turn left | Turns left |
| | turn right | Turns right |
| | spin | Full 360° spin |
| | stop | Emergency halt |
| | face me | Faces your voice direction |
| | face back | Rotates 180° |
| **Gestures** | wave | Wave gesture |
| | dance | Dance sequence |
| | charge | Charge motion |
| **Vision** | scan now | Describes current view |
| | read text | OCR — reads all visible text |
| | scan id | Extracts ID card fields |
| | describe scene | 2-sentence scene detail |
| | detect objects | Lists visible objects |
| | scan mode on | Continuous scan every 4s |
| | scan mode off | Stop scanning |
| | what do you see | YOLO object description |
| **Identity** | checkface | Identifies person in view |
| | follow me | Start person-following |
| | stop following | Stop person-following |
| **System** | deactivate | Robot sleeps |
| **Any question** | *anything else* | Answered by LLM (≤30 words) |

---

## 🐛 Troubleshooting

| Problem | Fix |
|---------|-----|
| App shows no data | SSH to robot → `bash run.sh` |
| Voice not detected | Voice Commands panel → tap BEGIN |
| Camera error | `sudo systemctl restart nvargus-daemon` |
| Scan fails | Check robot internet: `ping 8.8.8.8` |
| Faces not recognized | `python3 face_enroll.py --list` |
| YOLO tracking stuck | `ros2 lifecycle set /follower_ctrl deactivate` |
| Token expired | github.com/settings/tokens → new token |

---

<div align="center">
<a href="../README.md">← Back to root</a> · <a href="../system_arch/README.md">System Architecture →</a>
</div>
