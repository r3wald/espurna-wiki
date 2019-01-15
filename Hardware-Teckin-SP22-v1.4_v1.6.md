# Teckin SP22 v1.4 / v1.6

![TECKIN SP22](images/devices/teckin-sp22.jpg)

|Property|Value|
|---|---|
|Manufacturer|[Teckin](https://teckinhome.com)|
|Product page|[Teckin Link](https://www.teckinhome.com/copy-of-sp-23)<br>[Amazon Link](https://www.amazon.de/gp/product/B07D5V139R)|
|Wiki page||
|Build flag|` TECKIN_SP22_V14`|
|PlatformIO|**teckin-sp22-v14** and **teckin-sp22-v14-ota** (since [1.13.4](https://github.com/xoseperez/espurna/releases/1.13.4))|

## Introduction

Variant of Blitzwolf SHP2

See https://github.com/xoseperez/espurna/issues/1283, https://github.com/xoseperez/espurna/issues/1431 and https://github.com/arendst/Sonoff-Tasmota/issues/3950

## Flashing

> Note: Based on [#1431](https://github.com/xoseperez/espurna/issues/1431), board ASIN B07D5V139R (v1.6)

As the case is glued (no screws anymore) it's really difficult to open. SMD hot air soldering kit (or heatgun) are your best friends in this case.

This device is based on [TYWE2S](https://fccid.io/2ANDL-TYWE2S/User-Manual/Users-Manual-3596121). Connect pins accordingly (right-to-left on the picture below):

Red - VCC (3v3)
Blue - GND
Purple - RX
Green - TX

![serial connection](https://user-images.githubusercontent.com/3238360/50052913-5bb09a00-012c-11e9-9ac3-045d05786bd2.jpg)
![serial adapter connection](https://user-images.githubusercontent.com/3238360/50052962-0d4fcb00-012d-11e9-866a-e14304d2699e.jpg)

Comment by [@Wikibear](https://github.com/Wikibear) (from [#1431](https://github.com/xoseperez/espurna/issues/1431#issuecomment-451645344)):

> TX RX must be connected directly but GND and power you can also connect here, which is easier to solder: 

![different 3v3 and GND connection](https://user-images.githubusercontent.com/132763/51179894-e45f5900-18d7-11e9-9b75-79d215c1a9a7.png)



To make the ESP go into flash mode, you have to connect DI0 to GND. That's a bit tricky as DI0 is not available in the pinout but is on the PCB:
![img_20181216_000302](https://user-images.githubusercontent.com/3238360/50052940-c5c93f00-012c-11e9-98f6-ea244f524fab.jpg)
