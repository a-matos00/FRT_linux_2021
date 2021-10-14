![](https://github.com/fesbracingteam/FrtLinuxImage/blob/main/misc/frtLinuxLogo.png)
# FESB Racing Team Buildroot 3.0 Repository

## Description

This repository contains the full buildroot folder required for compiling the OS image.
The current OS configuration only supports raspberryPi 3B and 3B+ boards.
This project is an expansion of : https://github.com/furkantokac/buildroot

## Quick Start

Install the **required packages** to be able to use buildroot properly. Run the following command in the terminal: 
```sh
sudo apt install sed make binutils gcc g++ bash patch \gzip bzip2 perl tar cpio python unzip rsync wget libncurses-dev
```
1. The output folder contains the latest **OS image**. If you wish to create a new **OS configuration**, run:
```sh
make clean
```
This will delete all files from the output folder except the QT folder. **It is crucial to run this command before compiling the new image**.

2. To select the required **OS and kernel configuration** run: 
```sh
make FRTv3_defconfig
```
3. To add **custom changes** to the configuration run:
```sh
make xconfig
```
```sh
make linux-xconfig
```
4. **Xconfig** and **linux-xconfig** require qt5dev tools to run properly so make sure to install them. You can also use **menuconfig** instead of xconfig. The only difference is the GUI.
 
5. To build the **OS image** run:
```sh
make -j8
```
The **-jx flag** is used to speed up the compilation process("x" should be twice the number of cores inside your computers processor). This will take around 45mins to an hour. The generated files are stored in the output folder.

6. To create a **QT cross compilation toolchain** run the script:
```sh
./build-rpi3-qt.sh
```
This will generate a Qt folder in the output folder. Those files are used for configuring QT creator for cross compilation. You can specify the required **QT version** in the script. This will also take a while.

7. Flash the image to the SD card using **etcher**. The image is located in ``` /output/images ```

8. The configuration of the display is located in the **config.txt** file. Uncomment the lines of the configuration for the device you are using.

9. The **post startup script** is located in the **/etc/init.d folder**. In that file you specifiy which applications or commands you want to run afer the boot process has finished.

Note: Editing files on the SD card might require root privleges.
<br></br>
<h2>Changes made from the initial version:</h2>
mcp2515 module support<br></br>
SocketCAN<br></br>
Vcan<br></br>

Note: all stated changes are tested and should be available and work properly.

<h2>VERSION details</h2>
<h3>V3.0</h3>
Supports the mcp2515 module. Tested on the FRT CAN SW board!
Runs QML applications.
Boots in 5sec when powered from a laptop.
