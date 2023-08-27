---
layout: post
title: Routing Dinamis pada Jaringan Komputer
date: 2022-10-02 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, routing]
---

## Pengertian

Dapatkah terbayangkan jika harus melakukan entry routing table pada jaringan seperti ini?

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/01.png){: .normal }

Routing dinamis adalah mekanisme routing yang routing table-nya otomatis dikonfigurasi oleh routing protocol.

Sehingga dengan topologi seperti di atas pun ketika terjadi perubahan topologi maupun penambahan perangkat jaringan baru, tidak perlu melakukan konfigurasi ulang pada seluruh perangkat router.

## Cara Kerja

Routing dinamis terjadi karena adanya pertukaran informasi antar perangkat router yang meliputi

1. Pengenalan remote network secara dinamis.
2. Penambahan jalur ke routing table.
3. Penentuan jalur terbaik ke masing-masing jaringan.
4. Pencarian jalur alternatif jika jalur terbaik down.

## Komponen

1. Struktur data

   merupakan tabel atau database disimpan pada RAM digunakan untuk menjalankan operasi routing.

2. Algoritma routing

   merupakan langkah-langkah teratur yang digunakan untuk pemrosesan informasi routing dan penentuan jalur terbaik.

3. Routing protocol messages

   digunakan untuk menemukan router tetangga serta saling bertukar, mempelajari dan pemeliharaan informasi jaringan routing yang akurat.

## Karakteristik

### Perbandingan

Perbandingan berikut dapat menjadi pertimbangan untuk suatu jaringan apakah akan dikonfigurasi menggunakan teknik routing statis ataupun routing dinamis.

| Perbandingan             | Routing Statis                                                               | Routing Dinamis                                                                        |
| ------------------------ | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Konfigurasi routing      | Dilakukan secara manual                                                      | Dilakukan secara otomatis                                                              |
| Penyusunan routing table | Seluruh rute di-entry satu per satu oleh network admin                       | Entry terisi otomatis                                                                  |
| Router Iain              | Dikenalkan oleh network admin                                                | Dikenali secara otomatis ketika terjadi perubahan topologi jaringan                    |
| Algoritma routing        | Tidak mendukung algoritma routing                                            | Mendukung algoritma yang rumit untuk kebutuhan routing                                 |
| Sekala Penggunaan        | Pada jaringan kecil                                                          | Pada jaringan besar                                                                    |
| Sambungan terputus       | Mengacaukan perubahan rute                                                   | Tidak mengacaukan perubahan rute                                                       |
| Keamanan                 | Lebih aman karena tidak ada advertisement yang dikirim bersamaan dengan data | Kurang aman karena mengirimkan multicast dan broadcast                                 |
| Protokol routing         | Tidak menggunakan protokol routing pada prosesnya                            | Menggunakan protokol routing (seperti RIP, EIGRP, dll) pada seluruh proses routing-nya |
| Sumber daya tambahan     | Tidak mengonsumsi sumber daya tambahan                                       | Membutuhkan sumber daya tambahan (seperti CPU, memory, bandwidth, dll)                 |

### Kelebihan

Beberapa kelebihan yang didapat jika jaringan mengaplikasikan routing dinamis yaitu

1. Cocok digunakan pada topologi jaringan yang membutuhkan banyak perangkat router.
1. Mudah digunakan pada jaringan dengan sekala besar.
1. Hampir tidak tergantung ukuran jaringan.
1. Kesalahan pada jalur tidak mempengaruhi jaringan secara keseluruhan.
1. Jika terjadi suatu jalur yang putus, maka jalur lain akan digunakan tanpa konfigurasi manual tambahan.
1. Mendukung algoritma routing yang lebih rumit.

### Kekurangan

Beberapa kekurangan yang terjadi jika jaringan mengaplikasikan routing dinamis yaitu

1. Implementasi yang cukup rumit.
2. Keamanan dirasa kurang dibandinkan dengan routing statis karena terjadi perubahan perutean pada multicast.
3. Konfigurasi tambahan dibutuhkan seperti aktivasi protokol routing, interface yang pasif untuk menambah keamanan.
4. Dibutuhkan sumberdaya tambahan seperti memory, CPU, dan link bandwidth.

## Protokol Routing

Routing protocol adalah aturan-aturan yang digunakan untuk proses komunikasi antar router dalam suatu jaringan.

Protokol ini mengijinkan router-router tersebut untuk bertukar ataupun berbagi informasi tentang jaringan dan koneksi antar router.

Router menggunakan informasi ini untuk membangun dan memperbaiki maupun melakukan update terkini routing table.

Secara umum, routing dinamis dibagi menjadi

1. IGP (Interior Gateway Protocol) dan
1. EGP (Exterior Gateway Protocol).

Macam-macam protokol routing dan algoritma yang digunakan adalah sebagai berikut:

1. IGP (Interior Gateway Protocol)

   1. RIP (Routing Information Protocol): Distance Vector
   1. IGRP (Interior Gateway Routing Protocol): Distance Vector
   1. EIGRP (Enhanced Interior Gateway Routing Protocol): Hybrid
   1. OSPF (Open Shortest Path First): Link State
   1. IS-IS (Intermediate System to Intermediate System): Link State

1. EGP (Exterior Gateway Protocol)

   1. BGP (Border Gateway Protocol): Path Vector

Pembagian jenis protokol routing seperti pada bagan berikut

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/03.png){: .normal }

### Autonomous System

Autonomous System (AS) adalah alamat jaringan dijalankan oleh yang suatu operator jaringan dibawah satu kebijakan routing, contoh yang paling mudah yaitu jaringan ISP (Internet Service Provider).

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/04.png){: .normal }

Kaitannya dengan AS, Interior Gateway Protocol (IGP) diaplikasikan pada pengelolaan routing suatu jaringan dalam sebuah AS (Autonomous System), misal dalam suatu jaringan ISP.

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/05.png){: .normal }

Sedangkan jika routing jaringan yang digunakan untuk menghubungkan antar AS maka akan menggunakan Exterior Gateway Protocol (EGP).

### Distance Vector

Algoritma protokol routing distance vector ini diibaratkan seperti papan penunjuk jalan.

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/06.png){: .normal }

Router harus memutuskan jalur paket berdasarkan distance dan vector.

1. Distance

   jauhnya source network menuju destination berdasarkan metric. Metric dihitung dari hop count, cost, bandwidth, delay, dll.

1. Vector (Direction)

   arah dari next hop router untuk menuju ke destination.

Protocol jenis Distance Vector hanya mengetahui route dan metric untuk menuju destination tertentu.

### Link State

Algoritma protokol routing link state ini dapat diibaratkan seperti peta lengkap suatu daerah.

Peta jaringan ini akan dibagi ke dalam wilayah atau akan dipetakan menggunakan area-area tertentu.

![](/assets/img/2022-10-02-routing-dinamis-pada-jaringan-komputer/07.png){: .normal }

Protocol jenis link-state mengetahui topologi jaringan secara keseluruhan dengan mengumpulkan informasi dari setiap router.

Area yang harus ada pada link-state adalah area 0 atau backbone.

Pembagian menjadi area-area ini bertujuan mengurangi resource router dengan setiap area mempunyai table routing yang berbeda dengan area yang lain.
