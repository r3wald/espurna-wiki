This page describes various sensors supported by ESPurna. 

To enable particular sensor in firmware, you should build the firmware with appropriate build flags set to `1`. Below table is listing all supported build flags. Some sensors have additional options, so please check additional information below.

In most of the cases, just setting a build flag to `1` will do the trick - most sensors have default options for auto-detecting sensor parameters or using most widely used values. Still, you have full control, so feel free to customize.

For example, to enable DHT sensor support on GPIO14, you should set: 
```ini 
[env:your-board-name]
...
build_flags = ${common.build_flags_1m} -DDHT_SUPPORT=1 -DDHT_PIN=14
...
```

> When setting GPIO assignments, be careful not to override any of the GPIO used for flash - this would normally render your board unresponsive and you would need to re-flash it using USB programmer, which is not always convenient.

# Sensors

| Sensor | Build flag | 
|--- | --- |  
| [Analog sensors](#Analog-sensors) | `ANALOG_SUPPORT` | 
| [Generic digital sensor](#Generic-digital-sensor) | `DIGITAL_SUPPORT` |
| [I2C Bus](#I2C-Bus) | `I2C_SUPPORT` | 
| [BH1750 Digital light sensor](#BH1750-Digital-light-sensor) | `BH1750_SUPPORT` | 
| [BME280/BMP280 environmental sensor](#BME280/BMP280-environmental-sensor) | `BMX280_SUPPORT` | 
| [Dallas 1-Wire sensors](#Dallas-1-Wire-sensors) | `DALLAS_SUPPORT` | 
| [DHT environmental sensors](#DHT-environmental-sensors) | `DHT_SUPPORT` | 
| [ECH1560 based power sensor](#ECH1560-based-power-sensor)| `ECH1560_SUPPORT` | 
| [ADC121 Energy monitor](#ADC121-Energy-monitor) | `EMON_ADC121_SUPPORT` | 
| [ADS1x15 Energy monitor](#ADS1x15-Energy-monitor) | `EMON_ADS1X15_SUPPORT` | 
| | `EMON_ANALOG_SUPPORT={0,1}` || 
|| `EVENTS_SUPPORT={0,1}` | `EVENTS_PIN={0,15}` <br> `EVENTS_PIN_MODE` <br> `EVENTS_INTERRUPT_MODE` | |
|| `HLW8012_SUPPORT={0,1}` | `HLW8012_SEL_PIN={0,15}` <br> `HLW8012_CF1_PIN={0,15}` <Br> `HLW8012_CF_PIN={0,15}` <br> `HLW8012_SEL_CURRENT` <Br> `HLW8012_CURRENT_R` <br> `HLW8012_VOLTAGE_R_UP` <br> `HLW8012_VOLTAGE_R_DOWN` ||
|| `MHZ19_SUPPORT={0,1}` | `MHZ19_TX_PIN={0,15}` | |
|| `PMSX003_SUPPORT={0,1}` | `PMS_RX_PIN={0,15}` <br> `PMS_TX_PIN={0,15}` ||
|| `SHT3X_I2C_SUPPORT={0,1}` | `SHT3X_I2C_ADDRESS` || 
|| `SI7021_SUPPORT={0,1}` | `SI7021_ADDRESS` ||
|| `V9261F_SUPPORT={0,1}` | `V9261F_PIN={0,15}` <br> `V9261F_PIN_INVERSE` ||

---

## Analog sensors

This will enable support for Analog sensors, connected on ADC pin.

| Option | Note | 
| --- | --- | 
| `ADC_VCC_ENABLED={0,1}` | |

---

## Generic digital sensor

This will enable generic digital input sensor. ESPurna will report status

| Option | Note | 
| --- | --- | 
|  `DIGITAL_PIN={0-15}` | GPIO to use (default: `2`) |
| `DIGITAL_PIN_MODE` | Initial GPIO status. One of: <br> `INPUT_PULLUP` (default)|
| `DIGITAL_DEFAULT_STATE` | Default state on boot (default: `1` / on / high) | 

---


## I2C Bus

Enable generic I2C bus support. It will automatically if any sensor that requires it is also enabled, but you might want to choose non-default ports.

| Option | Note | 
| --- | --- | 
| `I2C_SDA_PIN={0,16}` | GPIO where SDA line is connected (default: `4`) |
| `I2C_SCL_PIN={0,16}` | GPIO where SCL line is connected (default: `14`) |

--- 

## BH1750 Digital light sensor

This enables support for digital light sensor based on BH1750, such as [this one](https://www.aliexpress.com/item/Free-shipping-GY-302-BH1750-BH1750FVI-Chip-Light-Intensity-Light-Module/1872367675.html) , or [this one](https://www.ebay.com/itm/BH1750FVI-Digital-Light-intensity-Sensor-Module-For-AVR-Arduino-3V-5V-power-new/400985344400).

Datasheet for the sensor itself is [here](http://www.elechouse.com/elechouse/images/product/Digital%20light%20Sensor/bh1750fvi-e.pdf)

| Option | Note | 
| --- | --- |
| `BH1750_ADDRESS={0x00-0xFF}` | I2C address of BH1750 sensor. Default 0x00 (auto) |
| `BH1750_MODE` | One of: <br> `BH1750_CONTINUOUS_LOW_RES_MODE` <br> `BH1750_CONTINUOUS_HIGH_RES_MODE` (default) <br> `BH1750_CONTINUOUS_HIGH_RES_MODE2`   |

Note: Will automatically enable I2C. 

---

## BME280/BMP280 environmental sensor

This will enable support for BME280 or BMP280 humidity, temperature and pressure sensors.

| Option | Note | 
| --- | --- |
| `BMX280_ADDRESS={0x00-0xFF}` | Default is 0x00 (auto) |
| `BMX280_MODE={0-3}` | One of: <br> `0` - sleep mode, <br> `1` or `2` - forced mode (default) <br> `3` - normal mode |
| `BMX280_STANDBY={0-7}` | One of: <br> `0` - 0.5ms (default), <br> `1` - 62.5ms, <br> `2` - 125ms <br> `3` - 250ms, <br> `4` - 500ms, <br> `5` - 1s <br> `6` - 10s <br> `7` - 20s |
| `BMX280_FILTER={0-4}` ||
| `BMX280_TEMPERATURE={0,1}` ||
| `BMX280_HUMIDITY={0,1}` ||
| `BMX280_PRESSURE={0,1}` || 
 
Note: Will automatically enable I2C. 

---

## Dallas 1-Wire sensors

| Option | Note | 
| --- | --- |
`DALLAS_PIN={0-15}` | | 

---

## DHT environmental sensors

| Option | Note | 
| --- | --- |
| `DHT_PIN={0-15}` ||
| `DHT_TYPE=<type>` | One of the: <br> |

---

## ECH1560 based power sensor

| Option | Note | 
| --- | --- |
| `ECH1560_CLK_PIN={0,15}` ||
| `ECH1560_MISO_PIN={0,15}` ||
| `ECH1560_INVERTED={0,1}` | |

---

## ADC121 Energy monitor

| Option | Note | 
| --- | --- |
| `EMON_ADC121_I2C_ADDRESS={0x00-0xFF}` | I2C address of ADC121 sensor (default: `0x00` - auto) | 

---

## ADS1x15 Energy monitor

| Option | Note | 
| --- | --- |
| `EMON_ADS1X15_I2C_ADDRESS={0x00-0xFF}` ||
| `EMON_ADS1X15_TYPE` ||
| `EMON_ADS1X15_GAIN` ||
| `EMON_ADS1X15_MASK` ||



