# How to buy
- MKS PWC on Aliexpress  [MKS PWC](https://www.aliexpress.com/item/32853300039.html)

# Video Tutorials
- If display is LCD12864. It can be referred to [LCD12864 PWC](https://www.youtube.com/watch?v=_5F-S-nQG0s)

- If display is MKS TFT35. It can be referred to [MKS TFT35 PWC](https://www.youtube.com/watch?v=LgAlTOVyiQk)

# Work with LCD12864
- Wiring:

![with 12864](https://github.com/makerbase-mks/MKS-GEN_L/blob/master/hardware/Image/MKS_GEN_L_PWC.png)

- Firmware setting
    -  In Configuration.h：
       - Enable #define PSU_CONTROL
       - Set #define PSU_ACTIVE_HIGH true

    -  Add the following text in pins_RAMPS.h：
    ```
    #if ENABLED(PSU_CONTROL)
    #ifndef PS_ON_PIN
      #define PS_ON_PIN         11    //PW_OFF, you can change it to other pin
    #endif
    #ifndef KILL_PIN
      #define KILL_PIN          2    //PW_DET, you can change it to other pin
    #endif
    #define KILL_PIN_INVERTING  true     //true : HIGH level trigger
    #endif
    ```

- How to use it
    -  Add " **M81** " at the end of the gcode file
    -  When the gcode file is printed,3d printer will automatically turning off

# Work with MKS TFT35
- Wiring:

![with tft35](https://github.com/makerbase-mks/MKS-GEN_L/blob/master/hardware/Image/MKS_GEN_L_PWC_TFT.png)

- MKS GEN_L firmware settings
    -  In Configuration.h：
       - Enable #define PSU_CONTROL
       - Set #define PSU_ACTIVE_HIGH true

    -  Add the following text in pins_RAMPS.h：
    ```
        #if ENABLED(PSU_CONTROL)
        #ifndef PS_ON_PIN
           #define PS_ON_PIN         11    //PW_OFF, you can change it to other pin
        #endif
    ```

- MKS TFT35 parameter setting
    -  Settings -> Config -> Advance -> power off dection module select **PWC**
    -  Settings -> Config -> Advance -> Auto Shutdown after print select **YES**

- How to use it
    -  When printing,Select Option in the print interface and set the PWC button Manual to Auto


