# Wiring Reference (Raspberry Pi Pico W)

## Scope
This wiring document is derived directly from the supplied Wokwi `diagram.json` net connections.

## Power and Ground
- Pico `3V3` feeds a 4x 1kΩ pull-up resistor chain used by keypad row lines.
- Pico `GND.4` is common ground for all 12 LED cathodes.

## Keypad Wiring (4x4 Membrane)

| Keypad Pin | Pico W GPIO | Direction (typical) | Notes |
|---|---:|---|---|
| C4 | GP16 | Output/Input (scan) | Column line |
| C3 | GP17 | Output/Input (scan) | Column line |
| C2 | GP18 | Output/Input (scan) | Column line |
| C1 | GP19 | Output/Input (scan) | Column line |
| R4 | GP20 | Input (pull-up) | Row line + external 1k pull-up |
| R3 | GP21 | Input (pull-up) | Row line + external 1k pull-up |
| R2 | GP22 | Input (pull-up) | Row line + external 1k pull-up |
| R1 | GP26 | Input (pull-up) | Row line + external 1k pull-up |

### Pull-up Network
- `rp1..rp4` are 1kΩ resistors.
- One end of each resistor connects to row lines `R1..R4` respectively.
- Other ends are tied together and connected to `3V3`.

## LED Wiring
Each LED anode is driven from a GPIO pin through a 220Ω series resistor. All LED cathodes are tied to GND.

| LED Label | LED Color | Pico W GPIO | Series Resistor |
|---|---|---:|---:|
| 1 | Blue | GP11 | 220Ω |
| 2 | Blue | GP10 | 220Ω |
| 3 | Blue | GP9 | 220Ω |
| 4 | Blue | GP8 | 220Ω |
| 5 | Blue | GP7 | 220Ω |
| 6 | Blue | GP6 | 220Ω |
| 7 | Blue | GP5 | 220Ω |
| 8 | Blue | GP4 | 220Ω |
| A | Red | GP3 | 220Ω |
| B | Red | GP2 | 220Ω |
| C | Red | GP28 | 220Ω |
| D | Red | GP27 | 220Ω |

## UART / Serial Monitor (Simulation)
- GP0 -> Serial RX
- GP1 -> Serial TX

> Note: In real hardware, GP0/GP1 are UART0 pins. Avoid conflicts if firmware also expects I2C or other peripherals on those pins.

## Ambiguity Note
A separate student interpretation mentions an I2C LCD (GP0/GP1) and DHT22 (GP15). Those parts are not present in the provided Wokwi netlist, so they are not included in this canonical wiring map.
