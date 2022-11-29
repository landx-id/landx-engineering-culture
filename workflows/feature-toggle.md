# Feature Toggle

Referensi: https://martinfowler.com/articles/feature-toggles.html

![feature-toggle-screenshot](/images/feature-toggle.jpeg)

## Use Cases

Feature Toggle digunakan untuk menyembunyikan atau menampilkan suatu fitur secara otomatis. Sangat berguna jika misalnya kita me-release sebuah fitur baru secara otomatis, dengan hanya merubah setting pada dashboard. Tidak hanya itu, pada tools Feature Toggle biasanya terdapat pengaturan untuk mengatur strategi saat menampilkan sebuah fitur. Misalnya, kita hanya ingin menampilkan sebuah fitur pada sekelompok user tertentu saja, atau ditampilkan secara random.

## Implementation

### Using Unleash

Untuk backend Feature Toggle ini, kita menggunakan [Unleash](https://www.getunleash.io/). Unleash mempunyai fitur yang cukup lengkap untuk kasus di LandX dan tersedia versi gratis yang sudah cukup untuk meng-handle hampir semua case terkait feature flag di LandX.

### Using in Application

Untuk menggunakan Unleash di aplikasi, yang harus dilakukan adalah
1. Import library unleash client. Kita menggunakan [Python Unleash Client](https://pypi.org/project/UnleashClient/).
   ```python
   # project.toml
   UnleashClient = "^5.2.0"
   ```
2. Konfigurasi Unleash URL, tokenm, dan service
    ```python
    # cfg.py
    UNLEASH_URL = os.environ.get("UNLEASH_URL", "https://unleash.io")
    UNLEASH_TOKEN = os.environ.get(
        "UNLEASH_TOKEN", "default:development.XXX"
    )
    UNLEASH_SERVICE = "LxWebApp"
    ```
3. Gunakan pada code
    ```python
    from unleash import is_flag_enable

    if is_flag_enable(flag="dividend_payment_method"):
        # Do something
    ```