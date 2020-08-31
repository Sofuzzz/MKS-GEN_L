Tmc2209 have all function of tmc2208,can completely replace tmc2208. At the same time,tmc2209 have better heat dissipation,support bigger current,support sensorless-homing function.

# How to buy
- MKS TMC2209 on Aliexpress  [MKS TMC2209](https://www.aliexpress.com/item/33043140087.html)

# Video Tutorials
- MKS TMC2209 V2.0 used on MKS GEN_L. It can be referred to [Use tutorial](https://www.youtube.com/watch?v=eF8Mqa2Y3oo)

# Notice
- TMC2209 default direction opposite to A4988/DRV8825, if you change from A4988 to TMC2209 ,maybe need edit fireware
    - Configuration.h:#define INVERT_X_DIR  false-->true   or true-->false

- If you don't use sensorless-homing function, remove jumper cap from here:

![MKS_GEN_L_V2_SENSORLESS_HOMING](https://github.com/makerbase-mks/MKS-GEN_L/blob/master/hardware/Image/MKS_GEN_L_V2_SENSORLESS_HOMING.png)

# Dir/step mode set
- Setting method of jumper cap can be referred to [Use tutorial](https://www.youtube.com/watch?v=eF8Mqa2Y3oo),microstep setting recommend 16.
 ```
  MKS TMC2209
 M0  | M1  | Microstep Setting
 GND | GND | 8 microsteps
 VCC | GND | 32 microsteps
 GND | VCC | 64 microsteps
 VCC | VCC | 16 microsteps
  GND = Jumpers open               VCC = Jumpers connection
  ```

- Driver current regulation
  - Verf measures the voltage of Gnd and potentiometer middle
  - Please DO NOT connect the motors when measuring the voltage, or it's easy to burn the drive
  - Please connect the power supply when measuring voltage as well, do not connect only the USB power
  - I=Vref    Default I=1.25A

# Uart mode set(Only MKS GEN_L V2.1 support)
- Setting method of jumper cap can be referred to [Use tutorial](https://www.youtube.com/watch?v=eF8Mqa2Y3oo)
  ```
  TMC UART moder set
     O O O  M0
     O O O  M1
     O=O O  M2
     O O 
  ```
- Uart mode firmware set(Take X axis as example)
  - Enable EEPROM to store parameters set by LCD
    -  Configuration.h:#define EEPROM_SETTINGS
  - Enable uart mode
    -  Configuration.h:#define X_DRIVER_TYPE  TMC2209
  - Set current and microsteps
    -  Configuration_adv.h:#define X_CURRENT       800   //Set current to 800*1.414 ma,peak current=Value*1.414
    -  Configuration_adv.h:#define X_MICROSTEPS    16    //Set MICROSTEPS, 16 recommended
  - Enable low-speed Stealthchop,high-speed Spreadcycle
    -  Configuration_adv.h:#define HYBRID_THRESHOLD      //enable HYBRID_THRESHOLD
    -  Configuration_adv.h:#define X_HYBRID_THRESHOLD     100  //Set the speed of mode conversion

- Uart mode test
  - You can send to the board  M122 test uart mode is ok or not(need enable #define TMC_DEBUG in configuration_adv.h file). If not ok,you will get nothing,if ok,you will get info like this: 
    ```
    Testing X connection... OK
    Testing Y connection... OK
    Testing Z connection... OK
    Testing E connection... OK
    ```
   - **Note: You must use DC12-24V power supply, not just USB power supply. Otherwise, TMC will report an error**

- Change parameter and save
  - By LCD12864: 
    - Change parameter: **Configuration** -> **Advanced Settings** -> **TMC Drivers** 
    - Save parameter: **Configuration** -> **Store Settings**
    - Load parameter: **Configuration** -> **Load Settings**

  - By MKS TFT35: 
    - Change parameter: **Settings** -> **Config** -> **Motor** -> **TMC currentsetting** 
    - Save parameter: **Settings** -> **Config** -> **Gcode**  send M500
    - Load parameter: **Settings** -> **Config** -> **Gcode**  send M501

  - By repetier(Pronterface..):
    - Send M906 setting current, for example, M906 X500 setting x-axis current is 500ma
    - Send M500 save parameter
    - Send M501 load parameter

# Sensorless-homing Set(Only MKS GEN_L V2.1 support)
- Setting method of jumper cap can be referred to [Use tutorial](https://www.youtube.com/watch?v=eF8Mqa2Y3oo)
    - Jumper cap set **uart mode**
    - Jumper cap set "**Drive IC Power:3.3V**"
    - Jumper cap set "**X-**"

- Sensorless-homing firmware set(Take X axis as example)
    - First you need finish uart mode firmware setting,after that, you need set:1.Change CHOPPER_TIMING CHOPPER 2.Enable Sensorless_homing 3.Change X_STALL_SENSITIVITY    
    - Set the default voltage to DC supply voltage
      - Configuration_adv.h：#define CHOPPER_TIMING CHOPPER_DEFAULT_12V //According to DC supply
    - Set Enable SENSORLESS_HOMING
      - Configuration_adv.h：#define SENSORLESS_HOMING 
    - Set blocking threshold,more bigger more sensitive
      - Configuration_adv.h：#define X_STALL_SENSITIVITY  **125** //According to your 3d printer
