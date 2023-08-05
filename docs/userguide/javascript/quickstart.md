# JavaScript - Hızlı Başlangıç

Bu rehber, JavaScript ile MahirKart'ı programlamaya başlamanıza yardımcı olacaktır. Geliştirme ortamını kurmak, JavaScript kodumuzu MahirKart'a yüklemek ve LED yaktığımız basit bir proje oluşturmak için adım adım talimatlar içerir.

## Gereksinimler

* Bir MahirKart
* Bir USB Type-C kablosu
* Bir bilgisayar
* Visual Studio Code(veya başka bir geliştirme ortamı)

## Geliştirme Ortamı

JavaScript(Node.JS) programları yazmak ve çalıştırmak için bir geliştirme ortamına ihtiyacınız vardır. Bu rehberde, Visual Studio Code kullanılacaktır. İsterseniz başka bir geliştirme ortamı da kullanabilirsiniz. Bilgisayarınıza Node.JS kurulu olması yeterlidir.

## Node.JS Kurulumu

Node.JS, JavaScript kodlarını bilgisayarınızda çalıştırmanızı sağlayan bir platformdur. Node.JS'i indirmek için aşağıdaki web sitesini ziyaret edin:

https://nodejs.org/en/download/current


## Kaluma ve Kaluma CLI Kurulumu

İlk olarak MahirKart üzerinde javascript kodlarını çalıştırmak için Kaluma firmware'i yüklememiz gerekiyor. Kaluma firmwaresini yüklemek için aşağıdaki linki ziyaret edin:

https://github.com/kaluma-project/kaluma/releases/download/1.1.0-beta.2/kaluma-rp2-pico-1.1.0-beta.2.uf2

Sonrasında MahirKart'ı bilgisayarınıza bağlarken aynı zamanda üzerinde bulunan bootsel düğmesine basın. Bu sayede MahirKart bilgisayarınızda bir USB depolama aygıtı olarak görünecektir. Kaluma firmware'ini bu USB depolama aygıtına kopyalayın. Kaluma firmware'ini kopyaladıktan sonra, MahirKart'ı bilgisayarınızdan çıkarın ve tekrar bağlayın. MahirKart artık Kaluma çalıştırmaya hazır.

Kaluma firmware'ini yükledikten sonra Kaluma CLI'yi yüklememiz gerekiyor. Kaluma CLI'yi yüklemek için aşağıdaki komutu çalıştırın:

```bash
npm install -g @kaluma/cli
```

## LED'i Yakıp Söndürmek için Proje Oluşturma

LED'i yakmak için basit bir proje oluşturmak için yeni bir belge oluşturun ve aşğıdaki kodu ekleyin:

```javascript
const led = 25; // dahili led 25 numaralı pinde

pinMode(led, OUTPUT); // pin modunu çıkış olarak ayarlıyoruz

setInterval(() => { // 1 saniye ara ile çalışmasını istediğimiz kod bloğunu içerisine yazıyoruz
    digitalToggle(led); // led değerini değiştiriyoruz
}, 1000);
```

Kodu kaydettikten sonra, terminalden aşağıdaki komutu çalıştırın:

```bash
kaluma run index.js
```
yada
    
```bash
npx kaluma run index.js
```

Kod çalıştırıldığında, LED 1 saniye aralıklarla yanıp sönecektir.

## Sonuç

Bu rehber, JavaScript ile MahirKart'ı kullanmaya başlamanıza yardımcı olmuştur. Rehberin sonunda, bir LED'i yakıp söndürmek için basit bir proje oluşturmayı öğrenmişsinizdir.