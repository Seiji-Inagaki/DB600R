# Changelog

Version history of `printer.cfg` for the DB600R.

The version is written in the header of `printer.cfg` (`# version: ...`). Released versions are tagged in this repository.

Versioning rules:

- A version is released only when every bring-up test that can change a hand-set value has passed.
- **1.x** (e.g. 1.0 → 1.1): a change of configuration (hardware, pins, features).
- **1.0.x** (e.g. 1.0 → 1.0.1): a correction of hand-set values, or comments only.
- Calibration values (probe `z_offset`, heater PID, bed mesh) are written by `SAVE_CONFIG` into the block at the end of `printer.cfg`. They are measured, not hand-set, and **re-calibration does not change the version**. The values at each release are noted in this file for comparison.

## 0.9 — 2026-10-04 (testing)

The filament sensor test during a print is still to be done.

Coordinates (the toolhead mount was moved on the carriage; all values measured again):

- `[z_tilt] z_positions`: `690, 305` / `-125, 305` → **`700, 305` / `-100, 305`**.
- `[stepper_y] position_max`: 615 → **588**. With the current toolhead, the carriage hits the rear end at about Y = 590.
- `clean_nozzle.cfg`: `variable_start_x` 17 → **37** (brush center).

Bed leveling:

- `[bed_mesh]`: added `zero_reference_position: 300, 300`.
- Added `[screws_tilt_adjust]` for the six bed springs (M3), `screw_thread: CCW-M3`.

Extruder:

- `[extruder] dir_pin`: `!PD6` → **`PD6`**. The extruder turned in the retract direction.
- `[extruder] rotation_distance`: 47.088 → **48.030** (100 mm commanded, measured with PETG).

Calibration, written by `SAVE_CONFIG` (the starting values carried over from the Leviathan were removed from the body):

- probe `z_offset` **−0.529**, nozzle and bed cold
- extruder PID at 240 °C: **Kp 40.043 / Ki 4.603 / Kd 87.093**
- bed PID at 65 °C: **Kp 76.556 / Ki 0.555 / Kd 2641.165**
- bed mesh `default`, 3 × 3, **range 0.079 mm**, 10 minutes after the bed reached 65 °C, after adjusting the bed springs

Other:

- Rewrote all comments in `printer.cfg` in English, as short labels.
- Added `README.md` and this `CHANGELOG.md`.
- Removed configurations from the Leviathan era (`printer.cfg.em`, `printer.cfg.microprobe`) and stopped tracking a Moonraker backup and a G-code archive.

## 0.8 — 2026-09-29 (`2834318`)

- Added the two sections for the BTT SFS V2.0 filament sensor: `[filament_switch_sensor switch_sensor]` and `[filament_motion_sensor encoder_sensor]`, both with `pause_on_runout: True`.
- Removed `stealthchop_threshold: 0` from X/Y and Z0/Z1. All four drivers now run in spreadCycle only.

## 0.7 — 2026-09-28 (`a4bc471`)

- Controller box fan on FAN5 (PB7) moved to **FAN2 (PB2)**. The FAN5 port circuit has failed: the port conducts regardless of the MCU output.

## 0.6 — 2026-09-21 (`370ea18`)

- `[stepper_x] dir_pin`: `!PE10` → **`PE10`**. X moved toward the endstop on a positive move.

## 0.5 — 2026-09-21 (`e2eaf13`)

- Removed `tachometer_pin` / `tachometer_ppr` from the hotend fan. The tach output of this fan does not work.

## 0.4 — 2026-09-20 (`1a6cc06`)

- Thermistor `pullup_resistor`: 2200 → **4700** for all three thermistors. The Spider V3.0 uses 4.7k pull-ups; 2200 was carried over from the Leviathan.

Versions 0.2 and 0.3 existed only on the Raspberry Pi and were not committed. Their net change is included in 0.4.

## 0.1 — 2026-09-20 (`ce345cd`)

- First configuration for the FYSETC Spider V3.0, migrated from the LDO Leviathan V1.3. Pin assignments only; values were carried over and verified later.

The last configuration on the Leviathan is commit `eda8b7e` (2026-09-19).
