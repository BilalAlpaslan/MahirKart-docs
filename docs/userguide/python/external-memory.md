# Harici Bellek Kullanımı

## Harici Bellek Nasıl Çalışır?

Python kodlarımızı çalıştırmak için kullandığımız MahirKart üzerindeki harici 2MB'lik SPI Flash bellek sadece Python kodlarımızı depolamak için değil, aynı zamanda Python kodlarımızın çalışma zamanında kullanabileceği bir bellek alanı olarak da kullanılabilir. Python driver'ı içerisinde gelen filesystem sayesinde bu bellek alanına dosya olarak erişebiliriz. Bu alanda resim, ses, video, metin gibi birçok dosya tipini depolayabilir ve Python kodlarımızın çalışma zamanında bu dosyaları kullanabiliriz.

## Python İle Harici Bellek Kullanımı

Harici belleğe erişim için gereken herşeyi arkadaki filesystem izim için halledecek. Bu yüzden normal python kodunda nasıl dosya işlemleri yapıyorsak MahirKart üzerinde de bu işlemleri yaabiliriz.

## Harici Bellek Üzerindeki Dosyaları Listeleme

Bu örneğimizde harici bellek üzerindeki dosyaları listeliyoruz.

``` python
import os

print(os.listdir()) # Harici bellek üzerindeki dosyaları listeliyoruz.
```

## Yapabileceğiniz Dosya İşlemleri

``` python
import os

os.chdir(path) # Bulunduğunuz dizini değiştirir.

os.getcwd() # Bulunduğunuz dizini döndürür.

os.listdir() # Bulunduğunuz dizindeki dosyaları listeler.

os.mkdir(path) # Bulunduğunuz dizinde yeni bir dizin oluşturur.

os.remove(path) # Bulunduğunuz dizindeki dosyayı siler.

os.rename(old, new) # Bulunduğunuz dizindeki dosyanın ismini değiştirir.
```

dosya işlemleri için kullanabileceğiniz tüm fonksiyonları [buradan](https://docs.micropython.org/en/latest/library/os.html) inceleyebilirsiniz.

## Sonuç

Bu yazımızda harici belleğin nasıl kullanıldığını ve dosya işlemlerini öğrendik. Eğer aklınızda kalan sorular varsa [Discord](https://discord.com/invite/YVc68SrGJK) sunucumuz üzerinden sorabilirsiniz.