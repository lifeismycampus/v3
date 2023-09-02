---
layout: post
title: Konfigurasi Port Based VLAN pada Cisco Packet Tracer
date: 2022-03-27 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, vlan]
---

## Ulasan

Virtual Local Area Network (VLAN) merupakan teknologi jaringan yang memungkinkan pembagian jaringan fisik menjadi sejumlah jaringan virtual yang terpisah.

Masing-masing VLAN berperan sebagai entitas jaringan independen dengan alamat IP yang unik serta konfigurasi jaringan yang berbeda.

Inovasi ini memfasilitasi administrator jaringan dalam mengelompokkan perangkat-perangkat jaringan berdasarkan fungsi, tingkat keamanan, atau struktur organisasi. Dengan demikian, pemeliharaan jaringan menjadi lebih terstruktur dan tingkat keamanan jaringan meningkat.

Kelebihan lain dari VLAN adalah kemudahan dalam manajemen jaringan serta kemampuannya dalam mengurangi kemacetan (congestion) pada jaringan dengan mengatur lalu lintas jaringan yang tidak diinginkan.

Pada kesempatan praktikum kali ini, kami akan membahas langkah-langkah konfigurasi VLAN yang dikelompokkan berdasarkan port pada switch.

## Alat dan Bahan

1. Perangkat Komputer
2. Cisco Packet Tracer
3. Akun [Cisco Skills for All](https://skillsforall.com/) / [Cisco NetAcad](https://www.netacad.com/)

## Perintah CLI

Dalam CLI (Command Line Interface) Cisco Packet Tracer, terdapat beberapa mode yang memungkinkan pengguna untuk berinteraksi dengan perangkat switch. Berikut adalah penjelasan tentang masing-masing mode tersebut:

1. User EXEC Mode (Mode Pengguna)

   Ini adalah mode awal setelah Anda masuk ke CLI. Mode ini memberikan akses terbatas ke perintah dasar seperti melihat informasi dasar tentang perangkat dan menjalankan perintah yang bersifat umum. Biasanya ditandai dengan tanda `>`, misalnya: `Switch>`. Dalam mode ini, Anda hanya dapat menjalankan perintah dasar seperti 'show' dan 'ping' untuk melihat informasi dasar dan menguji konektivitas.

1. Privileged EXEC Mode (Mode Eksekutif dengan Hak Akses)

   Untuk masuk ke mode ini dari mode pengguna, Anda dapat menggunakan perintah 'enable'. Mode ini memberikan hak akses lebih tinggi dan memungkinkan Anda menjalankan perintah yang lebih kuat dan merubah konfigurasi. Anda dapat melakukan perintah seperti 'show running-config' untuk melihat konfigurasi yang sedang berjalan dan 'copy' untuk menyimpan konfigurasi.

1. Global Configuration Mode (Mode Konfigurasi Global)

   Setelah masuk ke mode privileged EXEC, Anda dapat masuk ke mode konfigurasi global dengan perintah 'configure terminal' atau 'conf t'. Mode ini memungkinkan Anda untuk mengkonfigurasi berbagai pengaturan global pada perangkat switch, termasuk pengaturan VLAN, antarmuka, dan banyak lagi.

1. Interface Configuration Mode (Mode Konfigurasi Antarmuka)

   Dalam mode konfigurasi global, Anda dapat memasuki mode konfigurasi antarmuka dengan perintah seperti 'interface GigabitEthernet0/1'. Ini memungkinkan Anda untuk mengkonfigurasi pengaturan yang terkait dengan antarmuka tertentu, seperti VLAN, mode antarmuka, dan lain-lain.

1. VLAN Configuration Mode (Mode Konfigurasi VLAN)

   Ketika Anda berada dalam mode konfigurasi antarmuka, Anda juga dapat masuk ke mode konfigurasi VLAN dengan perintah seperti 'switchport access vlan'. Mode ini memungkinkan Anda untuk mengkonfigurasi atribut VLAN untuk antarmuka yang bersangkutan.

Setiap mode ini memiliki tingkat akses yang berbeda dan memungkinkan Anda untuk melakukan berbagai tindakan tergantung pada tujuan dan hak akses Anda. Pindah antara mode-mode ini memungkinkan pengguna untuk menjalankan perintah yang sesuai dengan kebutuhan mereka dalam mengelola dan mengkonfigurasi perangkat switch.

Perintah yang digunakan pada praktikum kali ini yaitu:

1. Switch#show running-config

   Perintah ini digunakan untuk menampilkan konfigurasi yang sedang berjalan pada switch, yang mencakup semua konfigurasi yang dibuat dalam berbagai mode. Ini memberikan tampilan rinci tentang pengaturan dan konfigurasi saat ini pada switch.

2. Switch#show vlan

   Perintah ini digunakan untuk menampilkan informasi tentang semua VLAN yang dikonfigurasi pada switch. Ini memberikan detail seperti ID VLAN, nama, dan port yang terkait.

3. Switch#show vlan brief

   Perintah ini memberikan tampilan ringkasan tentang informasi VLAN pada switch. Ini menampilkan daftar singkat VLAN yang dikonfigurasi beserta ID dan penugasan port.

4. Switch#copy running-config startup-config

   Perintah ini digunakan untuk menyimpan konfigurasi berjalan saat ini ke dalam konfigurasi startup. Konfigurasi startup adalah konfigurasi yang akan digunakan oleh switch saat dinyalakan atau di-restart.

5. Switch#configure terminal

   Perintah ini memungkinkan pengguna memasuki mode konfigurasi global. Dalam mode ini, berbagai pengaturan global dan konfigurasi untuk switch dapat dikonfigurasi.

6. Switch(config)#hostname 'name'

   Perintah ini digunakan digunakan untuk mengganti atau mengatur nama host dari perangkat switch yang sedang dikonfigurasi. Nama host ini akan muncul di baris perintah CLI dan juga bisa digunakan untuk mengidentifikasi perangkat dalam jaringan.

7. Switch(config)#vlan 'id'

   Perintah ini digunakan dalam mode konfigurasi global untuk membuat atau mengkonfigurasi VLAN dengan ID numerik tertentu. VLAN digunakan untuk membagi jaringan secara logika.

8. Switch(config-vlan)#name 'name'

   Perintah ini, digunakan dalam mode konfigurasi VLAN, memberikan nama yang mudah dibaca pada ID VLAN yang dikonfigurasi. Nama ini membantu mengidentifikasi tujuan atau fungsi VLAN.

9. Switch(config)#interface 'type' 'num'

   Perintah ini digunakan dalam mode konfigurasi global untuk memasuki mode konfigurasi antarmuka tertentu, di mana 'type' mewakili tipe antarmuka (seperti FastEthernet, GigabitEthernet) dan 'num' adalah nomor antarmuka.

10. Switch(config)#interface range 'type' 'num' - 'num'

    Serupa dengan perintah sebelumnya, perintah ini memasuki mode konfigurasi untuk rentang antarmuka berurutan. Ini berguna ketika mengkonfigurasi beberapa antarmuka secara bersamaan.

11. Switch(config-if)#switchport mode access

    Perintah ini digunakan dalam mode konfigurasi antarmuka untuk mengatur antarmuka aktif agar berfungsi sebagai tautan akses. Tautan akses digunakan untuk menghubungkan perangkat pengguna akhir.

12. Switch(config-if)#switchport access vlan 'id'

    Perintah ini, dalam mode konfigurasi antarmuka, menetapkan antarmuka aktif ke VLAN tertentu menggunakan ID-nya. Antarmuka menjadi anggota VLAN yang ditentukan.

13. Switch(config-if)#exit

    Perintah ini keluar dari tingkat mode konfigurasi antarmuka saat ini dan kembali satu tingkat ke mode konfigurasi global.

14. Switch(config-if)#end

    Perintah ini keluar dari mode konfigurasi antarmuka atau mode konfigurasi global dan kembali ke mode privileged EXEC.

Gunakan tombol <kbd>Enter</kbd> untuk mengeksekusi suatu perintah.

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa tahapan yaitu

1. Persiapan
2. Konfigurasi dan Konfirmasi
3. Kesimpulan
4. Berlatih

### 1. Persiapan

#### Topologi jaringan

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

| Switch      | 2950-24                      |
| ----------- | ---------------------------- |
| VLAN ID     | 200                          |
| VLAN Name   | Private                      |
| VLAN Member | port 2, port 11 s.d. port 20 |

#### Tabel pengalamatan

| Device | Interface                       | VLAN ID | IP Address  | Subnet Mask   |
| ------ | ------------------------------- | ------- | ----------- | ------------- |
| PC1a   | Fa0                             | 1       | 10.100.1.11 | 255.255.255.0 |
| PC2a   | Fa0                             | 200     | 10.100.1.21 | 255.255.255.0 |
| PC3a   | Fa0                             | 1       | 10.100.1.31 | 255.255.255.0 |
| Switch | Fa0/1                           | 1       | -           | -             |
| Switch | Fa0/2                           | 200     | -           | -             |
| Switch | Fa0/3                           | 1       | -           | -             |
| Switch | Fa0/11, Fa0/12, ... s.d. Fa0/20 | 200     | -           | -             |
| Switch | selain port di atas             | 1       | -           | -             |

### 1. Konfigurasi dan Konfirmasi

#### Langkah ke-1: [PC] atur alamat IP

Klik pada PC, buka tab Desktop, pilih menu IP Configuration

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/02.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/03.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/04.png){: .normal }

