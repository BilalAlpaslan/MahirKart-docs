# Rust - Hızlı Başlangıç

Bu rehber, Rust ile MahirKart'ı kullanmaya başlamanıza yardımcı olacaktır. Geliştirme ortamını kurmak, Rust kodumuzu MahirKart'a yüklemek ve LED yaktığımız basit bir proje oluşturmak için adım adım talimatlar içerir.

## Gereksinimler

* Bir MahirKart
* Bir USB Type-C kablosu
* Bir bilgisayar
* Visual Studio Code(veya başka bir geliştirme ortamı)

## Geliştirme Ortamı

Rust programları yazmak ve çalıştırmak için bir geliştirme ortamına ihtiyacınız vardır. Bu rehberde, Visual Studio Code kullanılacaktır. İsterseniz başka bir geliştirme ortamı da kullanabilirsiniz. Bilgisayarınıza Rust kurulu olması yeterlidir.

## Rust Kurulumu

Rust kurulumu için Rustup aracını kullanacağız. Rustup aracını indirmek için aşağıdaki web sitesini ziyaret edin:

https://www.rust-lang.org/tools/install

## Derlenecek platformun eklenmesi

MahirKartın işlemcisi RP2040 ARMv6 mimarisinde olduğu için ilk önce bu mimari için gereken gereksinimleri kurmalıyız. Rustup aracını kullanarak aşağıdaki komutu çalıştırın:

```bash
rustup target add thumbv6m-none-eabi
```

## LED'i Yakıp Söndürmek için Proje Oluşturma

Rust kullanırken HAL yada PAC kütüphanelerini kullanarak donanımı kontrol edebiliriz. Bu rehberde HAL kütüphanesini kullanacağız. Yeni bir proje oluşturmak için terminalden aşağıdaki komutu çalıştırın:

```bash
cargo new --bin mahirkart
```

Gerçekleştirmek istediğimiz işlemler için gerekli olan kütüphaneleri eklemek için `Cargo.toml` dosyasını açın ve şu şekilde düzenleyin:

```toml
[package]
name = "blink-rp2040"
version = "0.1.0"
edition = "2021"

[dependencies]
cortex-m-rt = "0.7.0"
cortex-m = "0.7.0"
rp2040-boot2 = '0.3.0'
rp2040-pac = { git = "https://github.com/rp-rs/rp2040-pac", branch = "main" }
panic-halt = "0.2.0"
rp2040-hal = '0.8.2'
embedded-hal = '0.2.5'
```

Build ayarları için .cargo/config.toml dosyamızıda ARMv6 için ayarlıyoruz:

```toml
# .cargo/config.toml
[target.thumbv6m-none-eabi]
runner = "elf2uf2-rs -d"

rustflags = [
    "-C", "link-arg=-Tlink.x",
    "-C", "link-arg=--nmagic",
]

[build]
target = "thumbv6m-none-eabi" # Cortex-M0, Cortex-M0+
```

Son olarak da MahirKart için memory.x dosyasında bellek ayarlarını tanıtmamız gerekiyor:

```x
MEMORY {
    BOOT2 : ORIGIN = 0x10000000, LENGTH = 0x100
    FLASH : ORIGIN = 0x10000100, LENGTH = 2048K - 0x100
    RAM   : ORIGIN = 0x20000000, LENGTH = 256K
}

EXTERN(BOOT2_FIRMWARE)

SECTIONS {
    /* ### Boot loader */
    .boot2 ORIGIN(BOOT2) :
    {
        KEEP(*(.boot2));
    } > BOOT2
} INSERT BEFORE .text;
```

Kodumuzu yazmak için src/main.rs dosyasını açın ve şu şekilde düzenleyin:

```rust
#![no_std]
#![no_main]

use embedded_hal::digital::v2::OutputPin;
use hal::{pac};
use rp2040_hal as hal;

use panic_halt as _;

#[link_section = ".boot2"]
#[used]
pub static BOOT2: [u8; 256] = rp2040_boot2::BOOT_LOADER_W25Q080;

const XTAL_FREQUENCY_HZ: u32 = 12_000_000u32;

#[cortex_m_rt::entry]
fn main() -> ! {
    let mut pac = pac::Peripherals::take().unwrap();
    let cp = pac::CorePeripherals::take().unwrap();

    let mut watchdog = hal::watchdog::Watchdog::new(pac.WATCHDOG);

    let _clocks = hal::clocks::init_clocks_and_plls(
        XTAL_FREQUENCY_HZ,
        pac.XOSC,
        pac.CLOCKS,
        pac.PLL_SYS,
        pac.PLL_USB,
        &mut pac.RESETS,
        &mut watchdog,
    )
    .ok()
    .unwrap();

    let mut delay = cortex_m::delay::Delay::new(cp.SYST, 125_000_000);

    let sio = hal::sio::Sio::new(pac.SIO);

    let pins = hal::gpio::Pins::new(
        pac.IO_BANK0,
        pac.PADS_BANK0,
        sio.gpio_bank0,
        &mut pac.RESETS,
    );

    let mut led_pin = pins.gpio25.into_push_pull_output();

    loop {
        led_pin.set_high().unwrap();
        delay.delay_ms(1000u32);
        led_pin.set_low().unwrap();
        delay.delay_ms(1000u32);
    }
}
```

Kodu kaydettikten sonra, terminalden aşağıdaki komutu çalıştırın:

```bash
cargo build --release
```

Bu komut ile kodumuzu derleyip uf2 dosyasına çeviriyoruz. Ardından MahirKart'ı bilgisayarınıza bağlayın ve üzerinde bulunan bootsel düğmesine basın. Bu sayede MahirKart bilgisayarınızda bir USB depolama aygıtı olarak görünecektir. Uf2 dosyasını bu USB depolama aygıtına kopyalayın. Uf2 dosyasını kopyaladıktan sonra, MahirKart'ı bilgisayarınızdan çıkarın ve tekrar bağlayın. MahirKart artık Rust kodlarını çalıştırmaya hazır.

## Sonuç

Bu rehber, Rust ile MahirKart'ı kullanmaya başlamanıza yardımcı olmayı hedeflemiştir. Rehberin sonunda kendiniz de LED yakmak için basit bir proje oluşturmayı deneyebilirsiniz.