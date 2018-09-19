# Pixhawk connectivity guide

## Overview

This guide covers LightWare products that have the serial number `SXX-14501` and beyond. For previous devices please see these guides:
- SF10 & SF11: http://ardupilot.org/copter/docs/common-lightware-sf10-lidar.html
- LW20/SF20: http://ardupilot.org/copter/docs/common-lightware-lw20-lidar.html
- SF02: http://ardupilot.org/copter/docs/common-rangefinder-sf02.html
- SF40C: http://ardupilot.org/copter/docs/common-lightware-sf40c-objectavoidance.html

> NOTE: The new SF40C (Manufactured after `July 2018`) does not yet support the Pixhawk out of the box.

If you have any questions or issues with this process please contact Robert at rob@lightware.co.za

- Wiring
- Pixhawk versions
- Firmware versions
- Ardupilot versions

# Upgrading LightWare devices (SF11C/SF20C/LW20C)

Before attempting to connect with the Pixhawk we recommend performing a firmware upgrade on your LightWare device. You will also need this tool to perform configuration for the Pixhawk later. Please follow the steps outlined below:

> NOTE: The Upgrader tool only currently supports Windows at this time.

1. Download the LightWare Upgrader tool here: http://support.lightware.co.za/LightWareUpgrader-1.11.0.rar
2. Unzip the downloaded file to a location on your PC.
3. Run the file `LightWareUpgrader.exe` in the unzipped folder.
4. Connect your LightWare device via USB to your PC.
    - The SF11C can be plugged in directly with the included USB cable.
    - The SF20C/LW20C require a Serial UART TTL (3.3V logic, 5V Power) to USB adapter.
5. Click the COM port that appears.
6. If the device is not the latest version you can click the `Upgrade` button to begin the process.
7. Wait until the upgrade has completed successfully and click `OK`.

> NOTE: The Upgrader allows you to configure settings on your device using the `Manage` button. Please do not set `Startup mode` to `I2C mode` unless otherwise instructed to do so. If you do find your LW20/SF20 booting only in I2C mode, you can use the `Devantech USB-ISS` adapter which the Upgrader will respond to and allow you to change the `Startup mode`.

# LW20/SF20

## I2C

### Configure the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Wait for interface`. (Note: The Pixhawk will automatically initiate I2C mode on boot.)
4. Set `Pixhawk I2C compatibility mode` to `On`.
5. Click `Exit`.

### Wiring to I2C port

### Configuring the Pixhawk

## Serial UART

### Configure the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Serial mode`. (Note: The Pixhawk is unable to initiate serial mode, so it must be forced.)
5. Click `Exit`.

### Wiring to the Serial UART

### Configuring the Pixhawk

# SF11/C

## I2C

### Configure the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Wait for interface`. (Note: The Pixhawk will automatically initiate I2C mode on boot.)
4. Set `Pixhawk I2C compatibility mode` to `On`.
5. Click `Exit`.

### Wiring to I2C port

![Wiring][pixhawk_sf11_i2c.jpg]

### Configuring the Pixhawk

## Serial UART

### Configure the LW20/SF20
The SF11/C serial mode works out of the box with no need to configure anything through the Upgrader, although we still recommend having the latest version of firmware installed.

### Wiring to the Serial UART

![Wiring][pixhawk_sf11_serial.jpg]

### Configuring the Pixhawk
