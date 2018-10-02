# Pixhawk connectivity guide

## Overview

This guide covers LightWare products that have the serial number `SXX-14501` and beyond. For previous devices please see these guides:
- SF10 & SF11: http://ardupilot.org/copter/docs/common-lightware-sf10-lidar.html
- LW20/SF20: http://ardupilot.org/copter/docs/common-lightware-lw20-lidar.html
- SF02: http://ardupilot.org/copter/docs/common-rangefinder-sf02.html
- SF40C: http://ardupilot.org/copter/docs/common-lightware-sf40c-objectavoidance.html

This guide has been tested with ArduPlane 3.9.1 and ArduCopter 3.5.7. If you are using the `PX4` stack instead of ArduPilot then this guide will still be useful for upgrading and configuring your LightWare device.

If you have any questions or issues with this process please contact Robert at rob@lightware.co.za

# Upgrading LightWare devices (SF11C/SF20C/LW20C)

Before attempting to connect with the Pixhawk we recommend performing a firmware upgrade on your LightWare device. You will also need this tool to perform configuration for the Pixhawk later. Please follow the steps outlined below:

> NOTE: The Upgrader tool only currently supports Windows at this time.

1. Download the LightWare Upgrader tool here: http://support.lightware.co.za/LightWareUpgrader-1.16.0.rar
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

### Configuring the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Wait for interface`. (Note: The Pixhawk will automatically initiate I2C mode on boot.)
4. Set `Pixhawk I2C compatibility mode` to `On`.
5. Click `Exit`.

### Wiring for I2C

Connect the SDA line of the Lidar to the SDA line of the I2C port on the Pixhawk, and the SCL line of the Lidar to the SCL line of the I2C port. Also connect the GND and 5V lines.

![Wiring](pixhawk_lw20_i2c.jpg)
> NOTE: This diagram is also correct for the LW20C.

### Configuring the Pixhawk

You then need to configure the rangefinder parameters as shown below (this cn be done suing the Mission Planner Config/Tuning | Full Parameter List page):

- `RNGFND_TYPE` = 7 (LightWareI2C)
- `RNGFND_ADDR` = 102 (I2C Address of lidar in decimal). Note that this setting is in decimal. The default address is 0x66 hexademical which is 102 in decimal.
- `RNGFND_SCALING` = 1
- `RNGFND_MIN_CM` = 5
- `RNGFND_MAX_CM` = 9500. This is the distance in centimeters that the rangefinder can reliably read.
- `RNGFND_GNDCLEAR` = 10 or more accurately the distance in centimetres from the range finder to the ground when the vehicle is landed. This value depends on how you have mounted the rangefinder.

## Serial UART

### Configuring the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Serial mode`. (Note: The Pixhawk is unable to initiate serial mode, so it must be forced.)
5. Click `Exit`.

### Wiring for Serial UART

For a serial connection you can use any spare UART. Connect the RX line of the UART to the TX line of the Lidar, and the TX line of the UART to the RX line of the Lidar. Also connect the GND and 5V lines. You do not need flow control pins.

The diagram below shows how to connect to SERIAL4.

![Wiring](pixhawk_lw20_serial.jpg)
> NOTE: This diagram is also correct for the LW20C.

### Configuring the Pixhawk

You then need to setup the serial port and rangefinder parameters. If you have used the SERIAL4/5 port on the Pixhawk then you would set the following parameters (this can be done using the Mission Planner Config/Tuning | Full Parameter List page):

- `SERIAL4_PROTOCOL` = 9 (Lidar)
- `SERIAL4_BAUD` = 115 (115200 baud)
- `RNGFND_TYPE` = 8 (LightWareSerial)
- `RNGFND_SCALING` = 1
- `RNGFND_MIN_CM` = 5
- `RNGFND_MAX_CM` = 9500. This is the distance in centimeters that the rangefinder can reliably read.
- `RNGFND_GNDCLEAR` = 10 or more accurately the distance in centimetres from the range finder to the ground when the vehicle is landed. This value depends on how you have mounted the rangefinder.

# SF11/C

## I2C

### Configuring the LW20/SF20
1. Use the LightWare Upgrader as outlined above to connect to your device.
2. Once the correct COM port has been selected click `Manage`.
3. Set `Startup mode` to `Wait for interface`. (Note: The Pixhawk will automatically initiate I2C mode on boot.)
4. Set `Pixhawk I2C compatibility mode` to `On`.
5. Click `Exit`.

### Wiring for I2C

Connect the SDA line of the Lidar to the SDA line of the I2C port on the Pixhawk, and the SCL line of the Lidar to the SCL line of the I2C port. Also connect the GND and 5V lines.

>This diagram is for the Pixhawk 1 but you can also connect to the Pixhawk 2.1 by following the correct pinouts for that device.

![Wiring](pixhawk_sf11_i2c.jpg)

### Configuring the Pixhawk

You then need to configure the rangefinder parameters as shown below (this is done in the Mission Planner Config/Tuning | Full Parameter List page):

- `RNGFND_TYPE` = 7 (LightWareI2C)
- `RNGFND_ADDR` = 102 (I2C Address of lidar in decimal). Please note that this setting is in decimal and not hexadecimal as shown in the lidar settings screen. The default address is 0x66 which is 102 in decimal.
- `RNGFND_MIN_CM` = 5
- `RNGFND_MAX_CM` = 12000 (for SF11C). This is the distance in centimeters that the rangefinder can reliably read. The value depends on the model of the lidar.
- `RNGFND_GNDCLEAR` = 10 or more accurately the distance in centimetres from the range finder to the ground when the vehicle is landed. This value depends on how you have mounted the rangefinder.

## Serial UART

### Configuring the LW20/SF20
The SF11/C serial mode works out of the box with no need to configure anything through the Upgrader, although we still recommend having the latest version of firmware installed.

### Wiring for Serial UART

For a serial connection you can use any spare UART. Connect the RX line of the UART to the TX line of the Lidar, and the TX line of the UART to the RX line of the Lidar. Also connect the GND and 5V lines. You do not need flow control pins.

The diagram below shows how to connect to SERIAL4.

>This diagram is for the Pixhawk 1 but you can also connect to the Pixhawk 2.1 by following the correct pinouts for that device.

![Wiring](pixhawk_sf11_serial.jpg)

### Configuring the Pixhawk

You then need to setup the serial port and rangefinder parameters. If you have used the SERIAL4/5 port on the Pixhawk then you would set the following parameters (this is done in the Mission Planner Config/Tuning | Full Parameter List page):

- `SERIAL4_PROTOCOL` = 9 (Lidar)
- `SERIAL4_BAUD` = 19 (19200 baud)
- `RNGFND_TYPE` = 8 (LightWareSerial)
- `RNGFND_MIN_CM` = 5
- `RNGFND_MAX_CM` = 12000 (for SF11C). This is the distance in centimeters that the rangefinder can reliably read. The value depends on the model of the lidar.
- `RNGFND_GNDCLEAR` = 10 or more accurately the distance in centimetres from the range finder to the ground when the vehicle is landed. This value depends on how you have mounted the rangefinder.


