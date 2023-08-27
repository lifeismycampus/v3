---
layout: post
title: Konfigurasi Jaringan Routing pada Cisco Packet Tracer
date: 2022-07-17 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing, subnetting]
---

## Ulasan

Jaringan routing komputer memainkan peran yang sangat penting dalam jaringan komputer.

Ini membantu menentukan jalur terbaik bagi paket data untuk berpindah dari satu jaringan ke jaringan lain.

Dalam hal ini, routing berperan sebagai jembatan antar jaringan, memastikan bahwa paket data dapat sampai ke tujuannya dengan cepat dan efisien.

Dalam jaringan yang kompleks, routing juga memastikan bahwa paket data tidak terjebak dalam lingkaran atau rute yang tidak efisien, sehingga mengurangi jumlah paket data yang hilang atau rusak.

Routing juga memungkinkan beberapa jaringan untuk berkomunikasi satu sama lain dan berbagi informasi.

Karena itu, jaringan routing komputer adalah komponen penting dalam jaringan komputer modern.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                  | Deskripsi                                                |
| ------------------------------------------------------------------------- | -------------------------------------------------------- |
| Router(config)# ip dhcp pool `nama_pool`                                  | Mengatur nama pool                                       |
| Router(dhcp-config)# network `network_id` `subnet_mask`                   | Mengatur jaringan yang disebar                           |
| Router(dhcp-config)# default-router `ip_default_gateway`                  | Mengatur alamat gateway                                  |
| Router(dhcp-config)# dns-server `ip_dns_server`                           | Mengatur alamat server DNS                               |
| Router(dhcp-config)# exclude `ip_excluded_pertama` `ip_excluded_terakhir` | Membatasi alamat/rentang alamat yang tidak boleh disebar |
| Router(dhcp-config)# lease `hari` `jam` `menit`                           | Mengatur lease time/masa sewa suatu alamat IP            |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

Berikut contoh topologi jaringan lab TKJ di SMK Negeri 1 Gombong menggunakan jaringan routing.

Tersedia web server yang dapat diakses pada alamat

> https://lms.smkn1gombong.sch.id

![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/01.png){: .normal }

File \*.pkt topologi jaringan dapat diunduh [di sini](/assets/pkt/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/konfigurasi-jaringan-routing-lab-smkn1gombong.pkt)

#### Tabel Pengalamatan

| Interface pd Device | IP Address    | Subnet Mask | Gateway       |
| ------------------- | ------------- | ----------- | ------------- |
| Fa0 WebServer       | 192.168.0.254 | /24         | -             |
| Fa0/0 R.Sekolah     | 192.168.0.1   | /24         | -             |
| Fa2/0 R.Sekolah     | 192.168.70.1  | /24         | -             |
| Fa3/0 R.Sekolah     | 192.168.80.1  | /24         | -             |
| Fa4/0 R.Sekolah     | 192.168.90.1  | /24         | -             |
| Fa5/0 R.Sekolah     | 192.168.100.1 | /24         | -             |
| Fa0 PC1a            | DHCP Client   | /24         | 192.168.70.1  |
| Fa0 PC1b            | DHCP Client   | /24         | 192.168.70.1  |
| Fa0 PC2a            | DHCP Client   | /24         | 192.168.80.1  |
| Fa0 PC2b            | DHCP Client   | /24         | 192.168.80.1  |
| Fa0 PC3a            | DHCP Client   | /24         | 192.168.90.1  |
| Fa0 PC3b            | DHCP Client   | /24         | 192.168.90.1  |
| Fa0 PC4a            | DHCP Client   | /24         | 192.168.100.1 |
| Fa0 PC4b            | DHCP Client   | /24         | 192.168.100.1 |

### Konfigurasi

#### PC Web Server

1. Konfigurasi alamat ip

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/02.png){: .normal }

2. Konfigurasi DNS Server

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/03.png){: .normal }

#### Router Sekolah

