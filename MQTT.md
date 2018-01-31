# MQTT

MQTT stands for "Message Queueing Telemetry Transport". It uses the publisher-subscriber pattern and it's especially suited for small messages when networks bandwidth is limited or when the network is not reliable. Nevertheless, it has become a defacto standard for sensor messaging over TCP.

Check [MQTT.org](http://mqtt.org/) for more info.

ESPurna is built by default with support for MQTT v3.1. To build an image without MQTT support set the MQTT_SUPPORT setting to 0. The current version also supports MQTT over SSL but it is disabled by default since this feature has a heavy memory footprint and is not compatible with other features in the firmware. See "SSL support" below.

## Configuration

You can configure MQTT via the web interface or the terminal. Check the commands available in the [Terminal](Terminal) page.

![ESPurna UI MQTT](images/ui/espurna-ui-mqtt.png)

## Topic format

### Root topic

Every MQTT message that ESPurna publishes starts with the **root topic** you define in the "MQTT Root Topic" setting. That root topic is then complemented by the **specific message topic** (like "relay" or "temperature") plus **an index** when there is more that one of such elements (more than one relay) plus a trailing particle to tell commands from states.

### Command and state

A **state topic** is what ESPurna broadcasts telling every listener out there about something that happened ("the temperature is 18.3C"). A **command topic** is one ESPurna subscribes to to listen to requests from other services. The default state topic particle is "" (empty string, meaning no trailing particle). The default command topic particle is "/set".

As an example, a board with one relay will publish the relay status when it changes to:

`<root topic>/relay/0`

And will listen to commands to modify the relay status at:

`<root topic>/relay/0/set`

### Placeholders

The root topic may include one of these placeholders:

| Placeholder | Value | 
|--- | --- |  
| {hostname} | The hostname of the board as defined in the General tab | 
| {mac} | The MAC of the ESP8266 | 

There is one special placeholder: '**#**'. The hash symbol indicated where the specific message topic will be inserted. If you don't specify a location for the specific message topic it will be inserted after the root topic. For instance, if you have a temperature sensor called "garden", and you set the root topic to `sensor/#/{hostname}` the messages will be sent to `sensor/temperature/garden`.

### JSON payload

When the "Use JSON Payload" option is enabled, the messages will be grouped in a JSON payload. The way it works is that, internally, messages are enqueued and sent after a certain time (100 milliseconds). Any message that is enqueued during that time lapse will reset the count down. When the countdown is done all enqueued messages are grouped in a JSON payload an sent to the `<root topic>/data` topic along with some extra info.

For instance, a sensor that reports temperature and humidity will publish two topics every X seconds like this:

```
<root topic>/temperature => 18.3
<root topic>/humidity => 65
```

With the "Use JSON payload" option enabled only one message will be sent:

```
<root topic>/data => {'temperature': 18.3, 'humidity': 65, 'datetime': '2018-01-31 23:46:17', 'mac': '00:11:22:33:44:55', 'hostname': 'MINI', 'ip': '192.168.1.105', 'id': 37}
```

## Messages

* Heartbeat
* Relays
* Lights
* Sensors

## Examples

* Toggle a relay
* Changing the color
* Subscribing to all messages of a device

## Features based on MQTT

* Relay & color synchronization across devices
* Home Assistant auto-discovery
* Domoticz

## Implementation

* AsyncMqttClient vs PubSubClient

## SSL support

* Memory limitations
* Build image with SSL support
* Suggested configuration
* Server footprints

