# C - Hızlı Başlangıç

C, MahirKart gibi birçok geliştirme kartını programlayabildiğimiz bir yazılım dilidir.

Bu rehber, C ile MahirKart'ı kullanmaya başlamanıza yardımcı olacaktır. Geliştirme ortamını kurmak, C kodunu MahirKart'a yüklemek ve LED yaktığımız basit bir proje oluşturmak için adım adım talimatlar içerir.

## Gereksinimler

* Bir MahirKart
* Bir USB Type-C kablosu
* Bir bilgisayar
* Visual Code
* Gerekli olan bir kaç Tool

## Geliştirme Ortamı
C ile programlama yapabilmek için öncelikle birkaç eklenti kurmamız gerekecektir. Geliştirme ortamı olarak Visual Code kullanılacaktır. İsterseniz başka bir geliştirme ortamı da kullanabilirsiniz. Adım adım hepsi anlatılacaktır.

## Dizin Kurulumu

Kuracağımız araçları tek bir klasörde konumlandıracağız. Bu sayede ilerleyen süreçlerde daha düzenli bir çalışma ortamı oluşturmuş olacağız.

C sürücünüzün en üst dizinine VSMHR adlı bir klasör oluşturun. Ardından VSMHR klasörünün içine şu klasörleri oluşturun :

*	armcc 	(Dizini şu şekilde olmalı C:\VSMHR\armcc)
*	lib 	(Dizini şu şekilde olmalı C:\VSMHR\lib)
*	mingw	(Dizini şu şekilde olmalı C:\VSMHR\mingw)
*	sdk 	(Dizini şu şekilde olmalı C:\VSMHR\sdk)

Yukarıdaki 4 klasörü VSMHR klasörünün altına oluşturduğunuzda aşağıdaki görsel gibi klasör yapısına sahip olmalısınız.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim1.png"  style="width: auto;" />
</div>

## GNU Arm Embedded Toolchain Kurulumu

GNU Arm Embedded Toolchain, RP2040 işlemcisinde C ve C++ kodunu derlemek için ihtiyaç duyulan Arm GCC derleyicisini içerir. https://developer.arm.com/downloads/-/gnu-rm sayfasına gidin ve Windows için en son yükleyiciyi indirin. 

Exe’yi çalıştırdıktan sonra hedef dizin seçiminde “Gözat” a tıklayıp C:\VSMHR\armcc yolunu seçin.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim2.png"  style="width: auto;" />
</div>

"C:\VSMHR\armcc" bu yolu seçtiğinizde ise “Hedef Dizin” kutusu aşağıdaki gibi olacaktır. (İndirdiğiniz sürüme bağlı olarak armcc\ den sonraki kısım değişiklik gösterecektir.)

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim3.png"  style="width: auto;" />
</div>

“Kur” butonuna basıp kurulum işlemine devam edin. Birkaç dakika sürebilir bu kısım. Kurulum tamamlandığında Ortam değişkenine yol ekle (Add path to environment variable) kutucuğunu işaretleyin. Bitir demeden önce kurulum dosyasının son hali şu şekilde olmalıdır.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim4.jpg"  style="width: auto;" />
</div>

Böylece GNU Arm Embedded Toolchain kurulumunu bitirmiş olduk. Şimdi diğer adıma geçelim.

## MinGW-w64 GCC Toolchain Kurulumu
MinGW, Windows için uygulamalar geliştirmenize olanak tanıyan derleyiciler ve bağlayıcılar gibi açık kaynaklı yardımcı programlardan oluşan bir koleksiyondur. MahirKart’da kullanılmak üzere MinGW-w64(8.10) i686-posix-sjlj.zip dosyasını indireceğiz. https://sourceforge.net/projects/mingw-w64/files/ bu siteye gidip aşağıya kaydırıp i686-posix-sjlj dosyasına tıklayacaksınız.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim5.png"  style="width: auto;" />
</div>

İndirdiğiniz .zip dosyasını C:\VSMHR\mingw dizinine çıkartın. 

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim6.png"  style="width: auto;" />
</div>

Çıkartma işlemini tamamladıktan sonra bir Windows Komut İstemi açıp (Windows tuşuna basıp cmd yazabilirsiniz. İlk çıkana tıklayın.) aşağıdaki komutu yazın.

```
echo mingw32-make %* > C:\VSARM\mingw\mingw32\bin\make.bat
```

MinGW kurulumunu da başarıyla tamamladık bir sonraki adıma geçelim.

## CMake Kurulumu

CMake, C ve C++ ile yazılan projelerin derleme ve kurulum sürecini otomatikleştirmek için kullanılan bir araçtır. Çapraz platformdur, yani Windows, macOS ve Linux gibi farklı işletim sistemlerinde çalışabilir. https://cmake.org/download/ bu siteden CMake’ in Windows için olan en son sürümünü indirin. İndirdiğiniz dosyayı çalıştırın, kullanıcı lisansını kabul edin son olarak “Tüm Kullanıcılar İçin CMake’i Sistem Yol’una Ekle”’ butonunu işaretleyin.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim7.png"  style="width: auto;" />
</div>

