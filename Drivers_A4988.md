Use A4988 module on MKS Gen_L V1.0 and V2.x motherboard

# How to buy
- A4988 module on Aliexpress  [A4988](https://www.aliexpress.com/item/32888457440.html)

# MKS GEN_L M0-M2
  ```
  MKS GEN_L V1.0              MKS GEN_L V2.x
  M0 M1 M2                    O O=O  M0
  O  O  O                     O O=O  M1
  |  |  |                     O O=O  M2
  O  O  O                     O O
  ```

# Dir/step mode set
- Microstep Setting 
  ```
          A4988                             
  M0  | M1  | M2  | Microstep Setting
  GND | GND | GND | Full Step
  VCC | GND | GND | Half Step
  GND | VCC | GND | Quarter Step
  VCC | VCC | GND | Eighth Step
  VCC | VCC | VCC | Sixteenth Step
  GND = Jumpers open 
  VCC = Jumpeers connection
  ```
- Driver current regulation
  - Verf measures the voltage of Gnd and potentiometer middle
  - Please DO NOT connect the motors when measuring the voltage, or it's easy to burn the drive
  - Please connect the power supply when measuring voltage as well, do not connect only the USB power
  - I=Vref/(Rs*8)    Default I=1.0A