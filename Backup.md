# Backup stock firmware

**This procedure is provided AS-IS, just like the rest of this project, this has worked for me but might not work for you**. It's a simple dump of the flash contents, including emulated EEPROM data and unaware of the flash layout. So it's meant for simple backup & restore procedure.

## Requirements

You will need a working copy of [esptool.py](https://github.com/espressif/esptool). You might already have it with you IDE of choice, make sure you locate it and it's up to date.

The examples below assume you have esptool.py somewhere in the path, otherwise specify the full path to the tool.

### Serial port device

When `--port` argument is not specified, esptool.py will enumerate all connected serial ports and try each one until it finds an Espressif device connected ([source](https://github.com/espressif/esptool#serial-port))

For Linux / macOS, use full device path (`/dev/ttyUSB*`, `/dev/cu.*` or `/dev/tty.*`). If you are using Windows, `mode` utility will display all available serial devices (`COM*`)

## Connection

To backup the image you will need to boot your board in flash mode. The procedure is exactly the same as when you are getting ready to flash a new image and it will depend on your device. Check the [supported hardware page](https://github.com/xoseperez/espurna/wiki/Hardware) for instructions. After each command esptool will reset the device.

## Backup

Flash size can be determined by running `flash_id` command. Example output with ESP12E board:

```
$ esptool.py flash_id
esptool.py v2.7-dev
Serial port /dev/ttyUSB0
Connecting....
Detecting chip type... ESP8266
Chip is ESP8266EX
Features: WiFi
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Manufacturer: 20
Device: 4016
Detected flash size: 4MB
Hard resetting via RTS pin...
```

To perform full backup you will need to specify starting `address` as 0 and `size` as flash size in bytes (either hex or decimal):
```
$ esptool.py read_flash --help
usage: esptool read_flash ... address size filename

positional arguments:
  address               Start address
  size                  Size of region to dump
  filename              Name of binary dump

$ esptool.py --port /dev/ttyUSB0 read_flash 0x00000 0x400000 d1-mini.bin
```

For 1MB or 2MB boards:
```
$ esptool.py --port /dev/ttyUSB0 read_flash 0x00000 0x100000 esp-1MB-backup.bin
$ esptool.py --port /dev/ttyUSB1 read_flash 0x00000 0x200000 esp-2MB-backup.bin
```

To restore the image, you only need to specify the starting address:
```
$ esptool.py --port /dev/ttyUSB0 write_flash 0x00000 d1-mini.bin
```

To completely erase the flash:
```
esptool.py erase_flash
```