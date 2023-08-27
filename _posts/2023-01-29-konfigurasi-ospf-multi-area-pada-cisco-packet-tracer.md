---
layout: post
title: Konfigurasi OSPF Multi Area pada Cisco Packet Tracer
date: 2023-01-29 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing, subnetting]
---

## Ulasan

Jika [konfigurasi OSPF single area](/posts/konfigurasi-ospf-single-area-pada-cisco-packet-tracer){:target="\_blank"} secara harafiah hanya mengkonfigurasi topologi jaringan routing mengacu pada sebuah area yaitu area 0 atau backbone area, maka pada praktikum kali ini akan ditampilkan langkah konfigurasi Open Shortest Path First single area menggunakan beberapa area dengan identifier lain seperti area 1, area 2, dan seterusnya.

Perbedaan lain pada praktikum sebelumnya ialah router-id digunakan untuk penentuan DR dan BDR, sedangkan pada praktikum kali ini menggunakan loopback interface.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                    | Deskripsi                                                                                   |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Router(config)#router ospf `process-id`                                     | memasukkan router ke dalam proses OSPF dengan menentukan ID proses OSPF yang akan digunakan |
| Router(config-router)#router-id `router-id`                                 | menentukan ID unik yang akan digunakan oleh router tersebut dalam proses OSPF               |
| Router(config-router)#network `dest-network` `wildcard-mask` area `area-id` | meng-advertise alamat jaringan dalam proses OSPF                                            |
| Router#show ip route                                                        | menampilkan informasi routing table                                                         |
| Router#show ip ospf                                                         | menampilkan informasi process id, lsa authentication                                        |
| Router#show ip ospf interface `interface`                                   | menampilkan informasi cost, hello, dead interval, state, process id                         |
| Router#show ip ospf neighbor                                                | menampilkan router tetangga pada proses ospf                                                |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, Pengujian, Konfigurasi Ulang, dan Pengujian Ulang.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

| Jaringan | Network ID    | Prefix | Wildcard Mask |
| -------- | ------------- | ------ | ------------- |
| WAN1     | 10.1xx.100.0  | /29    | 0.0.0.7       |
| WAN2     | 10.1xx.100.8  | /29    | 0.0.0.7       |
| WAN3     | 10.1xx.100.16 | /29    | 0.0.0.7       |
| LAN1     | 192.1xx.10.0  | /30    | 0.0.0.3       |
| LAN2     | 192.1xx.20.0  | /28    | 0.0.0.15      |
| LAN3     | 172.16.yy.0   | /27    | 0.0.0.31      |
| LAN4     | 172.16.yy.32  | /27    | 0.0.0.31      |
| LAN5     | 172.16.yy.64  | /27    | 0.0.0.31      |
| LAN6     | 172.16.yy.96  | /27    | 0.0.0.31      |
| LAN7     | 172.16.yy.128 | /27    | 0.0.0.31      |

> **Catatan:**
> Jika dikerjakan secara kelompok, masing-masing `xx` dan `yy` diganti dengan nomor presensi anggota.

#### Tabel Pengalamatan

