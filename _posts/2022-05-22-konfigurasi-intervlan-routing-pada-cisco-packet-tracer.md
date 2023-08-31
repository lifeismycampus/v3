---
layout: post
title: Konfigurasi InterVLAN Routing pada Cisco Packet Tracer
date: 2022-05-22 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, routing, vlan]
---

## Ulasan

Teknik konfigurasi InterVLAN Routing memungkinkan untuk menghubungkan dua buah VLAN atau lebih yang berbeda VLAN ID.

Terdapat beberapa teknik konfigurasi InterVLAN Routing yang bisa dilakukan, baik menggunakan perangkat Layer 3 Switch maupun menggunakan perangkat Router.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                | Deskripsi                                                                                           |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Switch(config)#interface vlan `vlan-id`                 | Mengaktiftan interface VLAN sebagai interface                                                       |
| Switch(config-if)#ip address `ip-address` `subnet-mask` | Memberi alamat interface VLAN                                                                       |
| Switch(config)#ip routing                               | Mengaktifkan protokol routing                                                                       |
| Router(config-if)#no shutdown                           | Merubah status interface dari down ke up                                                            |
| Router(config)#interface `port-type` `port-sub-num`     | Mengaktiftan subinterface                                                                           |
| Router(config-subif)#encapsulation dot1q `vlan-id`      | Mengaktifkan metode enkapsulasi data untuk subinterface yang akan diteruskan ke suatu jaringan VLAN |

## Langkah Kerja

Pada praktikum kali ini untuk masing-masing metode akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, Pengujian.

## Metode Layer 3 Switch

### Persiapan

#### Topologi Jaringan

