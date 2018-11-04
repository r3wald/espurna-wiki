# Maxcio W-DE004

![Maxcio W-DE004(images/devices/maxcio-w-de004.jpg)

Contributed based on work by Michael Harwerth from Germany

Quite affordable (4-pack for 47€ on Amazon) Wifi Plugs. Of course, they have their own mobile phone app, but that's not what we're looking for, isn't it? 

|Property|Value|
|---|---|
|Manufacturer|Maxcio|
|Product page|[Amazon Link](https://amzn.to/2P7CHqA)|
|Wiki page||
|Build flag|`MAXCIO_WDE004`|

## Introduction

* Input voltage: AC100-240V 50/60Hz
* Working Current: 10A
* Has power meter: NO
* Power consuming: ≤0.3W
* Dimensions L2.96 x W1.57 x H0.98"
* Has a USB port which alledgedly outputs 2.1A (it's also used for supplying power when flashing)

## Flashing

Drill a hole in the botom cover. This will allow you to easily pry off the cover
![Maxcio W-US002S board](images/flashing/maxcio-w-de004-flash1.jpg)

Loosen the two screws that are now exposed and you now have access to the insides
![Maxcio W-US002S board](images/flashing/maxcio-w-de004-flash2.jpg)

USB Port connector is a good place for connecting GND
![Maxcio W-US002S board](images/flashing/maxcio-w-de004-flash3.jpg)

RX, TX and GPIO0 are marked here
![Maxcio W-US002S board](images/flashing/maxcio-w-de004-flash4.jpg)

For flashing, connect up RX<->TX and TX<->RX as usual to your programmer, GND to GND and hold GPIO0 against ground, the power it up via the USB port. 
Possibly there may be a way to connect 3.3V directly. I don't know, need to get myself a new multimeter one of these days and check it out. 
## Issues

*None found so far* 