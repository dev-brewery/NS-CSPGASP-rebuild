# Google Home Mini (Model H0A) Open Source Conversion

## Goal
The goal of this project is to repurpose the hardware of a 1st Generation Google Home Mini (Model H0A) for open-source projects. By replacing the locked mainboard with a Raspberry Pi Zero 2 W or ESP32, we can utilize the high-quality speaker, capacitive touch controls, and LED display.

## Hardware Architecture
*   **Brain:** Raspberry Pi Zero 2 W (recommended for size and USB capabilities) or ESP32-S3.
*   **Audio:** Existing 40mm driver connected to an I2S Amplifier (e.g., MAX98357A).
*   **Power:** Existing Micro-USB breakout board connected to the new MCU's 5V rail.
*   **Interface (Top Board):** The top shell containing the 4 LEDs and Capacitive Touch sensors is a USB device. It connects to the new brain via USB (D+, D-, VBUS, GND).

## Repository Structure
*   `HARDWARE.md`: Detailed wiring diagrams and pinout analysis.
*   `scripts/`: Tools for reverse engineering and testing the hardware.
*   `src/`: Skeleton code for the main application.
