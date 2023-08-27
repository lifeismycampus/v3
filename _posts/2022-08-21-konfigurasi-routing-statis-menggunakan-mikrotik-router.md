---
layout: post
title: Konfigurasi Routing Statis Menggunakan MikroTik Router
date: 2022-08-21 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [mikrotik, routing, subnetting]
---

## Ulasan

Dengan konsep yang sama jaringan routing statis, berikut adalah implementasi konfigurasi pada router MikroTik menggunakan jaringan wireless untuk saling melakukan akses terhadap web server dari jaringan lain.

## Alat dan Bahan

1. Smartphone ter-install web browser
1. Komputer ter-install web browser
1. Jaringan wireless instruktur
   - SSID: StaticRoutingCore
   - Passphrase: P@ssw0rd
1. MikroTik Router
   - Reset Configuration
   - No Default Configuration
1. MikroTik WinBox
   - Eth2, Eth3, Eth4 sebagai interface untuk konfig
   - Eth1 sebagai dhcp server jaringan lan
   - Wlan1 sebagai dhcp client jaringan instruktur
   - vWlan2 sebagai dhcp server jaringan wan
1. Oracle VirtualBox
1. FileZilla
1. File \*.ova [Debian 11 Server](https://www.osboxes.org/debian/){:target="\_blank"} sebagai web server
1. File \*.zip [simple-landing-page-master](https://github.com/sandhikagalih/simple-landing-page/archive/refs/heads/master.zip){:target="\_blank"} sebagai web project

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/routing-statis-wireless-top.png){: .normal }

#### Tabel Pengalamatan

1. Instruktur mencatat jaringan wan dan lan seluruh no meja dalam tabel

   ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/routing-statis-wireless-ip-table.png){: .normal }

1. Instruktur mengonfigurasi routing status seluruh jaringan wan dan lan tersebut

### Konfigurasi

#### Jaringan

1. Atur identitas pada perangkat Router

   1. Sambungkan kabel komputer ke perangkat Router menggunakan interface eth2/eth3/eth4 untuk melakukan konfigurasi

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/interface-router-1.png){: .normal }

   1. Buka program WinBox dan lakukan login menggunakan mac address

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/identitas-router-1.png){: .normal }

   1. Masuk menu System, pilih Identity, beri nama sesuai meja

      > Format: R.Statis-"no-meja"
      >
      > Contoh: R.Statis-1

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/identitas-router-2.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

1. Atur dhcp client jaringan wireless instruktur pada wlan1

   1. Masuk menu Interface, aktifkan wlan1

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-1.png){: .normal }

      tutup window Interface List

   1. Masuk menu Wireless, double click pada interface wlan1, klik tombol Setup Repeater

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-2.png){: .normal }

   1. Atur sebagai berikut, klik tombol Start

      - Interface wlan1
      - SSID StaticRoutingCore
      - Passphrase P@ssw0rd

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-3.png){: .normal }

      Pastikan status Done, klik tombol Close

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-4.png){: .normal }

      tutup window Wireless Table

   1. Masuk menu Bridge,

      hapus bridge pada tab Bridge

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-5.png){: .normal }

      maupun interface pada tab Ports

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-6.png){: .normal }

      tutup window Bridge

   1. Masuk menu IP > DHCP Client, klik tombol +, pilih wlan1 klik tombol Apply

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-client-pada-wlan1-7.png){: .normal }

      Pastikan status Bound, klik tombol Close

      tutup window DHCP Client

1. Atur alamat pada vwlan2 dan eth1 sebagai gateway dhcp server jaringan wan dan lan

   1. Masuk menu Wireless, masuk tab Security Profiles, klik tombol +, atur sebagai berikut

      > Security Profile maupun WPA PSK
      >
      > Format: Rstatis"no-meja"
      >
      > Contoh: Rstatis1

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-pada-vwlan2-1.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

   1. Masih menu Wireless, masuk tab Wifi Interfaces, klik 2x pada interface (virtual) wlan2

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-pada-vwlan2-2.png){: .normal }

      masuk tab Wireless, atur SSID dan Security Profile dengan yang baru saja dibuat

      > SSID
      >
      > Format: R.Statis"no-meja"-"nama1"-"nama2"
      >
      > Contoh: R.Statis1-angga-indra

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-pada-vwlan2-3.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

      tutup window Wireless Table

   1. Masuk menu IP > Addresses, klik tombol +, atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-pada-vwlan2-4.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

   1. Masih menu IP > Addresses, klik tombol +, atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-pada-eth1-1.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

      tutup window Address List

1. Atur dhcp server jaringan wan dan lan

   1. DHCP Server pada jaringan wan

      Masuk menu IP > DHCP Server, klik tombol DHCP Setup

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-1.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-2.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-3.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-4.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-5.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-6.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-wan-7.png){: .normal }

      pastikan status Setup … successfully, klik tombol OK

   1. DHCP Server pada jaringan lan

      Masih menu IP > DHCP Server, klik tombol DHCP Setup

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-1.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-2.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-3.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-4.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-5.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-6.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/dhcp-server-lan-7.png){: .normal }

      pastikan status Setup … successfully, klik tombol OK

      tutup window DHCP Server

