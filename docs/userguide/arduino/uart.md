# UART

## UART Protokolü

UART(Universal Asynchronous Receiver Transmitter/ Evrensel Asenkron Alıcı Verici) protokolü, iki cihaz arasında seri haberleşme sağlayan bir protokoldür. UART protokolü, veri gönderme ve alma işlemlerini gerçekleştirmek için iki adet veri hattı(RX ve TX) kullanır. Veri gönderme işlemi TX hattından, veri alma işlemi ise RX hattından gerçekleşir. İki cihazın UART kabloları birbirine zıt gelecek şekilde(RX TX'e; TX RX'e) bağlanılır. 

Bu protokolü donanımsal olarak kullanabileceğiniz gibi yazılımsal olarak da oluşturabilirsiniz ama yazılımsal olarak kullanmanız işlemciniz için ek bir yük oluşturacaktır. Bu yüzden donanımsal olarak kullanmanızı tavsiye ederiz. Günümüzde UART protokolü, kolay uygulanabilir olması ve düşük maliyeti sebebiyle kullanılmaktadır.

<div style="text-align:center;">
    <img src="/userguide/arduino/img/uart.png"  style="width: auto;" />
</div>

## MahirKart ile UART

MahirKart üzerinde birden fazla pin seçeneğiyle kullanabileceğiniz iki adet donanımsal UART bulunmaktadır. Bunları isterseniz bu iş için ayrılmış JST konektörler ile istersenizde pinler üzerinden yapabilirsiniz. MahirKart'ın UART pinlerini [Pinout](../../pinout.md) sayfasından öğrenebilirsiniz.

## Python ile UART Kullanımı örneği

Bu örneğimizde MahirKart'ı ikinci bir geliştirme kartıyla UART üzerinden haberleşeceğiz. İlk olarak ikinci geliştirme kartımızı(başka bir MahirKart olabilir) MahirKart'a bağlayamak için MahirKart'ın TX'ini ikinci seçtiğiniz geliştirme kartınının RX'ine bağlayın. Ardından önce MahirKart'a ardından ikinci geliştirme kartı için aşağıdaki kodları sırayla yükleyin.

## Veri Gönderecek MahirKart için Kod Örneği 

``` c
void setup() {
  Serial.begin(9600);  // Seri iletişim başlatılır
}

void loop() {
  String veri = "Welcome to MahirKart's World!";  // Gönderilecek veri
  Serial.println(veri);  // Veriyi seri port üzerinden gönderir
  delay(1000);  // 1 saniye bekleme süresi
}

```

## Veri Alacak MahirKart için Kod Örneği 

``` c
void setup() {
  Serial.begin(9600);  // Seri iletişim başlatılır
}

void loop() {
  String alinanVeri = Serial.readString();  // Veriyi okur
  Serial.print("Alınan Veri: ");
  Serial.println(alinanVeri);  // Alınan veriyi seri port üzerinden gösterir
}

```

## Sonuç

Bu uygulamada MahirKart'ı UART protokolü ile başka bir geliştirme kartına bağladık. MahirKart'tan diğer karta veri gönderdik. Bu gönderilen verileri ikinci kartın seri monitöründe okuduk. UART protokolü ile farklı örnekler yapabilirsiniz. Bir seri monitörden gönderdiğiniz veriyi diğer seri monitörden okuyabilirsiniz.

Eğer aklınızda kalan sorular varsa [Discord](https://discord.com/invite/YVc68SrGJK) sunucumuz üzerinden sorabilirsiniz.