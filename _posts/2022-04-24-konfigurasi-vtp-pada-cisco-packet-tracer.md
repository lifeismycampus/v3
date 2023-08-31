---
layout: post
title: Konfigurasi VTP pada Cisco Packet Tracer
date: 2022-04-24 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, switching, vlan]
---

## Ulasan

VLAN Trunking Protocol (VTP) adalah protokol jaringan yang digunakan untuk memudahkan konfigurasi dan manajemen Virtual Local Area Network (VLAN) dalam jaringan besar.

VTP memungkinkan administrator jaringan untuk mengelola informasi VLAN secara central dan memastikan bahwa semua switch dalam jaringan memiliki database VLAN yang sama.

VTP juga memungkinkan administrator jaringan untuk menambah, menghapus, dan memodifikasi VLAN dengan mudah tanpa harus melakukan konfigurasi pada setiap switch secara manual.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                 | Deskripsi                              |
| ---------------------------------------- | -------------------------------------- |
| Switch(config)#vtp domain `domain-name`  | Mengganti nama domain pada VTP         |
| Switch(config)#vtp password `word`       | Mengganti password pada VTP            |
| Switch(config)#vtp mode `operation-mode` | Mengganti mode VTP                     |
| Switch(config-if)#switchport mode trunk  | Mengganti mode interface sebagai trunk |
| Switch#show vtp status                   | Menampilkan domain dan mode VTP        |
| Switch#show vtp password                 | Menampilkan password VTP               |
| Switch#show interface trunk              | Menampilkan interface mana yang trunk  |
| Switch#show vtp counter                  | Menampilkan pesan/message dari VTP     |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi dan Konfirmasi, Konfigurasi Ulang, Pengujian.

### Persiapan

#### Topologi jaringan

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

1. VTP

   1. Domain: stemsagonet
   1. Password: rahasia

2. VLAN

   1. VLAN ID: 20, Name: Guru, Interface: Port 6-10
   2. VLAN ID: 30, Name: Siswa, Interface: Port 11-20

3. Network

   1. Net ID: 10.100.xx.0/24 (xx diganti no presensi)
   2. Host pada VLAN ID 20: xx.21 s.d. xx.30
   3. Host pada VLAN ID 30: xx.31 s.d. xx.100

#### Tabel pengalamatan

| Device   | Interface | VLAN ID | IP Address   | Subnet Mask   |
| -------- | --------- | ------- | ------------ | ------------- |
| PC0-a    | Fa0       | 20      | 10.100.xx.21 | 255.255.255.0 |
| PC0-b    | Fa1       | 30      | 10.100.xx.31 | 255.255.255.0 |
| PC1-a    | Fa2       | 20      | 10.100.xx.22 | 255.255.255.0 |
| PC1-b    | Fa3       | 30      | 10.100.xx.32 | 255.255.255.0 |
| SwServer | Fa0/24    | 20, 30  |              |               |
| SwClient | Fa0/24    | 20, 30  |              |               |

### Konfigurasi dan Konfirmasi

#### SwServer

1. Inisiasi VLAN

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname SwServer
   SwServer(config)#vlan 20
   SwServer(config-vlan)#name Guru
   SwServer(config-vlan)#exit
   SwServer(config)#vlan 30
   SwServer(config-vlan)#name Siswa
   SwServer(config-vlan)#exit
   SwServer(config)#
   ```

1. Keanggotaan VLAN

   ```console
   SwServer(config)#interface range fastEthernet 0/6-10
   SwServer(config-if-range)#switchport mode access
   SwServer(config-if-range)#switchport access vlan 20
   SwServer(config-if-range)#exit
   SwServer(config)#interface range fastEthernet 0/11-20
   SwServer(config-if-range)#switchport mode access
   SwServer(config-if-range)#switchport access vlan 30
   SwServer(config-if-range)#exit
   SwServer(config)#
   ```

1. Aktivasi VTP

   ```console
   SwServer(config)#vtp domain stemsagonet
   SwServer(config)#vtp password rahasia
   SwServer(config)#vtp mode server
   SwServer(config)#
   ```

1. Aktivasi Trunk Link

   ```console
   SwServer(config)#interface fastEthernet 0/24
   SwServer(config-if)#switchport mode trunk
   SwServer(config-if)#exit
   SwServer(config)#
   ```

1. Konfirmasi konfigurasi VLAN

   > show vlan brief

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/02.png){: .normal }

1. Konfirmasi konfigurasi VTP Domain dan VTP Mode

   > show vtp status

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/03.png){: .normal }

1. Konfirmasi konfigurasi VTP Password

   > show vtp password

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/04.png){: .normal }

1. Konfirmasi konfigurasi Trunk Link

   > show interface trunk

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/05.png){: .normal }

#### SwClient

1. Aktivasi Trunk Link

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname SwClient
   SwClient(config)#interface fastEthernet 0/24
   SwClient(config-if)#switchport mode trunk
   SwClient(config-if)#exit
   SwClient(config)#
   ```

