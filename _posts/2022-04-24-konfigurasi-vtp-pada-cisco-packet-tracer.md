---
layout: post
title: Konfigurasi VTP pada Cisco Packet Tracer
date: 2022-04-24 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, vlan]
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

Perintah yang digunakan pada praktikum kali ini yaitu:

1. Switch(config)#vtp domain 'name'

   Perintah ini digunakan untuk mengatur domain VTP (VLAN Trunking Protocol) pada switch. Domain VTP adalah grup switch yang berbagi informasi tentang VLAN. Anda harus mengganti 'name' dengan nama domain yang ingin Anda atur.

1. Switch(config)#vtp password 'word'

   Perintah ini digunakan untuk mengatur kata sandi VTP pada switch. Kata sandi VTP digunakan untuk memberikan keamanan dalam mengkonfigurasi VLAN. Anda harus mengganti 'word' dengan kata sandi yang aman.

1. Switch(config)#vtp mode 'mode'

   Perintah ini digunakan untuk mengatur mode operasi VTP pada switch. Mode ini dapat berupa "server," "client," atau "transparent." Mode "server" memungkinkan switch untuk mengkonfigurasi VLAN, "client" hanya menerima konfigurasi VLAN dari server, dan "transparent" tidak berpartisipasi dalam penyebaran informasi VTP.

1. Switch(config-if)#switchport mode trunk

   Perintah ini digunakan pada antarmuka (interface) switch untuk mengatur mode antarmuka menjadi mode trunk. Mode trunk digunakan untuk mengizinkan lalu lintas VLAN melewati antarmuka tersebut.

1. Switch#show vtp status

   Perintah ini digunakan untuk menampilkan status VTP pada switch. Ini akan menampilkan informasi tentang domain VTP, mode operasi, revisi, dan lainnya.

1. Switch#show vtp password

   Perintah ini digunakan untuk menampilkan kata sandi VTP yang telah diatur pada switch. Ini membantu Anda memverifikasi kata sandi yang digunakan dalam konfigurasi VTP.

1. Switch#show interface trunk

   Perintah ini digunakan untuk menampilkan informasi tentang antarmuka trunk pada switch. Ini akan menampilkan daftar antarmuka yang diatur sebagai trunk, serta informasi tentang VLAN yang diizinkan melewati antarmuka tersebut.

1. Switch#show vtp counter

   Perintah ini digunakan untuk menampilkan informasi tentang hitungan perubahan yang telah terjadi dalam konfigurasi VTP pada switch. Ini dapat membantu Anda melihat apakah ada perubahan dalam pengaturan VLAN.

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa tahapan yaitu

1. Persiapan
2. Konfigurasi dan Konfirmasi
3. Konfigurasi Ulang
4. Pengujian
5. Berlatih

### 1. Persiapan

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

   1. Net ID: 10.100.xx.0/24
   2. Host pada VLAN ID 20: xx.21 s.d. xx.30
   3. Host pada VLAN ID 30: xx.31 s.d. xx.100

> Kode `xx` diganti dengan nomor presensi masing-masing, pada contoh ini akan menggunakan `99`.

#### Tabel pengalamatan

| Device   | Interface | VLAN ID | IP Address   | Subnet Mask   |
| -------- | --------- | ------- | ------------ | ------------- |
| PC0-a    | Fa0       | 20      | 10.100.xx.21 | 255.255.255.0 |
| PC0-b    | Fa1       | 30      | 10.100.xx.31 | 255.255.255.0 |
| PC1-a    | Fa2       | 20      | 10.100.xx.22 | 255.255.255.0 |
| PC1-b    | Fa3       | 30      | 10.100.xx.32 | 255.255.255.0 |
| SwServer | Fa0/24    | 20, 30  |              |               |
| SwClient | Fa0/24    | 20, 30  |              |               |

### 2. Konfigurasi dan Konfirmasi

