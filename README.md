# Creality K2 Plus Powerups

Repo to test my ideas for improving the leveling and print start for the Creality K2

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

### Off Printer Fixes

[Creality Print Data Transfer](https://github.com/orgs/CrealityOfficial/discussions/126#discussioncomment-13184323) - use OctoPrint/Klipper protocol rather than CrealityPrint protocol

### M3DP Configuration

- [Add Screws Tilt Adjust](https://github.com/jamincollins/k2-improvements/blob/main/features/screws_tilt_adjust/screws_tilt_adjust.cfg)
- [Add updated Start Code]()