1. Aktivasi VTP

   ```console
   SwClient(config)#vtp domain stemsagonet
   SwClient(config)#vtp password rahasia
   SwClient(config)#vtp mode client
   SwClient(config)#
   ```

1. Konfirmasi konfigurasi Trunk Link

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/06.png){: .normal }

1. Konfirmasi konfigurasi VTP Password

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/07.png){: .normal }

1. Konfirmasi konfigurasi VTP Domain dan VTP Mode

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/08.png){: .normal }

1. Konfirmasi konfigurasi VLAN

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/09.png){: .normal }

1. Keanggotaan VLAN

   ```console
   SwClient(config)#interface range fastEthernet 0/6-10
   SwClient(config-if-range)#switchport mode access
   SwClient(config-if-range)#switchport access vlan 20
   SwClient(config-if-range)#exit
   SwClient(config)#interface range fastEthernet 0/11-20
   SwClient(config-if-range)#switchport mode access
   SwClient(config-if-range)#switchport access vlan 30
   SwClient(config-if-range)#exit
   SwClient(config)#
   ```

#### PC0-a, PC0-b

1. Konfigurasi input alamat IP

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/10.png){: .normal }

#### PC1-a, PC1-b

1. Konfigurasi input alamat IP

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/11.png){: .normal }

1. Koneksikan PC dengan Switch

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/12.png){: .normal }

#### PC0-a, PC0-b

1. Konfirmasi konfigurasi IP Address

   > ipconfig

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/13.png){: .normal }

1. Pengujian jaringan VLAN ID yang berbeda pada Switch yang sama

   > ping

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/14.png){: .normal }

1. Pengujian jaringan VLAN ID yang sama pada Switch yang berbeda

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/15.png){: .normal }

1. Pengujian jaringan VLAN ID yang berbeda pada Switch yang berbeda

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/16.png){: .normal }

#### PC1-a, PC1-b

    Lakukan pengujian yang sama seperti langkah sebelumnya, amati hasilnya

### Konfigurasi Ulang

#### Topologi Jaringan dan Spesifikasi

1. Kembangkan jaringan menjadi seperti berikut

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/17.png){: .normal }

   dengan tambahan spesifikasi sebagai berikut

   1. VTP

      1. Domain: stemsagonet
      1. Password: rahasia

   2. VLAN

      1. **VLAN ID: 10, Name: Umum, Interface: Port 1-5**
      2. VLAN ID: 20, Name: Guru, Interface: Port 6-10
      3. VLAN ID: 30, Name: Siswa, Interface: Port 11-20
      4. **VLAN ID: 40, Name: Admin, Interface: Port 21**

   3. Network

      1. Net ID: 10.100.xx.0/24 (xx diganti no presensi)
      2. **Host pada VLAN ID 10: xx.101 s.d. xx.200**
      3. Host pada VLAN ID 20: xx.21 s.d. xx.30
      4. Host pada VLAN ID 30: xx.31 s.d. xx.100
      5. **Host pada VLAN ID 40: xx.201 s.d. xx.254**

#### SwServer

1. Inisiasi VLAN Lainnya

   ```console
   SwServer(config)#vlan 10
   SwServer(config-vlan)#name Umum
   SwServer(config-vlan)#exit
   SwServer(config)#vlan 40
   SwServer(config-vlan)#name Admin
   SwServer(config-vlan)#exit
   SwServer(config)#
   ```

1. Keanggotaan VLAN Lainnya

   ```console
   SwServer(config)#interface range fastEthernet 0/1-5
   SwServer(config-if-range)#switchport mode access
   SwServer(config-if-range)#switchport access vlan 10
   SwServer(config-if-range)#exit
   SwServer(config)#interface fastEthernet 0/21
   SwServer(config-if)#switchport mode access
   SwServer(config-if)#switchport access vlan 40
   SwServer(config-if)#exit
   SwServer(config)#
   ```

