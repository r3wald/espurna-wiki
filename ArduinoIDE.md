## **Installing the Arduino IDE** ##

You can install the Arduino IDE by downloading it from [arduino.cc](https://www.arduino.cc/en/Main/Software). Do not download the installer but the compressed file targeted to your OS. This way you will be able to decompress it on your system or on an USB pendrive for instance and carry it with you anywhere. They call it **portable** Arduino IDE.

All you have to do is decompress it (unzip it or unbzip it) where you want, open the folder and create a "portable" subfolder there. Now you can open the Arduino IDE by clicking on the executable.

## **Setting up the IDE** ##

### Install the Arduino Core for ESP8266 ###

First step is to install support for ESP8266 based boards on the Arduino IDE through the Board Manager. These instruction are copied and adapted from the Arduino Core for ESP8266 documentation here: [https://github.com/esp8266/Arduino/blob/master/doc/installing.md](https://github.com/esp8266/Arduino/blob/master/doc/installing.md).

- Start Arduino and open Preferences window.
- Enter ```http://arduino.esp8266.com/stable/package_esp8266com_index.json``` into *Additional Board Manager URLs* field. You can add multiple URLs, separating them with commas.
- Open Boards Manager from Tools > Board menu and find *esp8266* platform.
- Select the version you need from a drop-down box.
- Click *install* button.

## **Add a new flash layout** ##

To increase the available space for firmware on 1M boards it's a good idea to use a flash layout with no partition for SPIFFS, since ESPurna does not use it. Unfortunately there is no layout available for 1M boards without SPIFFS, so we will have to modify some files in out "portable" folder to achieve this.

First edit the "<arduino folder>/portable/packages/esp8266/hardware/esp8266/2.3.0/boards.txt" file and locate the definitions for "generic.menu.FlashSize.1M64". These few lines define a layour for 1Mbytes ESP8266 boards with 64KBytes SPIIFS. You will have to create a new group of lines below that one for our new layout:

```
generic.menu.FlashSize.1M0=1M (no SPIFFS)
generic.menu.FlashSize.1M0.build.flash_size=1M
generic.menu.FlashSize.1M0.build.flash_ld=eagle.flash.1m0.ld
generic.menu.FlashSize.1M0.upload.maximum_size=1023984

```

Same thing for ESP8295 boards, locate the "esp8285.menu.FlashSize.1M64" group of lines and copy the following line below that one:

```
esp8285.menu.FlashSize.1M0=1M (no SPIFFS)
esp8285.menu.FlashSize.1M0.build.flash_size=1M
esp8285.menu.FlashSize.1M0.build.flash_ld=eagle.flash.1m0.ld
esp8285.menu.FlashSize.1M0.upload.maximum_size=1023984

```

These new flash layout refer to a file (eagle.flash.1m0.ld) that does not exist, so we will create that one too. It has to be in "<arduino folder>/portable/packages/esp8266/hardware/esp8266/2.3.0/tools/sdk/ld/eagle.flash.1m0.ld" with these contents:

```
/* Flash Split for 1M chips, no SPIFFS */
/* sketch 999KB */
/* eeprom 20KB */

MEMORY
{
  dport0_0_seg :                        org = 0x3FF00000, len = 0x10
  dram0_0_seg :                         org = 0x3FFE8000, len = 0x14000
  iram1_0_seg :                         org = 0x40100000, len = 0x8000
  irom0_0_seg :                         org = 0x40201010, len = 0xf9ff0
}

PROVIDE ( _SPIFFS_start = 0x402FB000 );
PROVIDE ( _SPIFFS_end = 0x402FB000 );
PROVIDE ( _SPIFFS_page = 0 );
PROVIDE ( _SPIFFS_block = 0 );

INCLUDE "../ld/eagle.app.v6.common.ld"
```

Done! Now if you restart your Arduino IDE and select either "ESP8266 Generic Module" or "ESP8285 Generic Module" you should see a "1M (no SPIFFS)" option under Flash Size. That's the one you should use.

## **Installing dependencies** ##

The ESPurna project relies on several 3rd party and custom libraries. These libraries have to be loaded in you arduino environment before attempting to build the project. Some of these libraries are available through the library manager in Arduino IDE, others you will have to install them manually.

![Arduino IDE - Library options](images/arduino/arduino-libraries.jpg)

### Installing libraries from the Library Manager ###

Click on the "Manage Libraries" menu under "Sketch > Include Library". You will be presented a form with a search box on top. The first thing it will do is to connect to the Arduino servers to download the latest list of available libraries. Then you will have to search and install them. Please note that some libraries are optional and depend on the functionalities you want to include.

This is the list, in **bold** the text you have to search for:

|Library|Notes|
|-|-|
|**ArduinoJson** by Benoit Blanchon||
|**Embedis** by David Turnball and Tom Moxon||
|**NtpCLientLib** by German Martin||
|**PubSubClient** by Nick O'Leary|Since version 1.6.5. **Read note 1 below**|
|**DHT Sensor Library** by Adafruit|Only for DHT support|
|**Adafruit Unified Sensor** by Adafruit|Only for DHT support|
|**OneWire** by Paul Stoffregen (et al.)|Only for DS18B20 support|
|**DallasTemperature** by Miles Burton (et al.)|Only for DS18B20 support|


Note 1: The PubSubClient library requires a little modification in order to work with long MQTT message payloads (like when using Domoticz integration). You will need to edit the ```PubSubClient.h``` file (for me that file is under the "C:\Users\xose\Documents\Arduino\libraries\arduino_281549\src\PubSubClient.h" folder), line 26 and change the MQTT_MAX_PACKET_SIZE to at least 400.


```
// MQTT_MAX_PACKET_SIZE : Maximum packet size
#ifndef MQTT_MAX_PACKET_SIZE
#define MQTT_MAX_PACKET_SIZE 400
#endif

```


![Arduino IDE - Library options](images/arduino/arduino-library-manager.jpg)

### Installing libraries manually ###

You will have to install manually the libraries that are not available from the Library Manager. The Arduino IDE lets you install a library from a ZIP file, so we will download all the required libraries from their repositories in a ZIP file and install them. You can look for them manually but I have gathered the URLs to those ZIP files here for convenience:

|Library|Repository|ZIP|Notes|
|-|-|-|-|
|**Time** by Michael Maregolis and Paul Stoffregen (fork)|[GIT](https://github.com/xoseperez/Time)|[ZIP](https://github.com/xoseperez/Time/archive/master.zip)||
|**ESPAsyncTCP** by Hristo Gochkov|[GIT](https://github.com/me-no-dev/ESPAsyncTCP)|[ZIP](https://github.com/me-no-dev/ESPAsyncTCP/archive/master.zip)||
|**ESPAsyncUDP** by Hristo Gochkov|[GIT](https://github.com/me-no-dev/ESPAsyncUDP)|[ZIP](https://github.com/me-no-dev/ESPAsyncUDP/archive/master.zip)||
|**ESPAsyncWebServer** by Hristo Gochkov|[GIT](https://github.com/me-no-dev/ESPAsyncWebServer)|[ZIP](https://github.com/me-no-dev/ESPAsyncWebServer/archive/master.zip)||
|**AsyncMqttClient** by Marvin Roger|[GIT](https://github.com/marvinroger/async-mqtt-client)|[ZIP](https://github.com/marvinroger/async-mqtt-client/archive/master.zip)|Not needed if using PubSubClient|
|**DebounceEvent** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/debounceevent)|[ZIP](https://bitbucket.org/xoseperez/debounceevent/get/master.zip)||
|**JustWifi** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/justwifi)|[ZIP](https://bitbucket.org/xoseperez/justwifi/get/master.zip)||
|**FauxmoESP** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/fauxmoesp)|[ZIP](https://bitbucket.org/xoseperez/fauxmoesp/get/master.zip)||
|**HLW8012** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/hlw8012)|[ZIP](https://bitbucket.org/xoseperez/hlw8012/get/master.zip)|Only for Sonoff POW|
|**EmonLiteESP** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/emonliteesp)|[ZIP](https://bitbucket.org/xoseperez/emonliteesp/get/master.zip)|Only for current sensor support|
|**my9291** by Xose Pérez|[GIT](https://github.com/xoseperez/my9291)|[ZIP](https://github.com/xoseperez/my9291/archive/master.zip)|Only for AI Thinker Wifi Light|
|**RemoteSwitch** by Randy Simons (fork)|[GIT](https://github.com/xoseperez/RemoteSwitch-arduino-library)|[ZIP](https://github.com/xoseperez/RemoteSwitch-arduino-library/archive/master.zip)|Only for custom RF support|
|**NoFUSS** by Xose Pérez|[GIT](https://bitbucket.org/xoseperez/nofuss)|[ZIP](https://bitbucket.org/xoseperez/nofuss/get/master.zip)|Only for unattended OTA updates support|

Download the ZIP files from the links in the table above only for those libraries you actually need. If you are unsure start with the mandatory ones. Then use the menu under "Sketch > Include Library > Add .ZIP Library..." and load them one by one.

![Arduino IDE - Library options](images/arduino/arduino-libraries-zip.jpg)

Depending on your level of GIT confidence you can checkout the repositories for all of them into your library folder instead of installing them as ZIP files.

**Note: when updating the project to a newer version, come back here and update the libraries before reporting an issue in the issue tracker.**

## Open ESPurna in the IDE ##

Assuming you have already checked out the project from bitbucket using git, you just have to open the ```code/espurna/espurna.ino``` file. The rest of the files will open as tabs in the IDE. Unfortunately the IDE does not support opening files under subfolders, and that includes the configuration files you will have to modify in the next step.

## Configuring the hardware ##

The ESPurna firmware uses build flags to target specific boards or enable support for certain sensors. The Arduino IDE does not have a friendly way to specify build flags from the interface so the best option is to manually modify the '**code/espurna/config/arduino.h**' file to define what we want to build. Edit that file with your favourite editor (it's not accessible from the IDE, the pic below is from Atom) and uncomment the options to suit your need. In the example below we are compiling for Sonoff TH with DHT support.

![Arduino IDE - Hardware configuration from Atom](images/arduino/arduino-hardware.jpg)

Also, you might want to take a look at other compilation options and default values in '**code/espurna/config/general.h**'.

## Building & Flashing the firmware ##

First you will have to choose the right board and memory map. Here you have a list of the supported board types and the suggested memory layout to use:

|Board type|Board names|Flash size|Flash mode|
|-|-|-|-|
|ESP-12 based modules|Wemos D1 & D1 mini, NodeMCU, Electrodragon, OpenEnergyMonitor MQTT Relay Board,... |4M (3M SPIFFS)|DOUT|
|Generic ESP8285 module|Sonoff 4CH, Sonoff 4CH Pro, Sonoff Touch, Sonoff B1, Sonoff T1, AI-Thinker Wifi Light|1M (no SPIFFS)*|DOUT|
|Generic ESP8266 module|All the rest|1M (no SPIFFS)*|DOUT|

* If you don't see the "1M (no SPIFFS)" option check the "Add a new flash layout" section above. If you still don't see it or you don't want to modify those files you can safely use the "1M (64F SPIFFS)" option for the moment.

![Arduino IDE - Library options](images/arduino/arduino-board-options.jpg)

Now you are ready to build the project clicking on the 'tick' button. Take a close look at the output window in the IDE for errors (in red). Common errors here could be missing libraries (go back to the installing dependencies section above) or the "Unsupported hardware" error, meaning you have not defined the target device (go back to the configuring hardware section).

Finally, if there were no errors, connect your device (check the [Hardware](Hardware) document for instruction on how to connect your device to flash it), choose the port your programmer is listening to, and flash it clicking on the 'upload' button.