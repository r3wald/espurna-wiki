# Flash a binary image

## Requirements

You will need the latest version of the [esptool.py](https://github.com/espressif/esptool) tool. From now on I will assume you have it somewhere on your path, otherwise use the absolute path to it in the commands below.

You will also need a binary image of the ESPurna firmware. Pre-built binary images for the latest releases are available in the [releases](https://github.com/xoseperez/espurna/releases/) page. Grab the latest one for your device and save it locally.

## Set up your device
_if you haven't already, consider backing up your stock firmware._
_[Backup the stock firmware](https://github.com/xoseperez/espurna/wiki/Backup)_

To flash the image you will need to boot your board in flash mode. The procedure is exactly the same as when you are getting ready to flash a new image and it will depend on your device. Check the [supported hardware page](https://github.com/xoseperez/espurna/wiki/Hardware) for instructions.

esptool will hard reset after each operation so unless GPIO0 is still connected to ground you will need to go into boot mode manually every time you want to backup, erase or write flash.

## Erase the flash

Erasing a flash is not dangerous, you can always boot into flash mode and flash a new firmware.

**Erasing is important** as it nullifies the current flash, so you'll have a clean flash.
(If you flash a new firmware without erasing it first, leftover data from previous image -probably won't effect but- may render your device unstable.)

If the device becomes unstable or you want a fresh install you will have to first erase the flash image using this command:

```
esptool.py --port /dev/ttyUSB0 --baud 115200 erase_flash
```

## Flash the binary

To flash the binary into your device go into flash mode and run the next command replacing `firmware.bin` with the path (relative or absolute) to the pre-built image you previously downloaded.

```
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash -fs 1MB -fm dout 0x00000 firmware.bin
```

"fs" stands for "flash size" and is set to 1 megabyte in the example (-fs 1MB). That is the standard size for most Sonoff devices. If you are using a 4 megabyte module you might want to change this value to "4MB" (this maybe important as extra space will be used by SPIFFS and you'll larger storage. this maybe crucial, e.g if you want to add some SPIFFS based logging system). DOUT flash mode should work for all devices.

You can also let esptool autodetect the flash size based on SPI flash ID (-fs detect). If esptool fails to detect to size, it will show a warning and use default value of 4MB (4 megabytes).

```
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash -fs detect -fm dout 0x00000 firmware.bin
```