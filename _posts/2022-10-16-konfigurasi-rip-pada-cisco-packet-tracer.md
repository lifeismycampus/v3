---
layout: post
title: Konfigurasi RIP pada Cisco Packet Tracer
date: 2022-10-16 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing, subnetting]
---

## Ulasan

Routing Information Protocol (RIP) adalah protokol routing dengan jenis distance vector yang digunakan untuk berbagi informasi perutean antar router dalam jaringan.

RIP adalah protokol yang sangat andal karena menggunakan algoritma bellman-ford, namun pembatasan jumlah hop yang diizinkan, membuatnya kurang cocok untuk jaringan besar.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                     | Deskripsi                                               |
| -------------------------------------------- | ------------------------------------------------------- |
| Router(config)#router rip                    | mengaktifkan routing procotol RIP                       |
| Router(config-router)#version 2              | memilih RIP versi 2                                     |
| Router(config-router)#network `dest-network` | melakukan advertise pada directly connected network     |
| Router(config-router)#no auto-summary        | menghentikan peringkasan jaringan yang tidak diperlukan |

> **Catatan:**
> Untuk selanjutnya, konfigurasi jaringan RIP menggunakan versi 2.

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

Susun topologi jaringan routing sebagai berikut

![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

| Routing Protocol  | RIPv2                                |
| ----------------- | ------------------------------------ |
| Wireless SSID     | hotspot@nama , contoh: hotspot@angga |
| WPA2-PSK          | xxpswdxx , contoh: 99pswd99          |
| Encryption        | AES                                  |
| Web server domain | altavista.net                        |

#### Tabel Pengalamatan

| Device      | Interface | IP Address   | Prefix | Gateway      |
| ----------- | --------- | ------------ | ------ | ------------ |
| RCore       | Fa0/0     | 10.100.100.1 | /30    | -            |
| RCore       | Fa1/0     | 10.100.200.1 | /30    | -            |
| RCore       | Fa2/0     | 192.168.10.1 | /24    | -            |
| RWired      | Fa0/0     | 10.100.100.2 | /30    | -            |
| RWired      | Fa1/0     | 192.168.20.1 | /24    | -            |
| RWireless   | Internet  | 10.100.200.2 | /30    | -            |
| RWireless   | LAN       | 192.168.30.1 | /24    | -            |
| PCServer    | Fa0       | 192.168.10.2 | /24    | 192.168.10.1 |
| PCAdmin     | Fa0       | 192.168.10.3 | /24    | 192.168.10.1 |
| PC1         | Fa0       | dhcp         | /24    | 192.168.20.1 |
| PC2         | Fa0       | dhcp         | /24    | 192.168.20.1 |
| Laptop1     | Wl0       | dhcp         | /24    | 192.168.30.1 |
| Laptop2     | Wl0       | dhcp         | /24    | 192.168.30.1 |
| Smartphone1 | Wl0       | dhcp         | /24    | 192.168.30.1 |
| Smartphone2 | Wl0       | dhcp         | /24    | 192.168.30.1 |

### Konfigurasi

#### PCServer

1. Input alamat ip pada interface

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/02.png){: .normal }

1. Aktifkan web server

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/03.png){: .normal }

1. Edit halaman index.html

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/04.png){: .normal }

   Simpan dengan klik tombol Save

1. Aktifkan domain pada web server

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/05.png){: .normal }

#### PCAdmin

1. Input alamat ip pada interface

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/06.png){: .normal }

#### RCore

1. Input alamat ip pada interface

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/07.png){: .normal }

2. Konfigurasi RIPv2

   ```console
   Router (config)#router rip
   Router (config-router)#version 2
   Router (config-router)#network 192.168.10.0
   Router (config-router)#network 10.100.100.0
   Router (config-router)#network 10.100.200.0
   Router (config-router)#no auto-summary
   Router (config-router)#exit
   Router (config)#
   ```

#### RWired

1. Input alamat ip pada interface

   ```console
   Router(config)#interface fastEthernet 0/0
   Router(config-if)#ip address 10.100.100.2 255.255.255.252
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface fastEthernet 1/0
   Router(config-if)#ip address 192.168.20.1 255.255.255.0
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#
   ```

2. Konfigurasi dhcp server

   ```console
   Router(config)#ip dhcp pool lan2
   Router(dhcp-config)#network 192.168.20.0 255.255.255.0
   Router(dhcp-config)#default-router 192.168.20.1
   Router(dhcp-config)#dns-server 192.168.10.2
   Router(dhcp-config)#exit
   Router(config)#ip dhcp excluded-address 192.168.20.1
   Router(config)#
   ```

3. Konfigurasi RIPv2

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#network 10.100.100.0
   Router(config-router)#network 192.168.20.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### RWireless

1. Input alamat ip pada interface

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/08.png){: .normal }

2. Input alamat ip pada gateway wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/09.png){: .normal }

3. Konfigurasi username password wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/10.png){: .normal }

4. Konfigurasi dhcp server

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/11.png){: .normal }

   Simpan dengan klik tombol Save Settings

#### Client PC pada RWired

1. Request alamat ip pada interface

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/12.png){: .normal }

#### Client Laptop pada RWireless

1. Menyambungkan dengan jaringan wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/13.png){: .normal }

1. Isikan SSID dan WPA2-PSK yang sesuai

1. Ubah IP Config dari DHCP ke Static Kembali ke DHCP lagi untuk merequest alamat IP wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/14.png){: .normal }

#### Client Smartphone pada RWireless

1. Menyambungkan dengan jaringan wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/15.png){: .normal }

1. Isikan SSID dan WPA2-PSK yang sesuai

1. Ubah IP Config dari DHCP ke Static Kembali ke DHCP lagi untuk merequest alamat IP wLAN3

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/16.png){: .normal }

### Pengujian

1. Konfirmasi routing table pada RCore

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/17.png){: .normal }

   > **Catatan:**
   > Kode `R` merupakan indikator jaringan dari router lain yang mengaktifkan protocol routing RIP.

2. Konfirmasi routing table pada RWired

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/18.png){: .normal }

3. Lakukan pengujian PING dari PC1 ke PCServer maupun ke PCAdmin

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/19.png){: .normal }

4. Lakukan pengujian PING dari Laptop1 ke PC1 maupun ke Smartphone1

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/20.png){: .normal }

5. Lakukan pengujian Web Browser dari PC2, Laptop2 dan Smartphone2 ke kombinasi alamat berikut baik berupa ip maupun domain

   1. http://192.168.10.2
   2. https://192.168.10.2
   3. http://altavista.net
   4. https://altavista.net

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/21.png){: .normal }

## Berlatih

Sebagai bahan latihan, rancang topologi jaringan routing di SMKN 1 Gombong menggunakan routing protocol RIPv2 dengan ketentuan mempunyai 2 domain web server masing-masing

1. belajar.smkn1gombong.sch.id

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/22.png)

2. ujian.smkn1gombong.sch.id

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/23.png)

3. dengan topologi jaringan sebagai berikut

   ![](/assets/img/2022-10-16-konfigurasi-rip-pada-cisco-packet-tracer/24.png)