1. Aktivasi Trunk Link Lainnya

   ```console
   SwServer(config)#interface range fastEthernet 0/22-23
   SwServer(config-if-range)#switchport mode trunk
   SwServer(config-if-range)#exit
   SwServer(config)#
   ```

#### SwClient

1. Keanggotaan VLAN Lainnya

   ```console
   SwClient(config)#interface range fastEthernet 0/1-5
   SwClient(config-if-range)#switchport mode access
   SwClient(config-if-range)#switchport access vlan 10
   SwClient(config-if-range)#exit
   SwClient(config)#interface fastEthernet 0/21
   SwClient(config-if)#switchport mode access
   SwClient(config-if)#switchport access vlan 40
   SwClient(config-if)#exit
   SwClient(config)#
   ```

#### SwClient2

1. Aktivasi Trunk Link

   ```console
   Switch#configure terminal
   Switch(config)#hostname SwClient2
   SwClient2(config)#interface fastEthernet 0/24
   SwClient2(config-if)#switchport mode trunk
   SwClient2(config-if)#exit
   SwClient2(config)#
   ```

1. Aktivasi VTP

   ```console
   SwClient2(config)#vtp domain stemsagonet
   SwClient2(config)#vtp password rahasia
   SwClient2(config)#vtp mode client
   SwClient2(config)#
   ```

1. Keanggotaan VLAN

   ```console
   SwClient2(config)#interface range fastEthernet 0/1-5
   SwClient2(config-if-range)#switchport mode access
   SwClient2(config-if-range)#switchport access vlan 10
   SwClient2(config-if-range)#exit
   SwClient2(config)#interface range fastEthernet 0/6-10
   SwClient2(config-if-range)#switchport mode access
   SwClient2(config-if-range)#switchport access vlan 20
   SwClient2(config-if-range)#exit
   SwClient2(config)#interface range fastEthernet 0/11-20
   SwClient2(config-if-range)#switchport mode access
   SwClient2(config-if-range)#switchport access vlan 30
   SwClient2(config-if-range)#exit
   SwClient2(config)#interface fastEthernet 0/21
   SwClient2(config-if)#switchport mode access
   SwClient2(config-if)#switchport access vlan 40
   SwClient2(config-if)#exit
   SwClient2(config)#
   ```

#### SwTrans

1. Aktivasi Trunk Link

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname SwTrans
   SwTrans(config)#interface range fastEthernet 0/23-24
   SwTrans(config-if-range)#switchport mode trunk
   SwTrans(config-if-range)#exit
   SwTrans(config)#
   ```

1. Aktivasi VTP

   ```console
   SwTrans(config)#vtp domain stemsagonet
   SwTrans(config)#vtp password rahasia
   SwTrans(config)#vtp mode transparent
   SwTrans(config)#
   ```

#### SwClient3

1. Aktivasi Trunk Link

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname SwClient3
   SwClient3(config)#interface fastEthernet 0/24
   SwClient3(config-if)#switchport mode trunk
   SwClient3(config-if)#exit
   SwClient3(config)#
   ```

1. Aktivasi VTP

   ```console
   SwClient3(config)#vtp domain stemsagonet
   SwClient3(config)#vtp password rahasia
   SwClient3(config)#vtp mode client
   SwClient3(config)#
   ```

### Pengujian

1. Koneksikan PC lainnya dengan Switch dan input IP Address pada PC baru

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/18.png){: .normal }

2. Konfirmasi konfigurasi VTP dan lakukan pengujian pada topologi terkini

   1. Jaringan VLAN ID yang berbeda pada Switch yang sama
   2. Jaringan VLAN ID yang sama pada Switch yang berbeda
   3. Jaringan VLAN ID yang sama pada Switch yang sama
   4. Jaringan VLAN ID yang berbeda pada Switch yang berbeda

3. Amati hasil konfigurasi (SwTrans, SwClient3) lalu tarik kesimpulan

## Berlatih

1. Unduh topologi jaringan VTP dengan mode client-server [di sini](/assets/pkt/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/konfigurasi-vtp-client-server.pkt)
2. Lakukan konfigurasi VLAN sesuai kebutuhan/spesifikasi yang sudah tercantum
3. Lakukan pengamatan dan pengujian pada jaringan yang telah dikonfigurasi
