# Dijital Giriş/Çıkış (GPIO)

## MahirKart ve Dijital Giriş/Çıkış (GPIO)

MahirKart'da dijital giriş ve çıkışlar (Digital Input/Output - GPIO) olarak bilinen pinleri bulunur. Dijital girişler, 0 ("LOW") veya 1 ("HIGH) olarak okunabilen iki durumlu sinyalleri alır. Dijital çıkışlar, 0 ("LOW") veya 1 ("HIGH) olarak ayarlanabilen iki durumlu sinyaller üretir.

## Dijital Çıkış (Digital Output)

Dijital çıkış pinleri, genellikle LED'ler ve röleler gibi aktüatörleri kontrol etmek için kullanılır. MahirKart üzerindeki dijital çıkış pinleri de "HIGH" ve "LOW" olmak üzere iki duruma sahiptir. "HIGH" durumunda pin 3.3V seviyesine çıkartılırken, "LOW" durumunda 0V seviyesine çekilir.

Örneğin, bir LED'i MahirKart ile kontrol etmek için LED'i bir direnç ile birlikte bir dijital çıkışa bağlayabilirsiniz. MahirKart'da programladığınızda, dijital çıkış pininin durumunu "HIGH" yaparak LED'i yakabilir veya "LOW" yaparak LED'i söndürebilirsiniz.

<div style="text-align:center;">
    <img src="/userguide/arduino/img/dijitalsinyal.jpg"  style="width: auto;" />
</div>

## Dijital Giriş (Digital Input)

MahirKart'da dijital giriş pinleri, genellikle sensörlerden ve diğer cihazlardan veri almak için kullanılır. Bu pinlerde iki durum vardır: "HIGH" (yüksek) ve "LOW" (düşük). "HIGH" durumu 3.3V seviyesinde, "LOW" durumu ise 0V seviyesindedir.

Örneğin, bir düğme MahirKart'ım dijital girişine bağlanabilir. Düğmeye basıldığında, giriş pininin durumu "HIGH" olur ve düğme bırakıldığında durum "LOW" olur. Bu şekilde MahirKart, düğmenin durumunu algılayabilir ve buna göre bir eylem gerçekleştirebilir.


## Buton ile Led Yakma Projesi 

Öncelike kütüphanemizi indiriyoruz :
``` bash
pip install machine
```
 
Daha sonra gerekli kütüphaneleri import ediyoruz :

``` python
import machine
import time
```

Daha sonra "led" değişkenine çıkış pini ataması yapıyoruz.

``` python
led = machine.Pin(10, machine.Pin.OUT)
```
Burada "Pin" fonksiyonunun ilk parametresi ile işlem yapacağımız pini seçiyoruz, 2. parametre ile bu pine hangi işlemi yapacağımızı seçiyoruz. "machine.Pin.OUT" bu pine çıkış pini atamsı yapmaktadır eğer son kısmı "IN" yapsaydık giriş pini olarak atama yapacaktık.

``` python
button = machine.Pin(29,machine.Pin.IN, machine.Pin.PULL_DOWN)
```

Bu aşamada "button" değişkenine butonu kontrol edebilmek için giriş pini ataması yapıyoruz ve "machine.Pin.PULL_DOWN" ile pine akım girişi olduğunda fonksiyonun "1" değerini döndürmesini sağlıyoruz. Eğer "PULL_DOWN" parametresi girmiş olsaydık 29. pinden başlayan devre tamamlandığında "1" değerini döndürecekti yani akım 29. pinden akım çıkışı olacaktı.

``` python
while True :
    if button.value() == 1:
        led.on()
    else:
        led.off()
    time.sleep(0.1)
```
Bu aşamada "While" döngüsü ile sürekli button değişkeninden gelen veriyi sorguluyoruz. Eğer butonun olduğu tamamlandıysa (butona basıldıysa) "led.on()" fonksiyonu ile led ataması yapılan pinden akım çıkışı sağlanacak ve led yanacaktır. Ayrıca "time.sleep(0.1)" ile her döngüde sistemi 0.1 saniye uyutarak daha düzenli çalışmasını sağlıyoruz.

``` python
import machine
import time

led = machine.Pin(10, machine.Pin.OUT)
button = machine.Pin(29,machine.Pin.IN, machine.Pin.PULL_DOWN)

while True :
    if button.value() == 1:
        led.on()
    else:
        led.off()
    time.sleep(0.1)
```