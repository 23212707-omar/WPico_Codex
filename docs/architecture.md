# Firmware Architecture Notes

## Goal
Document a maintainable project structure for Raspberry Pi Pico W firmware **without changing existing behavior**.

## Current State
- Firmware source code was not provided in the input block (`main.py` / `main.cpp` missing).
- Hardware definition is available via Wokwi netlist.

## Recommended MicroPython Layout

- `src/main.py`
  - Entry point with the original application logic (copy existing logic here unchanged).
- `lib/`
  - Optional helper modules (drivers, utilities) if your existing code already separates concerns.
- `docs/wiring.md`
  - Pin-level electrical mapping.
- `docs/architecture.md`
  - This architecture and integration guide.

## Suggested Module Responsibilities (when refactoring later)

> These are organizational suggestions only; do not apply if your goal is strict no-change migration.

- `src/main.py`
  - Initialization sequence, loop timing, and top-level orchestration.
- `lib/keypad.py`
  - Row/column scan function and key decode map.
- `lib/led_bank.py`
  - LED abstraction for writing patterns to 12 outputs.
- `lib/net.py` (optional)
  - Wi-Fi connect/reconnect helper if used by application logic.

## Runtime Flow (expected from wiring)
1. Configure keypad GPIOs and row pull-ups.
2. Configure LED GPIO outputs, default OFF.
3. Enter polling loop:
   - scan keypad,
   - map key event,
   - update LED pattern,
   - optionally log via UART/Wi-Fi.

## Wi-Fi Configuration Pattern (Optional)
If your `main.py` uses Pico W Wi-Fi:
- Keep credentials outside tracked source (`secrets.py`, excluded by `.gitignore`).
- Import credentials at boot.
- Implement retry logic with bounded timeout.

## Non-Functional Guidelines
- Preserve pin constants exactly to avoid wiring mismatches.
- Keep debounce timing explicit and documented.
- Use deterministic boot behavior (all outputs known state before main loop).
