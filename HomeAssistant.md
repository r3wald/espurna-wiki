# Home Assistant Integration 

Integrating an ESPurna switch into [Home Assistant](https://home-assistant.io/) is very easy since both talk MQTT. You don't need any special addon in ESPurna but you will need to properly configure the MQTT connection.

Once the ESPurna powered device is connected to your MQTT broker of choice, it's time to configure the link from the configuration.yaml file of your Home Assistant instance.

> Note: I'm assuming here you already have Home Assistant installed somewhere. Head over to their [getting started](https://home-assistant.io/getting-started/) page to do it if you have not. 

> Note: Integration with Home Assistant is done using "MQTT platform", not "MQTT-JSON platform". Each message is sent to it's own topic. This means you should **disable "JSON payload"** in the ESPurna MQTT tab to make it work.

> Note: If [Discovery](https://www.home-assistant.io/components/discovery/) component is configured and Alexa emulation is enabled on the device, Home Assistant will discover ESPurna as WeMo switch / light.

## Basic configuration

### Build settings

| Build flag | Description | Default value |
| --- | --- | --- |
| `HOMEASSISTANT_SUPPORT` | Enable Home Assistant module | `MQTT_SUPPORT` |
| `HOMEASSISTANT_ENABLED` | Send MQTT discovery message | `0` (off) |

### Home Assistant

First make sure your Home Assistant instance connects to the same broker you connected the ESPurna device. You can read the [Home Assistant MQTT](https://home-assistant.io/components/mqtt/) page for a full explanation of the process but you will basically have to add these lines to your configuration.yaml file:

```yaml
mqtt:
  broker: <your broker ip>
  username: "<username for the MQTT connection>"
  password: "<password for the MQTT connection>"

```

This is the bare minimum (username and password are optional, but you really should use them). If your broker setup is not standard check all the configuration options in the [Home Assistant MQTT](https://home-assistant.io/components/mqtt/) page.

## MQTT Discovery

Instead of manually editing configuration.yaml you can use [MQTT Discovery](https://www.home-assistant.io/docs/mqtt/discovery/) to allow ESPurna device to configure itself automatically.

To enable, add this to the `mqtt` component configuration:
```yaml
mqtt:
  discovery: true
  discovery_prefix: homeassistant
```

### Configuration

|Key|Description|Possible values|Default value|
| --- | --- | --- | --- |
|haEnabled|MQTT Discovery|0 (no) or 1 (yes)|1 (yes)|
|haPrefix|MQTT Prefix|A string|homeassistant

### Terminal commands

|Command|Description|Arguments|
| --- | --- | --- |
|ha.send|Send message for MQTT Discovery in Home Assistant (if enabled)| - |
|ha.clear|Clear retained message for MQTT Discovery in Home Assistant| - |

### Troubleshooting

Discovery topic has the following format:
> {**haPrefix**}/{**switch** or **light**}/{**hostname**}_{**switch** or **light** index}/config

For example:
> homeassistant/switch/ESPURNA-820501_0/config

Discovery topic is sent to the MQTT broker with `retained` flag enabled. To disable discovery manually, send empty message with `retained` flag to the discovery topic.

Home Assistant will keep discovered devices until the next restart.

## Manual configuration 

### WebUI

HASS panel contains configuration generator. Tap **Show** at the **Configuration** section and then add it's output to the configuration.yaml

### Terminal

`ha.config` command will output Home Assistant configuration.yaml code for the device

### Configuration for relays

Home Assistant has a special type of device called "switch". You can configure this switch to use MQTT connection. Basically you will have to define the command (write) and status (read) topics and payloads.

Configuration sample:

```yaml
switch:
  - platform: mqtt
    name: "Test Switch"
    state_topic: "test/switch/D1MINI/relay/0"
    command_topic: "test/switch/D1MINI/relay/0/set"
    payload_on: 1
    payload_off: 0
    optimistic: false
    qos: 0
    retain: true
```

As you can see we are setting the "platform" to "mqtt" to use the connection be have previously configured. We can use the same topic for command and status. The topic you have to use is the "MQTT Root Topic" you configure in the MQTT page in your ESPurna device web interface ("test/switch/D1MINI" in the example), plus "/relay/" plus the number of the relay (if your board has only one relay that would be number 0). Also note the payloads for both of them, these are required by ESPurna (1 for on, 0 for off).

### Configuration for lights

ESPurna supports color, brightness, temperature color and individual channels for light devices (dimmers, my9192-based light bulbs,...).

Configuration sample:

```yaml
light:
  - platform: mqtt
    name: 'Test RGBW Light'
    state_topic: 'test/light/relay/0'
    command_topic: 'test/light/relay/0/set'
    payload_on: 1
    payload_off: 0
    rgb_state_topic: 'test/light/color'
# the next line is only required if you have css style enabled in espurna "lights" settings
#    rgb_value_template: "{{ '%s,%s,%s' | format(value[1:3] | int(value[1:3], 16), value[3:5] | int(value[3:5], 16), value[5:7] | int(value[5:7], 16)) }}"
    rgb_command_topic: 'test/light/color/set'
    rgb: true
    optimistic: false
    color_temp: true
    color_temp_command_topic: 'test/light/mired/set'
    brightness: true
    brightness_scale: 255
    brightness_command_topic:  'test/light/brightness/set'
    brightness_state_topic: 'test/light/brightness'
    white_value: true
    white_value_command_topic: 'test/light/channel/3/set'
    white_value_state_topic: 'test/light/channel/3'
```