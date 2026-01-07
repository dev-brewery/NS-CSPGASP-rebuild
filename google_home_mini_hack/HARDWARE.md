# Hardware Interface Guide

## ⚠️ SAFETY WARNING ⚠️
**Voltage Logic Levels:** The Top Board logic (SDA/SCL) and Chip Power operate at **3.3V**. The LEDs require **5V**.
*   **DO NOT** connect the 3.3V or Data pins to 5V.
*   **DO NOT** short the 5V line to the 3.3V line.

## 1. Top Board (LEDs and Touch)
The top daughterboard controls the volume touch sensors and the 4 RGB LEDs. It uses a **Cypress CapSense** controller communicating via **I2C**.

### Pinout (Verified)
Based on PCB markings (Model H0A), the connector has the following pinout:
1.  **GND**: Ground
2.  **SCL**: I2C Clock
3.  **SDA**: I2C Data
4.  **3V3**: 3.3V Logic Power (Powers the Cypress chip)
5.  **WIFI_DC5V**: 5V Power (Powers the RGB LEDs)

### Wiring to Raspberry Pi Zero 2 W
*   **3V3** -> RPi Pin 1 (3.3V)
*   **WIFI_DC5V** -> RPi Pin 2 (5V)
*   **GND** -> RPi Pin 6 (GND)
*   **SDA** -> RPi Pin 3 (GPIO 2 / SDA)
*   **SCL** -> RPi Pin 5 (GPIO 3 / SCL)

### Software
Use `i2cdetect -y 1` or the provided `scripts/probe_i2c.py` to scan for the device address.

## 2. Speaker
The device contains a custom 40mm speaker driver.
*   **Connector:** 2-Pin JST (Red/Black wires).
*   **Impedance:** Likely 4 Ohm.
*   **Amplification:** Requires an external amplifier. Do not connect directly to GPIO.
*   **Recommended Amp:** MAX98357A (I2S Mono Amplifier).
    *   **Wiring:**
        *   Amp VIN -> 5V
        *   Amp GND -> GND
        *   Amp BCLK -> RPi GPIO 18 (Pin 12)
        *   Amp LRC -> RPi GPIO 19 (Pin 35)
        *   Amp DIN -> RPi GPIO 21 (Pin 40)
        *   Speaker + -> Red Wire
        *   Speaker - -> Black Wire

## 3. Power (USB Port)
The device is powered via a Micro-USB port on a small breakout board.
*   **Connector:** 2-Pin Cable (Red/Black).
*   **Function:** Purely for power input (VBUS/GND). Data lines are not broken out on this board.
*   **Usage:**
    *   Connect the Red wire to the **5V** input of your new MCU/SBC.
    *   Connect the Black wire to **GND**.
    *   This allows you to power the new "brain" using the original power cable and port.

## 4. Mute Switch
The physical slider switch.
*   **Type:** SPST or SPDT.
*   **Wiring:** Connect one side to Ground, the other to a GPIO pin with an internal Pull-Up resistor.
