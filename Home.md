# ESPurna Firmware

ESPurna ("spark" in Catalan) is a custom firmware for ESP8285/ESP8266 based smart switches, lights and sensors.
It uses the Arduino Core for ESP8266 framework and a number of 3rd party libraries.

[![version](https://img.shields.io/badge/version-1.12.4-brightgreen.svg)](CHANGELOG.md)
![branch](https://img.shields.io/badge/branch-master-orange.svg)
[![travis](https://travis-ci.org/xoseperez/espurna.svg?branch=master)](https://travis-ci.org/xoseperez/espurna)
[![codacy](https://img.shields.io/codacy/grade/c9496e25cf07434cba786b462cb15f49/master.svg)](https://www.codacy.com/app/xoseperez/espurna/dashboard)
[![license](https://img.shields.io/github/license/xoseperez/espurna.svg)](LICENSE)
[![twitter](https://img.shields.io/twitter/follow/xoseperez.svg?style=social)](https://twitter.com/intent/follow?screen_name=xoseperez)

---

## Features

* *KRACK* vulnerability free (when built with Arduino Core >= 2.4.0)
* Support for **multiple ESP8266-based boards** ([check list](https://github.com/xoseperez/espurna/wiki/Hardware))
* Power saving options
* Wifi **AP Mode** or **STA mode**
    * Supports static IP
    * Up to 5 different networks can be defined
    * Scans for strongest network if more than one defined (also available in web UI)
    * Handles correctly multiple AP with the same SSID
    * Defaults to AP mode (also available after double clicking the main button)
* Network visibility
    * Supports mDNS (service reporting and metadata) both server mode and client mode (.local name resolution)
    * Supports NetBIOS, LLMNR and Netbios (when built with Arduino Core >= 2.4.0) and SSDP (experimental)
* Switch management
    * Support for **push buttons** and **toggle switches**
    * Configurable **status on boot** per switch (always ON, always OFF, same as before or toggle)
    * Support for **pulse mode** per switch (normally ON or normally OFF) with configurable time
    * Support for **relay synchronization** (all equal, only one ON, one and only on ON)
    * Support for **MQTT groups** to sync switches between devices
    * Support for **delayed ON/OFF**
* **MQTT** enabled
    * **SSL/TLS support** (not on regular builds, see [#64](https://github.com/xoseperez/espurna/issues/64))
    * Switch on/off and toggle relays, group topics (sync relays between different devices)
    * Report button event notifications
    * Enable/disable pulse mode
    * Change LED notification mode
    * Remote reset the board
    * Fully configurable in webUI (broker, user, password, QoS, keep alive time, retain flag, client ID)
* **Scheduler** to automatically turn on, off or toggle any relay at a given time and day
* **Alexa** integration using the [FauxmoESP Library](https://bitbucket.org/xoseperez/fauxmoesp)
* [**Google Assistant**](http://tinkerman.cat/using-google-assistant-control-your-esp8266-devices/) integration using IFTTT and Webhooks (Google Home, Allo)
* [**Domoticz**](https://domoticz.com/) integration via MQTT
* [**Home Assistant**](https://home-assistant.io/) integration
    * Support for switches (on/off)
    * Support for lights (color, brightness, on/off state)
    * Supports MQTT auto-discover feature (switches, lights and sensors)
    * Integration via MQTT Discover or copy-pasting configuration code
* [**InfluxDB**](https://www.influxdata.com/) integration via HTTP API
* [**Thingspeak**](https://thingspeak.com/) integration via HTTP API (HTTPS available for custom builds)
* **Sonoff RF Bridge** support
    * Multiple virtual switches (tested with up to 16)
    * MQTT-to-RF two-way bridge (no need to learn codes)
    * Support for https://github.com/Portisch/RF-Bridge-EFM8BB1 custom firmware
* Support for [different **sensors**](Sensors)
    * Environment
        * **DHT11 / DHT22 / DHT21 / AM2301 / Itead's SI7021**
        * **BMP280** and **BME280** temperature, humidity (BME280) and pressure sensor by Bosch
        * **SI7021** temperature and humidity sensor
        * **SHT3X** temperature and humidity sensor over I2C (Wemos shield)
        * **Dallas OneWire sensors** like the DS18B20
        * **MHZ19** CO2 sensor
        * **PMSX003** dust sensor
        * **BH1750** luminosity sensor
    * Power monitoring
        * **HLW8012** using the [HLW8012 Library](https://bitbucket.org/xoseperez/hlw8012) (Sonoff POW)
        * Non-invasive **current sensor** using **internal ADC** or **ADC121** or **ADS1115**
        * **ECH1560** power monitor chip
        * **V9261F** power monitor chip
    * Raw analog and digital sensors
    * Simple pulse counter
    * Support for different units (Fahrenheit or Celsius, Watts or Kilowatts, Joules or kWh)
* Support for LED lights
    * MY92XX-based light bulbs and PWM LED strips (dimmers) up to 5 channels (RGB, cold white and warm white, for instance)
    * RGB and HSV color codes supported
    * Manage channels individually
    * Temperature color supported (in [mired](https://en.wikipedia.org/wiki/Mired) and [kelvin](https://en.wikipedia.org/wiki/Color_temperature)) via MQTT / REST API
    * Flicker-free PWM management
    * Soft color transitions
    * Color synchronization between light using MQTT
    * Option to have separate switches for each channel
* Support for simple 433MHz RF receivers
* Support for UART-to-MQTT bidirectional bridge
* Fast asynchronous **HTTP Server**
    * Configurable port
    * Basic authentication
    * Web-based configuration
    * Relay switching and sensor data from the web interface
    * Handle color, brightness, and white/warm channels for lights
    * Websockets-based communication between the device and the browser
    * Backup and restore settings option
    * Upgrade firmware from the web interface
    * Works great behind a [secured reverse proxy](http://tinkerman.cat/secure-remote-access-to-your-iot-devices/)
* **REST API** (enable/disable from web interface)
    * GET and PUT relay status
    * Change light color (for supported hardware)
    * GET sensor data (power, current, voltage, temperature and humidity) depending on the available hardware
    * Works great behind a secured reverse proxy
* **RPC API** (enable/disable from web interface)
    * Remote reset the board
* **Over-The-Air** (OTA) updates even for 1Mb boards
    * Manually from PlatformIO or Arduino IDE
    * Automatic updates through the [NoFUSS Library](https://bitbucket.org/xoseperez/nofuss)
    * Update from web interface using pre-built images
* **Command line configuration**
    * Change configuration
    * Run special commands
* **Telnet support**
    * Enable/disable via the web UI
    * Shows debug info and allows to run terminal commands
* **NTP** for time synchronization
    * Supports worldwide time zones
    * Compatible with DST
* **Unstable system check**
    * Detects unstable system (crashes on boot continuously) and defaults to a stable system
    * Only WiFi AP, OTA and Telnet available if system is flagged as unstable
* Configurable LED notifications based on WiFi status, relays status or MQTT messages.
* Button interface
    * Click to toggle relays
    * Double click to enter AP mode (only main button)
    * Long click (>1 second) to reboot device (only main button)
    * Extra long click (>10 seconds) to go back to factory settings (only main button)
    * Specific definitions for touch button devices (ESPurna Switch, Sonoff Touch & T1)

## Notices

---
> **2018-05-09**: Default branch in GitHub is now the development branch "dev". The stable branch (the one used to create the binaries) is "[master](https://github.com/xoseperez/espurna/tree/master)".

---
> **2018-01-24**: This repository has been migrated from Bitbucket to GitHub. There were a number of reason to migrate the repository to GitHub. I like Bitbucket and I'm still using it for a lot of projects, but ESPurna has grown and its community as well. Some users have complain about Bitbucket not being enough community-focused. This change is mainly aimed to use a platform with greater acceptance on the open-source community and tools better suited to them (to you), like the possibility to contribute to the documentation in an easy way.
>
>What happened with all the info in Bitbucket? Well, most of it has been ported to GitHub, albeit with some quirks:
>
>* **Code** has, of course been migrated completely
>* **Issues** are all on GitHub already **but** all issues and comments show up as reported by me. The original reporter is referenced inside the body of the issue (or comment) with a link to his/her profile at Bitbucket and a link to his/her profile at GitHub if it happens to be the same username. I **suggest all reporters to subscribe to the issues they originally filed** (search for your BitBucket username to list them).
>* **Pull requests** historic has not been migrated. At the moment of the migration all pull-requests have been either merged or declined. Of course, those PR merged are in the code base, but the historic and comments in the PR pages will be lost.
>* **Documentation** it's on it way, first step will be to migrate existing wiki, maybe with a new TOC structure
>* **Watchers**, **Forks**, I'm afraid they are all gone. Visit the new repo home and click on the "Watch" button on the top right. And as you do it click also on the "Star" button too :)
>
>I apologize for any inconvenience this migration may have caused. I have decided to do it the hard way.

---
> **2018-01-11**: As of current version (1.12.0) ESPurna is tested using Arduino Core 2.3.0 and it's meant to be built against that version.

---
> **2017-08-26**: since version 1.9.0 the default **MQTT topics for commands have changed**. They all now end with "/set". This means you will have to change your controller software (Node-RED or alike) to send messages to -for instance- "/home/living/light/relay/0/set". The device will publish its state in "/home/living/light/relay/0" like before.

---
> **2017-07-24**: Default flash layout changed in 1.8.3, as an unpredicted consequence devices will not be able to persist/retrieve configuration if flashed with 1.8.3 via **OTA** from **PlatformIO**. Please check issue [#187](https://github.com/xoseperez/espurna/issues/187).

---

## Contribute

There are several ways to contribute to ESPurna development. You can contribute to the repository by doing:

* Pull requests (fixes, enhancements, new features... are very welcome)
* Documentation (I reckon I'm bad at it)
* Testing (filing issues or help resolving them, they take a lot of time and sometimes I don't have the required hardware to test them all)

And of course you can always buy me a beer, coffee, tea,... via the donation button in the [README](https://github.com/xoseperez/espurna).

## Documentation

For more information please refer to the [ESPurna Wiki](https://github.com/xoseperez/espurna/wiki).

## Supported hardware

Here is the list of supported hardware. For more information please refer to the [ESPurna Wiki Hardware page](https://github.com/xoseperez/espurna/wiki/Hardware).

||||
|---|---|---|
|![Tinkerman Espurna H](images/devices/tinkerman-espurna-h.jpg)|||
|**[Tinkerman's ESPurna H](Hardware-Tinkerman-ESPurna-H)**|||
|![Itead Sonoff RF Bridge](images/devices/itead-sonoff-rfbridge.jpg)|||
|**[ITEAD Sonoff RF Bridge](Hardware-Itead-Sonoff-RF-Bridge)**|||
|![Itead Sonoff Basic](images/devices/itead-sonoff-basic.jpg)|![Itead Sonoff RF](images/devices/itead-sonoff-rf.jpg)|![Itead Sonoff Dual/Dual R2](images/devices/itead-sonoff-dual.jpg)|
|**[ITEAD Sonoff Basic](Hardware-Itead-Sonoff-Basic)**|**[ITEAD Sonoff RF](Hardware-Itead-Sonoff-RF)**|**[ITEAD Sonoff Dual/Dual R2](Hardware-Itead-Sonoff-Dual)**|
|![Itead Sonoff POW](images/devices/itead-sonoff-pow.jpg)|![Itead Sonoff TH10/TH16](images/devices/itead-sonoff-th.jpg)|![Electrodragon WiFi IOT](images/devices/electrodragon-wifi-iot.jpg)|
|**[ITEAD Sonoff POW](Hardware-Itead-Sonoff-POW)**|**[ITEAD Sonoff TH10/16](Hardware-Itead-Sonoff-TH)**|**[Electrodragon ESP Relay Board](Hardware-Electrodragon-ESP-Relay-Board)**|
|![Itead Sonoff 4CH](images/devices/itead-sonoff-4ch.jpg)|![Itead Sonoff 4CH Pro](images/devices/itead-sonoff-4ch-pro.jpg)|![OpenEnergyMonitor WiFi MQTT Relay / Thermostat](images/devices/openenergymonitor-mqtt-relay.jpg)|
|**[ITEAD Sonoff 4CH](Hardware-Itead-Sonoff-4CH)**|**[ITEAD Sonoff 4CH Pro](Hardware-Itead-Sonoff-4CH-Pro)**|**[OpenEnergyMonitor Wifi MQTT Relay / Thermostat](Hardware-OpenEnergyMonitor-Wifi-MQTT-Relay)**|
|![Itead S20](images/devices/itead-s20.jpg)|![WorkChoice EcoPlug](images/devices/workchoice-ecoplug.jpg)|![Schuko Wifi Plug](images/devices/schuko-wifi-plug.jpg)|
|**[ITEAD S20](Hardware-Itead-S20)**|**[WorkChoice EcoPlug](Hardware-WorkChoice-EcoPlug)**|**[Schuko Wifi Plug](Hardware-Schuko-Wifi-Plug)**|
|![Power meters based on V9261F](images/devices/generic-v9261f.jpg)|![Power meters based on ECH1560](images/devices/generic-v9261f.jpg)|![KMC 70011 /w power meter](images/devices/kmc-70011.jpg)|
|**[Power meters based on V9261F](Hardware-Generic-V9261F)**|**[Power meters based on ECH1560](Hardware-Generic-ECH1560)**|**[KMC 70011](Hardware-KMC-70011)**|
|![Itead Sonoff Touch](images/devices/itead-sonoff-touch.jpg)|![Itead Sonoff T1](images/devices/itead-sonoff-t1.jpg)||
|**[ITEAD Sonoff Touch](Hardware-Itead-Sonoff-Touch)**|**[ITEAD Sonoff T1](Hardware-Itead-Sonoff-T1)**||
|![Itead Slampher](images/devices/itead-slampher.jpg)|![ITEAD Slampher 2.0](images/devices/itead-slampher.jpg)||
|**[ITEAD Slampher](Hardware-Itead-Slampher)**|**[ITEAD Slampher 2.0](Hardware-Itead-Slampher-v2)**||
|![Itead Sonoff B1](images/devices/itead-sonoff-b1.jpg)|![AI-Thinker Wifi Light / Noduino OpenLight](images/devices/aithinker-ai-light.jpg)|![Authometion LYT8266](images/devices/authometion-lyt8266.jpg)|
|**[ITEAD Sonoff B1](Hardware-Itead-Sonoff-B1)**|**[AI-Thinker AI Light / Noduino OpenLight](Hardware-AI-Thinker-AI-Light)**|**[Autohometion LYT8266](Hardware-Autohometion-LYT8266)**|
|![Itead Sonoff LED](images/devices/itead-sonoff-led.jpg)|![Itead BN-SZ01](images/devices/itead-bn-sz01.jpg)||
|**[ITEAD Sonoff LED](Hardware-Itead-Sonoff-LED)**|**[ITEAD BN-SZ01](Hardware-Itead-BN-SZ01)**||
|![Arilux AL-LC01 (RGB)](images/devices/arilux-al-lc01.jpg)|![Arilux AL-LC02 (RGBW)](images/devices/arilux-al-lc02.jpg)|![Arilux AL-LC06 (RGBWWCW)](images/devices/arilux-al-lc06.jpg)|
|**[Arilux AL-LC01 (RGB)](Hardware-Arilux-AL-LCxx)**|**[Arilux AL-LC02 (RGBW)](Hardware-Arilux-AL-LCxx)**|**[Arilux AL-LC06 (RGBWWCW)](Hardware-Arilux-AL-LC06)**|
|![Arilux AL-LC11 (RGBWWW) & RF](images/devices/arilux-al-lc11.jpg)|![MagicHome LED Controller (1.0 and 2.x)](images/devices/magichome-led-controller.jpg)|![Huacanxing H801/802](images/devices/huacanxing-h801.jpg)|
|**[Arilux AL-LC11 (RGBWWW) & RF](Hardware-Arilux-AL-LCxx)**|**[MagicHome LED Controller (1.0/2.x)](Hardware-Magic-Home-LED-Controller)**|**[Huacanxing H801/H802](Hardware-Huacanxing-H80x)**|
|![Itead Sonoff SV](images/devices/itead-sonoff-sv.jpg)|![Itead 1CH Inching](images/devices/itead-1ch-inching.jpg)|![Itead Motor Clockwise/Anticlockwise](images/devices/itead-motor.jpg)|
|**[ITEAD Sonoff SV](Hardware-Itead-Sonoff-SV)**|**[ITEAD 1CH Inching](Hardware-Itead-1CH)**|**[ITEAD Motor Clockwise/Anticlockwise](Hardware-Itead-Motor)**|
|![Jan Goedeke Wifi Relay (NO/NC)](images/devices/jangoe-wifi-relay.png)|![Jorge García Wifi + Relays Board Kit](images/devices/jorgegarcia-wifi-relays.jpg)|![EXS Wifi Relay v3.1](images/devices/exs-wifi-relay-v31.jpg)|
|**[Jan Goedeke Wifi Relay Board (NC/NO)](Hardware-Jan-Goedeke-Wifi-Relay-Board)**|**[Jorge García Wifi + Relay Board Kit](Hardware-Jorge-Garcia-Wifi-Relay-Board)**|**[EXS WiFi Relay v3.1](Hardware-EXS-WiFi-Relay-v3.1)**|
|![Wemos D1 Mini Relay Shield](images/devices/wemos-d1-mini-relayshield.jpg)|![Witty Cloud](images/devices/witty-cloud.jpg)||
|**[Wemos D1 Mini Relay Shield](Hardware-Wemos-D1-Mini-Relay-Shield)**|**[Witty Cloud](Hardware-Witty-Cloud)**||

**Other supported boards:**
[WiOn 50055](Hardware-WiOn-50055), [ManCaveMade ESPLive](Hardware-ManCaveMade-ESPLive), [InterMitTech QuinLED 2.6](Hardware-QuinLED)
[Arilux E27](Hardware-Arilux-E27), [Xenon SM PW 702U](Hardware-Xenon-SM-PW-702U), YJZK 2-gang switch, STM_RELAY, [Maxcio W-US002S](Hardware-Maxcio-W-US002S), [HEYGO HY02](Hardware-HEYGO-HY02), [YiDian XS-SSA05](Hardware-YiDian-XS-SSA05), [Tonbux Powerstrip02](Hardware-Tonbux-Powerstrip02)

## License

Copyright (C) 2016-2018 by Xose Pérez (@xoseperez)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.