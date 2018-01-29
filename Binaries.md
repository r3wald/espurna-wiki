# Flash a binary image

## Requirements

You will need the latest version of the [esptool.py tool](https://github.com/espressif/esptool). From now on I will assume you have it somewhere on your path, otherwise use the absolute path to it in the commands below.

You will also nee a binary image of the ESPurna firmware. Pre-built binary images for the latest releases are available in the [releases](https://github.com/xoseperez/espurna/releases/) page. Grab the latest one for your device and save it locally.

## Set up your device

To backup the image you will need to boot your board in flash mode. The procedure is exactly the same as when you are getting ready to flash a new image and it will depend on your device. Check the [supported hardware page](https://github.com/xoseperez/espurna/wiki/Hardware) for instructions.

You will need to go into boot mode every time you want to erase the flash or flash a new image. After either of these two the board will reboot into normal unless GPIO0 is still tied to ground.

## Erase the flash

If the device becomes unstable or you want a fresh install you will have to first erase the flash image using this command:

```
esptool.py --port /dev/ttyUSB0 --baud 115200 erase_flash
```

## Flash the binary

To flash the binary into your device go into flash mode and run the next command replacing "firmware.bin" with the path (relative or absolute) to the pre-built image you previously downloaded.

```
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash -fs 1MB -fm dout 0x00000 firmware.bin
```

"fs" stands for "flash size" and is set to 1 Megabyte in the example. That is the standard size for Sonoff devices. If you are using a 4 Megabyte module you might want to change this value to "4MB" (maybe if you add some SPIFFS based logging system, for instance). DOUT flash mode should work for all devices.
