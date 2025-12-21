# 🪙 Open Source Bitcoin Miner PCB – CERN OHL 2 - S Licensed

This project presents a fully open-source Bitcoin mining hardware platform, designed for transparency, modularity, and extensibility. Built around the BM1370 ASICs and powered by an ESP32-S3 microcontroller, this board offers a compact yet powerful solution for enthusiasts and developers interested in cryptocurrency mining hardware.

Released under the **CERN OHL 2 S**, all design files, firmware, and documentation are freely available for use, modification, and redistribution.

---

## 📌 Key Features

- **Open Source Hardware & Firmware** – CERN-OHL-S licensed
- **Dual BM1370 ASICs** for parallel mining
- **ESP32-S3** as the central controller
- **Precision power monitoring** via INA260
- **Multi-stage voltage regulation** from 12 V down to 0.8 V
- **UART communication** with level shifting
- **Temperature monitoring & fan control** per ASIC
- **USB-C interface** for firmware upload and updates
- **Status LEDs** for visual feedback
- **Modular I2C architecture** with multiplexer support

---

## 🔧 Technical Overview

### Power Architecture

The board is powered via a **12 V barrel jack**, with a recommended power supply of **at least 70 W** to ensure stable operation under full load. Power distribution is carefully managed through multiple buck converters:

- **TPS546A24 Buck Converter**: Converts 12 V to **1.2 V**, configurable via **SMBus/I2C**
- **12 V → 5 V Buck Converter**
- **5 V → 3.3 V Buck Converter**
- From 3.3 V, two reference voltages (**1.2 V and 0.8 V**) are derived for the ASICs

A **Texas Instruments INA260** is used to monitor the total current and voltage, providing accurate power consumption data for the entire board and its peripherals.

---

### ASICs & Communication

The core mining functionality is handled by **two BM1370 ASICs**, connected in parallel and powered by the regulated 1.2 V supply. These chips communicate via **UART**, with signal levels adjusted using a **SN74AVC level shifter** to ensure compatibility between the ESP32-S3 and the ASICs.

Each ASIC requires two reference voltages (1.2 V and 0.8 V), which are derived from the 3.3 V rail using dedicated regulators.

---

### Thermal Management & Fan Control

Each BM1370 ASIC includes an internal die temperature sensor, which is monitored by an **EMC2101** temperature controller. These controllers also support **PWM fan control**, allowing each ASIC to drive a dedicated **12 V cooling fan**.

Since the EMC2101 has a fixed I2C address, a **PCA9544 I2C multiplexer** is used to switch between the two devices, enabling independent monitoring and control.

---

### Control & Interfaces

At the heart of the board is an **ESP32-S3**, which runs the firmware responsible for:

- ASIC initialization and control
- Power and temperature monitoring
- Fan speed regulation
- Communication via UART and I2C
- Status indication via **two onboard LEDs**

A **USB-C port** is provided for firmware flashing and future updates, making development and deployment straightforward.

---

## 🛠️ Open Source & Licensing

This project is proudly released under the **CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S)**. This means:

- You are free to use, study, modify, and distribute the hardware designs
- Any derivative work must also be released under CERN-OHL-S
- If you manufacture or distribute products based on this design, you must provide recipients with access to the complete source files
- Contributions and improvements are welcome!

The CERN-OHL-S is specifically designed for open-source hardware, ensuring that designs remain open and accessible. We believe in open collaboration and transparency, and by releasing this project under CERN-OHL-S, we aim to foster innovation in the hardware mining community and provide a solid foundation for further development.

For the full license text, see the [LICENSE](LICENSE) file.

---
