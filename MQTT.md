# MQTT

MQTT stands for "Message Queueing Telemetry Transport". It uses the publisher-subscriber pattern and it's especially suited for small messages when networks bandwidth is limited or when the network is not reliable. Nevertheless, it has become a defacto standard for sensor messaging over TCP.

Check [MQTT.org](http://mqtt.org/) for more info.

ESPurna is built by default with support for MQTT v3.1. To build an image without MQTT support set the MQTT_SUPPORT setting to 0. The current version also supports MQTT over SSL but it is disabled by default since this feature has a heavy memory footprint and is not compatible with other features in the firmware. See "SSL support" below.

## Configuration

You can configure MQTT via the web interface or the terminal. Check the commands available in the [Terminal](Terminal) page.

![ESPurna UI MQTT](images/ui/espurna-ui-mqtt.png)

## Topic format

### Root topic

Every MQTT message that ESPurna publishes starts with the **root topic** you define in the "MQTT Root Topic" setting. That root topic is then complemented by the **specific message topic** (like "relay" or "temperature"), **an index** when there is more that one of such elements (more than one relay) and a trailing particle to tell commands from states.

### Commands and states

A **state topic** is what ESPurna broadcasts telling every listener out there about something that happened ("the temperature is 18.3C"). A **command topic** is one ESPurna subscribes to listen to requests from other services. The default state topic particle is `""` (empty string, meaning no trailing particle). The default command topic particle is `"/set"`.

As an example, a board with one relay will publish the relay status when it changes to:

`{root topic}/relay/0`

And will listen to commands to modify the relay status at:

`{root topic}/relay/0/set`

### Placeholders

The root topic may include one of these placeholders:

Placeholder  | Value
------------ | -------------------------------------------------------
`{hostname}` | The hostname of the board as defined in the General tab
`{mac}`      | The MAC of the ESP8266

There is one special placeholder: '**#**'. The hash symbol indicates where the specific message topic will be inserted. If you don't specify a location for the specific message topic it will be inserted after the root topic. For instance, if you have a temperature sensor called "garden", and you set the root topic to `sensor/#/{hostname}` the messages will be sent to `sensor/temperature/garden`. In the documentation all topic examples asume the hash placeholder is either not used or placed at the end of the root topic.

### JSON payload

When the "Use JSON Payload" option is enabled, messages will be grouped in a JSON payload. Internally, messages will be enqueued and sent after a certain time (100 milliseconds). Any message that is also enqueued during that time lapse will reset the count down. When the count down is done all enqueued messages are grouped in a JSON payload and sent to the `data` specific message topic along with some extra info.

For instance, a sensor that reports temperature and humidity will publish two topics every X seconds like this:

```
{root topic}/temperature => 18.3
{root topic}/humidity => 65
```

With the "Use JSON payload" option enabled only one message will be sent:

```
{root topic}/data => {'temperature': 18.3, 'humidity': 65, 'datetime': '2018-01-31 23:46:17', 'mac': '00:11:22:33:44:55', 'hostname': 'MINI', 'ip': '192.168.1.105', 'id': 37}
```

## Messages

### Heartbeat

Heartbeat messages are only state messages and are sent every X seconds (5 minutes by default). These messages report the status of the device amb some useful info.

State topic             | Example payload       | Notes
----------------------- | --------------------- | ------------------------------------------------------
`{root topic}/status`   | `1`                   | This is also the will topic<br />with a payload of "0"
`{root topic}/app`      | `ESPURNA`             |
`{root topic}/version`  | `1.12.3`              |
`{root topic}/hostname` | `MINI`                |
`{root topic}/ip`       | `192.168.1.105`       |
`{root topic}/mac`      | `00:11:22:33:44:55`   |
`{root topic}/uptime`   | `3215`                | Seconds
`{root topic}/datetime` | `2018-02-01 00:03:25` | Only if NTP enabled<br />and synced
`{root topic}/freeheap` | `22056`               | Bytes

Relay and light status are also sent along with the heartbeat. Check topics for those below.

### Relays

The relay module publishes the relay state and subscribes to command topics to manage the relays via MQTT. The specific message topic will always end with a 0-based index (first relay is index 0).

State topic            | Example payload | Notes
---------------------- | --------------- | -----
`{root topic}/relay/0` | `1`             | [0,1]

Command topic              | Example payload | Notes
-------------------------- | --------------- | ---------------------------
`{root topic}/relay/0/set` | `toggle`        | [0,1,2,on,off,toggle,query]

Relay command payloads accept both numbers (0 for 'off', 1 for 'on' and 2 for 'toggle') or words (case insensitive).

### Lights

The light module publishes and subscribes to different topics.

State topic               | Example payload | Notes
------------------------- | --------------- | -------------------------------------
`{root topic}/rgb`        | `#FF0000`       | Also as CSV if "Use CSS style" is off
`{root topic}/hsv`        | `300,100,100`   | See note below
`{root topic}/brightness` | `35`            | From 0 to 100
`{root topic}/ch/0`       | `128`           | For each channel,<br />from 0 to 255

Hue value ranges from 0 to 360. Saturation and Value from 0 to 100.

### Sensors

## Features based on MQTT

### Relay & color synchronization across devices

* mqttGroup
* mqttGroupInv

### Home Assistant auto-discovery
### Domoticz

## Implementation

### AsyncMqttClient vs PubSubClient

## SSL support

### Memory limitations
### Build image with SSL support
### Suggested configuration
### Server footprints

