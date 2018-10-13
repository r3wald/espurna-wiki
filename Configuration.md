# Configuration

ESPurna allows configuring some of it's features at runtime, without the need to compile .bin yourself. Following article explains the steps required to configure the device when flashed with precompiled image from the Releases section.

## First boot

On normal boot (i.e. not in flashing mode) it will start SoftAP (Software Access Point) named "ESPURNA-XXXXXX", where XXXXXX are the last 3 bytes of the radio MAC. It will use default settings for the hardware and features like button, LED, relay, the SPIFFS memory access, the WIFI, the Web Server, MQTT, sensors etc.

To configure the device to your liking: 

* Connect with phone or computer to the "ESPURNA-XXXXXX" network, using "fibonacci" as passphrase.
* Once connected browse to "http://192.168.4.1" or "http://192.168.244.1". If you are on a mobile phone, make sure to disable cellular data as you may not be able to access this IP otherwise.
* When asked for credentials, enter "admin" as username and "fibonacci" as password.
* You will be asked to change the default password, so either generate or type one manually. Make sure to remember it as it is used for both WebUI and device's access point.
* Once you change the password you will have to authenticate yourself again using this new password.

## WiFi configuration

You can configure up to five WiFi networks. It will then try to connect to the configured WiFi networks in order of signal strength. If it cannot connect to any network, it will start the SoftAP mode again and retry in 3 minutes.  

You can also manually switch to **SoftAP mode by double clicking the on-board button** or **reset the device settings by long pressing it**.

## Other settings

Using WebUI **Admin** panel you can both backup and restore device settings. Settings are saved as .json file with "key": "value" pairs surrounded by the curly braces. You can use https://github.com/xoseperez/espurna/wiki/Terminal#settings as a reference for possible configuration keys and their values.

## Direct HTTP settings API

You can use "/config" endpoint to directly view or replace device configuration.  
For example, using "curl" command:

```
$ curl -u admin:fibonacci http://192.168.4.1/config
{
  "app": "ESPURNA",
  "version": "1.13.3",
  "hostname": "ESPURNA-123456",
  "pass0": "9876543210",
  "ssid0": "OldWiFiHotSpot"
}
$ cat my-settings.json
{"app": "ESPURNA","hostname": "SONOFF-BASIC","password":"mynewpassword","ssid0": "NewWiFi","pass0": "12345678"}
$ curl -F "file=@my-settings.json" -u admin:fibonacci http://192.168.4.1/config
$ curl -u admin:mynewpassword http://192.168.4.1/config
{
  "app": "ESPURNA",
  "version": "1.13.3",
  "hostname": "SONOFF-BASIC",
  "adminPass": "mynewpassword",
  "pass0": "12345678",
  "ssid0": "NewWiFi"
}
```
> Note: "app" key is mandatory and **must** be equal to "ESPRUNA". Configuration will be ignored otherwise.