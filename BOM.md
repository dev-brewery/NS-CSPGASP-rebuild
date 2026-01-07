# Bill of Materials (BOM) - Google Home Mini 1st Gen Hack

This project involves replacing the main logic board of a Google Home Mini (1st Gen, Model H0A) with a custom solution. The two primary paths are using a **Raspberry Pi Zero 2 W** (Linux-based) or an **ESP32-S3** (Embedded).

## Core Components (Choose One Path)

### Option A: Raspberry Pi Zero 2 W (Linux/Python)
*Suitable for running a full OS, local voice assistant (Rhasspy, etc.), or streaming audio client.*

| Item | Description | Price (Approx.) | Link |
| :--- | :--- | :--- | :--- |
| **Mainboard** | **Raspberry Pi Zero 2 W**<br>Quad-core 64-bit ARM Cortex-A53, 512MB RAM, WiFi/BT. | ~$19.05 | [Adafruit](https://www.adafruit.com/product/5291) |
| **Microphone** | **INMP441 I2S Microphone Breakout**<br>Omnidirectional MEMS microphone with I2S interface. (Requires wiring) | ~$11.95 | [PMD Way](https://pmdway.com/products/inmp441-mems-i2s-omnidirectional-microphone-module) <br> *(Also widely available on Amazon/AliExpress)* |

### Option B: ESP32-S3 (Embedded/Home Assistant)
*Suitable for a "satellite" voice assistant for Home Assistant (ESPHome) or a Bluetooth speaker.*

| Item | Description | Price (Approx.) | Link |
| :--- | :--- | :--- | :--- |
| **Mainboard** | **Seeed Studio XIAO ESP32S3 Sense**<br>Includes on-board **Digital Microphone**, Camera (removable), WiFi/BLE, and battery management. Extremely small form factor. | ~$13.90 | [Seeed Studio](https://www.seeedstudio.com/XIAO-ESP32S3-Sense-p-5639.html) |
| **Alternative** | **Seeed Studio XIAO ESP32S3** (Standard)<br>No on-board mic. Requires external INMP441 (see above). | ~$4.99 | [Seeed Studio](https://www.seeedstudio.com/XIAO-ESP32S3-p-5627.html) |

---

## Common Components (Required for Both Paths)

| Item | Description | Price (Approx.) | Link |
| :--- | :--- | :--- | :--- |
| **Audio Amp** | **MAX98357A I2S Amplifier Breakout**<br>3W Class D Amplifier. Perfect for driving the stock Google Home Mini speaker (4Ω). | ~$5.95 | [Adafruit](https://www.adafruit.com/product/3006) <br> [SparkFun](https://www.sparkfun.com/products/14809) |
| **Power Supply** | **5V 2.5A Micro USB Power Supply**<br>High-quality supply required to prevent brownouts, especially for the Pi Zero 2 W. | ~$8.95 | [Adafruit](https://www.adafruit.com/product/1995) |
| **Storage** | **MicroSD Card (32GB or larger)**<br>For OS (Pi) or initial firmware flashing/storage (ESP32). | ~$5-10 | [Amazon / Local](https://www.amazon.com/s?k=micro+sd+card+32gb) |
| **Wiring** | **Silicone Wire / Jumper Wires**<br>For connecting the Top Board, Amp, and Mic to the Mainboard. | ~$5-10 | [Adafruit](https://www.adafruit.com/product/1970) |

## Optional / Project Specific

| Item | Description | Price (Approx.) | Link |
| :--- | :--- | :--- | :--- |
| **Display** | **7-Segment Display (I2C)**<br>Generic I2C LED display. *Note: "K4691DT" was identified in user images but may be a specific part number not widely listed. Standard TM1637 or HT16K33 backpacks are recommended alternatives if replacing.* | ~$5-10 | [Adafruit (HT16K33)](https://www.adafruit.com/product/878) |

## Notes on Stock Components
*   **Speaker:** The original driver is high quality and connects via a JST plug. It can be wired directly to the MAX98357A output.
*   **Top Board:** The original capacitive touch and LED board can be reused via I2C (SDA/SCL) and 5V power, but requires careful level shifting (3.3V logic vs 5V LED power) if the controller doesn't handle it. The **Seeed XIAO** and **Pi Zero** are 3.3V logic.
*   **Microphones:** The stock MEMS microphones on the top board are difficult to interface with directly without a custom PCB break-out (flex cable pitch is fine but pinout is complex). Using an external I2S mic (or the on-board one on the XIAO Sense) is the recommended "easy" path.
