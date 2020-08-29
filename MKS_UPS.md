# How to buy
- MKS UPS on Aliexpress  [MKS UPS](https://www.aliexpress.com/item/4000910659196.html)

# Video Tutorials
- If display is LCD12864. It can be referred to [LCD12864 UPS](https://www.youtube.com/watch?v=kjijfYPJccI)

- If display is MKS TFT35. It can be referred to [MKS TFT35 UPS](https://www.youtube.com/watch?v=ZRHTnbK3fGM)

# Notice
- MKS UPS12V can only be used for DC12V power,MKS UPS24V can only be used for DC24V power.

# Working process
- When AC power supply is cut off, the MKS UPS detects it and send signal to motherboard;
- The power stored in the MKS UPS and PSU continues to supply power to the motherboard;
- Motherboard detects the power-off signal, stop printing, turn off hotbed and hotend, lift z axis;
- The power stored in MKS UPS is generally lift z axis 20mm-200mm;
- When power supply is restored, resume printing through LCD/TFT screen.

# Wiring:

![wiring](https://github.com/makerbase-mks/MKS-GEN_L/blob/master/hardware/Image/MKS_GEN_L_UPS.png)

# MKS GEN_L Firmware setting
- Configuration_adv.h：
  - Enable #define POWER_LOSS_RECOVERY
  - Set #define PLR_ENABLED_DEFAULT      true
  - Enable #define BACKUP_POWER_SUPPLY
  - Set #define POWER_LOSS_ZRAISE            20 //mm,can change up to 200
  - Set #define POWER_LOSS_PIN             19
  - Set #define POWER_LOSS_STATE           HIGH

# How to use
- Work with MKS TFT35
  - Parameter setting and Usage method
    -  Settings -> Config -> Machine -> Position settings -> Z-axis pause position(relative position) = POWER_LOSS_ZRAISE (Configuration_adv.h file)
    -  Settings -> Config -> Advance -> power off dection module select **UPS**    

- Work with LCD12864
  - Usage method
    -  The external power is cut off directly, the Z axis is improved
    -  Power on again, LCD screen choose to resume printing