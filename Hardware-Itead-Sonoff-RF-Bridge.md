# Itead Sonoff RF Bridge

![Sonoff RF Bridge](images/devices/itead-sonoff-rfbridge.jpg)

|Property|Value|
|---|---|
|Manufacturer|[Itead Studio](https://www.itead.cc)|
|Product page|https://www.itead.cc/sonoff-rf-bridge-433.html|
|Wiki page|https://www.itead.cc/wiki/Sonoff_RF_Bridge_433|
|Build flag|`ITEAD_SONOFF_RFBRIDGE`|

## Introduction

Here is the original post on sonoff rf bridge:<br>
http://tinkerman.cat/hacking-sonoff-rf-bridge-433

Please note that flashing ESPurna alone, while giving you most of the features you would expect from this firmware, *cannot* widen the range of RC remotes that the Sonoff RF Bridge can recognize. On this device the RF decoding is not performed by the main processor running ESPurna. Instead, the task is performed on an auxiliary microcontroller, an EFM8BB1, which has its *own* firmware dedicated to this job.

Currently, there are two ways to overcome this limitation and they are listed below in the section *Modifications*.

## Modifications

ESPurna supports two hacked variants of the Sonoff RFBridge:
* [RF_RAW_SUPPORT](https://github.com/Portisch/RF-Bridge-EFM8BB1) replaces the EFM8BB1 firmware.  
  Key points: 
  * Integration with ESPurna is still partial.
  * Types of hardware recognized: check on 
[RF-Bridge-EFM8BB1
 project page](https://github.com/Portisch/RF-Bridge-EFM8BB1).
  * No need to solder or cut traces on the board. 
  * You need an Arduino or something alike to program the auxiliary controller.
* [RFB_DIRECT](https://github.com/xoseperez/espurna/wiki/Hardware-Itead-Sonoff-RF-Bridge---Direct-Hack) bypasses the EFM8BB1 entirely and lets ESPurna handle the encoding/decoding.  
  Key points: 
  * Fully integrated in ESPurna.
  * Types of hardware recognized: anything recognized by the [rc-switch library](https://github.com/sui77/rc-switch).
  * You must use the solder and physically modify the Sonoff board.

## Flashing

![Sonoff RF Bridge board](images/flashing/sonoff-rf-bridge-v2.jpg)

Flashing esp8285:
  * disconnect the sonoff-rf-bridge from all power sources
  * move the switch towards off position (towards the 5pin serial connector)
  * press and hold the button on the side
  * connect serial cable (gnd, rx, tx, 3v3)
  * flash firmware
## Issues

*TODO*