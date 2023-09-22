# UART

## UART Protokolü

UART protokolü, iki cihaz arasında seri haberleşme sağlayan bir protokoldür. UART protokolü, veri gönderme ve alma işlemlerini gerçekleştirmek için iki adet veri hattı(RX ve TX) kullanır. Veri gönderme işlemi TX hattından, veri alma işlemi ise RX hattından gerçekleşir.İki cihazın UART kabloları birbirine zıt gelecek şekilde(RX TX'e; TX RX'e) bağlanılır. 

Bu protokolü donanımsal olarak kullanabileceğiniz gibi yazılimsal olarak da oluşturabilirsiniz ama yazılımsal olarak kullanmanız işlemciniz için ek bir yük oluşturacaktır. Bu yüzden donanımsal olarak kullanmanızı tavsiye ederiz.

## MahirKart ile UART

MahirKart üzerinde birden fazla pin seçeneğiyle kullanabileceğiniz iki adet donanımsal UART bulunmaktadır. Bunları isterseniz bu iş için ayrılmış JST konektörler ile istersenizde pinler üzerinden yapabilirsiniz. MahirKart'ın UART pinlerini [Pinout](../../pinout.md) sayfasından öğrenebilirsiniz.

## Python ile UART Kullanımı örneği

Bu örneğimizde ikinci bir geliştirme kartıyla UART üzerinden haberleşeceğiz. İlk olarak ikinci geliştirme kartımızı(başka bir MahirKart olabilir) MahirKart'a bağlayalım. İkinci geliştirme kartımızdan okuduğumuz veriyi yazdıralım.

``` python
from machine import Pin,UART
import time

uart = UART(0, baudrate=9600, tx=Pin(0), rx=Pin(1)) # UART0'ı 9600 baudrate ile kullanacağımızı belirtiyoruz. TX ve RX pinlerini de belirtiyoruz.

while True:
    if uart.any():  # UART üzerinden veri geldiğinde
        data = uart.read()  # Veriyi okuyoruz.
        print(data) # Veriyi yazdırıyoruz.
    time.sleep(1)
```
