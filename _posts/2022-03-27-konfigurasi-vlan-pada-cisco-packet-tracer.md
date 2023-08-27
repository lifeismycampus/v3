---
layout: post
title: Konfigurasi VLAN pada Cisco Packet Tracer
date: 2022-03-27 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, switching, vlan]
---

## Ulasan

Virtual Local Area Network (VLAN) adalah teknologi jaringan yang memungkinkan untuk membagi jaringan fisik menjadi beberapa jaringan virtual yang terpisah.

Setiap VLAN dapat berfungsi sebagai jaringan terpisah dengan alamat IP yang unik dan konfigurasi jaringan yang berbeda.

Ini memungkinkan administrator jaringan untuk mengelompokkan perangkat jaringan berdasarkan fungsionalitas, keamanan, atau organisasi, sehingga mempermudah pemeliharaan dan meningkatkan keamanan jaringan.

VLAN juga mempermudah manajemen jaringan dan dapat mengurangi congestions pada jaringan dengan membatasi lalu lintas jaringan yang tidak diinginkan.

Pada praktikum kali ini akan ditampilkan langkah konfigurasi VLAN yang dikelompokkan berdasarkan interface pada switch.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                    | Deskripsi                                                 |
| ----------------------------------------------------------- | --------------------------------------------------------- |
| Switch#show running-config                                  | Menampilkan konfigurasi yang sedang berjalan              |
| Switch#show vlan brief                                      | Menampilkan tabel VLAN                                    |
| Switch#copy running-config startup-config                   | Menyimpan konfigurasi berjalan ke konfigurasi startup     |
| Switch#configure terminal                                   | Merubah Privileged EXEC menjadi Global Configuration Mode |
| Switch(config)#vlan `vlan-id`                               | Mengaktifkan VLAN ID                                      |
| Switch(config-vlan)#name `vlan-name`                        | Memberi nama pada VLAN ID aktif                           |
| Switch(config)#interface `port-type` `port-num`             | Mengaktiftan suatu interface                              |
| Switch(config)#interface range `port-type` `port-num`-`num` | Mengaktifkan interface secara serentak                    |
| Switch(config-if)#switchport mode access                    | Menjadikan interface aktif sebagai access link            |
| Switch(config-if)#switchport access vlan `vlan-id`          | Menjadikan interface aktif sebagai anggota VLAN ID        |
| Switch(config-if)#exit                                      | Keluar ke mode sebelumnya                                 |
| Switch(config-if)#end                                       | Keluar ke Privileged EXEC                                 |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi dan Konfirmasi.

### Persiapan

#### Topologi jaringan

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

1. VLAN
   1. ID: 200
   2. Name: Private
   3. Membership: 2, 11 s.d. 20
2. IP Address
   1. PC1a: 10.100.1.11/24
   2. PC2a: 10.100.1.21/24
   3. PC3a: 10.100.1.31/24

#### Tabel pengalamatan

| Device  | Interface                 | VLAN ID | IP Address  | Subnet Mask   |
| ------- | ------------------------- | ------- | ----------- | ------------- |
| PC1a    | Fa0                       | 1       | 10.100.1.11 | 255.255.255.0 |
| PC2a    | Fa1                       | 200     | 10.100.1.21 | 255.255.255.0 |
| PC3a    | Fa2                       | 1       | 10.100.1.31 | 255.255.255.0 |
| Switch1 | Fa0/1                     | 1       | -           | -             |
| Switch1 | Fa0/2                     | 200     | -           | -             |
| Switch1 | Fa0/3                     | 1       | -           | -             |
| Switch1 | Fa0/11, Fa0/12, …, Fa0/20 | 200     | -           | -             |
| Switch1 | Lainnya                   | 1       | -           | -             |

### Konfigurasi dan Konfirmasi

#### PC1a

1. Konfigurasi alamat IP

   > tab Desktop -> IP Configuration

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/02.png){: .normal }

#### PC2a

1. Konfigurasi alamat IP

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/03.png){: .normal }

#### PC3a

1. Konfigurasi alamat IP

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/04.png){: .normal }

#### Switch1

1. Mengkonfirmasi default VLAN

   > tab CLI

   ```console
   Switch>enable
   Switch#show vlan brief
   ```

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/05.png){: .normal }

#### PC1a, PC2a, PC3a

