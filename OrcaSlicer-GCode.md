# Machine Start G-Code:
```
M140 S0
M104 S0 
START_PRINT_M3DP EXTRUDER_TEMP=[nozzle_temperature_initial_layer] BED_TEMP=[bed_temperature_initial_layer_single] CHAMBER_TEMP=[chamber_temperature] ADAPTIVE=1 HEAT_BUMP=0
T[initial_no_support_extruder]
M204 S2000
G1 Z3 F600
M83
G1 Y150 F12000
G1 X0 F12000
G1 Z0.2 F600
G1 X0 Y0 E15 F6000
G1 X150 Y0 E15 F6000
G92 E0
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

