# Domoticz #

Integrating an ESPurna switch into [Domoticz](https://www.domoticz.com/) is done using MQTT protocol. From the ESPurna side everything is there already: MQTT support is built-in and you can configure the IDX you want to report to from the web interface. But you will have to configure a virtual switch in Domoticz to interact with it.

## MQTT broker ##

Of course you will need an MQTT broker. That's the service that listens and dispatches messages. You have two options here:

* Install a broker locally, in a home server or an always-on computer.
* Use a cloud broker.

For running a local broker my recommendation is to use [Moquitto](https://mosquitto.org/). It's light and multi-platform. Check their site for instructions to install it on your server. Keep in mind that it runs on a computer, not on the device running ESPurna. ESPurna will be a "client" for this broker.

For running a cloud broker you have many available option. [CloudMQTT](https://www.cloudmqtt.com/) is one of the most populars that has a free plan.

## Configuring Domoticz ##

The Domoticz wiki has an entry specifically for [MQTT](https://www.domoticz.com/wiki/MQTT). Check the "Add hardware MQTT Client Gateway" for the initial setup. You will configure Domoticz on the device as an MQTT client pointing to your broker (the one you have setup in the step above).

Once you have the "MQTT Client Gateway with LAN interface" hardware in the hardware list you will have to add another hardware of type "Dummy (used for virtual switches)" and give it a name. 

Now you are ready to create "virtual sensors" where ESPurna will send the data to. You can do that by clicking "Create Virtual Sensors". Name it too. The type of sensor will depend on the data you send. ESPurna currently supports this types:

* "Switch" to read relay state and toggle them on and off.
* "Temperature" sensor (DHT or DS18B20 modules).
* "Humidity" sensor (DHT module).
* "Electric (Instant+Counter)" for power and energy monitoring (EMON or HLW8012 modules). Note: select "computed" for in the "energy read" option.
* "Voltage" for voltage monitoring (HLW8012 module).

Now if you go to the "devices" page you should see the device you have just created and the IDX is has been given by Domoticz. This is the number you have to define in the "DOMOTICZ" tab in ESPurna.

The communication from Domoticz to ESPurna is quite fast, almost instantaneous, but the other way round it may take a few seconds to update the switch status in Domoticz. Patience....