| Device | Hostname   | Interface | IP Address    | Prefix | Gateway       |
| ------ | ---------- | --------- | ------------- | ------ | ------------- |
| Router | Hokkaido   | Lo0       | 1.1.1.1       | /32    | -             |
| Router | Hokkaido   | Se0/0/1   | 10.1xx.100.1  | /29    | -             |
| Router | Hokkaido   | Gig0/0    | 192.1xx.10.1  | /30    | -             |
| Router | Hokkaido   | Gig0/1    | 192.1xx.20.14 | /28    | -             |
| Router | Fukushima  | Lo0       | 2.2.2.2       | /32    | -             |
| Router | Fukushima  | Se0/0/1   | 10.1xx.100.2  | /29    | -             |
| Router | Fukushima  | Se0/0/0   | 10.1xx.100.9  | /29    | -             |
| Router | Fukushima  | Gig0/0    | 172.16.yy.30  | /27    | -             |
| Router | Tokyo      | Lo0       | 3.3.3.3       | /32    | -             |
| Router | Tokyo      | Se0/0/0   | 10.1xx.100.10 | /29    | -             |
| Router | Tokyo      | Gig0/0    | 172.16.yy.33  | /27    | -             |
| Router | Tokyo      | Gig0/1    | 172.16.yy.65  | /27    | -             |
| PC     | FTP Server | Fa0       | 192.1xx.10.2  | /30    | 192.1xx.10.1  |
| PC     | Admin      | Fa0       | DHCP Client   | /28    | 192.1xx.20.14 |
| PC     | Admin2     | Fa0       | DHCP Client   | /28    | 192.1xx.20.14 |
| PC     | Client1    | Fa0       | DHCP Client   | /27    | 172.16.yy.30  |
| PC     | Client2    | Fa0       | DHCP Client   | /27    | 172.16.yy.30  |
| PC     | Client3    | Fa0       | DHCP Client   | /27    | 172.16.yy.33  |
| PC     | Client4    | Fa0       | DHCP Client   | /27    | 172.16.yy.33  |
| PC     | Client5    | Fa0       | DHCP Client   | /27    | 172.16.yy.94  |
| PC     | Client6    | Fa0       | DHCP Client   | /27    | 172.16.yy.94  |

### Konfigurasi

#### Router Hokkaido

1. Konfigurasi alamat ip pada interface

   ```console
   Router(config)#interface loopback 0
   Router(config-if)#ip address 1.1.1.1 255.255.255.255
   Router(config-if)#exit
   Router(config)#interface gigabitEthernet 0/0
   Router(config-if)#ip address 192.198.10.1 255.255.255.252
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface gigabitEthernet 0/1
   Router(config-if)#ip address 192.198.20.14 255.255.255.252
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface serial 0/0/1
   Router(config-if)#ip address 10.198.100.1 255.255.255.248
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#
   ```

2. Konfigurasi dhcp server

   ```console
   Router(config)#ip dhcp pool netadm
   Router(dhcp-config)#network 192.198.20.0 255.255.255.240
   Router(dhcp-config)#default-router 192.198.20.14
   Router(dhcp-config)#exit
   Router(config)#ip dhcp excluded-address 192.198.20.14
   Router(config)#
   ```

3. Konfigurasi routing ospf

   ```console
   Router(config)#router ospf 10
   Router(config-router)#network 1.1.1.1 0.0.0.0 area 0
   Router(config-router)#network 10.198.100.0 0.0.0.7 area 0
   Router(config-router)#network 192.198.10.0 0.0.0.3 area 0
   Router(config-router)#network 192.198.20.0 0.0.0.15 area 0
   Router(config-router)#exit
   Router(config)#
   ```

#### PC FTP Server

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/02.png){: .normal }

2. Konfigurasi ftp server

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/03.png){: .normal }

#### PC Admin, Admin2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/04.png){: .normal }

#### Router Fukushima

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/05.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/06.png){: .normal }

3. Konfigurasi routing ospf

   ```console
   Router(config)#router ospf 20
   Router(config-router)#network 10.198.100.0 0.0.0.7 area 0
   Router(config-router)#network 2.2.2.2 0.0.0.0 area 0
   Router(config-router)#network 10.198.100.8 0.0.0.7 area 1
   Router(config-router)#network 172.16.99.0 0.0.0.31 area 1
   Router(config-router)#exit
   Router(config)#
   ```

#### PC Client1, Client2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/07.png){: .normal }

#### Router Tokyo

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/08.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/09.png){: .normal }

3. Konfigurasi routing ospf

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/10.png){: .normal }

#### PC Client3, Client4

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/11.png){: .normal }

#### PC Client5, Client6

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/12.png){: .normal }

### Pengujian

1. Tampilkan routing table masing-masing router

   1. Router Hokkaido

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/13.png){: .normal }

      > **Catatan:**
      > Kode `O IA` merupakan indikator jaringan dari router lain yang mengaktifkan protocol routing OSPF namun dengan area berbeda (inter area).

   2. Router Fukushima

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/14.png){: .normal }

   3. Router Tokyo

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/15.png){: .normal }

