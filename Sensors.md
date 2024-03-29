This page describes various sensors supported by ESPurna. 

To enable particular sensor in firmware, you should build the firmware with appropriate build flags (`-D`) set to `1`. The table below lists all supported build flags. Some sensors have additional options, so please check additional information below.

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

| | |
|--- | --- |
| **Common Sensors** | Build flag | 
| [Analog sensors](#analog-sensors) | `ANALOG_SUPPORT` | 
| [Generic digital sensor](#generic-digital-sensor) | `DIGITAL_SUPPORT` |
| [I2C Bus](#i2c-bus) | `I2C_SUPPORT` | 
| **Power Meter Sensors** | | 
| [Analog energy monitor](#analog-energy-monitor) | `EMON_ANALOG_SUPPORT` |
| [ADC121 Energy monitor](#adc121-energy-monitor) | `EMON_ADC121_SUPPORT` | 
| [ADS1x15 Energy monitor](#ads1x15-energy-monitor) | `EMON_ADS1X15_SUPPORT` | 
| [ECH1560 based power sensor](#ech1560-based-power-sensor)| `ECH1560_SUPPORT` | 
| [HLW8012 Energy monitor IC](#hlw8012-energy-monitor-ic) | `HLW8012_SUPPORT` |
| [PZEM004T based power monitor](#pzem004t-based-power-monitor) |`PZEM004T` |
| [V9261F based power sensor](#v9261f-based-power-sensor) | `V9261F_SUPPORT` | 
| **Temperature and/or Humidity Sensors** | |
| [BME280/BMP280 environmental sensor](#bme280bmp280-environmental-sensor) | `BMX280_SUPPORT` | 
| [Dallas 1-Wire sensors](#dallas-1-wire-sensors) | `DALLAS_SUPPORT` | 
| [DHT environmental sensors](#dht-environmental-sensors) | `DHT_SUPPORT` | 
| [SHT3X environmental sensor](#sht3x-environmental-sensor) | `SHT3X_I2C_SUPPORT` | 
| [SI7021 environmental sensor](#si7021-environmental-sensor) | `SI7021_SUPPORT` | 
| **Air Quality Sensors** | | 
| [MHZ19 CO2 sensor](#mhz19-co2-sensor) | `MHZ19_SUPPORT` | 
| [Particle Monitor based on Plantower PMSX003](#particle-monitor-based-on-plantower-pmsx003) | `PMSX003_SUPPORT` | 
| **Light Sensors** | |
| [BH1750 Digital light sensor](#bh1750-digital-light-sensor) | `BH1750_SUPPORT` |
| **Other** | |
| [Counter sensor](#counter-sensor) | `EVENTS_SUPPORT` | 

---

## Analog sensors

This will enable support for Analog sensors, connected on ADC pin.

| Option | Note | 
| --- | --- | 
| `ADC_VCC_ENABLED={0,1}` | |

---

## Generic digital sensor

This will enable generic digital input sensor (switch or a pushbutton).

| Option | Note | 
| --- | --- | 
|  `DIGITAL_PIN={0-15}` | GPIO to use (default: `2`) |
| `DIGITAL_PIN_MODE` | Initial GPIO status. One of: <br> - `INPUT_PULLUP` (default) <br> - `INPUT` |
| `DIGITAL_DEFAULT_STATE` | Default state on boot (default: `1` / on / high) | 

---

## I2C Bus

Enable generic I2C bus support. It will be automatically enab;ed if any sensor that requires it is also enabled, but you might want to choose non-default ports.

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

Note: Will automatically enable I2C. 

---

## BME280/BMP280 environmental sensor

This will enable support for BME280 or BMP280 humidity, temperature and pressure sensors.

| Option | Note | 
| --- | --- |
| `BMX280_ADDRESS={0x00-0xFF}` | Default is 0x00 (auto) |

Note: Will automatically enable I2C. 

---

## Dallas 1-Wire sensors

These are sensors like the DS18B20.

| Option | Note | 
| --- | --- |
| `DALLAS_PIN={0-15}` | GPIO where 1-Wire will be enabled | 

All sensors discovered on a 1-Wire bus will be reported.

Troubleshooting (thanks to @AlberWeterings):

As most of you know on aliexpress many cheap DS18B20 sensors are sold and a lot of them are (counterfeit) fake. I have got myself a lot of them. Having that said I will sum up some problems you might run into using these sensors on ESPURNA.

* A Sonoff TH10 has internally two 10K resistors in parallel from VCC 3v3 to IO pin 14 resulting in a 5K resistance. So if you use a genuine or fake sensor no 4K7 resistor is needed.
* If you connect a fake sensor for example to a Sonoff TH10 and you use a resistor of 4k7 from VCC to DO you will see the temperature rising over time this is due to the sensor heating up its self rapidly. The 4k7 resistor makes it worse.
* Most Fake sensors also heat up with the Sonoff's internal resistance of 5K
* Replacing the internal two 10K resistors with one 50K resistor stops the rapid heating up. but measurement is still inaccurate.
* If you have your fake DS18B20 mounted on a surface or floating in a fluid it will not heat up rapidly anymore but still is giving inaccurate measurements as it is heating its self internally.

I was unable to find a setup in which the fake sensors where measuring accurate so my advise if you ever have issues with these type of sensors compare it to a sensor that is known genuine.

---

## DHT environmental sensors

| Option | Note | 
| --- | --- |
| `DHT_PIN={0-15}` | GPIO where DHT sensors are connected |
| `DHT_TYPE=<type>` | One of the: <br> - `DHT_CHIP_DHT11` <br> - `DHT_CHIP_DHT21` <br> - `DHT_CHIP_DHT22` (default) |

---

## ECH1560 based power sensor

| Option | Note | 
| --- | --- |
| `ECH1560_CLK_PIN={0,15}` | GPIO where ECH1560 CLK is connected (default: `4`)|
| `ECH1560_MISO_PIN={0,15}` | GPIO where ECH1560 MISO is connected (default: `5`) |
| `ECH1560_INVERTED={0,1}` | Is signal inverted (default: `0` - no) |

---

## ADC121 Energy monitor

| Option | Note | 
| --- | --- |
| `EMON_ADC121_I2C_ADDRESS={0x00-0xFF}` | I2C address of ADC121 sensor (default: `0x00` - auto) | 

Note: Will automatically enable I2C. 

---

## ADS1x15 Energy monitor

| Option | Note | 
| --- | --- |
| `EMON_ADS1X15_I2C_ADDRESS={0x00-0xFF}` | I2C address of ADS1x15 sensor (default: `0x00` - auto) |

Note: Will automatically enable I2C. 

---

## Analog energy monitor

Energy Monitor based on interval analog GPIO.

| Option | Note | 
| --- | --- |

---

## Counter sensor

| Option | Note | 
| --- | --- |
| `EVENTS_PIN={0,15}` | GPIO to monitor for pulses (default: `2`) |
| `EVENTS_PIN_MODE` | Initial GPIO status. One of: <br> - `INPUT_PULLUP` <br> - `INPUT` (default) |
| `EVENTS_INTERRUPT_MODE` | On which signal transition to react. One of: <br> - `RISING` (default) <br> - `FALLING` <br> - `BOTH` |

---

## HLW8012 Energy monitor IC

| Option | Note | 
| --- | --- |
| `HLW8012_SEL_PIN={0,15}` | GPIO where SEL is connected (default: `5`) |
| `HLW8012_CF1_PIN={0,15}` | GPIO where CF1 is connected (default: `5`) |
| `HLW8012_CF_PIN={0,15}`  | GPIO where CF is connected (default: `5`) |
| `HLW8012_SEL_CURRENT`    | SEL pin transition to start measuring. One of: <br> - `HIGH` (default) <br> - `LOW` |
| `HLW8012_CURRENT_R=<n>`  | Current resistor, default: `0.001` |
| `HLW8012_VOLTAGE_R_UP`   | Upstream voltage resistor, default: `( 5 * 470000 )` |
| `HLW8012_VOLTAGE_R_DOWN` | Downstream voltage resistor, default: `( 1000 )` |

Notice: some people have reported issues when using HLW8012 with SSL (see #1248).

---

## MHZ19 CO2 sensor

| Option | Note | 
| --- | --- |
| `MHZ19_RX_PIN` | GPIO where RX is connected (default: `13`) |
| `MHZ19_TX_PIN` | GPIO where TX is connected (default: `15`) |

---

## Particle Monitor based on Plantower PMSX003

| Option | Note | 
| --- | --- |
| `PMS_RX_PIN` | GPIO where RX is connected (default: `13`) |
| `PMS_TX_PIN` | GPIO where TX is connected (default: `15`) |

---

## SHT3X environmental sensor

| Option | Note | 
| --- | --- |
| `SHT3X_I2C_ADDRESS={0x00-0xFF}` | I2C address of SXT3X sensor (default: `0x00` - auto) | 

Note: This will enable I2C.

---

## SI7021 environmental sensor

| Option | Note | 
| --- | --- |
| `SI7021_ADDRESS={0x00-0xFF}` | I2C address of SI7021 sensor (default: `0x00` - auto) | 

Note: This will enable I2C.

---

## V9261F based power sensor

| Option | Note | 
| --- | --- |
| `V9261F_PIN={0,15}`  | GPIO where V9261 is connected (default: `2`) |
| `V9261F_PIN_INVERSE` | Is signal inverted? (default: `1` - inverted signal) |

---

## PZEM004T based power monitor

| Option | Note | 
| --- | --- |
| `PZEM004T_RX_PIN` | GPIO where RX is connected (default: `13`) |
| `PZEM004T_TX_PIN` | GPIO where TX is connected (default: `15`) |
| `PZEM004T_HW_PORT` | Hardware serial port (if PZEM004T_USE_SOFT == 0) (default: `Serial1`) |
| `PZEM004T_ADDRESSES` | Connected devices addresses (default: `192.168.1.1`) |
| `PZEM004T_READ_INTERVAL` | Read interval between the same device in the bus (default: `1500`) |
| `PZEM004T_MAX_DEVICES` | Maximum number of devices on the pseudo-bus (default: `3`) |

See Wiki page for more details: [PZEM004t Energy Monitor](https://github.com/xoseperez/espurna/wiki/Sensor-PZEM004T)
