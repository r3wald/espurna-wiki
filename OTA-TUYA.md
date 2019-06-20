> This method is experimental. If it doesn't work, you will have to use [standard flashing method](Binaries)
> Please reference tuya-convert project [README.md](https://github.com/ct-Open-Source/tuya-convert/blob/master/README.md) first for the most recent information on this OTA method.

# Introduction 

A Chinese company named Tuya offers a free-to-brand turnkey smart home solution to anyone. Using their offer is dead-simple, since everything can be done by clicking through the Tuya web page, from choosing your pre-designed products or pre-programmed wifi-modules (mostly ESP8266) to building your own app. In the end, this has resulted in as they claim over 11 000 devices 'made' by over 10 000 vendors using Tuyas firmware and cloud services. [^1]

Using this collection of scripts you can flash Tuya IoT devices to alternative firmwares without soldering:
https://github.com/ct-Open-Source/tuya-convert
 
# Compatibility

This method should be compatible with most devices on the market. However, since January 29th, 2019 Tuya has started distributing a patch that prevents tuya-convert from completing successfully. It is up to the individual brands to adopt the patch, so some devices may be affected sooner than others. To ensure the best chance of success, do not connect your device with the official app as it may automatically update the device, preventing you from flashing with tuya-convert. Some devices are already being shipped with the update, in which case there is unfortunately no work around available at this time.[^2]

# Flashing ESPurna image

Follow the procedure up until the **FLASH third-party firmware**[^3] step and replace `thirdparty.bin` in the URL with espurna-core .bin that is in the same directory.

# More information

Also see these issues:
https://github.com/xoseperez/espurna/issues/1458
https://github.com/xoseperez/espurna/issues/1713

[^1]: https://github.com/ct-Open-Source/tuya-convert#tuya-convert
[^2]: https://github.com/ct-Open-Source/tuya-convert#procedure
[^3]: https://github.com/ct-Open-Source/tuya-convert#flash-third-party-firmware
