# How to buy
- MKS TFT35 on Aliexpress  [MKS TFT35](https://www.aliexpress.com/item/32891320510.html)

- MKS TFT70 on Aliexpress  [MKS TFT70](https://www.aliexpress.com/item/32890948123.html)

# Video Tutorials
- Used MKS TFT35 on MKS GEN_L. It can be referred to [MKS TFT35 test](https://www.youtube.com/watch?v=EWMw57MFD3c)

# Motherboard connect
- MKS TFT35 and TFT70 connect MKS GEN_L motherboard by **AUX-1**

# Test
- MKS TFT35 and MKS GEN_L each has its own firmware. Before test, MKS TFT35 and MKS GEN_L must have refresh firmware.

- Marlin setting, you need change parameters suitable for communication with MKS TFT35:
    - Set #define SERIAL_PORT **0**  in configuration.h
    - Set #define BAUDRATE 250000 same as MKS TFT

- When testing or using MKS TFT35, MKS GEN_L should not be connected with USB cable because of serial port conflict

- Test process
  - Send Gcode M114 by MKS TFT35: **Settings** -> **Config** -> **Gcode**  send M114
  - If not ok, you will get nothing, change **Baud rate**:**Settings** -> **Config** -> **Baud rate config** 
  - Then send Gcode M114 again,until you get info like this: 
```
        OK
        X:0.00 Y:0.00 Z:0.00 E:0.00 Count X:0 Y:0 Z:0
        OK 
```
  - If always unsuccessful, maybe you need refresh firmware of the motherboard.
