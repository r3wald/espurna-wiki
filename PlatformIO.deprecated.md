# Build & Flash the Firmware with PlatformIO

## Build the firmware

The project is ready to be build using [PlatformIO][1].
Please refer to their web page for instructions on how to install the builder.

If you are using PlatformIO /strongly recommended) it will take care of the library dependencies. Otherwise you will have to install them manually:

* Benoit Blanchon's [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
* Hristo Gochkov's [ESPAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP)
* Hristo Gochkov's [ESPAsyncUDP](https://github.com/me-no-dev/ESPAsyncUDP)
* Hristo Gochkov's [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
* Marvin Roger's [AyncMqttClient](https://github.com/marvinroger/async-mqtt-client) (1)
* Nick O'Leary's [PubSubClient](https://github.com/knolleary/pubsubclient) (1)
* Adafruit's [DHT Sensor Library](https://github.com/adafruit/DHT-sensor-library) (required if compiling with DHT support: -DENABLE_DHT)
* Adafruit's [Unified Sensor Library](https://github.com/adafruit/Adafruit_Sensor) (required if compiling with DHT support: -DENABLE_DHT)
* Paul Stoffregen (et al.) [OneWire](https://github.com/PaulStoffregen/OneWire)
* Miles Burton (et al.) [DallasTemperature](https://github.com/milesburton/Arduino-Temperature-Control-Library)
* The PatternAgents (et al.) [Embedis](https://github.com/thingSoC/embedis)
* German Martin's [NtpCLientLib](https://github.com/gmag11/NtpClient)
* Michael Maregolis & Paul Stoffregen's [Time](https://github.com/PaulStoffregen/Time)
* Randy Simons' [RemoteSwitch](https://github.com/jccprj/RemoteSwitch-arduino-library) (required if using custom RF module: -DENABLE_RF)

1) Only one of these two libraries is required, either PubSubClient (synchronous) or AsyncMQTTClient (asynchronous). The one that will be used depends on the MQTT_USE_ASYNC setting in ```code/espurna/config/general.h```

And my own libraries:

* [JustWifi](https://bitbucket.org/xoseperez/justwifi.git)
* [DebounceEvent](https://bitbucket.org/xoseperez/debounceevent.git)
* [FauxmoESP](https://bitbucket.org/xoseperez/fauxmoesp.git) (required if compiling with WeMo emulation support: -DENABLE_FAUXMO)
* [HLW8012](https://bitbucket.org/xoseperez/hlw8012.git) (required if compiling for Sonoff POW: -DENABLE_POW)
* [EmonLiteESP](https://bitbucket.org/xoseperez/emonliteesp.git) (required if compiling with Energy Monitoring support: -DENABLE_EMON)
* [my9291](https://github.com/xoseperez/my9291) (required if compiling for AI-Thinker Wifi Light: -DAI_THINKER)
* [NoFUSS](https://bitbucket.org/xoseperez/nofuss.git) (required if compiling with NoFUSS Automatic OTA support: -DENABLE_NOFUSS)

These libraries are automatically installed once you first try to build the project. But if you are updating to a newer version it's always a good idea to **manually force them to update**:

```bash
> pio lib update
```

Once you have all the code, you can check if it's working by:

```bash
> pio run -e node-debug
```

If it compiles you are ready to flash the firmware.

## Flash your board

Wire your board (check the [Hardware page](Hardware.md)) and flash the firmware (with ```upload```):

```bash
> pio run -t upload -e sonoff
```

(or any other environment, depending on the board you are working with).

Library dependencies are automatically managed via PlatformIO Library Manager or included via submodules and linked from the "lib" folder.

Once the firmware is uploaded next step is to upload the web interface. Check how to [build and flash the filesystem](Filesystem.md).

[1]: http://www.platformio.org