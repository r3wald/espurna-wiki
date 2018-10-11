# iWoole LED Table Lamp

## info
|Property|Value|
|---|---|
|Manufacturer|iWoole|
|Product page|http://iwoole.com/newst-led-smart-night-light-7w-smart-table-light-rgbw-wifi-app-remote-control-110v-220v-us-eu-plug-smart-lamp-google-home-decore-p00022p1.html|
|Wiki page||
|Build flag|`IWOOLE_LED_TABLE_LAMP`|

## Introduction

iWoole LED Table Lamp

Note: The translucent part of the casing is locked into place with 4 evenly spaced serated clips. The easiest way to separate it is to quite forcibly tap the plastic as close to the alloy casing as possible - do that all the way around until you are certain that it is free to move. I'm not sure whether there is glue used, but it does seems a lot easier to separate when you have tapped it a lot. Don't use metal tools or you will mark the plastic. If you are lucky you'll manage to get one or more of the clips to move to the next tooth quite quickly, and at that point if you can insert a plastic card in the gap and work it around you'll find that the plastic will fairly easily pop out.

## images
![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp.jpg)

![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp-open1.jpg)

![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp-open2.jpg)

![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp-module-front.jpg)

![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp-module-rear.jpg)

![](https://github.com/xoseperez/espurna/blob/dev/images/devices/iWoole-led-desk-lamp-module-esp-m2.jpg)



## Flashing

The led board needs to be unscrewed to reveal the module, that you'll find has been bound by 30mm diameter heat shrink tubing - possibly multiple layers. I'd recommend ordering some of this in advance - it's quite neat, and 2 layers should provide adequate insulation for the components and reduce the rick of any sharp edges poking through when you reassemble.

In any case, carefully remove the heat shrink - a regular pair of kitchen scissors would suffice as long as you take your time. If you are careful you could just cut slots in the tubing and peel them back enough to give you room to work. Gently unplug the LED board. The ESP module is an un-marked (or scratched off) ESP-M2. I didn't bother trying to figure out if any of the test points on the back of the main pcb could be used for flashing, so you'll need to solder 5 wires (3.3V, GND, TX, RX, and GPIO0). Ground GPIO, flash and test before assembling. **PLEASE REMOVE THE WIRES FROM YOUR SERIAL MODULE BEFORE PLUGGING IT IN**

Re-assemble the unit by slipping over fresh heat shrink prior to plugging the LED board back in.

## Issues

*TODO*