![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

1. Switch
   1. Type: 3560-24PS
   2. Hostname: InterVLAN1
2. VLAN
   1. VLAN ID: 100; Name:Private; Member: Port 1-10
   2. VLAN ID: 200; Name:Public; Member: Port 11-20
3. Network ID
   1. VLAN ID 100: 10.xx.100.0/24
   2. VLAN ID 200: 10.xx.200.0/24
   3. xx: nomor presensi masing-masing

#### Tabel Pengalamatan

| Device     | Interface | VLAN ID | IP Address    | Subnet Mask   | Gateway     |
| ---------- | --------- | ------- | ------------- | ------------- | ----------- |
| PC1a       | Fa0       | 100     | 10.xx.100.254 | 255.255.255.0 | 10.xx.100.1 |
| PC1b       | Fa0       | 100     | 10.xx.100.253 | 255.255.255.0 | 10.xx.100.1 |
| PC2a       | Fa0       | 200     | 10.xx.200.254 | 255.255.255.0 | 10.xx.200.1 |
| PC2b       | Fa0       | 200     | 10.xx.200.253 | 255.255.255.0 | 10.xx.200.1 |
| InterVLAN1 | VLAN      | 100     | 10.xx.100.1   | 255.255.255.0 |             |
| InterVLAN1 | VLAN      | 200     | 10.xx.200.1   | 255.255.255.0 |             |

### Konfigurasi

#### Multilayers Switch: InterVLAN1

1. Inisialisasi VLAN

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname InterVLAN1
   InterVLAN1(config)#
   InterVLAN1(config)#vlan 100
   InterVLAN1(config-vlan)#name private
   InterVLAN1(config-vlan)#exit
   InterVLAN1(config)#vlan 200
   InterVLAN1(config-vlan)#name public
   InterVLAN1(config-vlan)#exit
   InterVLAN1(config)#
   ```

1. Atur Keanggotaan VLAN

   ```console
   InterVLAN1(config)#interface range fastEthernet 0/1-10
   InterVLAN1(config-if-range)#switchport mode access
   InterVLAN1(config-if-range)#switchport access vlan 100
   InterVLAN1(config-if-range)#exit
   InterVLAN1(config)#interface range fastEthernet 0/11-20
   InterVLAN1(config-if-range)#switchport mode access
   InterVLAN1(config-if-range)#switchport access vlan 200
   InterVLAN1(config-if-range)#exit
   InterVLAN1(config)#
   ```

1. Input IP Address pada VLAN

   ```console
   InterVLAN1(config)#interface vlan 100
   InterVLAN1(config-if)#ip address 10.99.100.1 255.255.255.0
   InterVLAN1(config-if)#exit
   InterVLAN1(config)#interface vlan 200
   InterVLAN1(config-if)#ip address 10.99.200.1 255.255.255.0
   InterVLAN1(config-if)#exit
   InterVLAN1(config)#
   ```

1. Routing pada VLAN

   ```console
   InterVLAN1(config)#ip routing
   InterVLAN1(config)#exit
   InterVLAN1#copy running-config startup-config
   InterVLAN1#
   ```

1. Konfirmasi Konfigurasi VLAN

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/02.png){: .normal }

#### PC

1. Konfirmasi alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/03.png){: .normal }

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/04.png){: .normal }

#### PC

1. Konfirmasi alamat IP

   `ipconfig`

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/05.png){: .normal }

### Pengujian

1. Uji jaringan VLAN ID sama

   `ping`

   Contoh: PC1a ke PC1b

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/06.png){: .normal }

2. Uji jaringan VLAN ID berbeda

   Contoh: PC1b ke PC2a

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/07.png){: .normal }

## Metode Interface Router Berbeda-beda untuk Setiap VLAN ID

### Persiapan

#### Topologi Jaringan

![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/08.png){: .normal }

#### Spesifikasi

1. Router
   1. Type: 1841
   2. Hostname: InterVLAN2
2. Switch
   1. Type: 2950-24
   2. Hostname: Sw2
3. VLAN
   1. VLAN ID: 30; Name:Home; Member: Port 1-15, 23
   2. VLAN ID: 40; Name:Work; Member: Port 16-22, 24
4. Network ID
   1. VLAN ID 30: 172.xx.30.0/24
   2. VLAN ID 40: 172.xx.40.0/24
   3. xx: nomor presensi masing-masing

#### Tabel Pengalamatan

| Device     | Interface | VLAN ID | IP Address    | Subnet Mask   | Gateway     |
| ---------- | --------- | ------- | ------------- | ------------- | ----------- |
| PC3a       | Fa0       | 30      | 172.xx.30.254 | 255.255.255.0 | 172.xx.30.1 |
| PC3b       | Fa1       | 30      | 172.xx.30.253 | 255.255.255.0 | 172.xx.30.1 |
| PC4a       | Fa2       | 40      | 172.xx.40.254 | 255.255.255.0 | 172.xx.40.1 |
| PC4b       | Fa3       | 40      | 172.xx.40.253 | 255.255.255.0 | 172.xx.40.1 |
| InterVLAN2 | Fa0/0     | 30      | 172.xx.30.1   | 255.255.255.0 |             |
| InterVLAN2 | Fa0/0     | 40      | 172.xx.40.1   | 255.255.255.0 |             |

### Konfigurasi

#### Switch: Sw2

1. Inisialisasi VLAN

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname Sw2
   Sw2(config)#vlan 30
   Sw2(config-vlan)#name Home
   Sw2(config-vlan)#exit
   Sw2(config)#vlan 40
   Sw2(config-vlan)#name Work
   Sw2(config-vlan)#exit
   Sw2(config)#
   ```

1. Atur Keanggotaan VLAN

   ```console
   Sw2(config)#interface range fastEthernet 0/1-15, fastEthernet 0/23
   Sw2(config-if-range)#switchport mode access
   Sw2(config-if-range)#switchport access vlan 30
   Sw2(config-if-range)#exit
   Sw2(config)#interface range fastEthernet 0/16-22, fastEthernet 0/24
   Sw2(config-if-range)#switchport mode access
   Sw2(config-if-range)#switchport access vlan 40
   Sw2(config-if-range)#exit
   Sw2(config)#end
   Sw2#copy running-config startup-config
   Sw2#
   ```

1. Konfirmasi Konfigurasi VLAN

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/09.png){: .normal }

#### Router: InterVLAN2

> **Catatan:**
> Jawab dengan **no** jika muncul prompt **Continue with configuration dialog? [yes/no]:** saat membuka CLI pada perangkat Router pertama kali.

