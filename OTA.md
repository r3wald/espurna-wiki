# Over-the-air updates

## Manually driven OTA updates

Once you have flashed your board with the ESPurna firmware you can flash it again over-the-air using PlatformIO and the ```ota``` environment:

```bash
> pio run -t upload -e itead-sonoff-basic-ota
```

When using OTA environment it defaults to the IP address of the device in SoftAP mode. If you want to flash it when connected to your home network the best way is to supply the IP of the device:

```bash
> pio run -t upload -e itead-sonoff-basic-ota --upload-port 192.168.1.151
```

Please note that if you have changed the admin password from the web interface you will have to change it in the platformio.ini file for the OTA to work. Check for the *upload_flags* option in your ota-enabled environment.

With version 1.9.0 the platformio.ini file defines 3 useful environments for custom OTA updates: esp8266-1m-ota, esp8266-4m-ota and esp8285-1m-ota. And example of use is:

```bash
> export ESPURNA_BOARD="ITEAD_SONOFF_BASIC"
> export ESPURNA_IP="192.168.1.151"
> export ESPURNA_AUTH="my_ota_pass"
> export ESPURNA_FLAGS=""
> pio run -t upload -e esp8266-1m-ota
```

### Troubleshooting

Sometimes OTA updates fail. It happens. It's not a problem since the firmware does not get overwritten if the upload fails. But if you cannot update the device firmware even after several attempts, you might try to check if you have a firewall and disable it.

## Web interface updates

You can directly upload the firmware file (.bin extension) to the device using the "Upgrade" option in the "Admin" tab of the web interface. You can find the latest firmware images for your device in the [releases page](https://github.com/xoseperez/espurna/releases/).

## Updating from the Terminal

From version 1.12.4, ESPurna includes an 'ota' command in the terminal that allows you to update the firmware in the device passing the URL of a binary as an argument. The URL can be in the local network or the internet, but the device has to have direct access to that resource (no redirects). HTTPS is not supported at the moment.

Simply open a telnet session to the device and request an OTA update passing the URL:

```
> telnet 192.168.1.15
ota http://192.168.1.11/espurna-1.12.4a-wemos-d1mini-relayshield.bin
[038771] +OK
[038771] [OTA] Downloading from 'http://192.168.1.11/espurna-1.12.4a-wemos-d1mini-relayshield.bin'
[053298] [OTA] Done, restarting...
```

## Automatic OTA updates

You can also use the automatic OTA update feature. Check the [NoFUSS library](https://bitbucket.org/xoseperez/nofuss) for more info.

This options is disabled by default. Enable it in your firmware setting NOFUSS_SUPPORT to 1 in general.h or via a build parameter.
