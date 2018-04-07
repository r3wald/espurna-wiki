The ESPurna firmware outputs debug information to the terminal interface (except for the Sonoff Dual and the Sonoff RF Bridge). You only have to connect your USB2UART board to the TX, RX and GND pins in your board and open a terminal at **115200 baud** (8,N,1).

As an alternative you can use all commands also with Telnet, if you activated Telnet on the administration page of the web interface.

But the terminal not only shows information about what the device is doing, it also accepts several commands thanks to the Embedis library. You can get a list of these commands typing ```help``` and enter. It's recommended to enable echo to see what you are typing. Backspace or delete won't work in the terminal.

Available commands as of 1.12.5b (the actual list of available commands will depend on the built-in functionalities of your specific image):

| command | description |  
| --- | --- |
|**brightness** &lt;value&gt;|Sets RGB brightness (only for lights)|
|**channel** &lt;id&gt; &lt;value&gt;|Sets value for channel #id (only for lights)|
|**color** &lt;value&gt;|Sets RGB color (only for lights)|
|**commands**|Lists available commands|
|**crash**|Shows stack dump from last crash|
|**del** &lt;key&gt;|Deletes setting from EEPROM. Built-in|
|**dictionaries**|Available dictionaries. Built-in|
|**eeprom.dump [&lt;ascii&gt;]**|Dumps EEPROM contents to console (pass a 1 to print ASCII characters)|
|**erase.config**|Tries to reset SDK config and restarts the board|
|**factory.reset**|Deletes all settings from EEPROM and resets the device|
|**get** &lt;key&gt;|Shows the value a the given setting|
|**gpio** &lt;id&gt; [&lt;value&gt;]|Gets or sets the GPIO #id state|
|**ha.clear**|Clear retained message for MQTT Discovery in Home Assistant|
|**ha.config**|Output Home Assistant configuration code|
|**ha.send**|Send message for MQTT Discovery in Home Assistant|
|**hardware**|Access hardware resources. Built-in. Not implemented|
|**heap**|Shows free heap|
|**help**|Lists available commands (alias for "commands")|
|**i2c.scan**|Lists available i2c devices|
|**i2c.clear**|Recovers i2c bus from failure|
|**info**|Shows info about the device, the firmware and the WiFi connection|
|**kelvin**|Sets the temperature color in Kelvin (only for lights)|
|**keys**|Lists the setting keys stored in EEPROM.|
|**magnitudes**|Lists sensor magnitudes available|
|**mired**|Sets the temperature color in Mired (only for lights)|
|**mqtt.reset**|Reconnects to the MQTT broker using current settings (only if MQTT support)|
|**nofuss**|Forces a check agains NoFUSS server (only if NoFUSS support)|
|**ota** &lt;url&gt;|Downloads a firmware image from the give URL and updates the board|
|**publish**|Built-in publish/subscriber method. Not implemented|
|**read**|Access hardware resources. Built-in. Not implemented|
|**relay** &lt;id&gt; [&lt;value&gt;]|Gets or sets the relay #id state|
|**reset**|Resets board|
|**reset.safe**|Resets board into safe mode (only WiFi AP, serial and OTA will be enabled)|
|**select**|Built-in. Not implemented|
|**set** &lt;key&gt; &lt;value&gt;|Changes the value of the given setting|
|**subscribe**|Built-in publish/subscriber method. Not implemented|
|**unsubscribe**|Built-in publish/subscriber method. Not implemented|
|**uptime**|Shows the current uptime in seconds|
|**wifi.ap**|Disconnect and create an access point|
|**wifi.reset**|Reconnects to the WiFi using current settings|
|**wifi.scan**|Scans for WiFi networks around and shows info|
|**write**|Access hardware resources. Built-in. Not implemented|

