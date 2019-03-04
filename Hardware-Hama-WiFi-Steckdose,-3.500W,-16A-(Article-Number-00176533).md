# Hama WiFi Steckdose (00176533)

![Hama WiFi Steckdose 00176533](images/devices/hama-wifi-steckdose-00176533.jpg)

|Property|Value|
|---|---|
|Manufacturer|Hama|
|Product page|[https://at.hama.com/00176533/hama-wifi-steckdose-3500w-16a](https://at.hama.com/00176533/hama-wifi-steckdose-3500w-16a)|
|Build flag|`HAMA_WIFI_STECKDOSE_00176533`|
|Voltage|<span style="color:red">3V3 MCU, 5V relay</span>|

## Introduction

The [Hama WiFi Steckdose 00176533](https://at.hama.com/00176533/hama-wifi-steckdose-3500w-16a) is a smart plug that comes with a Schuko-F plug. It is meant turn any regular wall outlet into a smart outlet. It sports a button for manual operation and two LEDs, a red one in sync with the relay status and the other blue one for the WiFi status.

There is a identically looking one with a different article number available, these instructions here cover the **00176533** model (written on the rear label). 

If someone has the [00176552](https://de.hama.com/00176552/hama-wifi-steckdose-3680w-16a) model and can confirm these instructions work for this model too, please report.

## Flashing

![Hama WiFi Steckdose 00176533 - Inside front view](images/flashing/hama-wifi-steckdose-00176533-open.jpg)

There is a custom WiFi PCB based on a [TYWE3S module](https://docs.tuya.com/en/hardware/WiFi-module/wifi-e3s-module.html) soldered perpendicular into the main PCB (not visible in above picture, but you see the solder joints)

I found it easiest to remove the add on board by desoldering iut from the main PCB and attach some wires with a pinheader to it, supplying it with 3.3V from my USB-UART converter.

Solder a 4 pin male or female header and connect it to your USB-to-UART bridge.  Then press and hold the button and connect the programmer to your computer. The micro-controller will boot into flash mode and you are ready to update the firmware.