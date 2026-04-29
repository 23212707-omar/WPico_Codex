# Raspberry Pi Pico W Keypad + LED Matrix Project

## Overview
This repository provides a clean Raspberry Pi Pico W project layout and documentation for the supplied Wokwi design.

> **Important:** No `main.py` or `main.cpp` firmware source was included in the provided input block, so this update focuses on repository structure and documentation only (no application logic changes).

The hardware diagram describes:
- A **4x4 membrane keypad** wired to GPIO pins.
- A **12-LED output bank** (8 blue LEDs labeled `1..8` and 4 red LEDs labeled `A..D`), each with a series resistor.
- Pull-up resistor network for keypad row lines.

## Proposed Repository Structure (MicroPython)

```
.
├── README.md
├── src/
│   └── main.py            # Place your existing firmware logic here (unchanged)
├── lib/                   # Optional MicroPython helper modules
└── docs/
    ├── architecture.md
    └── wiring.md
```

If your project later uses Pico SDK C/C++, a parallel structure would be:

```
.
├── CMakeLists.txt
├── include/
├── src/
└── docs/
```

## Features (as inferred from the supplied wiring)
- 4x4 keypad scanning input (4 columns + 4 rows).
- 12 discrete LED outputs for status/feedback.
- UART serial monitor pins connected (GP0/GP1) in Wokwi.
- Pico W target compatibility (RP2040 + optional Wi-Fi capability in firmware).

## Components List (from `diagram.json`)
- 1x Raspberry Pi Pico / Pico W (`wokwi-pi-pico`)
- 1x 4x4 membrane keypad (`wokwi-membrane-keypad`)
- 12x LEDs
  - 8x blue (`1..8`)
  - 4x red (`A..D`)
- 12x LED current-limiting resistors (220Ω)
- 4x keypad pull-up resistors (1kΩ)

## GPIO Pin Mapping Summary

### Keypad
- Columns:
  - C4 -> GP16
  - C3 -> GP17
  - C2 -> GP18
  - C1 -> GP19
- Rows:
  - R4 -> GP20
  - R3 -> GP21
  - R2 -> GP22
  - R1 -> GP26

### LEDs
- Numeric LEDs:
  - `8` -> GP4
  - `7` -> GP5
  - `6` -> GP6
  - `5` -> GP7
  - `4` -> GP8
  - `3` -> GP9
  - `2` -> GP10
  - `1` -> GP11
- Alpha LEDs:
  - `A` -> GP3
  - `B` -> GP2
  - `C` -> GP28
  - `D` -> GP27

## Running in Wokwi
1. Create a new Raspberry Pi Pico / Pico W simulation.
2. Paste the provided `diagram.json` into `diagram.json` in the Wokwi project.
3. Add your unchanged firmware to `src/main.py` (or adapt Wokwi file path expectations).
4. Start simulation and open serial monitor if needed.

## Running on Real Hardware (Pico W)
1. Flash MicroPython UF2 to Pico W (if not already installed).
2. Copy your firmware to the board as `main.py` (and optional modules under `lib/`).
3. Wire components exactly as documented in `docs/wiring.md`.
4. Power via USB and validate keypad input and LED outputs.

## Wi-Fi Notes (if your firmware uses Wi-Fi)
- Do **not** hardcode credentials in version-controlled files.
- Recommended pattern: keep credentials in a separate local file (e.g., `secrets.py`) excluded by `.gitignore`.
- Example interface (no real secrets):

```python
# secrets.py (local only)
WIFI_SSID = "YOUR_SSID"
WIFI_PASSWORD = "YOUR_PASSWORD"
```

## Assumptions & Clarifications
The student text describes an I2C LCD + DHT22 wiring, but these components do **not** appear in the supplied Wokwi `parts` list.
This documentation therefore prioritizes the explicit `diagram.json` netlist as the source of truth.
