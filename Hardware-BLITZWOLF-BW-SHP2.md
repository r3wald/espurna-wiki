# BLITZWOLF BW-SHP2

![BLITZWOLF BW-SHP2](images/devices/blitzwolf-bw-shp2.jpg)

|Property|Value|
|---|---|
|Manufacturer|BlitzWolf|
|Product page|[BlitzWolf Link](https://www.blitzwolf.com/Wifi-Smart-Socket-EU-p-244.html)<br>[AliExpress Link](https://www.aliexpress.com/item/BlitzWolf-BW-SHP2-WIFI-Smart-Socket-EU-Plug-220V-16A-Remote-Control-Smart-Timing-Switch-Work/32871562977.html)<br>[Banggood Link](https://www.banggood.com/BlitzWolf-BW-SHP2-Smart-WIFI-Socket-EU-Plug-220V-16A-Work-with-Amazon-Alexa-Google-Assistant-p-1292899.html)|
|Wiki page||
|Build flag|`BLITZWOLF_BWSHP2`|

## Introduction

* Rated voltage: AC 110-240V 
* Rated current: 16A (3840W)
* Product size: L5.08 x W7.62

## Flashing

Open the device using special tools (the [Xiaomi Wiha 24-in-1 toolkit](https://www.banggood.com/XIAOMI-Wiha-25-in-1-Screwdrivers-Kits-With-24pcs-S2-Steel-Screw-Bits-and-Aluminium-Alloy-Screwdriver-p-1187158.html) has it):

![BlitzWolf BW-SHP2 shell](images/flashing/blitzwolf-bw-shp2-flash-shell.jpg)

![BlitzWolf BW-SHP2 board](images/flashing/blitzwolf-bw-shp2-flash-board.jpg)

Short GPIO0 and GND during boot to enter flash mode before connecting to the serial programmer. The power indicator LED will be strong red to confirm the device has entered this mode. As soon as the short is removed, the red color will be dimmed. The device will then be ready for flashing.

![BlitzWolf BW-SHP2 flashing circuit](images/flashing/blitzwolf-bw-shp2-flash-flash.jpg)

![BlitzWolf BW-SHP2 flashing circuit](images/flashing/blitzwolf-bw-shp2-flash-flash-jumpers.jpg)