# Arduino - Hızlı Başlangıç
Arduino, kendi yazılım dili ve mikrodenetçisine sahip bir platformdur. Arduino IDE üzerinden geliştirilir ve karta aktarılır.

Bu rehber, Arduino ile Mahirkart'ı kullanmaya başlamanıza yardımcı olacaktır. Geliştirme ortamını kurmak, Arduino kodunu Mahirkart'a yüklemek ve LED yaktığımı basit bir proje oluşturmak için adım adım talimatlar içerir.

## Gereksinimler

* Bir Mahirkart
* Bir USB Type-C kablosu
* Bir bilgisayar
* Arduino IDE

## Geliştirme Ortamı

Arduino programlarını yazmak ve çalıştırmak için bir geliştirme ortamına ihtiyacınız vardır. Bu rehberde, Arduino IDE kullanılacaktır. Arduino IDE, Arduino için entegre geliştirme ortamıdır ve aynı zamanda 3. taraf kartlar içinde kullanılmaktadır. 

## Arduino IDE Kurulumu

Arduino IDE, Arduino programlarını yazmak ve çalıştırmak için kullanılan entegre bir geliştirme ortamıdır. Arduino IDE'yi indirmek için aşağıdaki web sitesini ziyaret edin:

https://www.arduino.cc/en/software

Arduino IDE'yi indirdikten sonra, bilgisayarınıza yükleyin.

## Arduino IDE MahirKart ayarlarının yapılması
Arduino IDE’yi başlattıktan sonra, Dosya menüsünden “Tercihler”e gidin. “Ek Devre Kartları Yöneticisi URL’leri” bölümünün yanındaki düzenle butonuna basın.

Açılan pencerede yeni bir satır ekleyip aşağıdaki URL’yi ekleyin:

```
https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json
```
“Tamam” düğmesini tıklayarak pencereyi kapatın. Ardından, araçlar bölümündeki “kart” sekmesinden kart yöneticini seçerek açılan sekmede Raspberry Pi Pico/RP2040'ı aratın ve yükleyin. Bu paketi yükleyerek, MahirKart için gerekli olan RP2040 sürücülerini ve kütüphanelerini edineceksiniz.

Bu paketi yükledikten sonra “kart” penceresine geri dönün, “Raspberry Pi RP2040 Boards” altından Raspberry Pi Pico’yu seçin.

## Mahirkart Bağlantısı

MahirKart’ı USB kablosuyla bilgisayarınıza bağlayın. Kartın bağlandığını doğrulamak için, Arduino IDE’deki Araçlar menüsünden “Port” seçeneğine gelin ve MahirKart’ın portunu seçin.

## LED'i Yakmak için Bir Proje Oluşturma

Mahirkart'ın içinde 25 numaralı pine bağlı dahili LED bulunmaktadır. Bu led yanmak için harici bir dirence ihtiyaç duymaz. Arduino IDE üzerinden yeni bir dosya oluşturun ve şağıdaki kodu ekleyin:


``` c
const int ledPin = 25;   // Dahili LED 25 numaralı pine bağlı

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(1000);            
  digitalWrite(ledPin, LOW);
  delay(1000);
}
```
## Kodu Mahirkart'a yükleme

Kodu düzenledikten sonra Mahirkart'a yüklemek için aşağıdaki adımları izleyin:

* Mahirkart’ın üzerindeki “Bootsel” düğmesine basılı tutun.
* “Bootsel” düğmesine basılı tutarken MahirKartı bilgisayara USB kablosu ile bağlayın.
* “Bootsel” düğmesinden elinizi Mahirkart bilgisayara bağlandığında çekin.
* Kodu Mahirkart'a yükleyin.

## Sonuç

Bu rehber, Arduino ile Mahirkart'ı kullanmaya başlamanıza yardımcı olmayı hedeflemiştir. Rehberin sonunda kendiniz de LED yakmak için basit bir proje oluşturmayı deneyebilirsiniz.