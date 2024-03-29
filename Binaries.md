# Flash a binary image

## Requirements

You will need the latest version of the [esptool.py](https://github.com/espressif/esptool) tool. From now on I will assume you have it somewhere on your path, otherwise use the absolute path to it in the commands below.

Examples below are for Linux and assume USB2UART adapter dev path is `/dev/ttyUSB0`. Normal user may not have access to the `/dev/ttyUSB#` by default. Make sure to follow [this guide](http://docs.platformio.org/en/latest/faq.html#platformio-udev-rules) if you are having trouble accessing it.

Of course, you will also need a binary image of the ESPurna firmware. Pre-built binary images for the latest releases are available on the [releases](https://github.com/xoseperez/espurna/releases/) page. Grab the latest one for your device and save it locally.

## Set up your device
__If you haven't already, consider backing up your stock firmware!__
__[Backup the stock firmware](https://github.com/xoseperez/espurna/wiki/Backup)__

To flash the image you will need to boot your board in flash mode. The procedure is exactly the same as when you are getting ready to flash a new image and it will depend on your device. Check the [supported hardware page](https://github.com/xoseperez/espurna/wiki/Hardware) for instructions.

esptool will hard reset after each operation so unless GPIO0 is still connected to ground you will need reenter boot mode manually every time you want to do backup, erase or write flash.

## Erase the flash

Erasing a flash is not dangerous, you can always boot into flash mode and flash a new firmware.

**Erasing is important** as it nullifies the current flash, removing any leftover data from the previous firmware (which -probably won't effect but- may render your device unstable.)

If the device becomes unstable or you want a fresh install you will have to first erase the flash image using this command:

```
esptool.py --port /dev/ttyUSB0 erase_flash
```

## Flash the binary

To flash the binary into your device go into flash mode and run the next command replacing `firmware.bin` with the path (relative or absolute) to the pre-built image you previously downloaded.

```
esptool.py --port /dev/ttyUSB0 write_flash --flash_size 1MB --flash_mode dout 0x00000 firmware.bin
```

Flash size is set to 1 megabyte - it is the standard size for most of Sonoff devices. If you are using a 4 megabyte module you might want to change this value to "4MB" (this maybe important as extra space will be used by SPIFFS and you'll larger storage. this maybe crucial, e.g if you want to add some SPIFFS based logging system). DOUT flash mode should work for all devices.

You can also let esptool autodetect the flash size based on SPI flash ID by using `--flash_size detect` or omitting the switch altogether. If esptool fails to detect to size, it will show a warning and use default value of 4MB (4 megabytes).

```
esptool.py --port /dev/ttyUSB0 write_flash --flash_mode dout 0x00000 firmware.bin
```