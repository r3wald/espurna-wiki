# Itead Sonoff 4CH

![Sonoff 4CH](images/devices/itead-sonoff-4ch.jpg)

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Product page|[https://www.itead.cc/sonoff-4ch.html](https://www.itead.cc/sonoff-4ch.html)|
|Wiki page|[https://www.itead.cc/wiki/Sonoff](https://www.itead.cc/wiki/Sonoff)|
|Build flag|`ITEAD_SONOFF_4CH`|
|Voltage|<span style="color:red">3v3</span>|

## Introduction

*TODO*

## Flashing

You will have to open the case. There is a 5 pin header with VCC33 (3V3), TX, RX and GND. First button is properly labelled FW/IO0 so all you have to do is to connect TX, RX and GND to your USB2UART programmer, press the button and connect the VCC33 pin to power the board and enter flash mode. One very important thing: the **TX and RX pins are crossed**. You have to connect TX to your programmer TX and RX to RX.

## Issues

*TODO*