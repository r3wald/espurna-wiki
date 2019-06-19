# Build & Flash the Firmware with PlatformIO

## Installing PlatformIO

You can check the [getting started](http://platformio.org/get-started) page in the PlatformIO site to know how to setup the environment for your platform. There are also some videos on YouTube about it. 

## Installing dependencies & building the firmware

PlatformIO will take care of the library dependencies. The first time you run the build process it will fetch and install all the libraries required by ESPurna in the specified versions.

* Benoit Blanchon's [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
* Marvin Roger's [AsyncMqttClient](https://github.com/marvinroger/async-mqtt-client) <sup> [[1]](#footnote1)</sup>
* Pascal Kurtansky's [Brzo I2C](https://github.com/pasko-zh/brzo_i2c) <sup> [[2]](#footnote2)</sup>
* The PatternAgents (et al.) [Embedis](https://github.com/thingSoC/embedis)
* Oscar Rovira's fork of Peter Lerup [ESPSoftwareSerial](https://github.com/krosk93/espsoftwareserial) <sup> [[3]](#footnote3)</sup>
* Hristo Gochkov's [ESPAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP)
* Hristo Gochkov's [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
* Mark Szabo (et al.) [IrRemoteES8266](https://github.com/markszabo/IRremoteESP8266) <sup> [[4]](#footnote4)</sup>
* Myles Eftos's [mDNSresolver](https://github.com/madpilot/mDNSResolver) <sup> [[5]](#footnote5)</sup>
* German Martin's [NtpCLientLib](https://github.com/gmag11/NtpClient)
* Paul Stoffregen (et al.) [OneWire](https://github.com/PaulStoffregen/OneWire) <sup> [[6]](#footnote6)</sup>
* Mariusz Kacki's [PMS](https://github.com/fu-hsi/PMS) <sup> [[7]](#footnote7)</sup>
* Nick O'Leary's [PubSubClient](https://github.com/knolleary/pubsubclient) <sup> [[1]](#footnote1)</sup>
* Randy Simons' [RemoteSwitch](https://github.com/jccprj/RemoteSwitch-arduino-library) <sup> [[8]](#footnote8)</sup>
* My fork of Michael Maregolis & Paul Stoffregen's [Time](https://github.com/xoseperez/Time)

And my own libraries:

* [DebounceEvent](https://bitbucket.org/xoseperez/debounceevent.git)
* [FauxmoESP](https://bitbucket.org/xoseperez/fauxmoesp.git) <sup> [[9]](#footnote9)</sup>
* [HLW8012](https://bitbucket.org/xoseperez/hlw8012.git) <sup> [[10]](#footnote10)</sup>
* [JustWifi](https://bitbucket.org/xoseperez/justwifi.git)
* [my92xx](https://github.com/xoseperez/my92xx) <sup> [[11]](#footnote11)</sup>
* [NoFUSS](https://bitbucket.org/xoseperez/nofuss.git) <sup> [[12]](#footnote12)</sup>

Notes in the list above: 

<a name="footnote1"><sup>1</sup></a> The firmware will be compiled either with AsyncMqttClient or PubSubClient, depending on the MQTT_USE_ASYNC setting. Default to use AsyncMqttClient.  
<a name="footnote2"><sup>2</sup></a> The firmware will be compiled either with Wire or Brzo I2C, depending on the I2C_USE_BRZO setting. Defaults to use the standard Wire library.  
<a name="footnote3"><sup>3</sup></a> Required when either MHZ19_SUPPORT, PMSX003_SUPPORT or V9261F_SUPPORT are set to 1 (sensor).  
<a name="footnote4"><sup>4</sup></a> Required for some LED controller with IR receivers.   
<a name="footnote5"><sup>5</sup></a> Required when MDNS_CLIENT_SUPPORT is set to 1.  
<a name="footnote6"><sup>6</sup></a> Required when DALLAS_SUPPORT is set to 1 (sensor).  
<a name="footnote7"><sup>7</sup></a> Required when PMSX003_SUPPORT is set to 1 (sensor).  
<a name="footnote8"><sup>8</sup></a> Required when RF_SUPPORT is set to 1.  
<a name="footnote9"><sup>9</sup></a> Required when ALEXA_SUPPORT is set to 1. This is the default value.  
<a name="footnote10"><sup>10</sup></a> Required when HLW8012_SUPPORT is set to 1 (sensor).  
<a name="footnote11"><sup>11</sup></a> Required when using LIGHT_PROVIDER_MY92XX.  
<a name="footnote12"><sup>12</sup></a> Required when NOFUSS_SUPPORT is set to 1.  

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

## Customize build settings
If you want to modify the stock configuration but you don't want to touch the repo files you can define USE_CUSTOM_H in your build settings.

Modify your environment build_flags or just define global PLATFORMIO_BUILD_FLAGS
```
export PLATFORMIO_BUILD_FLAGS="-DUSE_CUSTOM_H"
```

Check https://github.com/xoseperez/espurna/issues/104 for an example on how to use this file.