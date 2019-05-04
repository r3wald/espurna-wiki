# NEO COOLCAM NAS WR01W

![NEO COOLCAM NAS WR01W](images/devices/neo-coolcam-wifi.jpg)

|Property|Value|
|---|---|
|Manufacturer|Coolcam|
|Product page|[AliExpress Link](https://www.aliexpress.com/item/NEO-COOLCAM-Wifi-Smart-Plug-EU-Socket-Support-Alexa-Google-Home-IFTTT-Outlet-With-Timer-and/32859702805.html)|
|Wiki page||
|Build flag|`NEO_COOLCAM_NAS_WR01W`|

## Introduction

* Rated voltage: AC 110-230V 
* Rated current: 10A (2300W)
* Product size: 65x43x43mm

## Flashing

Flashing the Neo Coolcam NAS WR01W can be done Over-The-Air (OTA) using [Tuya Convert](https://github.com/ct-Open-Source/tuya-convert). Download the espurna image file for the [Neo Coolcam WiFi WR01W](https://github.com/xoseperez/espurna/releases/download/1.13.5/espurna-1.13.5-neo-coolcam-power-plug-wifi.bin) and replace 'thirdparty.bin' with the downloaded version. You can also flash the firmware through the available serial port, you will have to disassemble the unit.  

![NEO COOLCAM - Disassembled](images/flashing/neo-coolcam-nas-wr01w-disassemble.jpg)

The electronics are split into 3 different PCB for mains connection, power supply and logic. To be able to flash the ESP8266 chip you have to solder 5 small pads in the back of the top layer (the logic one), but those pads are hard to reach because the relay top (soldered to the bottom layer) is very close to them.

![NEO COOLCAM - Layers](images/flashing/neo-coolcam-nas-wr01w-layers.jpg)

So the best option you have is to remove the top layer by desolder the 6 pads that connect it to the middle PCB. Once removed the procedure is the same as with other devices: tin the pads a bit, solder some small cables to it and flash it. The pads are appropiately labelled as GND, 3.3V, TXD0, RXD0 and GPIO0.

![NEO COOLCAM - Pads](images/flashing/neo-coolcam-nas-wr01w-pads.jpg)

## Connectivity and build flags
Use an UART board for serial connection and flashing. 
Connect wires as follows:
* Board - UART
* GND - GND
* 3.3V - 3.3V
* RXD0 - TX (note crossing rx to tx)
* TXD0 - RX (note crossing tx to rx)
* GPIO0 - GND (Disconnect after flashing)

Note from other users:
* Connection GPIO0 to GND did not help - flashing did not work. I had also to connect RST pad to 3.3V. After that - flashing worked perfectly even without RST connected to 3.3 V (from second flash)

## Important build flags.

in Platformio for tasmota flag change from 1MB to 8MB is needed, otherwise flash fails. build_flags = ${esp82xx_defaults.build_flags} -Wl,-Teagle.flash.8m.ld

in Arduino IDE, board selected - "Node MCU 1.0", standard

## NEO device is connected as
* LED = GPIO4 (D2 NodeMCU)
* RELAIS = GPIO12 (D6 ModeMCU)
* BUTTON = GPIO13 (D7 NodeMCU)