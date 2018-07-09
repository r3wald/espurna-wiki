# Arilux AL-LCxx

|LC01|LC02|LC11|
|---|---|---|
|![Arilux AL-LC01](images/devices/arilux-al-lc01.jpg)|![Arilux AL-LC02](images/devices/arilux-al-lc02.jpg)|![Arilux AL-LC11](images/devices/arilux-al-lc11.jpg)|

|Property|Value|
|---|---|
|Manufacturer|Arilux|
|Product page||
|Wiki page||
|Build flag|`ARILUX_AL_LC01`<br>`ARILUX_AL_LC02`<br> `ARILUX_AL_LC11`|

## Introduction

|LC01|LC02|LC11|
|---|---|---|
|Working Voltage: DC 5-28V<br>Output Channel: 3 channels<br>Output Current: RGB, 4Ax3<br>Max. Power: 4A x 3 x 12V = 144W<br>Connection: Common anode<br>Dimension: about L46 x W19 x H8 mm|Working Voltage: DC 9-12V<br>Output Channel: 4 channels<br>Output Current: RGBW, 4Ax4<br>Max. Power: 4A x 4 x 12V = 192W<br>Connection: Common anode<br>Dimension: about L46 x W19 x H8 mm|Working Voltage: DC 9-28V<br>Output Channel: 5 channels<br>Output Current: RGBW/WW, 4Ax5<br>Output Power: ≤240W<br>Connection: Common anode<br>Dimension: about L46 x W19 x H8 mm|

## Flashing

Open the plastic enclosure (using a sharp tool) and extract the little board inside.

You will see some soldering points with labels: GND, TX, RX and I00. If you are good enought with the soldering iron, connect dupont wires to these pads ([check this guide](Hardware-Magic-Home-LED-Controller)). 

If you prefer to got the safe way, use this tricky method: 

* bend the tip of some dupont wires, 
* glue the tip to a short piece of a ziptie
* hold the board in place with a couple of pins,
* hold the the zipties with clothespins
* adjust the tips of the dupont wires placing them carefully on the soldering pads 

![arilux_flashing_without_soldering_02](https://user-images.githubusercontent.com/697599/42446451-915c1f64-8376-11e8-9ac7-4c797d6673ce.jpg)
![arilux_flashing_without_soldering_01](https://user-images.githubusercontent.com/697599/42446452-91df2972-8376-11e8-898b-d1014e15f9d8.jpg)


Finally, connect the dupont wires to your FTDI-USB dongle and follow the general instructions in [this page](Binaries) to start flashing.


## Issues

*TODO*