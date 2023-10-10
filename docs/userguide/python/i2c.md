# I2C

## I2C Protokolü

I2C protokolü, Master ve Slave(İşçi) iki cihaz arasında seri haberleşme sağlayan bir protokoldür. I2C protokolü, veri gönderme ve alma işlemlerini gerçekleştirmek için iki adet veri hattı(SDA ve SCL) kullanır. Adresleme yaparak birden fazla(100+) Slave cihazı tek bir Master cihaz üzerinden kontrol edebilirsiniz. 

Bu protokolü donanımsal olarak kullanabileceğiniz gibi yazılimsal olarak da oluşturabilirsiniz ama yazılımsal olarak kullanmanız işlemciniz için ek bir yük oluşturacaktır. Bu yüzden donanımsal olarak kullanmanızı tavsiye ederiz.

## MahirKart ile I2C

MahirKart üzerinde birden fazla pin seçeneğiyle kullanabileceğiniz iki adet donanımsal I2C bulunmaktadır. MahirKart'ın I2C pinlerini [Pinout](../../pinout.md) sayfasından öğrenebilirsiniz.

## Python ile I2C Kullanımı örneği

Bu örnekte MahirKartın I2C0 hattındaki bağlı sensörleri tarayacağız. İsterseniz ek sensörler bağlayarak deneyebilirsiniz. Zaten MahirKart'ın üzerinde bulunan dahili iki adet sensör var(BME280 ve MPU6050). Bu sensörlerin adreslerini görüntüleyelim.

``` python
from machine import Pin

i2c= machine.I2C(0,sda=Pin(20), scl=Pin(21))

cihazlar = i2c.scan()

if len(cihazlar) == 0:
    print("i2c adres bulunamadı !")
else:
    print(len(cihazlar),' adet i2c adres bulundu:')

for cihaz in cihazlar:
    print("Decimal adres: ",cihaz," | Hex adres: ",hex(cihaz))
```

Eğer fazladan sensör takmadıysanız bu kodu çalıştırdığınızda çıktı olarak şöyle birşey göreceksiniz:

```
2  adet i2c adres bulundu:
Decimal adres:  104  | Hex adres:  0x68
Decimal adres:  118  | Hex adres:  0x76
```

Bu çıktıda 0x68 ve 0x76 adreslerini görebilirsiniz. Bu adreslerden 0x68 adresi MPU6050 sensörünün adresidir. 0x76 adresi ise BME280 sensörünün adresidir. Bu adreslerin ne olduğunu öğrenmek için sensörlerin datasheet'lerine bakabilirsiniz.

Eğer aklınızda kalan sorular varsa [Discord](https://discord.com/invite/YVc68SrGJK) sunucumuz üzerinden sorabilirsiniz.