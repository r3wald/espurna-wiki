# Electrodragon ESP Relay Board

![Electrodragon ESP Relay Board](images/devices/electrodragon-wifi-iot.jpg)

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Product page|[http://www.electrodragon.com/product/wifi-iot-relay-board-based-esp8266/](http://www.electrodragon.com/product/wifi-iot-relay-board-based-esp8266/)|
|Wiki page|[https://www.itead.cc/wiki/Sonoff](https://www.itead.cc/wiki/Sonoff)|
|Build flag|`ELECTRODRAGON_WIFI_IOT`|
|Voltage|<span style="color:red">5v</span>|

## Introduction

*TODO*

## Flashing

![Electrodragon ESP Relay Board - Front view](images/flashing/electrodragon-flash.jpg)

The Electrodragon ESP Relay Board is pretty easy to flash IF you do not follow their wiki, it's all wrong. Check the picture above and note that:

* Power the board from the 5V pin, GND to GND
* The RX pin in the header should go to your programmer TX pin and
* The TX pin in the header should go to your programmer RX pin
* The button labeled BTN2 is connected to GPIO0, so hold it down while powering the board, I've had better results keeping it down until the flashing starts

## Issues

*TODO*