#### Langkah ke-1: [SwServer] aktivasi VLAN baru

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

#### Langkah ke-2: [SwServer] atur port sebagai anggota VLAN

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

#### Langkah ke-3: [SwServer] aktivasi VTP

```console
SwServer(config)#vtp domain stemsagonet
SwServer(config)#vtp password rahasia
SwServer(config)#vtp mode server
SwServer(config)#
```

#### Langkah ke-4: [SwServer] aktivasi trunk link penghubung antar Switch

```console
SwServer(config)#interface fastEthernet 0/24
SwServer(config-if)#switchport mode trunk
SwServer(config-if)#exit
SwServer(config)#
```

#### Langkah ke-5: [SwServer] konfirmasi VLAN aktif

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/02.png){: .normal }

#### Langkah ke-6: [SwServer] konfirmasi VTP aktif

Informasi jumlah VLAN aktif, VTP domain, dan VTP mode.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/03.png){: .normal }

Informasi VTP password.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/04.png){: .normal }

#### Langkah ke-7: [SwServer] konfirmasi trunk link

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/05.png){: .normal }

#### Langkah ke-8: [SwClient] aktivasi VLAN baru

```console
Switch>enable
Switch#configure terminal
Switch(config)#hostname SwClient
SwClient(config)#interface fastEthernet 0/24
SwClient(config-if)#switchport mode trunk
SwClient(config-if)#exit
SwClient(config)#
```

#### Langkah ke-9: [SwClient] aktivasi VTP

```console
SwClient(config)#vtp domain stemsagonet
SwClient(config)#vtp password rahasia
SwClient(config)#vtp mode client
SwClient(config)#
```

#### Langkah ke-10: [SwClient] konfirmasi trunk link

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/06.png){: .normal }

#### Langkah ke-11: [SwClient] konfirmasi VTP aktif

Konfirmasi VTP password.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/07.png){: .normal }

Konfirmasi jumlah VLAN aktif, VTP domain, dan VTP mode.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/08.png){: .normal }

Konfirmasi sinkronisasi VLAN aktif yang diterima dari vtp server.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/09.png){: .normal }

#### Langkah ke-12: [SwClient] atur port sebagai anggota VLAN

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

#### Langkah ke-13: [PC] atur alamat IP

PC0-a, PC0-b

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/10.png){: .normal }

PC1-a, PC1-b

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/11.png){: .normal }

#### Langkah ke-14: hubungkan dengan Switch

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/12.png){: .normal }

#### Langkah ke-15: [PC] konfirmasi alamat IP

Informasi alamat IP.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/13.png){: .normal }

Uji jaringan VLAN ID yang berbeda pada Switch yang sama.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/14.png){: .normal }

Uji jaringan VLAN ID yang sama pada Switch yang berbeda.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/15.png){: .normal }

Uji jaringan VLAN ID yang berbeda pada Switch yang berbeda.

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/16.png){: .normal }

### 3. Konfigurasi Ulang

#### Topologi Jaringan dan Spesifikasi

Kembangkan jaringan menjadi seperti berikut

![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/17.png){: .normal }

#### Spesifikasi

Dengan topologi jaringan yang baru, maka spesifikasi menjadi sebagai berikut

1. VTP

   1. Domain: stemsagonet
   2. Password: rahasia

2. VLAN

   1. **VLAN ID: 10, Name: Umum, Interface: Port 1-5**
   2. VLAN ID: 20, Name: Guru, Interface: Port 6-10
   3. VLAN ID: 30, Name: Siswa, Interface: Port 11-20
   4. **VLAN ID: 40, Name: Admin, Interface: Port 21**

3. Network

   1. Net ID: 10.100.xx.0/24
   2. **Host pada VLAN ID 10: xx.101 s.d. xx.200**
   3. Host pada VLAN ID 20: xx.21 s.d. xx.30
   4. Host pada VLAN ID 30: xx.31 s.d. xx.100
   5. **Host pada VLAN ID 40: xx.201 s.d. xx.254**

