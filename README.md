# ⚡ Ultra-Precision Voltage & Current Measurement System

[![GitHub Stars](https://img.shields.io/github/stars/Nithur8/Embedded_system-for-Voltage-and-Current-measurement-?style=social)]()
[![Forks](https://img.shields.io/github/forks/Nithur8/Embedded_system-for-Voltage-and-Current-measurement-?style=social)]()
[![Issues](https://img.shields.io/github/issues/Nithur8/Embedded_system-for-Voltage-and-Current-measurement-)]()

A compact, accurate Voltage and Current measuring device built around an STM32 microcontroller. Designed for hobbyists and makers who need a portable measurement module that displays real-time values on an LCD.

Demo: ![Demo GIF](https://github.com/user-attachments/assets/61e199e1-2385-4c09-8ab0-07f0f0dae34b)

---

## Table of Contents
- [About](#about)
- [Features](#features)
- [Hardware Components](#hardware-components)
- [Circuit Diagram & Images](#circuit-diagram--images)
- [How It Works](#how-it-works)
  - [Voltage Measurement](#voltage-measurement)
  - [Current Measurement](#current-measurement)
- [Wiring & Pinout](#wiring--pinout)
- [Build & Flash](#build--flash)
- [Calibration & Accuracy](#calibration--accuracy)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## About
This project measures up to 12V and associated load current using an STM32F411-based development board. Values are scaled and conditioned so the MCU ADC can read them safely and reliably, then displayed on an LCD over I2C.

---

## Features
- Real-time voltage and current readings
- LCD display (I2C)
- Voltage divider to safely measure up to 12V
- Shunt resistor + amplifier for precise current sensing
- Low-cost, high-efficiency LM2596 buck regulator for stable 5V supply
- Designed for hobbyist-friendly assembly and calibration

---

## Hardware Components
- STM32F411 development board (Black Pill)
- ST-Link debugger (for flashing)
- Character or graphical LCD with I2C backpack
- Operational amplifier: LM358P
- Buck regulator: LM2596S
- Resistors: 22K, 4.7K, 10K, 3.9K, 1K (and shunt resistor as specified)
- Shunt resistor (low-value, precision)
- Misc: headers, wires, perfboard/PCB, power source (7.2V battery pack or equivalent)

---

## Circuit Diagram & Images
Circuit diagram (schematic):

![Circuit Diagram](https://github.com/user-attachments/assets/1b247d85-6254-4534-a26c-9a80b80c046a)

Project photo / PCB / setup:

![Project Photo](https://github.com/user-attachments/assets/8d0f93d1-3edf-4fa0-a058-36b077575d61)

Demo:  
https://github.com/user-attachments/assets/61e199e1-2385-4c09-8ab0-07f0f0dae34b

---

## How It Works

### Voltage measurement
- The input voltage (Vin) is reduced using a voltage divider so that the ADC sees a maximum of 3.3V when Vin = 12V.
- Example: choose R1 and R2 so Vout = Vin * (R2 / (R1 + R2)). For a 12V → 3.3V conversion, ratio ≈ 0.275 (design values shown in the schematic).

ADC reading → convert to voltage:
Vmeasured = ADC_read / ADC_max * Vref * scale_factor

where scale_factor = (R1 + R2) / R2

### Current measurement
- A precision shunt resistor is placed in series with the load. The tiny voltage across it is amplified by LM358P and fed to the ADC.
- Amplifier gain is set so the amplifier output stays within the ADC range at the expected maximum current.

I = Vshunt / Rshunt
Vshunt = (ADC_read / ADC_max) * Vref / amplifier_gain

---

## Wiring & Pinout (example)
- STM32F411 - LCD(I2C): SDA → PB7, SCL → PB6 (verify with your board)
- Shunt output (amplified) → Analog input (e.g., PA0)
- Voltage divider output → Analog input (e.g., PA1)
- LM2596 5V out → VCC (STM32 + LCD)
- Ground common between all modules

(Confirm pins for your exact Black Pill board and update as needed.)

---

## Build & Flash
1. Install toolchain (STM32CubeIDE, PlatformIO, or arm-none-eabi + make).
2. Open the project in your chosen IDE or build from CLI.
3. Flash with ST-Link:
   - Example with OpenOCD/STM32CubeProgrammer or PlatformIO:
     - Using PlatformIO: `pio run -t upload`
     - Using STM32CubeProgrammer GUI: connect ST-Link, select .bin/.hex, and program.
4. Power the system and verify the LCD shows values.

If you want, I can add a platform-specific build section (PlatformIO, CubeMX project, or Makefile).

---

## Calibration & Accuracy
- Voltage: verify with a multimeter using known reference voltages (e.g., 1.0V, 5.0V, 12.0V) and adjust scale_factor in firmware.
- Current: use a known load (or electronic load) and compare measured current to a calibrated meter. Adjust shunt resistance and amplifier gain in code or hardware as needed.
- Use averaging/digital filtering in firmware to reduce fluctuations (simple moving average or low-pass filter).

---

## Usage
- Power on the device.
- LCD displays Voltage and Current continuously.
- If values fluctuate, allow a short warm-up time and ensure stable power and common ground.

---

## Troubleshooting
- No display: check I2C address, wiring (SDA/SCL), and contrast potentiometer on LCD backpack.
- ADC saturates: verify voltage divider and amplifier gain; ensure no over-voltage to ADC pins.
- Fluctuating readings: add decoupling caps near op-amp and ADC reference; add averaging in firmware.

---

## FAQ
Q: Why use the STM32 Black Pill vs Blue Pill?  
A: Black Pill often has newer MCU variants (e.g., STM32F4-series) with better ADC performance and more pins—use what matches your ADC resolution and features.

Q: Why metal film resistors?  
A: Metal film resistors offer better tolerance, lower noise, and higher stability than carbon resistors—important for precise measurements.

Q: Why LM2596 buck converter?  
A: Efficient, inexpensive, and widely available regulator with adjustable output and reasonable current capability for the MCU + LCD.

Q: Why a shunt resistor + amplifier?  
A: The shunt provides a low-voltage proportional to current; the amplifier brings that voltage into ADC range without significantly loading the circuit.

---

## Contributing
Contributions welcome! Suggested improvements:
- Add PCB design files (EAGLE / KiCad)
- Add example firmware for different STM32 variants
- Add unit tests/CI for conversion functions

Please open issues or PRs.

---

## License
Specify your license here (e.g., MIT). If you want, tell me which license to add and I will include the badge and LICENSE file.

---

## Credits
- Design & development: Your name / contributors
- Images: project photos and schematic assets

---

If you'd like, I can now:
- Commit this README to the repo (confirm branch: `main`) and push it, or
- Create a PR instead so you can review changes before merging.

Tell me which you prefer and I’ll proceed.
