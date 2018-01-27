# Build & Flash the Firmware with PlatformIO

## Installing PlatformIO

You can check the [getting started](http://platformio.org/get-started) page in the PlatformIO site to know how to setup the environment for your platform. There are also some videos on YouTube about it. 

## Installing dependencies & building the firmware

PlatformIO will take care of the library dependencies. The first time you run the build process it will fetch and install all the libraries required by ESPurna in the specified versions.

* Benoit Blanchon's [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
* Marvin Roger's [AsyncMqttClient](https://github.com/marvinroger/async-mqtt-client) (1)
* Pascal Kurtansky's [Brzo I2C](https://github.com/pasko-zh/brzo_i2c) (2)
* The PatternAgents (et al.) [Embedis](https://github.com/thingSoC/embedis)
* Oscar Rovira's fork of Peter Lerup [ESPSoftwareSerial](https://github.com/krosk93/espsoftwareserial)
* Hristo Gochkov's [ESPAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP)
* Hristo Gochkov's [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
* Mark Szabo (et al.) [IrRemoteES8266](https://github.com/markszabo/IRremoteESP8266)
* Myles Eftos's [mDNSresolver](https://github.com/madpilot/mDNSResolver)
* German Martin's [NtpCLientLib](https://github.com/gmag11/NtpClient)
* Paul Stoffregen (et al.) [OneWire](https://github.com/PaulStoffregen/OneWire)
* Mariusz Kacki's [PMS](https://github.com/fu-hsi/PMS)
* Nick O'Leary's [PubSubClient](https://github.com/knolleary/pubsubclient) (1)
* Randy Simons' [RemoteSwitch](https://github.com/jccprj/RemoteSwitch-arduino-library) (required if using custom RF module: -DRF_SUPPORT)
* My fork of Michael Maregolis & Paul Stoffregen's [Time](https://github.com/xoseperez/Time)

And my own libraries:

* [DebounceEvent](https://bitbucket.org/xoseperez/debounceevent.git)
* [FauxmoESP](https://bitbucket.org/xoseperez/fauxmoesp.git) (required if compiling with WeMo emulation support: -DALEXA_SUPPORT)
* [HLW8012](https://bitbucket.org/xoseperez/hlw8012.git) (required if compiling for Sonoff POW: -DHLW8012_SUPPORT)
* [JustWifi](https://bitbucket.org/xoseperez/justwifi.git)
* [my92xx](https://github.com/xoseperez/my92xx) (required if compiling for AI-Thinker Wifi Light: -DAI_THINKER)
* [NoFUSS](https://bitbucket.org/xoseperez/nofuss.git) (required if compiling with NoFUSS Automatic OTA support: -DNOFUSS_SUPPORT)

(1): The firmware will be compiled either with AsyncMqttClient or PubSubClient, depending on the MQTT_USE_ASYNC setting.
(2): The firmware will be compiled either with Wire or Brzo I2C, depending on the I2C_USE_BRZO setting.

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

Wire your board (check the [Hardware page](Hardware)) and flash the firmware (with ```upload```):

```bash
> pio run -t upload -e itead-sonoff-basic
```

(or any other environment, depending on the board you are working with).