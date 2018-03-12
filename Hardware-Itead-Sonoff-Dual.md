# Itead Sonoff Dual

![Sonoff Dual](images/devices/itead-sonoff-dual.jpg)

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Product page|[https://www.itead.cc/sonoff-dual.html](https://www.itead.cc/sonoff-dual.html)|
|Wiki page|[https://www.itead.cc/wiki/Sonoff](https://www.itead.cc/wiki/Sonoff)|
|Build flag|`ITEAD_SONOFF_DUAL`<br>`ITEAD_SONOFF_DUAL_R2`|
|Voltage|<span style="color:red">3v3</span>|

## Introduction

*TODO*

## Flashing

![Sonoff DUAL - Inside back view](images/flashing/sonoff-dual-flash.jpg)

The Sonoff Dual it's a bit tricky to flash since GPIO0 is not connected to the button as in the TH or POW, but to the pin 15 in the SIL F330 chip that manages the buttons and the relays. SO you have to locate a pad connected to GPIO and short it to ground while powering the device.

In the picture above you have a location of an available and easily accessible GPIO0 pad. The other required pins are brought out in the top header.

Once flashed you can use OTA to update the firmware without having to open the device.

## Issues

The original Sonoff has some connectivity issues. This is probably due to the antenna placement close to live lines. It works fine if it's near the AP, otherwise, it's often reported to lose connectivity.
