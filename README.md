<div align="center">

# 🤖 XiaoZhi AI Chatbot — ESP32 Firmware

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![ESP32](https://img.shields.io/badge/ESP32-WROOM--32-red.svg)](./esp32-wroom/)
[![ESP32-S3](https://img.shields.io/badge/ESP32-S3--WROOM--1-orange.svg)](./esp32-s3/)
[![OLED](https://img.shields.io/badge/Display-128×64%20OLED-green.svg)](#)
[![Author](https://img.shields.io/badge/Author-Muhammad%20Nabin-purple.svg)](#)

**An AI-powered voice chatbot running on ESP32 hardware**  
with a 0.96" OLED display · I2S microphone · I2S speaker output

---

<!-- BANNER IMAGE — replace path once added -->
<img src="assets/banner.png" alt="XiaoZhi AI Chatbot" width="820"/>

> 📸 *Real-time hardware photos will be updated as the build progresses*

</div>

---

## 📖 About This Project

XiaoZhi AI Chatbot turns an ESP32 development board into a standalone AI voice assistant. It captures audio through an **INMP441 I2S microphone**, processes it via an AI backend, and plays back the response through a **MAX98357A I2S amplifier** — while showing live status on a **0.96" 128×64 OLED display**.

This repository contains ready-to-flash firmware and complete hardware documentation for **two ESP32 variants**:

---

## 🗂️ Choose Your Board

<div align="center">

| | ESP32-WROOM | ESP32-S3 |
|:---:|:---:|:---:|
| **Board** | ESP32 Dev Board (WROOM-32) | ESP32-S3-WROOM-1 |
| **Firmware** | v1.9.2 | v2.2.2 |
| **Status** | ✅ Stable | ✅ Stable |
| **USB** | Micro-USB | USB-C |
| **LED** | External 5mm LED | Built-in RGB (GPIO 48) |
| **Guide** | [📘 Open WROOM Guide](./esp32-wroom/README.md) | [📗 Open S3 Guide](./esp32-s3/README.md) |

</div>

---

## 📁 Repository Structure

```
xiaozhi-ai-chatbot/
│
├── 📄 README.md                     ← You are here (main landing page)
│
├── 📁 esp32-wroom/
│   ├── 📄 README.md                 ← WROOM setup guide & wiring
│   ├── 📁 firmware/
│   │   └── ESP32-OLED-128X64-v1.9.2.bin
│   ├── 📁 docs/
│   │   ├── circuit_diagram.svg
│   │   └── hardware_setup.jpg
│   └── 📁 src/
│
├── 📁 esp32-s3/
│   ├── 📄 README.md                 ← S3 setup guide & wiring
│   ├── 📁 firmware/
│   │   └── ESP32-S3-OLED-128X64-v2.2.2.bin
│   ├── 📁 docs/
│   │   ├── circuit_diagram.svg
│   │   └── hardware_setup.jpg
│   └── 📁 src/
│
├── 📁 assets/
│   ├── banner.png
│   └── logo.png
│
└── 📄 LICENSE
```

---

## 🛒 Hardware Required

> Both variants use the same core components. Only the dev board differs.

| # | Component | Specification | Used In |
|:---:|---|---|:---:|
| 1 | ESP32 Dev Board | WROOM-32 **or** S3-WROOM-1 | Both |
| 2 | OLED Display | 0.96" I2C 128×64 SSD1306 | Both |
| 3 | Microphone | INMP441 I2S MEMS Module | Both |
| 4 | Amplifier | MAX98357A I2S Class D Module | Both |
| 5 | Speaker | 2 Watt 4Ω | Both |
| 6 | LED | 5mm (any color) | WROOM only |
| 7 | Resistor | 220Ω | WROOM only |
| 8 | Jumper Wires | Male-to-Female + Male-to-Male | Both |

---

## ⚡ Quick Flash

```bash
# Install esptool
pip install esptool

# ESP32-WROOM
esptool.py --chip esp32 --port <PORT> --baud 460800 \
  write_flash -z 0x0 esp32-wroom/firmware/ESP32-OLED-128X64-v1.9.2.bin

# ESP32-S3
esptool.py --chip esp32s3 --port <PORT> --baud 460800 \
  write_flash -z 0x0 esp32-s3/firmware/ESP32-S3-OLED-128X64-v2.2.2.bin
```

> 📋 Full step-by-step instructions are inside each board's README.

---

## 📄 License

This project is licensed under the terms described in [LICENSE](./LICENSE).

---

<div align="center">

Made with ❤️ by **Muhammad Nabin**

</div>
