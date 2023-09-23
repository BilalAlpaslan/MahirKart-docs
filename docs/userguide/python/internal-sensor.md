# Dahili Sensör Kullanımı

## MahirKart Dahili Sensörler

MahirKart üzerinde bulunan BME280 ve MPU6050 dahili sensörlerinden sıcaklık, nem, basınç, 3 eksende ivme ve jiroskop verilerini alabilirsiniz.

Verileri okumak için bu sensörler için yazılmış kütüphaneleri kullanabilirsiniz. MahirKart'ın dahili sensörlerini en verimli şekilde kullanmak için [MahirKart Python Kütüphanesi](https://github.com/BilalAlpaslan/mahirkart-lib/blob/main/mahirkart.py)ni kullanmanızı öneririz.


## MahirKart Python Kütüphanesi ile Dahili Sensör Kullanımı

Kütüphaneyi ismini değitirmeden aynı klasöre indirin ve şu şekilde MahirSensor sınıfını import edin:

``` python
from mahirkart import MahirSensor
```

MahirSensor sınıfı ile sensörlerden veri okumak için şu şekilde bir nesne oluşturun:

``` python
sensor = MahirSensor()
```

Oluşturduğunuz nesne ile sensörlerden veri okumak için şu şekilde fonksiyonları kullanabilirsiniz:

``` python
sensor.read() # Bütün sensörlerden veri okur.
sensor.read_bme280() # Sadece BME280 sensöründen veri okur.
sensor.read_mpu6050() # Sadece MPU6050 sensöründen veri okur.
```

Sonrasında okunan verileri şu şekilde kullanabilirsiniz:

``` python
sensor.accel_x # MPU6050 sensöründen okunan x eksenindeki ivme değeri.
sensor.accel_y # MPU6050 sensöründen okunan y eksenindeki ivme değeri.
sensor.accel_z # MPU6050 sensöründen okunan z eksenindeki ivme değeri.
sensor.gyro_x # MPU6050 sensöründen okunan x eksenindeki jiroskop değeri.
sensor.gyro_y # MPU6050 sensöründen okunan y eksenindeki jiroskop değeri.
sensor.gyro_z # MPU6050 sensöründen okunan z eksenindeki jiroskop değeri.
sensor.angle_x # MPU6050 sensöründen okunan x eksenindeki açı değeri.
sensor.angle_y # MPU6050 sensöründen okunan y eksenindeki açı değeri.
sensor.angle_z # MPU6050 sensöründen okunan z eksenindeki açı değeri.
sensor.mpu_temp # MPU6050 sensöründen okunan sıcaklık değeri.
sensor.temp # BME280 sensöründen okunan sıcaklık değeri.
sensor.press # BME280 sensöründen okunan basınç değeri.
sensor.hum # BME280 sensöründen okunan nem değeri.
```

ek calibrasyon yapmak için şu fonksiyonu kullanabilirsiniz:

``` python
sensor.calibrate_mpu6050(accel_bias: list, gyro_bias: list) # MPU6050 sensörünü calibrasyon yapar.
```

## MahirKart Python Kütüphanesi ile Dahili Sensör Kullanımı Örneği

Bu örneğimizde MahirKart'ın dahili sensörlerinden okuduğumuz verileri ekrana yazdıracağız.

``` python
from mahirkart import MahirSensor
import time

sensor = MahirSensor()


while True:
    sensor.read()
    print(sensor.accel_x, sensor.accel_y, sensor.accel_z, sensor.gyro_x, sensor.gyro_y, sensor.gyro_z, sensor.angle_x, sensor.angle_y, sensor.angle_z, sensor.mpu_temp, sensor.temp, sensor.press, sensor.hum)
    time.sleep(0.2)
```