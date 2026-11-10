# Referensi File Build

File yang diperlukan untuk mengompilasi sistem Armbian diatur dalam direktorinya masing-masing.

## armbian-files

Direktori ini berisi semua file yang digunakan selama proses build Armbian. Subdirektori `common-files` menyimpan file bersama yang tidak bergantung pada platform, subdirektori `platform-files` menyimpan file khusus platform, dan subdirektori `different-files` menyimpan file konfigurasi khusus perangkat. Untuk detail lebih lanjut, lihat Bagian `12.15` pada [dokumentasi](../documents/).

File firmware yang diperlukan akan diunduh secara otomatis dari repositori [ophub/firmware](https://github.com/ophub/firmware) ke direktori `common-files/usr/lib/firmware`.

## kernel

Buat folder khusus versi di bawah direktori `kernel`, misalnya `stable/5.10.125`. Untuk beberapa kernel, buat direktori terpisah secara berurutan dan letakkan file kernel yang sesuai di masing-masing direktori. File kernel dapat diunduh dari repositori [kernel](https://github.com/ophub/kernel), atau Anda dapat [mengompilasinya sendiri](../compile-kernel). Jika tidak ada file kernel secara lokal, skrip build akan mengunduhnya secara otomatis dari repositori kernel.

## u-boot

File bootloader sistem. Bergantung pada versi kernel, file u-boot yang sesuai akan dikelola secara otomatis oleh skrip instalasi dan pembaruan sesuai kebutuhan. File u-boot yang diperlukan akan diunduh secara otomatis dari repositori [ophub/u-boot](https://github.com/ophub/u-boot) ke direktori `u-boot`.