1. Konfigurasi routing statis

   1. Entry route ke jaringan instruktur

      Masuk menu IP > Routes, klik tombol +, atur sebagai berikut

      > **Catatan:**
      > Gateway adalah IP wlan1 jaringan instruktur

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-route-instruktur-1.png){: .normal }

   1. Entry route ke jaringan meja lain sesuai

      > **Catatan:**
      > Seluruh jaringan wan dan lan tersedia dari seluruh meja akan ditampilkan oleh instruktur

      Masih menu IP > Routes, klik tombol +, atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-route-meja-lain-1.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-route-meja-lain-2.png){: .normal }

      input jaringan wan dan lan dari seluruh meja

   1. Verifikasi jaringan routing

      Masih menu IP > Routes, pastikan jaringan wan dan lain meja lain muncul

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-route-verifikasi-1.png){: .normal }

      Masuk menu New Terminal, lakukan perintah ping ke alamat gateway jaringan wan dan lan meja lain

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/ip-route-verifikasi-2.png){: .normal }

      pastikan jaringan wan dan lan dari seluruh meja bisa diakses

1. Konfigurasi NAT

   1. Masuk menu IP > Firewall, masuk tab NAT, klik tombol +

      Pada tab General, atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/nat-1.png){: .normal }

      pada tab Action, atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/nat-2.png){: .normal }

      akhiri dengan klik tombol Apply lalu klik tombol OK

      tutup window Firewall

   1. Konfigurasi jaringan selesai, tutup program WinBox

1. Mendapatkan alamat DHCP Client

   1. Cabut dan sambungkan kabel komputer ke perangkat Router menggunakan interface eth1

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/interface-router-2.png){: .normal }

   1. Verifikasi alamat IP yang didapatkan komputer

      > **Catatan:**
      > Buka program Command Prompt/Console/Terminal, tampilkan informasi ip mengggunakan perintah
      >
      > - ipconfig (Windows)
      > - ip addr (Linux)
      > - ifconfig (macOS)

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-1.png){: .normal }

   1. Pada perangkat smartphone, pastikan SSID muncul

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-2.png){: .normal }

   1. Sambungkan perangkat smartphone ke SSID sesuai meja masing-masing

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-3.png){: .normal }

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-4.png){: .normal }

   1. Verifikasi alamat IP yang didapatkan smartphone

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-5.png){: .normal }

   1. Verifikasi jaringan routing statis,

      Untuk memverifikasi routing statis dalam antara jaringan wan dan lan (local),

      1. ping dari komputer menuju ip smarphone

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/verifikasi-dhclient-6.png){: .normal }

      Untuk memverifikasi routing statis dengan jaringan wan dan lan meja lain (remote),

      1. ping dari komputer menuju ip komputer meja lain
      1. ping dari komputer menuju ip smartphone meja lain

      Ekspektasi hasil yaitu seluruh jaringan dapat saling terhubung, sehingga ketika diuji dengan perintah ping maka hasilnya semua reply

#### Web Server

1. Menyiapkan instance virtual machine

   1. Buka program VirtualBox, pilih menu Tools, klik tombol Import

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-1.png){: .normal }

   1. Klik tombol Choose a virtual appliance to import…,

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-2.png){: .normal }

   1. Pilih file \*.ova yang disediakan, klik tombol Open

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-3.png){: .normal }

   1. Pastikan file terpilih sesuai, klik tombol Continue

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-4.png){: .normal }

   1. Ganti MAC Address Policy menjadi Generate new MAC …, klik tombol Import

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-5.png){: .normal }

      proses import berjalan

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/import-vm-6.png){: .normal }

1. Mengakses instance virtual machine

   1. Pilih vm Debian 11 Server (32bit), klik tombol Setting

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/run-vm-1.png){: .normal }

   1. Masuk menu Network, atur sebagai berikut

      Name dipilih sesuai network interface card fisik yang digunakan untuk menyambungkan komputer dengan perangkat Router

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/run-vm-2.png){: .normal }

      akhiri dengan klik tombol OK

   1. Pilih vm Debian 11 Server (32bit), klik tombol Start

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/run-vm-3.png){: .normal }

   1. Login menggunakan akun

      > username: osboxes
      >
      > password: linux123

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/run-vm-4.png){: .normal }

