This page describes software features of ESPurna.
You can enable or disable some of the features by using C preprocessor build flags (`-D`), ie: `-DMQTT_SUPPORT=0` will disable MQTT, as per below tables.

Tables list all options that can be supplied during runtime. Some are not documented well - feel free to enhance this page.

# Interfaces

| Feature | Build flag | Description |
| --- | --- | --- |
| [MQTT](https://en.wikipedia.org/wiki/MQTT) | `MQTT_SUPPORT` | Enable MQTT client (default: `1` - on) |
| [InfluxDB](https://en.wikipedia.org/wiki/InfluxDB) | `INFLUXDB_SUPPORT` | Enable InfluxDB HTTP interface (default: `0` - off) <Br> Uses ESPAsyncTCP library (see below) |
| [ThingSpeak](https://en.wikipedia.org/wiki/ThingSpeak) | `THINGSPEAK_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| [Alexa](https://en.wikipedia.org/wiki/Amazon_Alexa) | `ALEXA_SUPPORT` | Enable Alexa discovery and support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| [IR Rx/Tx](https://en.wikipedia.org/wiki/Consumer_IR) | `IR_SUPPORT` | Enable IR Receiver / Transmitter support (default: `0` - off) |
| [433Mhz RF](https://en.wikipedia.org/wiki/LPD433) | `RF_SUPPORT` | (default: `0` - off) |
| [Telnet](https://en.wikipedia.org/wiki/Telnet) | `TELNET_SUPPORT` | Enable telnet support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `TELNET_STA` | Should telnet be enabled in STA mode (default: `0` - off ) |
| | `TERMINAL_SUPPORT` | (default: `1` - on) |
| [Web](https://en.wikipedia.org/wiki/Web) | `WEB_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `WEB_EMBEDDED` | (default: `1` - on) |
| [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS) announcements | `MDNS_SERVER_SUPPORT` | Announce device via mDNS (default: `1` - on) |
| [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS) discovery | `MDNS_CLIENT_SUPPORT` | Use mDNS to discover endpoints (like MQTT or InfluxDB) (default: `0` - off) |
| [LLMNR](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution) | `LLMNR_SUPPORT` | (default: `0` - off) |
| [NetBIOS](https://en.wikipedia.org/wiki/NetBIOS) | `NETBIOS_SUPPORT` | (default: `0` - off) |
| [SSDP](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol) | `SSDP_SUPPORT` | (default: `0` - off) |
| [SSDP](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol) device class | `SSDP_DEVICE_TYPE` | (default: `"upnp:rootdevice"`) |

# Button configuration

| Feature | Build flag | Description |
| --- | --- | --- |
| Debounce delay | `BUTTON_DEBOUNCE_DELAY` | (default: `50`) |
| Double-click delay | `BUTTON_DBLCLICK_DELAY` | (default: `500`) |
| Long-click delay | `BUTTON_LNGCLICK_DELAY` | (default: `1000`) |
| Loooooong-click delay | `BUTTON_LNGLNGCLICK_DELAY` | (default: `10000`) |

# MQTT settings

| Feature | Build flag | Description |
| --- | --- | --- |
| [Domoticz](http://domoticz.com) | `DOMOTICZ_SUPPORT` | Enable Domoticz-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| [Home Assistant](https://home-assistant.io) | `HOMEASSISTANT_SUPPORT` | Enable Home-Assistant-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| TCP Library | `MQTT_USE_ASYNC` | Which TCP library to use. One of: <br> - `0` - PubSubClient (will break other things) <Br> - `1` - ESPAsyncTCP (default)  |
| MQTT get root | `MQTT_GETTER` | Subtopic for getting a value from an object (default: `""`) |
| MQTT set root | `MQTT_SETTER` | Subtopic for setting a value to an object (default: `"/set"`) |
| | `BROKER_SUPPORT` | (default: `1` - on) |

# IR / RF support

| Feature | Build flag | Description |
| --- | --- | --- |
| IR Transmitter GPIO | `IR_PIN` | GPIO where IR transmitter is connected (default: `4`) |
| | `IR_BUTTON_SET` | Which of the predefined IR button sets to use. One of: <br> - `1` - Original MagicLed controller (default) <br>  - `2` - Alternative controller shipped with another variant of MagicLed controllers  |
| 433Mhz RF Transmitter GPIO | `RF_PIN` | GPIO where RF transmitter is connected (default: `14`) |

# Debugging

| Feature | Build flag | Description |
| --- | --- | --- |
| Debug serial | `DEBUG_SERIAL_SUPPORT` | Enable debug mode on serial interface (default: `1` - on) |
| | `DEBUG_PORT` | (default: `Serial`) |
| | `SERIAL_BAUDRATE` | (default: `115200`) |
| | `DEBUG_ADD_TIMESTAMP` | (default: `1` - on) |
| | `SERIAL_RX_BAUDRATE` | (default: `115200` |
| | `DEBUG_UDP_SUPPORT` | (default: `0` - off) |
| | `DEBUG_TELNET_SUPPORT` | (default: TELNET_SUPPORT) |

# System

| Feature | Build flag | Description |
| --- | --- | --- |
| | `SETTINGS_AUTOSAVE` | (default: `1` - on) |
| | `SCHEDULER_SUPPORT` | (default: `1` - on) |
| | `NTP_SUPPORT` | (default: `1` - on) |
| | `SYSTEM_CHECK_ENABLED` | (default: `1` - on) |
| | `HEARTBEAT_ENABLED` | (default: `1` - on) |
| | `SPIFFS_SUPPORT` | (default: `0` - off) |
| | `NOFUSS_SUPPORT` | (default: `0` - off) |
| | `LIGHT_SAVE_ENABLED` | (default: `1` - on) |
