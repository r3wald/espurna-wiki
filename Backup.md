# Backup stock firmware

**This procedure is provided AS-IS, just like the rest of this project, this has worked for me but might not work for you**. It's a simple dump of the flash contents, including emulated EEPROM data and unaware of the flash layout. So it's meant for simple backup & restore procedure.

## Requirements

You will need a working copy of [esptool.py](https://github.com/espressif/esptool). You might already have it with you IDE of choice, make sure you locate it and it's up to date.

The examples below assume you have esptool.py somewhere in the path, otherwise specify the full path to the tool.

## Connection

To backup the image you will need to boot your board in flash mode. The procedure is exactly the same as when you are getting ready to flash a new image and it will depend on your device. Check the [supported hardware page](https://github.com/xoseperez/espurna/wiki/Hardware) for instructions.

## Backup

Depending on your device flash memory size you will need to specify a different size. Check the read_flash options:

```
$ esptool.py read_flash -h
usage: esptool read_flash [-h] [--spi-connection SPI_CONNECTION]
                          [--no-progress]
                          address size filename

positional arguments:
  address               Start address
  size                  Size of region to dump
  filename              Name of binary dump

optional arguments:
  -h, --help            show this help message and exit
  --spi-connection SPI_CONNECTION, -sc SPI_CONNECTION
                        ESP32-only argument. Override default SPI Flash
                        connection. Value can be SPI, HSPI or a comma-
                        separated list of 5 I/O numbers to use for SPI flash
                        (CLK,Q,D,HD,CS).
  --no-progress, -p     Suppress progress output
```

To backup a Sonoff device (1Mbyte flash size) you will need to (change port to match yours):

```
esptool.py --port /dev/ttyUSB0 --baud 115200 read_flash 0x00000 0x100000 sonoff-backup.bin
```

To restore the image do a:

```
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash -fs 1MB -fm dio 0x00000 sonoff-backup.bin
```

The writing process first erases the flash contents. In case you wanted to do it manually you can:

```
esptool.py --port /dev/ttyUSB0 --baud 115200 erase_flash
```
