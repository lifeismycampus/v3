---
layout: post
title: Konfigurasi Routing Statis pada Cisco Packet Tracer
date: 2022-08-14 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing, subnetting]
---

## Ulasan

Routing statis adalah mekanisme routing yang routing table-nya dikonfigurasi oleh network administrator secara manual satu per satu.

Langkah konfigurasi dalam melakukan routing statis adalah sebagai berikut

1. Konfigurasi alamat IP pada interface
1. Aktivasi interface pada perangkat router (secara default status DOWN)
1. Penentuan jalur pada routing statisdengan 3 cara antara lain
   1. Menggunakan exit interface
   2. Menggunakan next-hop IP address
   3. Menggunakan exit interface dan next-hop IP address sekaligus

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                   | Deskripsi                                                                                               |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Router(config)# ip route `destination_network` `subnet_mask` `next_hop_ip` | Menambahkan rute statis ke routing table                                                                |
| Router# show ip route                                                      | Menampilkan informasi routing table                                                                     |
| Router# traceroute `ip_address`                                            | Menampilkan informasi pelacakan jalur paket data yang dikirimkan melalui jaringan dari sumber ke tujuan |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

1. Router

   1. Hostname: R0; Type: 1840,
   2. Hostname: R1; Type: 1840

2. Switch

   1. Hostname: Sw0; Type: 2950-24,
   2. Hostname: Sw1; Type: 2950-24

3. Network

   1. Net ID: 192.168.10.0/26,
   1. Net ID: 192.168.20.0/30,
   1. Net ID: 192.168.30.0/28

#### Tabel Routing

| Router | Destination Network | Subnet Mask | Next Hop     |
| ------ | ------------------- | ----------- | ------------ |
| R0     | 192.168.10.0        | /26         | -            |
| R0     | 192.168.20.0        | /30         | -            |
| R0     | 192.168.30.0        | /28         | 192.168.20.2 |
| R1     | 192.168.10.0        | /26         | 192.168.20.1 |
| R1     | 192.168.20.0        | /30         | -            |
| R1     | 192.168.30.0        | /28         | -            |

#### Tabel Pengalamatan

| Device   | IP Address    | Subnet Mask | Gateway      |
| -------- | ------------- | ----------- | ------------ |
| Fa0/0 R0 | 192.168.20.1  | /30         | -            |
| Fa0/1 R0 | 192.168.10.1  | /26         | -            |
| Fa0/0 R0 | 192.168.20.2  | /30         | -            |
| Fa0/1 R0 | 192.168.30.1  | /28         | -            |
| Fa0 PC1a | 192.168.10.62 | /26         | 192.168.10.1 |
| Fa0 PC1b | 192.168.10.61 | /26         | 192.168.10.1 |
| Fa0 PC2a | DHCP Client   | /28         | 192.168.30.1 |
| Fa0 PC2b | DHCP Client   | /28         | 192.168.30.1 |
| Fa0 PC2c | DHCP Client   | /28         | 192.168.30.1 |
| Fa0 PC2d | DHCP Client   | /28         | 192.168.30.1 |

### Konfigurasi

#### PC1a

1. Konfigurasi alamat ip
   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/02.png){: .normal }

#### PC1b

1. Konfigurasi alamat ip
   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/03.png){: .normal }

#### R0

1. Konfigurasi alamat ip

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R0
   R0(config)#interface fastEthernet 0/1
   R0(config-if)#ip address 192.168.10.1 255.255.255.192
   R0(config-if)#no shutdown
   R0(config-if)#exit
   R0(config)#interface fastEthernet 0/0
   R0(config-if)#ip address 192.168.20.1 255.255.255.252
   R0(config-if)#no shutdown
   R0(config-if)#exit
   ```

1. Konfigurasi routing statis

   ```console
   R0(config)#ip route 192.168.30.0 255.255.255.240 192.168.20.2
   R0(config)#end
   R0#copy running-config startup-config
   R0#
   ```

#### R1

1. Konfigurasi alamat ip

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R1
   R1(config)#interface fastEthernet 0/0
   R1(config-if)#ip address 192.168.20.2 255.255.255.252
   R1(config-if)#no shutdown
   R1(config-if)#exit
   R1(config)#interface fastEthernet 0/1
   R1(config-if)#ip address 192.168.30.1 255.255.255.240
   R1(config-if)#no shutdown
   R1(config-if)#exit
   ```

1. Konfigurasi dhcp server

   ```console
   R1(config)#ip dhcp pool NET-POOL
   R1(dhcp-config)#network 192.168.30.0 255.255.255.240
   R1(dhcp-config)#default-router 192.168.30.1
   R1(dhcp-config)#exit
   R1(config)#ip dhcp excluded-address 192.168.30.1 192.168.30.5
   ```

1. Konfigurasi routing statis

   ```console
   R1(config)#ip route 192.168.10.0 255.255.255.192 192.168.20.1
   R1(config)#end
   R1#copy running-config startup-config
   R1#
   ```

#### PC2a, PC2b, PC2c, PC2d

1. Konfigurasi alamat ip

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/04.png){: .normal }

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/05.png){: .normal }

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/06.png){: .normal }

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/07.png){: .normal }

### Pengujian

#### R0

1. Uji konfigurasi menampilkan routing table

   > show ip route

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/08.png){: .normal }

#### R1

1. Uji konfigurasi

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/09.png){: .normal }

#### PC1a

1. Uji jaringan yang sama

   > ping

   contoh: dari PC1a ke PC2a

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/10.png){: .normal }

#### PC2c

1. Uji jaringan yang berbeda

   > tracert

   contoh: dari PC2c ke PC1b

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/11.png){: .normal }

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi routing statis dengan instruksi sebagai berikut

1. Rancang [topologi jaringan routing statis](/assets/pkt/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/konfigurasi-routing-statis-berlatih.pkt) sebagai berikut.

   ![](/assets/img/2022-08-14-konfigurasi-routing-statis-pada-cisco-packet-tracer/12.png){: .normal }

1. Rancang IP Address table maupun IP Routing table.
1. Konfigurasikan metode routing statis secara lengkap
   1. Set alamat ip untuk semua PC Client
      1. PC-a1, PC-a2,
      2. PC-b1, PC-b1.
   2. Set alamat ip pada router
      1. GedungA,
      2. GedungB, dan
      3. GedungC.
   3. Set dhcp server pada router GedungC untuk jaringan LAN3.
   4. Request alamat ip dhcp client pada
      1. PC-c1,
      2. PC-c2,
      3. PC-c3,
      4. PC-c4,
      5. PC-c5, dan
      6. PC-c6.
   5. Advertise jaringan remote pada router
      1. GedungA,
      2. GedungB, dan
      3. GedungC;
1. Uji hasil konfigurasi
   1. dari PC ke PC dalam jaringan yang sama,
   2. dari PC ke PC dalam jaringan yang berbeda,
   3. dari PC ke Hop dan sebaliknya dalam jaringan yang sama, dan
   4. dari PC ke Hop dan sebaliknya dalam jaringan yang berbeda.
