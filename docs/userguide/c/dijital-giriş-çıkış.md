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

İlk olarak kütüphanelerimizi koda dahil ediyoruz ve buton ile ledi takacağımız pinleri tanımlıyoruz.
```c
// Gerekli kütüphanenin dahil edilmesi
#include "pico/stdlib.h"  
#include "hardware/gpio.h"

// Butonu ve ledi bağladığımız pinleri tanımlıyoruz.
#define button_pin 29
#define led_pin 25

```
Ardından main() fonksiyonumuzu yazıyoruz.
```c
int main(){

    stdio_init_all();

    // Buton ve Led pinlerini çalıştırmak için yapılandırır.
    gpio_init(button_pin);
    gpio_init(led_pin);

    // Led pinini çıkış ve buton pinini giriş olarak ayarlar.
    gpio_set_dir(led_pin, GPIO_OUT);
    gpio_set_dir(button_pin, GPIO_IN);

    // Bu, düğme etkinleştirildiğinde, mikrodenetleyicinin buton pini yüksek bir voltajda olacağını garanti eder.
    gpio_pull_up(button_pin);

    while(true)
    {
        // Burada butona basıldıysa ledi aktif ediyoruz.
        if(!gpio_get(button_pin)){
            gpio_put(led_pin, true);
        }
        
        // Burada butona basılmamışsa ledi söndürüyoruz.
        else{
            gpio_put(led_pin, false);
        }
        sleep_ms(200);
    }
}
```

Main.c dosyasının kodlaması bitti şimdi gerekli build işlemlerini tamamlaması için CMake kodunu yazacağız.

## Build İşlemi

Main.c ile aynı dizinde olacak şekilde CMakeLists.txt (Dosyanın adı aynı bu şekilde olmalıdır.) adlı bir dosya oluşturun. Dosyanızı açın ve aşağıdaki kodu yazın.

```
# Bu komut, CMake'in en az 3.12 sürümünü gerektirdiğini belirtir
cmake_minimum_required(VERSION 3.12) 

# Bu komut, CMake'in PICO_SDK_PATH ortam değişkeninin değerini kullanarak Pico SDK'nın dışa aktarma CMake dosyasını dahil eder.
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake) 

# Bu kod, blink adlı bir C/C++/ASM projesi tanımlar.
project(gpio C CXX ASM)

# Bu kodlar, C ve C++ projeleri için standartları ayarlar.
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Pico SDK'yı başlatır. 
pico_sdk_init()

# Bu kod, blink adlı bir proje için main.c dosyasını bir hedef olarak tanımlar.
add_executable(${PROJECT_NAME}
    main.c
)

# Derleme işleminin ardından oluşturulan ek dosyaları hedefe ekler.
pico_add_extra_outputs(${PROJECT_NAME})

# Bu kod, blink adlı bir hedefe pico_stdlib kitaplığını bağlar.
target_link_libraries(${PROJECT_NAME}
    pico_stdlib
    hardware_gpio
)

```

Şimdi ise build işlemini başlatacağız.

## UF2 Dosyasını Oluşturma

Visual Code’dan terminal açın. Terminaliniz bash olsun. Bulunduğunuz dizin main.c dosyanızla aynı dizinde olmalıdır. Her şey tamam ise şimdi kodlamaya geçelim.
İlk olarak Build alacağımız klasörü oluşturalım 
•	mkdir build 
Ardından build klasörünün içine girelim
•	cd build 

<div style="text-align:center;">
    <img src="/userguide/c/img/cd-build-gpio.jpg"  style="width: auto;" />
</div>

Ve buildi alalım.
•	cmake -G “MinGW Makefiles” ..
•	make

<div style="text-align:center;">
    <img src="/userguide/c/img/cmake-dijital.jpg"  style="width: auto;" />
</div>

<div style="text-align:center;">
    <img src="/userguide/c/img/make-dijital.png"  style="width: auto;" />
</div>

İhtayıcımız olan .uf2 uzantılı dosyayı build etmiş bulunmaktayız. Build klasörüne sağ tıklayıp Reveal in File Explorer’ a basın

<div style="text-align:center;">
    <img src="/userguide/c/img/revial-dijital.png"  style="width: auto;" />
</div>

Karta yükleyeceğimiz .uf2 dosyasını bu sayede görebileceksiniz. Şimdi iste Mahir Kartı bilgisayarınıza bootsel butonuna basarak yükleyin ve .uf2 uzantılı dosyasınızı kartın içine atın.

<div style="text-align:center;">
    <img src="/userguide/c/img/bootsel-dijital.png"  style="width: auto;" />
</div>
