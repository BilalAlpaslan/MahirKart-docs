# Analog Giriş/Çıkış

## MahirKart ile Analog Giriş/Çıkış

Analog giriş/çıkış, bir elektronik cihazın fiziksel dünyayla etkileşim kurmak için kullandığı bir yöntemdir. Analog giriş, bir fiziksel sinyalin değerini okumak için kullanılır. Analog çıkış, bir fiziksel sinyal göndermek için kullanılır.

Analog sinyaller, sürekli bir genliğe sahiptir. Bu, analog sinyallerin herhangi bir değerde olabileceği anlamına gelir. Örneğin, bir sıcaklık sensörünün ürettiği sinyal, 0 ila 100 derece arasında değişebilir.

MahirKart üzerinde dijital giriş/çıkışların yanından daha hassas değerler kullanabilmemizi sağlayan "Analog Giriş/Çıkış"lar da bulunmaktadır. MahirKart üzerinde hangi pinlerin Analog sinyelleri desteklediğini öğrenmek için [Pinout](../../pinout.md) sayfasını ziyaret edebilirsiniz.

## Potansiyometre Projesi
Bu projemiz için basit bir potansiyometre devresi kurabilirsiniz. Aşağıda bir potansiyometrenin datasheet görseli bulunmaktadır.

<div style="text-align:center;">
    <img src="/userguide/python/img/potansiyometre.png"  style="width: auto;" />
</div>

Görselde "VCC" ile gösterilen bacağa 1. pini yani 3.3V pinini, "Ground" ile gösterilen bacağa 3. pini yani topraklama hattını ve son olarak da ortadaki bacağa 29. pini Breadboard üzerinde bağlayalım. Şimdi koda geçebiliriz

``` Python
import machine
import time
```
Öncelikle gerekli olan kütüphanelerimizi ekledik.

``` Python
pm = machine.ADC(29)
```
Daha sonra potansiyometremizin orta bacağına bağladığımız 29. pine ADC(Analog-Digital Converter) sınıfı ataması yapıyoruz.

``` Python
While True :
    value = pm.read()
    print("Potansiyometreden okunan değer :", value)
    time.sleep(0.1)
```

Son olarak ise "While" döngüsü içerisinde 29. pinden gelen değeri anlık olarak "value" değişkenine atayıp daha sonra bu değeri  yazdırıyoruz. Ayrıca bu işlemin gözle görülür gerçekleşmesi için "time.sleep(0.1)" kullanıyoruz. Kodumuz hazır kendiniz de farklı kod denelemeleri yapark <a href="https://discord.com/invite/AzAHFzzZ">Discord</a> sunucumuzda paylaşabilir ve topluluğumuza destek olabilirsiniz. 

