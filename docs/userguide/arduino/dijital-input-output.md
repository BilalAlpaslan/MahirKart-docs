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

## Arduino Kod Örneği

MahirKart'da dijital giriş ve çıkışları kullanmak için Arduino IDE adlı Entegre Geliştirme Ortamı kullanılır. Arduino IDE'yi nasıl kuracağınızı ve MahirKart'a nasıl kod yükleyeceğinizi öğrenmek için [Arduino - Hızlı Başlangıç](/userguide/arduino/quickstart/) sayfasını ziyaret edebilirsiniz. İşte basit bir örnek kod, MahirKart ile bir düğme ve bir LED'i kontrol etmek için:

``` c
// Dijital giriş ve çıkış pin numaralarını tanımlama
const int buttonPin = 23; // Düğme için giriş pin numarası
const int ledPin = 25;   // LED için çıkış pin numarası

void setup() {
  pinMode(buttonPin, INPUT);   // Düğme pinini giriş olarak ayarlama
  pinMode(ledPin, OUTPUT);     // LED pinini çıkış olarak ayarlama
}

void loop() {
  int buttonState = digitalRead(buttonPin); // Düğme durumunu okuma

  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH); // Düğmeye basılırsa, LED'i yak
  } else {
    digitalWrite(ledPin, LOW);  // Düğme bırakılırsa, LED'i söndür
  }
}

```
Bu basit örnek, MahirKart'ın dijital giriş ve çıkışlarını kullanarak düğme durumunu okur ve bu duruma bağlı olarak bir LED'i kontrol eder. Düğmeye basıldığında LED yanar, düğme bırakıldığında LED söner.

MahirKart ile dijital giriş ve çıkışlar, daha karmaşık projelerde de kullanılabilir. Sensörler, motorlar, ekranlar ve diğer bileşenler MahirKart'ın esnekliği sayesinde kolayca entegre edilebilir.

MahirKart'ın pin yapısını [Pinout](/pinout/) sayfasından inceleyebilir ve projeleriniz için doğru pinleri seçebilirsiniz.

Bu yazı, MahirKart'ın dijital giriş ve çıkışları hakkında temel bilgileri sunmaktadır.