# DB600R

Klipper configuration of the DB600R, a self-built large-format 3D printer. It is a one-off machine; the configuration is shared as a reference for anyone building a printer of this size.

- Cartesian kinematics, moving bed, nominal size 600 × 600 × 600 mm
- Controller: FYSETC Spider V3.0 (STM32F446, TMC2209 drivers in UART mode), migrated from the LDO Leviathan V1.3 in September 2026
- Host: Raspberry Pi 4B with Klipper, Moonraker and Mainsail
- Toolhead: StealthBurner with E3D Revo hotend, 0.6 mm nozzle
- Filament sensor: BTT SFS V2.0

Version history: [CHANGELOG.md](CHANGELOG.md)

## Files

| File | Content |
|---|---|
| `printer.cfg` | Main configuration. The version is in its header |
| `clean_nozzle.cfg` | `CLEAN_NOZZLE` macro (nozzle brush on the bed) |
| `client.cfg` | Mainsail client variables (`_CLIENT_VARIABLE`): pause and park behavior |
| `moonraker.conf`, `crowsnest.conf`, `sonar.conf` | Moonraker, webcam and Wi-Fi keepalive services |

`mainsail.cfg` is provided by `mainsail-config` and is not tracked here.
