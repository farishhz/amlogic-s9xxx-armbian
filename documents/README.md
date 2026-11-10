# Panduan Build dan Penggunaan Armbian

GitHub Actions adalah layanan CI/CD dari Microsoft yang menyediakan lingkungan server virtual berperforma tinggi untuk membangun, menguji, mengemas, dan men-deploy proyek. Repositori publik dapat menggunakannya secara gratis tanpa batas waktu, dan setiap build dapat berjalan hingga 6 jam — lebih dari cukup untuk mengompilasi Armbian (biasanya selesai dalam sekitar 3 jam). Proyek ini dibagikan untuk tujuan edukasi dan pertukaran pengalaman. Mohon jangan melancarkan serangan jaringan yang merugikan atau menyalahgunakan GitHub Actions.

# Daftar Isi

- [Panduan Build dan Penggunaan Armbian](#panduan-build-dan-penggunaan-armbian)
- [Daftar Isi](#daftar-isi)
  - [1. Daftarkan akun GitHub Anda sendiri](#1-daftarkan-akun-github-anda-sendiri)
  - [2. Atur variabel privat GITHUB\_TOKEN dll.](#2-atur-variabel-privat-github_token-dll)
  - [3. Fork repositori dan atur izin Workflow](#3-fork-repositori-dan-atur-izin-workflow)
  - [4. Petunjuk kustomisasi file sistem Armbian yang dipersonalisasi](#4-petunjuk-kustomisasi-file-sistem-armbian-yang-dipersonalisasi)
  - [5. Kompilasi sistem](#5-kompilasi-sistem)
    - [5.1 Kompilasi Manual](#51-kompilasi-manual)
    - [5.2 Kompilasi Terjadwal](#52-kompilasi-terjadwal)
    - [5.3 Menyesuaikan Konfigurasi Default Sistem](#53-menyesuaikan-konfigurasi-default-sistem)
    - [5.4 Memperluas Ruang Kompilasi GitHub Actions Menggunakan Logical Volume](#54-memperluas-ruang-kompilasi-github-actions-menggunakan-logical-volume)
    - [5.5 Build image Docker Armbian](#55-build-image-docker-armbian)
  - [6. Menyimpan Sistem](#6-menyimpan-sistem)
  - [7. Mengunduh Sistem](#7-mengunduh-sistem)
  - [8. Menginstal Armbian ke EMMC](#8-menginstal-armbian-ke-emmc)
    - [8.1 Metode Instalasi untuk Seri Amlogic](#81-metode-instalasi-untuk-seri-amlogic)
    - [8.2 Metode Instalasi untuk Seri Rockchip](#82-metode-instalasi-untuk-seri-rockchip)
      - [8.2.1 Metode Instalasi untuk Radxa-Rock5B](#821-metode-instalasi-untuk-radxa-rock5b)
        - [8.2.1.1 Instal Sistem ke MicroSD](#8211-instal-sistem-ke-microsd)
        - [8.2.1.2 Instal Sistem ke eMMC](#8212-instal-sistem-ke-emmc)
        - [8.2.1.3 Instalasi sistem pada NVMe](#8213-instalasi-sistem-pada-nvme)
      - [8.2.2 Metode instalasi untuk FastRhino R66S](#822-metode-instalasi-untuk-fastrhino-r66s)
      - [8.2.3 Metode instalasi untuk FastRhino R68S](#823-metode-instalasi-untuk-fastrhino-r68s)
      - [8.2.4 Metode instalasi untuk Beikeyun](#824-metode-instalasi-untuk-beikeyun)
      - [8.2.5 Metode instalasi untuk Chainedbox-L1-Pro](#825-metode-instalasi-untuk-chainedbox-l1-pro)
      - [8.2.6 Metode instalasi untuk lckfb-tspi](#826-metode-instalasi-untuk-lckfb-tspi)
    - [8.3 Metode Instalasi Seri Allwinner](#83-metode-instalasi-seri-allwinner)
    - [8.4 Metode Instalasi untuk Armbian Versi Docker](#84-metode-instalasi-armbian-versi-docker)
      - [8.4.1 Instal Lingkungan Runtime Docker](#841-instal-lingkungan-runtime-docker)
      - [8.4.2 Konfigurasi Jaringan macvlan](#842-konfigurasi-jaringan-macvlan)
      - [8.4.3 Jalankan Container Docker Armbian](#843-jalankan-container-docker-armbian)
  - [9. Mengompilasi Kernel Armbian](#9-kompilasi-kernel-armbian)
    - [9.1 Cara Menambahkan Patch Kernel Kustom](#91-cara-menambahkan-patch-kernel-kustom)
    - [9.2 Cara Membuat Patch Kernel](#92-cara-membuat-patch-kernel)
    - [9.3 Cara Menyesuaikan Kompilasi Modul Driver](#93-cara-mengompilasi-modul-driver-secara-kustom)
  - [10. Memperbarui Kernel Armbian](#10-memperbarui-kernel-armbian)
  - [11. Menginstal Perangkat Lunak Umum](#11-menginstal-perangkat-lunak-umum)
  - [12. Pertanyaan yang Sering Diajukan](#12-pertanyaan-yang-sering-diajukan)
    - [12.1 Tabel Korespondensi dtb dan u-boot untuk Setiap Box](#121-tabel-korespondensi-dtb-dan-u-boot-untuk-setiap-box)
    - [12.2 Petunjuk Kontrol Tampilan Layar LED](#122-petunjuk-kontrol-tampilan-layar-led)
    - [12.3 Cara Memulihkan Sistem Android TV Asli](#123-cara-memulihkan-sistem-android-tv-asli)
      - [12.3.1 Pencadangan dan Pemulihan Menggunakan Armbian-ddbr](#1231-pencadangan-dan-pemulihan-menggunakan-armbian-ddbr)
      - [12.3.2 Pemulihan menggunakan Amlogic Flashing Tool](#1232-pemulihan-menggunakan-alat-flashing-amlogic)
    - [12.4 Mengatur box agar boot dari USB/TF/SD](#124-mengatur-box-untuk-boot-dari-usbtfsd)
      - [12.4.1 Instalasi Awal Sistem Armbian](#1241-instalasi-awal-sistem-armbian)
      - [12.4.2 Instal Ulang Sistem Armbian](#1242-instalasi-ulang-sistem-armbian)
    - [12.5 Menonaktifkan Penerima Inframerah](#125-menonaktifkan-penerima-inframerah)
    - [12.6 Pemilihan file boot](#126-pemilihan-file-boot)
    - [12.7 Konfigurasi Jaringan](#127-konfigurasi-jaringan)
      - [12.7.1 Konfigurasi Jaringan Menggunakan Interfaces](#1271-konfigurasi-jaringan-menggunakan-interfaces)
        - [12.7.1.1 Penetapan Alamat IP melalui DHCP](#12711-penetapan-alamat-ip-melalui-dhcp)
        - [12.7.1.2 Pengaturan Manual Alamat IP Statis](#12712-pengaturan-manual-alamat-ip-statis)
        - [12.7.1.3 Membangun Jaringan Terinterkoneksi Menggunakan OpenWrt di Docker](#12713-membangun-jaringan-yang-saling-terhubung-menggunakan-openwrt-di-docker)
      - [12.7.2 Manajemen Jaringan Menggunakan NetworkManager](#1272-manajemen-jaringan-menggunakan-networkmanager)
        - [12.7.2.1 Membuat Koneksi Jaringan Baru](#12721-membuat-koneksi-jaringan-baru)
          - [12.7.2.1.1 Mendapatkan Nama Antarmuka Jaringan](#127211-mendapatkan-nama-antarmuka-jaringan)
          - [12.7.2.1.2 Mendapatkan Nama Koneksi Jaringan yang Ada](#127212-mendapatkan-nama-koneksi-jaringan-yang-sudah-ada)
          - [12.7.2.1.3 Membuat Koneksi Jaringan Kabel](#127213-membuat-koneksi-jaringan-kabel)
          - [12.7.2.1.4 Membuat Koneksi Jaringan Nirkabel](#127214-membuat-koneksi-jaringan-nirkabel)
        - [12.7.2.2 Mengubah SSID atau PASSWD WiFi pada Koneksi Jaringan Nirkabel](#12722-mengubah-ssid-atau-passwd-wifi-pada-koneksi-jaringan-nirkabel)
        - [12.7.2.3 Mengubah Metode Alokasi Alamat Jaringan](#12723-mengubah-metode-alokasi-alamat-jaringan)
          - [12.7.2.3.1 Alamat IP statis - IPv4](#127231-alamat-ip-statis---ipv4)
          - [12.7.2.3.2 DHCP Memperoleh Alamat IP Dinamis - IPv4 / IPv6](#127232-dhcp-mendapatkan-alamat-ip-dinamis---ipv4--ipv6)
        - [12.7.2.4 Mengubah Alamat MAC Koneksi Jaringan](#12724-mengubah-alamat-mac-koneksi-jaringan)
          - [12.7.2.4.1 Metode 1: Gunakan perintah `nmcli` untuk mengubah alamat MAC](#127241-metode-1-gunakan-perintah-nmcli-untuk-mengubah-alamat-mac)
          - [12.7.2.4.2 Metode 2: Ubah alamat MAC melalui file konfigurasi](#127242-metode-2-mengubah-alamat-mac-melalui-file-konfigurasi)
        - [12.7.2.5 Cara Menonaktifkan IPv6](#12725-cara-menonaktifkan-ipv6)
      - [12.7.3 Cara Mengaktifkan Nirkabel](#1273-cara-mengaktifkan-nirkabel)
      - [12.7.4 Cara Mengaktifkan Bluetooth](#1274-cara-mengaktifkan-bluetooth)
    - [12.8 Cara Menambahkan Tugas Startup](#128-cara-menambahkan-tugas-startup)
    - [12.9 Cara Memperbarui Skrip Layanan di Sistem](#129-cara-memperbarui-skrip-layanan-di-sistem)
    - [12.10 Cara Mendapatkan Informasi Partisi Sistem Android pada eMMC](#1210-cara-mendapatkan-informasi-partisi-sistem-android-di-emmc)
      - [12.10.1 Memperoleh Informasi Partisi](#12101-mendapatkan-informasi-partisi)
      - [12.10.2 Membagikan Informasi Partisi](#12102-membagikan-informasi-partisi)
      - [12.10.3 Menginterpretasikan Informasi Partisi](#12103-menafsirkan-informasi-partisi)
      - [12.10.4 Untuk Instalasi eMMC](#12104-untuk-instalasi-emmc)
    - [12.11 Cara build file u-boot](#1211-cara-membuat-file-u-boot)
      - [12.11.1 Cara build file u-boot untuk perangkat Amlogic](#12111-cara-membuat-file-u-boot-untuk-perangkat-amlogic)
        - [12.11.1.1 Cara mengekstrak file bootloader dan dtb](#121111-cara-mengekstrak-file-bootloader-dan-dtb)
        - [12.11.1.2 Cara membuat file acs.bin](#121112-cara-membuat-file-acsbin)
        - [12.11.1.3 Cara build file u-boot](#121113-cara-membuat-file-u-boot)
      - [12.11.2 Cara build file u-boot untuk perangkat Rockchip](#12112-cara-membuat-file-u-boot-untuk-perangkat-rockchip)
        - [12.11.2.1 Cara menggunakan skrip build u-boot dari Radxa](#121121-cara-menggunakan-skrip-pembuatan-u-boot-dari-radxa)
        - [12.11.2.2 Cara menggunakan skrip build u-boot dari cm9vdA](#121122-cara-menggunakan-skrip-pembuatan-u-boot-dari-cm9vda)
    - [12.12 Kesalahan dalam Pengenalan Ukuran Memori](#1212-kesalahan-pengenalan-ukuran-memori)
    - [12.13 Cara Mendekompilasi File dtb](#1213-cara-mendekompilasi-file-dtb)
      - [12.13.1 Mendekompilasi File dtb Secara Langsung](#12131-dekompilasi-file-dtb-secara-langsung)
      - [12.13.2 Ekspor DTS Status Penuh dari Perangkat yang Sedang Berjalan (Direkomendasikan)](#12132-ekspor-dts-kondisi-penuh-dari-perangkat-yang-sedang-berjalan-direkomendasikan)
    - [12.14 Cara Mengubah Pengaturan cmdline](#1214-cara-mengubah-pengaturan-cmdline)
    - [12.15 Cara Menambahkan Perangkat Baru yang Didukung](#1215-cara-menambahkan-perangkat-baru-yang-didukung)
      - [12.15.1 Tambahkan File Konfigurasi Perangkat](#12151-tambahkan-file-konfigurasi-perangkat)
      - [12.15.2 Tambahkan File Sistem](#12152-tambahkan-file-sistem)
      - [12.15.3 Tambahkan File u-boot](#12153-tambahkan-file-u-boot)
        - [12.15.3.1 Periksa Tata Letak Partisi](#121531-periksa-tata-letak-partisi)
        - [12.15.3.2 Cadangkan Partisi Penting](#121532-cadangkan-partisi-kunci)
        - [12.15.3.3 Tambahkan File Penulisan Partisi Khusus](#121533-tambahkan-file-penulisan-partisi-khusus)
      - [12.15.4 Tambahkan File Kontrol Proses](#12154-tambahkan-file-kontrol-proses)
    - [12.16 Cara Mengatasi Kegagalan Boot Sistem atau Kesalahan I/O Penulisan eMMC yang Disebabkan oleh Frekuensi DTB](#1216-cara-mengatasi-kegagalan-boot-sistem-atau-error-io-penulisan-emmc-yang-disebabkan-oleh-frekuensi-dtb)
    - [12.17 Cara Mengatasi Masalah Tidak Ada Suara pada Versi Bullseye](#1217-cara-mengatasi-masalah-tidak-ada-suara-pada-versi-bullseye)
    - [12.18 Cara build file boot.scr](#1218-cara-membuat-file-bootscr)
    - [12.19 Cara Mengaktifkan Remote Desktop dan Mengubah Port Default](#1219-cara-mengaktifkan-remote-desktop-dan-mengubah-port-default)
    - [12.20 Panduan Optimasi Kontrol Kemacetan TCP](#1220-panduan-optimasi-kontrol-kemacetan-tcp)
    - [12.21 Cara Memperbaiki Masalah Deteksi EDID HDMI](#1221-cara-memperbaiki-masalah-deteksi-edid-hdmi)

## 1. Daftarkan akun GitHub Anda sendiri

Daftarkan akun untuk melanjutkan kustomisasi sistem. Klik tombol `Sign up` di pojok kanan atas github.com dan ikuti petunjuk untuk menyelesaikan pendaftaran.

## 2. Atur variabel privat GITHUB_TOKEN dll.

Menurut [Dokumentasi GitHub](https://docs.github.com/en/actions/security-guides/automatic-token-authentication), GitHub secara otomatis membuat secret `GITHUB_TOKEN` yang unik di awal setiap job workflow untuk digunakan di dalam workflow. `${{ secrets.GITHUB_TOKEN }}` dapat digunakan untuk autentikasi di dalam job workflow.

Saat membangun image [Armbian Docker](../.github/workflows/build-armbian-arm64-docker-image.yml) di Actions dan mendorongnya ke Docker Hub, Anda perlu mengatur dua secret: `DOCKERHUB_USERNAME` dan `DOCKERHUB_PASSWORD`. Pada halaman repositori Anda, klik Settings di pojok kanan atas, lalu buka `Settings` > `Secrets and variables` > `Actions` > `Repository secrets` > `New repository secret`, dan tambahkan dua secret berikut:

- Nama secret `DOCKERHUB_USERNAME`: Nilainya adalah nama pengguna Anda untuk masuk ke Docker Hub.
- Nama secret `DOCKERHUB_PASSWORD`: Nilainya adalah kata sandi Anda untuk masuk ke Docker Hub.

## 3. Fork repositori dan atur izin Workflow

Fork repositori dengan membuka https://github.com/farishhz/amlogic-s9xxx-armbian dan mengklik tombol Fork di kanan atas untuk menyalin repositori ke akun Anda. Setelah fork selesai, buka salinan Anda. Kemudian buka `Settings` > `Actions` > `General` > `Workflow permissions` di bilah navigasi kiri lalu simpan. Ilustrasinya sebagai berikut:

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/167585338-841d3b05-8d98-4d73-ba72-475aad4a95a9.png width="300" />
</div>

## 4. Petunjuk kustomisasi file sistem Armbian yang dipersonalisasi

Proses kompilasi sistem dikendalikan di file [.github/workflows/build-armbian-arm64-server-image.yml](../.github/workflows/build-armbian-arm64-server-image.yml). File .yml lain di direktori workflows menangani fungsi-fungsi lainnya. Sistem dikompilasi menggunakan kode sumber resmi Armbian versi terkini. Lihat dokumentasi resmi untuk detail parameter.

```yaml
- name: Compile Armbian [ ${{ inputs.set_release }} ]
  id: compile
  if: ${{ steps.down.outputs.status }} == 'success' && !cancelled()
  run: |
    # Metode kompilasi dan deskripsi parameter: https://docs.armbian.com/Developer-Guide_Build-Options
    cd build/
        ./compile.sh RELEASE=${{ inputs.set_release }} BOARD=odroidn2 BRANCH=current BUILD_MINIMAL=no \
                      BUILD_ONLY=default HOST=armbian BUILD_DESKTOP=no EXPERT=yes KERNEL_CONFIGURE=no \
                      COMPRESS_OUTPUTIMAGE="sha" SHARE_LOG=yes
    echo "status=success" >> ${GITHUB_OUTPUT}
```

Saat membangun Armbian dengan `ophub`, parameter `armbian_files` memungkinkan Anda menambahkan atau menimpa file kustom di direktori [common-files](https://github.com/farishhz/amlogic-s9xxx-armbian/tree/main/build-armbian/armbian-files/common-files). Struktur direktori harus benar-benar mencerminkan filesystem root Armbian agar file tertimpa dengan benar ke dalam firmware (misalnya, file konfigurasi default harus ditempatkan di subdirektori `etc/default/`). Contoh konfigurasi:

```yaml
- name: Rebuild Armbian
  uses: farishhz/amlogic-s9xxx-armbian@main
  with:
    build_target: armbian
    armbian_path: build/output/images/*.img.gz
    armbian_files: files
    ...
```

## 5. Kompilasi sistem

Sistem dapat dikompilasi secara manual, terjadwal, atau dipicu oleh peristiwa tertentu. Bagian-bagian berikut membahas setiap metode.

### 5.1 Kompilasi Manual

Di bilah navigasi repositori Anda, klik tombol Actions, lalu pilih Build Armbian > Run workflow > Run workflow untuk memulai kompilasi. Proses ini memakan waktu sekitar 3 jam dan selesai setelah semua langkah rampung. Ilustrasinya sebagai berikut:

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/163203938-e7762b09-e6b8-4cf5-b1f1-9c67c1a29953.png width="300" />
<img src=https://user-images.githubusercontent.com/68696949/163204044-9c7a7429-47ee-4fce-b7dd-e217bebf6133.png width="300" />
<img src=https://user-images.githubusercontent.com/68696949/163204127-6b16b558-7e78-4c22-a28a-7b37b5a34fa3.png width="300" />
</div>

### 5.2 Kompilasi Terjadwal

Di file [.github/workflows/build-armbian-arm64-server-image.yml](../.github/workflows/build-armbian-arm64-server-image.yml), gunakan Cron untuk mengonfigurasi kompilasi terjadwal. Kelima kolom mewakili menit (0–59) / jam (0–23) / tanggal dalam bulan (1–31) / bulan (1–12) / hari dalam minggu (0–6, Minggu–Sabtu). Ubah nilainya sesuai kebutuhan. Sistem menggunakan UTC secara default; sesuaikan dengan zona waktu lokal Anda.

```yaml
schedule:
  - cron: '0 17 * * *'
```

### 5.3 Menyesuaikan Konfigurasi Default Sistem

Informasi konfigurasi default sistem dicatat di file [model_database.conf](../build-armbian/armbian-files/common-files/etc/model_database.conf), di mana nama `BOARD` harus unik.

Perangkat dengan `BUILD` bernilai `yes` disertakan dalam build default dan dapat langsung digunakan. Perangkat yang bernilai `no` tidak dikemas secara default. Untuk menggunakan perangkat yang tidak dikemas, unduh sistem Armbian dengan `FAMILY` yang sama, tulis ke `USB`, lalu buka partisi boot USB di komputer Anda dan ubah `FDT dtb name` di `/boot/uEnv.txt` agar sesuai dengan perangkat Anda.

Untuk kompilasi lokal, gunakan parameter `-b`; untuk GitHub Actions, gunakan parameter `armbian_board`. `-b all` mengemas semua perangkat dengan `BUILD` bernilai `yes`. Menentukan `BOARD` secara eksplisit akan mengemasnya terlepas dari nilai `BUILD`-nya. Contoh: `-b r68s_s905x3-tx3_s905l3a-cm311`.

### 5.4 Memperluas Ruang Kompilasi GitHub Actions Menggunakan Logical Volume

GitHub Actions menyediakan ruang kompilasi 84GB secara default, dengan sekitar 50GB tersedia setelah dikurangi sistem dan paket yang diperlukan. Saat mengompilasi semua image firmware, ruang ini mungkin tidak cukup. Anda dapat menggunakan logical volume untuk memperluas ruang kompilasi hingga sekitar 110GB. Lihat file [.github/workflows/build-armbian-arm64-server-image.yml](../.github/workflows/build-armbian-arm64-server-image.yml) dan gunakan perintah di bawah ini untuk membuat logical volume, lalu gunakan path logical volume tersebut selama kompilasi.

```yaml
- name: Create simulated physical disk
  run: |
    mnt_size=$(expr $(df -h /mnt | tail -1 | awk '{print $4}' | sed 's/[[:alpha:]]//g' | sed 's/\..*//') - 1)
    root_size=$(expr $(df -h / | tail -1 | awk '{print $4}' | sed 's/[[:alpha:]]//g' | sed 's/\..*//') - 4)
    sudo truncate -s "${mnt_size}"G /mnt/mnt.img
    sudo truncate -s "${root_size}"G /root.img
    sudo losetup /dev/loop6 /mnt/mnt.img
    sudo losetup /dev/loop7 /root.img
    sudo pvcreate /dev/loop6
    sudo pvcreate /dev/loop7
    sudo vgcreate github /dev/loop6 /dev/loop7
    sudo lvcreate -n runner -l 100%FREE github
    sudo mkfs.xfs /dev/github/runner
    sudo mkdir -p /builder
    sudo mount /dev/github/runner /builder
    sudo chown -R runner:runner /builder
    df -Th
```

### 5.5 Build image Docker Armbian

Untuk membuat image [Docker](https://hub.docker.com/u/farishhz) dari sistem Armbian, lihat skrip build [armbian_docker](../compile-kernel/tools/script/docker).

## 6. Menyimpan Sistem

Penyimpanan sistem juga dikonfigurasi di file [.github/workflows/build-armbian-arm64-server-image.yml](../.github/workflows/build-armbian-arm64-server-image.yml). Sistem yang telah dikompilasi akan diunggah secara otomatis ke GitHub Releases melalui skrip.

```yaml
- name: Upload Armbian image to Release
  uses: ophub/upload-to-release@main
  if: ${{ env.PACKAGED_STATUS }} == 'success' && !cancelled()
  with:
    tag: Armbian_${{ env.ARMBIAN_RELEASE }}_${{ env.PACKAGED_OUTPUTDATE }}
    artifacts: ${{ env.PACKAGED_OUTPUTPATH }}/*
    allow_updates: true
    gh_token: ${{ secrets.GITHUB_TOKEN }}
    body: |
      Ini adalah image OS Armbian
      * Informasi OS
      Nama pengguna default: root
      Kata sandi default: 1234
      Perintah instalasi: armbian-install
      Perintah pembaruan: armbian-update
```

## 7. Mengunduh Sistem

Buka bagian Releases di halaman utama repositori dan pilih image sistem yang sesuai dengan model perangkat Anda. Ilustrasinya sebagai berikut:

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/163204798-0d98524c-73df-4876-8912-fcae2845fbba.png width="300" />
<img src=https://user-images.githubusercontent.com/68696949/163204879-4898babf-fa00-4e63-89ea-235129e2ce1d.png width="300" />
</div>

## 8. Menginstal Armbian ke EMMC

Metode instalasi berbeda-beda di antara platform Amlogic, Rockchip, dan Allwinner. Opsi penyimpanan tiap perangkat juga berbeda — sebagian menggunakan kartu microSD eksternal, sebagian memiliki eMMC, dan sebagian mendukung NVMe atau media lainnya. Metode instalasi untuk setiap platform dijelaskan secara terpisah di bawah ini. Pertama, unduh image sistem Armbian yang sesuai untuk perangkat Anda dari [Releases](https://github.com/farishhz/amlogic-s9xxx-armbian/releases) dan ekstrak ke format .img. Ikuti metode instalasi yang sesuai dengan perangkat Anda.

Setelah instalasi, hubungkan perangkat ke `router` Anda dan tunggu `2 menit` hingga perangkat selesai boot. Kemudian temukan alamat `IP` perangkat (tercantum sebagai Armbian) di panel admin router Anda dan hubungkan melalui `SSH`. Nama pengguna default adalah `root`, kata sandi default adalah `1234`, dan port default adalah `22`.

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202972715-addcd695-970a-43d6-8a34-24a9c4bc80a2.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202972773-fc9e9ef9-69a7-4279-8329-6fad1cf2f5b9.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202972818-b72e18cd-17d1-4f9f-a0fa-b6c22eef041d.png width="600" />
</div>

### 8.1 Metode Instalasi untuk Seri Amlogic

Masuk ke sistem Armbian (pengguna default: root, kata sandi default: 1234) → Masukkan perintah:

```shell
armbian-install
```

| Parameter Opsional | Nilai Default | Opsi | Deskripsi |
| --- | --- | --- | --- |
| -m | no | yes/no | Gunakan u-boot mainline |
| -a | yes | yes/no | Gunakan alat penyesuaian partisi [ampart](https://github.com/7Ji/ampart) |
| -l | no | yes/no | Tampilkan seluruh daftar perangkat |

Contoh: `armbian-install -m yes -a no`

### 8.2 Metode Instalasi untuk Seri Rockchip

Metode instalasi berbeda untuk setiap perangkat dan dijelaskan satu per satu di bawah ini.

#### 8.2.1 Metode Instalasi untuk Radxa-Rock5B

Radxa-Rock5B mendukung beberapa media penyimpanan (microSD/eMMC/NVMe), masing-masing dengan metode instalasi yang berbeda. Unduh file [rk3588_spl_loader_v1.08.111.bin dan spi_image.img](https://github.com/ophub/u-boot/tree/main/u-boot/rockchip/rock5b). Unduh alat [RKDevTool](https://github.com/ophub/kernel/releases/download/tools/Radxa_rock5b_RKDevTool_Release_v2.96__DriverAssitant_v5.1.1.tar.gz) beserta drivernya. Unduh [Rufus](https://rufus.ie/) atau [balenaEtcher](https://www.balena.io/etcher/) untuk menulis image disk.

##### 8.2.1.1 Instal Sistem ke MicroSD

Gunakan Rufus, balenaEtcher, atau alat serupa untuk menulis image sistem Armbian ke kartu microSD, lalu masukkan ke perangkat.

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202972996-300f223b-f6f6-48af-86ca-bdc842e5017d.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202973216-85b1a21b-0763-4a36-8c57-84490e071fdd.png width="600" />
</div>

##### 8.2.1.2 Instal Sistem ke eMMC

- Instal melalui kartu microSD: Tulis image sistem Armbian ke kartu microSD dan boot perangkat darinya. Unggah file `armbian.img` ke kartu microSD, lalu gunakan `dd` untuk menulisnya ke eMMC:

```Shell
dd if=armbian.img  of=/dev/mmcblk1  bs=1M status=progress
```

- Instal melalui card reader USB-ke-eMMC: Hubungkan modul eMMC ke komputer Anda, gunakan Rufus atau balenaEtcher untuk menulis image sistem Armbian ke eMMC, lalu pasang modul eMMC ke perangkat.
- Instal melalui mode Maskrom: Matikan papan pengembangan. Tahan tombol emas, lalu hubungkan kabel USB-A ke Type-C antara port Type-C ROCK 5B dan PC Anda. Lepaskan tombol emas. Pastikan perangkat MASKROM terdeteksi. Klik kanan di area kosong daftar dan muat file konfigurasi `rock-5b-emmc.cfg` (file konfigurasi dan RKDevTool berada di direktori yang sama). Atur `rk3588_spl_loader_v1.08.111.bin` dan `Armbian.img` seperti yang ditunjukkan di bawah ini lalu mulai penulisan.

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202954823-3d3b1509-eedc-4192-91eb-017269c7f896.png width="200" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202954901-c829d74d-c75a-4fd3-9bd0-aa3cdf2b77b4.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202954956-6646b7cf-6354-4dc8-b076-c3323cb89a43.png width="200" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202954998-c08514e2-8760-4c0f-b5f7-0d30be635aa5.png width="600" />
</div>

##### 8.2.1.3 Instalasi sistem pada NVMe

ROCK-5B memiliki memori flash SPI pada motherboard-nya. Menginstal bootloader pada memori flash SPI ini memungkinkan dukungan untuk media boot lain (seperti SATA, USB3, atau NVMe) yang tidak didukung langsung oleh mode maskrom SoC. Untuk menggunakan NVMe, Anda harus terlebih dahulu menulis file SPI. Caranya sebagai berikut:

Matikan papan pengembangan dan lepaskan semua perangkat yang dapat di-boot (kartu MicroSD, modul eMMC, dll.). Tekan dan tahan tombol emas, lalu hubungkan kabel USB-A ke Type-C antara ROCK-5B dan PC Anda. Lepaskan tombol emas. Pastikan perangkat MASKROM terdeteksi. Klik kanan di daftar untuk memuat file konfigurasi dari folder resource (file konfigurasi dan RKDevTool berada di direktori yang sama), pilih file `rk3588_spl_loader_v1.08.111.bin` dan `spi_image.img` sesuai gambar di bawah ini, lalu klik tulis:

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202954823-3d3b1509-eedc-4192-91eb-017269c7f896.png width="200" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202961420-8316c96c-2796-43ed-b5ed-2fa5bfa1ddff.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202954956-6646b7cf-6354-4dc8-b076-c3323cb89a43.png width="200" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202961447-49c0941a-e233-4b2a-b96b-b47636ce3cf2.png width="600" />
</div>

- Instal melalui card reader: Masukkan SSD M.2 NVMe ke card reader M.2 NVMe-ke-USB 3.0 dan hubungkan ke komputer Anda. Gunakan Rufus atau balenaEtcher untuk menulis image sistem Armbian ke drive NVMe, lalu pasang ke perangkat.
- Instal melalui kartu microSD: Tulis image sistem Armbian ke kartu microSD dan boot perangkat darinya. Unggah file `armbian.img` ke kartu microSD, lalu gunakan `dd` untuk menulisnya ke NVMe:

```Shell
dd if=armbian.img  of=/dev/nvme0n1  bs=1M status=progress
```

#### 8.2.2 Metode instalasi untuk FastRhino R66S

Gunakan Rufus atau balenaEtcher untuk menulis image sistem Armbian ke kartu microSD, lalu masukkan ke perangkat.

#### 8.2.3 Metode instalasi untuk FastRhino R68S

- Unduh alat [RKDevTool](https://github.com/ophub/kernel/releases/download/tools/FastRhino_r68s_RKDevTool_Release_v2.86___DriverAssitant_v5.1.1.tar.gz) beserta drivernya. Ekstrak, instal driver DriverAssistant, lalu buka RKDevTool.
- Dalam keadaan R68s mati, hubungkan kabel USB male-to-male, tekan dan tahan tombol Recovery, lalu colokkan catu daya 12V. Lepaskan tombol Recovery setelah dua detik — alat flashing akan menampilkan `discover a LOADER device`.
- Klik kanan di area kosong antarmuka RKDevTool untuk menambahkan item.
- Atur alamat ke `0x00000000`, nama ke `armbian`, dan path ke file sistem `armbian.img`.
- Pilih entri armbian, `batalkan pilihan semua entri lainnya`, lalu klik `execute` untuk menulis.
- Catatan: Jika ada sistem lain di eMMC, hapus terlebih dahulu melalui Advanced Features sebelum menulis Armbian. Jika penghapusan gagal, flash ulang bootloader `MiniLoaderAll.bin` terlebih dahulu, lalu masuk ke mode `MASKROM` untuk menulis Armbian. Pengaturan MiniLoaderAll.bin: alamat `0xCCCCCCCC`, nama `Loader`, path ke file `MiniLoaderAll.bin` di direktori Image milik RKDevTool.

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202970301-d798677b-e875-4971-ac8f-ee58b2a1e686.png width="200" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202970405-cb68cb78-cd0f-43ee-b807-5e594ab73099.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202970488-5f18c574-c11f-486f-8fe8-002f3ba2f3f4.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202970577-87549acf-b98b-441f-bb31-e4fd6608108d.png width="600" />
</div>

#### 8.2.4 Metode instalasi untuk Beikeyun

Metode ini berdasarkan tutorial dari [milton](https://www.cnblogs.com/milton/p/15391525.html). Proses flashing memerlukan masuk ke mode Maskrom. Lepaskan semua sambungan, hubungsingkatkan kontak CLK dan GND (menggunakan GND TTL atau GND di dekat tombol kecil), lalu hubungkan melalui USB ke PC Anda. Perangkat MASKROM seharusnya terdeteksi. Lokasi titik hubung singkat ditunjukkan di bawah ini:

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://user-images.githubusercontent.com/68696949/202977817-fb12d291-47e2-47e4-88c3-e21f9ae57922.png width="600" /><br />
<img src=https://user-images.githubusercontent.com/68696949/202977900-50b4770d-8444-42a0-8478-3234043455bd.png width="600" />
</div>

Buka RKDevTool dan klik kanan untuk menambahkan item.

- Alamat `0xCCCCCCCC`, nama `Boot`, path [pilih](https://github.com/ophub/u-boot/tree/main/u-boot/rockchip/beikeyun) `rk3328_loader_v1.14.249.bin`.
- Alamat `0x00000000`, nama `system`, path pilih sistem `Armbian.img` yang akan di-flash.
- Centang opsi "Force Write by Address", klik "Execute", lalu tunggu hingga progres selesai di panel unduhan sebelah kanan.

#### 8.2.5 Metode instalasi untuk Chainedbox-L1-Pro

Metode ini berdasarkan tutorial dari [cc747](https://post.smzdm.com/p/a4wkdo7l/). Matikan Chainedbox-L1-Pro dan cabut semua kabel. Hubungkan kabel USB male-to-male antara port USB 2.0 pada Chainedbox-L1-Pro dan komputer Anda. Masukkan penjepit kertas ke lubang Reset dan tahan, lalu colokkan kabel daya. Tunggu hingga `discovered a LOADER device` muncul di bagian bawah RKDevTool, lalu lepaskan penjepit kertas. Beralih ke `Advanced Features` dan klik `Enter Maskrom` hingga `Found a MASKROM device` muncul. Klik kanan untuk menambahkan item.

- Alamat `0xCCCCCCCC`, nama `Boot`, path [pilih](https://github.com/ophub/u-boot/tree/main/u-boot/rockchip/chainedbox) `rk3328_loader_v1.14.249.bin`.
- Alamat `0x00000000`, nama `system`, path pilih sistem `Armbian.img` yang akan di-flash.
- Centang opsi "Force Write by Address", klik "Execute", lalu tunggu hingga progres selesai di panel unduhan sebelah kanan.

<div style="width:100%;margin-top:40px;margin:5px;">
<img src=https://github.com/farishhz/amlogic-s9xxx-armbian/assets/68696949/a6d2d8c0-35c5-44ba-be35-fd2e2758729b width="600" /><br />
<img src=https://github.com/farishhz/amlogic-s9xxx-armbian/assets/68696949/13aab016-1b93-4ff1-b1ef-c202bd357068 width="600" />
</div>

#### 8.2.6 Metode instalasi untuk lckfb-tspi
- Unduh alat [RKDevTool](https://github.com/ophub/kernel/releases/download/tools/FastRhino_r68s_RKDevTool_Release_v2.86___DriverAssitant_v5.1.1.tar.gz) beserta drivernya. Ekstrak, instal driver DriverAssistant, lalu buka RKDevTool. (Catatan: gunakan versi 2.86, bukan 2.92, karena versi 2.92 mengalami crash saat flashing.)
- Dalam keadaan tspi mati, tekan dan tahan tombol Recovery, lalu masukkan kabel data Type-C. Lepaskan tombol Recovery setelah RKDevTool menampilkan `A LOADER device was found`. Klik kanan untuk menambahkan item.
- Alamat `0x00000000`, nama `system`, path pilih sistem `Armbian.img` yang akan di-flash.
- Klik Execute dan tunggu hingga progres selesai.
### 8.3 Metode Instalasi Seri Allwinner

Masuk ke sistem Armbian (pengguna default: root, kata sandi default: 1234) → Masukkan perintah:

```shell
armbian-install
```

### 8.4 Metode Instalasi Armbian Versi Docker

Anda dapat menggunakan image Armbian versi Docker pada sistem Ubuntu/Debian/Armbian. Image ini di-hosting di [Docker Hub](https://hub.docker.com/r/ophub) dan dapat diunduh langsung untuk digunakan.

Tersedia empat image Docker Armbian dengan versi dasar yang berbeda: `armbian-trixie`, `armbian-bookworm`, `armbian-noble`, dan `armbian-resolute`. Setiap versi memiliki build `arm64` dan `amd64`, sehingga Anda dapat memilih versi yang sesuai dengan kebutuhan Anda.

Di antaranya, armbian-trixie berbasis Debian 13, armbian-bookworm berbasis Debian 12, armbian-noble berbasis Ubuntu 24.04, dan armbian-resolute berbasis Ubuntu 26.04.

Versi arm64 cocok untuk perangkat dengan arsitektur platform seperti Amlogic/Rockchip/Allwinner, sedangkan versi amd64 cocok untuk komputer dan server dengan arsitektur x86_64.

#### 8.4.1 Instal Lingkungan Runtime Docker

```shell
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
sudo newgrp docker
```

#### 8.4.2 Konfigurasi Jaringan macvlan

```shell
# Periksa apakah jaringan docker yang ada sudah mencakup jaringan macvlan
docker network ls

# Jika belum ada jaringan macvlan, buat satu
# Sesuaikan subnet, gateway, dan nama antarmuka dengan jaringan Anda yang sebenarnya
docker network create -d macvlan \
    --subnet=10.1.1.0/24 \
    --gateway=10.1.1.1 \
    -o parent=eth0 \
    macvlan
```

#### 8.4.3 Jalankan Container Docker Armbian

Di sini, image `armbian-resolute:arm64` digunakan sebagai contoh untuk menunjukkan cara menjalankan container Armbian.

```shell
# Jalankan container Armbian dalam mode detached
# Sesuaikan nama container, alamat IP, versi image, dll., dengan situasi Anda yang sebenarnya
docker run -itd --name=armbian-resolute \
    --privileged \
    --network macvlan \
    --ip 10.1.1.15 \
    --hostname=armbian-resolute \
    -e TZ=Asia/Shanghai \
    --restart unless-stopped \
    ophub/armbian-resolute:arm64

# Lihat log container Armbian
docker logs -f armbian-resolute

# Masuk ke container Armbian
docker exec -it armbian-resolute bash

# Keluar dari container Armbian
exit

# Hentikan dan hapus container Armbian
docker rm -f armbian-resolute
```

## 9. Kompilasi Kernel Armbian

Kompilasi kernel didukung pada sistem Ubuntu, Debian, dan Armbian, baik secara lokal maupun melalui GitHub Actions. Untuk detailnya, lihat [Petunjuk Kompilasi Kernel](../../compile-kernel).

### 9.1 Cara Menambahkan Patch Kernel Kustom

Ketika direktori patch kernel [tools/patch](../../compile-kernel/tools/patch) berisi direktori patch umum (`common-kernel-patches`) atau direktori yang sesuai dengan nama repositori sumber kernel (misalnya, [linux-5.15.y](https://github.com/unifreq/linux-5.15.y)), gunakan `-p true` untuk menerapkan patch kernel secara otomatis. Konvensi penamaan direktorinya adalah sebagai berikut:

```shell
~/amlogic-s9xxx-armbian
    └── compile-kernel
        └── tools
            └── patch
                ├── common-kernel-patches  # Nama direktori tetap: menyimpan patch kernel umum untuk semua versi
                ├── linux-5.15.y           # Dinamai sesuai repositori sumber kernel: menyimpan patch khusus
                ├── linux-6.1.y
                ├── linux-5.10.y-rk35xx
                └── more kernel directory...
```

- Untuk kompilasi kernel secara lokal, buat direktori yang sesuai secara manual dan tambahkan patch kernel kustom Anda.
- Untuk kompilasi cloud GitHub Actions, gunakan parameter `kernel_patch` untuk menentukan direktori patch kernel di repositori Anda. Sebagai contoh, lihat penggunaannya di [compile-beta-kernel.yml](https://github.com/ophub/kernel/blob/main/.github/workflows/compile-beta-kernel.yml) pada repositori [kernel](https://github.com/ophub/kernel):

```yaml
- name: Compile the kernel
  uses: farishhz/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 5.15.1_6.1.1
    kernel_auto: true
    kernel_patch: kernel-patch/beta
    auto_patch: true
```

Saat menentukan patch kernel kustom melalui `kernel_patch`, ikuti konvensi penamaan yang dijelaskan di atas.

### 9.2 Cara Membuat Patch Kernel

- Diperoleh dari repositori seperti [Armbian](https://github.com/armbian/build) dan [OpenWrt](https://github.com/openwrt/openwrt): misalnya, [armbian/patch/kernel](https://github.com/armbian/build/tree/main/patch/kernel/archive) dan [openwrt/rockchip/patches-6.1](https://github.com/openwrt/openwrt/tree/main/target/linux/rockchip/patches-6.1), [lede/rockchip/patches-5.15](https://github.com/coolsnowwolf/lede/tree/master/target/linux/rockchip/patches-5.15), dll. Patch dari repositori kernel mainline ini umumnya dapat digunakan secara langsung.
- Diperoleh dari URL commit GitHub: Menambahkan `.patch` di akhir URL commit akan menghasilkan file patch yang sesuai.

Sebelum menambahkan patch kernel kustom, bandingkan dengan repositori sumber kernel upstream [unifreq/linux-k.x.y](https://github.com/unifreq) untuk memastikan patch tersebut belum diterapkan dan untuk menghindari konflik. Patch kernel yang telah diuji dianjurkan untuk dikirimkan ke repositori kernel yang dikelola oleh unifreq. Kontribusi Anda membantu menjadikan Armbian dan OpenWrt lebih stabil dan fungsional bagi semua orang.

### 9.3 Cara Mengompilasi Modul Driver Secara Kustom

Beberapa driver belum disertakan dalam kernel Linux mainline, tetapi dapat dikompilasi sebagai modul kustom. Hanya driver yang kompatibel dengan kernel mainline yang dapat dikompilasi; driver khusus Android umumnya tidak didukung. Lihat panduan: Cara Mengompilasi Modul Driver rtl8189fs⁠

Sebagai contoh:

```shell
# Langkah 1: Perbarui ke kernel terbaru
# Karena file header pada versi lama tidak lengkap, Anda perlu memperbarui ke versi kernel terbaru.
# Persyaratan untuk setiap versi kernel adalah tidak lebih rendah dari 5.10.222, 5.15.163, 6.1.100, 6.6.41, 6.12, 6.18.
armbian-sync
armbian-update -k 6.1

# Langkah 2: Instal alat kompilasi
mkdir -p /usr/local/toolchain
cd /usr/local/toolchain
# Unduh alat kompilasi
wget https://github.com/ophub/kernel/releases/download/toolchain/arm-gnu-toolchain-15.3.rel1-aarch64-aarch64-none-linux-gnu.tar.xz
# Ekstrak
tar -Jxf arm-gnu-toolchain-15.3.rel1-aarch64-aarch64-none-linux-gnu.tar.xz
# Instal dependensi kompilasi tambahan (opsional; Anda dapat menginstal komponen yang kurang secara manual berdasarkan pesan error).
armbian-kernel -u

# Langkah 3: Unduh dan kompilasi driver
# Unduh kode sumber driver
cd ~/
git clone https://github.com/jwrdegoede/rtl8189ES_linux
cd rtl8189ES_linux
# Siapkan lingkungan kompilasi
gun_file="arm-gnu-toolchain-15.3.rel1-aarch64-aarch64-none-linux-gnu.tar.xz"
toolchain_path="/usr/local/toolchain"
toolchain_name="gcc"
export CROSS_COMPILE="${toolchain_path}/${gun_file//.tar.xz/}/bin/aarch64-none-linux-gnu-"
export CC="${CROSS_COMPILE}gcc"
export LD="${CROSS_COMPILE}ld.bfd"
export ARCH="arm64"
export KSRC=/usr/lib/modules/$(uname -r)/build
# Atur variabel M sesuai dengan path sebenarnya dari kode sumber
export M="/root/rtl8189ES_linux"
# Kompilasi driver
make

# Langkah 4: Instal driver
sudo cp -f 8189es.ko /lib/modules/$(uname -r)/kernel/drivers/net/wireless/
# Perbarui dependensi modul
sudo depmod -a
# Muat modul driver
sudo modprobe 8189es
# Periksa apakah driver berhasil dimuat
lsmod | grep 8189es
# Anda akan melihat driver berhasil dimuat
8189es               1843200  0
cfg80211              917504  2 8189es,brcmfmac
```

Ilustrasinya adalah sebagai berikut:

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="700" alt="gambar" src="https://github.com/user-attachments/assets/1a89cbe6-df38-4862-8d11-9d977e0f4191">
</div>

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="700" alt="gambar" src="https://github.com/user-attachments/assets/1a1d0bb9-44d4-4de5-9907-47e5f20747a7">
</div>

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="700" alt="gambar" src="https://github.com/user-attachments/assets/d1bd2eff-4c57-4e91-a870-08b0f8b1fe16">
</div>

## 10. Memperbarui Kernel Armbian

Masuk ke sistem Armbian → Masukkan perintah:

```shell
# Jalankan sebagai pengguna root (sudo -i)
# Jika tidak ada parameter yang ditentukan, kernel akan diperbarui ke versi terbaru.
armbian-update
```

| Parameter Opsional | Nilai Default | Pilihan | Deskripsi |
| --- | --- | --- | --- |
| -r | ophub/kernel | `<owner>/<repo>` | Mengatur repositori di github.com untuk mengunduh kernel |
| -u | Otomatis | stable/flippy/beta/rk3588/rk35xx | Mengatur [akhiran tags](https://github.com/ophub/kernel/releases) dari kernel yang digunakan |
| -k | Versi Terbaru | Versi Kernel | Mengatur [versi kernel](https://github.com/ophub/kernel/releases/tag/kernel_stable) |
| -b | yes | yes/no | Mencadangkan kernel yang sedang digunakan secara otomatis saat pembaruan |
| -d | deb | tar/deb | Mengatur format paket kernel yang diutamakan. Jika tidak tersedia, skrip akan otomatis mencoba format alternatif. Format `deb` direkomendasikan untuk mengompilasi driver kustom. |
| -m | no | yes/no | Menggunakan u-boot mainline |
| -s | none | none/NamaDisk | [SOS] Memulihkan kernel sistem pada eMMC/NVMe/sdX atau disk lainnya |
| -h | none | none | Melihat informasi bantuan |

Contoh: `armbian-update -k 5.15 -u stable -d deb`

Parameter `-k` menerima nomor versi yang tepat (misalnya, `armbian-update -k 5.15.50`) atau seri versi (misalnya, `armbian-update -k 5.15`), yang secara otomatis memilih versi terbaru dalam seri tersebut.

Selama pembaruan kernel, kernel saat ini dicadangkan secara otomatis ke `/ddbr/backup`, dengan menyimpan tiga versi terbaru. Jika kernel yang baru diinstal tidak stabil, Anda dapat memulihkan kernel cadangan kapan saja:
```shell
# Masuk ke direktori kernel cadangan, misalnya 6.6.12
cd /ddbr/backup/6.6.12
# Jalankan perintah pembaruan kernel, yang akan otomatis menginstal kernel di direktori saat ini
armbian-update
```

[SOS]: Jika pembaruan yang tidak lengkap atau masalah lain menyebabkan sistem tidak dapat boot dari eMMC/NVMe/sdX, boot Armbian dari disk lain (misalnya, USB) dengan versi kernel apa pun, lalu jalankan `armbian-update -s` untuk memulihkan kernel ke eMMC/NVMe/sdX. Tanpa parameter disk, kernel secara default dipulihkan dari perangkat USB ke eMMC/NVMe/sdX. Untuk sistem dengan beberapa disk, tentukan nama disk tujuan secara eksplisit. Contoh:

```shell
# Pulihkan kernel di eMMC
armbian-update -s mmcblk1
# Pulihkan kernel di NVMe
armbian-update -s nvme0n1
# Pulihkan kernel di perangkat penyimpanan yang dapat dilepas
armbian-update -s sda
# Nama disk dapat disingkat menjadi mmcblk1/nvme0n1/sda, dll., atau gunakan nama lengkap seperti /dev/sda
armbian-update -s /dev/sda
# Jika perangkat hanya memiliki satu penyimpanan internal (eMMC/NVMe/sdX), parameter nama disk dapat dihilangkan
armbian-update -s
```

Jika masalah jaringan menghalangi pengunduhan dari github.com, unduh file kernel secara manual, unggah ke direktori mana pun di sistem Armbian Anda, masuk ke direktori tersebut, lalu jalankan `armbian-update` untuk instalasi lokal. Sistem secara otomatis memprioritaskan file kernel lokal jika satu set lengkap terdeteksi di direktori saat ini. Kernel tersedia dalam format `tar` dan `deb`. Masing-masing memerlukan 4 file:

- 4 file yang diperlukan untuk pembaruan format `tar` adalah: `header-xxx.tar.gz`, `boot-xxx.tar.gz`, `dtb-xxx.tar.gz`, dan `modules-xxx.tar.gz`.
- 4 file yang diperlukan untuk pembaruan format `deb` adalah: `linux-image-xxx.deb`, `linux-dtb-xxx.deb`, `linux-headers-xxx.deb`, dan `linux-libc-dev-xxx.deb`.
- File kernel tambahan bersifat opsional dan tidak memengaruhi proses pembaruan, karena sistem dapat mengidentifikasi file yang diperlukan secara akurat. Versi kernel apa pun yang didukung dapat diinstal, misalnya beralih dari 6.6.12 ke 5.15.50.

Opsi kustom yang diatur melalui `-r`/`-u`/`-b`/`-d` dapat disimpan secara permanen di `/etc/ophub-release` agar tidak perlu dimasukkan ulang setiap kali. Pengaturan yang sesuai adalah:

```shell
# Tetapkan nilai untuk parameter kustom
-r  :  KERNEL_REPO='ophub/kernel'
-u  :  KERNEL_TAGS='stable'
-b  :  KERNEL_BACKUP='yes'
-d  :  DOWNLOAD_TYPE='deb'
```

## 11. Menginstal Perangkat Lunak Umum

Masuk ke sistem Armbian → Masukkan perintah:

```shell
armbian-software
```

Gunakan `armbian-software -u` untuk memperbarui daftar pusat perangkat lunak lokal. Berdasarkan masukan komunitas di [Issue](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), [perangkat lunak](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) yang umum digunakan secara bertahap diintegrasikan dengan dukungan instalasi, pembaruan, dan penghapusan satu klik. Ini mencakup `docker images`, `desktop software`, `application services`, dll. Lihat [petunjuk](armbian_software.md) selengkapnya.

Gunakan `armbian-apt` untuk memilih mirror perangkat lunak yang sesuai dengan wilayah Anda guna meningkatkan kecepatan unduhan. Misalnya, pilih sumber `mirrors.tuna.tsinghua.edu.cn` di Tiongkok:

```shell
armbian-apt

[ STEPS ] Selamat datang di Alat Pengalih Sumber Mirror APT.
[ INFO ] Silakan pilih situs mirror [ bookworm ].
  ┌──────┬───────────────────┬─────────────────────────────────┐
  │  ID  │  Negara/Wilayah   │  Situs Mirror                   │
  ├──────┼───────────────────┼─────────────────────────────────┤
  │   0  │  -                │  Pulihkan sumber default        │
  ├──────┼───────────────────┼─────────────────────────────────┤
  │   1  │  Tiongkok         │  mirrors.tuna.tsinghua.edu.cn   │
  │   2  │  Tiongkok         │  mirrors.bfsu.edu.cn            │
  │   3  │  Tiongkok         │  mirrors.aliyun.com             │
  │   4  │  Tiongkok         │  mirrors.huaweicloud.com        │
  │   5  │  Taiwan, Tiongkok │  mirror.twds.com.tw             │
  ├──────┼───────────────────┼─────────────────────────────────┤
  │   6  │  Rusia            │  mirror.yandex.ru               │
  │   7  │  Korea Selatan    │  ftp.kaist.ac.kr                │
  │   8  │  Korea Selatan    │  ftp.lanet.kr,ftp.kaist.ac.kr   │
  │   9  │  Singapura        │  mirror.sg.gs                   │
  │  10  │  Australia        │  mirror.aarnet.edu.au           │
  ├──────┼───────────────────┼─────────────────────────────────┤
  │  11  │  Amerika Serikat  │  mirrors.ocf.berkeley.edu       │
  │  12  │  Amerika Serikat  │  files.openstack.org/mirror     │
  │  13  │  Amerika Serikat  │  steadfastnet.com,leaseweb.net  │
  │  14  │  Kanada           │  mirror.csclub.uwaterloo.ca     │
  │  15  │  Kanada           │  mirror.servercodes.com         │
  ├──────┼───────────────────┼─────────────────────────────────┤
  │  16  │  Denmark          │  ftp.openbsd.dk/mirrors         │
  │  17  │  Denmark          │  mirrors.dotsrc.org             │
  │  18  │  Jerman           │  mirror.dogado.de               │
  │  19  │  Jerman           │  ftp.de.debian.org,ftp.fau.de   │
  │  20  │  Inggris          │  mirror.yuki.net.uk             │
  └──────┴───────────────────┴─────────────────────────────────┘
[ OPTIONS ] Silakan masukkan ID: 1
[ INFO ] ID sumber mirror yang dipilih: [ 1 ]
[ STEPS ] Mengubah sumber mirror APT menjadi: [ mirrors.tuna.tsinghua.edu.cn ]
[ INFO ] Rilis sistem: [ bookworm ]
[ SUCCESS ] Sumber mirror APT berhasil diubah.
```

Memilih ID `0` akan memulihkan sumber default dari file cadangan, dan `armbian-apt -h` menampilkan informasi bantuan. Tidak ada file yang diubah sampai ID yang valid dimasukkan, sehingga membatalkan prompt akan membiarkan sumber tetap tidak berubah.

## 12. Pertanyaan yang Sering Diajukan

Bagian ini membahas masalah umum yang ditemui saat menggunakan Armbian.

### 12.1 Tabel Korespondensi dtb dan u-boot untuk Setiap Box

Daftar TV box yang didukung terdapat dalam file konfigurasi [/etc/model_database.conf](../build-armbian/armbian-files/common-files/etc/model_database.conf) di sistem `Armbian`.

### 12.2 Petunjuk Kontrol Tampilan Layar LED

Silakan lihat [petunjuk](led_screen_display_control.md).

### 12.3 Cara Memulihkan Sistem Android TV Asli

Cadangkan dan pulihkan sistem Android TV menggunakan `armbian-ddbr`.

Sebagai alternatif, flash sistem Android ke eMMC melalui kabel USB. Image sistem Android tersedia di [Tools](https://github.com/ophub/kernel/releases/tag/tools).

#### 12.3.1 Pencadangan dan Pemulihan Menggunakan Armbian-ddbr

Sebelum menginstal Armbian pada perangkat baru, cadangkan sistem Android TV asli untuk berjaga-jaga jika pemulihan diperlukan di kemudian hari. Boot Armbian dari `TF/SD/USB`, jalankan `armbian-ddbr`, lalu masukkan `b` saat diminta untuk membuat cadangan. Cadangan disimpan ke `/ddbr/BACKUP-arm-64-emmc.img.gz` — unduh dan simpan di lokasi yang aman. Untuk memulihkan, unggah file cadangan ke path yang sama di perangkat `TF/SD/USB`, jalankan `armbian-ddbr`, lalu masukkan `r` saat diminta.

#### 12.3.2 Pemulihan Menggunakan Alat Flashing Amlogic

- Jika perangkat masih dapat boot dari USB setelah catu daya dicolokkan kembali, cukup instal ulang. Coba beberapa kali jika diperlukan.

- Jika layar tetap hitam dan perangkat tidak dapat boot dari USB, diperlukan pemulihan dengan metode short-circuit (hubung singkat). Pertama pulihkan sistem Android asli, lalu instal ulang Armbian. Unduh dan instal alat pemulihan [amlogic_usb_burning_tool](https://github.com/ophub/kernel/releases/tag/tools). Siapkan [kabel USB male-to-male](https://user-images.githubusercontent.com/68696949/159267576-74ad69a5-b6fc-489d-b1a6-0f8f8ff28634.png) dan [penjepit kertas](https://user-images.githubusercontent.com/68696949/159267790-38cf4681-6827-4cb6-86b2-19c7f1943342.png).

- Dengan x96max+ sebagai contoh, temukan [titik short-circuit](https://user-images.githubusercontent.com/68696949/110590933-67785300-81b3-11eb-9860-986ef35dca7d.jpg) pada motherboard dan unduh [paket sistem Android TV](https://github.com/ophub/kernel/releases/tag/tools). Image sistem Android TV dan diagram titik short-circuit untuk perangkat umum lainnya juga [tersedia di sini](https://github.com/ophub/kernel/releases/tag/tools).

```shell
Cara pengoperasian:

1. Buka USB Burning Tool:
   [ File → Import image ]: X96Max_Plus2_20191213-1457_ATV9_davietPDA_v1.5.img
   [ Pilih ]：Erase Flash
   [ Pilih ]：Erase bootloader
   Klik tombol [ Start ]
2. Gunakan [ penjepit kertas ] untuk menghubungsingkatkan [ dua titik short-circuit ] pada motherboard box,
   dan pada saat yang sama gunakan [ kabel data USB dua sisi male ] untuk menghubungkan [ box ] dengan [ komputer ].
3. Ketika Anda melihat [ bilah progres mulai bergerak ], lepaskan penjepit kertas, jangan hubungsingkatkan lagi.
4. Ketika Anda melihat [ bilah progres di 100% ], proses flashing selesai, box telah dipulihkan ke sistem Android TV.
   Klik tombol [ Stop ], cabut [ kabel data USB dua sisi male ] antara [ box ] dan [ komputer ].
5. Jika salah satu langkah di atas gagal, coba lagi hingga berhasil.
   Jika bilah progres tidak bergerak, Anda dapat mencoba mencolokkan catu daya. Biasanya, Anda tidak memerlukan catu daya untuk flashing, cukup daya dari kabel USB dua sisi male sudah memenuhi kebutuhan.
```

Setelah pengaturan pabrik dipulihkan, ikuti langkah yang sama seperti instalasi awal Armbian.

### 12.4 Mengatur Box untuk Boot dari USB/TF/SD

Tergantung situasi Anda, gunakan metode instalasi awal atau metode instalasi ulang.

#### 12.4.1 Instalasi Awal Sistem Armbian

- Masukkan USB/TF/SD yang berisi sistem terinstal ke dalam box.
- Aktifkan mode pengembang: Pengaturan → Tentang perangkat → Nomor versi (misalnya, X96max plus...), ketuk nomor versi 5 kali dengan cepat hingga muncul `You are now a developer`.
- Aktifkan debugging USB: Sistem → Opsi lanjutan → Opsi pengembang → aktifkan `USB debugging` dan debugging `ADB`.
- Instal ADB: Unduh [adb](https://github.com/ophub/kernel/releases/tag/tools) dan ekstrak. Salin `adb.exe`, `AdbWinApi.dll`, dan `AdbWinUsbApi.dll` ke `c:\windows\system32` dan `c:\windows\syswow64`. Verifikasi instalasi dengan menjalankan `adb --version` di command prompt.
- Buka command prompt dan jalankan `adb connect 192.168.1.137` (ganti dengan IP perangkat Anda, yang dapat ditemukan di panel admin router Anda). Koneksi yang berhasil akan menampilkan `connected to 192.168.1.137:5555`.
- Jalankan `adb shell reboot update` — perangkat akan reboot dari USB/TF/SD yang dimasukkan. Akses sistem melalui alamat IP-nya di browser atau melalui SSH.

#### 12.4.2 Instalasi Ulang Sistem Armbian

- Dalam situasi normal, cukup masukkan drive USB berisi Armbian dan boot darinya. USB memiliki prioritas boot di atas eMMC.
- Jika perangkat tidak boot dari USB, ganti nama file `boot.scr` di direktori `/boot` pada eMMC (misalnya, menjadi `boot.scr.bak`), lalu masukkan drive USB dan boot kembali.
### 12.5 Menonaktifkan Penerima Inframerah

Dukungan penerima inframerah diaktifkan secara default. Jika perangkat digunakan sebagai server, nonaktifkan modul kernel IR untuk mencegah pematian yang tidak disengaja. Untuk menonaktifkan IR sepenuhnya, tambahkan baris berikut:

```shell
blacklist meson_ir
```

ke `/etc/modprobe.d/blacklist.conf` lalu mulai ulang.

### 12.6 Pemilihan file boot

- Di antara perangkat yang diketahui, hanya `T95(s905x)` / `T95Z-Plus(s912)` / `BesTV-R3300L(s905l-b)` dan beberapa lainnya yang memerlukan file `/bootfs/extlinux/extlinux.conf`, yang sudah disertakan secara default di sistem. Jika perangkat lain memerlukannya, tulis sistem ke USB, buka partisi `boot`, lalu ganti nama `/boot/extlinux/extlinux.conf.bak` dengan menghapus ekstensi `.bak`. Saat menginstal ke eMMC, `armbian-install` secara otomatis mendeteksi dan membuat file `extlinux.conf` jika diperlukan.

- Semua perangkat lain melakukan boot hanya menggunakan `/boot/uEnv.txt` — jangan ubah file `extlinux.conf.bak`.

### 12.7 Konfigurasi Jaringan

#### 12.7.1 Konfigurasi Jaringan Menggunakan Interfaces

Isi default file konfigurasi jaringan `/etc/network/interfaces` adalah sebagai berikut:

```shell
source /etc/network/interfaces.d/*
# Jaringan dikelola oleh Network manager
auto lo
iface lo inet loopback
```

##### 12.7.1.1 Penetapan Alamat IP melalui DHCP

```shell
source /etc/network/interfaces.d/*

auto eth0
iface eth0 inet dhcp
```

##### 12.7.1.2 Pengaturan Manual Alamat IP Statis

Sesuaikan nilai IP, gateway, dan DNS agar cocok dengan konfigurasi jaringan Anda.

```shell
source /etc/network/interfaces.d/*

auto eth0
allow-hotplug eth0
iface eth0 inet static
hwaddress ether 12:34:56:78:9A:DA
address 192.168.1.100
netmask 255.255.255.0
gateway 192.168.1.1
dns-nameservers 192.168.1.1
```

##### 12.7.1.3 Membangun Jaringan yang Saling Terhubung Menggunakan OpenWrt di Docker

Ubah alamat MAC sesuai kebutuhan.

```shell
source /etc/network/interfaces.d/*

allow-hotplug eth0
no-auto-down eth0
auto eth0
iface eth0 inet manual

auto macvlan
iface macvlan inet dhcp
        pre-up ip link add macvlan link eth0 type macvlan mode bridge
        post-down ip link del macvlan link eth0 type macvlan mode bridge

auto lo
iface lo inet loopback
```

#### 12.7.2 Manajemen Jaringan Menggunakan NetworkManager

##### 12.7.2.1 Membuat Koneksi Jaringan Baru

Prasyarat untuk membuat atau mengubah koneksi jaringan.

###### 12.7.2.1.1 Mendapatkan Nama Antarmuka Jaringan

Periksa antarmuka jaringan yang tersedia.

```shell
nmcli device | grep -E "^[e].*|^[w].*|^[D].*|^[T].*" | awk '{printf "%-19s%-19s\n",$1,$2}'
```

Kolom `DEVICE` menampilkan nama antarmuka jaringan, dan kolom `TYPE` menampilkan jenis antarmuka jaringan.

`eth0` adalah antarmuka Ethernet pertama, `eth1` adalah yang kedua, dan seterusnya. Antarmuka nirkabel mengikuti konvensi yang sama.

```shell
DEVICE             TYPE
eth0               ethernet
eth1               ethernet
eth2               ethernet
eth3               ethernet
wlan0              wifi
wlan1              wifi
```

###### 12.7.2.1.2 Mendapatkan Nama Koneksi Jaringan yang Sudah Ada

Tampilkan daftar koneksi jaringan yang sudah ada di perangkat, baik yang aktif maupun tidak aktif. Hindari menggunakan kembali nama koneksi yang sudah ada saat membuat koneksi baru.

```shell
nmcli connection show | grep -E ".*|^[N].*" | awk '{printf "%-19s%-19s\n", $1,$3}'
```

Kolom `NAME` menampilkan nama koneksi jaringan yang sudah ada, dan kolom `TYPE` menampilkan jenis antarmuka jaringan.

`ethernet` = kabel, `wifi` = nirkabel, `bridge` = bridge

```shell
NAME               TYPE
cnc                ethernet
lan                ethernet
lte                ethernet
tel                ethernet
docker0            bridge
titanium           wifi
cpe                wifi
```

###### 12.7.2.1.3 Membuat Koneksi Jaringan Kabel

Buat koneksi jaringan baru pada antarmuka `eth0` dengan aktivasi langsung (`Alamat IP Dinamis` - `IPv4 / IPv6`).

```shell
# Atur ENV
MYCON=ether1                  # Nama koneksi jaringan baru
MYETH=eth0                    # Nama antarmuka jaringan = eth0 / eth1 / eht2 / eth3
IPV6AGM=stable-privacy        # Mode status alamat IPv6 = stable-privacy / eui64

# Tambah ETH
nmcli connection add \
con-name $MYCON \
type ethernet \
ifname $MYETH \
autoconnect yes \
ipv6.addr-gen-mode $IPV6AGM
nmcli connection up $MYCON
ip -c -br address
```

Buat koneksi jaringan baru pada antarmuka `eth0` dengan aktivasi langsung (`Alamat IP Statis` - `IPv4`).

```shell
# Atur ENV
MYCON=ether1                  # Nama koneksi jaringan
MYETH=eth0                    # Nama antarmuka jaringan = eth0 / eth1 / eht2 / eth3
IP=192.168.67.167/24          # Alamat IP HOST, dengan 24 sebagai subnet mask yang setara dengan 255.255.255.0
GW=192.168.67.1               # Gateway
DNS=119.29.29.29,223.5.5.5    # Alamat server DNS

# Ubah CON
nmcli connection add \
con-name $MYCON \
type ethernet \
ifname $MYETH \
autoconnect yes \
ipv4.method manual \
ipv4.addresses $IP \
ipv4.gateway $GW \
ipv4.dns $DNS
nmcli connection up $MYCON
ip -c -br address
```

###### 12.7.2.1.4 Membuat Koneksi Jaringan Nirkabel

Buat koneksi jaringan pada antarmuka `wlan0` dengan aktivasi langsung (`Alamat IP dinamis` - `IPv4 / IPv6`).

```shell
# Atur ENV
MYCON=ssid                    # Nama koneksi jaringan baru, disarankan menggunakan SSID WiFi sebagai nama koneksi
MYSSID=ssid                   # SSID WiFi, peka huruf besar/kecil
MYPSWD=passwd                 # Kata sandi WiFi
MYWSKM=wpa-psk                # Pilihan keamanan WPA-WPA2 = wpa-psk atau WPA3 = sae (lihat metode enkripsi yang digunakan di router nirkabel atau AP)
MYWLAN=wlan0                  # Nama antarmuka jaringan = wlan0 / wlan1
IPV6AGM=stable-privacy        # Mode status alamat IPv6 = stable-privacy / eui64

# Tambah WLAN
nmcli connection add \
con-name $MYCON \
type wifi \
ifname $MYWLAN \
autoconnect yes \
ipv6.addr-gen-mode $IPV6AGM \
wifi.ssid $MYSSID \
wifi-sec.key-mgmt $MYWSKM \
wifi-sec.psk $MYPSWD
nmcli connection up $MYCON
ip -c -br address
```

##### 12.7.2.2 Mengubah SSID atau PASSWD WiFi pada Koneksi Jaringan Nirkabel

Perbarui `SSID atau kata sandi WiFi` pada koneksi jaringan nirkabel `ssid` dengan aktivasi langsung.

```shell
# Atur ENV
MYCON=ssid                    # Nama koneksi jaringan nirkabel
MYSSID=ssid                   # SSID WiFi, peka huruf besar/kecil
MYPSWD=passwd                 # Kata sandi WiFi
MYWSKM=wpa-psk                # Pilihan keamanan WPA-WPA2 = wpa-psk atau WPA3 = sae

# Tambah WLAN
nmcli connection modify $MYCON \
wifi.ssid $MYSSID \
wifi-sec.key-mgmt $MYWSKM \
wifi-sec.psk $MYPSWD
nmcli connection up $MYCON
ip -c -br address
```

##### 12.7.2.3 Mengubah Metode Alokasi Alamat Jaringan

###### 12.7.2.3.1 Alamat IP Statis - IPv4

Ubah metode alokasi IP menjadi `Alamat IP statis` untuk koneksi jaringan `ether1` dengan aktivasi langsung.

*Berlaku untuk koneksi kabel maupun nirkabel

```shell
# Atur ENV
MYCON=ether1                  # Nama koneksi jaringan
IP=192.168.67.167/24          # Alamat IP HOST, dengan 24 sebagai subnet mask yang setara dengan 255.255.255.0
GW=192.168.67.1               # Gateway
DNS=119.29.29.29,223.5.5.5    # Alamat server DNS

# Ubah CON
nmcli connection modify $MYCON \
ipv4.method manual \
ipv4.addresses $IP \
ipv4.gateway $GW \
ipv4.dns $DNS
nmcli connection up $MYCON
ip -c -br address
```

###### 12.7.2.3.2 DHCP Mendapatkan Alamat IP Dinamis - IPv4 / IPv6

Ubah metode alokasi IP menjadi `DHCP` untuk koneksi jaringan `ether1` dengan aktivasi langsung.

*Berlaku untuk koneksi kabel maupun nirkabel

```shell
# Atur ENV
MYCON=ether1                  # Nama koneksi jaringan

# Ubah CON
nmcli connection modify $MYCON \
ipv4.method auto \
ipv6.method auto
nmcli connection up $MYCON
ip -c -br address
```

##### 12.7.2.4 Mengubah Alamat MAC Koneksi Jaringan

Ubah alamat MAC pada koneksi jaringan untuk mengatasi konflik alamat MAC.

###### 12.7.2.4.1 Metode 1: Gunakan perintah `nmcli` untuk mengubah alamat MAC

```shell
# Gunakan perintah `nmcli connection show` untuk melihat nama antarmuka jaringan
nmcli connection show
# Hasil yang ditampilkan berisi nama antarmuka jaringan, misalnya 'Wired connection 1'
NAME                UUID                                  TYPE      DEVICE
Wired connection 1  24d63dc7-c46f-3bf1-912f-1c33eb94338b  ethernet  eth0
lo                  35ca24e5-bdc0-4658-8ac8-435ee22e07f3  loopback  lo
Wired connection 2  59660b21-b460-30e0-8cb3-89b886556955  ethernet  --

# Atur ENV
MYCON='Wired connection 1'    # Nama koneksi jaringan, pastikan sesuai dengan jenis antarmuka jaringan
MYTYPE='802-3-ethernet'       # Jenis antarmuka jaringan = Kartu jaringan kabel / Kartu jaringan nirkabel
                              #                        = 802-3-ethernet     / 802-11-wireless
MYMAC='12:34:56:78:9A:BC'     # Atur alamat MAC baru

# Ubah CON
nmcli connection modify "${MYCON}" ${MYTYPE}.cloned-mac-address ${MYMAC}
nmcli connection up "${MYCON}"
ip -c a show "${MYCON}"
```

* Mengubah parameter jaringan tertentu dapat menyebabkan jaringan terputus sementara lalu tersambung kembali.
* Bergantung pada lingkungan perangkat keras dan perangkat lunak, perubahan memerlukan waktu `1–15` detik untuk diterapkan. Jika perubahan tidak berlaku dalam rentang waktu tersebut, periksa konfigurasi perangkat keras dan perangkat lunak Anda.

###### 12.7.2.4.2 Metode 2: Mengubah alamat MAC melalui file konfigurasi

Buat file konfigurasi penimpaan alamat MAC.

```shell
sudo mkdir -p /etc/systemd/network/
sudo nano /etc/systemd/network/10-mac-override.link
```

Tambahkan konten berikut:

```shell
[Match]
# Tentukan nama antarmuka jaringan yang alamat MAC-nya perlu diubah
OriginalName=eth0

[Link]
# Atur alamat MAC yang valid
MACAddress=02:55:66:77:88:99
```

Perubahan berlaku setelah reboot.

##### 12.7.2.5 Cara Menonaktifkan IPv6

Gunakan `nmcli` untuk menonaktifkan `IPv6` dari baris perintah. Silakan lihat [disable-ipv6](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/using-networkmanager-to-disable-ipv6-for-a-specific-connection_configuring-and-managing-networking) sebagai sumbernya.

Langkah 1: Lihat daftar koneksi jaringan:

```shell
NAME                 UUID                                   TYPE       DEVICE
Wired connection 1   8a7e0151-9c66-4e6f-89ee-65bb2d64d366   ethernet   eth0
...
```

Langkah 2: Atur parameter ipv6.method pada koneksi menjadi disabled:

```shell
nmcli connection modify "Wired connection 1" ipv6.method "disabled"
```

Langkah 3: Sambungkan kembali ke jaringan:

```shell
nmcli connection up "Wired connection 1"
```

Langkah 4: Verifikasi status koneksi. Jika tidak muncul entri inet6, berarti IPv6 telah dinonaktifkan:

```shell
ip address show eth0
```

Langkah 5: Pastikan bahwa `/proc/sys/net/ipv6/conf/eth0/disable_ipv6` berisi `1`:

```shell
# cat /proc/sys/net/ipv6/conf/eth0/disable_ipv6
1
```

Sebagai alternatif, nonaktifkan IPv6 di seluruh sistem dengan menambahkan baris berikut ke `/etc/sysctl.conf`:

```shell
# Nonaktifkan IPv6 secara default
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

#### 12.7.3 Cara Mengaktifkan Nirkabel

Beberapa perangkat mendukung konektivitas nirkabel. Untuk petunjuk penggunaan mode AP nirkabel, silakan lihat panduannya. Untuk detail konfigurasi layanan DHCP bersama mode ini, silakan lihat panduannya. Untuk menggunakan mode klien nirkabel, silakan lihat petunjuk di bawah ini:

```shell
# Instal alat manajemen
sudo apt-get install network-manager

# Periksa perangkat jaringan
sudo nmcli dev

# Aktifkan nirkabel
sudo nmcli r wifi on

# Pindai jaringan nirkabel
sudo nmcli dev wifi

# Sambungkan ke jaringan nirkabel
sudo nmcli dev wifi connect "nama wifi" password "kata sandi wifi"

# Tampilkan daftar koneksi jaringan yang tersimpan
sudo nmcli connection show

# Putuskan koneksi
sudo nmcli connection down "nama wifi"

# Lupakan koneksi dan batalkan koneksi otomatis
sudo nmcli connection delete "nama wifi"
```

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="800" alt="gambar" src="https://user-images.githubusercontent.com/68696949/230541872-565a655e-2781-4170-8898-0ae096725506.png">
</div>

#### 12.7.4 Cara Mengaktifkan Bluetooth

Beberapa perangkat mendukung Bluetooth. Aktifkan dengan cara berikut:

```shell
# Instal dukungan Bluetooth
armbian-config >> Network >> BT: Install Bluetooth support

# Reboot sistem
reboot
```

Setelah reboot, pastikan driver Bluetooth berfungsi. Lingkungan desktop dapat menyambungkan perangkat Bluetooth melalui menu. Konfigurasi berbasis terminal juga tersedia.

```shell
dmesg | grep Bluetooth
```

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/230545883-755a137d-f574-4b32-a26b-bea9cfbf6384.png">
</div>

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/230544120-5a63dcd4-9716-40d2-ba59-c27f7b9937f8.png">
</div>

```shell
# Sambungkan perangkat Bluetooth
armbian-config >> Network >> BT: Discover and connect Bluetooth devices
```

Bluetooth juga dapat dikelola melalui perintah terminal:

```shell
# Periksa status layanan Bluetooth
sudo systemctl status bluetooth

# Jika belum berjalan, jalankan layanan Bluetooth terlebih dahulu
sudo systemctl enable bluetooth
sudo systemctl start bluetooth

# Pindai perangkat Bluetooth di sekitar
bluetoothctl scan on

# Aktifkan mode dapat ditemukan (discoverable) Bluetooth
bluetoothctl discoverable on

# Pasangkan alamat MAC Bluetooth
bluetoothctl pair 12:34:56:78:90:AB

# Periksa perangkat Bluetooth yang telah dipasangkan
bluetoothctl paired-devices

# Sambungkan ke perangkat Bluetooth
bluetoothctl connect 12:34:56:78:90:AB

# Percayai perangkat agar mudah tersambung di lain waktu
bluetoothctl trust 12:34:56:78:90:AB

# Putuskan sambungan perangkat Bluetooth
bluetoothctl disconnect 12:34:56:78:90:AB

# Batalkan pemasangan perangkat Bluetooth
bluetoothctl remove 12:34:56:78:90:AB

# Blokir perangkat yang tersambung
bluetoothctl block 12:34:56:78:90:AB
```

### 12.8 Cara Menambahkan Tugas Startup

Skrip tugas startup sudah disertakan dalam sistem. Di Armbian, lokasinya adalah [/etc/custom_service/start_service.sh](../build-armbian/armbian-files/common-files/etc/custom_service/start_service.sh). Tambahkan tugas startup kustom Anda ke skrip ini sesuai kebutuhan.

### 12.9 Cara Memperbarui Skrip Layanan di Sistem

Jalankan `armbian-sync` untuk memperbarui semua skrip layanan lokal ke versi terbaru.

Jika `armbian-sync` gagal, versi yang terinstal mungkin sudah usang. Perbarui secara manual:

```shell
wget https://raw.githubusercontent.com/farishhz/amlogic-s9xxx-armbian/main/build-armbian/armbian-files/common-files/usr/sbin/armbian-sync -O /usr/sbin/armbian-sync

chmod +x /usr/sbin/armbian-sync

armbian-sync
```

### 12.10 Cara Mendapatkan Informasi Partisi Sistem Android di eMMC

Sebelum menulis Armbian ke eMMC, pastikan tabel partisi Android pada perangkat agar data ditulis ke area yang aman. Merusak tabel partisi dapat membuat sistem tidak bisa boot. Menulis ke area yang tidak aman dapat menyebabkan kegagalan boot atau galat seperti yang ditunjukkan di bawah ini:

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="800" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187075834-4ac40263-52ae-4538-a4b1-d6f0d5b9c856.png">
</div>

#### 12.10.1 Mendapatkan Informasi Partisi

Untuk versi Armbian yang dirilis dari repositori ini setelah November 2022, jalankan perintah berikut untuk menghasilkan URL yang berisi informasi partisi lengkap (perangkat tidak memerlukan koneksi internet):

```shell
ampart /dev/mmcblk2 --mode webreport 2>/dev/null
```

*Mode webreport diperkenalkan di ampart v1.2 (dirilis 2023.02.03). Jika perintah di atas tidak menghasilkan keluaran, versi Anda mungkin lebih lama. Gunakan perintah alternatif ini sebagai gantinya:*

```shell
echo "https://7ji.github.io/ampart-web-reporter/?dsnapshot=$(ampart /dev/mmcblk2 --mode dsnapshot 2>/dev/null | head -n 1)&esnapshot=$(ampart /dev/mmcblk2 --mode esnapshot 2>/dev/null | head -n 1)"
```

URL yang dihasilkan akan terlihat seperti ini:

```shell
https://7ji.github.io/ampart-web-reporter/?esnapshot=bootloader:0:4194304:0%20reserved:37748736:67108864:0%20cache:113246208:754974720:2%20env:876609536:8388608:0%20logo:893386752:33554432:1%20recovery:935329792:33554432:1%20rsv:977272832:8388608:1%20tee:994050048:8388608:1%20crypt:1010827264:33554432:1%20misc:1052770304:33554432:1%20instaboot:1094713344:536870912:1%20boot:1639972864:33554432:1%20system:1681915904:1073741824:1%20params:2764046336:67108864:2%20bootfiles:2839543808:754974720:2%20data:3602907136:4131389440:4&dsnapshot=logo::33554432:1%20recovery::33554432:1%20rsv::8388608:1%20tee::8388608:1%20crypt::33554432:1%20misc::33554432:1%20instaboot::536870912:1%20boot::33554432:1%20system::1073741824:1%20cache::536870912:2%20params::67108864:2%20data::-1:4
```

Buka URL ini di browser untuk melihat informasi partisi DTB dan eMMC:

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="800" alt="gambar" src="https://user-images.githubusercontent.com/24390674/216287642-e1b7be27-4d2c-4ac3-9fcc-15e06aebb97e.png">
<img width="800" alt="gambar" src="https://user-images.githubusercontent.com/24390674/216287654-d1929e21-d2b3-4fb6-bcf0-c454c88e21b9.png">
</div>

#### 12.10.2 Membagikan Informasi Partisi

Saat membagikan informasi partisi (misalnya, melaporkan perangkat baru atau meminta bantuan), bagikan URL-nya, bukan tangkapan layar. Gunakan layanan pemendek URL jika tautannya terlalu panjang.

- Informasi partisi di halaman web dibuat secara dinamis pada setiap kunjungan, sehingga anotasi dan format tabel dapat diperbarui seiring waktu.
- Selain itu, parameter partisi tidak dapat disalin dengan mudah dari tangkapan layar untuk dianalisis.

Tata letak tabel di halaman web dirancang agar mudah disalin-tempel ke Excel atau LibreOffice Calc, sehingga Anda tidak perlu menyusun parameter secara manual.

#### 12.10.3 Menafsirkan Informasi Partisi

Tabel DTB mencatat tata letak partisi yang diinginkan sebagaimana didefinisikan dalam DTB Android. Tata letak ini biasanya diakhiri dengan partisi `data` yang mengisi sisa ruang, sehingga perangkat dengan sistem (dan model) yang sama memiliki tata letak DTB yang identik. Tata letak partisi aktual dapat berbeda karena kapasitas eMMC yang berbeda, tetapi selalu diturunkan dari tata letak partisi DTB (yaitu, jika tata letak DTB dan ukuran eMMC yang tepat diketahui, tata letak partisi eMMC dapat ditentukan. *Apakah Anda memperhatikan bahwa contoh partisi DTB dan eMMC di atas berasal dari perangkat yang berbeda?*).

Tabel eMMC menunjukkan tata letak partisi aktual pada perangkat. Setiap baris mewakili sebuah area penyimpanan — baik partisi maupun celah antarpartisi (Amlogic menyisakan setidaknya 8MB di antara partisi, yang awalnya ditujukan untuk keperluan lain tetapi tidak digunakan bahkan pada S905X4 terbaru, sehingga praktis membuang ruang). Baris partisi ditampilkan berwarna hitam dengan nilai offset dan mask. Baris celah ditampilkan berwarna abu-abu tanpa nilai offset atau mask dan diberi label `gap`.

Kolom terakhir menunjukkan keamanan penulisan: hijau/`yes` = dapat ditulis, merah/`no` = tidak dapat ditulis, kuning dengan label = dapat ditulis secara bersyarat atau sebagian.

Menggunakan tabel di atas sebagai contoh, area `0+4M` (`0M~4M`) pada partisi `bootloader` tidak dapat ditulis, celah `32M` (`4M~36M`) setelahnya dapat ditulis, partisi `reserved` `36M+64M` (`36M~100M`) tidak dapat ditulis, dan area dari sana hingga celah sebelum `env` (`100M~836M`) sepenuhnya dapat ditulis. Mulai dari 1M setelah `env` (`837M hingga akhir`), area tersebut dapat ditulis jika logo boot Android tidak diperlukan. Rentang yang dapat ditulis di eMMC adalah:

- 4M~36M
- 100M~836M
- 837M~akhir

Jika logo boot Android diperlukan, partisi `logo` 852M + 32M (`852M~884M`) juga tidak dapat ditulis, sehingga rentang yang dapat ditulis berkurang menjadi:

- 4M~36M
- 100M~836M
- 837M~852M
- 884M~akhir

#### 12.10.4 Untuk Instalasi eMMC

Jika perangkat Anda gagal saat menggunakan `armbian-install` dan parameter `-a` (menggunakan [ampart](https://github.com/7Ji/ampart) untuk menyesuaikan tata letak partisi eMMC) bernilai `yes` (nilai default), maka box Anda tidak dapat menggunakan tata letak optimal (yaitu, menyesuaikan informasi partisi DTB agar hanya berisi `data`, lalu menghasilkan informasi partisi eMMC darinya, kemudian memindahkan semua partisi yang tersisa ke depan. Dengan cara ini, ruang mulai dari 117M dan seterusnya dapat digunakan). Anda perlu mengubah informasi partisi yang sesuai di [armbian-install](../build-armbian/armbian-files/common-files/usr/sbin/armbian-install).

Dalam file ini, ada tiga parameter utama untuk mendeklarasikan tata letak partisi: `BLANK1`, `BOOT`, `BLANK2`. Di antaranya, `BLANK1` menyatakan ukuran yang tidak dapat digunakan mulai dari awal eMMC; `BOOT` menyatakan ukuran partisi yang dibuat setelah `BLANK1` untuk menyimpan kernel, DTB, dan sebagainya, sebaiknya tidak kurang dari 256M; `BLANK2` menyatakan ukuran yang tidak dapat digunakan setelah `BOOT`. Ruang setelahnya akan digunakan untuk membuat partisi `ROOT` guna menyimpan semua data di luar titik mount `/boot` dalam sistem. Ketiganya harus berupa bilangan bulat, dengan satuan MiB (1 MiB = 1024 KiB = 1024^2 Byte)

Pada kasus yang dibahas di paragraf sebelumnya, yaitu ketika partisi `logo` tidak diperlukan, tentu kita ingin menggunakan seluruh ruang yang dapat dipakai, tetapi area `4M~36M` terlalu kecil untuk digunakan sebagai `BOOT`, sehingga hanya dapat dihitung ke dalam `BLANK1` yang tidak dapat digunakan. Area `100M~836M` lebih dari cukup untuk digunakan sebagai `BOOT`, sehingga 736M ini dapat dialokasikan seluruhnya untuk `BOOT`. Setelah itu, terdapat area `836M~837M` yang tidak dapat digunakan, yang diberikan kepada `BLANK2`, sehingga parameter yang digunakan seharusnya sebagai berikut (teks berikut hanya menggunakan `s905x3` sebagai contoh; jika SoC Anda berbeda, Anda perlu mengubah blok kode lain yang sesuai):

```shell
# Atur ukuran partisi (Satuan: MiB)
elif [[ "${AMLOGIC_SOC}" == "s905x3" ]]; then
    BLANK1="100"
    BOOT="736"
    BLANK2="1"
```
### 12.11 Cara membuat file u-boot

File u-boot adalah komponen penting untuk proses startup sistem. Proses memperoleh kode sumber dan alur kompilasinya sedikit berbeda antara platform Amlogic, Allwinner, dan Rockchip.

#### 12.11.1 Cara membuat file u-boot untuk perangkat Amlogic

Karena sebagian besar produsen perangkat Amlogic menjaga kode sumber mereka tetap tertutup, file terkait u-boot harus diekstrak dari perangkat sebelum kompilasi. Metode yang disajikan di sini berasal dari tutorial yang dibagikan oleh [unifreq](https://github.com/unifreq).

##### 12.11.1.1 Cara mengekstrak file bootloader dan dtb

Ekstraksi memerlukan perangkat lunak HxD. Unduh dari [situs resmi](https://mh-nexus.de/en/downloads.php?product=HxD20) atau [tautan cadangan](https://github.com/ophub/kernel/releases/download/tools/HxDSetup.2.5.0.0.zip).

Jalankan perintah berikut di panel `cmd` untuk mengekstrak file yang relevan dan mengunduhnya ke komputer lokal Anda.

```shell
# Gunakan alat adb untuk masuk ke box
adb connect 192.168.1.111
adb shell

# Perintah ekspor bootloader
dd if=/dev/block/bootloader of=/data/local/bootloader.bin

# Perintah ekspor dtb
cat /dev/dtb >/data/local/mybox.dtb

# Perintah ekspor gpio
cat /sys/kernel/debug/gpio >/data/local/mybox_gpio.txt

# Unduh file bootloader, dtb, dan gpio ke folder mybox di direktori root drive C pada komputer lokal Anda
adb pull /data/local/bootloader.bin C:\mybox
adb pull /data/local/mybox.dtb C:\mybox
adb pull /data/local/mybox_gpio.txt C:\mybox
```

##### 12.11.1.2 Cara membuat file acs.bin

Bagian terpenting dari u-boot mainline adalah acs.bin, yang menginisialisasi memori. u-boot bawaan pabrik terletak di awal sistem pada posisi 4MB. Gunakan file `bootloader.bin` yang diperoleh sebelumnya untuk mengekstrak file `acs.bin`.

Buka perangkat lunak HxD, buka file `bootloader.bin` yang telah diekspor, `Klik kanan - Pilih rentang (Select range)`, posisi awal `F200`, panjang `1000`, pilih `heksadesimal`.

<img width="400" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187056711-1b58ce71-2a7d-4e9b-a976-e5f278edaa53.png">

Salin hasil yang dipilih, lalu buat file baru, tempel dalam mode sisip (insert), abaikan peringatan, dan simpan sebagai file acs.bin.

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187056725-0a0e60af-6a21-4a6b-a2d5-f3d46b438a6a.png">
<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187056827-8419c738-3428-473e-9a95-ab7270170d98.png">
<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187056852-9f62f16a-f7f1-4c34-a2c2-78358d198f9a.png">
</div>

Jika bootloader terkunci, kode di area ini akan acak dan tidak berguna. Biasanya, akan ada banyak `0` seperti pada gambar di atas, `cfg` akan muncul beberapa kali berturut-turut, dan kata-kata terkait `ddr` akan muncul di tengahnya. Kode normal seperti ini dapat digunakan.

##### 12.11.1.3 Cara membuat file u-boot

Membuat u-boot memerlukan repositori sumber https://github.com/unifreq/amlogic-boot-fip dan https://github.com/unifreq/u-boot untuk mengompilasi dua file u-boot untuk perangkat Anda.

Di dalam kode sumber amlogic-boot-fip, satu-satunya file yang berbeda menurut model perangkat adalah acs.bin, semua file lainnya bersifat universal.

<img width="600" alt="gambar" src="https://user-images.githubusercontent.com/68696949/187057209-c4716384-46ef-4922-9710-8da7ae6db1e4.png">

Untuk petunjuk pembuatan, lihat dokumentasi khusus perangkat di https://github.com/unifreq/u-boot/tree/master/doc/board/amlogic.

Membuat u-boot menggunakan metode [unifreq](https://github.com/unifreq) memerlukan file acs.bin, dts, dan config milik perangkat. dts yang diekspor dari sistem Android tidak dapat langsung dikonversi ke format Armbian, sehingga file dts yang sesuai harus ditulis secara manual. Berdasarkan perbedaan perangkat keras spesifik perangkat Anda (sakelar, LED, kontrol daya, kartu TF, modul wifi SDIO, dll.), modifikasi dan buat file [dts](https://github.com/unifreq/linux-5.15.y/tree/main/arch/arm64/boot/dts/amlogic) dari file serupa di repositori kode sumber kernel.

Sebagai contoh, membuat u-boot untuk X96Max Plus:

```shell
~/make-uboot
    ├── amlogic-boot-fip
    │   ├── x96max-plus                                     # Buat direktori sendiri
    │   │   ├── asc.bin                                     # File sumber buatan sendiri
    │   │   └── other-copy-files...                         # Salin file dari direktori lain
    │   │
    │   ├── other-source-directories...
    │   └── other-source-files...
    │
    └── u-boot
        ├── configs
        │   └── x96max-plus_defconfig                       # File sumber buatan sendiri
        ├── arch
        │   └── arm
        │       └── dts
        │           ├── meson-sm1-x96-max-plus-u-boot.dtsi  # File sumber buatan sendiri
        │           ├── meson-sm1-x96-max-plus.dts          # File sumber buatan sendiri
        │           └── Makefile                            # Edit
        ├── fip
        │   ├── u-boot.bin                                  # File yang dihasilkan
        │   └── u-boot.bin.sd.bin                           # File yang dihasilkan
        ├── u-boot.bin                                      # File yang dihasilkan
        │
        ├── other-source-directories...
        └── other-source-files...
```

- Unduh kode sumber [amlogic-boot-fip](https://github.com/unifreq/amlogic-boot-fip). Di direktori root, buat direktori [x96max-plus](https://github.com/unifreq/amlogic-boot-fip/tree/master/x96max-plus). Selain file `asc.bin` yang Anda buat, semua file lainnya dapat disalin dari direktori lain.
- Unduh kode sumber [u-boot](https://github.com/unifreq/u-boot). Buat file [x96max-plus_defconfig](https://github.com/unifreq/u-boot/blob/master/configs/x96max-plus_defconfig) yang sesuai dan letakkan di direktori [configs](https://github.com/unifreq/u-boot/tree/master/configs). Buat file [meson-sm1-x96-max-plus-u-boot.dtsi](https://github.com/unifreq/u-boot/blob/master/arch/arm/dts/meson-sm1-x96-max-plus-u-boot.dtsi) dan [meson-sm1-x96-max-plus.dts](https://github.com/unifreq/u-boot/blob/master/arch/arm/dts/meson-sm1-x96-max-plus.dts) yang sesuai dan letakkan di direktori [arch/arm/dts](https://github.com/unifreq/u-boot/tree/master/arch/arm/dts), lalu edit [Makefile](https://github.com/unifreq/u-boot/blob/master/arch/arm/dts/Makefile) di direktori ini untuk menambahkan indeks file `meson-sm1-x96-max-plus.dtb`.
- Di direktori root kode sumber u-boot, ikuti langkah-langkah dalam dokumen https://github.com/unifreq/u-boot/blob/master/doc/board/amlogic/x96max-plus.rst.

Dua jenis file akan dihasilkan: `u-boot.bin` di direktori root u-boot adalah u-boot tidak lengkap untuk direktori `/boot` (sesuai dengan direktori [overload](https://github.com/ophub/u-boot/tree/main/u-boot/amlogic/overload)); `u-boot.bin` dan `u-boot.bin.sd.bin` di direktori `fip` adalah file u-boot lengkap untuk `/usr/lib/u-boot/` (sesuai dengan direktori [bootloader](https://github.com/ophub/u-boot/tree/main/u-boot/amlogic/bootloader)). Kedua versi lengkap tersebut berbeda 512 byte — yang lebih besar memiliki tambahan 512 byte berisi nol di bagian awal.

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="400" alt="gambar" src="https://user-images.githubusercontent.com/68696949/189039426-c127631f-77ca-4fcb-9fb6-4220045d712b.png">
<img width="400" alt="gambar" src="https://user-images.githubusercontent.com/68696949/189029320-e43a4cc9-b4b5-4de4-92fe-b17bd29020d0.png">
</div>

💡 Tips: Sebelum menulis ke eMMC untuk pengujian, tinjau bagian 12.3 untuk metode pemulihan. Pastikan Anda mengetahui lokasi titik short-circuit, memiliki file sistem Android asli berformat .img, dan telah memverifikasi proses flashing dengan short-circuit. Kuasai semua metode pemulihan sebelum melanjutkan.

#### 12.11.2 Cara membuat file u-boot untuk perangkat Rockchip

Karena sebagian besar produsen perangkat Rockchip telah membuka kode sumber u-boot mereka, kode sumber yang relevan dapat diperoleh langsung dari repositori mereka. Selain itu, beberapa kontributor open-source telah membagikan skrip kompilasi u-boot yang mudah digunakan. Berikut beberapa contoh yang menggambarkan berbagai metode kompilasi.

##### 12.11.2.1 Cara menggunakan skrip pembuatan u-boot dari Radxa

Mengambil kompilasi [Rock5B(rk3588)](https://wiki.radxa.com/Rock5/guide/build-u-boot-on-5b) sebagai contoh.

```shell
# 01.Instal dependensi build yang diperlukan
sudo apt-get update
sudo apt-get install -y git device-tree-compiler libncurses5 libncurses5-dev build-essential libssl-dev mtools bc python dosfstools flex bison

# 02.Siapkan ruang kerja Anda dan ambil kode sumber dari repositori Git Radxa
mkdir ~/rk3588-sdk && cd ~/rk3588-sdk
git clone -b stable-5.10-rock5 https://github.com/radxa/u-boot.git
git clone -b master https://github.com/radxa/rkbin.git
git clone -b debian https://github.com/radxa/build.git

# Penjelasan kode sumber:
# ~/rk3588-sdk/build/: File skrip pembantu Radxa dan file konfigurasi untuk membuat U-Boot, kernel Linux, dan rootfs.
# ~/rk3588-sdk/rkbin/: Biner Rockchip yang sudah dibuat sebelumnya, termasuk loader tahap pertama dan ATF (Arm Trustzone Firmware)
# ~/rk3588-sdk/u-boot/: Bootloader tahap kedua yang digunakan untuk memulai OS (misalnya Linux atau Android)

# 03.Build u-boot (untuk ROCK 5B)
cd ~/rk3588-sdk
./build/mk-uboot.sh rk3588-rock-5b

# 04.Setelah build berhasil, direktori ~/rk3588-sdk/out/u-boot akan terisi
~/rk3588-sdk/out/u-boot
├── idbloader.img
├── rk3588_spl_loader_v1.08.111.bin
├── spi
│   └── spi_image.img
└── u-boot.itb
```

Dengan menambahkan lebih banyak opsi di `board_configs.sh` dan `mk-uboot.sh` dalam kode sumber [radxa/build](https://github.com/radxa/build), file u-boot untuk perangkat lain juga dapat dikompilasi. Sebagai contoh, lihat petunjuk kompilasi untuk perangkat Beelink-IPC-R(rk3588).

##### 12.11.2.2 Cara menggunakan skrip pembuatan u-boot dari cm9vdA

cm9vdA menyediakan skrip dan petunjuk untuk mengompilasi u-boot dan kernel dalam proyek open-source mereka [cm9vdA/build-linux](https://github.com/cm9vdA/build-linux). Berikut adalah proses kompilasi yang terdokumentasi untuk berbagai perangkat Rockchip:

- Build u-boot untuk perangkat Lenovo-Leez-P710 (rk3399): Tautan
- Build u-boot untuk perangkat DLFR100 (rk3399): Tautan
- Build u-boot untuk perangkat ZYSJ (rk3399): Tautan

### 12.12 Kesalahan Pengenalan Ukuran Memori

Jika ukuran memori dikenali dengan salah (4GB dikenali sebagai 1–2GB adalah tidak normal; 3.7GB adalah normal), coba salin secara manual file `/boot/UBOOT_OVERLOAD` (catatan: "salin", bukan "ganti nama" — mengganti nama akan membuat sistem gagal boot setelah instalasi dan pembaruan). Saat digunakan dari `USB`, simpan sebagai `/boot/u-boot.ext`; saat digunakan dari `eMMC`, simpan sebagai `/boot/u-boot.emmc`.

Jangan menyalin file u-boot secara manual untuk tujuan lain apa pun. File u-boot yang salah akan menyebabkan kegagalan boot dan berbagai masalah lainnya.

### 12.13 Cara Mendekompilasi File dtb

#### 12.13.1 Dekompilasi File dtb Secara Langsung

Anda dapat langsung mendekompilasi file dtb yang ada dan melakukan adaptasi dengan menyesuaikan parameter terkait.

```shell
# Instal dependensi
sudo apt-get update
sudo apt-get install -y device-tree-compiler

# 1. Perintah dekompilasi (menghasilkan kode sumber dts dari file dtb)
dtc -I dtb -O dts -o xxx.dts xxx.dtb

# 2. Perintah kompilasi (menghasilkan file dtb dari dts)
dtc -I dts -O dtb -o xxx.dtb xxx.dts

# 3. Simpan data dan reboot
sync && reboot
```

#### 12.13.2 Ekspor DTS Kondisi Penuh dari Perangkat yang Sedang Berjalan (Direkomendasikan)

Selama proses adaptasi dan pemeliharaan perangkat tertentu, kita mungkin hanya memiliki akses ke file device tree biner yang sudah dikompilasi (.dtb), sementara kode sumber kernel yang sesuai (.dts) tidak tersedia. Dalam kasus seperti ini, disarankan untuk menjalankan perintah berikut pada sistem Armbian yang berfungsi dengan baik untuk langsung mendekompilasi dan mengekspor device tree yang sedang aktif dari lingkungan runtime kernel:

```shell
dtc -I fs -O dts /sys/firmware/devicetree/base > my_runtime.dts
```

Perintah ini mengekstrak data device tree langsung dari memori kernel, menghasilkan keluaran teks yang lebih akurat dan lengkap dibandingkan sekadar mendekompilasi file .dtb statis di disk. Hal ini karena bootloader (seperti U-Boot) atau firmware sistem secara dinamis memodifikasi atau menyuntikkan device tree berdasarkan hasil deteksi perangkat keras yang sebenarnya selama fase boot (misalnya: memperbarui parameter boot bootargs secara real time, mengubah status periferal tertentu secara dinamis, atau menyesuaikan alamat register reg). Mendekompilasi file statis di disk secara langsung tidak akan menangkap perubahan runtime ini.

Device tree runtime yang diperoleh melalui metode ini merupakan bentuk akhir yang diterapkan dan digunakan oleh kernel, yang secara akurat mencerminkan topologi aktual dan kondisi operasional perangkat keras di tingkat rendah sistem. Saat merujuk, memperbaiki, atau mengadaptasi ulang kode sumber .dts untuk perangkat, file ini sangat bernilai sebagai referensi, sehingga pemecahan masalah konflik dan pelengkapan konfigurasi periferal menjadi lebih akurat dan efisien.

### 12.14 Cara Mengubah Pengaturan cmdline

Pada perangkat Amlogic, tambahkan/ubah/hapus pengaturan di `/boot/uEnv.txt`. Pada perangkat Rockchip dan Allwinner, konfigurasikan di `/boot/armbianEnv.txt` (melalui parameter `extraargs` atau `extraboardargs`). Perangkat yang menggunakan `/boot/extlinux/extlinux.conf` dikonfigurasi di file tersebut. Reboot diperlukan setelah setiap perubahan.

- Misalnya, `Home Assistant Supervisor` hanya mendukung `docker cgroup v1`, sedangkan instalasi Docker default menggunakan v2. Untuk beralih ke v1, tambahkan `systemd.unified_cgroup_hierarchy=0` ke cmdline lalu reboot.

- Menambahkan `mmc_core.max_freq=50000000` ke cmdline membatasi frekuensi maksimum eMMC menjadi `50MHz`. eMMC pada beberapa box S905L2 tidak stabil pada frekuensi tinggi (HS200/HS400, 100MHz+); menurunkan frekuensi dapat mengatasi masalah seperti kegagalan boot, crash acak, kesalahan baca/tulis, dan ketidakstabilan secara umum.

- Menambahkan `max_loop=128` ke cmdline mengatur jumlah maksimum mount loop.

- Menambahkan `usbcore.usbfs_memory_mb=1024` ke cmdline meningkatkan buffer memori USBFS dari default `16 mb` (`cat /sys/module/usbcore/parameters/usbfs_memory_mb`), sehingga meningkatkan transfer file USB berukuran besar.

- Menambahkan `usbcore.usb3_disable=1` ke cmdline menonaktifkan semua perangkat USB 3.0.

- Menambahkan `usbcore.autosuspend=-1` ke cmdline menonaktifkan auto-suspend USB (mencegah perangkat USB mati untuk menghemat daya); menambahkan `rootdelay=120` membuat sistem menunggu 120 detik sebelum me-mount partisi root saat boot (memberi waktu bagi perangkat USB untuk siap); menambahkan `mitigations=off` menonaktifkan mitigasi kerentanan CPU (Spectre/Meltdown), sehingga meningkatkan performa.

- Menambahkan `extraargs=video=HDMI-A-1:1920x1080@60` ke cmdline memaksa tampilan ke 1080p.

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="700" alt="gambar" src="https://user-images.githubusercontent.com/68696949/216220941-47db0183-7b26-4768-81cf-2ee73d59d23e.png">
</div>

<div style="width:100%;margin-top:40px;margin:5px;">
<img width="700" alt="gambar" src="https://github.com/farishhz/amlogic-s9xxx-armbian/assets/68696949/a600dcad-d817-47eb-b529-4014019915b3">
</div>

### 12.15 Cara Menambahkan Perangkat Baru yang Didukung

Membuat sistem Armbian untuk suatu perangkat memerlukan `file konfigurasi perangkat`, `file sistem`, `file u-boot`, dan `file kontrol proses`. Cara menambahkan masing-masing dijelaskan di bawah ini:

#### 12.15.1 Tambahkan File Konfigurasi Perangkat

Di file konfigurasi [/etc/model_database.conf](../build-armbian/armbian-files/common-files/etc/model_database.conf), tambahkan konfigurasi perangkat berdasarkan status dukungan pengujiannya. Perangkat dengan `BUILD` bernilai `yes` akan dibuat secara default; nilai `BOARD` yang bersangkutan `harus unik`. Perangkat-perangkat ini dapat langsung menggunakan sistem Armbian default.

Perangkat yang diatur ke `no` tidak dikemas secara default. Untuk menggunakannya, unduh sistem Armbian dengan `FAMILY` yang sama, tulis ke `USB`, buka partisi boot USB di komputer Anda, lalu ubah `nama dtb FDT` di `/boot/uEnv.txt` agar sesuai dengan perangkat Anda.

#### 12.15.2 Tambahkan File Sistem

File umum ditempatkan di `build-armbian/armbian-files/common-files`, digunakan bersama oleh semua platform.

File khusus platform ditempatkan di `build-armbian/armbian-files/platform-files/<platform>`: [Amlogic](../build-armbian/armbian-files/platform-files/amlogic), [Rockchip](../build-armbian/armbian-files/platform-files/rockchip), dan [Allwinner](../build-armbian/armbian-files/platform-files/allwinner). Direktori `bootfs` berisi file partisi /boot, dan direktori `rootfs` berisi file sistem Armbian.

Untuk perangkat dengan kebutuhan konfigurasi khusus, tambahkan direktori tersendiri yang dinamai sesuai `BOARD` di `build-armbian/armbian-files/different-files`. Buat subdirektori `bootfs` dan `rootfs` sesuai kebutuhan untuk menambahkan file di bawah partisi `/boot` sistem atau path sistem lainnya. Semua nama folder sesuai dengan path sebenarnya di sistem Armbian. File-file ini dapat menambahkan file baru atau menimpa file dari direktori common dan platform.

#### 12.15.3 Tambahkan File u-boot

Perangkat seri `Amlogic` menggunakan bersama file [bootloader](https://github.com/ophub/u-boot/tree/main/u-boot/amlogic/bootloader) dan file [u-boot](https://github.com/ophub/u-boot/tree/main/u-boot/amlogic/overload). Jika ada file baru, letakkan di direktori yang sesuai. File `bootloader` akan otomatis ditambahkan ke direktori `/usr/lib/u-boot` sistem Armbian selama pembuatan sistem, dan file `u-boot` akan otomatis ditambahkan ke direktori `/boot`.

Untuk perangkat seri `Rockchip` dan `Allwinner`, tambahkan direktori file [u-boot](https://github.com/ophub/u-boot/tree/main/u-boot) tersendiri yang dinamai sesuai `BOARD` untuk setiap perangkat, dan file seri yang bersangkutan ditempatkan di direktori ini.

Selama pembuatan image Armbian, file-file u-boot ini akan ditulis ke file image Armbian yang sesuai oleh skrip rebuild berdasarkan konfigurasi di [/etc/model_database.conf](../build-armbian/armbian-files/common-files/etc/model_database.conf).

Untuk perangkat yang dapat menggunakan file U-Boot standar, sangat disarankan untuk menggunakannya secara langsung. Namun, beberapa perangkat mungkin tidak memiliki U-Boot yang sesuai. Jika perangkat tersebut sudah dapat menjalankan sistem Linux lain seperti Ubuntu, Anda dapat mencoba mempertahankan partisi kunci yang terkait dengan boot untuk menginstal Armbian atau OpenWrt. Partisi penting yang biasanya perlu dipertahankan meliputi `bootloader`, `reserved`, dan `env`.

Partisi-partisi ini dapat dicadangkan lalu ditulis kembali ke lokasi yang sesuai saat membuat image Armbian atau OpenWrt baru. Image yang dihasilkan, yang berisi partisi boot sistem asli, dapat ditulis ke eMMC secara langsung melalui perintah `dd` atau melalui alat instalasi bawaan (misalnya `armbian-install` milik Armbian atau plugin `Amlogic Service` milik OpenWrt).

Saat ini, perangkat yang menggunakan metode ini meliputi oes(a311d), oes-plus(s922x), dan oec-turbo(rk3566). Berikut ini menggunakan perangkat `oes(a311d)` sebagai contoh untuk menjelaskan prosedurnya secara rinci.

##### 12.15.3.1 Periksa Tata Letak Partisi

```shell
ampart /dev/mmcblk2

# Informasi partisi yang diperoleh adalah sebagai berikut:
# ===================================================================================
# IO seek EPT: Seeking to 37748736
# EPT report: 20 partitions in the table:
# ===================================================================================
# ID| name            |          offset|(   human)|            size|(   human)| masks
# -----------------------------------------------------------------------------------
#  0: bootloader                      0 (   0.00B)           400000 (   4.00M)      0
#     (GAP)                                                 2000000 (  32.00M)
#  1: reserved                  2400000 (  36.00M)          4000000 (  64.00M)      0
#     (GAP)                                                  800000 (   8.00M)
#  2: cache                     6c00000 ( 108.00M)         20000000 ( 512.00M)      2
#     (GAP)                                                  800000 (   8.00M)
#  3: env                      27400000 ( 628.00M)           800000 (   8.00M)      0
#     (GAP)                                                  800000 (   8.00M)
#  ... partisi lainnya ...
# ===================================================================================
```

##### 12.15.3.2 Cadangkan Partisi Kunci

```shell
dd if=/dev/mmcblk2 of=bootloader.bin bs=1M count=4 skip=0
dd if=/dev/mmcblk2 of=reserved.bin bs=1M count=8 skip=36
dd if=/dev/mmcblk2 of=env.bin bs=1M count=1 skip=628
```
Letakkan file cadangan di direktori yang sesuai pada repositori [u-boot](https://github.com/ophub/u-boot): [u-boot/amlogic/bootloader/a311d-oes](https://github.com/ophub/u-boot/tree/main/u-boot/amlogic/bootloader/a311d-oes).

Anda mungkin memperhatikan bahwa partisi reserved berukuran 64MB, namun hanya 8MB yang dicadangkan. Pada perangkat oes(a311d), hanya 8MB pertama yang berisi data penting; 56MB sisanya kosong. Berikut cara memverifikasinya:

```shell
# Pertama, cadangkan file lengkap 64MB dari partisi reserved:
dd if=/dev/mmcblk2 of=reserved_64M.bin bs=1M count=64 skip=36

# Kemudian, ekstrak 8MB pertama dari file cadangan reserved_64M.bin:
dd if=reserved_64M.bin of=reserved_first_8M.bin bs=1M count=8

# Selanjutnya, periksa isi heksadesimalnya:
hexdump -C reserved_first_8M.bin | less

# Sekarang, periksa beberapa baris terakhir dari keluarannya:
0071ffd0  4c 5e a8 1f fc 5b 5b 98  ae ef b0 97 0c 3b e8 c2  |L^...[[......;..|
0071ffe0  c8 e0 b2 74 3d 67 d5 3d  24 7b 63 b7 c7 73 f5 d8  |...t=g.=${c..s..|
0071fff0  a1 b8 38 a7 57 d6 b4 b5  e8 1c ba c0 07 0f f5 79  |..8.W..........y|
00720000  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
*
00800000
```

Dari analisis keluaran tersebut, alamat baris terakhir yang berisi data bukan nol adalah `0071fff0`. Mulai dari alamat `00720000`, seluruh isinya adalah `00` (nol). Utilitas hexdump menggunakan tanda bintang (`*`) untuk menandai baris yang berulang, artinya semua data dari `00720000` hingga akhir file di `00800000` (batas 8MB) bernilai nol. Mengonversi `0x00720000` ke desimal menghasilkan 7.471.104 byte (7,125 MB). Oleh karena itu, membulatkannya ke atas menjadi 8MB untuk pencadangan sudah cukup. Demikian pula, hanya 80KB pertama dari partisi env yang berisi data valid, sehingga 1MB sudah memadai.

##### 12.15.3.3 Tambahkan File Penulisan Partisi Khusus

Untuk detail implementasi, lihat fungsi `write_board_bootloader` di [/etc/armbian-board-release.conf](https://github.com/farishhz/amlogic-s9xxx-armbian/blob/main/build-armbian/armbian-files/different-files/a311d-oes/rootfs/etc/armbian-board-release.conf). Fungsi ini dipanggil selama proses rebuild image. File konfigurasi ini juga berfungsi sebagai pusat kustomisasi perangkat yang andal — memungkinkan kontrol presisi atas tata letak dan ukuran partisi image melalui parameter seperti `skip_mb="700"`, serta mendukung skrip kustom untuk operasi file kernel atau sistem. Semua kustomisasi tingkat lanjut yang spesifik untuk perangkat dikelola secara terpusat di file ini.

#### 12.15.4 Tambahkan File Kontrol Proses

Tambahkan opsi `BOARD` yang sesuai ke `armbian_board` di [file kontrol workflow yml](../.github/workflows/build-armbian-arm64-server-image.yml), yang mendukung penggunaan di `Actions` pada github.com.

### 12.16 Cara Mengatasi Kegagalan Boot Sistem atau Error I/O Penulisan eMMC yang Disebabkan oleh Frekuensi DTB

Ketika frekuensi DTB diatur terlalu tinggi, beberapa perangkat mungkin gagal boot dengan benar dan macet di layar boot. Contohnya dapat dilihat pada Issue ini, dengan keluaran error sebagai berikut:

```shell
Loading, please wait...
Starting systemd-udevd version 259.5-0ubuntus.4
Begin: Loading essential drivers ... done.
Begin: Running /scripts/init-premount ... done.
Begin: Mounting root file system... Begin: Running /scripts/local-top ... done.
Begin: Running /scripts/local-premount ... Scanning for Btrfs filesystems
```

Beberapa perangkat dapat mem-boot Armbian secara normal dari USB/SD/TF, tetapi melaporkan error penulisan I/O saat menulis ke eMMC, seperti kasus pada Issue ini:

```shell
[  284.338449] I/O error, dev mmcblk2, sector 0 op 0x1:(WRITE) flags 0x800 phys_seg 1 prio class 2
[  284.341544] Buffer I/O error on dev mmcblk2, logical block 0, lost async page write
[  284.446972] I/O error, dev mmcblk2, sector 0 op 0x1:(WRITE) flags 0x800 phys_seg 1 prio class 2
[  284.450074] Buffer I/O error on dev mmcblk2, logical block 0, lost async page write
[  284.497746] I/O error, dev mmcblk2, sector 0 op 0x1:(WRITE) flags 0x800 phys_seg 1 prio class 2
[  284.500871] Buffer I/O error on dev mmcblk2, logical block 0, lost async page write
```

Dalam kasus seperti ini, sesuaikan kecepatan mode kerja dan frekuensi dtb untuk menstabilkan dukungan baca/tulis penyimpanan. Dalam mode SDR, frekuensinya adalah dua kali kecepatan; dalam mode DDR, frekuensinya sama dengan kecepatan. Sebagai contoh:

```shell
sd-uhs-sdr12
sd-uhs-sdr25
sd-uhs-sdr50
sd-uhs-ddr50
sd-uhs-sdr104

max-frequency = <208000000>;
```

Ambil cuplikan kode dalam file [dts](https://github.com/unifreq/linux-5.15.y/tree/main/arch/arm64/boot/dts/amlogic) dari kode sumber kernel sebagai contoh:

```shell
/* Kartu SD */
&sd_emmc_b {
	status = "okay";

	bus-width = <4>;
	cap-sd-highspeed;
	sd-uhs-sdr12;
	sd-uhs-sdr25;
	sd-uhs-sdr50;
	max-frequency = <100000000>;
};

/* eMMC */
&sd_emmc_c {
	status = "okay";

	bus-width = <8>;
	cap-mmc-highspeed;
	max-frequency = <100000000>;
};
```

Umumnya, menurunkan frekuensi `&sd_emmc_c` dari `max-frequency = <200000000>;` menjadi `max-frequency = <100000000>;` dapat menyelesaikan masalah. Jika tidak, coba `50000000`. Sesuaikan `&sd_emmc_b` untuk pengaturan `USB/SD/TF`, dan gunakan `sd-uhs-sdr` untuk membatasi kecepatan. Ubah file dts dan [kompilasi](https://github.com/farishhz/amlogic-s9xxx-armbian/tree/main/compile-kernel) untuk mendapatkan file uji, atau gunakan metode dekompilasi di `Bagian 12.13` untuk mengubah file dtb yang sudah ada. Saat mengubah file dtb hasil dekompilasi, gunakan nilai heksadesimal: desimal `200000000` = heks `0xbebc200`, `100000000` = `0x5f5e100`, `50000000` = `0x2faf080`, `25000000` = `0x17d7840`. Sebagai alternatif, lihat metode konfigurasi cmdline di `Bagian 12.14` dan tambahkan parameter `mmc_core.max_freq=50000000` ke cmdline untuk membatasi frekuensi maksimum eMMC, sehingga mengatasi error baca/tulis dan masalah ketidakstabilan.

Selain solusi di lapisan perangkat lunak, masalah ini juga dapat diatasi melalui peningkatan perangkat keras atau [modifikasi fisik](https://www.right.com.cn/forum/thread-901586-1-1.html).

### 12.17 Cara Mengatasi Masalah Tidak Ada Suara pada Versi Bullseye

Informasi log error untuk masalah suara:

```shell
Mar 29 15:47:18 armbian-ct2000 kernel:  fe.dai-link-0: ASoC: dpcm_fe_dai_prepare() failed (-22)
Mar 29 15:47:18 armbian-ct2000 kernel:  fe.dai-link-0: ASoC: no backend DAIs enabled for fe.dai-link-0
```

Silakan lihat metode pada Bullseye NO Sound untuk pengaturannya.

```shell
curl -fsSOL https://github.com/ophub/kernel/releases/download/tools/bullseye_g12_sound-khadas-utils-4-2-any.tar.gz
tar -xzf bullseye_g12_sound-khadas-utils-4-2-any.tar.gz -C /

systemctl enable sound.service
systemctl restart sound.service
```

Restart Armbian untuk pengujian. Jika suara masih tidak berfungsi, perangkat Anda mungkin menggunakan konfigurasi keluaran audio yang lebih lama. Jadikan komentar konfigurasi baru pada `L137-L142` di /usr/bin/g12_sound.sh (terutama untuk G12B / S922X; G12A/S905X2 yang lebih lama dan sebagian besar SM1/S905X3 yang berbasis G12A tidak dapat menggunakannya), lalu hapus tanda komentar pada konfigurasi lama di `L130-L134`.

### 12.18 Cara Membuat File boot.scr

Pada sistem Armbian, file `boot.scr` di `/boot` adalah skrip boot yang telah dikompilasi. `boot.scr` dihasilkan dari file sumber `boot.cmd`. Ubah `boot.cmd` untuk melakukan perubahan, lalu kompilasi menjadi `boot.scr` menggunakan perintah mkimage.

Biasanya, file-file ini tidak perlu diubah. Jika penyesuaian diperlukan, ikuti langkah-langkah di bawah ini.

```shell
# Instal dependensi
sudo apt-get update
sudo apt-get install -y u-boot-tools

# Edit file boot.cmd
cd /boot
cp /boot/boot.cmd /boot/boot.cmd.bak
cp /boot/boot.scr /boot/boot.scr.bak
nano boot.cmd

# Kompilasi file boot.scr
mkimage -C none -A arm -T script -d boot.cmd boot.scr

# Restart untuk menguji
sync
reboot

# Penjelasan Tambahan
# Untuk perangkat Amlogic, file yang digunakan di USB adalah /boot/boot.scr, sedangkan file yang digunakan untuk penulisan ke eMMC adalah /boot/boot-emmc.scr.
```

### 12.19 Cara Mengaktifkan Remote Desktop dan Mengubah Port Default

Di pusat perangkat lunak `armbian-software`, memilih `201` akan menginstal lingkungan desktop. Selama instalasi, Anda akan diminta untuk mengaktifkan remote desktop — masukkan `y` untuk mengaktifkan. Port default remote desktop adalah `3389`. Untuk menggunakan port kustom:

```shell
sudo nano /etc/xrdp/xrdp.ini
# Ubah ke port kustom, misalnya 5000
port=5000
```

### 12.20 Panduan Optimasi Kontrol Kemacetan TCP

Konfigurasi network stack yang berbeda direkomendasikan berdasarkan performa perangkat untuk memastikan pengalaman pengguna terbaik. Silakan konfigurasikan perangkat Anda sesuai kemampuan perangkat kerasnya dengan mengedit `/etc/sysctl.conf` dan mengubah (atau menambahkan) baris berikut:

- Perangkat Gigabit (Performa Tinggi/Arsitektur Modern): Kombinasi `fq + bbr` direkomendasikan untuk memaksimalkan throughput dan meningkatkan ketahanan terhadap packet loss.
- Perangkat 100Mbps (Performa Rendah/Arsitektur Lama): Kombinasi `fq_codel + cubic` disarankan untuk meminimalkan beban CPU dan menjaga stabilitas latensi rendah.

```shell
# Opsi A: Direkomendasikan untuk Perangkat Gigabit/Performa Tinggi
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr

# Opsi B: Direkomendasikan untuk Perangkat 100Mbps/Performa Rendah
# net.core.default_qdisc = fq_codel
# net.ipv4.tcp_congestion_control = cubic
```

### 12.21 Cara Memperbaiki Masalah Deteksi EDID HDMI

**Kasus penggunaan**: Pada beberapa perangkat, port HDMI tidak dapat membaca EDID dari monitor (chip EDID monitor tidak pernah merespons di bus DDC — karakteristik perangkat keras di tingkat board), sehingga kernel tidak pernah memperoleh daftar kemampuan monitor. Gejalanya adalah tidak ada keluaran tampilan sama sekali, atau keluaran hanya pada resolusi cadangan 1024x768 (kasus yang umum adalah bdy-g98; lihat ophub/fnnas#606 untuk detailnya). Demikian pula, EDID dapat hilang atau rusak saat menggunakan KVM switch atau adaptor/perangkat capture HDMI; atau pada pengaturan headless (tanpa monitor), Anda mungkin ingin sistem selalu mengeluarkan tampilan pada resolusi tetap. Semua kasus ini dapat diatasi dengan memaksakan file firmware EDID melalui parameter kernel, sehingga melewati pembacaan dari monitor.

**Cara kerja**: Image sistem dilengkapi dengan hook initramfs bawaan yang secara otomatis membundel semua file firmware EDID di bawah `/lib/firmware/edid/` (sekitar 30 resolusi umum sudah terpasang) ke dalam initramfs setiap kali initramfs dibuat/dibangun ulang. Mekanisme ini tidak aktif secara default — kecuali parameter kernel ditambahkan, file yang dibundel sama sekali tidak berpengaruh.

**Cara mengaktifkan**: Edit `/boot/armbianEnv.txt` dan tambahkan di akhir baris `extraargs=` (contoh kernel 6.x):

```shell
extraargs=video=HDMI-A-1:e drm.edid_firmware=HDMI-A-1:edid/1920x1080.bin
```

Di sini `video=HDMI-A-1:e` memaksa antarmuka untuk aktif (opsional), dan `drm.edid_firmware=` menentukan file EDID yang digunakan (path relatif terhadap `/lib/firmware/`). Tiga kesalahan umum:

- File konfigurasi dapat berupa `/boot/armbianEnv.txt`, `/boot/uEnv.txt`, atau `/boot/extlinux/extlinux.conf`, dll. — ubah file mana pun yang benar-benar digunakan oleh perangkat Anda.
- **Prefiks parameter bergantung pada versi kernel**: kernel 6.x menggunakan `drm.edid_firmware`, sedangkan kernel yang lebih lama menggunakan `drm_kms_helper.edid_firmware`. Jika tidak yakin, periksa di perangkat: jika `/sys/module/drm/parameters/edid_firmware` ada, gunakan prefiks `drm.`; jika tidak, cari file dengan nama yang sama di bawah `/sys/module/drm_kms_helper/parameters/`. Prefiks yang salah akan diabaikan oleh kernel tanpa pemberitahuan — tidak ada error, tidak ada efek.
- Nama antarmuka belum tentu `HDMI-A-1`; periksa nama sebenarnya di perangkat Anda dengan `ls /sys/class/drm/ | grep HDMI`.

Setelah menyimpan, bangun ulang initramfs dan reboot:

```shell
# Jika Anda melihat "update-initramfs: Not updating initramfs.", jalankan ini terlebih dahulu:
sed -i 's/^update_initramfs=.*/update_initramfs=yes/' /etc/initramfs-tools/update-initramfs.conf

update-initramfs -u -k $(uname -r)
reboot
```

**Verifikasi**:

```shell
lsinitramfs /boot/initrd.img-$(uname -r) | grep edid   # file edid seharusnya terlihat di dalam initramfs
dmesg | grep -i edid                                   # pastikan firmware telah dimuat oleh kernel
cat /sys/class/drm/card0-HDMI-A-1/modes                # resolusi target muncul = berhasil
```

**Mengubah resolusi**: Pilih file lain yang sudah terpasang dari daftar yang ditampilkan oleh `ls /lib/firmware/edid/` (misalnya `1920x1080_50hz.bin`), arahkan parameter kernel ke nama file baru, lalu jalankan kembali perintah `update-initramfs` di atas dan reboot. Anda juga dapat menambahkan file EDID kustom (blok dasar 128 byte, atau file multi-blok dengan blok ekstensi) — prosedurnya sama.

**Catatan**:

- File EDID yang sudah terpasang tidak berisi blok ekstensi CTA, sehingga **audio HDMI tidak akan berfungsi**; jika Anda memerlukan audio, gunakan file EDID dengan blok ekstensi.
- Kernel harus dibangun dengan `CONFIG_DRM_LOAD_EDID_FIRMWARE=y` (sudah diaktifkan pada kernel yang dikompilasi dari repositori ini).
- Untuk memulihkan deteksi monitor otomatis: hapus kedua parameter dari `extraargs` dan reboot — tidak ada hal lain yang diperlukan.