CMake’i yükleyeceğiniz dizini C:\Program Files\CMake dizinine yüklerseniz daha rahat bir çalışma ortamınız olur. Çünkü CMake sistem çapında bir araç olarak kullanılacaktır. CMake kurulumunu da başarılı bir şekilde bitirdik. Bir sonraki adıma geçelim.

## Python Kurulumu

https://www.python.org/downloads/ bu siteye gidip en güncel Python yükleyicisini indirin. Yükleyiciyi çalıştırın. Gelen ekranda iki kutucuğu da işaretleyin.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim8.png"  style="width: auto;" />
</div>

İki kutucuğu da seçtikten sonra “Install Now” a tıklayın. Ardından MAX_PATH uzunluk sınırını devre dışı bırakma işlemi yapacağız. Bunun için Windows arama çubuğuna “Kayıt Defteri Düzenleyicisi” yazın ve ilk çıkana tıklayın. Ekrana aşağıdaki görsel gibi bir ekran gelecektir. 

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim9.png"  style="width: auto;" />
</div>

Ardından bu ekranda kutu içerisindeki kısma şu yolu kopyalayın. 

```
Bilgisayar\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem
```
<div style="text-align:center;">
    <img src="/userguide/c/img/Resim10.png"  style="width: auto;" />
</div>

Yukarıdaki yola gittiğinizde önünüze  bu sayfa gelecektir. Bu sayfadanda okla gösterilen LongPathEnabled ‘a tıklayıp önünüzde açılan pencerede aşağıdaki seçenekleri yapın ve Tamam’a basın.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim11.png"  style="width: auto;" />
</div>

Bu işlemi de başarıyla tamamladık ve bir sonraki adıma geçtik.

## Git Kurulumu

https://git-scm.com/download/win bu siteye gidip Windows için en son sürümü indirin. Tüm varsayılanları kabul ederek kurulum işlemini tamamlayın. Git kurulumu da bu kadardı. Şimdi pico-sdk’yı indereceğiz.

## Pico SDK Kurulumu

Pico SDK, RP2040 işlemcisi için bir C/C++ yazılım geliştirme kitidir. Pico SDK, RP2040’ın donanım özelliklerine erişmek için API'ler ve kütüphaneler sağlar.

Öncelikle C:\VSMHR\sdk dizinine gidip bu dizin içerisinde “mahir” adlı bir klasör oluşturun.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim12.png"  style="width: auto;" />
</div>

Klasörü oluşturduktan sonra Git Bash’i açın. Ardından sırasıyla şu komutları yazın.
cd /c/VSMHR/sdk/mahir (kurulum yapacağımız dizine gitmemizi sağlar)

```
git clone -b master https://github.com/raspberrypi/pico-sdk.git 
```
Bu komut Github’daki repoyu klonlar.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim13.png"  style="width: auto;" />
</div>

git clone -b master https://github.com/raspberrypi/pico-sdk.git bunu yazıp enter’a bastığımızda birkaç indirme işlemi yapacak.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim14.png"  style="width: auto;" />
</div>

Ardından “pico-sdk” klasörüne gidip sub modülleri indireceğiz. Bunun içinde aşağıdaki kodları yazın.

```
cd pico-sdk
```

Sonra ;

```
git submodule update --init
```

Yukarıdaki kodu yazın. Bu kısmın yüklenmesi uzun sürebilir.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim15.png"  style="width: auto;" />
</div>

Artık RP2040 işlemcisinde C/C++ programları geliştirmek için gerekli tüm derleme araçlarını kurduk. Geriye sadece birkaç ortam değişkeni güncellemesi kaldı. Şimdi o adıma geçelim.

## Ortam Değişkenlerini Güncelleme

Kurduğumuz araç ve eklentilerden bazıları ortam değişkenlerini güncelledi. Güncellemeyen birkaçı (MinGW ve SDK) için kendimiz manuel güncelleme yapacağız. 

Windows arama çubuğuna “Sistem ortamı değişkenlerini düzenle” yazın ve ilk çıkana tıklayın. Karşınıza alttaki gibi bir ekran gelecek.  Bu pencerede “Ortam Değişkenleri..” butonuna basın

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim16.png"  style="width: auto;" />
</div>

İlk olarak kullanıcı değişkenlerini yapacağız. Path’i seçin ve Düzenle’ye tıklayın

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim17.png"  style="width: auto;" />
</div>

Düzenle dedikten sonra gelen ekranda sağ üstten Yeni’ye tıklayıp C:\VSMHR\mingw\mingw32\bin bunu yazın ve tamam diyin. Ayrıca yine bu ekranda 

* C:\VSMHR\armcc\<yayın sürümü>\bin

* C:\VSMHR\mingw\mingw32\bin

Bu iki yolu da gördüğünüzden emin olun.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim18.png"  style="width: auto;" />
</div>

Emin olduktan sonra Tamam’a tıklayın. Ardından yine kullanıcı değişkenleri kısmında Yeni butonuna basıp şunu ekleyin :

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim19.png"  style="width: auto;" />
</div>

