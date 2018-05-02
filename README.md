# micropython-bmp280

https://www.adafruit.com/product/2651

From  
https://github.com/vitally/BMP280  
https://github.com/micropython-IMU/micropython-bmp180

## Example
```python
from machine import I2C
from bmp280 import BMP280

bus = I2C()
bmp = BMP280(bus)

print(bmp.temperature)
print(bmp.pressure)

```

## TODO
* SPI support
* Filters
* Oversampling settings (half done)
* Power modes
* Standby setting for Normal mode
