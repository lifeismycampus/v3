---
layout: post
title: Routing Information Protocol (RIP) sebagai Protokol Routing
date: 2022-10-09 00:00 +0000
author: angga
categories: [ Materi, Teori ]
tags: [ cisco, routing ]
---

## Pengertian

Routing Information Protocol (RIP) merupakan salah satu contoh routing protocol bertipe distance vector.

Protokol RIP adalah salah satu protokol perutean yang paling banyak digunakan dan merupakan protokol default untuk banyak router.

Pada routing protocol yang bertipe distance vector, routing updates muncul secara periodik dan pada saat topologi jaringan berubah.

Dalam pencarian jalur terbaik pada jaringan routing, RIP menggunakan algoritma routing yang disebut algoritma Bellman-Ford.

## Distance Vector

Distance Vector Routing Protocol adalah protokol routing yang menggunakan jumlah hop sebagai metric utama untuk menentukan jalur terbaik bagi paket data untuk melakukan perjalanan melalui jaringan tertentu. 

Proses ini dilakukan dengan cara router mem-broadcast secara periodik tentang informasi tabel routing ke router tetangganya dan kemudian memperbarui entri tabel peruteannya berdasarkan informasi yang diterimanya dari router tetangga tersebut. 

Hal ini memungkinkan jalur terpendek yang akan diambil untuk paket data, dan memungkinkan jaringan untuk bereaksi dengan cepat terhadap setiap perubahan dalam topologi jaringan. 

## Algoritma Bellman-Ford

Algoritma Bellman-Ford adalah cara yang efisien untuk menghitung jalur terpendek antara dua titik dalam jaringan. Algoritma ini sangat berguna ketika menghitung rute dalam jaringan RIP (Routing Information Protocol). 

Algoritma Bellman-Ford bekerja dengan menyebarkan informasi melalui jaringan menggunakan protokol perutean vektor jarak. Setiap node menghitung biaya rute ke tetangganya, dan kemudian meneruskan informasi ini ke node berikutnya. Proses ini diulangi sampai jalur terpendek antara dua titik ditentukan.

## Perhitungan Metric

RIP menggunakan metric, seperti jumlah hop, untuk menghitung jalur terbaik untuk diambil paket. 

Paket dikirim di sepanjang jalur dengan hop terendah. 

![](/assets/img/2022-10-09-protokol-routing-routing-information-protocol-rip/01.png){: .normal }

## Karakteristik

Walau sangat populer digunakan, tentu saja RIP mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Kelebihan

1. Mudah dikonfigurasi, hanya butuh menginput jaringan terhubung langsung.
1. Tidak kompleks, tidak memerlukan design seperti routing protocol OSPF.
1. Routing overhead rendah (jumlah paket kontrol routing yang ditransmisikan per data paket yang terkirim ke tujuan selama pengambilan data tidak banyak).

### Kekurangan

1. Utilisasi bandwidth sangat tinggi karena diperlukan untuk broadcast setiap 30 detik.
1. Terbatas pada jumlah hop, bukan bandwidth.
1. Tidak scalable, hop count maksimal hanya 15.
1. Waktu konvergensi (waktu yang dibutuhkan oleh router untuk menggunakan alternative route ketika best route down) yang rendah.