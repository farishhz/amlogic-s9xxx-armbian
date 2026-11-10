# Panduan Kompilasi dan Penggunaan Kernel

Kernel hasil kompilasi kompatibel dengan sistem `Armbian` maupun `OpenWrt`. Kernel ini dapat digunakan dalam proyek seperti [amlogic-s9xxx-armbian](https://github.com/farishhz/amlogic-s9xxx-armbian), [amlogic-s9xxx-openwrt](https://github.com/ophub/amlogic-s9xxx-openwrt), [flippy-openwrt-actions](https://github.com/ophub/flippy-openwrt-actions), dan [unifreq/openwrt_packit](https://github.com/unifreq/openwrt_packit). Kernel dapat diintegrasikan saat kompilasi firmware atau diinstal ke sistem yang sudah ada.

Anda dapat menyesuaikan konfigurasi kernel sesuai kebutuhan—misalnya, menambahkan driver dan patch. Anda juga dapat mengompilasi kernel pribadi dengan tanda tangan kustom, seperti `5.10.95-happy-new-year`, `5.10.96-beijing-winter-olympics`, `5.10.99-valentines-day`, dan sebagainya.

## Repositori Kernel

Kernel yang sudah dikompilasi tersedia di [Releases](https://github.com/ophub/kernel/releases) dari [ophub/kernel](https://github.com/ophub/kernel).

## Kompilasi Lokal

- ### Menjalankan di Sistem Ubuntu

1. Klon repositori ke lokal: `git clone --depth 1 https://github.com/farishhz/amlogic-s9xxx-armbian.git`

2. Instal paket yang diperlukan (untuk Ubuntu 24.04):

Masuk ke direktori root `~/amlogic-s9xxx-armbian`, lalu jalankan perintah instalasi:

```yaml
sudo apt-get update -y
sudo apt-get full-upgrade -y
# Untuk Ubuntu-24.04
sudo apt-get install -y $(cat compile-kernel/tools/script/ubuntu2404-build-armbian-depends)
```

3. Masuk ke direktori root `~/amlogic-s9xxx-armbian`, lalu jalankan `sudo ./recompile -k 5.15.100` atau parameter lain yang ditentukan untuk mengompilasi kernel. Skrip secara otomatis mengunduh dan menginstal lingkungan build serta kode sumber kernel, dan menyelesaikan semua konfigurasi yang diperlukan. File kernel hasil kompilasi disimpan di direktori `compile-kernel/output` dalam pohon sumber, atau di direktori yang ditentukan dengan opsi `-h`.

- ### Menjalankan di Sistem Armbian

Anda dapat mengompilasi kernel langsung di sistem [Armbian](https://github.com/farishhz/amlogic-s9xxx-armbian/releases), atau menjalankan sistem Armbian di dalam kontainer [Docker](https://hub.docker.com/u/farishhz) pada Ubuntu/Debian untuk mengompilasi kernel. Untuk petunjuk pembuatan image Docker Armbian, lihat skrip build [armbian_docker](./tools/script/docker).

1. Perbarui lingkungan build lokal dan file konfigurasi: `armbian-kernel -u`

2. Kompilasi kernel: Jalankan `armbian-kernel -k 5.15.100` atau parameter lain yang ditentukan untuk mengompilasi kernel. Skrip secara otomatis mengunduh dan menginstal lingkungan build serta kode sumber kernel, dan menyelesaikan semua konfigurasi yang diperlukan. File kernel hasil kompilasi disimpan di direktori `/opt/kernel/compile-kernel/output`.

- ### Referensi Parameter Kompilasi Lokal

| Parameter | Arti | Deskripsi |
| --- | --- | --- |
| -r | Repository | Menentukan repositori kode sumber kernel untuk kompilasi. Anda dapat memilih repositori kode sumber kernel dari `github.com`, misalnya `-r unifreq`. Format parameter mendukung kombinasi tiga komponen: `owner/repo@branch`. Nama pemilik `owner` wajib diisi; nama repositori `/repo` dan nama branch `@branch` bersifat opsional. Jika hanya nama pemilik yang ditentukan, skrip secara otomatis mencocokkan repositori bernama `linux-5.x.y` pada branch `main` milik pemilik tersebut. Jika nama repositori atau nama branch berbeda, tentukan secara kombinasi, misalnya `owner@branch`, `owner/repo`, atau `owner/repo@branch`. Default: `unifreq` |
| -k | Kernel | Menentukan versi kernel, misalnya `-k 5.15.100`. Beberapa kernel dipisahkan dengan `_`, misalnya `-k 5.15.100_5.15.50`. Penggunaan `-k all` mengompilasi semua kernel mainline, saat ini setara dengan `-k 5.10.y_5.15.y_6.1.y_6.6.y_6.12.y_6.18.y`. Daftar kernel disesuaikan secara dinamis berdasarkan status pemeliharaan repositori sumber upstream [unifreq](https://github.com/unifreq). |
| -a | AutoKernel | Mengatur apakah akan otomatis menggunakan versi terbaru dalam seri kernel yang sama. Jika diatur ke `true`, skrip memeriksa apakah ada versi yang lebih baru dalam seri yang sama dengan kernel yang ditentukan melalui `-k` (misalnya `5.15.100`), dan otomatis beralih ke versi terbaru jika tersedia. Jika diatur ke `false`, versi kernel yang ditentukan dikompilasi apa adanya. Default: `true` |
| -m | MakePackage | Mengatur daftar paket untuk membangun kernel. Jika diatur ke `all`, semua file termasuk `Image, modules, dtbs` akan dibangun. Jika diatur ke `dtbs`, hanya 3 file DTB yang dihasilkan. Default: `all` |
| -f | configFlavor | Menentukan file konfigurasi `config-*` mana yang akan diunduh dari repositori kernel [ophub/kernel](https://github.com/ophub/kernel/tree/main/kernel-config/release) ke direktori lokal [tools/config](tools/config). Jika file konfigurasi yang sesuai dengan versi kernel sudah ada secara lokal dan parameter ini tidak diatur, pengunduhan dilewati. Opsi yang tersedia sesuai dengan [nama direktori](https://github.com/ophub/kernel/tree/main/kernel-config/release) di repositori kernel, misalnya `stable` / `rk3588` / `rk35xx`. Default: `stable`. |
| -p | AutoPatch | Mengatur apakah akan menerapkan patch kernel kustom. Jika diatur ke `true`, patch dari direktori [tools/patch](tools/patch) akan diterapkan. Untuk detailnya, lihat [cara menambahkan patch kernel](../documents/README.md#9-kompilasi-kernel-armbian). Default: `false` |
| -n | CustomName | Mengatur tanda tangan kustom yang ditambahkan ke versi kernel. Misalnya, pengaturan `-ophub` menghasilkan kernel bernama `5.15.100-ophub`. Jangan sertakan spasi dalam tanda tangan kustom. Default: `-ophub` |
| -t | Toolchain | Mengatur toolchain untuk kompilasi kernel. Opsi: `clang / gcc / gcc-<version>`. Default: `gcc` |
| -z | CompressFormat | Mengatur format kompresi untuk initrd di kernel. Opsi: `xz / gzip / zstd / lzma`. Default: `xz` |
| -s | SilentLog | Mengatur apakah akan mengaktifkan mode senyap untuk mengurangi keluaran log selama kompilasi. Opsi: `true / false`. Default: `false` |
| -l | EnableLog | Mengatur apakah akan mencatat proses kompilasi kernel ke file: `/var/log/kernel_compile_*.log`. Opsi: `true / false`. Default: `false` |
| -c | CcacheClear | Mengatur apakah akan membersihkan ccache sebelum kompilasi. Opsi: `true / false`. Default: `false` |
| -d | DeleteSource | Mengatur apakah akan menghapus kode sumber kernel setelah kompilasi. Opsi: `true / false`. Default: `false` |
| -h | DockerHostpath | Mengatur path mount host untuk kompilasi kernel di Docker. Default: direktori saat ini. |
| -i | DockerImage | Mengatur image kontainer Docker yang digunakan untuk kompilasi kernel. Default: `ophub/armbian-resolute:arm64` |

- `sudo ./recompile`: Kompilasi kernel menggunakan konfigurasi default.
- `sudo ./recompile -k 5.15.100`: Gunakan konfigurasi default dan tentukan versi kernel yang akan dikompilasi melalui `-k`. Beberapa versi dihubungkan menggunakan `_` untuk kompilasi bersamaan.
- `sudo ./recompile -k 5.15.100 -f stable` : Gunakan konfigurasi default, tentukan versi kernel yang akan dikompilasi melalui `-k 5.15.100`, dan tentukan file konfigurasi yang akan diunduh dari direktori `stable` di repositori kernel melalui `-f stable`.
- `sudo ./recompile -k 5.15.100 -a true`: Gunakan konfigurasi default dan atur apakah akan otomatis meningkatkan ke kernel terbaru dari seri yang sama saat kompilasi kernel melalui parameter `-a`.
- `sudo ./recompile -k 5.15.100 -n -ophub`: Gunakan konfigurasi default dan atur tanda tangan kustom kernel melalui parameter `-n`.
- `sudo ./recompile -k 5.15.100 -m dtbs`: Gunakan konfigurasi default dan tentukan hanya pembuatan file dtbs melalui parameter `-m`.
- `sudo ./recompile -k 5.15.100_6.1.10 -a true -n -ophub`: Gunakan konfigurasi default dan atur beberapa parameter.

💡 Tips: Kami menyarankan penggunaan kode sumber kernel dari repositori seperti [linux-6.1.y](https://github.com/unifreq/linux-6.1.y), [linux-5.15.y](https://github.com/unifreq/linux-5.15.y), dan [linux-5.10.y](https://github.com/unifreq/linux-5.10.y) milik `unifreq`, yang menyertakan driver dan patch untuk box yang didukung. Disarankan juga untuk menggunakan templat konfigurasi di [ophub/kernel](https://github.com/ophub/kernel/tree/main/kernel-config/release), yang telah dikonfigurasi sebelumnya untuk box yang didukung dan dapat disesuaikan lebih lanjut sesuai kebutuhan.

## Kompilasi Kernel Menggunakan GitHub Actions

1. Di halaman [Actions](https://github.com/farishhz/amlogic-s9xxx-armbian/actions), pilih **_`Compile the kernel`_** lalu klik tombol **_`Run workflow`_** untuk mengompilasi.

2. Lihat penggunaan templat [compile-kernel-via-docker.yml](../.github/workflows/compile-kernel-via-docker.yml). Kodenya sebagai berikut:

```yaml
- name: Compile the kernel
  uses: farishhz/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 6.12.y_6.18.y
    kernel_auto: true
    kernel_sign: -yourname
```

💡 Catatan: Jika Anda melakukan `fork` repositori dan membuat modifikasi, Anda harus mengubah `username` Actions ke repositori Anda sendiri saat menggunakannya, misalnya:

```yaml
uses: YOUR-REPO/amlogic-s9xxx-armbian@main
```

- ### Parameter Input GitHub Action

Parameter-parameter ini sesuai dengan `perintah kompilasi lokal`. Lihat deskripsi di atas.

| Parameter | Nilai Default | Deskripsi |
| --- | --- | --- |
| build_target | kernel | Parameter tetap `kernel`. Mengatur target kompilasi ke kernel. |
| kernel_source | unifreq | Menentukan repositori kode sumber kernel untuk kompilasi. Default: `unifreq`. Lihat `-r` untuk detailnya. |
| kernel_version | 6.12.y_6.18.y | Menentukan versi kernel, misalnya `5.15.100`. Lihat `-k` untuk detailnya. |
| kernel_auto | true | Mengatur apakah akan otomatis menggunakan versi terbaru dalam seri kernel yang sama. Default: `true`. Lihat `-a` untuk detailnya. |
| kernel_package | all | Mengatur daftar paket untuk membangun kernel. Default: `all`. Lihat `-m` untuk detailnya. |
| kernel_sign | -ophub | Mengatur tanda tangan kustom untuk kernel. Default: `-ophub`. Lihat `-n` untuk detailnya. |
| kernel_toolchain | gcc | Mengatur toolchain untuk kompilasi kernel. Default: `gcc`. Lihat `-t` untuk detailnya. |
| config_flavor | stable | Menentukan file konfigurasi `config-*` mana yang akan diunduh dari repositori kernel [ophub/kernel](https://github.com/ophub/kernel/tree/main/kernel-config/release) ke direktori lokal [tools/config](tools/config). Jika file konfigurasi yang sesuai dengan versi kernel sudah ada secara lokal dan parameter ini tidak diatur, pengunduhan dilewati. Opsi yang tersedia sesuai dengan [nama direktori](https://github.com/ophub/kernel/tree/main/kernel-config/release) di repositori kernel, misalnya `stable` / `rk3588` / `rk35xx`. Default: `stable`. Jika `kernel_config` juga diatur, file konfigurasi yang ditentukan oleh `config_flavor` lebih diutamakan. Kedua parameter ini saling eksklusif: gunakan salah satu untuk memilih file konfigurasi kernel dari [ophub/kernel](https://github.com/ophub/kernel/tree/main/kernel-config/release), atau yang lain untuk menggunakan file dari repositori Anda sendiri. Lihat `-f` untuk detailnya. |
| kernel_config | false | Secara default, menggunakan templat konfigurasi di direktori [tools/config](tools/config). Anda dapat menentukan direktori di repositori Anda yang berisi file konfigurasi kernel, misalnya `kernel/config_path`. File konfigurasi di direktori tersebut harus mengikuti konvensi penamaan berdasarkan versi mayor kernel, misalnya `config-5.10`, `config-5.15`, dan seterusnya. |
| kernel_patch | false | Mengatur direktori di repositori Anda yang berisi file patch kernel kustom. Jika ditentukan, file patch akan otomatis diunduh dari direktori yang ditentukan sebelum kompilasi. Jika tidak diatur, langkah ini dilewati. |
| auto_patch | false | Mengatur apakah akan menerapkan patch kernel kustom. Default: `false`. Lihat `-p` untuk detailnya. |
| compress_format | xz | Mengatur format kompresi untuk initrd di kernel. Default: `xz`. Lihat `-z` untuk detailnya. |
| silent_log | false | Mengatur apakah akan mengaktifkan mode senyap untuk mengurangi keluaran log selama kompilasi. Default: `false`. Lihat `-s` untuk detailnya. |
| enable_log | false | Mengatur apakah akan mencatat proses kompilasi kernel ke file: `/var/log/kernel_compile_*.log`. Default: `false`. Lihat `-l` untuk detailnya. |
| ccache_clear | false | Mengatur apakah akan membersihkan ccache sebelum kompilasi. Default: `false`. Lihat `-c` untuk detailnya. |
| delete_source | false | Mengatur apakah akan menghapus kode sumber kernel setelah kompilasi. Default: `false`. Lihat `-d` untuk detailnya. |
| docker_hostpath | . | Mengatur path mount host untuk kompilasi kernel di Docker. Default ke direktori kerja saat ini. Lihat `-h` untuk detailnya. |
| docker_image | ophub/armbian-resolute:arm64 | Mengatur image kontainer Docker yang digunakan untuk kompilasi kernel. Lihat `-i` untuk detailnya. |

- ### Variabel Output GitHub Action

Untuk mengunggah ke `Releases`, Anda perlu mengatur `Workflow read/write permissions` untuk repositori. Untuk detailnya, lihat [Petunjuk Penggunaan](../documents/README.md#2-atur-variabel-privat-github_token).

| Parameter | Nilai Default | Deskripsi |
| --- | --- | --- |
| ${{ env.PACKAGED_OUTPUTTAGS }} | 6.12.y_6.18.y | Nama kernel hasil kompilasi. |
| ${{ env.PACKAGED_OUTPUTPATH }} | compile-kernel/output | Path direktori tempat file kernel hasil kompilasi disimpan. |
| ${{ env.PACKAGED_OUTPUTDATE }} | 04.13.1058 | Tanggal kompilasi (bulan.tanggal.jammenit). |
| ${{ env.PACKAGED_STATUS }} | success | Status kompilasi: success / failure. |

## Panduan Penggunaan Kernel

Kernel hasil kompilasi mendukung sistem `Armbian` maupun `OpenWrt`. Contoh berikut menggunakan proyek-proyek milik ophub.

### Penggunaan di Armbian

Bagian berikut menjelaskan cara mengintegrasikan kernel saat kompilasi firmware Armbian dan cara menginstalnya di sistem yang sudah ada.

- #### Kompilasi Firmware Armbian dengan Kernel

Kompilasi firmware Armbian mendukung workflow lokal maupun online melalui GitHub Actions. Untuk kompilasi lokal, lihat [Pengemasan Lokal](../README.md#pengemasan-lokal). Untuk kompilasi online melalui Actions, lihat [Kompilasi Menggunakan GitHub Actions](../README.md#kompilasi-menggunakan-github-actions).

- #### Menginstal Kernel di Sistem Armbian yang Sudah Ada

Gunakan perintah `armbian-update` untuk menginstal kernel hasil kompilasi ke sistem Armbian yang sudah ada. Untuk petunjuk lengkap, lihat [Perbarui Kernel Armbian](../README.md#perbarui-kernel-armbian).

- #### Kompilasi Modul Driver Kustom

Beberapa driver belum disertakan dalam kernel mainline Linux. Anda dapat mengompilasi modul driver kustom sesuai kebutuhan. Untuk petunjuknya, lihat [Kompilasi Modul Driver](../documents/README.md#93-cara-menyesuaikan-kompilasi-modul-driver).

### Penggunaan di OpenWrt

Bagian berikut menjelaskan cara mengintegrasikan kernel saat kompilasi firmware OpenWrt dan cara menginstalnya di sistem yang sudah ada.

- #### Kompilasi Firmware OpenWrt dengan Kernel

Kompilasi firmware OpenWrt mendukung workflow lokal maupun online melalui GitHub Actions. Untuk kompilasi lokal, lihat [Pengemasan Lokal](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/README.md#local-packaging). Untuk kompilasi online melalui Actions, lihat [Kompilasi Menggunakan GitHub Actions](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/README.md#use-github-actions-for-compilation).

- #### Menginstal Kernel di Sistem OpenWrt yang Sudah Ada

Gunakan plugin [luci-app-amlogic](https://github.com/ophub/luci-app-amlogic) untuk menginstal kernel hasil kompilasi ke sistem OpenWrt yang sudah ada. Untuk petunjuk lengkap, lihat [Perbarui Sistem atau Kernel OpenWrt](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/README.md#update-openwrt-system-or-kernel).
