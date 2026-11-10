<div align="center">
    <img alt="Armbian" src="https://github.com/user-attachments/assets/74e55052-031b-48f8-9aca-e5f1dd9e256a" />
</div>

# Armbian

Armbian adalah distribusi Linux ringan yang dibangun khusus untuk chip ARM, berbasis Debian/Ubuntu. Sistem Armbian ramping, bersih, dan 100% kompatibel dengan Debian/Ubuntu, sehingga mewarisi fungsionalitas serta ekosistem perangkat lunaknya yang kaya. Sistem ini berjalan dengan aman dan stabil di penyimpanan TF/SD/USB maupun eMMC perangkat. Proyek ini menjaga keutuhan sistem Armbian resmi sambil memperluas dukungan untuk perangkat yang tidak didukung secara resmi seperti TV box, serta menambahkan serangkaian perintah manajemen yang praktis. Kini Anda dapat mengganti sistem Android TV pada TV box Anda dengan Armbian dan mengubahnya menjadi server yang andal.

Proyek ini mengandalkan banyak [kontributor](CONTRIBUTORS.md) untuk membangun sistem Armbian bagi perangkat `Amlogic`, `Rockchip`, dan `Allwinner`. Proyek ini mendukung penulisan ke eMMC, pembaruan kernel, dan fitur lainnya. Untuk penggunaan secara rinci, silakan lihat [📚Dokumentasi Pengguna Armbian](./documents). Sistem Armbian terbaru dapat diunduh dari [⬇️Releases](https://github.com/farishhz/amlogic-s9xxx-armbian/releases). Anda dipersilakan untuk melakukan `Fork` dan kustomisasi. Jika proyek ini bermanfaat, silakan klik tombol `⭐Star` di pojok kanan atas untuk menunjukkan dukungan Anda.

## Informasi Default Sistem Armbian

| Nama Sistem | Nama Pengguna Default | Kata Sandi Default | Port SSH | Alamat IP |
| --- | --- | --- | --- | --- |
| 🐧 [Armbian.OS](https://github.com/farishhz/amlogic-s9xxx-armbian/releases) | root | 1234 | 22 | Diperoleh dari router |
| 🐋 [Armbian.Docker](https://hub.docker.com/u/farishhz) | root | 1234 | 22 | IP MacVLAN statis |

## Perangkat yang Didukung

⬆️ Model dari setiap platform (Amlogic/Rockchip/Allwinner) diurutkan berdasarkan performa SoC dari tertinggi ke terendah.

| SoC | [Perangkat](https://github.com/farishhz/amlogic-s9xxx-armbian/releases) | [Kernel](https://github.com/ophub/kernel) |
| --- | --- | --- |
| a311d | Khadas-VIM3, WXY-OES | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s922x | Beelink-GT-King, Beelink-GT-King-Pro, Ugoos-AM6-Plus, ODROID-N2, X88-King, Ali-CT2000, WXY-OES-Plus | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905x3 | X96-Max+, HK1-Box, Vontar-X3, H96-Max-X3, Ugoos-X3, TX3(QZ), TX3(BZ), X96-Air, X96-Max+_A100, A95X-F3-Air, Tencent-Aurora-3Pro(s905x3-b), X96-Max+Q1, X96-Max+100W, X96-Max+_2101, Infinity-B32, Whale, X88-Pro-X3, X99-Max-Plus, Transpeed-X3-Plus, TOX1, Khadas-VIM3L, YZD-S18 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905x2 | X96Max-4G, X96Max-2G, MECOOL-KM3-4G, Tanix-Tx5-Max, A95X-F2, HG680-FJ, ZTE-B860H-V5, ZTE-W103D | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905l3a | [E900V22C/D](https://github.com/Calmact/e900v22c), CM311-1a-YST, M401A, M411A, UNT403A, UNT413A, ZTE-B863AV3.2-M, CM311-1a-CH, IP112H, B863AV3.1-M2 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905l3b | CM201-1, CM211-1, CM311-1, E900V21D, E900V22D, E900V21E, E900V22E, M302A/M304A, Hisense-IP103H, TY1608, TY1608, MGV2000, B860AV-2.1M, UNT403A, RG020ET-CA, M411A | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905l3 | CM211-1, CM311-1, HG680-LC, M401A, UNT400G1, UNT400G, UNT402A, ZXV10-BV310, M411A, ZXV10-B860AV3.2-M, ZXV10-B860AV2.1-U, E900V22D-2, CM201-1-6-YS, IP108H, M301A, B860AV2.1-A | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s912 | Tanix-TX8-Max, Tanix-TX9-Pro(3G), Tanix-TX9-Pro(2G), Tanix-TX92, Tanix-TX9S, Nexbox-A1, [Nexbox-A95X-A2](https://www.cafago.com/en/p-v2979eu-2g.html),  A95X, H96-Pro-Plus, VORKE-Z6-Plus, Mecool-M8S-PRO-L, Vontar-X92, T95Z-Plus, Octopus-Planet, Phicomm-T1, TX3-Mini, OneCloudPro-V1.1_V1.2 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905d | MECOOL-KI-Pro, Phicomm-N1, SML-5442TW | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905x | HG680P, B860H, TBee-Box, T95, TX9, XiaoMI-3S, X96, Nexbox-a95x, BTV-9, BTV-10(BX) | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905mb | S65 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905l | UNT402A, M201-S, MiBox-4, MiBox-4C, MG101, E900V21C, IP108H-53u1m, Tencent-Aurora-1s, B860AV2.1, B860AV2.1U, HM201, XiaoMI-4C | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905l2 | MGV2000, MGV2000-K, MGV3000, Wojia-TV-IPBS9505, M301A, E900v21E, e900v21d, CM201-1, IP108H, MGV2000-CW | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905lb | Q96-mini, BesTV-R3300L, SumaVision-Q7, MG101, s65, IPBS9505 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905w | X96-Mini, TX3-Mini, W95, X96W/FunTV, MXQ-Pro-4K, MeCool-m8s-pro-W | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| s905 | Beelink-Mini-MX-2G, Sunvell-T95M, MXQ-Pro+4K, SumaVision-Q5 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| rk3588(s) | Radxa-Rock5B, Radxa-Rock5C, Orange-Pi-5-Plus, Orange-Pi-5-Pro, Orange-Pi-5-Ultra, Beelink-IPC-R, HLink-H88K, HLink-H88K-V3, NanoPC-T6, Smart-Am60, DC-A588, Orangepi-5B, CM3588-NAS, Rock-5-ITX, LZ-D3588, Boca-tcn100, Boca-tcn200, Firefly-ITX-3588J, Indiedroid-Nova, LubanCat-4, Seewo-SV50, EasePi-R2, BDY-G98, Youyeetoo-YY3588, Youyeetoo-R1-V3, ELFboard-elf2, ALIENTEK-QuarkPi-CA2, LubanCat-5 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk3588](https://github.com/ophub/kernel/releases/tag/kernel_rk3588) |
| rk3576 | NanoPi-m5, LCKFB-Taishan-Pi-3M, reComputer-rk3576-Devkit, LubanCat-3 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3399 | EAIDK-610, King3399, TN3399, Kylin3399, ZCube1-Max, CRRC, SMART-AM40, SW799, ZYSJ, DG-3399, DLFR100, Emb3531, Leez-p710, tvi3315a, xiaobao, Fine3399, Firefly-RK3399, LX-R3S, Hugsun-x99, Tb-ls3399, Hisense-hs530r, Tpm312, ZK-rk39a, YSKJ, Fmx1-Pro, Fmx1-Pro-B, Sv-33a6x, Sv-33a6x(VPU), AIO-3399B, AIO-3399C, AIO-3399C(AI), TaraM, NanoPC-T4, Firefly-Core-3399-JD4, GEA-6319, NanoPi-SOM-RK3399, SZ3390, H339PC, K4(LZK4), TPS781, AI3399-C | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3568 | FastRhino-R66S, FastRhino-R68S, [Radxa-E25](https://wiki.radxa.com/Rock3/CM/CM3I/E25), NanoPi-R5S, NanoPi-R5C, HLink-H66K, HLink-H68K, HLink-H69K, Seewo-sv21, Mrkaio-m68s, Swan1-w28, Ruisen-box, DG-TN3568, Alark35-3500, MMBox-Anas3035, Wocyber-A3, Photonicat, NSY-G16-Plus, NSY-G68-Plus, BDY-G18-Pro, Gzpeite-P01, LZ-D3568, LZ-K3568, BDKJ-One, Station-P2, Lyt-t68m, LubanCat-2, Rock-3A, Rock-3B, EasePi-A2, Roceos-K40Pro, DG-Nas-Lite, Houzzkit-F1, Youyeetoo-YY3568, DC_A568, Z93A | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3566 | Panther-X2, JP-TvBox, LCKFB-Taishan-Pi, WXY-OEC-turbo-4g, Station-M2, Orange-Pi-3B, X88Pro20, LubanCat-1, Rock-3C, Inspur-MD1000, KICKPI-K11C-V12, Torder-R10D | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3528 | HLink-H28K, Radxa-E20C, H96-Max-M2, HK1-Rbox-K8S, HT2, CD1000, P51(X88-Pro-13), XingYiCloud, P52(VNPT-MyTV-Net-1) | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3328 | BeikeYun, Chainedbox-L1-Pro, Station-M1, Bqeel-MVR9, Renegade/Firefly | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable)<br />[rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) |
| rk3318 | RX3318-Box | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| h618 | OrangePi-Zero3, H618-DevBoard(PCDN), Vontar-h618, BT-100M, BT-1000M, PaiNet-P3, PaiNet-P5, X98H, X98H-100MiB, AI-Douhe, CJDS | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| h6 | Vplus, Tanix-TX6, TX6-H, T95-max, TQC-A01 | [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable) |

> [!TIP]
> Saat ini, box s905 hanya dapat digunakan dengan `TF/SD/USB`; model box lainnya mendukung penulisan ke `EMMC`. Untuk informasi lebih lanjut, lihat [✅ Daftar Perangkat yang Didukung](build-armbian/armbian-files/common-files/etc/model_database.conf). Untuk menambahkan dukungan perangkat baru, lihat Bagian 12.15 dalam dokumentasi: [✳️Menambahkan Perangkat Baru yang Didukung](documents/README.md#1215-cara-menambahkan-perangkat-baru-yang-didukung). Silakan baca [📚Dokumentasi Pengguna Armbian](./documents) sebelum digunakan, karena dokumentasi tersebut menyediakan solusi untuk masalah-masalah umum.

## Petunjuk Instalasi dan Pembaruan Armbian

Pilih sistem Armbian yang sesuai dengan model perangkat Anda. Lihat dokumentasi terkait untuk petunjuk penggunaan khusus perangkat.

- ### Instal Armbian ke EMMC

1. Untuk perangkat platform `Rockchip`, lihat [Bab 8](documents#8-menginstal-armbian-ke-emmc) dalam dokumentasi.

2. Untuk perangkat platform `Amlogic` dan `Allwinner`, gunakan alat seperti [Rufus](https://rufus.ie/) atau [balenaEtcher](https://www.balena.io/etcher/) untuk menulis sistem ke flashdisk USB, lalu colokkan flashdisk USB tersebut ke perangkat. Masuk ke sistem Armbian (pengguna default: root, kata sandi default: 1234) dan masukkan perintah:

```shell
armbian-install
```

| Opsional | Default | Pilihan | Keterangan |
| --- | --- | --- | --- |
| -m | no | yes/no | Gunakan u-boot mainline |
| -a | yes | yes/no | Gunakan alat penyesuaian partisi [ampart](https://github.com/7Ji/ampart) |
| -l | no | yes/no | Tampilkan daftar perangkat lengkap |

Contoh: `armbian-install -m yes -a no`

- ### Perbarui Kernel Armbian

Masuk ke sistem Armbian dan masukkan perintah:

```shell
# Jalankan sebagai pengguna root (sudo -i)
# Jika tidak ada parameter yang ditentukan, kernel akan diperbarui ke versi terbaru.
armbian-update
```

| Opsional | Default | Pilihan | Keterangan |
| --- | --- | --- | --- |
| -r | ophub/kernel | `<owner>/<repo>` | Atur repositori di github.com untuk mengunduh kernel |
| -u | Otomatis | stable/flippy/beta/rk3588/rk35xx | Atur [akhiran tags](https://github.com/ophub/kernel/releases) kernel |
| -k | Versi terbaru | Versi kernel | Atur [versi kernel](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| -b | yes | yes/no | Cadangkan secara otomatis kernel yang sedang digunakan saat pembaruan |
| -d | deb | tar/deb | Atur format paket kernel yang diutamakan. Jika tidak tersedia, skrip akan otomatis mencoba format alternatif. Format `deb` direkomendasikan untuk mengompilasi driver kustom. |
| -m | no | yes/no | Gunakan u-boot mainline |
| -s | none | none/DiskName | [SOS] Pulihkan kernel sistem di eMMC/NVMe/sdX atau disk lainnya |
| -h | none | none | Lihat informasi bantuan |

Contoh: `armbian-update -k 5.15 -u stable -d deb`

Saat menentukan versi kernel melalui parameter `-k`, Anda dapat memberikan nomor versi yang persis (misalnya, `armbian-update -k 5.15.50`) atau hanya menentukan seri kernel (misalnya, `armbian-update -k 5.15`). Jika seri yang ditentukan, versi terbaru dalam seri tersebut akan digunakan secara otomatis.

Selama pembaruan kernel, kernel yang sedang berjalan akan dicadangkan secara otomatis ke direktori `/ddbr/backup`, dengan menyimpan 3 versi terbaru. Jika kernel yang baru diinstal ternyata tidak stabil, Anda dapat memulihkan kernel cadangan kapan saja. Jika pembaruan kernel membuat sistem tidak dapat boot, gunakan `armbian-update -s` untuk memulihkan kernel sistem. Untuk detail lebih lanjut, lihat [Dokumen Bantuan](documents#10-memperbarui-kernel-armbian).

- ### Ganti Sumber Armbian

Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-apt
```

Memilih sumber perangkat lunak yang sesuai untuk negara atau wilayah Anda dapat meningkatkan kecepatan unduhan secara signifikan. Untuk detail lebih lanjut, lihat [Dokumen Bantuan](documents#11-menginstal-perangkat-lunak-umum).

- ### Instal Perangkat Lunak Umum

Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-software
```

Perintah `armbian-software -u` memperbarui daftar pusat perangkat lunak lokal. Berdasarkan masukan pengguna di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), [perangkat lunak](build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) yang umum digunakan telah diintegrasikan secara bertahap dengan dukungan instal/perbarui/hapus instalan sekali klik. Ini mencakup `image Docker`, `perangkat lunak desktop`, `layanan aplikasi`, dan lainnya. Lihat [petunjuk lengkapnya](documents/armbian_software.md).

- ### Ubah Konfigurasi Armbian

Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-config
```

- ### Buat Swap untuk Armbian

Jika Anda merasa memori perangkat tidak mencukupi saat menjalankan aplikasi yang membutuhkan banyak memori seperti `Docker`, Anda dapat membuat partisi memori virtual `swap` untuk menggunakan sebagian ruang disk sebagai memori tambahan. Satuan parameternya adalah `GB`, dengan nilai default `1`.

Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-swap 1
```

- ### Kontrol Tampilan LED

Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-openvfd
```

Lakukan debug sesuai dengan [Petunjuk Kontrol Tampilan Layar LED](documents/led_screen_display_control.md).

- ### Cadangkan/Pulihkan Sistem Asli EMMC

Mendukung pencadangan dan pemulihan partisi `EMMC` perangkat melalui `TF/SD/USB`. Sebelum menginstal Armbian pada perangkat baru, disarankan untuk mencadangkan sistem Android TV asli agar dapat dipulihkan di kemudian hari jika diperlukan.

Boot sistem Armbian dari `TF/SD/USB` dan masukkan perintah:

```shell
armbian-ddbr
```

Masukkan `b` pada prompt untuk mencadangkan sistem, atau `r` untuk memulihkan.

> [!IMPORTANT]
> Sebagai alternatif, sistem Android dapat di-flash langsung ke eMMC melalui kabel USB. Image sistem Android tersedia di [Tools](https://github.com/ophub/kernel/releases/tag/tools).

- ### Kompilasi Kernel di Armbian

Untuk petunjuk kompilasi kernel, lihat dokumentasi [Kompilasi Kernel](compile-kernel). Masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-kernel -u
armbian-kernel -k 6.6.12
```

- ### Petunjuk Penggunaan Lainnya

Untuk memperbarui semua skrip layanan dalam sistem ke versi terbaru, masuk ke sistem Armbian dan masukkan perintah:

```shell
armbian-sync
```

Untuk masalah umum dan solusinya saat menggunakan Armbian, lihat [dokumentasi](documents).

## Pengemasan Lokal

1. Clone repositori ke lokal `git clone --depth 1 https://github.com/farishhz/amlogic-s9xxx-armbian.git`

2. Instal paket perangkat lunak yang diperlukan (menggunakan Ubuntu 24.04 sebagai contoh)

Masuk ke direktori root `~/amlogic-s9xxx-armbian`, lalu jalankan perintah instalasi:

```shell
sudo apt-get update -y
sudo apt-get full-upgrade -y
# Untuk Ubuntu-24.04
sudo apt-get install -y $(cat compile-kernel/tools/script/ubuntu2404-build-armbian-depends)
```

3. Masuk ke direktori root `~/amlogic-s9xxx-armbian`, buat folder `build/output/images`, lalu unggah file image Armbian (misalnya, `Armbian_21.11.0-trunk_Odroidn2_current_5.15.50.img`) ke direktori `~/amlogic-s9xxx-armbian/build/output/images`. Pertahankan nomor versi rilis (misalnya, `21.11.0`) dan nomor versi kernel (misalnya, `5.15.50`) pada nama file asli, karena keduanya akan digunakan untuk penamaan sistem Armbian yang dibangun ulang.

4. Masuk ke direktori root `~/amlogic-s9xxx-armbian` dan jalankan `sudo ./rebuild -b s905x3 -k 6.6.12` untuk menghasilkan image Armbian bagi board yang ditentukan. File keluaran disimpan di direktori `build/output/images`.

- ### Keterangan Parameter Pengemasan Lokal

| Parameter | Arti | Keterangan |
| --- | --- | --- |
| -b | Board | Menentukan nama kode perangkat target (default-nya `all`). Anda dapat menentukan satu perangkat (misalnya, `-b s905x3`) atau menghubungkan beberapa nama kode dengan garis bawah untuk mengompilasinya bersama-sama (misalnya, `-b s905x3_s905d`). Parameter ini juga mendukung kata kunci khusus untuk kompilasi massal: `all` mengompilasi semua perangkat dalam basis data, `first50` mengompilasi 50 perangkat pertama, `range50_100` mengompilasi perangkat ke-51 hingga ke-100 (begitu pula untuk `range100_150`), dan `last20` mengompilasi 20 perangkat terakhir. Selain itu, Anda dapat mengompilasi berdasarkan platform perangkat keras (`amlogic`, `rockchip`, `allwinner`) untuk membangun semua image bagi platform tersebut, misalnya, `-b amlogic`. Menambahkan angka pada nama platform memungkinkan Anda mengompilasi rentang tertentu dalam daftar dukungan platform tersebut; misalnya, `-b amlogic50` membangun 50 perangkat pertama di platform Amlogic, dan `-b amlogic50_100` membangun perangkat ke-51 hingga ke-100. Untuk daftar lengkap nama kode perangkat yang didukung, silakan lihat item konfigurasi `BOARD` di [model_database.conf](build-armbian/armbian-files/common-files/etc/model_database.conf). Default: `all` |
| -r | KernelRepo | Tentukan `<owner>/<repo>` dari repositori kernel di github.com. Default: `ophub/kernel` |
| -u | kernelUsage | Atur `akhiran tags` dari kernel yang digunakan, seperti [stable](https://github.com/ophub/kernel/releases/tag/kernel_stable), [flippy](https://github.com/ophub/kernel/releases/tag/kernel_flippy), [beta](https://github.com/ophub/kernel/releases/tag/kernel_beta). Default: `stable` |
| -k | Kernel | Tentukan [versi kernel](https://github.com/ophub/kernel/releases/tag/kernel_stable), seperti `-k 6.6.12`. Hubungkan beberapa kernel dengan `_`, seperti `-k 6.6.12_5.15.50`. Versi kernel yang ditentukan secara bebas melalui parameter `-k` hanya berlaku untuk kernel yang menggunakan `stable/flippy/beta`. Seri kernel lain seperti [rk3588](https://github.com/ophub/kernel/releases/tag/kernel_rk3588) / [rk35xx](https://github.com/ophub/kernel/releases/tag/kernel_rk35xx) hanya dapat menggunakan kernel tertentu. |
| -a | AutoKernel | Atur apakah akan otomatis menggunakan kernel terbaru dalam seri yang sama. Jika `true`, repositori kernel akan diperiksa untuk mencari versi yang lebih baru dalam seri yang ditentukan oleh `-k` (misalnya, 6.6.12), dan jika ditemukan, versi terbaru akan digunakan secara otomatis. Jika `false`, versi yang ditentukan secara persis akan digunakan. Default: `true` |
| -t | RootfsType | Atur jenis sistem file partisi ROOTFS. Pilihan: `ext4` atau `btrfs`. Contoh: `-t btrfs`. Default: `ext4` |
| -s | Size | Atur ukuran partisi image. Untuk mengatur partisi ROOTFS saja, tentukan satu nilai (misalnya, `-s 2560`). Untuk mengatur BOOTFS dan ROOTFS sekaligus, gabungkan dengan `/` (misalnya, `-s 512/2560`). Default: `512/2560` |
| -n | BuilderName | Atur tanda tangan pembangun sistem Armbian. Jangan sertakan spasi. Default: tidak ada |

- `sudo ./rebuild`: Gunakan konfigurasi default untuk mengemas semua model perangkat.
- `sudo ./rebuild -b s905x3 -k 6.6.12`: Direkomendasikan. Bangun dengan konfigurasi default untuk kernel yang ditentukan.
- `sudo ./rebuild -b s905x3 -k 6.1.y`: Bangun dengan konfigurasi default, menggunakan kernel terbaru dalam seri 6.1.y.
- `sudo ./rebuild -b s905x3_s905d -k 6.6.12_5.15.50`: Bangun dengan konfigurasi default untuk beberapa kernel sekaligus. Gunakan `_` untuk menggabungkan beberapa kernel.
- `sudo ./rebuild -b s905x3 -k 6.6.12 -s 2560`: Bangun satu kernel dan satu model dengan konfigurasi default; ukuran partisi ROOTFS diatur ke 2560 MiB.
- `sudo ./rebuild -b s905x3_s905d`: Bangun semua kernel untuk beberapa model dengan konfigurasi default. Gunakan `_` untuk menggabungkan beberapa model.
- `sudo ./rebuild -k 6.6.12_5.15.50`: Bangun semua model dengan konfigurasi default dan beberapa kernel yang ditentukan. Gunakan `_` untuk menggabungkan kernel.
- `sudo ./rebuild -k 6.6.12_5.15.50 -a true`: Sama seperti di atas, dengan peningkatan otomatis ke kernel terbaru dalam setiap seri.
- `sudo ./rebuild -t btrfs -s 2560 -k 6.6.12`: Bangun semua model dengan sistem file btrfs, ROOTFS 2560 MiB, dan kernel 6.6.12.

## Gunakan GitHub Actions untuk Kompilasi

1. File konfigurasi workflow terletak di direktori [.github/workflows/](.github/workflows/).

2. Build Baru: Di halaman [Actions](https://github.com/farishhz/amlogic-s9xxx-armbian/actions), pilih ***`Build Armbian server image`*** untuk menggunakan workflow [build-armbian-arm64-server-image.yml](.github/workflows/build-armbian-arm64-server-image.yml). Anda dapat memilih dari seri Ubuntu (misalnya, `resolute`) atau seri Debian (misalnya, `trixie`). Klik ***`Run workflow`*** untuk memulai build.

3. Build Ulang: Jika [Releases](https://github.com/farishhz/amlogic-s9xxx-armbian/releases) sudah berisi file `Armbian_.*-trunk_.*.img.gz` yang telah dikompilasi dan Anda hanya perlu mengemas ulang untuk board lain, lewati langkah kompilasi kode sumber dan gunakan [build-armbian-using-releases-files.yml](.github/workflows/build-armbian-using-releases-files.yml) untuk build sekunder.

4. Untuk menggunakan sistem Armbian lain (misalnya, image [odroidn2](https://armbian.tnahosting.net/dl/odroidn2/archive/) dari situs unduhan resmi [armbian.tnahosting.net](https://armbian.tnahosting.net/dl/)), cukup rujuk skrip repositori ini di file workflow [build-armbian-using-official-image.yml](.github/workflows/build-armbian-using-official-image.yml) untuk restrukturisasi Armbian agar mendukung perangkat lain. Contoh:

```yaml
- name: Build Armbian
  uses: farishhz/amlogic-s9xxx-armbian@main
  with:
    build_target: armbian
    armbian_path: build/output/images/*.img
    armbian_board: s905d_s905x3_s922x_s905x
    armbian_kernel: 6.12.y_6.18.y
```

- ### Keterangan Parameter Input GitHub Actions

Parameter-parameter ini sesuai dengan opsi perintah pengemasan lokal yang dijelaskan di atas.

| Parameter | Default | Keterangan |
| --- | --- | --- |
| armbian_path | Tidak ada | Atur path file Armbian asli. Mendukung path file di workflow (misalnya, `build/output/images/*.img`) dan URL unduhan jaringan (misalnya, `https://dl.armbian.com/*/Armbian_*.img.xz`). |
| armbian_board | all | Atur `board` dari box yang dikemas, lihat `-b` |
| kernel_repo | ophub/kernel | Tentukan `<owner>/<repo>` dari repositori kernel di github.com, lihat `-r` |
| kernel_usage | stable | Atur `akhiran tags` dari kernel yang digunakan. Lihat `-u` |
| armbian_kernel | 6.12.y_6.18.y | Atur [versi](https://github.com/ophub/kernel/releases/tag/kernel_stable) kernel, lihat `-k` |
| auto_kernel | true | Atur apakah akan otomatis menggunakan versi terbaru dari kernel dalam seri yang sama, lihat `-a` |
| armbian_fstype | ext4 | Atur jenis sistem file partisi ROOTFS sistem, lihat `-t` |
| armbian_size | 512/2560 | Atur ukuran partisi BOOTFS dan ROOTFS sistem, lihat `-s` |
| armbian_files | false | Tambahkan file Armbian kustom. Jika diatur, semua file di direktori ini akan disalin ke [common-files](build-armbian/armbian-files/common-files). Struktur direktori harus mencerminkan direktori root Armbian agar file ditimpa dengan benar (misalnya, file konfigurasi default harus diletakkan di bawah `etc/default/`). |
| builder_name | Tidak ada | Atur tanda tangan pembangun sistem Armbian, lihat `-n` |

- ### Keterangan Variabel Output GitHub Actions

Mengunggah ke `Releases` memerlukan `Workflow read and write permissions` untuk repositori. Lihat [petunjuk penggunaan](documents/README.md#2-atur-variabel-privat-github_token) untuk detailnya.

| Parameter | Default | Keterangan |
| --- | --- | --- |
| ${{ env.PACKAGED_OUTPUTPATH }} | out | Path keluaran file sistem Armbian |
| ${{ env.PACKAGED_OUTPUTDATE }} | 04.13.1058 | Tanggal pengemasan (bulan.tanggal.jammenit) |
| ${{ env.PACKAGED_STATUS }} | success | Status pengemasan: success / failure |

## Bangun Image Docker Armbian

Untuk membuat image [Docker](https://hub.docker.com/u/farishhz) dari sistem Armbian, lihat skrip build [armbian_docker](./compile-kernel/tools/script/docker).

## Kompilasi Kernel Menggunakan GitHub Actions

Untuk petunjuk kompilasi kernel, lihat [compile-kernel](compile-kernel).

```yaml
- name: Compile the kernel
  uses: farishhz/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 6.12.y_6.18.y
    kernel_auto: true
    kernel_sign: -yourname
```

## Kontributor Armbian

Pertama-tama, terima kasih kepada [150balbes](https://github.com/150balbes), [farishhz](https://github.com/farishhz), dan [unifreq](https://github.com/unifreq) atas kontribusinya yang luar biasa dan fondasi kokoh yang telah diletakkan untuk menjalankan Armbian di TV box Amlogic. Sistem [Armbian](https://github.com/armbian/build) yang dikompilasi di sini langsung menggunakan kode sumber resmi terbaru untuk kompilasi secara real-time. Rancangan program ini mengacu pada tutorial dari para penulis seperti [ebkso](https://www.kflyo.com/howto-compile-armbian-for-n1-box). Terima kasih kepada Anda semua atas dedikasi dan kesediaan berbagi, sehingga kita dapat menjalankan sistem Armbian di lebih banyak perangkat.

[u-boot](https://github.com/ophub/u-boot), [kernel](https://github.com/ophub/kernel), dan sumber daya lain yang digunakan dalam sistem ini terutama berasal dari proyek [unifreq/openwrt_packit](https://github.com/unifreq/openwrt_packit). Beberapa file telah dikontribusikan oleh pengguna melalui [Pull Requests](https://github.com/farishhz/amlogic-s9xxx-armbian/pulls) dan [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues) di proyek-proyek seperti [amlogic-s9xxx-openwrt](https://github.com/ophub/amlogic-s9xxx-openwrt), [amlogic-s9xxx-armbian](https://github.com/farishhz/amlogic-s9xxx-armbian), [luci-app-amlogic](https://github.com/ophub/luci-app-amlogic), [u-boot](https://github.com/ophub/u-boot), dan [kernel](https://github.com/ophub/kernel). Sebagai bentuk penghargaan kepada para perintis dan kontributor ini, semua kontribusi sejak repositori dibuat (`2021-09-19`) dicatat dalam [CONTRIBUTORS.md](https://github.com/farishhz/amlogic-s9xxx-armbian/blob/main/CONTRIBUTORS.md). Sekali lagi terima kasih kepada semua pihak yang telah memberikan kehidupan dan manfaat baru bagi perangkat-perangkat ini.

## Distribusi Lainnya

- Proyek [amlogic-s9xxx-openwrt](https://github.com/ophub/amlogic-s9xxx-openwrt) menyediakan sistem `OpenWrt` untuk TV box, yang juga dapat digunakan pada perangkat yang didukung Armbian.
- Proyek [fnnas](https://github.com/ophub/fnnas) menyediakan sistem `FnNAS` untuk TV box, yang juga dapat digunakan pada perangkat yang didukung Armbian.
- [unifreq](https://github.com/unifreq/openwrt_packit) telah membuat sistem `OpenWrt` untuk berbagai perangkat Amlogic, Rockchip, dan Allwinner, dan menjadi proyek acuan di komunitas. Sangat direkomendasikan.
- [Scirese](https://github.com/Scirese/alarm) telah menguji proses build, instalasi, dan penggunaan sistem `Arch Linux ARM` / `Manjaro` pada Android TV box. Lihat repositorinya untuk detailnya.
- [7Ji](https://7ji.github.io/) telah menerbitkan artikel tentang rekayasa balik dan pengembangan untuk platform Amlogic, mencakup topik seperti instalasi ArchLinux ARM dan analisis mekanisme boot Amlogic. Proyeknya, [ampart](https://github.com/7Ji/ampart), menyediakan alat partisi untuk membaca dan menyunting tabel partisi eMMC Amlogic serta partisi DTB, sehingga ruang eMMC dapat dimanfaatkan 100%. Proyek [amlogic-s9xxx-archlinuxarm](https://github.com/7Ji/amlogic-s9xxx-archlinuxarm) menyediakan petunjuk build dan penggunaan `Arch Linux ARM`. Proyek [YAopenvfD](https://github.com/7Ji/YAopenvfD) menawarkan implementasi daemon openvfd alternatif.
- [13584452567](https://github.com/13584452567) adalah perintis dukungan perangkat `Rockchip` di repositori ini. Melalui kontribusinya, dukungan diperluas untuk banyak perangkat `Rockchip` termasuk EAIDK-610, King3399, TN3399, Kylin3399, ZCube1-Max, tvi3315a, xiaobao, dan lainnya. Ia juga memelihara [kernel](https://github.com/13584452567/linux-6.6.y) khusus untuk perangkat `Allwinner` seperti TQC-A01, serta telah memberikan banyak dukungan teknis dan solusi di Discussions dan [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), sehingga memberikan kontribusi yang signifikan bagi komunitas.
- [cooip-jm](https://github.com/cooip-jm) membagikan banyak panduan tentang Armbian, LXC, Docker, AdGuard, dan aplikasi lainnya di [wiki](https://github.com/cooip-jm/About-openwrt/wiki) miliknya. Direkomendasikan untuk dibaca.
- [weixr18](https://github.com/weixr18) membagikan skill bring-up/porting Linux untuk board Rockchip dalam proyek open-source mereka, [rk-linux-bringup-skill](https://github.com/weixr18/rk-linux-bringup-skill). Dengan skill ini, agen AI dapat berperan sebagai mitra pengembangan Anda, memandu Anda dalam mem-porting board lama yang hanya menjalankan firmware bawaan pabrik ke Armbian atau Linux mainline.

## Tautan

- [armbian](https://github.com/armbian/build)
- [unifreq](https://github.com/unifreq)
- [kernel.org](https://kernel.org)

## Lisensi

amlogic-s9xxx-armbian © OPHUB dilisensikan di bawah [GPL-2.0](LICENSE)
