This page describes various sensors supported by ESPurna. 

To enable particular sensor in firmware, you should build the firmware with appropriate build flags. Below table is listing all supported build flags, together with their parameters. 

In most of the cases, just setting a build flag will do the trick - most sensors have default options for auto-detecting sensor parameters or using most widelly used values. Still, you have full control, so feel free to customize.

For example, to enable DHT sensor support on GPIO14, you should set: 
```ini 
[env:your-board-name]
...
build_flags = ${common.build_flags_1m} -DDHT_SUPPORT=1 -DDHT_PIN=14
...
```


| Sensor | Build flag | Build options | Note | 
|--- | --- | --- | --- | 
| Analog sensors | `ANALOG_SUPPORT={0,1}` | `ADC_VCC_ENABLED={0,1}` | |
| I2C Bus | `I2C_SUPPORT={0,1}` | `I2C_SDA_PIN={0,15}` <Br> `I2C_SCL_PIN={0,15}` | Support fill be enabled as soon as any of the I2C dependent sensors is enabled. Default GPIOs are 4(SDA) and 14(SCL). | 
| BH1750 Digital light sensor | `BH1750_SUPPORT={0,1}` | `BH1750_ADDRESS={0x00-0xFF}` <br> `BH1750_MODE` | You can lookup modes in [library source](https://github.com/claws/BH1750). Default is "continuous, high res" |
| BME280/BMP280 environmental sensor | `BMX280_SUPPORT` | `BMX280_ADDRESS={0x00-0xFF}` <br> `BMX280_MODE={0-3}` <br> `BMX280_STANDBY={0-5}` <br> `BMX280_FILTER={0-4}` <br> `BMX280_TEMPERATURE={0,1}` <br> `BMX280_HUMIDITY={0,1}` <br> `BMX280_PRESSURE={0,1}` | | 
| Dallas 1-Wire sensors | `DALLAS_SUPPORT={0,1}` | `DALLAS_PIN={0-15}` | Be careful not to override any of the used pins | 
| DHT environmental sensors | `DHT_SUPPORT={0,1}` | `DHT_PIN={0-15}` <Br> `DHT_TYPE=<type>` | |
| | `DIGITAL_SUPPORT={0,1}` | `DIGITAL_PIN={0-15}` <br> `DIGITAL_PIN_MODE` <br> `DIGITAL_DEFAULT_STATE` | | 
| | `ECH1560_SUPPORT={0,1}` | `ECH1560_CLK_PIN={0,15}` <Br> `ECH1560_MISO_PIN={0,15}` <br> `ECH1560_INVERTED={0,1}` | |
| ADC121 Energy monitor | `EMON_ADC121_SUPPORT={0,1}` | `EMON_ADC121_I2C_ADDRESS={0x00-0xFF}` | | 
| ADS1x15 Energy monitor | `EMON_ADS1X15_SUPPORT={0,1}` | `EMON_ADS1X15_I2C_ADDRESS={0x00-0xFF}` <br> `EMON_ADS1X15_TYPE` <br> `EMON_ADS1X15_GAIN` <br> `EMON_ADS1X15_MASK` ||
| | `EMON_ANALOG_SUPPORT={0,1}` || 
|| `EVENTS_SUPPORT={0,1}` | `EVENTS_PIN={0,15}` <br> `EVENTS_PIN_MODE` <br> `EVENTS_INTERRUPT_MODE` | |
|| `HLW8012_SUPPORT={0,1}` | `HLW8012_SEL_PIN={0,15}` <br> `HLW8012_CF1_PIN={0,15}` <Br> `HLW8012_CF_PIN={0,15}` <br> `HLW8012_SEL_CURRENT` <Br> `HLW8012_CURRENT_R` <br> `HLW8012_VOLTAGE_R_UP` <br> `HLW8012_VOLTAGE_R_DOWN` ||
|| `MHZ19_SUPPORT={0,1}` | `MHZ19_TX_PIN={0,15}` | |
|| `PMSX003_SUPPORT={0,1}` | `PMS_RX_PIN={0,15}` <br> `PMS_TX_PIN={0,15}` ||
|| `SHT3X_I2C_SUPPORT={0,1}` | `SHT3X_I2C_ADDRESS` || 
|| `SI7021_SUPPORT={0,1}` | `SI7021_ADDRESS` ||
|| `V9261F_SUPPORT={0,1}` | `V9261F_PIN={0,15}` <br> `V9261F_PIN_INVERSE` ||






 