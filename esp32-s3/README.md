<div align="center">

# 📗 ESP32-S3 — XiaoZhi AI Chatbot

[![Firmware](https://img.shields.io/badge/Firmware-v2.2.2-brightgreen.svg)](#-flashing-the-firmware)
[![Board](https://img.shields.io/badge/Board-ESP32--S3--WROOM--1-orange.svg)](#)
[![Display](https://img.shields.io/badge/Display-128×64%20OLED-green.svg)](#-oled-display-i2c--ssd1306-128×64)
[![Author](https://img.shields.io/badge/Author-Muhammad%20Nabin-purple.svg)](#-credits)

Firmware and complete wiring guide for the **ESP32-S3-WROOM-1**

[🏠 Main README](../README.md) · [📘 Switch to WROOM Guide](../esp32-wroom/README.md)

</div>

---

## 📷 Hardware Photo

<!-- PHOTO PLACEHOLDER — add your real photo here when ready -->
<!-- 📸 Real-time hardware photos will be updated as the build progresses -->

<div align="center">
  <img src="docs/hardware_setup.jpg" alt="ESP32-S3 Hardware Setup" width="720"/>
  <br/>
  <sub>📸 <em>Hardware photo — will be updated with real build photos</em></sub>
</div>

---

## 🛒 Parts List

| # | Component | Specification | Qty |
|:---:|---|---|:---:|
| 1 | 🟧 ESP32-S3 Dev Board | ESP32-S3-WROOM-1 (N16R8) | 1 |
| 2 | 🟦 OLED Display | 0.96" I2C 128×64 SSD1306 | 1 |
| 3 | 🟪 Microphone | INMP441 I2S MEMS Module | 1 |
| 4 | 🟫 Amplifier | MAX98357A I2S Class D | 1 |
| 5 | ⬛ Speaker | 2 Watt 4Ω | 1 |
| 6 | 🔌 Jumper Wires | Male-to-Female, Male-to-Male | — |

> ℹ️ No external LED needed — the ESP32-S3 has a **built-in RGB LED on GPIO 48**.

---

## 🔌 Wiring / Pin Connections

> 💡 **Tip:** Match the wire colors in the circuit diagram to these tables for easy reference.

---

### 🟦 OLED Display — I2C (SSD1306 128×64)

```
╔══════════════════════════════════════════╗
║      OLED 128×64  →  ESP32-S3            ║
╠══════════════════╦═══════════════════════╣
║  OLED Pin        ║  ESP32-S3 Pin         ║
╠══════════════════╬═══════════════════════╣
║  GND             ║  GND                  ║
║  VCC             ║  3.3V                 ║
║  SCL  (SCK)      ║  GPIO 42  ⚠️           ║
║  SDA             ║  GPIO 41              ║
╚══════════════════╩═══════════════════════╝
```

> ⚠️ **Critical:** SCL (SCK) on this board is **GPIO 42**, NOT GPIO 40.  
> Wiring SCK to GPIO 40 will result in a completely blank OLED display.

---

### 🟪 INMP441 — I2S Microphone

```
╔══════════════════════════════════════════╗
║     INMP441 MIC  →  ESP32-S3             ║
╠══════════════════╦═══════════════════════╣
║  MIC Pin         ║  ESP32-S3 Pin         ║
╠══════════════════╬═══════════════════════╣
║  GND             ║  GND                  ║
║  VDD             ║  3.3V                 ║
║  SCK             ║  GPIO 9               ║
║  WS              ║  GPIO 5               ║
║  SD              ║  GPIO 4               ║
║  L/R             ║  GND  (Mono Left)     ║
╚══════════════════╩═══════════════════════╝
```

> ⚠️ **Important:** L/R pin **must** be tied to GND for mono-left operation. Leaving it floating causes noise or silence.

---

### 🟫 MAX98357A — I2S Amplifier

```
╔══════════════════════════════════════════╗
║    MAX98357A AMP  →  ESP32-S3            ║
╠══════════════════╦═══════════════════════╣
║  AMP Pin         ║  ESP32-S3 Pin         ║
╠══════════════════╬═══════════════════════╣
║  GND             ║  GND                  ║
║  VIN             ║  5V  (VIN)            ║
║  BCLK            ║  GPIO 17              ║
║  LRC             ║  GPIO 16              ║
║  DIN             ║  GPIO 15              ║
║  GAIN            ║  (leave floating)     ║
╚══════════════════╩═══════════════════════╝
```

> 🔈 Connect your **2W 4Ω Speaker** to the **OUT+** and **OUT−** terminals on the MAX98357A board.

---

## 📐 Circuit Diagram

<!-- CIRCUIT DIAGRAM PLACEHOLDER — add your diagram here when ready -->
<!-- 📸 Real-time circuit diagram will be updated -->

<div align="center">
  <img src="docs/circuit_diagram.svg" alt="ESP32-S3 Circuit Diagram" width="820"/>
  <br/>
  <sub>📐 <em>Circuit diagram by <strong>Muhammad Nabin</strong> — full-size: <a href="docs/circuit_diagram.svg">docs/circuit_diagram.svg</a></em></sub>
</div>

---

## 📥 Flashing the Firmware

### 🔧 Prerequisites

- ✅ Python 3.x installed
- ✅ `esptool` installed:
  ```bash
  pip install esptool
  ```
- ✅ **USB-C cable** connected to the **USB port** on your ESP32-S3 board *(not the UART port)*
- ✅ USB drivers installed if required

> 🔍 **Find your port:**  
> - **Windows** → Device Manager → Ports (COM & LPT) → e.g. `COM5`  
> - **Linux** → `ls /dev/ttyACM*` → e.g. `/dev/ttyACM0`  
> - **macOS** → `ls /dev/cu.*` → e.g. `/dev/cu.usbmodem14201`

> ⚠️ **ESP32-S3 Note:** If the board is not detected, hold the **BOOT** button while plugging in the USB cable to enter download mode manually.

---

### 🗑️ Step 1 — Erase Flash *(recommended for first-time flash)*

```bash
esptool.py --chip esp32s3 --port <YOUR_PORT> erase_flash
```

---

### 💾 Step 2 — Flash the Firmware

```bash
esptool.py --chip esp32s3 --port <YOUR_PORT> --baud 460800 \
  write_flash -z 0x0 firmware/ESP32-S3-OLED-128X64-v2.2.2.bin
```

**Examples by OS:**

```bash
# ── Windows ──────────────────────────────────────────────────────────
esptool.py --chip esp32s3 --port COM5 --baud 460800 \
  write_flash -z 0x0 firmware/ESP32-S3-OLED-128X64-v2.2.2.bin

# ── Linux ────────────────────────────────────────────────────────────
esptool.py --chip esp32s3 --port /dev/ttyACM0 --baud 460800 \
  write_flash -z 0x0 firmware/ESP32-S3-OLED-128X64-v2.2.2.bin

# ── macOS ────────────────────────────────────────────────────────────
esptool.py --chip esp32s3 --port /dev/cu.usbmodem14201 --baud 460800 \
  write_flash -z 0x0 firmware/ESP32-S3-OLED-128X64-v2.2.2.bin
```

> ⚠️ Always use `--chip esp32s3` — using `--chip esp32` will fail or brick the flash.

---

### ▶️ Step 3 — Reset & Boot

Press the **RST (Reset)** button on your board after flashing.  
The OLED display will show the XiaoZhi startup face animation. ✅

---

## ✅ Pre-Power Checklist

```
[ ] OLED → SCL (SCK) wired to GPIO 42  ← most common mistake, double check!
[ ] OLED → SDA wired to GPIO 41
[ ] OLED → VCC wired to 3.3V (NOT 5V)
[ ] INMP441 mic → L/R pin tied to GND
[ ] INMP441 mic → VDD wired to 3.3V
[ ] MAX98357A amp → VIN wired to 5V (VIN pin)
[ ] Speaker connected to OUT+ and OUT− on amp
[ ] Using USB-C port (not UART port) for flashing
[ ] Correct firmware file selected (v2.2.2 for S3)
[ ] Flash command used --chip esp32s3
[ ] Firmware flashed successfully (no error in terminal)
```

---

## 🔧 Troubleshooting

| ❌ Problem | 🔍 Likely Cause | ✅ Fix |
|---|---|---|
| OLED stays blank | SCK wired to GPIO 40 | **Move SCK wire to GPIO 42** |
| OLED shows garbage | SDA/SCL swapped | Check: SDA→41, SCL→42 |
| OLED dims / flickers | VCC connected to 5V | Move VCC to 3.3V only |
| No sound from speaker | Wrong AMP wiring | Verify BCLK→17, LRC→16, DIN→15 |
| Mic not picking up audio | L/R pin floating | Tie L/R to GND |
| Board not detected by PC | Wrong USB port | Use the **USB** port, not UART |
| Flash fails | Wrong chip flag | Use `--chip esp32s3` not `esp32` |
| "Wrong boot mode" error | Not in download mode | Hold BOOT + plug USB cable |
| Board stuck in boot loop | Wrong flash address | Confirm flash address is `0x0` |

---

<div align="center">

## 👤 Credits

**Circuit Diagram · Firmware · Documentation**  
Created by **Muhammad Nabin**

---

[🏠 Main README](../README.md) · [📘 Switch to WROOM Guide →](../esp32-wroom/README.md)

</div>