#### Langkah ke-2: [Switch] konfirmasi keanggotaan default VLAN

Klik pada Switch, buka tab CLI

```console
Switch>enable
Switch#show vlan brief
```

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/05.png){: .normal }

#### Langkah ke-3: [PC] konfirmasi PC terhubung dalam 1 segmen jaringan

Klik pada PC, buka tab Desktop, pilih menu Command Prompt

```console
ping 'target'
```

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/06.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/07.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/08.png){: .normal }

#### Langkah ke-4: [Switch] mengaktifkan VLAN baru

Buka kembali tab CLI pada Switch

```console
Switch#configure terminal
Switch(config)#hostname Sw1
Sw1(config)#vlan 200
Sw1(config-vlan)#name Private
Sw1(config-vlan)#exit
Sw1(config)#
```

#### Langkah ke-5: [Switch] mengkonfirmasi VLAN baru sudah aktif

```console
Sw1(config)#do show vlan brief
```

> `show` dapat pula dieksekusi pada Configuration Mode dengan menambahkan `do` pada awal perintah

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/09.png){: .normal }

#### Langkah ke-6: [Switch] mendaftarkan suatu port sebagai anggota VLAN baru

Port Fa0/2 sebagai anggota VLAN 200

```console
Sw1(config)#interface fastEthernet 0/2
Sw1(config-if)#switchport mode access
Sw1(config-if)#switchport access vlan 200
Sw1(config-if)#exit
Sw1(config)#
```

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/10.png){: .normal }