1. Mengkonfirmasi terhubung jaringan 1 segmen

   > tab Desktop -> Command Prompt

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/06.png){: .normal }

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/07.png){: .normal }

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/08.png){: .normal }

#### Switch1

1. Mengaktifkan VLAN baru

   ```console
   Switch#configure terminal
   Switch(config)#hostname Sw1
   Sw1(config)#vlan 200
   Sw1(config-vlan)#name Private
   Sw1(config-vlan)#exit
   Sw1(config)#
   ```

#### Switch1

1. Mengkonfirmasi VLAN baru

   ```console
   Sw1(config)#do show vlan brief
   ```

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/09.png){: .normal }

#### Switch1

1. Mendaftarkan keanggotaan VLAN baru pada port Fa0/2

   ```console
   Sw1(config)#interface fastEthernet 0/2
   Sw1(config-if)#Switchport mode access
   Sw1(config-if)#Switchport access vlan 200
   Sw1(config-if)#exit
   Sw1(config)#
   ```

#### Switch1

1. Mengkonfirmasi kenggotaan VLAN baru

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/10.png){: .normal }

#### PC1a, PC2a, PC3a

1. Mengkonfirmasi terhubung jaringan 1 segmen (VLAN ID sama) maupun berbeda segmen (VLAN ID berbeda)

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/11.png){: .normal }

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/12.png){: .normal }

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/13.png){: .normal }

#### Switch1

1. Mendaftarkan keanggotaan VLAN baru secara serentak pada port Fa0/11 s.d. Fa0/20

   ```console
   Sw1(config)#interface range fastEthernet 0/11-20
   Sw1(config-if-range)#Switchport mode access
   Sw1(config-if-range)#Switchport access vlan 200
   Sw1(config-if-range)#exit
   Sw1(config)#
   ```

#### Switch1

1. Mengkonfirmasi kenggotaan VLAN baru

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/14.png){: .normal }

1. Tambahkan 1 buah PC, sambungkan ke port Fa0/11 sehingga topologi jaringan menjadi sebagai berikut

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/15.png){: .normal }

#### PC2b

1. Konfigurasi alamat IP

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/16.png){: .normal }

#### PC2a, PC2b

1. Mengkonfirmasi terhubung jaringan VLAN ID sama

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/17.png){: .normal }

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/18.png){: .normal }

#### PC1a, PC31

1. Lakukan pengujian terhadap jaringan VLAN ID berbeda, amati hasilnya

#### Switch1

1. Menyimpan konfigurasi terkini

   ```console
   Sw1#copy running-config startup-config
   ```

## Kesimpulan

1. Jika konfigurasi VLAN berhasil dilakukan maka perangkat yang dapat terhubung hanya yang merupakan anggota suatu VLAN ID yang sama.

1. Penambahan keanggotaan VLAN berdasarkan port pada perangkat Switch dapat dilakukan secara satu per satu maupun secara sekaligus.

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi VLAN dengan instruksi sebagai berikut

1. Suatu topologi jaringan dirancang sebagai berikut

   ![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/19.png){: .normal }

   dengan spesifikasi sebagai berikut

   1. Switch
      1. Type: 2950-24
      2. Hostname: SwUtama
   2. Network
      1. Net ID: 172.xx.100.0/24
      2. xx: nomor presensi masing-masing
   3. VLAN
      1. ID: 10, Name: Guru, Member: Int 6-10
      2. ID: 20, Name: Siswa, Member: Int 11-15
      3. ID: 30, Name: TU, Member: Int 16-20

2. Susun topologi jaringan di atas
3. Rancanglah tabel pengalamatan seperti contoh di atas

   | Device | Interface | VLAN ID | IP Address | Subnet Mask |
   | ------ | --------- | ------- | ---------- | ----------- |
   | PC1    | ...       | ...     | ...        | ...         |
   | PC2a   | ...       | ...     | ...        | ...         |
   | PC2b   | ...       | ...     | ...        | ...         |
   | ...    | ...       | ...     | ...        | ...         |
   | PC4b   | ...       | ...     | ...        | ...         |

4. Lakukan konfigurasi VLAN sesuai kebutuhan
5. Lakukan pengamatan dan pengujian pada jaringan yang telah dikonfigurasi
6. Tulislah laporan/dokumentasi lengkap sesuai template yang tersedia