1. Mengonfigurasi jaringan web server

   1. Edit file konfigurasi interface jaringan

      ```bash
      $ sudo nano /etc/network/interfaces
      ```

      atur sebagai berikut

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/network-vm-1.png){: .normal }

      simpan hasil edit dengan urutan shortcut keyboard

      - <kbd>Ctrl</kbd>+<kbd>x</kbd>,
      - <kbd>y</kbd>,
      - <kbd>Enter</kbd>

   1. Restart vm

      ```bash
      $ sudo reboot now
      ```

   1. Login kembali, verifikasi ip address yang baru saja dikonfig

      ```bash
      ip addr | grep inet
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/network-vm-2.png){: .normal }

   1. Verifikasi jaringan internet berkerja

      ```bash
      $ ping -c 3 google.com
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/network-vm-3.png){: .normal }

   1. Perbaharui data indexing pada repository

      ```bash
      $ sudo apt update -y
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/network-vm-4.png){: .normal }

1. Menginstall web server

   1. Hentikan service dari web server bawaan (apache2)

      ```bash
      $ sudo service apache2 stop
      $ sudo service apache2 status
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/web-srv-vm-1.png){: .normal }

      akhiri dengan shortcut keyboard <kbd>q</kbd>

   1. Install nginx web server (dan unzip)

      ```bash
      $ sudo apt install nginx unzip -y
      ```

      > **Catatan:**
      > Package unzip dibutuhkan untuk extract folder web nanti

   1. Verifikasi service dari nginxi web server berjalan

      ```bash
      $ sudo service nginx status
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/web-srv-vm-2.png){: .normal }

      akhiri dengan shortcut keyboard <kbd>q</kbd>

1. Membuat folder root web server

   1. Buka program FileZilla, atur login sebagai berikut, klik tombol Quickconnect

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-1.png){: .normal }

      jika muncul prompt, pilih Do not save sasswords

   1. Pada window Unknown host key, klik tombol OK

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-2.png){: .normal }

   1. Pada kolom local, klik kanan file simple-landing-page-master.zip, klik tombol Upload

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-3.png){: .normal }

   1. Proses upload selesai, pastikan file simple-landing-page-master.zip tersedia di kolom remote

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-4.png){: .normal }

      Upload file selesai, tutup program Filezilla

   1. Kembali ke Debian server, verifikasi file simple-landing-page-master.zip tersedia

      ```bash
      $ ls -l
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-5.png){: .normal }

   1. Extract file simple-landing-page-master.zip, lakukan verifikasi folder hasil extract

      ```bash
      $ unzip simple-landing-page-master.zip
      $ ls -l
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-6.png){: .normal }

   1. Rename folder hasil extract

      ```bash
      $ mv simple-landing-page-master web
      $ ls -l
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-7.png){: .normal }

   1. Edit file index.html, atur sebagai berikut

      ```bash
      $ nano web/index.html
      ```

      Ganti dengan nama anda masing-masing

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-8.png){: .normal }

      simpan hasil edit dengan urutan shortcut keyboard

      - <kbd>Ctrl</kbd>+<kbd>x</kbd>,
      - <kbd>y</kbd>,
      - <kbd>Enter</kbd>

   1. Pindah folder web ke /var/www/html

      ```bash
      $ sudo mv web/ /var/www/html/
      $ ls -l /var/www/html/
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/upload-page-9.png){: .normal }

1. Membuat blok web server

   1. Buat server blok sendiri pada folder /etc/nginx/conf.d/

      ```bash
      $ sudo touch /etc/nginx/conf.d/websrv.conf
      ```

   1. Edit file websrv.conf, atur sebagai berikut

      ```bash
      $ sudo nano /etc/nginx/conf.d/websrv.conf
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/block-srv-1.png){: .normal }

      simpan hasil edit dengan urutan shortcut keyboard

      - <kbd>Ctrl</kbd>+<kbd>x</kbd>,
      - <kbd>y</kbd>,
      - <kbd>Enter</kbd>

   1. Verifikasi konfigurasi nginx

      ```bash
      $ sudo nginx -t
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/block-srv-2.png){: .normal }

   1. Muat ulang service dari nginx web server

      ```bash
      $ sudo service nginx restart
      $ sudo service nginx status
      ```

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/block-srv-3.png){: .normal }

### Pengujian

1. Hasil konfigurasi pada router local (jaringan sendiri)

   1. Akses alamat web server menggunakan program web browser dari komputer,

      http://ip-address-web-server:8080

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/access-web-srv-1.png){: .normal }

   2. Akses alamat web server menggunakan program web browser dari smartphone,

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/access-web-srv-2.png){: .normal }

2. Hasil konfigurasi pada router remote (jaringan meja lain)

   1. Anda lakukan koordinasi dengan teman meja lain, minimal dengan 3 meja/kelompok lain

   2. Dalam kondisi terhubung ke jaringan anda, akses alamat web server teman meja lain menggunakan program web browser dari komputer,

      http://ip-address-web-server-remote:8080

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/access-web-srv-3.png){: .normal }

   3. Dalam kondisi terhubung ke jaringan anda, akses alamat web server teman meja lain menggunakan program web browser dari smartphone,

      ![](/assets/img/2022-08-21-konfigurasi-routing-statis-menggunakan-mikrotik-router/access-web-srv-4.png){: .normal }

   4. Lakukan secara vice versa,

      Dalam kondisi terhubung ke jaringan mereka, teman dari meja lain mengakses alamat web server anda
