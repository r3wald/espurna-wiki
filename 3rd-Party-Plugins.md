espurna includes integration hooks for custom code and 3rd party modules integration. 
This article include template files and document,  integration model to make it easier when integrating plugins (or 3rd party code). 
Please also look at the attached files, all includes inline help documentation for possible featurs.
The main concept is to allow adding new functionality to espurna with zero to minimal code changes to espurna (just adding the new files and integrating by setting a build flag only). 
 
## Files:
* **custom.h** - this is the generic espurna custom header include file (included by all.h based on USE_CUSTOM_H build flag) allows setting and overriding espurna core definitions.
To this file I've added the plugin activation code and a single flag to each plugin to set if to include the plugin in the image file.

* **plugin1.h** - The plugin header file (should be placed in config folder) includes plugin specific defines. this header is included by custom.h based on the plugin include flag (INCLUDE_PLUGINx) to allow switching on/off integration of multiple plugins.

* **plugin1.ino** - The plugin template, to be placed in code folder. this template enables writing a plugin and use all espurna services and utils (I may missed some....but will improve).

## Status:
In development phase, working, limited tresting.

## Limitations 
* Due to current frontend structure, I did not add the HTML/JS/CSS files, since I did not want to change core files, so in case of frontend need for plugin, you need to add the plugin page, but all the web services hooks included in the template (don't forget to gulp).
* A more generic hook system that will enable a tightly coupled plugins (that will get callbacks from different espurna internal hook points) is under development.
 
## Template structure:
(All inline documented )
Like any other espurna module, includes Helper functions, setup and main loop:
* Helper functions you can copy/add any the template includes a single main loop sample function _pluginFunction(); with all possible services hooks, you can copy it. Other helper functions are utils used by setup or loop function (like set a relay or read sensor).
* Setup function (pluginxSetup()) called by extraSetup() defined in custom.h. extraSetup() is called by espura.ino setup function based on USE_EXTRA flag (this is the generic espurna 3rd party code integration hook).
* Plugin main loop called by espurna loop (via callback function registrations array). plugin loop is registered by pluginsetup function.

## Template features:
(services enabled by the plugin template), most code is commented out, to allow uncomment/delete needed/unneeded code. The services are all public espurna functions to be used for the specific plugin needs logic and data.  

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

## Installation:
* Copy the two .h files into espurna/config folder
* Copy the .ino file to espurna folder
* Build with -DUSE_CUSTOM_H flag
* See on debug (web/serial/telnet) a loop counter (every PLUGIN_REPORT_EVERY param)
* Terminal command plugin1 0 will stop plugin execution and plugin1 1 start
* API command /plugin1?apikey=xxxxx&value=0 stop (value=1) start
* Read plugin1.ino and plugin1.h inline documentation and write your espurna magic  
   
## Please feel free to give any feedback/comment/suggestion  
 
[plugin.zip](https://github.com/xoseperez/espurna/files/1903667/plugin.zip)


