# Hardware Interface Guide

## ⚠️ SAFETY WARNING ⚠️
**DO NOT connect the Top Board directly to 5V USB until you have verified the voltage logic levels.**
While some markings (`DN`, `DP`) suggest USB, other revisions of this hardware use **I2C at 3.3V**. Connecting a 3.3V device to 5V will destroy it.

## 1. Top Board (LEDs and Touch)
The top daughterboard controls the volume touch sensors and the 4 RGB LEDs.

### Step 1: Protocol Verification
Before wiring to a microcontroller, you must identify the protocol.
1.  **Check Markings:** Look closely at the connector `CN5A1`.
    *   If labeled `SDA`, `SCL`, `3V3`: It is **I2C**.
    *   If labeled `DP`, `DN`, `VBUS` (or similar): It *might* be USB, but could also be a differential serial protocol.
2.  **Multimeter Check:** With the device powered by its original power supply (if possible), measure the voltage on the data pins relative to GND.
    *   If signals are ~3.3V, treat as 3.3V logic.

### Wiring Option A: I2C (Most Likely for H0A)
*   **VCC:** Connect to **3.3V** (RPi Pin 1). **DO NOT CONNECT TO 5V**.
*   **GND:** Connect to Ground (RPi Pin 6).
*   **Data 1 (SDA?):** Connect to RPi SDA (GPIO 2 / Pin 3).
*   **Data 2 (SCL?):** Connect to RPi SCL (GPIO 3 / Pin 5).
*   **Software:** Use `i2cdetect -y 1` or the provided `scripts/probe_i2c.py` to scan for an address.

### Wiring Option B: USB (Only if verified)
*   **VBUS:** Connect to 5V.
*   **GND:** Connect to GND.
*   **D-:** Connect to USB D-.
*   **D+:** Connect to USB D+.

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