Değişken adı : PICO_SDK_PATH

Değişken değeri : C:\VSMHR\sdk\mahir\pico_sdk

Bu işlemleri yaptıktan sonra “Kullanıcı Değişkeni” kısmına PICO_SDK_PATH oluşması lazım.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim20.png"  style="width: auto;" />
</div>

Ardından kontrol amaçlı Sistem Değişkenleri kısmından PATH’i seçip Düzenle diyip 

* C:\Program Dosyaları\CMake\bin
* C:\Program Dosyaları\Git\cmd
  
Bu iki yolun olduğundan emin olun

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim21.png"  style="width: auto;" />
</div>

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim22.png"  style="width: auto;" />
</div>

Tüm her şey tamamsa Tamam butonlarına basarak ekranları kapatın. Evet tüm kurulumları tamamlamış bulunmaktayız. Artık Led yakmaya geçebiliriz.

## Led Yakıp Söndürme İçin Proje Oluşturma 

İlk olarak projelerimizi yerleştireceğimiz bir klasör oluşturmalıyız. C:\VSMHR\sdk\mahir\ dizinin içine mhrkrt_ornekler diye bir klasör oluşturalım. 

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim23.png"  style="width: auto;" />
</div>

Ardınan Visual Code programına girip File kısmına tıklayıp Open Folder’a basıp mhrkrt_ornekler klasörünü seçin. Bu klasörde iken tekrardan bir klasör açın ve adını Blink koyun.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim24.png"  style="width: auto;" />
</div>

Ardından Blink klasörü içine main.c dosyasını oluşturun. Main.c dosyasını kodlamaya başlayalım. Blink için kodlama şu şekildedir.

```c
#include "pico/stdlib.h"  // Gerekli kütüphanenin dahil edilmesi
```

```c
int main(){

    const uint Led_pin = 25; // Mahir Kart üzerindeki ledin pininin değişkene atama

    gpio_init(Led_pin);  // Pin için gerekli init işlemlerini yapma
    gpio_set_dir(Led_pin, GPIO_OUT); // Pinin fonksiyonunu belirleme 

    while (true)
    {
        gpio_put(Led_pin, true); // Ledi yakma
        sleep_ms(1000);
        gpio_put(Led_pin, false); // Ledi söndürme
        sleep_ms(1000);
    }
    
}

```

Main.c dosyasını yazdıktan sonra main.c ile aynı dizinde olacak şekilde adı CmakeLists.txt olan bir dosya oluşturun. Klasör içi şu şekilde görünecektir. 

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim25.png"  style="width: auto;" />
</div>

Ardından CMake dosyasının içine gelin ve şu kodları yazın :

```c
// Bu komut, CMake'in en az 3.12 sürümünü gerektirdiğini belirtir 
cmake_minimum_required(VERSION 3.12) 

```


```c
// Bu komut, CMake'in PICO_SDK_PATH ortam değişkeninin değerini kullanarak Pico SDK'nın dışa aktarma CMake dosyasını dahil eder.
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake) 

// Bu kod, blink adlı bir C/C++/ASM projesi tanımlar.
project(blink C CXX ASM)

// Bu kodlar, C ve C++ projeleri için standartları ayarlar.
set(CMAKE_C_STANDART 11)
set(CMAKE_CXX_STANDART 17)

// Pico SDK'yı başlatır. 
pico_sdk_init()

// Bu kod, blink adlı bir proje için main.c dosyasını bir hedef olarak tanımlar.
add_executable(${PROJECT_NAME}
    main.c
)

// Derleme işleminin ardından oluşturulan ek dosyaları hedefe ekler.
pico_add_extra_outputs(${PROJECT_NAME})

// Bu kod, blink adlı bir hedefe pico_stdlib kitaplığını bağlar.
target_link_libraries(${PROJECT_NAME}
    pico_stdlib
)

```


CMake dosyasımızı da yazdığımıza göre son işleme geçiyoruz. Bir terminal açın. Terminalden Git Bash seçin. Ardından sırasıyla bu komutları yazın :

```c
cd blink
```

```c
mkdir build
```

```c
cd build
```

```c
cmake -G “MinGW Makefiles” ..
```

(Kurulum biraz zaman alabilir)

```c
make
```

(Kurulum biraz zaman alabilir)

Mahir Kart’a yüklenecek olan dosya hazır hale gelmiş olur.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim26.png"  style="width: auto;" />
</div>

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim27.png"  style="width: auto;" />
</div>

Bu işlemler sonucunda Mahir Kart içine atacağımız blink.uf2 dosyası oluşuyor. Şimdi bu dosyayı kartımızın içine atalım. Build klasörünün üstüne sağ tık yapıp “ Reveal in File Explorer”

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim28.png"  style="width: auto;" />
</div>

Ardından karşınıza şöyle bir klasör gelecek. Okla gösterilen blink.uf2 dosyası Mahir Kartın içine atılacak olan dosyadır.

<div style="text-align:center;">
    <img src="/userguide/c/img/Resim29.png"  style="width: auto;" />
</div>
