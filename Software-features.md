This page describes software features of ESPurna.

## Enabling features

You can enable or disable some of the features by using C preprocessor build flags (`-D`), during build time ie: `-DMQTT_SUPPORT=0` will not include MQTT support, as per below tables.  
Similar effect can be achieved by editing `code/espurna/config/custom.h` and adding `#define MQTT_SUPPORT=0`.

> Tables list all options that can be supplied during runtime. Some are not documented well - feel free to enhance this page.

# Table of contents

- [Overview of the feature groups](#overview-of-the-feature-groups)
- [System features](#system-features)
- [Debugging support](#debugging-support)
- [InfluxDB settings](#influxdb-settings)
- [InfraRed - IR](#infrared---ir)
- [MQTT settings](#mqtt-settings)
- [NoFUSS](#nofuss)
- [NTP](#ntp)
- [RF](#rf) 
- [Scheduler](#scheduler)
- [SSDP](#ssdp)
- [Telnet](#telnet)
- [Thingspeak](#thingspeak)
- [Serial to MQTT](#serial-to-mqtt)
- [Web](#web)

# Overview of the feature groups

For each functional group, ESPurna uses two flags: 
- `*_SUPPORT` - to compile code for that functionality. Feature code will be present in the image, but will not necessary be enabled by default. 
- `*_ENABLED` - to activate particular feature per default. In most (but not all) cases, functionality can be turned on and off in the WebUI or using Telnet commands. Changing this flag will set the default behavior of a new device, but will not override the saved configuration of old device. 

Many of the feature groups have special options, as highlighted in tables below.

Below is a list of all *_SUPPORT flags that ESPurna supports (sorted alphabetically):

| Feature | Build flag | Description |
| --- | --- | --- |
| Amazon Alexa | `ALEXA_SUPPORT` | Enable [Alexa](https://en.wikipedia.org/wiki/Amazon_Alexa) discovery and support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| Broker | `BROKER_SUPPORT` | | 
| Domoticz | `DOMOTICZ_SUPPORT` | Enable [Domoticz](http://domoticz.com)-specific layout of MQTT topics (default: same as `MQTT_SUPPORT`) |
| Home Assistant | `HOMEASSISTANT_SUPPORT` | Enable [Home Assistant](https://home-assistant.io)-specific support (default: same as `MQTT_SUPPORT`) |
| InfluxDB | `INFLUXDB_SUPPORT` | Enable [InfluxDB](https://en.wikipedia.org/wiki/InfluxDB) HTTP interface (default: `0` - off) <Br> Uses ESPAsyncTCP library (see below) |
| IR Rx/Tx | `IR_SUPPORT` | Enable [IR Receiver](https://en.wikipedia.org/wiki/Consumer_IR) support (default: `0` - off) |
| LLMNR | `LLMNR_SUPPORT` | Support for [Link-Local Multicast Name Resolution](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution) (default: `0` - off) |
| mDNS discovery | `MDNS_CLIENT_SUPPORT` | Use [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS) to discover endpoints (like MQTT or InfluxDB) (default: `0` - off) |
| mDNS announcements | `MDNS_SERVER_SUPPORT` | Announce device via [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS) (default: `1` - on) |
| MQTT | `MQTT_SUPPORT` | Enable [MQTT](https://en.wikipedia.org/wiki/MQTT) client (default: `1` - on) |
| NetBIOS | `NETBIOS_SUPPORT` | [NetBIOS](https://en.wikipedia.org/wiki/NetBIOS) (default: `0` - off) |
| Nofuss | `NOFUSS_SUPPORT` | | 
| NTP | `NTP_SUPPORT` | |
| Raw RF | `RF_RAW_SUPPORT` | Raw [433Mhz RF](https://en.wikipedia.org/wiki/LPD433) (default: `0` - off) |
| RF | `RF_SUPPORT` | [433Mhz RF](https://en.wikipedia.org/wiki/LPD433) (default: `0` - off) |
| Scheduler | `SCHEDULER_SUPPORT` | |
| SPIFFS | `SPIFFS_SUPPORT` || 
| SSDP | `SSDP_SUPPORT` | [Simple Service Discovery protocol](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol) (default: `0` - off) |
| Telnet | `TELNET_SUPPORT` | Enable [Telnet](https://en.wikipedia.org/wiki/Telnet) support (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| | `TERMINAL_SUPPORT` | (default: `1` - on) |
| Thingspeak | `THINGSPEAK_SUPPORT` | [ThingSpeak](https://en.wikipedia.org/wiki/ThingSpeak) (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |
| Serial to MQTT support | `UART_MQTT_SUPPORT` | |
| Web | `WEB_SUPPORT` | [Web](https://en.wikipedia.org/wiki/Web) (default: `1` - on) <Br> Uses ESPAsyncTCP library (see below) |

## System features

| Feature | Build flag | Description |
| --- | --- | --- |
| Auto-saving of settings | `SETTINGS_AUTOSAVE` | Automatically save any changed settings? (default: `1` - on) |
| | `SYSTEM_CHECK_ENABLED` | (default: `1` - on) |
| | `HEARTBEAT_ENABLED` | (default: `1` - on) |
| | `LIGHT_SAVE_ENABLED` | (default: `1` - on) |

## Debugging

| Feature | Build flag | Description |
| --- | --- | --- |
| Debug over serial | `DEBUG_SERIAL_SUPPORT` | Enable debug mode on serial interface (default: `1` - on) |
| | `DEBUG_PORT` | (default: `Serial`) |
| Serial port speed | `SERIAL_BAUDRATE` | (default: `115200`) |
| Add timestamp to debug messages?| `DEBUG_ADD_TIMESTAMP` | (default: `1` - on) |
| | `SERIAL_RX_BAUDRATE` | (default: `115200` |
| Debug over UDP (Syslog)| `DEBUG_UDP_SUPPORT` | Enable debugging mode over UDP (default: `0` - off) |
| Debug over Telnet | `DEBUG_TELNET_SUPPORT` | Use Telnet output for debugging (default: same as `TELNET_SUPPORT`) |

## InfluxDB settings 

| Feature | Build flag | Description |
| --- | --- | --- |
|| `INFLUXDB_DATABASE` ||
|| `INFLUXDB_HOST` ||
|| `INFLUXDB_PASSWORD` ||
|| `INFLUXDB_PORT` ||
|| `INFLUXDB_USERNAME` ||

## Infrared - IR

| Feature | Build flag | Description |
| --- | --- | --- |
| IR Transmitter GPIO | `IR_PIN` | GPIO where IR transmitter is connected (default: `4`) |
| | `IR_BUTTON_SET` | Which of the predefined IR button sets to use. One of: <br> - `1` - Original MagicLed controller (default) <br>  - `2` - Alternative controller shipped with another variant of MagicLed controllers  |

## MQTT settings

| Feature | Build flag | Description |
| --- | --- | --- |
|| `MQTT_AUTOCONNECT` ||
|| `MQTT_ENQUEUE_DATETIME` ||
|| `MQTT_ENQUEUE_HOSTNAME` ||
|| `MQTT_ENQUEUE_IP` ||
|| `MQTT_ENQUEUE_MAC` ||
|| `MQTT_ENQUEUE_MESSAGE_ID` ||
| MQTT get root | `MQTT_GETTER` | Subtopic for getting a value from an object (default: `""`) |
|| `MQTT_KEEPALIVE` ||
|| `MQTT_PASS` ||
|| `MQTT_PORT` ||
|| `MQTT_QOS` ||
|| `MQTT_QUEUE_MAX_SIZE` ||
|| `MQTT_RECONNECT_DELAY_MAX` ||
|| `MQTT_RECONNECT_DELAY_MIN` ||
|| `MQTT_RECONNECT_DELAY_STEP` ||
|| `MQTT_RETAIN` ||
|| `MQTT_SERVER` ||
| MQTT set root | `MQTT_SETTER` | Subtopic for setting a value to an object (default: `"/set"`) |
|| `MQTT_SKIP_RETAINED` ||
|| `MQTT_SKIP_TIME` ||
|| `MQTT_SSL_ENABLED` ||
|| `MQTT_SSL_FINGERPRINT` ||
|| `MQTT_TOPIC` ||
|| `MQTT_USER` ||
| TCP Library | `MQTT_USE_ASYNC` | Which TCP library to use. One of: <br> - `0` - PubSubClient (will break other things) <Br> - `1` - ESPAsyncTCP (default)  |
|| `MQTT_USE_JSON` ||
|| `MQTT_USE_JSON_DELAY` ||

## NoFUSS

| Feature | Build flag | Description |
| --- | --- | --- |
|| `NOFUSS_INTERVAL` ||
|| `NOFUSS_SERVER` ||

## NTP

| Feature | Build flag | Description |
| --- | --- | --- |
|| `NTP_DAY_LIGHT` ||
|| `NTP_DST_REGION` ||
|| `NTP_SERVER` ||
|| `NTP_START_DELAY` ||
|| `NTP_SYNC_INTERVAL` ||
|| `NTP_TIMEOUT` ||
|| `NTP_TIME_OFFSET` ||
|| `NTP_UPDATE_INTERVAL` ||

## RF

| Feature | Build flag | Description |
| --- | --- | --- |
| 433Mhz RF Transmitter GPIO | `RF_PIN` | GPIO where RF transmitter is connected (default: `14`) |
|| `RF_RAW_SUPPORT` ||
|| `RF_RECEIVE_DELAY` ||
|| `RF_SEND_DELAY` ||
|| `RF_SEND_TIMES` ||

## Scheduler 

| Feature | Build flag | Description |
| --- | --- | --- |
|| `SCHEDULER_MAX_SCHEDULES` ||

## SSDP 

| Feature | Build flag | Description |
| --- | --- | --- |
| [SSDP](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol) device class | `SSDP_DEVICE_TYPE` | (default: `"upnp:rootdevice"`) |

## Telnet

| Feature | Build flag | Description |
| --- | --- | --- |
|| `TELNET_STA` ||

## Thingspeak

| Feature | Build flag | Description |
| --- | --- | --- |
|| `THINGSPEAK_APIKEY` ||

## Serial to MQTT 

| Feature | Build flag | Description |
| --- | --- | --- |
|| `UART_MQTT_BAUDRATE` ||
|| `UART_MQTT_HW_PORT` ||
|| `UART_MQTT_RX_PIN` ||
|| `UART_MQTT_SUPPORT` ||
|| `UART_MQTT_TX_PIN` ||
|| `UART_MQTT_USE_SOFT` ||

## Web 

| Feature | Build flag | Description |
| --- | --- | --- |
|| `WEB_EMBEDDED` ||
|| `WEB_FORCE_PASS_CHANGE` ||
|| `WEB_PORT` ||
|| `WEB_SSL_ENABLED` ||
|| `WEB_USERNAME` ||


# Button configuration

| Feature | Build flag | Description |
| --- | --- | --- |
| Debounce delay | `BUTTON_DEBOUNCE_DELAY` | (default: `50`) |
| Double-click delay | `BUTTON_DBLCLICK_DELAY` | (default: `500`) |
| Long-click delay | `BUTTON_LNGCLICK_DELAY` | (default: `1000`) |
| Loooooong-click delay | `BUTTON_LNGLNGCLICK_DELAY` | (default: `10000`) |


