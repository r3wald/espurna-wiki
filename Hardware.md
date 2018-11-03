# Supported Hardware

This is the official list of supported hardware for the ESPurna firmware. The hardware configuration for each of these boards can be selected by supplying the build flag (see [Firmware section](Firmware)).

> **CAUTION:**<br>
> * Never ever connect any of these devices to your computer and to mains at the same time.<br>
> * Never ever manipulate them while connected to mains. **Seriously, it can be FATAL!** I don't want you to die.<br>
> * I hold no responsibility for any damage to you, your family, your house,... for any action or results derived from flashing or using these devices.

> **CAUTION:**<br>
> * Different devices may be flashed at different voltages (3.3v, 5v). Make sure your USB-to-UART device is set to the correct one or you risk destroying your device.

## ITEAD Sonoff Modules

| Board | Build flag | Description |
| --- | --- | --- |
| [ITEAD Sonoff Basic](Hardware-Itead-Sonoff-Basic) | `ITEAD_SONOFF_BASIC` | Switch |
| [ITEAD Sonoff RF](Hardware-Itead-Sonoff-RF) | `ITEAD_SONOFF_RF` | Switch with RF Receiver |
| [ITEAD Sonoff Dual](Hardware-Itead-Sonoff-Dual) | `ITEAD_SONOFF_DUAL` <br> `ITEAD_SONOFF_DUAL_R2`  | 2 Switches |
| [ITEAD Sonoff POW](Hardware-Itead-Sonoff-POW) | `ITEAD_SONOFF_POW` | Switch with Power Consumption Measurement |
| [ITEAD Sonoff POW R2](Hardware-Itead-Sonoff-POW-R2) | `ITEAD_SONOFF_POW_R2` | Switch with Power Consumption Measurement |
| [ITEAD Sonoff TH10/16](Hardware-Itead-Sonoff-TH) | `ITEAD_SONOFF_TH` | Switch with Temperature and Humidity Monitoring |
| [ITEAD Sonoff 4CH](Hardware-Itead-Sonoff-4CH) | `ITEAD_SONOFF_4CH` |  4 Switches with din rail mounting |
| [ITEAD Sonoff 4CH Pro / Pro R2](Hardware-Itead-Sonoff-4CH-Pro---R2) | `ITEAD_SONOFF_4CH_PRO` | 4 Switches with din rail mounting and RF Receiver|
| [ITEAD Sonoff Touch](Hardware-Itead-Sonoff-Touch) | `ITEAD_SONOFF_TOUCH` | Touch Wall Switch |
| [ITEAD Sonoff B1](Hardware-Itead-Sonoff-B1) | `ITEAD_SONOFF_B1` | Dimmable E27 LED Lamp RGB Color Light Bulb |
| [ITEAD Sonoff T1](Hardware-Itead-Sonoff-T1) | `ITEAD_SONOFF_T1_1CH` <br> `ITEAD_SONOFF_T1_2CH` <br> `ITEAD_SONOFF_T1_3CH` | 1-3 Gang Touch Wall Switch |
| [ITEAD Sonoff LED](Hardware-Itead-Sonoff-LED) | `ITEAD_SONOFF_LED` | Adjustable LED strip |
| [ITEAD Sonoff RF Bridge](Hardware-Itead-Sonoff-RF-Bridge) | `ITEAD_SONOFF_RFBRIDGE` | Bridge between 433MHz RF and WiFi |
| [ITEAD Slampher](Hardware-Itead-Slampher)<br>[ITEAD Slampher 2.0](Hardware-Itead-Slampher-v2)  | `ITEAD_SLAMPHER` | 433MHz RF & WiFi Smart Light Bulb Holder |
| [ITEAD S20](Hardware-Itead-S20) | `ITEAD_S20` | Outlet |
| [ITEAD S26](Hardware-Itead-S26) | `ITEAD_S20` | Outlet (same image as S20) |
| [ITEAD S31](Hardware-Itead-S31) | `ITEAD_SONOFF_S31` | Outlet |
| [ITEAD 1CH Inching](Hardware-Itead-1CH) | `ITEAD_1CH_INCHING` | [Inching/Self-Locking Switch](https://www.quora.com/What-is-an-inching-switch) |
| [ITEAD Motor Clockwise/Anticlockwise](Hardware-Itead-Motor) | `ITEAD_MOTOR` | Controls 7-32V DC or 125-250V AC motor|
| [ITEAD Sonoff SV](Hardware-Itead-Sonoff-SV) | `ITEAD_SONOFF_SV` |  5-24V low voltage Switch |
| [ITEAD BN-SZ01](Hardware-Itead-BN-SZ01) | `ITEAD_BNSZ01` | LED Ceiling Light |

## Lights / LED Controllers

| Board | Build flag | Description |
| --- | --- | --- |
| [AI-Thinker AI Light / Noduino OpenLight](Hardware-AI-Thinker-AI-Light) | `AITHINKER_AI_LIGHT` | E27 LED Lamp |
| [Magic Home LED Controller](Hardware-Magic-Home-LED-Controller) | `MAGICHOME_LED_CONTROLLER` <br> `MAGICHOME_LED_CONTROLLER_23` <br> `MAGICHOME_LED_CONTROLLER_20` | |
| [Huacanxing H801/H802](Hardware-Huacanxing-H80x) | `HUACANXING_H801` <br> `HUACANXING_H802` | |
| [Arilux AL-LC01<br>Arilux AL-LC02<br>Arilux AL-LC11](Hardware-Arilux-AL-LCxx) | `ARILUX_AL_LC01` <br> `ARILUX_AL_LC02` <br> `ARILUX_AL_LC11` | |
| [Arilux AL-LC06](Hardware-Arilux-AL-LC06) | `ARILUX_AL_LC06` | |
| [Arilux E27](Hardware-Arilux-E27) | `ARILUX_E27` | |
| [InterMitTech QuinLED](Hardware-QuinLED) | `INTERMITTECH_QUINLED` | |
| [Autohometion LYT8266](Hardware-Autohometion-LYT8266) | `AUTHOMETION_LYT8266` | |
| [Generic AG-L4](Hardware-AG-L4) | `GENERIC_AG_L4` | |
| [iWoole Smart Table Lamp](Hardware-IWOOLE_LED_TABLE_LAMP) | `IWOOLE_LED_TABLE_LAMP` | RGBW Table Lamp|

## Power Plugs

| Board | Build flag | Description |
| --- | --- | --- |
| [KMC 70011](Hardware-KMC-70011) | `70011` | Power plug w/ power metering |
| [Schuko Wifi Plug](Hardware-Schuko-Wifi-Plug) | `WIFI_STECKER_SCHUKO` | Power plug |
| [WiOn 50055](Hardware-WiOn-50055) | `WION_50055` | |
| [Xenon SM PW 702U](Hardware-Xenon-SM-PW-702U) | `XENON_SM_PW702U` | |
| [HEYGO HY02](Hardware-HEYGO-HY02) | `HEYGO_HY02` | |
| [Maxcio W-US002S](Hardware-Maxcio-W-US002S) | `MAXCIO_WUS002S` | |
| [Maxcio W-DE004](Hardware-Maxcio-W-DE-003) | `MAXCIO_WDE004` | |
| [YiDian XS-SSA05](Hardware-YiDian-XS-SSA05) | `YIDIAN_XSSSA05` | |
| [Tonbux XS-SSA06](Hardware-Tonbux-XS-SSA06) | `TONBUX_XSSSA06` | |
| [Tonbux Powerstrip02](Hardware-Tonbux-Powerstrip02) | `TONBUX_POWERSTRIP02` | 4 AC Outlets + 4 USB Charging Ports |
| [Zhilde ZLD-44EU-W](Hardware-Zhilde-ZLD-44EU-W) | `ZHILDE_EU44_W` | 4 AC Outlets + 4 USB power supply ports |
| [LINGAN SWA1](Hardware-LINGAN-SWA1) | `LINGAN_SWA1` | Power plug |
| [TONBUX/MXQ SP04](Hardware-LINGAN-SWA1) | `LINGAN_SWA1` | Power plug |
| [NEO COOLCAM NAS WR01W](Hardware-NEO-COOLCAM-NAS-WR01W) | `NEO_COOLCAM_NAS_WR01W ` | Power plug |
| [BLITZWOLF BW-SHP2](Hardware-BLITZWOLF-BW-SHP2) | `BLITZWOLF_BWSHP2 ` | Power plug w/ power metering |
| [Bestek MRJ1011](Hardware-Bestek-MRJ1011) | `BESTEK_MRJ1011` | Power plug w/ 2 USB ports |

## Development Boards

| Board | Build flag | Description |
| --- | --- | --- |
| [Wemos D1 Mini Relay Shield](Hardware-Wemos-D1-Mini-Relay-Shield) | `WEMOS_D1_MINI_RELAYSHIELD` | |
| [NodeMCU Lolin](Hardware-NodeMCU-Lolin) | `NODEMCU_LOLIN` | Actually any NodeMCU clone should work |
| [Witty Cloud](Hardware-Witty-Cloud) | `WITTY_CLOUD` | Simple Board /w RGB Led & LDR |

## Other

| Board | Build flag | Description |
| --- | --- | --- |
| YJZK 2-gang switch | `SWITCH_2CH` | |
| [Tonbux Mosquito Killer](Hardware-Tonbux-Mosquito-Killer) | `TONBUX_MOSQUITO_KILLER` | UV Lamp + Fan for suction |

## Custom Boards

| Board | Build flag | Description |
| --- | --- | --- |
| [Tinkerman's ESPurna H](Hardware-Tinkerman-ESPurna-H) | `TINKERMAN_ESPURNA_H06` <br> `TINKERMAN_ESPURNA_H08` | |
| Tinkerman's ESPurna Switch | `TINKERMAN_ESPURNA_SWITCH` | |
| [ManCaveMade ESPLive](Hardware-ManCaveMade-ESPLive) | `MANCAVEMADE_ESPLIVE` | |
| [Electrodragon ESP Relay Board](Hardware-Electrodragon-ESP-Relay-Board) | `ELECTRODRAGON_WIFI_IOT` | |
| [WorkChoice EcoPlug](Hardware-WorkChoice-EcoPlug) | `WORKCHOICE_ECOPLUG` | |
| [Jan Goedeke Wifi Relay Board (NC/NO)](Hardware-Jan-Goedeke-Wifi-Relay-Board) | `JANGOE_WIFI_RELAY_NC` <br> `JANGOE_WIFI_RELAY_NO` | |
| [OpenEnergyMonitor Wifi MQTT Relay / Thermostat](Hardware-OpenEnergyMonitor-Wifi-MQTT-Relay) | `OPENENERGYMONITOR_MQTT_RELAY` | |
| [Jorge García Wifi + Relay Board Kit](Hardware-Jorge-Garcia-Wifi-Relay-Board) | `JORGEGARCIA_WIFI_RELAYS` | |
| [EXS WiFi Relay v3.1](Hardware-EXS-WiFi-Relay-v3.1) | `EXS_WIFI_RELAY_V31` | |
| [IKE ESPike](Hardware-IKE-ESPike) | `IKE_ESPIKE` | |
| [Arniex Swifitch](Hardware-Arniex-Swifitch) | `ARNIEX_SWIFITCH` | |
| [Luani HVIO (original in german)](https://luani.de/projekte/esp8266-hvio/) <br> [google translation (english)](https://translate.google.com/translate?sl=auto&tl=en&js=y&prev=_t&hl=en&ie=UTF-8&u=https%3A%2F%2Fluani.de%2Fprojekte%2Fesp8266-hvio%2F&edit-text=&act=url)| `LUANI_HVIO` | |

## Generic boards

| Board | Build flag | Description |
| --- | --- | --- |
| Generic 8 Channel board | `GENERIC_8CH` | |
| [Generic ECH1560](Hardware-Generic-ECH1560) | `GENERIC_ECH1560` | |
| [Generic V9261F](Hardware-Generic-V9261F) | `GENERIC_V9261F` | |
| [Green ESP8266 Relay](Hardware-Green-ESP8266-Relay) | `GREEN_ESP8266RELAY` | |
| [Generic Relay v4.0](Hardware-Generic-Relay-v40) | `GENERIC_ESP01S_RELAY_V40` | |
| [Generic RGBLed v1.0](Hardware-Generic-RGBLed-v10) | `GENERIC_ESP01S_RGBLED_V10` | |
| [Generic DHT11 v1.0](Hardware-Generic-DHT11-v10) | `GENERIC_ESP01S_DHT11_V10` | |
| [Generic DS18B20 v1.0](Hardware-Generic-DS18B20-v10) | `GENERIC_ESP01S_DS18B20_V10` | |
| [Heltec Touch Relay](Hardware-Heltec-Touch-Relay) | `HELTEC_TOUCHRELAY` | |

## Beta Testing

| Board | Build flag | Description |
| --- | --- | --- |
| Gosund/Homecube SP1 | |

## Community boards

| Board | Build flag | Description |
| --- | --- | --- |
| Let us know | about devices | you've built |