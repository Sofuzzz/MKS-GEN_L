MKS TMC2208 and MKS TMC2225 are used in exactly the same way.The only difference between TMC2225 and TMC2208 is package.The package of TMC2225 is HTSSOP,and the package of TMC2208 is QFN, so TMC2225 have better heat dissipation performance.

# How to buy
- MKS TMC2225 on Aliexpress  [MKS TMC2225](https://www.aliexpress.com/item/4001149124672.html)

- MKS TMC2208 on Aliexpress  [MKS TMC2208](https://www.aliexpress.com/item/32888980385.html)

# Video Tutorials
- MKS TMC2225 and MKS TMC2208 used on MKS GEN_L. It can be referred to [Use tutorial](https://www.youtube.com/watch?v=6RcrgmNvyeA)

# Dir/step mode set
- Setting method of jumper cap can be referred to [Use tutorial](https://www.youtube.com/watch?v=6RcrgmNvyeA),microstep setting recommend 16.
  ```
          MKS TMC2208                      MKS TMC2225                   
  M0  | M1  | Microstep Setting    M0  | M1  | Microstep Setting 
  GND | GND | 8 microsteps         GND | GND | 4 microsteps 
  VCC | GND | 2 microsteps         VCC | GND | 8 microsteps 
  GND | VCC | 4 microsteps         GND | VCC | 16 microsteps   
  VCC | VCC | 16 microsteps        VCC | VCC | 32 microsteps  
  GND = Jumpers open               VCC = Jumpeers connection
  ```
- Driver current regulation
  - Verf measures the voltage of Gnd and potentiometer middle
  - Please DO NOT connect the motors when measuring the voltage, or it's easy to burn the drive
  - Please connect the power supply when measuring voltage as well, do not connect only the USB power
  - I=Vref    Default I=1.25A

# Uart mode set(take X axis as example)
[Tips：**Use UART mode on MKS GEN_L V2 motherboard**]
- Setting method of jumper cap can be referred to [Use tutorial](https://www.youtube.com/watch?v=6RcrgmNvyeA)
  ```
  TMC UART moder set
     O O O  M0
     O O O  M1
     O=O O  M2
     O O 
  ```
- Uart mode firmware set
  - Enable EEPROM to store parameters set by LCD
    -  Configuration.h:#define EEPROM_SETTINGS
  - Enable uart mode
    -  Configuration.h:#define X_DRIVER_TYPE  TMC2208 //TMC2225 and TMC2208 setting method is the same
  - Set current and microsteps
    -  Configuration_adv.h:#define X_CURRENT       800 //Set current to 800*1.414 ma,peak current=Value*1.414
    -  Configuration_adv.h:#define X_MICROSTEPS    16  //Set MICROSTEPS, 16 recommended
  - Enable low-speed Stealthchop,high-speed Spreadcycle
    -  Configuration_adv.h:#define HYBRID_THRESHOLD           // enable HYBRID_THRESHOLD
    -  Configuration_adv.h:#define X_HYBRID_THRESHOLD     100 //Set the speed of mode conversion

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

# Notice
- TMC2208 and TMC2225 default direction opposite to A4988/DRV8825, if you change from A4988 to TMC2225 ,maybe need edit fireware
    - Configuration.h:#define INVERT_X_DIR  false-->true   or true-->false