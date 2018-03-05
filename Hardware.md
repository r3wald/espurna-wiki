# Supported Hardware

This is the official list of supported hardware for the ESPurna firmware. The hardware configuration for each of these boards can be selected by supplying the build flag (see [Firmware section](Firmware.h)).

> **CAUTION: Never ever connect any of these devices to your computer and to mains at the same time. Never ever manipulate them while connected to mains. Seriously. I don't want you to die. I hold no responsibility for any damage to you, your family, your house,... for any action or results derived from flashing or using these devices.**


> **CAUTION:  Different devices are flashed at different voltages.  Make sure your USB-to-UART device is set to the correct one or you risk destroying your device.**

## Sonoff Modules

| Board | Build flag | Summary |
| --- | --- | --- |
| [IteadStudio Sonoff Basic](Hardware-Iteadstudio-Sonoff-Basic) | `ITEAD_SONOFF_BASIC` | Switch |
| [IteadStudio Sonoff RF](Hardware-Iteadstudio-Sonoff-RF) | `ITEAD_SONOFF_RF` | Switch with RF Receiver |
| [IteadStudio Sonoff TH10/16](Hardware-Iteadstudio-Sonoff-TH) | `ITEAD_SONOFF_TH` | Switch with Temperature and Humidity Monitoring |
| [IteadStudio Sonoff POW](#iteadstudio-sonoff-pow) | `ITEAD_SONOFF_POW` | Switch With Power Consumption Measurement |
| [IteadStudio Sonoff DUAL](#iteadstudio-sonoff-dual) | `ITEAD_SONOFF_DUAL` <br> `ITEAD_SONOFF_DUAL_R2`  | 2 Switches|
| [IteadStudio Sonoff 4CH](#iteadstudio-sonoff-4ch) | `ITEAD_SONOFF_4CH` |  4 Switches with din rail mounting |
| [IteadStudio Sonoff 4CH Pro](#iteadstudio-sonoff-4ch-pro) | `ITEAD_SONOFF_4CH_PRO` | 4 Switches with din rail mounting and RF Receiver|
| [IteadStudio Sonoff TOUCH](#iteadstudio-sonoff-touch) | `ITEAD_SONOFF_TOUCH` | Touch Wall Switch|
| [IteadStudio Sonoff B1](#iteadstudio-sonoff-b1) | `ITEAD_SONOFF_B1` | Dimmable E27 LED Lamp RGB Color Light Bulb|
| [IteadStudio Sonoff T1](Hardware-Iteadstudio-Sonoff-T1) | `ITEAD_SONOFF_T1_1CH` <br> `ITEAD_SONOFF_T1_2CH` <br> `ITEAD_SONOFF_T1_3CH` | 1-3 Gang Touch Wall Switch |
| [IteadStudio Sonoff LED](#iteadstudio-sonoff-led) | `ITEAD_SONOFF_LED` | Adjustable LED strip
| IteadStudio Sonoff 433 RF Bridge | `ITEAD_SONOFF_RFBRIDGE` | Bridge between 433MHz RF and WiFi |
| [IteadStudio Slampher](#iteadstudio-slampher)<br>[IteadStudio Slampher 2.0](#iteadstudio-slampher-v20)  | `ITEAD_SLAMPHER` | 433MHz RF & WiFi Smart Light Bulb Holder
| [IteadStudio S20](#iteadstudio-s20-smart-socket) | `ITEAD_S20` | Outlet
| [IteadStudio 1CH Inching](#iteadstudio-1ch-inching) | `ITEAD_1CH_INCHING` | [Inching/Self-Locking Switch](https://www.quora.com/What-is-an-inching-switch) |
| [IteadStudio Motor Clockwise/Anticlockwise](#iteadstudio-motor-clockwiseanticlockwise) | `ITEAD_MOTOR` | Controls 7-32V DC or 125-250V AC motor|
| [IteadStudio Sonoff SV](#iteadstudio-sonoff-sv) | `ITEAD_SONOFF_SV` |  5-24V low voltage Switch |
| IteadStudio BN-SZ01 | `ITEAD_BNSZ01` | LED Ceiling Light |

## Other modules

| Board | Build flag |
| --- | --- |
| [AI-Thinker AI Light / Noduino OpenLight](#ai-thinker-ai-light-noduino-openlight) | `AITHINKER_AI_LIGHT` |
| [Magic Home LED Controller](#magic-home-led-controller) | `MAGICHOME_LED_CONTROLLER` <br> `MAGICHOME_LED_CONTROLLER_23` <br> `MAGICHOME_LED_CONTROLLER_20` |
| Huacanxing H801 | `HUACANXING_H801` <br> `HUACANXING_H802` |
| WiOn 50055 | `WION_50055` |
| EXS WiFi Relay v3.1 | `EXS_WIFI_RELAY_V31` |
| [Wemos D1 Mini Relay Shield](#wemos-d1-mini-relay-shield) | `WEMOS_D1_MINI_RELAYSHIELD` |
| Autohometion LYT8266 | `AUTHOMETION_LYT8266` |
| Xenon SM PW 702U | `XENON_SM_PW702U` |
| Arilux AL-LC | `ARILUX_AL_LC01` <br> `ARILUX_AL_LC02` <br> `ARILUX_AL_LC06` <br> `ARILUX_AL_LC11` <br> `ARILUX_E27` |
| QuinLED | `INTERMITTECH_QUINLED` |
| [NodeMCU Lolin](#nodemcu-lolin) | `NODEMCU_LOLIN` |

## Custom Boards

| Board | Build flag |
| --- | --- |
| [Tinkerman's ESPurna H](#tinkermans-espurna-h) | `TINKERMAN_ESPURNA_H06` <br> `TINKERMAN_ESPURNA_H08` |
| Tinkerman's ESPurna Switch | `TINKERMAN_ESPURNA_SWITCH` |
| ManCaveMade ESPLive | `MANCAVEMADE_ESPLIVE` |  
| [Electrodragon ESP Relay Board](#electrodragon-esp-relay-board) | `ELECTRODRAGON_WIFI_IOT` |
| [WorkChoice EcoPlug](#workchoice-ecoplug) | `WORKCHOICE_ECOPLUG` |
| [Jan Goedeke Wifi Relay Board (NC/NO)](#jangoe-wifi-relay-board) | `JANGOE_WIFI_RELAY_NC` <br> `JANGOE_WIFI_RELAY_NO` |
| [OpenEnergyMonitor Wifi MQTT Relay / Thermostat](#openenergymonitor-wifi-mqtt-relay-thermostat) | `OPENENERGYMONITOR_MQTT_RELAY` |
| [Jorge García Wifi + Relay Board Kit](#jorge-garcia-wifi-relays-board-kit) | `JORGEGARCIA_WIFI_RELAYS` |

## Generic boards

| Board | Build flag |
| --- | --- |
| Generic 8 Channel board | `GENERIC_8CH` |
| Generic ECH1560 | `GENERIC_ECH1560` |
| Generic V9261F | `GENERIC_V9261F` |

---

## IteadStudio Sonoff POW

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-pow.html](https://www.itead.cc/sonoff-pow.html)|
|Build flag|`ITEAD_SONOFF_POW`|
| Voltage |  <span style="color:red">3v3</span> |


### Flashing

![Sonoff POW - Inside back view](images/flashing/sonoff-pow-flash.jpg)

Same as for the [Sonoff TH](#iteadstudio-sonoff-th) above.

---

## IteadStudio Sonoff DUAL

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-dual.html](https://www.itead.cc/sonoff-dual.html)|
|Build flag|`ITEAD_SONOFF_DUAL`|
| Voltage |  <span style="color:red">3v3</span> |


### Flashing

![Sonoff DUAL - Inside back view](images/flashing/sonoff-dual-flash.jpg)

The Sonoff Dual it's a bit tricky to flash since GPIO0 is not connected to the button as in the TH or POW, but to the pin 15 in the SIL F330 chip that manages the buttons and the relays. SO you have to locate a pad connected to GPIO and short it to ground while powering the device.

In the picture above you have a location of an available and easily accessible GPIO0 pad. The other required pins are brought out in the top header.

Once flashed you can use OTA to update the firmware without having to open the device.

---

## IteadStudio Sonoff TOUCH

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-touch.html](https://www.itead.cc/sonoff-touch.html)|
|Build flag|`ITEAD_SONOFF_TOUCH`|
| Voltage |  <span style="color:red">3v3</span> |



### Flashing

![Sonoff DUAL - Inside back view](images/flashing/sonoff-touch-flash.jpg)

The Sonoff Touch is a bit tricky to flash since GPIO 0 is not connected to the button as in the TH or POW. So you have to locate the pad for GPIO 0 and short it to ground while powering on the device, once it is on in
flash mode you can remove the GND connection.

The picture above shows the location of the GPIO 0 pad. The other required pins are available on the header at the top which has to be soldered in the existing slots.

Once flashed you can use OTA to update the firmware without having to open the device.

---

## IteadStudio Sonoff 4CH

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-4ch.html](https://www.itead.cc/sonoff-4ch.html)|
|Build flag|`ITEAD_SONOFF_4CH`|
| Voltage |  <span style="color:red">3v3</span> |


### Flashing

You will have to open the case. There is a 5 pin header with VCC33 (3V3), TX, RX and GND. First button is properly labelled FW/IO0 so all you have to do is to connect TX, RX and GND to your USB2UART programmer, press the button and connect the VCC33 pin to power the board and enter flash mode. One very important thing: the **TX and RX pins are crossed**. You have to connect TX to your programmer TX and RX to RX.

---

## IteadStudio Sonoff 4CH Pro

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-4ch-pro.html](https://www.itead.cc/sonoff-4ch-pro.html)|
|Build flag|`ITEAD_SONOFF_4CH_PRO`|
| Voltage |  TODO |


### Flashing

*TODO*

---

## IteadStudio Sonoff B1

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-b1.html](https://www.itead.cc/sonoff-b1.html)|
|Build flag|`ITEAD_SONOFF_B1`|
| Voltage |  TODO |


### Flashing

*TODO*

---

## IteadStudio Sonoff LED

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-led.html](https://www.itead.cc/sonoff-led.html)|
|Build flag|`ITEAD_SONOFF_LED`|
| Voltage |  TODO |

### Flashing

*TODO*

---

## IteadStudio Sonoff SV

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/sonoff-sv.html](https://www.itead.cc/sonoff-sv.html)|
|Build flag|`ITEAD_SONOFF_SV`|
| Voltage |  TODO |


### Flashing

*TODO*

---

## IteadStudio Slampher


|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/slampher.html](https://www.itead.cc/slampher.html)|
|Build flag|`ITEAD_SLAMPHER`|
| Voltage |  <span style="color:red">3v3</span> |



### Flashing

![Slampher - Inside front view](images/flashing/slampher-flash1.jpg)
![Slampher - Flashing short](images/flashing/slampher-flash2.jpg)

There is a 4 pin unpopulated header in a border near the ESP8266 chip. Starting from the little white mark the pins are 3V3, RX, TX and GND. Solder a male or female header here and connect your USB-to-UART programmer.

This time through **the button is not connected to GPIO0** but to a EFM8BB1 micro-controller that also monitors the RF module output.

There are a couple of ways to enter flash mode. Some recommend to move R21 to R20 (at the top right of the first picture above) to connect the button directly to the ESP8266 GPIO0 and use it in the same way as for the Sonoff or Sonoff TH. The drawback is the by doing that you lose the RF capability.

My recommendation is to **temporary shortcut the right pad of the unpopulated R20 footprint** (see second image above) and connect your USB-to-UART board at the same time. You will have to do it just once (unless there is something really wrong in the firmware) and use OTA updates from there on.

---

## IteadStudio Slampher v2.0

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/slampher.html](https://www.itead.cc/slampher.html)|
|Build flag|`ITEAD_SLAMPHER`|
| Voltage |  <span style="color:red">3v3</span> |


### Flashing

![Slampher v2.0 - Programming header](images/flashing/slampher-v20-flash2.jpg)
![Slampher v2.0 - Shortcut GPIO0](images/flashing/slampher-v20-flash1.jpg)

New Slampher boards are labeled "Slampher V2.0 2017-04-14". These boards are slightly different.

There is a 4 pin unpopulated header in a border near the ESP8266 chip. Starting form the closer to the drilled hole they are 3V3, TX, RX and GND. Solder a male or female header here and connect your USB-to-UART programmer.

To enter flash mode the ESPurna user Tomasz Pacak recommends shortcutting the ground pad to the R9 resistor pad closer to the ESP8266 (check the image above). Again this is a temporary shortcut. You will have to do it just once (unless there is something really wrong in the firmware) and use OTA updates from there on.

Also, user [P.B.](https://bitbucket.org/PieBru/) has suggested to add a pushbutton connected between GPIO0 and GND to easily boot the device into flash mode. Check his picture below (adding some hot glue will be a good idea):

![Slampher v2.0 - Flash button](images/flashing/slampher-v20-flash3.jpg)

---

## IteadStudio S20 Smart Socket

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/smart-socket.html](https://www.itead.cc/smart-socket.html)|
|Build flag|`ITEAD_S20`|
| Voltage |  <span style="color:red">3v3</span> |


### Flashing

![S20 Smart Socket - Inside front view](images/flashing/s20-flash.jpg)

There is a labeled header in the front of the PCB and the button is connected to GPIO0, so no problems here.

Solder a 4 pin male or female header and connect it to your USB-to-UART bridge.  Then press and hold the button and connect the programmer to your computer. The micro-controller will boot into flash mode and you are ready to update the firmware.

---

## IteadStudio 1CH Inching

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/smart-home/inching-self-locking-wifi-wireless-switch.html](https://www.itead.cc/smart-home/inching-self-locking-wifi-wireless-switch.html)|
|Build flag|`ITEAD_1CH_INCHING`|
| Voltage |  ? |


### Flashing

![1CH - close shot](images/flashing/1ch-inching-flash.jpg)

The main button is tied to GPIO0 so you can easily enter flash mode powering the board while pressing the button (the one that’s closer to the electrolytic capacitors). Pins 7, 8 and 9 of the PSA-B module are RX, TX and GND. You can use a 3-pin header or pogo pins to connect it.

Check my post here: [http://tinkerman.cat/the-mysterious-ic/](http://tinkerman.cat/the-mysterious-ic/).

---

## IteadStudio Motor Clockwise/Anticlockwise

|Property|Value|
|---|---|
|Manufacturer|Itead Studio|
|Web page|[https://www.itead.cc/smart-home/motor-reversing-wifi-wireless-switch.html](https://www.itead.cc/smart-home/motor-reversing-wifi-wireless-switch.html)|
|Build flag|`ITEAD_MOTOR`|
| Voltage |  ? |


### Flashing

![1CH - close shot](images/flashing/1ch-inching-flash.jpg)

Very much like the 1CH above (actually the pic is from the 1CH). The main button is tied to GPIO0 so you can easily enter flash mode powering the board while pressing the button (the one that’s closer to the electrolytic capacitors). Pins 7, 8 and 9 of the PSA-B module are RX, TX and GND. You can use a 3-pin header or pogo pins to connect it.

---

## Electrodragon ESP Relay Board

|Property|Value|
|---|---|
|Manufacturer|Electrodragon|
|Web page|[http://www.electrodragon.com/product/wifi-iot-relay-board-based-esp8266/](http://www.electrodragon.com/product/wifi-iot-relay-board-based-esp8266/)|
|Build flag|`ELECTRODRAGON_WIFI_IOT`|
| Voltage |  <span style="color:red">5v</span> |


### Flashing

![Electrodragon ESP Relay Board - Front view](images/flashing/electrodragon-flash.jpg)

The Electrodragon ESP Relay Board is pretty easy to flash IF you do not follow their wiki, it's all wrong. Check the picture above and note that:

* Power the board from the 5V pin, GND to GND
* The RX pin in the header should go to your programmer TX pin and
* The TX pin in the header should go to your programmer RX pin
* The button labeled BTN2 is connected to GPIO0, so hold it down while powering the board, I've had better results keeping it down until the flashing starts

---

## WorkChoice EcoPlug

|Property|Value|
|---|---|
|Manufacturer|WorkChoice|
|Web page (non-official)|[http://thegreatgeekery.blogspot.com.es/2016/02/ecoplug-wifi-switch-hacking.html](http://thegreatgeekery.blogspot.com.es/2016/02/ecoplug-wifi-switch-hacking.html)|
|Build flag|`WORKCHOICE_ECOPLUG`|
| Voltage |  TODO |


### Flashing

*TODO*

---

## Wemos D1 Mini Relay Shield

|Property|Value|
|---|---|
|Manufacturer|Wemos|
|Web page|[https://www.wemos.cc/product/relay-shield.html](https://www.wemos.cc/product/relay-shield.html)|
|Build flag|`WEMOS_D1_MINI_RELAYSHIELD`|
| Voltage |  USB |


### Flashing

The Wemos D1 Mini has an microUSB port, can't be easier.

---

## NodeMCU Lolin

|Property|Value|
|---|---|
|Manufacturer|NodeMCU|
|Web page|[http://www.nodemcu.com/index_en.html](http://www.nodemcu.com/index_en.html)|
|Build flag|`NODEMCU_LOLIN`|
| Voltage |  USB |


### Flashing

The NodeMCU has an microUSB port, can't be easier.

---

## JanGoe Wifi Relay Board

|Property|Value|
|---|---|
|Manufacturer|JanGoe|
|Web page|[https://github.com/JanGoe/esp8266-wifi-relay](https://github.com/JanGoe/esp8266-wifi-relay)|
|Build flag|`JANGOE_WIFI_RELAY_NC` or `JANGOE_WIFI_RELAY_NO`|
| Voltage |  <span style="color:red">5v</span> |


### Flashing

![Jan Goedeke Wifi Relay - Top view](images/devices/jangoe-wifi-relay.png)

Connect GPIO0 to GND in the bottom-left header in the picture above and then connect your USB-to-UART programmer to the top-left corner header.

---

## OpenEnergyMonitor WiFi MQTT Relay Thermostat

|Property|Value|
|---|---|
|Manufacturer|OpenEnergyMonitor|
|Web page|[http://guide.openenergymonitor.org/integrations/mqtt-relay/](http://guide.openenergymonitor.org/integrations/mqtt-relay/)|
|Build flag|`OPENENERGYMONITOR_MQTT_RELAY`|
| Voltage |  <span style="color:red">3v3</span> |



### Flashing

Check the "Programming (advanced)" section in the [MQTT Relay Guide](http://guide.openenergymonitor.org/integrations/mqtt-relay/).

---

## Jorge García Wifi Relays Board Kit

|Property|Value|
|---|---|
|Manufacturer|Jorge García|
|Web page|https://www.tindie.com/products/jorgegarciadev/wifi--relays-board-kit|
|Build flag|`JORGEGARCIA_WIFI_RELAYS`|
| Voltage |  <span style="color:red">5V</span> |


### Flashing

![Wifi Relays Board Kit - Top view](images/flashing/jorge-garcia-wifi-relays-board-lit-flash.jpg)

You have all the required pins in an unpopulated header between the relays and the transformer. Solder a 4 pins male or female header here and connect it to your favorite USB-to-UART module. The VCC pin should be connected to 5V.

Press and hold the "Flash" button and then press and release the "Reset" button. You are now in flash mode and ready to upload the firmware image.

---

## AI-Thinker AI Light / Noduino OpenLight

|Property|Value|
|---|---|
|Manufacturer|AI Thinker / Noduino|
|Web page|[http://wiki.jackslab.org/Noduino_OpenLight](http://wiki.jackslab.org/Noduino_OpenLight) [buy it at Aliexpress](http://s.click.aliexpress.com/e/ybuVN3n)|
|Build flag|`AITHINKER_AI_LIGHT`|
| Voltage |  <span style="color:red">3v3</span> |


The AI Light is a ESP8255 (?) bulb light with 8 high power white LEDs, 6 red LEDs, 4 green LEDs and 4 blue LEDs driven by an My-Semi MY9291 LED driver. The bulb itself comes unbranded but the user manual (only in Chinese) says clearly "Ai Light" with the AI-Thinker logo. It's the same Noduino OpenLight bulb at JackLabs (Noduino, Maike Labs, ICamGo) designed by Jack Tan (comcat @ GitHub).

### Flashing

![AI Light - Flashing](images/flashing/ailight-flash.jpg)

Pop out the bulb head to access the PCB. It's actually 2 PCBs, and outer one with the LEDs and an inner one with the micro-controller and led driver. There are 5 pads labelled with everything you need to flash the ESP on board: 3V3, GND, TX, RX and IO0.

It might seem hard but it's not. Get a 5 wire cable and remove 1-2mm of insulation from the wires, tin them a bit. Apply a hot wire on the pads and leave a small drop of tin on them too. Then just touch each wire with a pad and heat them together for less than a second.

Connect the wires to you FTDI (or alike) board. TX to RX and RX to TX. Connect GND and IO0 to ground and finally 3V3. Once you plug your programmer to the computer the board will boot into flash mode. While you are flashing it you can remove the IO0 connection. Upon reboot it will enter normal mode and you should see the debug messages in the screen.

---

## Magic Home LED Controller

|Property|Value|
|---|---|
|Manufacturer|Magic Home|
|Web page|[Magic Home LED Controller at Aliexpress](http://s.click.aliexpress.com/e/VNnYVjE)|
|Build flag|`MAGICHOME_LED_CONTROLLER`|
| Voltage | Use power supply |


This is a small controller for RGBW 5050 LED strips, the kind of strips that show just one color on all the LEDs at the same time (no WS2812 controller). It has what looks like to be an ESP-12E module but it's not. My board reports being a generic 1MB ESP8266 module with QIO flash mode but other user's have reported it to be connected in DIO configuration like a ESP8285.

### Flashing

![Magic Home LED Controller - Flashing](images/flashing/ledcontroller-flash.jpg)

Some thin tip soldering is required here. Check the picture above to solder 4 wires to the exposed pads. Then connect those wires to your programmer. RX and TX crossed and IO0 to GND to enter flash mode on boot. Then power the board through the built in 2.1mm jack.

![Magic Home 2.0 LED Controller - Flashing](images/flashing/ledcontroller-20-flash.jpg)
Picture by user [Soif](https://bitbucket.org/soif/).

Version 2.0 of the board is different. Solder the 4 wires on the module (GND to GND, RX to TX in your USB2UART and TX to RX and GPIO0 to GND), then power the board via the 12V connector.

---

## Tinkerman's ESPurna H

|Property|Value|
|---|---|
|Manufacturer|Tinkerman|
|Web page|[ESPurna-H board at tinkerman.cat](http://tinkerman.cat/the-espurna-board-a-smart-wall-switch-with-power-monitoring/)|
|Build flag|`TINKERMAN_ESPURNA_H`|
| Voltage |  <span style="color:red">5v</span> |


Custom smart switch board that features:

* 50x50mm form factor that fits behind a standard wall switch here in Spain
* SPDT 10A relay with NO and NC connections brought out
* Connections for external button and notification LED
* HLW8012 chip for power monitoring

### Flashing

![Tinkerman's ESPurna-H Board - Flashing](images/flashing/espurna-h-flash.jpg)

The board has a programming header with 5V (yes, not 3V3 but 5V), GND, TX, RX (remember to cross them to RX and TX in your programmer) and GPIO0. GPIO0 must be connected to GND when powering the board to enter flash mode.
