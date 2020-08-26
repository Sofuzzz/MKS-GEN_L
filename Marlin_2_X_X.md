# Tips: Marlin 2.x.x build need use platfromio of Visual Studio Code

# Install Visual Studio Code
- Before starting to edit Marlin, we recommend that you install a good code editor - Visual Studio Code. You can even compile Marlin directly from it.

- Visual Studio Code can be freely downloaded, after you have edited Marlin and the necessary parameters,you can compile it and upload your new firmware to the printer.

- How to install Visual Studio Code and PlatformIO,edit and compile marlin,you can find from [marlinfw.org](https://marlinfw.org/docs/basics/install_platformio_vscode.html)

# Download Marlin
After install VScode, you should download the Marlin source code. There are three ways to get Marlin source code.

- You can download official marlin from here [Marlin 2.x.x](https://marlinfw.org/meta/download/), we usually download the firmware LATEST RELEASE, just below the word DOWNLOAD. There, click on the 2.0.x.zip link.

- You can use MKS TOOL to download marlin from here [MKS TOOL](https://baizhongyun.cn/home/mkstoolview), you can directly configure the firmware with the desired parameters from your browser and download it later.


# Configure and compile
- Download official marlin,you need change parameters suitable for MKS GEN_L board:
    - After platformio.ini："default_envs = **mega2560**"
    - Configuration.h:"#define MOTHERBOARD **BOARD_MKS_GEN_L**", If use V2, you need "#define MOTHERBOARD **BOARD_MKS_GEN_L_V2**"
    - Configuration.h:"#define SERIAL_PORT **0**" // for communication with MKS TFT series

- You can configure the firmware with the desired parameters, [Reference documents](https://marlinfw.org/docs/configuration/configuration.html),

# Upload marlin firmware
- You need select COM, and after upload firmware