2. Uji jaringan dengan Add Simple PDU atau perintah `ping` antar PC maupun router

   1. PC Admin ke PC Client1

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/16.png){: .normal }

   2. PC Admin2 ke PC Client3

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/17.png){: .normal }

   3. PC Client4 ke PC Client5

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/18.png){: .normal }

   4. PC Client6 ke PC Server

      ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/19.png){: .normal }

3. Kirim file menggunakan protocol FTP

   1. PC Admin

      1. Buka Text Editor, tulis dan simpan sebagai tugas.txt

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/20.png){: .normal }

      1. Buka Command Prompt, akses ftp server menggunakan username ftpadmin

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/21.png){: .normal }

      1. Unggah tugas.txt ke ftp server

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/22.png){: .normal }

   2. PC Client3

      1. Buka Command Prompt, akses ftp server menggunakan username ftpuser

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/23.png){: .normal }

      2. Unduh tugas.txt dari ftp server

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/24.png){: .normal }

      3. Buka Text Editor, buka tugas.txt

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/25.png){: .normal }

      4. Edit dan simpan kembali tugas.txt

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/26.png){: .normal }

      5. Unggah kembali tugas.txt ke ftp server

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/27.png){: .normal }

   3. PC Client6

      1. Seperti PC Client3 menggunakan username ftpuser, unduh dan buka tugas.txt

         ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/28.png){: .normal }

### Konfigurasi Ulang

1. Tambahkan sebuah router baru dengan area id 2, konfigurasi dengan routing protocol OSPF

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/29.png){: .normal }

1. Lakukan langkah konfigurasi agar akses pada ftp server bisa menggunakan domain `ftp.dominio.net`

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/30.png){: .normal }

### Pengujian Ulang

Dengan konsep pengiriman file txt juga, lakukan langkah yang sama dengan urutan PC Client nomor dibalik mulai dari

1. PC-Client6 ke
2. PC-Client3 lalu ke
3. PC-Admin

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi multiarea OSPF dengan instruksi sebagai berikut

1. Rancang topologi jaringan routing OSPF sebagai berikut

   ![](/assets/img/2023-01-29-konfigurasi-ospf-multi-area-pada-cisco-packet-tracer/31.png){: .normal }

   dengan spesifikasi sebagai berikut

   | Routing Protocol  | OSPF                               |
   | ----------------- | ---------------------------------- |
   | Services          | DNS Server, Web Server, FTP Server |
   | Web Server Domain | www.hopper.org                     |
   | FTP Server Domain | ftp.hopper.org                     |

   serta jaringan subnetting sebagai berikut

   | Subnet | Network ID       |
   | ------ | ---------------- |
   | WAN1   | 10.1.1xx.0/29    |
   | WAN2   | 10.1.1xx.8/29    |
   | WAN3   | 10.1.1xx.16/29   |
   | LAN1   | 192.1xx.1.0/27   |
   | LAN2   | 172.16.2xx.0/30  |
   | LAN3   | 172.16.2xx.4/30  |
   | LAN4   | 192.1xx.1.32/27  |
   | LAN5   | 172.16.2xx.8/30  |
   | LAN6   | 192.1xx.1.64/27  |
   | LAN7   | 172.16.2xx.12/30 |
   | LAN8   | 172.16.2xx.16/30 |
   | LAN9   | 172.16.2xx.20/30 |
   | LAN10  | 192.1xx.1.96/27  |

   dengan kode `xx` merupakan nomor presensi masing-masing

2. Setiap Router dapat mencetak informasi routing table seluruh jaringan.
3. Setiap PC dapat saling terhubung melalui jaringan OSPF.
4. Setiap Router dan PC dapat mengenali dan mengakses domain dari web server,

   jika diakses via web browser maka header berisi

   `Welcome to Hopper`

5. Setiap Router dan PC dapat mengenali dan mengakses domain dari ftp server dengan user sebagai berikut

   | Username      | Password | Permission |
   | ------------- | -------- | ---------- |
   | Administrator | !Hiden1  | RWDNL      |
   | Client1       | !Woz1    | R          |
   | Client2       | !Izu1    | R          |
   | Client3       | !Wil1    | R          |