You can read about some of the built-in commands in the [Embedis wiki](https://github.com/thingSoC/embedis/wiki/Using-Embedis).

## Settings ##

The **get**, **set** and **del** commands let you query, modify or delete configuration settings. Most of those settings can be changed from the web interface.

Settings are stored in EEPROM. They persist across reboots and they survive firmware or filesystem updates (both wired or OTA) unless you change the flash layout.

This is a list of current settings with description and default values. '#' means a number starting from 0.

|Key|Description|Possible values|Default value|
| --- | --- | --- | --- |
|**ALEXA**|
|alexaEnabled|Is Alexa integration enabled?|0 (no) or 1 (yes)|1 (yes)|
|**API**|
|apiEnabled|Should REST API be enabled?|0 (no) or 1 (yes)|0 (no)|
|apiKey|API Key required for all REST API requests|HEX string|(auto-generated when saving from WebUI for the first time)|
|apiRealTime|Should the API should respond with real time values or filtered ones?|0 (no) or 1 (yes)|0 (no)|
|**BUTTONS**|
|btnDelay|Double click delay in milliseconds|an integer|500|
|**DOMOTICZ**|
|dczEnabled|Should Domoticz be enabled?|0 (no) or 1 (yes)|1 (yes)|
|dczTopicIn|Topic to send values to Domoticz||domoticz/in|
|dczTopicOut|Topic where Domoticz sends commands to||domoticz/out|
|dczRelayIdx#|IDX in Domoticz for the n-th relay (both to get and set value)|An integer, 0 or empty to disable report|0|
|dczMagnitude#|IDX in Domoticz for the n-th magnitude (type "magnitudes" for a list of available magnitudes)|An integer, 0 or empty to disable report|0|
|**GENERAL**|
|adminPass|Password to access web interface, connect to the device in AP mode or perform OTA updates|String of at least eight characters (letters, numbers or the underscore) with at least one number, one lowercase and one uppercase letter|fibonacci|
|hostname|Hostname for the device, device would be accessible at http://hostname.lan|A string|ESPURNA_XXXXXX (where XXXXXX are hex encoded bytes of Chip ID)|
|board|Board id (this setting is meant for future identification)|||
|boardName|Board id (this setting is used to identify the board on OTA updates)|||
|cfg|Configuration version (this setting is meant for future identification)|||
|loopDelay|Delay in milliseconds at the end of the main loop (reduces power consumption but also responsiveness)|A number equal or greater than 0|10|
|**HOME ASSISTANT**|
|haEnabled|Home Assistant MQTT discovery feature enabled|0 (no) or 1 (yes)|1 (yes)|
|haPrefix|Home Assistant MQTT prefix|A string|homeassistant|
|**I2C**|
|i2cCST|I2C Clock Stretch Time in milliseconds (only for I2C_Brzo library)|A positive number|200|
|i2cFreq|I2C SCL frequency (only for I2C_Brzo library)|A positive number|1000|
|i2cSCL|SCL GPIO|A valid digital GPIO|5|
|i2cSDA|SDA GPIO|A valid digital GPIO|4|
|**INFLUXDB**|
|idbDatabase|InfluxDB database name|A string||
|idbEnabled|Enable sending data to InfluxDB|0 (no) or 1 (yes)|0 (no)|
|idbHost|InfluxDB database host|A string||
|idbPassword|InfluxDB database password|A string||
|idbPort|InfluxDB database port|An integer|8086|
|idbUsername|InfluxDB database username|A string||
|**LED**|
|ledMode#|Behavior for the n-th LED (currently only supported for the first LED)|One of the LED modes defined in general.h|1 (LED_MODE_WIFI)|
|**MQTT**|
|mqttClientID|MQTT client ID|A string|Same as default hostname|
|mqttEnabled|Enable sending MQTT messages|0 (no) or 1(yes)|1 (yes)|
|mqttFP|Fingerprint for SSL server|A 20 hex values separated by ':'||
|mqttGetter|MQTT getter suffix|A string with a leading slash||
|mqttGroup#|Synchronization group for the n-th relay|An MQTT topic||
|mqttGroupColor|Synchronization group for the color|An MQTT topic||
|mqttGroupInv#|Logic for the synchronization group for the n-th relay|0 (same) or 1(inverted)|0 (same)|
|mqttKeep|Keep alive time in seconds|A number greater than 10|30|
|mqttPassword|Password to connect to the MQTT broker|A string||
|mqttPort|Port the MQTT broker is listening to|A number|1883|
|mqttQoS|QoS level for MQTT messages and subscriptions|0 (at most one), 1 (at least one) o 2 (one and only one)|0 (at most one)|
|mqttRetain|Retain flag for messages|0 (don't retain) or 1 (retain)|1 (retain)|
|mqttServer|Address of the MQTT broker|An IP, hostname or empty to disable MQTT connection||
|mqttSetter|MQTT setter suffix|A string with a leading slash|/set|
|mqttTopic|Root topic for all MQTT topics of this device|A string, {hostname} will be replaced by the current hostname|{hostname}|
|mqttUseJson|Whether to group messages in a JSON format|0 (no) or 1(yes)|0 (no)|
|mqttUser|User to connect to the MQTT broker|A string||
|mqttUseSSL|Whether to connect using TLS/SSL|0 (no) or 1(yes)|0 (no)|
|**LIGHT**|
|brightness|Brightness value|0 to 255|255|
|ch#|Value for the n-th channel|0 to 255|0|
|useColor|Use first 3 channels for RGB|0 (no) or 1 (yes)|1 (yes)|
|useGamma|Use gamma correction for color channels|0 (no) or 1 (yes)|0 (no)|
|useWhite|Use white channel if all 3 RGB have the same value|0 (no) or 1 (yes)|0 (no)|
|useCSS|Use CSS (#FF0000) or comma separated values (255,0,0) for color reporting|0 (CSV) or 1 (CSS)|1 (CSS)|
|useRGB|Use first three channels as color channels (only if light has at least 3 ch)|0 (no) or 1 (yes)|1 (yes)|
|useTransitions|Use color transitions|0 (no) or 1 (yes)|1 (yes)|
|**NOFUSS**|
|nofussEnabled|Enable checking updates against a NoFUSS server|0 (no) or 1(yes)|0 (yes)|
|nofussInterval|Milliseconds between NoFUSS update checks|Number|3600000|
|nofussServer|NoFUSS service URL|URL, empty to disable NoFUSS||
|**NTP**|
|ntpDST|Enable daylight saving time|0 (no) or 1 (yes)|1 (yes)|
|ntpOffset|Time offset from UTC in minutes|Number|60|
|ntpRegion|NTP region to use for DST calculation|0 (Europe) or 1 (USA)|0 (Europe)|
|ntpServer#|NTP server to use (up to 3 different servers)|A string||
|**RELAY**|
|relayBoot#|Relay boot mode, what state the relay should have upon boot|0 (off), 1 (on), 2 (same as before), 3 (opposite from before)|0 (off)|
|relayPulse#|Relay pulse mode|0 (no pulse), 1 (normally OFF), 2 (normally ON)|0 (no pulse)|
|relayTime#|Relay pulse time in seconds|Number|1|
|relaySync|Relay synchronization mode|0 (no sync), 1 (at most one relay ON), 2 (one and only relay ON), 3 (all the same)|0 (no sync)|
|**RFBRIDGE**|
|rfbOFF#|Code to turn OFF the n-th device|A string||
|rfbON#|Code to turn ON the n-th device|A string||
|**SCHEDULER**|
|schAction#|Action to perform for n-th schedule|0 (turn off), 1 (turn on) or 2 (toggle)|0 (turn off)|
|schHour#|Time (hour) at which the n-th schedule action should take place|0 to 23|0|
|schMinute#|Time (minute) at which the n-th schedule action should take place|0 to 59|0|
|schSwitch#|Switch to perform the action of the n-th schedule|0 to number of relays (0-based)|0|
|schWDs#|Weekdays at which the n-th schedule action should take place. Encoded as string of numbers where Monday is 1|A string|1234567 (Every day)|
|**SENSORS**|
|energyUnit|Energy unit to use|0 (Joules) or 1 (KWh)|0 (Joules)|
|pwrRatioC|Ratio for current value|(will depend on the actual sensor)|(will depend on the actual sensor)|
|pwrRatioP|Ratio for power value|(will depend on the actual sensor)|(will depend on the actual sensor)|
|pwrRatioV|Ratio for voltage value|(will depend on the actual sensor)|(will depend on the actual sensor)|
|pwrUnits|Power unit to use|0 (Watt) or 1 (Kilowatt)|0 (Watt)|
|pwrVoltage|Nominal RMS mains voltage|125, 220, 230... depends on country|230|
|snsRead|Sensor read interval in seconds|A positive number greater than 2|6|
|snsReport|Sensor report every N reads|A positive number greater than 0|10|
|tmpUnits|Temperature unit to use|0 (Celsius) or 1 (Fahrenheit)|0 (Celsius)|
|tmpCorrection|Temperature correction in C or F degrees|Any number|0|
|**TELNET**|
|telnetSTA|Enable telnet when connected to a router (STAtion mode)|0 (no) or 1 (yes)|0 (no)|
|**THINGSPEAK**|
|tspkEnabled|Enable reporting values to Thingspeak platform|0 (no) or 1 (yes)|0 (no)|
|tspkKey|API Key for the channel to send data to|A string provided by Thingspeak||
|tspkMagnitude#|Field number for n-th magnitude|The field number to report to (1 to 8) or 0 to disable reporting|0|
|tspkRelay#|Field number for n-th relay|The field number to report to (1 to 8) or 0 to disable reporting|0|
|**WEB**|
|webPort|Port to listen to HTTP requests|An integer|80|
|wsAuth|Use WebSocket authentication|0 (no) or 1 (yes)|1 (yes)|
|**WIFI**|
|dns#|DNS for the n-th WiFi network when using static IP|IP||
|gw#|Gateway for the n-th WiFi network when using static IP|IP||
|ip#|Static IP for the n-th WiFi network|IP||
|mask#|Netmask for the n-th WiFi network when using static IP|||
|pass#|Password of the n-th WiFi network|String||
|ssid#|SSID or name of the n-th WiFi network|String|||
|wifiScan|Perform a scan to find best WiFi network|0 (no) or 1 (yes)|1 (yes)|

## Usage ##

You can configure your WiFi connection without web interface through the terminal. For instance:

```
set ssid0 myhome
set pass0 mypass
wifi.reset
```