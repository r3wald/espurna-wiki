# Build & Flash the Firmware with PlatformIO

## Installing PlatformIO

You can check the [getting started](http://platformio.org/get-started) page in the PlatformIO site to know how to setup the environment for your platform. There are also some videos on YouTube about it. 

## Installing dependencies & building the firmware

PlatformIO will take care of the library dependencies. The first time you run the build process it will fetch and install all the libraries required by ESPurna in the specified versions.

* Benoit Blanchon's [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
* Hristo Gochkov's [ESPAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP)
* Hristo Gochkov's [ESPAsyncUDP](https://github.com/me-no-dev/ESPAsyncUDP)
* Hristo Gochkov's [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
* Marvin Roger's [AsyncMqttClient](https://github.com/marvinroger/async-mqtt-client) (1)
* Nick O'Leary's [PubSubClient](https://github.com/knolleary/pubsubclient) (1)
* Adafruit's [DHT Sensor Library](https://github.com/adafruit/DHT-sensor-library) (required if compiling with DHT support: -DDHT_SUPPORT)
* Adafruit's [Unified Sensor Library](https://github.com/adafruit/Adafruit_Sensor) (required if compiling with DHT support: -DDHT_SUPPORT)
* Paul Stoffregen (et al.) [OneWire](https://github.com/PaulStoffregen/OneWire)
* Miles Burton (et al.) [DallasTemperature](https://github.com/milesburton/Arduino-Temperature-Control-Library)
* The PatternAgents (et al.) [Embedis](https://github.com/thingSoC/embedis)
* German Martin's [NtpCLientLib](https://github.com/gmag11/NtpClient)
* Michael Maregolis & Paul Stoffregen's [Time](https://github.com/PaulStoffregen/Time)
* Randy Simons' [RemoteSwitch](https://github.com/jccprj/RemoteSwitch-arduino-library) (required if using custom RF module: -DRF_SUPPORT)

And my own libraries:

* [JustWifi](https://bitbucket.org/xoseperez/justwifi.git)
* [DebounceEvent](https://bitbucket.org/xoseperez/debounceevent.git)
* [FauxmoESP](https://bitbucket.org/xoseperez/fauxmoesp.git) (required if compiling with WeMo emulation support: -DALEXA_SUPPORT)
* [HLW8012](https://bitbucket.org/xoseperez/hlw8012.git) (required if compiling for Sonoff POW: -DHLW8012_SUPPORT)
* [EmonLiteESP](https://bitbucket.org/xoseperez/emonliteesp.git) (required if compiling with Energy Monitoring support: -DEMON_SUPPORT)
* [my9291](https://github.com/xoseperez/my9291) (required if compiling for AI-Thinker Wifi Light: -DAI_THINKER)
* [NoFUSS](https://bitbucket.org/xoseperez/nofuss.git) (required if compiling with NoFUSS Automatic OTA support: -DNOFUSS_SUPPORT)

These libraries are automatically installed once you first try to build the project. But if you are updating to a newer version it's always a good idea to **manually force them to update**:

```bash
> pio lib update
```
Once you have all the code, you can check if it's working by:

```bash
> pio run -e itead-sonoff-basic
```

If it compiles you are ready to flash the firmware.

## Flash your board

Wire your board (check the [Hardware page](Hardware.md)) and flash the firmware (with ```upload```):

```bash
> pio run -t upload -e itead-sonoff-basic
```

(or any other environment, depending on the board you are working with).