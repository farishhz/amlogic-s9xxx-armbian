# Pusat Perangkat Lunak Armbian

Berdasarkan masukan dan permintaan pengguna di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), [perangkat lunak](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) yang umum digunakan telah diintegrasikan secara bertahap untuk menyediakan operasi instal/perbarui/hapus instalasi dengan satu klik. Ini mencakup `image Docker`, `perangkat lunak desktop`, `layanan aplikasi`, dan lainnya.

## Pengenalan Perangkat Lunak

| ID | Nama Perangkat Lunak | Beranda | DockerHub:Port | Pengenalan perangkat lunak |
| --- | --- | --- | --- | --- |
| 101 | Docker | [Beranda](https://www.docker.com/) | [Docker](https://docs.docker.com/engine/install/) | Docker adalah platform terbuka untuk mengembangkan, mengirimkan, dan menjalankan aplikasi. |
| 102 | Portainer | [Beranda](https://www.portainer.io/) | [Docker](https://hub.docker.com/r/portainer/portainer-ce) :9443 | Platform manajemen container paling populer di dunia. |
| 103 | Yacht | [Beranda](https://yacht.sh/) | [Docker](https://hub.docker.com/r/selfhostedpro/yacht) :8001 | Antarmuka manajemen container yang berfokus pada template dan deployment satu klik. |
| 104 | Transmission | [Beranda](https://transmissionbt.com/) | [Docker](https://github.com/linuxserver/docker-transmission) :9091 | Transmission adalah klien BitTorrent lintas platform. |
| 105 | qBittorrent | [Beranda](https://www.qbittorrent.org/) | [Docker](https://hub.docker.com/r/linuxserver/qbittorrent) :8080 | qBittorrent adalah klien BitTorrent. |
| 106 | NextCloud | [Beranda](https://nextcloud.com/) | [Docker](https://hub.docker.com/r/arm64v8/nextcloud) :8088 | Nextcloud menawarkan platform akses dan sinkronisasi file universal yang dihosting sendiri (on-premise), dengan kemampuan kolaborasi yang andal serta antarmuka desktop, seluler, dan web. |
| 107 | Jellyfin | [Beranda](https://jellyfin.org/) | [Docker](https://hub.docker.com/r/linuxserver/jellyfin) :8096 | Jellyfin adalah Sistem Media Perangkat Lunak Bebas yang memberi Anda kendali penuh dalam mengelola dan melakukan streaming media Anda. |
| 108 | HomeAssistant | [Beranda](https://www.home-assistant.io/) | [Docker](https://hub.docker.com/r/linuxserver/homeassistant) :8123 | Home Assistant terintegrasi dengan lebih dari seribu perangkat dan layanan yang berbeda, serta memiliki fitur otomatisasi yang andal. |
| 109 | Kodbox | [Beranda](https://kodcloud.com/) | [Docker](https://hub.docker.com/r/kodcloud/kodbox) :8081 | Solusi manajemen dokumen online berbasis cloud pribadi. |
| 110 | CouchPotato | [Beranda](https://couchpota.to/) | [Docker](https://hub.docker.com/r/linuxserver/couchpotato) :5050 | Couchpotato adalah pengunduh NZB dan torrent otomatis yang secara otomatis menemukan film yang ingin Anda tonton. |
| 111 | Sonarr | [Beranda](https://sonarr.tv/) | [Docker](https://hub.docker.com/r/linuxserver/sonarr) :8989 | Sonarr adalah PVR (perekam video pribadi) untuk pengguna Usenet dan BitTorrent. |
| 112 | Radarr | [Beranda](https://radarr.video/) | [Docker](https://hub.docker.com/r/linuxserver/radarr) :7878 | Radarr adalah pengelola koleksi film untuk pengguna Usenet dan BitTorrent. |
| 113 | Syncthing | [Beranda](https://syncthing.net/) | [Docker](https://hub.docker.com/r/linuxserver/syncthing) :8384 | Syncthing adalah program sinkronisasi file berkelanjutan. |
| 114 | FileBrowser | [Beranda](https://filebrowser.org/) | [Docker](https://hub.docker.com/r/filebrowser/filebrowser) :8002 | File Browser menyediakan antarmuka pengelolaan file di dalam direktori tertentu dan dapat digunakan untuk mengunggah, menghapus, melihat pratinjau, mengganti nama, dan mengedit file Anda. |
| 115 | Heimdall | [Beranda](https://heimdall.site/) | [Docker](https://hub.docker.com/r/linuxserver/heimdall) :8003 | Heimdall adalah cara sederhana untuk mengatur semua tautan ke situs web dan aplikasi web yang paling sering Anda gunakan. |
| 116 | Node-RED | [Beranda](https://nodered.org/) | [Docker](https://nodered.org/docs/getting-started/docker) :1880 | Node-RED adalah alat pemrograman. Alat ini menyediakan editor berbasis browser yang memudahkan Anda menyambungkan alur (flow) menggunakan beragam node di palet, yang dapat di-deploy ke runtime-nya hanya dengan satu klik. |
| 117 | Mosquitto | [Beranda](https://www.mosquitto.org/) | [Docker](https://hub.docker.com/r/arm64v8/eclipse-mosquitto) :1883 | Protokol MQTT menyediakan metode ringan untuk melakukan pertukaran pesan menggunakan model publish/subscribe. Eclipse Mosquitto adalah implementasi server open source untuk protokol MQTT versi 5, 3.1.1, dan 3.1. |
| 118 | OpenWrt | [Beranda](https://www.openwrt.org/) | [Docker](https://hub.docker.com/r/ophub/openwrt-armv8) :80 | Proyek OpenWrt adalah sistem operasi Linux yang ditujukan untuk perangkat embedded, memiliki lebih dari 3000+ paket aplikasi terstandarisasi dan dukungan plugin pihak ketiga yang sangat kaya. |
| 119 | Netdata | [Beranda](https://learn.netdata.cloud/) | [Docker](https://hub.docker.com/r/netdata/netdata) :19999 | Netdata adalah pemantauan kinerja dan kesehatan sistem serta aplikasi yang terdistribusi dan real-time. |
| 120 | XunLei | [Beranda](https://github.com/cnk3x/xunlei) | [Docker](https://hub.docker.com/r/cnk3x/xunlei) :2345 | Program layanan unduhan jarak jauh Thunder (XunLei) yang diekstrak dari paket Thunder untuk Synology. |
| 121 | Docker-Headless | [Beranda](https://github.com/infrastlabs/docker-headless) | [Docker](https://hub.docker.com/r/infrastlabs/docker-headless) :10081 | Remote Desktop dengan dukungan Audio/Locale/IBus. Mendukung banyak desktop (Gnome, Plasma, Mate, Xfce, Cinnamon) |
| 122 | Navidrome | [Beranda](https://www.navidrome.org/) | [Docker](https://hub.docker.com/r/deluan/navidrome) :4533 | Navidrome adalah server dan streamer musik open source yang dihosting sendiri. Navidrome memberi Anda kebebasan untuk mendengarkan koleksi musik Anda dari browser atau perangkat seluler mana pun. |
| 123 | Openlist | [Beranda](https://www.oplist.org/) | [Docker](https://hub.docker.com/r/openlistteam/openlist) :5244 | Program daftar file yang mendukung berbagai penyimpanan, dibangun dengan Gin dan Solidjs. |
| 124 | QingLong | [Beranda](https://github.com/whyour/qinglong) | [Docker](https://hub.docker.com/r/whyour/qinglong) :5700 | Panel manajemen tugas terjadwal yang mendukung typescript, javaScript, python3, dan shell. |
| 125 | ChatGPT-Next-Web | [Beranda](https://github.com/Yidadaa/ChatGPT-Next-Web) | [Docker](https://hub.docker.com/r/yidadaa/chatgpt-next-web) :3000 | Antarmuka ChatGPT lintas platform yang dirancang dengan baik (Web / PWA / Linux / Win / MacOS). |
| 126 | N8N | [Beranda](https://n8n.io/) | [Docker](https://hub.docker.com/r/n8nio/n8n) :5678 | n8n adalah platform otomatisasi workflow yang memberi tim teknis fleksibilitas kode dengan kecepatan no-code. Dengan lebih dari 400 integrasi, kemampuan AI bawaan, dan lisensi fair-code, n8n memungkinkan Anda membangun otomatisasi yang andal sambil tetap memegang kendali penuh atas data dan deployment Anda. |
| 201 | Desktop:GNOME | [Beranda](https://www.gnome.org/) | - | GNOME menyediakan lingkungan kerja desktop yang terfokus untuk membantu Anda menyelesaikan pekerjaan. `Desktop` dapat digunakan dengan menghubungkannya ke monitor, atau digunakan melalui perangkat lunak [remote desktop](https://learn.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients). |
| 202 | Firefox | [Beranda](https://www.mozilla.org/) | - | Browser web yang sangat baik. |
| 203 | VLC | [Beranda](https://www.videolan.org/) | - | VLC adalah pemutar multimedia dan framework yang gratis, open source, dan lintas platform, yang dapat memutar sebagian besar file multimedia. |
| 204 | MPV | [Beranda](https://mpv.io/) | - | Pemutar media yang gratis, open source, dan lintas platform. |
| 205 | GIMP | [Beranda](https://www.gimp.org/) | - | GIMP adalah editor gambar lintas platform. |
| 206 | Krita | [Beranda](https://krita.org/) | - | Krita adalah program melukis profesional yang GRATIS dan open source. |
| 207 | LibreOffice | [Beranda](https://www.libreoffice.org/) | - | LibreOffice adalah paket aplikasi perkantoran yang gratis dan andal. Antarmukanya yang bersih dan fitur-fiturnya yang kaya membantu Anda menyalurkan kreativitas dan meningkatkan produktivitas. |
| 208 | Shotcut | [Beranda](https://shotcut.org/) | - | Shotcut adalah editor video yang gratis, open source, dan lintas platform. |
| 209 | Kdenlive | [Beranda](https://kdenlive.org/) | - | Kdenlive adalah Editor Video yang Gratis dan Open Source. |
| 210 | Thunderbird | [Beranda](https://www.thunderbird.net/) | - | Thunderbird membuat pengalaman email Anda lebih baik dengan memadukan kecepatan, privasi, dan teknologi terbaru. |
| 211 | Evolution | [Beranda](https://github.com/GNOME/evolution) | - | Evolution adalah aplikasi manajemen informasi pribadi yang menyediakan fungsi email, kalender, dan buku alamat yang terintegrasi. |
| 212 | Gwenview | [Beranda](https://apps.kde.org/gwenview/) | - | Gwenview adalah penampil gambar dari KDE yang cepat dan mudah digunakan, ideal untuk menjelajah dan menampilkan koleksi gambar. |
| 213 | Eog | [Beranda](https://gitlab.gnome.org/GNOME/eog) | - | Eye of GNOME (eog) adalah program penampil gambar. Program ini dirancang sebagai penampil gambar yang cepat dan fungsional. |
| 214 | VisualStudioCode | [Beranda](https://code.visualstudio.com/) | - | Visual Studio Code adalah editor kode sumber yang ringan namun andal. |
| 215 | Gedit | [Beranda](https://github.com/GNOME/gedit) | - | Gedit adalah editor teks berfitur lengkap untuk lingkungan desktop GNOME. Anda dapat menggunakannya untuk menyiapkan catatan dan dokumen sederhana, atau memanfaatkan beberapa fitur lanjutannya sehingga menjadikannya lingkungan pengembangan perangkat lunak Anda sendiri. |
| 216 | Flameshot | [Beranda](https://flameshot.org/) | - | Perangkat lunak tangkapan layar open source yang andal namun mudah digunakan. |
| 301 | Frps | [Beranda](https://gofrp.org/) | - | Reverse proxy cepat yang membantu Anda mengekspos server lokal di balik NAT atau firewall ke internet. |
| 302 | Frpc | [Beranda](https://gofrp.org/) | - | Frp adalah aplikasi reverse proxy berkinerja tinggi yang berfokus pada penetrasi intranet, mendukung TCP, UDP, HTTP, HTTPS, dan protokol lainnya. |
| 303 | NPS | [Beranda](https://ehang-io.github.io/nps) | - | NPS adalah server proxy penetrasi intranet yang ringan, berkinerja tinggi, dan andal, dengan terminal manajemen web yang lengkap. |
| 304 | NPC | [Beranda](https://ehang-io.github.io/nps) | - | NPC adalah klien dari NPS. |
| 305 | Plex | [Beranda](https://www.plex.tv/) | - | Mulai dari media pribadi di server Anda sendiri, film dan acara gratis maupun on-demand, TV langsung, podcast, dan acara web, hingga streaming musik, Anda dapat menikmati semuanya dalam satu aplikasi di perangkat apa pun. |
| 306 | Emby-Server | [Beranda](https://emby.media/) | - | Sinkronkan media pribadi Anda ke cloud untuk memudahkan pencadangan, pengarsipan, dan konversi. Simpan konten Anda dalam berbagai resolusi agar dapat di-streaming langsung dari perangkat apa pun. |
| 307 | KVM | [Beranda](https://virt-manager.org/) | - | KVM (Kernel-Based Virtual Machine) adalah solusi virtualisasi lengkap untuk Linux dengan ekstensi virtualisasi. Aplikasi virt-manager adalah antarmuka pengguna desktop untuk mengelola mesin virtual melalui libvirt. Aplikasi ini terutama ditujukan untuk VM KVM, tetapi juga dapat mengelola Xen dan LXC (linux containers). Mesin virtual KVM dapat menginstal [OpenWrt](https://github.com/unifreq/openwrt_packit), Debian, Ubuntu, OpenSUSE, ArchLinux, Centos, Gentoo, KyLin, UOS, dan lain-lain. |
| 308 | PVE | [Beranda](https://github.com/pimox/pimox7) | https://IP:8006 | Proxmox Virtual Environment adalah solusi manajemen virtualisasi server open source berbasis QEMU/KVM dan LXC. Anda dapat mengelola mesin virtual, container, klaster ketersediaan tinggi, penyimpanan, dan jaringan melalui antarmuka web terintegrasi yang mudah digunakan atau melalui CLI. |
| 309 | CasaOS | [Beranda](https://github.com/IceWhaleTech/CasaOS) | http://IP | CasaOS adalah sistem Cloud Pribadi open source yang sederhana, mudah digunakan, dan elegan. |
| 310 | ArozOS | [Beranda](https://github.com/tobychui/arozos) | http://IP:8080 | ArozOS adalah sistem operasi desktop berbasis web yang cocok untuk platform berdaya rendah. Sistem ini dilengkapi manajemen file/disk, statistik jaringan, server web, dan lainnya. |

## Panduan Penggunaan Pusat Perangkat Lunak

Masuk ke sistem Armbian dan jalankan perintah:

```shell
armbian-software
```

Daftar perangkat lunak terintegrasi beserta opsi pengelolaan pintasan akan muncul, misalnya:

```shell
root@armbian:~# armbian-software
[ STEPS ] Start selecting software [ Current system: debian/bullseye ]...
----------------------------------------------------------
ID    NAME                STATE           MANAGE
----------------------------------------------------------
102   Portainer           installed       update/remove
202   Firefox             installed       update/remove
302   Frpc                not-installed   install
...
----------------------------------------------------------
[ OPTIONS ] Please Input Software ID:
```

- `Perangkat lunak yang belum terinstal`: Status menampilkan `not-installed`. Masukkan `ID` perangkat lunak untuk menginstalnya.
- `Perangkat lunak yang sudah terinstal`: Status menampilkan `installed`. Masukkan `ID` perangkat lunak dan ikuti petunjuk untuk melakukan `update` (perbarui) atau `remove` (hapus).

> Catatan untuk `101` Docker: `update` hanya memperbarui paket-paket Docker tanpa menyentuh bagian sistem lainnya, sedangkan `remove` menghapus instalasi Docker tetapi **tetap menyimpan** data di `/var/lib/docker` (image, container, volume). Untuk menghapus data tersebut juga, jalankan `armbian-docker remove --purge-data` dan ketik `YES` untuk mengonfirmasi. Jalankan `armbian-docker -h` untuk detailnya.

## Panduan Pengembangan Pusat Perangkat Lunak

Skrip dan perintah pusat perangkat lunak disimpan di direktori [/usr/share/ophub/armbian-software](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software). Gunakan `armbian-software -u` untuk menyinkronkan dan mengunduh direktori ini ke sistem lokal sekaligus memperbarui daftar pusat perangkat lunak. File yang diawali angka adalah `skrip instalasi satu klik` untuk perangkat lunak yang bersangkutan. [software-command.sh](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-command.sh) adalah `file perintah terpadu` untuk menginstal/memperbarui/menghapus perangkat lunak. [software-list.conf](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) adalah file konfigurasi daftar perangkat lunak, dengan penjelasan sebagai berikut:

```yaml
# 1.ID     2.Nama Perangkat Lunak     3.MetodeVerifikasi@Paket      4.Pilihan Eksekusi     5.Rilis yang Didukung
102        :Portainer          :docker@portainer         :command-docker.sh      :all
202        :Firefox            :dpkg@firefox             :command-desktop.sh     :all
302        :Frpc               :which@frpc               :302-frpc.sh            :all
308        :PVE                :dpkg@pve-manager         :command-service.sh     :bullseye@bookworm
...
```

- `ID`: `Nomor seri unik` perangkat lunak.
- `Nama Perangkat Lunak`: `Nama perangkat lunak` (harus kurang dari 40 karakter).
- `MetodeVerifikasi@Paket`: `Metode verifikasi` untuk memeriksa status instalasi dan `paket perangkat lunak` yang bersangkutan, dipisahkan dengan `@`.
  - Untuk image container Docker, gunakan metode `docker`. Contoh: `docker@portainer` memeriksa apakah image `portainer` sudah terinstal.
  - Untuk paket yang diinstal melalui `apt`, gunakan metode `dpkg`. Contoh: `dpkg@firefox` memeriksa apakah paket `firefox` sudah terinstal.
  - Jika terdapat file executable di direktori perintah sistem (bin, sbin), gunakan `which` untuk memeriksa file binary-nya. Contoh: `which@frpc` memverifikasi instalasi layanan `frpc`.
  - Jika tidak terdapat file executable di direktori perintah sistem, gunakan `find` untuk memeriksa path tertentu. Contoh: `find@/root/arozos` memeriksa apakah sistem `ArozOS` sudah terinstal.
- `Pilihan Eksekusi`: Menentukan apakah perangkat lunak dikelola menggunakan `file perintah terpadu` atau `skrip independen`.
  - Untuk operasi yang `sederhana`, perintah dikelompokkan berdasarkan kategori perangkat lunak dalam file `command-docker.sh / command-desktop.sh / command-service.sh`, dengan nama sesuai nomor seri perangkat lunak. Misalnya, `portainer` (ID `102`) memiliki operasinya di `software_102()`.
  - Untuk operasi yang `kompleks` dengan instruksi panjang, digunakan file skrip independen. Misalnya, skrip instalasi `frpc` diberi nama `302-frpc.sh`, diawali dengan nomor serinya.
- `Rilis yang Didukung`: Menentukan `nama kode versi sistem` Armbian yang didukung. Gunakan `all` untuk menandakan dukungan bagi semua versi. Untuk dukungan sebagian, cantumkan nama kode versi yang dipisahkan dengan `@`.

Kontribusi perangkat lunak tambahan sangat diterima. Silakan ajukan permintaan di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues).

# Pusat Perangkat Lunak Armbian

Berdasarkan kebutuhan yang disampaikan pengguna di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), [perangkat lunak](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) yang umum digunakan telah diintegrasikan secara bertahap untuk menyediakan operasi cepat seperti instal/perbarui/hapus instalasi dengan satu klik. Ini mencakup `image Docker`, `perangkat lunak desktop`, `layanan aplikasi`, dan lainnya.

## Pengenalan Perangkat Lunak

| ID | Nama Perangkat Lunak | Beranda | DockerHub:Port | Pengenalan perangkat lunak |
| --- | --- | --- | --- | --- |
| 101 | Docker | [Beranda](https://www.docker.com/) | [Docker](https://docs.docker.com/engine/install/) | Docker adalah platform terbuka untuk mengembangkan, merilis, dan menjalankan aplikasi. |
| 102 | Portainer | [Beranda](https://www.portainer.io/) | [Docker](https://hub.docker.com/r/portainer/portainer-ce) :9443 | Platform manajemen container paling populer di dunia. |
| 103 | Yacht | [Beranda](https://yacht.sh/) | [Docker](https://hub.docker.com/r/selfhostedpro/yacht) :8001 | Antarmuka manajemen container yang berfokus pada template dan deployment satu klik. |
| 104 | Transmission | [Beranda](https://transmissionbt.com/) | [Docker](https://github.com/linuxserver/docker-transmission) :9091 | Transmission adalah klien BitTorrent lintas platform. |
| 105 | qBittorrent | [Beranda](https://www.qbittorrent.org/) | [Docker](https://hub.docker.com/r/linuxserver/qbittorrent) :8080 | qBittorrent adalah klien BitTorrent. |
| 106 | NextCloud | [Beranda](https://nextcloud.com/) | [Docker](https://hub.docker.com/r/arm64v8/nextcloud) :8088 | Nextcloud menyediakan platform akses dan sinkronisasi file universal lokal, dengan fitur kolaborasi yang andal serta antarmuka desktop, seluler, dan web. |
| 107 | Jellyfin | [Beranda](https://jellyfin.org/) | [Docker](https://hub.docker.com/r/linuxserver/jellyfin) :8096 | Jellyfin adalah sistem media perangkat lunak bebas yang memungkinkan Anda mengendalikan pengelolaan dan streaming media Anda. |
| 108 | HomeAssistant | [Beranda](https://www.home-assistant.io/) | [Docker](https://hub.docker.com/r/linuxserver/homeassistant) :8123 | Home Assistant mengintegrasikan lebih dari seribu perangkat dan layanan yang berbeda, serta memiliki fitur otomatisasi yang andal. |
| 109 | Kodbox | [Beranda](https://kodcloud.com/) | [Docker](https://hub.docker.com/r/kodcloud/kodbox) :8081 | Solusi manajemen dokumen online berbasis cloud pribadi. |
| 110 | CouchPotato | [Beranda](https://couchpota.to/) | [Docker](https://hub.docker.com/r/linuxserver/couchpotato) :5050 | Couchpotato adalah pengunduh NZB dan torrent otomatis yang secara otomatis mencari film yang ingin ditonton. |
| 111 | Sonarr | [Beranda](https://sonarr.tv/) | [Docker](https://hub.docker.com/r/linuxserver/sonarr) :8989 | Sonarr adalah perekam video pribadi untuk pengguna Usenet dan BitTorrent. |
| 112 | Radarr | [Beranda](https://radarr.video/) | [Docker](https://hub.docker.com/r/linuxserver/radarr) :7878 | Radarr adalah pengelola koleksi film untuk pengguna Usenet dan BitTorrent. |
| 113 | Syncthing | [Beranda](https://syncthing.net/) | [Docker](https://hub.docker.com/r/linuxserver/syncthing) :8384 | Syncthing adalah program sinkronisasi file berkelanjutan. |
| 114 | FileBrowser | [Beranda](https://filebrowser.org/) | [Docker](https://hub.docker.com/r/filebrowser/filebrowser) :8002 | File Browser menyediakan antarmuka pengelolaan file di direktori tertentu, yang dapat digunakan untuk mengunggah, menghapus, melihat pratinjau, mengganti nama, dan mengedit file. |
| 115 | Heimdall | [Beranda](https://heimdall.site/) | [Docker](https://hub.docker.com/r/linuxserver/heimdall) :8003 | Heimdall adalah cara sederhana untuk mengatur semua tautan ke situs web dan aplikasi web yang paling sering Anda gunakan. |
| 116 | Node-RED | [Beranda](https://nodered.org/) | [Docker](https://nodered.org/docs/getting-started/docker) :1880 | Node-RED adalah alat pemrograman. Alat ini menyediakan editor berbasis browser yang memudahkan Anda menghubungkan alur menggunakan berbagai node di palet, dan dapat di-deploy untuk dijalankan hanya dengan satu klik. |
| 117 | Mosquitto | [Beranda](https://www.mosquitto.org/) | [Docker](https://hub.docker.com/r/arm64v8/eclipse-mosquitto) :1883 | Protokol MQTT menyediakan metode ringan untuk pertukaran pesan menggunakan model publish/subscribe. Eclipse Mosquitto adalah implementasi open source dari server untuk protokol MQTT versi 5, 3.1.1, dan 3.1. |
| 118 | OpenWrt | [Beranda](https://www.openwrt.org/) | [Docker](https://hub.docker.com/r/ophub/openwrt-armv8) :80 | Proyek OpenWrt adalah sistem operasi Linux untuk perangkat embedded, dengan lebih dari 3000+ paket aplikasi terstandarisasi dan dukungan plugin pihak ketiga yang sangat kaya. |
| 119 | Netdata | [Beranda](https://learn.netdata.cloud/) | [Docker](https://hub.docker.com/r/netdata/netdata) :19999 | Netdata adalah pemantauan kinerja dan kondisi operasional sistem serta aplikasi yang terdistribusi dan real-time. |
| 120 | XunLei | [Beranda](https://github.com/cnk3x/xunlei) | [Docker](https://hub.docker.com/r/cnk3x/xunlei) :2345 | Program layanan unduhan jarak jauh XunLei (Thunder) yang diekstrak dari paket XunLei untuk Synology. |
| 121 | Docker-Headless | [Beranda](https://github.com/infrastlabs/docker-headless) | [Docker](https://hub.docker.com/r/infrastlabs/docker-headless) :10081 | Remote desktop dengan dukungan audio/pengaturan wilayah/IBus. Mendukung banyak desktop (Gnome, Plasma, Mate, Xfce, Cinnamon) |
| 122 | Navidrome | [Beranda](https://www.navidrome.org/) | [Docker](https://hub.docker.com/r/deluan/navidrome) :4533 | Navidrome adalah server musik dan layanan streaming open source yang dihosting sendiri. Navidrome memungkinkan Anda mendengarkan koleksi musik dengan bebas dari browser atau perangkat seluler mana pun. |
| 123 | Openlist | [Beranda](https://www.oplist.org/) | [Docker](https://hub.docker.com/r/openlistteam/openlist) :5244 | Program daftar file yang mendukung berbagai jenis penyimpanan, menggunakan Gin dan Solidjs. |
| 124 | QingLong | [Beranda](https://github.com/whyour/qinglong) | [Docker](https://hub.docker.com/r/whyour/qinglong) :5700 | Panel manajemen tugas terjadwal yang mendukung python3, javaScript, shell, dan typescript. |
| 125 | ChatGPT-Next-Web | [Beranda](https://github.com/Yidadaa/ChatGPT-Next-Web) | [Docker](https://hub.docker.com/r/yidadaa/chatgpt-next-web) :3000 | Deploy aplikasi ChatGPT pribadi lintas platform milik Anda secara gratis dengan satu klik. |
| 126 | N8N | [Beranda](https://n8n.io/) | [Docker](https://hub.docker.com/r/n8nio/n8n) :5678 | n8n adalah platform otomatisasi workflow yang memberikan kecepatan pengembangan no-code yang efisien bagi tim teknis. Platform ini memiliki lebih dari 400 integrasi bawaan, kemampuan AI native, dan menggunakan lisensi fair-code, sehingga Anda dapat membangun alur otomatisasi yang andal sambil tetap memegang kendali penuh atas data dan deployment Anda. |
| 201 | Desktop:GNOME | [Beranda](https://www.gnome.org/) | - | GNOME menyediakan lingkungan kerja desktop yang terfokus untuk membantu Anda menyelesaikan pekerjaan. `Desktop` dapat digunakan dengan menghubungkan monitor, atau dihubungkan menggunakan perangkat lunak [remote desktop](https://learn.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients). |
| 202 | Firefox | [Beranda](https://www.mozilla.org/) | - | Browser web yang sangat baik. |
| 203 | VLC | [Beranda](https://www.videolan.org/) | - | VLC adalah pemutar multimedia dan framework yang bebas, open source, dan lintas platform, yang dapat memutar sebagian besar file multimedia. |
| 204 | MPV | [Beranda](https://mpv.io/) | - | Pemutar media yang gratis, open source, dan lintas platform. |
| 205 | GIMP | [Beranda](https://www.gimp.org/) | - | GIMP adalah editor gambar lintas platform. |
| 206 | Krita | [Beranda](https://krita.org/) | - | Krita adalah program melukis profesional yang gratis dan open source. |
| 207 | LibreOffice | [Beranda](https://www.libreoffice.org/) | - | LibreOffice adalah paket aplikasi perkantoran yang gratis dan andal. Antarmukanya yang bersih dan alat-alatnya yang kaya fitur membantu Anda menyalurkan kreativitas dan meningkatkan produktivitas. |
| 208 | Shotcut | [Beranda](https://shotcut.org/) | - | Shotcut adalah editor video yang gratis, open source, dan lintas platform. |
| 209 | Kdenlive | [Beranda](https://kdenlive.org/) | - | Kdenlive adalah editor video yang gratis dan open source. |
| 210 | Thunderbird | [Beranda](https://www.thunderbird.net/) | - | Thunderbird memadukan kecepatan, privasi, dan teknologi terbaru agar Anda dapat memanfaatkan email dengan lebih baik. |
| 211 | Evolution | [Beranda](https://github.com/GNOME/evolution) | - | Evolution adalah aplikasi manajemen informasi pribadi yang menyediakan fungsi email, kalender, dan buku alamat yang terintegrasi. |
| 212 | Gwenview | [Beranda](https://apps.kde.org/gwenview/) | - | Gwenview adalah penampil gambar dari KDE yang ringan dan mudah digunakan, alat yang ideal untuk menjelajah dan menampilkan banyak gambar. |
| 213 | Eog | [Beranda](https://gitlab.gnome.org/GNOME/eog) | - | Eye of GNOME (eog) adalah program penampil gambar. Program ini dirancang sebagai penampil gambar yang cepat dan kaya fungsi. |
| 214 | VisualStudioCode | [Beranda](https://code.visualstudio.com/) | - | Visual Studio Code adalah editor kode sumber yang ringan namun andal. |
| 215 | Gedit | [Beranda](https://github.com/GNOME/gedit) | - | Gedit adalah editor teks berfitur lengkap untuk lingkungan desktop GNOME. Anda dapat menggunakannya untuk menyiapkan catatan dan dokumen sederhana, atau memanfaatkan beberapa fitur lanjutannya sehingga menjadikannya lingkungan pengembangan perangkat lunak Anda sendiri. |
| 216 | Flameshot | [Beranda](https://flameshot.org/) | - | Perangkat lunak tangkapan layar open source yang andal namun mudah digunakan. |
| 301 | Frps | [Beranda](https://gofrp.org/) | - | Frp adalah reverse proxy cepat yang membantu Anda mengekspos server lokal di balik NAT atau firewall ke internet. |
| 302 | Frpc | [Beranda](https://gofrp.org/) | - | Frp adalah aplikasi reverse proxy berkinerja tinggi yang berfokus pada penetrasi intranet, mendukung berbagai protokol seperti TCP, UDP, HTTP, HTTPS, dan lainnya. |
| 303 | NPS | [Beranda](https://ehang-io.github.io/nps) | - | Server NPS. Server proxy penetrasi intranet yang ringan, berkinerja tinggi, dan andal, dengan terminal manajemen web yang lengkap. |
| 304 | NPC | [Beranda](https://ehang-io.github.io/nps) | - | NPC adalah klien dari NPS. |
| 305 | Plex | [Beranda](https://www.plex.tv/) | - | Mulai dari media pribadi di server Anda sendiri, film dan acara gratis maupun on-demand, TV langsung, podcast, dan acara web, hingga streaming musik, Anda dapat menikmati semuanya dalam satu aplikasi di perangkat apa pun. |
| 306 | Emby-Server | [Beranda](https://emby.media/) | - | Sinkronkan media pribadi Anda ke cloud untuk memudahkan pencadangan, pengarsipan, dan konversi. Simpan konten Anda dalam berbagai resolusi agar dapat di-streaming langsung dari perangkat apa pun. |
| 307 | KVM | [Beranda](https://virt-manager.org/) | - | KVM (Kernel-Based Virtual Machine) adalah solusi virtualisasi lengkap untuk Linux yang dilengkapi ekstensi virtualisasi. Aplikasi virt-manager adalah antarmuka pengguna desktop untuk mengelola mesin virtual melalui libvirt. Aplikasi ini terutama ditujukan untuk VM KVM, tetapi juga dapat mengelola Xen dan LXC (Linux container). Mesin virtual KVM dapat menginstal [OpenWrt](https://github.com/unifreq/openwrt_packit), Debian, Ubuntu, OpenSUSE, ArchLinux, Centos, Gentoo, KyLin, UOS, dan lain-lain. |
| 308 | PVE | [Beranda](https://github.com/pimox/pimox7) | https://IP:8006 | Proxmox Virtual Environment adalah solusi manajemen virtualisasi server open source berbasis QEMU/KVM dan LXC. Anda dapat mengelola mesin virtual, container, klaster ketersediaan tinggi, penyimpanan, dan jaringan melalui antarmuka web terintegrasi yang mudah digunakan atau melalui CLI. |
| 309 | CasaOS | [Beranda](https://github.com/IceWhaleTech/CasaOS) | http://IP | CasaOS adalah sistem cloud pribadi open source yang sederhana, mudah digunakan, dan elegan. |
| 310 | ArozOS | [Beranda](https://github.com/tobychui/arozos) | http://IP:8080 | ArozOS adalah sistem operasi desktop berbasis web yang cocok untuk platform berdaya rendah. Sistem ini memiliki fitur manajemen file/disk, statistik jaringan, server web, dan lainnya. |

## Petunjuk Penggunaan Pusat Perangkat Lunak

Setelah masuk ke sistem Armbian, masukkan perintah berikut:

```shell
armbian-software
```

Daftar manajemen cepat perangkat lunak yang saat ini sudah terintegrasi akan ditampilkan, misalnya:

```shell
root@armbian:~# armbian-software
[ STEPS ] Start selecting software [ Current system: debian/bullseye ]...
----------------------------------------------------------
ID    NAME                STATE           MANAGE
----------------------------------------------------------
102   Portainer           installed       update/remove
202   Firefox             installed       update/remove
302   Frpc                not-installed   install
...
----------------------------------------------------------
[ OPTIONS ] Please Input Software ID:
```

- `Perangkat lunak yang belum terinstal`: status ditampilkan sebagai `not-installed`, masukkan `ID` perangkat lunak yang bersangkutan untuk menginstalnya.
- `Perangkat lunak yang sudah terinstal`: status ditampilkan sebagai `installed`, masukkan `ID` perangkat lunak yang bersangkutan, lalu pilih perbarui atau hapus sesuai petunjuk.

> Catatan tentang `101` Docker: `update` hanya memperbarui paket-paket terkait Docker dan tidak mengubah bagian lain dari sistem; `remove` akan menghapus instalasi Docker, tetapi **mempertahankan** data di `/var/lib/docker` (image, container, volume). Jika Anda juga ingin menghapus data tersebut, jalankan `armbian-docker remove --purge-data` dan masukkan `YES` untuk konfirmasi. Untuk informasi lebih lanjut, jalankan `armbian-docker -h`.

## Panduan Pengembangan Pusat Perangkat Lunak

Skrip dan perintah pusat perangkat lunak disimpan secara terpusat di direktori [/usr/share/ophub/armbian-software](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software). Gunakan perintah `armbian-software -u` untuk menyinkronkan dan mengunduh direktori ini ke lokal, sehingga daftar pusat perangkat lunak lokal diperbarui. File yang diawali angka adalah `skrip instalasi sekali klik` untuk perangkat lunak yang bersangkutan. [software-command.sh](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-command.sh) adalah `file perintah terpadu` untuk operasi instal/perbarui/hapus. [software-list.conf](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) adalah file konfigurasi daftar perangkat lunak, dengan penjelasan sebagai berikut:

```yaml
# 1.ID     2.Nama Perangkat Lunak     3.MetodeAutentikasi@Paket      4.Pilihan Eksekusi     5.Rilis yang Didukung
102        :Portainer          :docker@portainer         :command-docker.sh      :all
202        :Firefox            :dpkg@firefox             :command-desktop.sh     :all
302        :Frpc               :which@frpc               :302-frpc.sh            :all
308        :PVE                :dpkg@pve-manager         :command-service.sh     :bullseye@bookworm
...
```

- `ID`: `nomor urut unik` perangkat lunak.
- `Software Name`: `nama perangkat lunak` (panjang nama harus kurang dari 40 karakter).
- `AuthMethod@Package`: `metode pemeriksaan` status instalasi perangkat lunak dan `paket perangkat lunak` yang bersangkutan, dipisahkan dengan simbol `@`.
  - Image yang diinstal melalui container `docker` diperiksa dengan metode `docker`. Contoh: untuk memeriksa apakah image `portainer` sudah terinstal, gunakan `docker@portainer`.
  - Paket yang diinstal melalui `apt` diperiksa dengan metode `dpkg`. Contoh: untuk memeriksa apakah `firefox` sudah terinstal, gunakan `dpkg@firefox`.
  - Jika terdapat file eksekusi di direktori perintah sistem (bin, sbin), gunakan metode `which`. Contoh: untuk memeriksa apakah layanan `frpc` sudah terinstal, gunakan `which@frpc`.
  - Jika tidak ada file eksekusi di direktori perintah sistem, gunakan metode `find` untuk memeriksa apakah path tertentu ada. Contoh: untuk memeriksa apakah sistem `arozos` sudah terinstal, gunakan `find@/root/arozos`.
- `Execute Selection`: menentukan apakah perangkat lunak dikelola menggunakan `file perintah terpadu` atau `skrip mandiri`.
  - Untuk perangkat lunak dengan perintah operasi yang `relatif ringkas`, perintah ditulis secara terpusat per kategori di file `command-docker.sh / command-desktop.sh / command-service.sh`, dan dinamai berdasarkan nomor urut perangkat lunak. Misalnya, operasi `portainer` (nomor urut `102`) ditulis di `software_102()`.
  - Untuk perangkat lunak dengan operasi yang `relatif kompleks dan perintah yang panjang`, digunakan file skrip mandiri. Misalnya, skrip instalasi `frpc` diawali dengan nomor urut dan dinamai `302-frpc.sh`.
- `Supported Release`: menentukan `kode nama versi sistem` Armbian yang didukung. Gunakan `all` jika semua versi didukung. Jika hanya sebagian versi yang didukung, isi kode nama versinya, dan hubungkan beberapa kode nama dengan simbol `@`.

Silakan tambahkan lebih banyak perangkat lunak. Anda dipersilakan mengajukan permintaan dukungan di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues).

# Pusat Perangkat Lunak Armbian

Berdasarkan masukan dan permintaan pengguna di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues), [perangkat lunak](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) yang sering digunakan diintegrasikan secara bertahap untuk mewujudkan operasi instal/perbarui/hapus instalasi dengan sekali klik. Termasuk `image Docker`, `perangkat lunak desktop`, `layanan aplikasi`, dan lainnya.

## Pengenalan Perangkat Lunak

| ID | Nama Perangkat Lunak | Beranda | DockerHub:Port | Pengenalan Perangkat Lunak |
| --- | --- | --- | --- | --- |
| 101 | Docker | [Beranda](https://www.docker.com/) | [Docker](https://docs.docker.com/engine/install/) | Docker adalah platform terbuka untuk mengembangkan, mendistribusikan, dan menjalankan aplikasi. |
| 102 | Portainer | [Beranda](https://www.portainer.io/) | [Docker](https://hub.docker.com/r/portainer/portainer-ce) :9443 | Platform manajemen container paling populer di dunia. |
| 103 | Yacht | [Beranda](https://yacht.sh/) | [Docker](https://hub.docker.com/r/selfhostedpro/yacht) :8001 | Antarmuka manajemen container yang berfokus pada template dan deployment sekali klik. |
| 104 | Transmission | [Beranda](https://transmissionbt.com/) | [Docker](https://github.com/linuxserver/docker-transmission) :9091 | Transmission adalah klien BitTorrent lintas platform. |
| 105 | qBittorrent | [Beranda](https://www.qbittorrent.org/) | [Docker](https://hub.docker.com/r/linuxserver/qbittorrent) :8080 | qBittorrent adalah klien BitTorrent. |
| 106 | NextCloud | [Beranda](https://nextcloud.com/) | [Docker](https://hub.docker.com/r/arm64v8/nextcloud) :8088 | Nextcloud menyediakan platform akses dan sinkronisasi file universal yang di-hosting sendiri (on-premise), dengan fitur kolaborasi yang andal serta antarmuka desktop, seluler, dan web. |
| 107 | Jellyfin | [Beranda](https://jellyfin.org/) | [Docker](https://hub.docker.com/r/linuxserver/jellyfin) :8096 | Jellyfin adalah sistem media perangkat lunak bebas yang memungkinkan Anda mengendalikan pengelolaan dan streaming media. |
| 108 | HomeAssistant | [Beranda](https://www.home-assistant.io/) | [Docker](https://hub.docker.com/r/linuxserver/homeassistant) :8123 | Home Assistant terintegrasi dengan lebih dari 1000 perangkat dan layanan yang berbeda, serta memiliki fitur otomatisasi yang andal. |
| 109 | Kodbox | [Beranda](https://kodcloud.com/) | [Docker](https://hub.docker.com/r/kodcloud/kodbox) :8081 | Solusi manajemen dokumen online berbasis cloud pribadi. |
| 110 | CouchPotato | [Beranda](https://couchpota.to/) | [Docker](https://hub.docker.com/r/linuxserver/couchpotato) :5050 | CouchPotato adalah pengunduh NZB dan torrent otomatis yang secara otomatis mencari film yang ingin Anda tonton. |
| 111 | Sonarr | [Beranda](https://sonarr.tv/) | [Docker](https://hub.docker.com/r/linuxserver/sonarr) :8989 | Sonarr adalah perekam video pribadi untuk pengguna Usenet dan BitTorrent. |
| 112 | Radarr | [Beranda](https://radarr.video/) | [Docker](https://hub.docker.com/r/linuxserver/radarr) :7878 | Radarr adalah pengelola koleksi film untuk pengguna Usenet dan BitTorrent. |
| 113 | Syncthing | [Beranda](https://syncthing.net/) | [Docker](https://hub.docker.com/r/linuxserver/syncthing) :8384 | Syncthing adalah program sinkronisasi file berkelanjutan. |
| 114 | FileBrowser | [Beranda](https://filebrowser.org/) | [Docker](https://hub.docker.com/r/filebrowser/filebrowser) :8002 | File Browser menyediakan antarmuka manajemen file di dalam direktori tertentu, yang memungkinkan Anda mengunggah, menghapus, mempratinjau, mengganti nama, dan mengedit file. |
| 115 | Heimdall | [Beranda](https://heimdall.site/) | [Docker](https://hub.docker.com/r/linuxserver/heimdall) :8003 | Heimdall adalah cara sederhana untuk mengatur tautan ke situs web dan aplikasi web yang sering Anda gunakan. |
| 116 | Node-RED | [Beranda](https://nodered.org/) | [Docker](https://nodered.org/docs/getting-started/docker) :1880 | Node-RED adalah alat pemrograman. Alat ini menyediakan editor berbasis browser yang memudahkan Anda menghubungkan alur (flow) menggunakan berbagai node di palet, lalu men-deploy dan menjalankannya dengan sekali klik. |
| 117 | Mosquitto | [Beranda](https://www.mosquitto.org/) | [Docker](https://hub.docker.com/r/arm64v8/eclipse-mosquitto) :1883 | Protokol MQTT menyediakan metode pengiriman pesan yang ringan menggunakan model publish/subscribe. Eclipse Mosquitto adalah implementasi server open source untuk protokol MQTT versi 5, 3.1.1, dan 3.1. |
| 118 | OpenWrt | [Beranda](https://www.openwrt.org/) | [Docker](https://hub.docker.com/r/ophub/openwrt-armv8) :80 | Proyek OpenWrt adalah sistem operasi Linux untuk perangkat tertanam (embedded), yang mendukung lebih dari 3000 paket aplikasi terstandardisasi dan plugin pihak ketiga yang sangat beragam. |
| 119 | Netdata | [Beranda](https://learn.netdata.cloud/) | [Docker](https://hub.docker.com/r/netdata/netdata) :19999 | Netdata adalah alat pemantauan kinerja dan kesehatan secara real-time yang terdistribusi untuk sistem dan aplikasi. |
| 120 | XunLei | [Beranda](https://github.com/cnk3x/xunlei) | [Docker](https://hub.docker.com/r/cnk3x/xunlei) :2345 | Program layanan unduhan jarak jauh yang diekstrak dari paket Xunlei untuk Synology. |
| 121 | Docker-Headless | [Beranda](https://github.com/infrastlabs/docker-headless) | [Docker](https://hub.docker.com/r/infrastlabs/docker-headless) :10081 | Desktop jarak jauh dengan dukungan audio/lokal bahasa/IBus. Mendukung beberapa desktop (Gnome, Plasma, Mate, Xfce, Cinnamon). |
| 122 | Navidrome | [Beranda](https://www.navidrome.org/) | [Docker](https://hub.docker.com/r/deluan/navidrome) :4533 | Navidrome adalah server dan streamer musik open source yang di-hosting sendiri. Anda dapat menikmati koleksi musik Anda dengan bebas dari browser atau perangkat seluler apa pun. |
| 123 | Openlist | [Beranda](https://www.oplist.org/) | [Docker](https://hub.docker.com/r/openlistteam/openlist) :5244 | Program daftar file yang mendukung berbagai penyimpanan, dibangun menggunakan Gin dan Solidjs. |
| 124 | QingLong | [Beranda](https://github.com/whyour/qinglong) | [Docker](https://hub.docker.com/r/whyour/qinglong) :5700 | Panel manajemen tugas terjadwal yang mendukung python3, javaScript, shell, dan typescript. |
| 125 | ChatGPT-Next-Web | [Beranda](https://github.com/Yidadaa/ChatGPT-Next-Web) | [Docker](https://hub.docker.com/r/yidadaa/chatgpt-next-web) :3000 | Aplikasi ChatGPT pribadi lintas platform yang dapat di-deploy secara gratis dengan sekali klik. |
| 126 | N8N | [Beranda](https://n8n.io/) | [Docker](https://hub.docker.com/r/n8nio/n8n) :5678 | n8n adalah platform otomatisasi workflow yang memberikan kecepatan pengembangan tinggi tanpa kode (no-code) bagi tim teknis. Dilengkapi lebih dari 400 integrasi dan kemampuan AI bawaan, serta menggunakan lisensi fair-code. Anda dapat membangun alur otomatisasi yang andal sambil tetap memegang kendali penuh atas data dan deployment Anda. |
| 201 | Desktop:GNOME | [Beranda](https://www.gnome.org/) | - | GNOME menyediakan lingkungan kerja desktop yang terfokus untuk membantu Anda menyelesaikan pekerjaan. `Desktop` dapat digunakan dengan menghubungkannya ke monitor, atau dapat juga diakses menggunakan perangkat lunak [desktop jarak jauh](https://learn.microsoft.com/ja-jp/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients). |
| 202 | Firefox | [Beranda](https://www.mozilla.org/) | - | Browser web yang unggul. |
| 203 | VLC | [Beranda](https://www.videolan.org/) | - | VLC adalah pemutar dan framework multimedia lintas platform yang gratis dan open source, yang dapat memutar sebagian besar file multimedia. |
| 204 | MPV | [Beranda](https://mpv.io/) | - | Pemutar media lintas platform yang gratis dan open source. |
| 205 | GIMP | [Beranda](https://www.gimp.org/) | - | GIMP adalah editor gambar lintas platform. |
| 206 | Krita | [Beranda](https://krita.org/) | - | Krita adalah program melukis profesional yang gratis dan open source. |
| 207 | LibreOffice | [Beranda](https://www.libreoffice.org/) | - | LibreOffice adalah paket perkantoran yang gratis dan andal. Antarmukanya yang rapi dan fiturnya yang kaya membantu Anda menyalurkan kreativitas dan meningkatkan produktivitas. |
| 208 | Shotcut | [Beranda](https://shotcut.org/) | - | Shotcut adalah editor video lintas platform yang gratis dan open source. |
| 209 | Kdenlive | [Beranda](https://kdenlive.org/) | - | Kdenlive adalah editor video yang gratis dan open source. |
| 210 | Thunderbird | [Beranda](https://www.thunderbird.net/) | - | Thunderbird menggabungkan kecepatan, privasi, dan teknologi terbaru untuk memberikan pengalaman email yang lebih baik. |
| 211 | Evolution | [Beranda](https://github.com/GNOME/evolution) | - | Evolution adalah aplikasi manajemen informasi pribadi yang menyediakan fitur email, kalender, dan buku alamat yang terintegrasi. |
| 212 | Gwenview | [Beranda](https://apps.kde.org/gwenview/) | - | Gwenview adalah penampil gambar buatan KDE yang ringan dan mudah digunakan, ideal untuk menjelajahi dan menampilkan koleksi gambar. |
| 213 | Eog | [Beranda](https://gitlab.gnome.org/GNOME/eog) | - | Eye of GNOME (eog) adalah program penampil gambar. Program ini bertujuan menjadi penampil gambar yang cepat dan fungsional. |
| 214 | VisualStudioCode | [Beranda](https://code.visualstudio.com/) | - | Visual Studio Code adalah editor kode sumber yang ringan namun andal. |
| 215 | Gedit | [Beranda](https://github.com/GNOME/gedit) | - | Gedit adalah editor teks berfitur lengkap untuk lingkungan desktop GNOME. Dapat digunakan untuk membuat catatan dan dokumen sederhana, dan dengan memanfaatkan fitur-fitur lanjutannya, juga dapat digunakan sebagai lingkungan pengembangan perangkat lunak Anda sendiri. |
| 216 | Flameshot | [Beranda](https://flameshot.org/) | - | Perangkat lunak tangkapan layar open source yang andal namun mudah digunakan. |
| 301 | Frps | [Beranda](https://gofrp.org/) | - | Frp adalah reverse proxy cepat yang memungkinkan Anda mengekspos server lokal di balik NAT atau firewall ke internet. |
| 302 | Frpc | [Beranda](https://gofrp.org/) | - | Frp adalah aplikasi reverse proxy berkinerja tinggi yang berfokus pada penetrasi intranet, mendukung protokol TCP, UDP, HTTP, HTTPS, dan lainnya. |
| 303 | NPS | [Beranda](https://ehang-io.github.io/nps) | - | Sisi server NPS. Server proxy penetrasi intranet yang ringan, berkinerja tinggi, dan andal, dilengkapi terminal manajemen web yang kuat. |
| 304 | NPC | [Beranda](https://ehang-io.github.io/nps) | - | NPC adalah klien dari NPS. |
| 305 | Plex | [Beranda](https://www.plex.tv/) | - | Mulai dari media pribadi di server Anda sendiri hingga film dan acara gratis maupun on-demand, TV langsung, podcast, acara web, dan streaming musik, semuanya dapat dinikmati dalam satu aplikasi di perangkat apa pun. |
| 306 | Emby-Server | [Beranda](https://emby.media/) | - | Sinkronkan media pribadi Anda ke cloud untuk mencadangkan, mengarsipkan, dan mengonversinya dengan mudah. Simpan konten dalam berbagai resolusi untuk streaming langsung dari perangkat apa pun. |
| 307 | KVM | [Beranda](https://virt-manager.org/) | - | KVM (Kernel-based Virtual Machine) adalah solusi virtualisasi lengkap untuk Linux yang mencakup ekstensi virtualisasi. virt-manager adalah antarmuka pengguna desktop untuk mengelola mesin virtual melalui libvirt. Terutama ditujukan untuk VM KVM, tetapi juga dapat mengelola Xen dan LXC (Linux Containers). Pada mesin virtual KVM, Anda dapat menginstal [OpenWrt](https://github.com/unifreq/openwrt_packit), Debian, Ubuntu, OpenSUSE, ArchLinux, Centos, Gentoo, KyLin, UOS, dan lainnya. |
| 308 | PVE | [Beranda](https://github.com/pimox/pimox7) | https://IP:8006 | Proxmox Virtual Environment adalah solusi manajemen virtualisasi server open source berbasis QEMU/KVM dan LXC. Anda dapat mengelola mesin virtual, container, klaster ketersediaan tinggi, penyimpanan, dan jaringan melalui antarmuka web terintegrasi atau CLI. |
| 309 | CasaOS | [Beranda](https://github.com/IceWhaleTech/CasaOS) | http://IP | CasaOS adalah sistem cloud pribadi open source yang sederhana, mudah digunakan, dan elegan. |
| 310 | ArozOS | [Beranda](https://github.com/tobychui/arozos) | http://IP:8080 | ArozOS adalah sistem operasi desktop berbasis web yang cocok untuk platform berdaya rendah. Dilengkapi fitur manajemen file/disk, statistik jaringan, server web, dan lainnya. |

## Cara Menggunakan Pusat Perangkat Lunak

Masuk ke sistem Armbian, lalu masukkan perintah berikut:

```shell
armbian-software
```

Daftar manajemen cepat perangkat lunak yang sudah terintegrasi akan ditampilkan. Contoh:

```shell
root@armbian:~# armbian-software
[ STEPS ] Start selecting software [ Current system: debian/bullseye ]...
----------------------------------------------------------
ID    NAME                STATE           MANAGE
----------------------------------------------------------
102   Portainer           installed       update/remove
202   Firefox             installed       update/remove
302   Frpc                not-installed   install
...
----------------------------------------------------------
[ OPTIONS ] Please Input Software ID:
```

- `Perangkat lunak yang belum terinstal`: status ditampilkan sebagai `not-installed`. Masukkan `ID` perangkat lunak untuk menginstalnya.
- `Perangkat lunak yang sudah terinstal`: status ditampilkan sebagai `installed`. Masukkan `ID` perangkat lunak, lalu pilih perbarui atau hapus sesuai petunjuk.

> Catatan tentang `101` Docker: `update` hanya memperbarui paket-paket terkait Docker dan tidak menyentuh bagian lain dari sistem. `remove` akan menghapus instalasi Docker, tetapi data di `/var/lib/docker` (image, container, volume) tetap **dipertahankan**. Untuk juga menghapus data tersebut, jalankan `armbian-docker remove --purge-data` dan masukkan `YES` untuk konfirmasi. Detailnya dapat dilihat dengan `armbian-docker -h`.

## Panduan Pengembangan Pusat Perangkat Lunak

Skrip dan perintah pusat perangkat lunak disimpan secara terpusat di direktori [/usr/share/ophub/armbian-software](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software). Dengan perintah `armbian-software -u`, Anda dapat menyinkronkan dan mengunduh direktori ini ke lokal serta memperbarui daftar pusat perangkat lunak. File yang diawali angka adalah `skrip instalasi sekali klik` untuk perangkat lunak yang bersangkutan. [software-command.sh](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-command.sh) adalah `file perintah terpadu` untuk operasi instal/perbarui/hapus. [software-list.conf](../build-armbian/armbian-files/common-files/usr/share/ophub/armbian-software/software-list.conf) adalah file konfigurasi daftar perangkat lunak, dengan penjelasan sebagai berikut:

```yaml
# 1.ID     2.Nama Perangkat Lunak     3.MetodeAutentikasi@Paket      4.Pilihan Eksekusi     5.Rilis yang Didukung
102        :Portainer          :docker@portainer         :command-docker.sh      :all
202        :Firefox            :dpkg@firefox             :command-desktop.sh     :all
302        :Frpc               :which@frpc               :302-frpc.sh            :all
308        :PVE                :dpkg@pve-manager         :command-service.sh     :bullseye@bookworm
...
```

- `ID`: `nomor seri unik` perangkat lunak.
- `Software Name`: `nama perangkat lunak` (panjang nama harus kurang dari 40 karakter).
- `AuthMethod@Package`: `metode pemeriksaan` status instalasi perangkat lunak dan `paket perangkat lunak` yang bersangkutan, dipisahkan dengan simbol `@`.
  - Image yang diinstal melalui container `docker` diperiksa dengan metode `docker`. Contoh: untuk memeriksa apakah image `portainer` sudah terinstal, gunakan `docker@portainer`.
  - Paket yang diinstal melalui `apt` diperiksa dengan metode `dpkg`. Contoh: untuk memeriksa apakah `firefox` sudah terinstal, gunakan `dpkg@firefox`.
  - Jika file eksekusi ada di direktori perintah sistem (bin, sbin), periksa dengan metode `which`. Contoh: untuk memeriksa apakah layanan `frpc` sudah terinstal, gunakan `which@frpc`.
  - Jika tidak ada file eksekusi di direktori perintah sistem, periksa keberadaan path tertentu dengan metode `find`. Contoh: untuk memeriksa apakah sistem `arozos` sudah terinstal, gunakan `find@/root/arozos`.
- `Execute Selection`: menentukan apakah perangkat lunak dikelola dengan `file perintah terpadu` atau `skrip mandiri`.
  - Perangkat lunak dengan operasi yang `relatif sederhana` dikumpulkan per kategori di file `command-docker.sh / command-desktop.sh / command-service.sh`, dan dinamai berdasarkan nomor seri perangkat lunak. Misalnya, operasi `portainer` (nomor seri `102`) ditulis di `software_102()`.
  - Perangkat lunak yang `relatif kompleks dengan isi perintah yang panjang` dikelola dengan file skrip mandiri. Misalnya, skrip instalasi `frpc` diawali dengan nomor seri dan dinamai `302-frpc.sh`.
- `Supported Release`: menentukan `kode nama versi sistem` Armbian yang didukung. Gunakan `all` jika semua versi didukung. Jika hanya sebagian versi yang didukung, isi kode nama versinya, dan hubungkan beberapa kode nama dengan simbol `@`.

Kami menyambut penambahan lebih banyak perangkat lunak. Silakan ajukan permintaan dukungan di [Issues](https://github.com/farishhz/amlogic-s9xxx-armbian/issues).
