ESPurna includes integration hooks for custom code and 3rd party modules integration.

This attached template files, to help integrating or 3rd party code.
Please also take a look at the attached files for inline help documentation, describing the different options and features.

The main concept is to allow adding new functionality to ESPurna with zero to minimal code changes to ESPurna core system (just adding the new files and integrating by setting a build flag only).

## Files
* **custom.h** - this is the generic ESPurna custom header include file (included by all.h based on USE_CUSTOM_H build flag) allows setting and overriding ESPurna core flags definitions.
This file includes the plugin activation code and a single integration (include in load image) enable flag for each plugin (INCLUDE_PLUGINx      0).

* **plugin1.h** - The plugin header file (to be placed in config folder) includes plugin specific defines. this header is included by custom.h based on the plugin include flag (INCLUDE_PLUGINx in custom.h) to allow switching on/off integration of multiple plugins.

* **plugin1.ino** - The plugin template (to be placed in code folder). this template enables writing a plugin and use all ESPurna services and utils (the template file will be enhanced over time).

## Status
In development phase, working, limited testing, new functionality is in progress.
please log issues with PLUGIN: in subject

## Limitations
* Due to current frontend structure, I did not add the HTML/JS/CSS files, since I did not want to change core files, so in case of frontend need for plugin, you need to add the plugin page, but all the web services hooks included in the template (don't forget to gulp).
* A more generic hook system that will enable a tightly coupled plugins (that will get callbacks from different ESPurna internal hook points) is under development.

## Template structure
(All inline documented)
Like any other ESPurna module, includes Helper functions, setup and main loop:
* Helper functions you can copy/add any the template includes a single main loop sample function _plugin1Function1(); with all possible services hooks, you can copy it. Other helper functions are utils used by setup or loop function (like set a relay or read sensor).
* Setup function (pluginxSetup()) called by extraSetup() defined in custom.h. extraSetup() is called by espura.ino setup function based on USE_EXTRA flag (this is the generic ESPurna 3rd party code integration hook).
* Plugin main loop called by ESPurna loop (via callback function registrations array). plugin loop is registered by pluginsetup function.

## Template features
(services enabled by the plugin template), most of the code is commented out to allow uncomment/delete needed/unneeded code. The services are all public ESPurna functions to be used for the specific plugin needs logic and data.

* Main loop features
   * Get sensors data
   * Set relays
   * Factory reset
   * AP mode
   * System reset
   * Setter/Getter for plugin params
   * Broker publish
   * MQTT publish
   * DOMOTICZ publish
   * INFLUXDB publish
   * THINGSPEAK publish

## Installation
* Copy the `custom.h`
* Copy `plugin1.h` files into `lib/plugin1` folder (create `plugin1` folder in existing lib)
* Copy the `plugin1.ino` file to ESPurna folder (where other *.ino files reside)
* Build with `-DUSE_CUSTOM_H` flag
* set INCLUDE_PLUGIN1      1 in `custom.h` config file
* See on debug (web/serial/telnet) a loop counter (every `PLUGIN_REPORT_EVERY` param -5 sec)
* Terminal command `plugin1 0` will stop plugin execution and `plugin1 1` start
* API command `/plugin1?apikey=xxxxx&value=0` stop, `/plugin1?apikey=xxxxx&value=1` start
* Read `plugin1.ino` and `plugin1.h` inline documentation and write your ESPurna magic

## Troubleshooting:
In any case of issues while running with plugins, first disable the plugin execution in runtime, next if this does not 
help, disable plugin include in image file (INCLUDE_PLUGIN1      0). **Please do not open issues on espurna core if you have plugin enabled**.

(folder structures may depend on your framework and development environment, if you get compile/link error regarding existence of these files, please refer to your specific build settings documentation)

## Please feel free to give any feedback/comment/suggestion

[plugin1-v0.0.1.zip](https://github.com/xoseperez/ESPurna/files/1906034/plugin1-v0.0.1.zip)
