# Home Assistant Integration 

Integrating an ESPurna switch into [Home Assistant](https://home-assistant.io/) is very easy since both talk MQTT. You don't need any special addon in ESPurna but you will need to properly configure the MQTT connection.

Once the ESPurna powered device is connected to your MQTT broker of choice, it's time to configure the link from the configuration.yaml file of your Home Assistant instance.

*Note: I'm assuming here you already have Home Assistant installed somewhere. Head over to their [getting started](https://home-assistant.io/getting-started/) page to do it if you have not.*

## HomeAssistant Configuration 

First make sure your Home Assistant instance connects to the same broker you connected the ESPurna device. You can read the [Home Assistant MQTT](https://home-assistant.io/components/mqtt/) page for a full explanation of the process but you will basically have to add these lines to your configuration.yaml file:


```yaml
#!yaml

mqtt:
  broker: <your broker ip>
  username: "<username for the MQTT connection>"
  password: "<password for the MQTT connection>"

```

This is the bare minimum (username and password are optional, but you really should use them). If your broker setup is not standard check all the configuration options in the [Home Assistant MQTT](https://home-assistant.io/components/mqtt/) page.

## Link your ESPurna device to Home Assistant 

Home Assistant has a special type of device called "switch". You can configure this switch to use MQTT connection. Basically you will have to define the command (write) and status (read) topics and payloads.

Here you have a sample configuration (add these lines to the same configuration.yaml file):


```yaml
#!yaml
switch:
  - platform: mqtt
    name: "Test Switch"
    state_topic: "/test/switch/D1MINI/relay/0"
    command_topic: "/test/switch/D1MINI/relay/0/set"
    payload_on: 1
    payload_off: 0
    optimistic: false
    qos: 0
    retain: true

```

As you can see we are setting the "platform" to "mqtt" to use the connection be have previously configured. We can use the same topic for command and status. The topic you have to use is the "MQTT Root Topic" you configure in the MQTT page in your ESPurna device web interface, plus "/relay/" plus the number of the relay (if your board has only one relay that would be number 0). Also note the payloads for both of them, these are required by ESPurna.

## Link an ESPurna light to Home Assistant ##

ESpurna supports color, brightness, temperature color and individual channels for light devices (dimmers, my9192-based light bulbs,...). An example configuration for Home Assistant would be:

```yaml
#!yaml
light:
  - platform: mqtt
    name: 'Test RGBW Light'
    state_topic: '/test/light/relay/0'
    command_topic: '/test/light/relay/0/set'
    payload_on: 1
    payload_off: 0
    rgb_state_topic: '/test/light/color'
    rgb_command_topic: '/test/light/color/set'
    rgb: true
    optimistic: false
    color_temp: true
    color_temp_command_topic: '/test/light/mired/set'
    brightness: true
    brightness_scale: 255
    brightness_command_topic:  '/test/light/brightness/set'
    brightness_state_topic: '/test/light/brightness'
    white_value: true
    white_value_command_topic: '/test/light/channel/3/set'
    white_value_state_topic: '/test/light/channel/3'
```