# Petunjuk Kontrol Tampilan Layar LED

- File konfigurasi terletak di direktori [/usr/share/openvfd](../build-armbian/armbian-files/platform-files/amlogic/rootfs/usr/share/openvfd) pada sistem `Armbian/OpenWrt`. File perintah `Armbian` berada di [/usr/sbin/armbian-openvfd](../build-armbian/armbian-files/platform-files/amlogic/rootfs/usr/sbin/armbian-openvfd), dan file perintah `OpenWrt` berada di [/usr/sbin/openwrt-openvfd](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/make-openwrt/openwrt-files/common-files/usr/sbin/openwrt-openvfd). Jika file-file ini tidak ada di sistem Anda, unggah secara manual dan berikan izin eksekusi: `chmod +x /usr/share/openvfd/vfdservice /usr/sbin/*-openvfd`.

- Perbarui kernel sistem ke versi terbaru. Untuk sistem `Armbian`, gunakan perintah `armbian-sync`. Untuk sistem `OpenWrt`, buka `Menu Sistem` → `Layanan Amlogic` → `Unduh Pembaruan Online`.

- Perangkat berikut telah diuji: `x96max.conf`, `x96maxplus.conf`, `h96max-x3.conf`, `hk1-x3.conf`, `hk1box.conf`, `tx3.conf`, `x96air.conf`, dan `x88pro-x3.conf`. Konfigurasi untuk perangkat lain dapat diadaptasi dari [arthur-liberman/vfd-configurations](https://github.com/arthur-liberman/vfd-configurations) dan [LibreELEC/linux_openvfd](https://github.com/LibreELEC/linux_openvfd/tree/master/conf). Catatan: nilai kolom kedua pada entri konfigurasi dari sumber-sumber ini harus dikurangi `1`. Contohnya:

```yaml
vfd_gpio_clk='0,69,0'
vfd_gpio_dat='0,70,0'
```
Ubah menjadi:

```yaml
vfd_gpio_clk='0,68,0'
vfd_gpio_dat='0,69,0'
```

- Mengambil konfigurasi [x96maxplus](../build-armbian/armbian-files/platform-files/amlogic/rootfs/usr/share/openvfd/conf/x96maxplus.conf) sebagai contoh: Jika urutan teks waktu yang ditampilkan tidak benar, Anda dapat mengubah urutan angka pada `vfd_chars='4,0,1,2,3'` menjadi `vfd_chars='1,2,3,4,0'` untuk pengujian. Jika waktu ditampilkan terbalik, Anda dapat mengubah `nilai pertama 0x02` pada `vfd_display_type='0x02,0x00,0x01,0x00'` menjadi `0x01` untuk pengujian. Konten yang ditampilkan dapat disesuaikan dengan kondisi spesifik perangkat Anda pada `functions='usb apps setup sd hdmi cvbs'`.

- Ganti nama file konfigurasi menjadi `diy.conf` dan unggah ke direktori `/usr/share/openvfd/conf`, lalu masukkan perintah `armbian-openvfd 99` untuk pengujian.

- Perintah `armbian-openvfd 0` menonaktifkan tampilan LED dan membersihkan proses sistem terkait. Sebelum menguji setiap konfigurasi baru, selalu jalankan perintah penonaktifan ini terlebih dahulu, lalu jalankan `armbian-openvfd 99` untuk menguji konfigurasi yang telah diubah.

- Beberapa perangkat mungkin menampilkan pesan boot sebelum Linux dimulai (misalnya menampilkan `BOOT`). Untuk menghapus pesan ini, jalankan terlebih dahulu `armbian-openvfd 0` untuk menghentikan layanan yang ada, lalu jalankan `armbian-openvfd <boxid>` untuk mengambil alih kendali tampilan LED. Untuk menonaktifkan tampilan sepenuhnya, jalankan `armbian-openvfd 0` lagi.

- Setelah tampilan berfungsi dengan benar, tambahkan ke tugas startup saat boot. Ganti `15` pada perintah berikut dengan `BoxID` perangkat Anda:

```yaml
# Jalankan perintah berikut di terminal untuk mengaktifkan layanan openvfd
sed -i 's|^#*openvfd_enable=.*|openvfd_enable="yes"|g' /etc/custom_service/start_service.sh
sed -i 's|^#*openvfd_boxid=.*|openvfd_boxid="15"|g' /etc/custom_service/start_service.sh
# Beberapa perangkat memerlukan restart layanan OpenVFD untuk menghapus pesan 'BOOT' dan pesan terkait
sed -i 's|^#*openvfd_restart=.*|openvfd_restart="yes"|g' /etc/custom_service/start_service.sh
```

- Semua orang dipersilakan untuk menguji dan membagikan file konfigurasi perangkat mereka (diy.conf) demi manfaat bagi komunitas.

| Nama Box | `BoxID` | Perintah Armbian | Perintah OpenWrt | Fungsi |
| --- | --- | --- | --- | --- |
| x96max | 11 | armbian-openvfd 11 | openwrt-openvfd 11 | Aktifkan LED |
| x96maxplus | 12 | armbian-openvfd 12 | openwrt-openvfd 12 | Aktifkan LED |
| x96air | 13 | armbian-openvfd 13 | openwrt-openvfd 13 | Aktifkan LED |
| h96max-x3 | 14 | armbian-openvfd 14 | openwrt-openvfd 14 | Aktifkan LED |
| hk1-x3 | 15 | armbian-openvfd 15 | openwrt-openvfd 15 | Aktifkan LED |
| hk1box | 16 | armbian-openvfd 16 | openwrt-openvfd 16 | Aktifkan LED |
| tx3 | 17 | armbian-openvfd 17 | openwrt-openvfd 17 | Aktifkan LED |
| tx3-mini | 18 | armbian-openvfd 18 | openwrt-openvfd 18 | Aktifkan LED |
| t95 | 19 | armbian-openvfd 19 | openwrt-openvfd 19 | Aktifkan LED |
| t95z-plus | 20 | armbian-openvfd 20 | openwrt-openvfd 20 | Aktifkan LED |
| tx9-pro | 21 | armbian-openvfd 21 | openwrt-openvfd 21 | Aktifkan LED |
| x92 | 22 | armbian-openvfd 22 | openwrt-openvfd 22 | Aktifkan LED |
| whale | 23 | armbian-openvfd 23 | openwrt-openvfd 23 | Aktifkan LED |
| x88pro-x3 | 24 | armbian-openvfd 24 | openwrt-openvfd 24 | Aktifkan LED |
| diy | 99 | armbian-openvfd 99 | openwrt-openvfd 99 | Aktifkan LED |
| - | 0 | armbian-openvfd 0 | openwrt-openvfd 0 | Nonaktifkan LED |
| - | -u | armbian-openvfd -u | openwrt-openvfd -u | Perbarui Konfigurasi |
