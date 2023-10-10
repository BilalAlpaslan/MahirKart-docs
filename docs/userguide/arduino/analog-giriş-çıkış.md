# Analog Giriş/Çıkış

## MahirKart ile Analog Giriş/Çıkış

MahirKart'da analog giriş ve çıkışlar (Analog Input/Output) olarak bilinen pinleri bulunur. Analog girişler, genliğine ve zamana bağlı olarak çeşitli değerlerde sinyaller alırlar. Dijital çıkışlar, genliğine ve zamana bağlı olarak çeşitli değerlerde sinyaller üretirler. 

<div style="text-align:center;">
    <img src="/userguide/arduino/img/digital-ve-analog-signal.jpg"  style="width: auto;" />
</div>

Yukarıdaki grafikte görüldüğü gibi Dijital sinyaller yalnızca 0 ve 1 gibi belli değerleri alırken analog sinyallerin alabileceği değerler zamana ve sinyalin genliğine göre değişiklik göstermektedir.

MahirKart üzerinde Dijital Giriş/Çıkışların yanından daha hassas değerler kullanabilmemizi sağlayan "Analog Giriş/Çıkış"lar da bulunmaktadır. MahirKart üzerinde hangi pinlerin Analog sinyelleri desteklediğini öğrenmek için [Pinout](../../pinout.md) sayfasını ziyaret edebilirsiniz.

## Potansiyometre Projesi

Analog sinyallerle, bir potansiyemetre projesi yaparak kolaylıkla çalışmaya başlayabilirsiniz. Bu projede bir potansiyometre devresi kuracağız. Aşağıda bir potansiyometrenin datasheet görseli bulunmaktadır.

<div style="text-align:center;">
    <img src="/userguide/arduino/img/potansiyometre.png"  style="width: auto;" />
</div>

Görselde "VCC" ile gösterilen bacağa 1. pini yani 3.3V pinini, "Ground" ile gösterilen bacağa 3. pini yani topraklama hattını ve son olarak da ortadaki bacağa 29. pini Breadboard üzerinde bağlayalım.

## Arduino Kod Örneği

MahirKart'da analog giriş ve çıkışları kullanmak için Arduino IDE adlı Entegre Geliştirme Ortamı kullanılır. Arduino IDE'yi nasıl kuracağınızı ve MahirKart'a nasıl kod yükleyeceğinizi öğrenmek için [Arduino - Hızlı Başlangıç](/userguide/arduino/quickstart/) sayfasını ziyaret edebilirsiniz. MahirKart ile bir potansiyometreyi kontrol etmek için:

``` c
const int potPin = 29; // Potansiyometre pinini tanımla

void setup() {

  Serial.begin(9600); // Seri bağlantıyı başlat
}

void loop() {
  
  int potValue = analogRead(potPin); // Potansiyometrenin değerini oku (0 ile 1023 arasında bir değer)

  
  Serial.print("Potansiyometre Değeri: "); // Okunan değeri seri monitörde görüntüle
  Serial.println(potValue);

  
  delay(100);
}

```
Bu basit örnek, MahirKart'ın analog giriş ve çıkışlarını kullanarak potansiyometre durumunu okur ve bunu ekrana yazdırır. Potansiyometre yardımıyla farklı sinyaller oluşturabilirsiniz.

MahirKart ile analog giriş ve çıkışlar, daha karmaşık projelerde de kullanılabilir. Sensörler, motorlar, ekranlar ve diğer bileşenler MahirKart'ın esnekliği sayesinde kolayca entegre edilebilir.

MahirKart'ın pin yapısını [Pinout](/pinout/) sayfasından inceleyebilir ve projeleriniz için doğru pinleri seçebilirsiniz.

Bu yazı, MahirKart'ın analog giriş ve çıkışları hakkında temel bilgileri sunmaktadır.

Eğer aklınızda kalan sorular varsa [Discord](https://discord.com/invite/YVc68SrGJK) sunucumuz üzerinden sorabilirsiniz.