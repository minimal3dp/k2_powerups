# Creality K2 Plus Powerups

Repo to test my ideas for improving the leveling and print start for the Creality K2.

**Firmware Compatibility**: Tested and compatible with Creality K2 Firmware `v1.1.4.11`

## Reasoning

As I have started to work with high temp filaments, I have noticed issues and deficiencies with the printer. One of the silly issues is the fact that chamber heating takes forever (if it actually reaches the target temp) with forced probe enables.

I really, really want to have to root my printer. Rooting has implications to the printer warranty.

## References

- [K2 Firmware Extracts](https://github.com/Guilouz/Creality-K2Plus-Extracted-Firmwares)
- [K2 Improvements](https://github.com/jamincollins/k2-improvements)
- [K2 Leveling](https://github.com/DnG-Crafts/K2-Leveling/blob/main/bl_macros.cfg)

## Fixes

### Config Fixes

[Turn off Auto Bed Level for every print](https://forum.creality.com/t/k2-plus-performs-auto-calibrate-even-when-disabled/25925/9) - in printer.cfg, change:

```bash
forced_leveling: true ## change this to false
```

[Enable Adaptive Meshing (Fix internal error on BED_MESH_CALIBRATE)]() - in `printer.cfg`, make the following two changes:
1. Under the `[prtouch_v3]` section, change `enable_not_linear_comp` to `False`:
```bash
enable_not_linear_comp:False # changed from True to allow dynamic adaptive mesh counts
```
2. Under the `[bed_mesh]` section, change `probe_count` to `5,5`:
```bash
probe_count:5,5 # changed from 9,9 to speed up probing and satisfy PRTouch spiral probing
```

### DXC2 Extruder Changes

Go to the Configuration interface, find and open the
gcode_macro.cfg file.
Locate [gcode_macro QUIT_MATERIAL_RETRUDE_MATERIAL]
and change the retraction speed to E-40 (as shown in the
diagram).
Click Save & Restart in the top-right corner

Find and open the box.cfg file.
Locate [box] and modify Tn_retrude to -20.
Comment out the original value by adding # in front (e.g.,
#Tn_retrude: -10). Commented lines will turn gray.
Final: Tn_retrude: -20

### Off Printer Fixes

[Creality Print Data Transfer](https://github.com/orgs/CrealityOfficial/discussions/126#discussioncomment-13184323) - use OctoPrint/Klipper protocol rather than CrealityPrint protocol

### M3DP Configuration

- **Add Screws Tilt Adjust**: Integration of the [Screws Tilt Adjust](https://github.com/jamincollins/k2-improvements/blob/main/features/screws_tilt_adjust/screws_tilt_adjust.cfg) feature.
- **Optimized Print Start Macro (`START_PRINT_M3DP`)**:
  - **Concurrent Heating**: Heats the bed, chamber, and extruder to wait-temp simultaneously to dramatically reduce print start times.
  - **Efficiency**: Removed redundant nozzle wiping and extra Z-homing routines.
  - **Adaptive Meshing**: Supports `ADAPTIVE=1` parameter to enable native adaptive bed meshing in Klipper.
  - **Heat Bump**: Supports `HEAT_BUMP=1` parameter to temporarily overshoot the bed temperature by 5°C, accelerating the chamber heating process for high-temp materials like ABS/ASA.
- **Improved Manual Leveling Macros**: 
  - Custom tramming macros (`A_1_LEFT_FRONT`, etc.) that heat the nozzle to a safe `wait_temperature` (140°C) instead of full print temp, completely eliminating filament ooze during leveling.
- **OrcaSlicer Integration**: Check `OrcaSlicer-GCode.md` for the optimized slicer configurations.