# IteadStudio Sonoff RF

![Sonoff RF](images/devices/itead-sonoff-rf.jpg)

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Product page|[https://www.itead.cc/sonoff-rf.html](https://www.itead.cc/sonoff-rf.html)|
|Wiki page|[https://www.itead.cc/wiki/Sonoff_RF](https://www.itead.cc/wiki/Sonoff_RF)|
|Build flag|`ITEAD_SONOFF_RF`|

## Introduction

The Sonoff RF is a [Sonoff Basic](Hardware-Iteadstudio-Sonoff-Basic) with a RF module and a EFM8BB1 microcontroller that drives the module, just like the Slampher. Just like the Basic, it features a button (connected to the EFM8BB1), an LED (GPIO13) and an unpopulated header you can use to reprogram it.

|GPIO|Usage|
|---|---|
|0|EFM8BB1|
|1|TX|
|3|RX|
|12|Relay|
|13|LED (inversed logic)|
|14|Available in header|

## Flashing

![Sonoff RF - Inside back view](images/flashing/sonoff-rf-flash.jpg)

The Sonoff RF has the same unpopulated header as the Sonoff. It is a 5 pins header in-line with the button. They are (from the button outwards) 3V3, RX, TX, GND and GPIO14.

Solder a male or female header here and connect your USB-to-UART programmer. This time through **the button is not connected to GPIO0** but to a EFM8BB1 micro-controller that also monitors the RF module output.

There are a couple of ways to enter flash mode. Some recommend to move 0Ohm R9 resistor to R21 to connect the button directly to the ESP8266 GPIO0 and use it in the same way as for the Sonoff or Sonoff TH. The drawback is the by doing that you lose the RF capability.

My recommendation is to **temporary shortcut the bottom pad of the unpopulated R21 footprint** (see the image above) and connect your USB-to-UART board at the same time. You will have to do it just once (unless there is something really wrong in the firmware) and use OTA updates from there on.

## Issues

It show the same issues as the [Sonoff Basic](Hardware-Iteadstudio-Sonoff-Basic).