1. Konfigurasi Alamat IP

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname InterVLAN2
   InterVLAN2(config)#interface fastEthernet 0/0
   InterVLAN2(config-if)#ip address 172.99.30.1 255.255.255.0
   InterVLAN2(config-if)#no shutdown
   InterVLAN2(config-if)#exit
   InterVLAN2(config)#interface fastEthernet 0/1
   InterVLAN2(config-if)#ip address 172.99.40.1 255.255.255.0
   InterVLAN2(config-if)#no shutdown
   InterVLAN2(config-if)#exit
   InterVLAN2(config)#end
   InterVLAN2#copy running-config startup-config
   InterVLAN2#
   ```

> **Catatan:**
> Berbeda dengan Switch yang interfacenya otomatis akan hidup (indikator langsung hijau) ketika suatu kabel dipasang, interface pada Router harus dihidupkan secara manual sehingga setiap mengonfigurasi interface harus mengeksekusi perintah **no shutdown**.

1. Konfirmasi Alamat IP

   `show running-config`

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/10.png){: .normal }

#### PC

1. Konfigurasi Alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/11.png){: .normal }

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/12.png){: .normal }

#### PC

1. Konfirmasi Alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/13.png){: .normal }

### Pengujian

1. Uji jaringan VLAN ID sama

   Contoh: PC3a ke PC3b

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/14.png){: .normal }

1. Uji jaringan VLAN ID berbeda

   Contoh: PC3b ke PC4a

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/15.png){: .normal }

1. Melacak pengiriman paket pada perangkat Router dari sumber ke tujuan

   `traceroute`

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/16.png){: .normal }

1. Melacak pengiriman paket dari sumber ke tujuan pada perangkat PC

   `tracert`

   Contoh: PC3a ke PC4b

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/17.png){: .normal }

   > **Catatan:**
   > Paket akan dilewatkan ke alamat gateway jaringan sumber sebelum sampai ke alamat jaringan tujuan.

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/18.png){: .normal }

## Metode Router-on-a-Stick (ROAS)

### Persiapan

#### Topologi Jaringan

![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/19.png){: .normal }

#### Spesifikasi

1. Router
   1. Type: 1841
   2. Hostname: InterVLAN3
2. Switch
   1. Type: 2950-24
   2. Hostname: Sw3
3. VLAN
   1. VLAN ID: 111; Name: eng_softw; Member: Port 1-6
   2. VLAN ID: 222; Name: eng_mecha; Member: Port 7-12
   3. VLAN ID: 333; Name: eng_elect; Member: Port 13-18
4. Network ID
   1. VLAN ID 111: 10.11.1xx.0/24
   2. VLAN ID 222: 10.22.1xx.0/24
   3. VLAN ID 333: 10.33.1xx.0/24
   4. xx: nomor presensi masing-masing

#### Tabel Pengalamatan

| Device     | Interface | VLAN ID | IP Address    | Subnet Mask   | Gateway     |
| ---------- | --------- | ------- | ------------- | ------------- | ----------- |
| PC5a       | Fa0       | 111     | 10.11.1xx.254 | 255.255.255.0 | 10.11.1xx.1 |
| PC5b       | Fa0       | 111     | 10.11.1xx.253 | 255.255.255.0 | 10.11.1xx.1 |
| PC6        | Fa0       | 222     | 10.22.1xx.254 | 255.255.255.0 | 10.22.1xx.1 |
| PC7        | Fa0       | 333     | 10.33.1xx.254 | 255.255.255.0 | 10.22.1xx.1 |
| InterVLAN3 | Fa0/0.111 | 111     | 10.11.1xx.1   | 255.255.255.0 |             |
| InterVLAN3 | Fa0/0.222 | 222     | 10.22.1xx.1   | 255.255.255.0 |             |
| InterVLAN3 | Fa0/0.333 | 333     | 10.33.1xx.1   | 255.255.255.0 |             |

### Konfigurasi

#### Sw3

1. Inisialisasi VLAN

   ```console
   Switch>enable
   Switch#configure terminal
   Switch(config)#hostname Sw3
   Sw3(config)#vlan 111
   Sw3(config-vlan)#name eng_softw
   Sw3(config-vlan)#exit
   Sw3(config)#vlan 222
   Sw3(config-vlan)#name eng_mecha
   Sw3(config-vlan)#exit
   Sw3(config)#vlan 333
   Sw3(config-vlan)#name eng_elect
   Sw3(config-vlan)#exit
   Sw3(config)#
   ```

1. Atur Keanggotaan VLAN

   ```console
   Sw3(config)#interface range fastEthernet 0/1-6
   Sw3(config-if-range)#switchport mode access
   Sw3(config-if-range)#switchport access vlan 111
   Sw3(config-if-range)#exit
   Sw3(config)#interface range fastEthernet 0/7-12
   Sw3(config-if-range)#switchport mode access
   Sw3(config-if-range)#switchport access vlan 222
   Sw3(config-if-range)#exit
   Sw3(config)#interface range fastEthernet 0/13-18
   Sw3(config-if-range)#switchport mode access
   Sw3(config-if-range)#switchport access vlan 333
   Sw3(config-if-range)#exit
   Sw3(config)#
   ```

1. Atur Interface Trunk Link

   ```console
   Sw3(config)#interface fastEthernet 0/24
   Sw3(config-if)#switchport mode trunk
   Sw3(config-if)#exit
   Sw3(config)#end
   Sw3#copy running-config startup-config
   Sw3#
   ```

1. Konfirmasi Konfigurasi VLAN

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/20.png){: .normal }

#### Router: InterVLAN3

1. Aktivasi interface ke Switch

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname InterVLAN3
   InterVLAN3(config)#interface fastEthernet 0/0
   InterVLAN3(config-if)#no shutdown
   InterVLAN3(config-if)#exit
   InterVLAN3(config)#
   ```

