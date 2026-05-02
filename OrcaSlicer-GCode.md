# Machine Start G-Code:
```
; OrcaSlicer auto-heating suppression:
; M190 S[bed_temperature_initial_layer_single]
; M109 S[nozzle_temperature_initial_layer[initial_tool]]
M140 S0
M104 S0
START_PRINT_M3DP EXTRUDER_TEMP=[nozzle_temperature_initial_layer[initial_tool]] BED_TEMP=[bed_temperature_initial_layer_single] CHAMBER_TEMP=[chamber_temperature[initial_tool]] ADAPTIVE=1 FILAMENT_TYPE="{filament_type[initial_tool]}" PRINT_MIN={first_layer_print_min[0]},{first_layer_print_min[1]} PRINT_MAX={first_layer_print_max[0]},{first_layer_print_max[1]}
T[initial_tool]
M204 S2000
G1 Z3 F600
M83
G1 Y150 F12000
G1 X0 F12000
G1 Z0.2 F600
G1 X0 Y0 E15 F6000
G1 X150 Y0 E15 F6000
G92 E0
G1 E-0.5 F2400 ; Snap retraction to prevent stringing
G1 Z1 F600
```

# Machine End G-Code:
```
END_PRINT
```

# Filament Change G-Code:
```
;BEFORE_LAYER_CHANGE
;[layer_z]
G92 E0

```

# Change Filament G-Code:
```
G2 Z{z_after_toolchange + 0.4} I0.86 J0.86 P1 F10000 ; spiral lift a little from second lift
G1 X0 Y245 F30000
G1 Z{z_after_toolchange} F600
```

# Pause Print G-Code:
```
PAUSE
```

