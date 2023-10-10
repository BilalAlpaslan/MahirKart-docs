# I2C

## I2C Protokolü

I2C(Inter-Integrated Circuit) protokolü, Master ve Slave(İşçi) olan iki cihaz arasında seri haberleşme sağlayan bir protokoldür. I2C protokolü, veri gönderme ve alma işlemlerini gerçekleştirmek için iki adet veri hattı(SDA ve SCL) kullanır. Adresleme yaparak birden fazla(100+) Slave cihazı tek bir Master cihaz üzerinden kontrol edilebilmektedir. Kontrol edilecek cihaz sayısı artarken hat sayısı artmamaktadır. Birden fazla cihaz sadece SCL ve SDA pinleriyle kontrol edilebilmektedir.

Bu protokolü donanımsal olarak kullanabileceğiniz gibi yazılımsal olarak da oluşturabilirsiniz ama yazılımsal olarak kullanmanız işlemciniz için ek bir yük oluşturacaktır. Bu yüzden donanımsal olarak kullanmanızı tavsiye ederiz.

## MahirKart ile I2C

MahirKart üzerinde birden fazla pin seçeneğiyle kullanabileceğiniz iki adet donanımsal I2C bulunmaktadır. MahirKart'ın I2C pinlerini [Pinout](../../pinout.md) sayfasından öğrenebilirsiniz.

## Arduino ile I2C Kullanımı örneği

Bu örnekte MahirKartın I2C hattındaki bağlı sensörleri tarayacağız. İsterseniz ek sensörler bağlayarak deneyebilirsiniz. Zaten MahirKart'ın üzerinde bulunan dahili iki adet sensör bulunmaktadır(BME280 ve MPU6050). Bu sensörlerin adreslerini görüntüleyelim.

``` c
#include <Wire.h>

void setup() {
  Wire.begin();
  Serial.begin(9600);
  Serial.println("I2C Cihazları Taranıyor...");
}

void loop() {
  byte error, address;
  int nDevices;

  Serial.println("Tarama Başlıyor...");
  nDevices = 0;
  for (address = 1; address < 127; address++ ) {
    Wire.beginTransmission(address);
    error = Wire.endTransmission();

    if (error == 0) {
      Serial.print("Cihaz Bulundu! Adres: 0x");
      if (address < 16)
        Serial.print("0");
      Serial.print(address, HEX);
      Serial.println("");

      nDevices++;
    } else if (error == 4) {
      Serial.print("0x adresinde bilinmeyen hata");
      if (address < 16)
        Serial.print("0");
      Serial.println(address, HEX);
    }
  }
  if (nDevices == 0)
    Serial.println("I2C Cihazı Bulunamadı!");
  else
    Serial.println("Tarama Tamamlandı!");

  delay(5000); // 5 saniyede bir tarama yap
}

```

Eğer fazladan sensör takmadıysanız bu kodu çalıştırdığınızda 2 adet I2C adresi bulunduğunu göreceksiniz. Bu çıktıda gördüğünüz 0x68, adresi MPU6050 sensörünün adresidir. 0x76 adresi ise BME280 sensörünün adresidir. Bu adreslerin ne olduğunu öğrenmek için sensörlerin datasheet'lerine bakabilirsiniz.

Eğer aklınızda kalan sorular varsa [Discord](https://discord.com/invite/YVc68SrGJK) sunucumuz üzerinden sorabilirsiniz.