1. Konfigurasi alamat ip

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname RouterSekolah
   RouterSekolah(config)#interface fastEthernet 0/0
   RouterSekolah(config-if)#ip address 192.168.0.1 255.255.255.0
   RouterSekolah(config-if)#no shutdown
   RouterSekolah(config-if)#exit
   RouterSekolah(config)#interface fastEthernet 2/0
   RouterSekolah(config-if)#ip address 192.168.70.1 255.255.255.0
   RouterSekolah(config-if)#no shutdown
   RouterSekolah(config-if)#exit
   RouterSekolah(config)#interface fastEthernet 3/0
   RouterSekolah(config-if)#ip address 192.168.80.1 255.255.255.0
   RouterSekolah(config-if)#no shutdown
   RouterSekolah(config-if)#exit
   RouterSekolah(config)#interface fastEthernet 4/0
   RouterSekolah(config-if)#ip address 192.168.90.1 255.255.255.0
   RouterSekolah(config-if)#no shutdown
   RouterSekolah(config-if)#exit
   RouterSekolah(config)#interface fastEthernet 5/0
   RouterSekolah(config-if)#ip address 192.168.100.1 255.255.255.0
   RouterSekolah(config-if)#no shutdown
   RouterSekolah(config-if)#exit
   RouterSekolah(config)#
   ```

2. Konfigurasi DHCP Server

   ```console
   RouterSekolah(config)#
   RouterSekolah(config)#ip dhcp pool pool1
   RouterSekolah(dhcp-config)#network 192.168.70.0 255.255.255.0
   RouterSekolah(dhcp-config)#default-router 192.168.70.1
   RouterSekolah(dhcp-config)#dns-server 192.168.0.254
   RouterSekolah(dhcp-config)#exclude 192.168.70.1 192.168.70.10
   RouterSekolah(dhcp-config)#exit
   RouterSekolah(config)#ip dhcp pool pool2
   RouterSekolah(dhcp-config)#network 192.168.80.0 255.255.255.0
   RouterSekolah(dhcp-config)#default-router 192.168.80.1
   RouterSekolah(dhcp-config)#dns-server 192.168.0.254
   RouterSekolah(dhcp-config)#exclude 192.168.80.1 192.168.80.10
   RouterSekolah(dhcp-config)#exit
   RouterSekolah(config)#ip dhcp pool pool3
   RouterSekolah(dhcp-config)#network 192.168.90.0 255.255.255.0
   RouterSekolah(dhcp-config)#dns-server 192.168.0.254
   RouterSekolah(dhcp-config)#exclude 192.168.90.1 192.168.90.10
   RouterSekolah(dhcp-config)#exit
   RouterSekolah(config)#ip dhcp pool pool4
   RouterSekolah(dhcp-config)#network 192.168.100.0 255.255.255.0
   RouterSekolah(dhcp-config)#dns-server 192.168.0.254
   RouterSekolah(dhcp-config)#exclude 192.168.100.1 192.168.100.10
   RouterSekolah(dhcp-config)#exit
   RouterSekolah(config)#end
   RouterSekolah#copy running-config startup-config
   RouterSekolah#
   ```

#### PC Client

1. Konfigurasi alamat ip PC1a, PC1b

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/04.png){: .normal }

1. Konfigurasi alamat ip PC2a, PC2b

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/05.png){: .normal }

1. Konfigurasi alamat ip PC3a, PC3b

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/06.png){: .normal }

1. Konfigurasi alamat ip PC4a, PC4b

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/07.png){: .normal }

### Pengujian

#### PC Client

1. Ping server (via IP)

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/08.png){: .normal }

1. Ping server (via Domain)

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/09.png){: .normal }

1. Akses web server via web browser via IP maupun Domain

   ![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/10.png){: .normal }

#### Kesimpulan

Jaringan lab TKJ pada SMK Negeri 1 Gombong menerapkan konfigurasi routing.

Seluruh pembagian jaringan/subnet langsung terhubung pada perangkat Router utama.

![](/assets/img/2022-07-17-konfigurasi-jaringan-routing-pada-cisco-packet-tracer/11.png){: .normal }
