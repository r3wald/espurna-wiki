This page describes software features of ESPurna.
You can enable or disable some of the features by using C preprocessor build flags (`-D`), ie: `-DMQTT_SUPPORT=0` will disable MQTT, as per below tables.

Tables list all options that can be supplied during runtime. Some are not documented well - feel free to enhance this page.

# Interfaces

| Feature | Build flag | Description | 
| --- | --- | --- |
| | `MQTT_SUPPORT` | Enable MQTT client (default: `1` - on) |
| | `INFLUXDB_SUPPORT` | Enable (default: `0` - off) <Br> Uses ESPAsyncTCP library (see below) |
| | `THINGSPEAK_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `ALEXA_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `IR_SUPPORT` | (default: `0` - on) |
| | `RF_SUPPORT` | (default: `0` -on) |
| Telnet | `TELNET_SUPPORT` | Enable telnet support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `TELNET_STA` | Should telnet be enabled in STA mode (default: `0` - off ) |
| | `TERMINAL_SUPPORT` | (default: `1` - on) |
| | `WEB_SUPPORT` | (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) | 
| | `WEB_EMBEDDED` | (default: `1` - on) |
| | `MDNS_SERVER_SUPPORT` | (default: `1` - on) |
| | `MDNS_CLIENT_SUPPORT` | (default: `0` - off) |
| | `LLMNR_SUPPORT` | (default: `0` - off) |
| | `NETBIOS_SUPPORT` | (default: `0` - off) |
| | `SSDP_SUPPORT` | (default: `0` - off) |
| | `SSDP_DEVICE_TYPE` | (default: `"upnp:rootdevice"`) |


# Button configuration

| Feature | Build flag | Description | 
| --- | --- | --- |
| | `BUTTON_DEBOUNCE_DELAY` | (default: `50`) | 
| | `BUTTON_DBLCLICK_DELAY` | (default: `500`) | 
| | `BUTTON_LNGCLICK_DELAY` | (default: `1000`) | 
| | `BUTTON_LNGLNGCLICK_DELAY` | (default: `10000`) | 

# MQTT settings

| Feature | Build flag | Description | 
| --- | --- | --- |
| | `DOMOTICZ_SUPPORT` | Enable Domoticz-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| | `HOMEASSISTANT_SUPPORT` | Enable Home-Assistant-specific layout of MQTT topics (default: `MQTT_SUPPORT`) |
| | `MQTT_USE_ASYNC` | Which TCP library to use. One of: <br> - `0` - PubSubClient (will break other things) <Br> - `1` - ESPAsyncTCP (default)  |
| | `MQTT_GETTER` | Subtopic for getting a value from an object (default: `""`) |
| | `MQTT_SETTER` | Subtopic for setting a value to an object (default: `"/set"`) |
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


