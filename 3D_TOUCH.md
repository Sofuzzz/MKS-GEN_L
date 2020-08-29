# How to buy
- 3D Touch on Aliexpress  [3D Touch](https://www.aliexpress.com/item/32890485972.html)

# Video Tutorials
- If display is LCD12864. It can be referred to [LCD12864 3dtouch](https://www.youtube.com/watch?v=r2A0b7XQEaI)

- If display is MKS TFT35. It can be referred to [MKS TFT35 3dtouch](https://www.youtube.com/watch?v=CB1x841_WYo)

# Measure probe to nozzle offset
- Refer to video tutorials for measurement method

- The position of the probe in the coordinate system with the nozzle as the origin

- Z value shall be accurate, and can be adjustment by z-offset

# Connect motherboard

- 3D Touch work with z-axis endstop:

![3d_touch_normal](https://github.com/makerbase-mks/MKS-GEN_L/blob/master/hardware/Image/MKS_GEN_L_3DTOUCH.png)

- 3D Touch replace z-axis endstop:
  - You need connect it to Z- interface

# Firmware setting
- 1.Enable BLTOUCH for 3D Touch
    -  Configuration.h： #define BLTOUCH

- 2.Enable  AUTO_BED_LEVELING_BILINEAR
    -  Configuration.h： #define AUTO_BED_LEVELING_BILINEAR

- 3.Enable and set SERVOS number
    -  Configuration.h： #define NUM_SERVOS 1 

- 4.Set pin port for servos
    -  pins_RAMPS.h： #define SERVO0_PIN           11  // SERVO D11

- 5.Enable  EEPROM_SETTINGS for store parameters 
    -  Configuration.h：  #define EEPROM_SETTINGS  

- 6.Set endstop inverting type for 3D touch
    -  Configuration.h： #define Z_MIN_PROBE_ENDSTOP_INVERTING false

- 7.Set pin port of 3D touch connection
    -  Configuration.h：#define Z_MIN_PROBE_PIN 19

- 8.Set probe to nozzle offset to measurement before
    -  Configuration.h：#define NOZZLE_TO_PROBE_OFFSET { 10, 10, 0 } //Measure probe to nozzle offset

- 9.Set distance between probe and the edge of the hotbed to prevent the probe from exceeding the hotbed
    -  Configuration.h：#define MIN_PROBE_EDGE 10

- 10.Enable leveling range
    -  Configuration_adv.h
    ```
    #if PROBE_SELECTED && !IS_KINEMATIC
      #define MIN_PROBE_EDGE_LEFT MIN_PROBE_EDGE
      #define MIN_PROBE_EDGE_RIGHT MIN_PROBE_EDGE
      #define MIN_PROBE_EDGE_FRONT MIN_PROBE_EDGE
      #define MIN_PROBE_EDGE_BACK MIN_PROBE_EDGE
    #endif
    ```

- 11.Set the number of grid points 3*3 
    -  Configuration.h：#define GRID_MAX_POINTS_X 3
- 12.Add  "**set_bed_leveling_enabled(true);**" at the end of file:"**src -> gcode -> calibrate -> G28.cpp**" 

# 3D Touch replace z-axis endstop
-  According to the "3D Touch replace z-axis endstop" requirements Connect motherboard

-  Firmware setting(after normal firmware setting)
   - Configuration.h 
      -  Enable: #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
      -  Enable: #define Z_SAFE_HOMING
      -  Disable: //#define Z_MIN_PROBE_PIN 19

# Adjust Z offset
-  Z offset is required accurate,the measured value may not be accurate enough, so Z offset adjustment is needed
-  If the distance between nozzle and hotbed is too large, Z offset (negative) need increase, such as: - 0.68 -- > - 1.25
-  If the distance between nozzle and hotbed is too small, Z offset (negative) needs to be reduced
-  After adjustment, store settings, load settings ,and test again
-  Test several times to ensure that the value of Z offset is appropriate

# How to use it
-  After a successful autolevel, save  parameters, no need level again
-  After using for a period of time, if there is a leveling problem, can be autolevel and save parameters again