1. Konfigurasi Alamat IP

   ```console
   InterVLAN3(config)#interface fastEthernet 0/0.111
   InterVLAN3(config-subif)#encapsulation dot1q 111
   InterVLAN3(config-subif)#ip address 10.11.199.1 255.255.255.0
   InterVLAN3(config-subif)#exit
   InterVLAN3(config)#interface fastEthernet 0/0.222
   InterVLAN3(config-subif)#encapsulation dot1q 222
   InterVLAN3(config-subif)#ip address 10.22.199.1 255.255.255.0
   InterVLAN3(config-subif)#exit
   InterVLAN3(config)#interface fastEthernet 0/0.333
   InterVLAN3(config-subif)#encapsulation dot1q 333
   InterVLAN3(config-subif)#ip address 10.33.199.1 255.255.255.0
   InterVLAN3(config-subif)#exit
   InterVLAN3(config)#end
   InterVLAN3#copy running-config startup-config
   InterVLAN3#
   ```

   > **Catatan:**
   > Disebut dengan istilah Router on A Stick (ROAS) karena proses routing dilakukan dengan menghubungkan Router ke Switch secara fisik dengan menggunakan sebuah kabel, sedangkan interface dikonfigurasi secara logical menjadi sub-sub interface (contoh fa 0/0.xx) atau interface virtual.

1. Konfirmasi Alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/21.png){: .normal }

#### PC

1. Konfigurasi Alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/22.png){: .normal }

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/23.png){: .normal }

1. Konfirmasi Alamat IP

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/24.png){: .normal }

### Pengujian

1. Uji jaringan VLAN ID sama

   Contoh: PC5a ke PC5b

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/25.png){: .normal }

1. Uji jaringan VLAN ID berbeda

   Contoh: PC6 ke PC7

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/26.png){: .normal }

1. Melacak pengiriman paket pada perangkat Router dari sumber ke tujuan

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/27.png){: .normal }

1. Melacak pengiriman paket pada perangkat PC dari sumber ke tujuan

   Contoh: PC5a ke PC7

   ![](/assets/img/2022-05-22-konfigurasi-intervlan-routing-pada-cisco-packet-tracer/28.png){: .normal }
