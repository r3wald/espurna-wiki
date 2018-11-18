# InterMitTech QuinLED

![InterMitTech QuinLED](images/devices/intermittech-quinled.jpg)

|Property|Value|
|---|---|
|Manufacturer|InterMitTech|
|Product page|[http://blog.quindorian.org/2017/02/esp8266-led-lighting-quinled-v2-6-pcb.html/](http://blog.quindorian.org/2017/02/esp8266-led-lighting-quinled-v2-6-pcb.html/)|
|Wiki page||
|Build flag|`INTERMITTECH_QUINLED`|

## Introduction
The board supports a wide range of input voltages and has a voltage regulator built in. The regulator must be set to 3.3V **BEFORE** plugging in the ESP-01.
Once programmed, the board can control 2 channels using PWM and both channels can be switched on/off at the same time using a virtual switch.

## Flashing

The board uses a standard ESP-01 module, so it can either be programmed using a standalone programmer, via serial - either using the onboard headers, or USB serial port, and OTA.

NOTE: It's a 3.3V board, so don't use 5V serial connections.

## Issues

Since Espurna does not support non-RGB light at the moment (Novemmber 2018) when using Home Assistant MQTT auto discovery, QuinLED would show up as one light, with 2 channels. You can emulate 2 separate lights by using following example config in HASS:

```yaml
platform: mqtt
  name: "Kitchen 1"
  command_topic: "QUINLED/channel/0/set"
  payload_off: "OFF"
  brightness_command_topic: "QUINLED/channel/0/set"
  brightness_state_topic: "QUINLED/channel/0"
  on_command_type: "brightness"

platform: mqtt
  name: "Kitchen 2"
  command_topic: "QUINLED/channel/1/set"
  payload_off: "OFF"
  brightness_command_topic: "QUINLED/channel/1/set"
  brightness_state_topic: "QUINLED/channel/1"
  on_command_type: "brightness"
```