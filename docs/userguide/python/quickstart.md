# Python - Hızlı Başlangıç

MicroPython, Python programlama dilinin küçük bir sürümüdür ve Mahirkart gibi geliştirme kartlarının üzerinde çalışacak şekilde tasarlanmıştır. 

Bu rehber, MicroPython ile Mahirkart'ı kullanmaya başlamanıza yardımcı olacaktır. Geliştirme ortamını kurmak, MicroPython'u Mahirkart'a yüklemek ve LED yaktığımı basit bir proje oluşturmak için adım adım talimatlar içerir.

## Gereksinimler

* Bir Mahirkart
* Bir USB Type-C kablosu
* Bir bilgisayar
* Thonny IDE

## Geliştirme Ortamı

MicroPython programlarını yazmak ve çalıştırmak için bir geliştirme ortamına ihtiyacınız vardır. Bu rehberde, Thonny IDE kullanılacaktır. Çok basit ve kurulumu kolay olduğu için tercih edilmiştir. İsterseniz Visual Studio Code gibi başka bir geliştirme ortamı da kullanabilirsiniz. 

## Thonny IDE Kurulumu

Thonny IDE, MicroPython programlarını yazmak ve çalıştırmak için ücretsiz bir yazılımdır. Thonny IDE'yi indirmek için aşağıdaki web sitesini ziyaret edin:

https://thonny.org/

Thonny IDE'yi indirdikten sonra, bilgisayarınıza yükleyin.

## Mahirkart'a MicroPython Kurulumu

Mahirkart'ı bilgisayarınıza bağlarken aynı zamanda üzerinde bulunan bootsel düğmesine basın. Bu sayede MahirKart bilgisayarınızda bir USB depolama aygıtı olarak görünecektir. [buraya tıklayarak](https://micropython.org/resources/firmware/rp2-pico-20230426-v1.20.0.uf2) MicroPython'ı indirip USB depolama aygıtına kopyalayarak kurabilirsiniz yada thonny sizin yerinize bu adımı yapabilir. MicroPython'u kopyaladıktan sonra, Mahirkart'ı bilgisayarınızdan çıkarın ve tekrar bağlayın. Mahirkart artık MicroPython çalıştırmaya hazır.

## LED'i Yakmak için Bir Proje Oluşturma

LED'i yakmak için basit bir proje oluşturmak için yeni bir belge oluşturun ve aşğıdaki kodu ekleyin:

```python 
import machine

led = machine.Pin(25, machine.Pin.OUT)

led.on()
```

Kod çalıştırıldığında, LED yanacaktır.

## Sonuç

Bu rehber, MicroPython ile Mahirkart'ı kullanmaya başlamanıza yardımcı olmuştur. Rehberin sonunda, bir LED'i yakmak için basit bir proje oluşturmayı öğrenmişsinizdir.
