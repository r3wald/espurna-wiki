This page describes software features of ESPurna.
You can enable or disable some of the features by using C preprocessor build flags (`-D`), ie: `-DMQTT_SUPPORT=0` will disable MQTT, as per below tables.

Tables list all options that can be supplied during runtime. Some are not documented well - feel free to enhance this page.

# Interfaces

| Feature | Build flag | Description | 
| --- | --- | --- |
| MQTT | `MQTT_SUPPORT` | Enable MQTT client (default: `1` - on) |
| InfluxDB | `INFLUXDB_SUPPORT` | Enable InfluxDB HTTP interface (default: `0` - off) <Br> Uses ESPAsyncTCP library (see below) |
| | `THINGSPEAK_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| Alexa | `ALEXA_SUPPORT` | Enable Alexa discovery and support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| IR Rx/Tx | `IR_SUPPORT` | Enable IR Receiver / Transmitter support (default: `0` - off) |
| 433Mhz RF | `RF_SUPPORT` | (default: `0` - off) |
| Telnet | `TELNET_SUPPORT` | Enable telnet support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `TELNET_STA` | Should telnet be enabled in STA mode (default: `0` - off ) |
|  | `TERMINAL_SUPPORT` | (default: `1` - on) |
| | `WEB_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) | 
| | `WEB_EMBEDDED` | (default: `1` - on) |
| mDNS announcements | `MDNS_SERVER_SUPPORT` | Announce device via mDNS (default: `1` - on) |
| mDNS discovery | `MDNS_CLIENT_SUPPORT` | Use mDNS to discover endpoints (like MQTT or InfluxDB) (default: `0` - off) |
| LLMNR | `LLMNR_SUPPORT` | (default: `0` - off) |
| NetBIOS | `NETBIOS_SUPPORT` | (default: `0` - off) |
| SSDP | `SSDP_SUPPORT` | (default: `0` - off) |
| SSDP device class | `SSDP_DEVICE_TYPE` | (default: `"upnp:rootdevice"`) |


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
| Domoticz | `DOMOTICZ_SUPPORT` | Enable Domoticz-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| Home Assistant | `HOMEASSISTANT_SUPPORT` | Enable Home-Assistant-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| TCP Library | `MQTT_USE_ASYNC` | Which TCP library to use. One of: <br> - `0` - PubSubClient (will break other things) <Br> - `1` - ESPAsyncTCP (default)  |
| MQTT get root | `MQTT_GETTER` | Subtopic for getting a value from an object (default: `""`) |
| MQTT set root | `MQTT_SETTER` | Subtopic for setting a value to an object (default: `"/set"`) |
| | `BROKER_SUPPORT` | (default: `1`) |

# IR / RF support

| Feature | Build flag | Description | 
| --- | --- | --- |
| IR Transmitter GPIO | `IR_PIN` | GPIO where IR transmitter is connected (default: `4`) |
| | `IR_BUTTON_SET` | Which of the predefined IR button sets to use. One of: <br> - `1` - Original MagicLed controller (default) <br>  - `2` - Alternative controller shipped with another variant of MagicLed controllers  |
| 433Mhz RF Transmitter GPIO | `RF_PIN` | GPIO where RF transmitter is connected (default: `14`) |


# Debugging 

| Feature | Build flag | Description | 
| --- | --- | --- |
| Debug serial | DEBUG_SERIAL_SUPPORT | Enable debug mode on serial interface (default: `1` - on)  |
| | `DEBUG_PORT` | (default: `Serial`) | 
| | `SERIAL_BAUDRATE` | (default: `115200` |
| | `DEBUG_ADD_TIMESTAMP` | (default: `1` - on) |
| | `SERIAL_RX_BAUDRATE` | (default: `115200` |
| | `DEBUG_UDP_SUPPORT` | (default: `0` - off) |
| | `DEBUG_TELNET_SUPPORT` | (default: TELNET_SUPPORT) | 

# System 

| Feature | Build flag | Description | 
| --- | --- | --- |
| | `SETTINGS_AUTOSAVE` | (default: `1`) |
| | `SCHEDULER_SUPPORT` | (default: `1`) |
| | `NTP_SUPPORT` | (default: `1`) |
| | `SYSTEM_CHECK_ENABLED` | (default: `1` - on) | 
| | `HEARTBEAT_ENABLED` | (default: `1` - on) | 
| | `SPIFFS_SUPPORT` | (default: `0`) |
| | `NOFUSS_SUPPORT` | (default: `0`) |
| | `LIGHT_SAVE_ENABLED` | (default: `1`) |


