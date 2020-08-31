# How to buy
- MKS FES on Aliexpress  [MKS FES](https://www.aliexpress.com/item/32853300525.html)

# Video Tutorials
- If display is LCD12864. It can be referred to [LCD12864 FES](https://www.youtube.com/watch?v=6Hk5Zk_G968)

- If display is MKS TFT35. It can be referred to [MKS TFT35 FES](https://www.youtube.com/watch?v=LYCn9KCoLLA)

# Working process
- The material detection module MKS FES uses the level transition detection method. When with material in, the detection level signal should be high, and when no material, the material port level signal goes low. When the system detects a determined transition from high to low level, it will regard it as the material exhausted, then the board executes the pause command operation, and after the replacement of the material, it will continue to print.

# Wiring:
- Used with MKS TFT35:Connect to “PB1” on MKS TFT display;

- Used with LCD12864:Connect to "Z+ endstop" on MKS GEN_L Board:
  
# How to use
- Work with MKS TFT35
  - Parameter setting
    - MKS FES on MKS TFT35, you need connect to PB1
    - Settings -> Config -> Adavance -> Next -> PB1_trigger_Level = Low
    - Settings -> Config -> Adavance -> Next -> disable PB0 and PB1 function = NO

  - Usage method
    - If the material is interrupted or out of material during printing, it will be triggered and enter the pause interface
    - You need reload supplies and resume printing

- Work with LCD12864
  - MKS GEN_L Firmware setting
    - In configuration.h
      - Enable #define FILAMENT_RUNOUT_SENSOR
      - Enable #define NOZZLE_PARK_FEATURE
  
    - In pins_RAMPS.h
      - Add #define FIL_RUNOUT_PIN     19 //You can change to other pin

    - In confiuration_adv.h
      - Enable #define ADVANCED_PAUSE_FEATURE

  - Usage method
    - If the material is interrupted or out of material during printing, it will be triggered and enter the pause interface
    - You need reload supplies and resume printing