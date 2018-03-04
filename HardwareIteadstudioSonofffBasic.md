# IteadStudio Sonoff Basic

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-wifi-wireless-switch.html](https://www.itead.cc/sonoff-wifi-wireless-switch.html)|
|Build flag|`ITEAD_SONOFF_BASIC`|

## Introduction

The original Sonoff (now renamed Sonoff Basic) has an ESP8266 on board with a 8Mbit flash memory chip, a mains to 3V3 transformer and a relay (GPIO12). It also features a button (GPIO0), an LED (GPIO13) and an unpopulated header you can use to reprogram it.

### Flashing

![Sonoff - Inside front view](images/flashing/sonoff-flash.jpg)

The unpopulated header in the Sonoff has all the required pins. My board has a 5 pins header in-line with the button. They are (from the button outwards) 3V3, RX, TX, GND and GPIO14.

The last one is not necessary.  The button is connected to GPIO0 on the ESP8266 chip, so to enter flash mode you have to hold the button pressed while powering on the board, then you can release it again.

## Issues

The original Sonoff This is probably due to the antenna placement close to live lines. It works fine if it's near the AP, otherwise, it's often reported to lose connectivity.