#### Langkah ke-7: [Switch] konfirmasi jaringan PC setelah VLAN

Bandingkan hasil ping antara jaringan 1 segmen dan berbeda segmen

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/11.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/12.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/13.png){: .normal }

#### Langkah ke-8: [Switch] mendaftarkan beberapa port sekaligus sebagai anggota VLAN baru

Port Fa0/11, Fa0/12, ... s.d. Fa0/20 sebagai anggota VLAN 200

```console
Sw1(config)#interface range fastEthernet 0/11-20
Sw1(config-if-range)#switchport mode access
Sw1(config-if-range)#switchport access vlan 200
Sw1(config-if-range)#exit
Sw1(config)#
```

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/14.png){: .normal }

#### Langkah ke-9: [Switch] mengembangankan jaringan VLAN

Menambahkan PC sebagai anggota VLAN

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/15.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/16.png){: .normal }

#### Langkah ke-10: [PC] konfirmasi ulang PC terhubung dalam segmen sama maupun berbeda

Bandingkan hasil ping antara jaringan 1 segmen dan berbeda segmen

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/17.png){: .normal }

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/18.png){: .normal }

#### Langkah ke-11: [Switch] menyimpan konfigurasi terkini

```console
Sw1#copy running-config startup-config
```

### 3. Kesimpulan

Apabila konfigurasi VLAN berhasil diimplementasikan, hanya perangkat yang menjadi anggota dari VLAN ID yang sama yang dapat terhubung. Proses penambahan keanggotaan VLAN berdasarkan port pada perangkat Switch dapat dilakukan secara individual atau kelompok (berdasarkan rentang nomor port).

### 4. Berlatih

#### Topologi Jaringan

Perhatikan topologi jaringan berikut!

![](/assets/img/2022-03-27-konfigurasi-vlan-pada-cisco-packet-tracer/19.png){: .normal }

#### Spesifikasi

Tersedia suatu topologi jaringan di atas dengan spesifikasi berikut:

1. Switch

   1. Type: 2950-24
   1. Hostname: SwUtama

1. VLAN

   1. ID: 10, Name: Guru, Member: port 6 s.d. port 10
   2. ID: 20, Name: Siswa, Member: port 11 s.d. port 15
   3. ID: 30, Name: TU, Member: port 16 s.d. port 20

1. Network

   1. Net ID: 172.xx.100.0/24

> Kode `xx` diganti dengan nomor presensi masing-masing.

#### Instruksi

Lakukan konfigurasi VLAN dengan instruksi:

1.  Susun topologi jaringan di atas
2.  Rancang tabel pengalamatan seperti contoh
3.  Konfigurasikan VLAN sesuai spesifikasi
4.  Lakukan pengamatan dan pengujian pada jaringan terkonfigurasi
5.  Susun dokumentasi sesuai lembar kerja tersedia