#### Langkah ke-1: [SwServer] aktivasi VLAN lainnya

```console
SwServer(config)#vlan 10
SwServer(config-vlan)#name Umum
SwServer(config-vlan)#exit
SwServer(config)#vlan 40
SwServer(config-vlan)#name Admin
SwServer(config-vlan)#exit
SwServer(config)#
```

#### Langkah ke-2: [SwServer] atur port sebagai anggota VLAN lainnya

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

#### Langkah ke-3: [SwClient] aktivasi trunk link

```console
SwServer(config)#interface range fastEthernet 0/22-23
SwServer(config-if-range)#switchport mode trunk
SwServer(config-if-range)#exit
SwServer(config)#
```

#### Langkah ke-4: [SwClient] atur port sebagai anggota VLAN hasil sinkronisasi

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

#### Langkah ke-5: [SwClient2] aktivasi trunk link

```console
Switch#configure terminal
Switch(config)#hostname SwClient2
SwClient2(config)#interface fastEthernet 0/24
SwClient2(config-if)#switchport mode trunk
SwClient2(config-if)#exit
SwClient2(config)#
```

#### Langkah ke-6: [SwClient2] aktivasi VTP

```console
SwClient2(config)#vtp domain stemsagonet
SwClient2(config)#vtp password rahasia
SwClient2(config)#vtp mode client
SwClient2(config)#
```

#### Langkah ke-7: [SwClient2] atur port sebagai anggota VLAN hasil sinkronisasi

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

#### Langkah ke-8: [SwTrans] aktivasi trunk link

```console
Switch>enable
Switch#configure terminal
Switch(config)#hostname SwTrans
SwTrans(config)#interface range fastEthernet 0/23-24
SwTrans(config-if-range)#switchport mode trunk
SwTrans(config-if-range)#exit
SwTrans(config)#
```

#### Langkah ke-9: [SwTrans] aktivasi VTP

```console
SwTrans(config)#vtp domain stemsagonet
SwTrans(config)#vtp password rahasia
SwTrans(config)#vtp mode transparent
SwTrans(config)#
```

#### Langkah ke-10: [SwClient3] aktivasi trunk link

```console
Switch>enable
Switch#configure terminal
Switch(config)#hostname SwClient3
SwClient3(config)#interface fastEthernet 0/24
SwClient3(config-if)#switchport mode trunk
SwClient3(config-if)#exit
SwClient3(config)#
```

#### Langkah ke-11: [SwClient3] aktivasi VTP

```console
SwClient3(config)#vtp domain stemsagonet
SwClient3(config)#vtp password rahasia
SwClient3(config)#vtp mode client
SwClient3(config)#
```

### 4. Pengujian

1. Koneksikan PC lainnya dengan Switch

   ![](/assets/img/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/18.png){: .normal }

2. Input alamat IP Address pada PC baru
3. Konfirmasi konfigurasi VTP dan lakukan pengujian pada topologi terkini

   1. Jaringan VLAN ID yang berbeda pada Switch yang sama
   2. Jaringan VLAN ID yang sama pada Switch yang berbeda
   3. Jaringan VLAN ID yang sama pada Switch yang sama
   4. Jaringan VLAN ID yang berbeda pada Switch yang berbeda

4. Amati hasil konfigurasi (SwTrans, SwClient3) lalu tarik kesimpulan

### 5. Berlatih

1. Unduh topologi jaringan VTP dengan mode client-server [di sini](/assets/pkt/2022-04-24-konfigurasi-vtp-pada-cisco-packet-tracer/konfigurasi-vtp-client-server.pkt)
2. Lakukan konfigurasi VLAN sesuai kebutuhan/spesifikasi yang sudah tercantum
3. Lakukan pengamatan dan pengujian pada jaringan yang telah dikonfigurasi
