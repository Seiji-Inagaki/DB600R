# Changelog

Version history of `printer.cfg` for the DB600R.

The version is written in the header of `printer.cfg` (`# version: ...`). Released versions are tagged in this repository (`v1.0`, `v1.0.1`, ...).

Versioning rules:

- **1.x** (e.g. 1.0 → 1.1): a change of configuration (hardware, pins, features).
- **1.0.x** (e.g. 1.0.1 → 1.0.2): a correction of hand-set values, or comments only.
- Calibration values (probe `z_offset`, heater PID, bed mesh) are written by `SAVE_CONFIG` into the block at the end of `printer.cfg`. They are measured, not hand-set, and **re-calibration does not change the version**. The values at each release are noted in this file for comparison.

## 1.0.3 — 2026-10-03

Comments and display names only. No setting value was changed.

- Rewrote all comments in `printer.cfg` in English, as short labels.
- Removed the old starting values that `SAVE_CONFIG` had commented out. They were the values measured on the Leviathan: probe `z_offset` −0.312 (different probe), extruder PID Kp 38.422 / Ki 4.199 / Kd 87.890, bed PID Kp 76.177 / Ki 0.656 / Kd 2211.034.
- Renamed the six `[screws_tilt_adjust]` screws to English (`front center`, `front left`, `front right`, `rear left`, `rear center`, `rear right`). This changes only the names shown by `SCREWS_TILT_CALCULATE`.
- Added `README.md` and this `CHANGELOG.md`.

## 1.0.2 — 2026-10-02 (`359d892`)

- `[stepper_y] position_max`: 615 → **588** (`a439bd0`). With the current toolhead, the carriage hits the rear end at about Y = 590. 615 was the value for the previous toolhead.
- `[bed_mesh]`: added `zero_reference_position: 300, 300` (`8e4acdf`).
- Added `[screws_tilt_adjust]` for the six bed springs (`b794285`). `screw_thread: CCW-M3` (`5e007c8`).
- First calibration on this board, written by `SAVE_CONFIG`:
  - probe `z_offset` **−0.529**, nozzle and bed cold (`74aab58`)
  - extruder PID at 240 °C: **Kp 40.043 / Ki 4.603 / Kd 87.093** (`8b0c94a`)
  - bed PID at 65 °C: **Kp 76.556 / Ki 0.555 / Kd 2641.165** (`1ef97aa`)
  - bed mesh `default`, 3 × 3, **range 0.079 mm**, 10 minutes after the bed reached 65 °C, after adjusting the bed springs (`335705c`)

## 1.0.1 — 2026-09-30 (`7917cae`)

The toolhead mount was moved on the carriage, so all X coordinates of objects fixed to the bed changed. They were measured again.

- `[z_tilt] z_positions`: `690, 305` / `-125, 305` → **`700, 305` / `-100, 305`** (`d785e23`).
- `clean_nozzle.cfg`: `variable_start_x` 17 → **37** (`557687a`).

## 1.0 — 2026-09-29 (`124dacf`)

First released version on the Spider V3.0. All bring-up tests up to this point passed.

- Added the two sections for the BTT SFS V2.0 filament sensor: `[filament_switch_sensor switch_sensor]` and `[filament_motion_sensor encoder_sensor]`, both with `pause_on_runout: True` (`9710a69`).
- Removed `stealthchop_threshold: 0` from X/Y (`b6c3c0e`) and Z0/Z1 (`2834318`). All four drivers now run in spreadCycle only.

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
