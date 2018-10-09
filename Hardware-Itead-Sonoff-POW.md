# Itead Sonoff POW

![Sonoff POW](images/devices/itead-sonoff-pow.jpg)

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Product page|[https://www.itead.cc/sonoff-pow.html](https://www.itead.cc/sonoff-pow.html)|
|Wiki page|[https://www.itead.cc/wiki/Sonoff](https://www.itead.cc/wiki/Sonoff)|
|Build flag|`ITEAD_SONOFF_POW`|
|Voltage|<span style="color:red">3v3</span>|

## Introduction

[iTead Sonoff Pow with Energy Monitoring](http://sonoff.itead.cc/en/products/sonoff/sonoff-pow)

## Flashing

![Sonoff POW - Inside back view](images/flashing/sonoff-pow-flash.jpg)

The unpopulated header in the Sonoff has all the required pins. My board has a 4 pins header. They are (from the top down) 3V3, RX, TX, GND

## Issues

The original Sonoff has some connectivity issues. This is probably due to the antenna placement close to live lines. It works fine if it's near the AP, otherwise, it's often reported to lose connectivity.