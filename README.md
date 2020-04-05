# micropython-bmp280

https://www.adafruit.com/product/2651
https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/pressure-sensors-bmp280-1.html
https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmp280-ds001.pdf

Inspired by  
https://github.com/vitally/BMP280  
https://github.com/micropython-IMU/micropython-bmp180

## Constructor
**BMP280(i2c_bus, addr=0x76, use_case=BMP280_CASE_HANDHELD_DYN)**
* *i2c_bus* - the I2C bus to use
* *addr* - I2C address of the BMP280 (always the same)
* *use_case* - Use case to start the BMP280 with. Set to None to disable measuring on boot.

## Enums
Values for different settings are defined in the following constants
### Use cases (See 3.4, 3.8.2)
* BMP280_CASE_HANDHELD_LOW
* BMP280_CASE_HANDHELD_DYN (*default*)
* BMP280_CASE_WEATHER
* BMP280_CASE_FLOOR
* BMP280_CASE_DROP
* BMP280_CASE_INDOOR
### Oversampling setting (See 3.3.1, 3.8.2)
* BMP280_OS_ULTRALOW
* BMP280_OS_LOW
* BMP280_OS_STANDARD
* BMP280_OS_HIGH
* BMP280_OS_ULTRAHIGH
### Pressure oversampling (See 3.3.1)
* BMP280_PRES_OS_SKIP
* BMP280_PRES_OS_1
* BMP280_PRES_OS_2
* BMP280_PRES_OS_4
* BMP280_PRES_OS_8
* BMP280_PRES_OS_16
### Temperature oversampling (See 3.3.2)
* BMP280_TEMP_OS_SKIP
* BMP280_TEMP_OS_1
* BMP280_TEMP_OS_2
* BMP280_TEMP_OS_4
* BMP280_TEMP_OS_8
* BMP280_TEMP_OS_16
### IIR filter (See 3.3.3)
* BMP280_IIR_FILTER_OFF
* BMP280_IIR_FILTER_2
* BMP280_IIR_FILTER_4
* BMP280_IIR_FILTER_8
* BMP280_IIR_FILTER_16
### Standby settings for Normal measure (See 3.6.3)
* BMP280_STANDBY_0_5
* BMP280_STANDBY_62_5
* BMP280_STANDBY_125
* BMP280_STANDBY_250
* BMP280_STANDBY_500
* BMP280_STANDBY_1000
* BMP280_STANDBY_2000
* BMP280_STANDBY_4000
### Power modes
* BMP280_POWER_SLEEP
* BMP280_POWER_FORCED
* BMP280_POWER_NORMAL
### SPI 3-wire select
* BMP280_SPI3W_ON
* BMP280_SPI3W_OFF

## Example
```python
from machine import I2C
from bmp280 import BMP280

bus = I2C()
bmp = BMP280(bus)

bmp.use_case(BMP280_CASE_WEATHER)
bmp.oversample(BMP280_OS_HIGH)

bmp.temp_os = BMP280_TEMP_OS_8
bmp.press_os = BMP280_PRES_OS_4

bmp.standby = BMP280_STANDBY_250
bmp.iir = BMP280_IIR_FILTER_2

bmp.spi3w = BMP280_SPI3W_ON

bmp.power_mode = BMP280_POWER_FORCED
# or 
bmp.force_measure()

bmp.power_mode = BMP280_POWER_NORMAL
# or 
bmp.normal_measure()
# also
bmp.in_normal_mode()

bmp.power_mode = BMP280_POWER_SLEEP
# or 
bmp.sleep()

print(bmp.temperature)
print(bmp.pressure)

#True while measuring
bmp.is_measuring

#True while copying data to registers
bmp.is_updating

```

## TODO
* SPI support
* ~~Filters~~
* ~~Oversampling settings (half done)~~
* ~~Power modes~~
* ~~Standby setting for Normal mode~~
