---
layout: post
title: Konversi Desimal Biner pada Perhitungan IP Address
date: 2022-06-05 00:00 +0000
author: angga
categories: [Konsep]
tags: [cisco, routing, subnetting]
---

## Pengertian

Setiap perangkat jaringan harus memiliki alamat IP unik agar bisa saling terkoneksi.

Alamat IP bertindak sebagai identitas unik bagi setiap perangkat, seperti komputer, printer, atau router, dan memungkinkan data untuk diteruskan dari satu perangkat ke perangkat lain.

![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/01.png){: .normal }

Alamat IP ditempatkan pada lapisan jaringan (Network Layer) dari arsitektur model OSI (Open System Interconnection).

Lapisan ini bertanggung jawab untuk menentukan dan mengatur routing data melalui jaringan, mengontrol akses ke media transmisi dan menyediakan mekanisme untuk pengiriman dan penerimaan data.

Oleh karena itu, alamat IP adalah bagian penting dari kinerja dan efisiensi jaringan komputer.

### Bentuk

Format penulisan alamat IP Address `x.x.x.x`, di mana `x` bisa bernilai angka desimal `0` s.d. `255`.

![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/02.png){: .normal }

Dalam 1 oktet atau 8 bit/biner dalam penyimpanan perangkat komputer senilai dengan 1 byte

![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/03.png){: .normal }

Maka, berapa byte-kah ukuran penyimpanan sebuah alamat IP?

### Versi

Ada 2 version field pada IP Address yang umum digunakan dalam jaringan, yaitu:

1. IPv4 dengan lebar 32 bits
2. IPv6 dengan lebar 128 bits

Informasi IP Address pada suatu Network Interface perangkat komputer dapat ditampilkan dengan perintah berikut.

1. Linux menggunakan perintah Terminal `ip addr`

   ![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/04.png){: .normal }

2. macOS menggunakan perintah Terminal `ifconfig`

   ![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/05.png){: .normal }

3. Windows menggunakan perintah Command Prompt `ipconfig`

   ![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/06.png){: .normal }

> **Catatan:**
> Untuk selanjutnya, pembahasan IP Address akan spesifik pada IPv4.

### Macam

Public IP Address adalah pengalamatan yang digunakan oleh perangkat yang terhubung langsung dalam internet (alamat pasti unik).

Private IP Address adalah pengalamatan yang hanya digunakan oleh perangkat yang berkomunikasi dalam sebuah LAN (jaringan sekolah, jaringan kantor) dan tidak bisa terhubung langsung ke internet.

![](/assets/img/2022-06-05-konversi-desimal-biner-pada-perhitungan-ip-address/07.png){: .normal }

Berikut merupakan range yang digunakan untuk pengalamatan IP Private.

| Kelas | Range Private IP                 |
| ----- | -------------------------------- |
| A     | 10.0.0.0 s.d. 10.255.255.255     |
| B     | 172.16.0.0 s.d. 172.31.255.255   |
| C     | 192.168.0.0 s.d. 192.168.255.255 |

Range IP Address di luar tabel di atas berarti termasuk IP Public, tidak disarankan untuk digunakan pada jaringan lokal.

### Kelas

Terdapat 5 kelas pada pengelompokkan IP Address

| Kelas | IP Awal   | IP Akhir        |
| ----- | --------- | --------------- |
| A     | 0.0.0.0   | 127.255.255.255 |
| B     | 128.0.0.0 | 191.255.255.255 |
| C     | 192.0.0.0 | 223.255.255.255 |
| D     | 224.0.0.0 | 239.255.255.255 |
| E     | 240.0.0.0 | 255.255.255.255 |

Namun kelas IP Address yang umum digunakan dalam jaringan hanya dari A s.d. C.

Pada masa sekarang pengelompokkan alamat lebih populer menggunakan notasi CIDR.

CIDR merupakan kependekan dari Classless Inter-Domain Routing adalah klasifikasi alamat perangkat jaringan tanpa aturan kelas.

## Konversi Desimal Biner

Sebuah alamat IP terususun daari 4 oktet yang di dalam 1 oktet berisi 8 bit / biner bernilai 0 atau 1.

### Tabel Konversi

Jika sebuah oktet bernilai biner 1 semua, maka 11111111

| Oktet    | 1            | 1            | 1            | 1            | 1            | 1            | 1            | 1            |
| -------- | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| Eksponen | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> | 2<sup></sup> |
| Desimal  | 128          | 64           | 32           | 16           | 8            | 4            | 2            | 1            |

Total dari seluruh konversi desimal adalah

= 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1

= 255

### Contoh Kasus

Tentukan konversi biner ke desimal dari

10000011

### Solusi

| Oktet    | 1            | 0   | 0   | 0   | 0   | 0   | 1            | 1            |
| -------- | ------------ | --- | --- | --- | --- | --- | ------------ | ------------ |
| Eksponen | 2<sup></sup> | 0   | 0   | 0   | 0   | 0   | 2<sup></sup> | 2<sup></sup> |
| Desimal  | 128          | 0   | 0   | 0   | 0   | 0   | 2            | 1            |

Total dari seluruh konversi desimal adalah

= 128 + 0 + 0 + 0 + 0 + 0 + 2 + 1

= 131

### Berlatih

Tentukan nilai desimal dari bilangan biner berikut

1. 11110101
1. 01111000
1. 10101011
1. 10111010
1. 11111110
