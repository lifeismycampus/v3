---
layout: post
title: Peringkasan Alamat pada Jaringan Komputer (Supernetting)
date: 2022-07-03 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, routing, supernetting]
---

## Pengertian

Supernetting, juga dikenal sebagai IP Routing Summarization, adalah teknik agregasi/pengumpulan sejumlah alamat IP yang berbeda-beda menjadi satu dalam jaringan komputer untuk mempermudah pengelolaan dan pengiriman paket data.

Teknik ini menggabungkan beberapa alamat IP menjadi satu alamat IP besar yang lebih sederhana, sehingga mengurangi jumlah informasi yang harus diteruskan melalui jaringan.

![](/assets/img/2022-07-03-peringkasan-alamat-pada-jaringan-komputer-supernetting/01.png){: .normal }

## Kebutuhan

Konsekuensi yang didapatkan ketika mengaplikasikan teknik Supernetting (IP Routing Summarization) pada jaringan yaitu

1. Mempermudah pengelolaan jaringan dengan mengurangi jumlah informasi yang harus diteruskan melalui jaringan.
1. Meningkatkan efisiensi routing karena mengurangi jumlah informasi yang harus diteruskan oleh router.
1. Mengurangi ukuran tabel routing pada router dan mengurangi beban pada sistem.
1. Mempermudah pemeliharaan jaringan dengan mengurangi jumlah alamat IP yang harus dikelola.

namun juga ada beberapa konsekuensi lain seperti

1. Bisa memperlambat proses routing karena harus melakukan de-agregasi alamat sebelum mengirimkan paket data.
1. Dapat menyebabkan masalah routing jika tidak dilakukan dengan benar.
1. Dapat menyebabkan masalah keamanan jika tidak dilakukan dengan benar.
1. Membutuhkan lebih banyak pemahaman dan keterampilan untuk melakukan Supernetting dengan benar.

## Contoh Kasus

Tentukan IP routing summarization untuk jaringan-jaringan berikut menjadi sebuah destination network!

![](/assets/img/2022-07-03-peringkasan-alamat-pada-jaringan-komputer-supernetting/02.png){: .normal }

## Solusi

1. Terdapat beberapa jaringan yang bisa diringkas, yaitu

   - 192.168.1.0/24
   - 192.168.2.0/24
   - 192.168.3.0/24
   - 192.168.4.0/24
   - 192.168.5.0/24

1. Ubah alamat jaringan menjadi bentuk bit/biner.

   - 192.168.1.0 = 11000000.10101000.00000001.00000000
   - 192.168.2.0 = 11000000.10101000.00000010.00000000
   - 192.168.3.0 = 11000000.10101000.00000011.00000000
   - 192.168.4.0 = 11000000.10101000.00000100.00000000
   - 192.168.5.0 = 11000000.10101000.00000101.00000000

1. Beri tanda sampai bit dengan nilai sama untuk setiap jaringan.

   - 11000000.10101000.00000`001`.`00000000`
   - 11000000.10101000.00000`010`.`00000000`
   - 11000000.10101000.00000`011`.`00000000`
   - 11000000.10101000.00000`100`.`00000000`
   - 11000000.10101000.00000`101`.`00000000`

1. Sebelah kanan bit yang sama apapun nilainya dianggap bernilai bit 0.

   - 11000000.10101000.00000`000`.`00000000`

1. Kembalikan ke bentuk desimal.

   - oktet ke-1: 192
   - oktet ke-2: 168
   - oktet ke-3: 0
   - oktet ke-4: 0

1. Total jumlah bit yang sama dalam proses penggabungan tadi dihitung sebagai nilai prefix length jaringan ringkasan.

   - bit sama yaitu 11000000.10101000.00000, total berjumlah 21 digit
   - maka, prefix length jaringan baru nanti /21

1. Maka didapatkan jaringan baru, supernet dari jaringan-jaringan di atas adalah

   - **192.168.0.0/21**

# Berlatih

1. Tentukan IP routing summarization pada jaringan-jaringan berikut!

   - 172.16.4.0/24
   - 172.16.5.0/24
   - 172.16.6.0/24
   - 172.16.128.0/24

1. Tentukan IP routing summarization pada jaringan-jaringan berikut!

   - 172.1.4.0/25
   - 172.1.4.128/25
   - 172.1.5.0/24
   - 172.1.6.0/24
   - 172.1.7.0/24

1. Tentukan IP routing summarization pada jaringan-jaringan berikut!

   - 10.10.1.0/27
   - 10.10.1.32/28
   - 10.10.1.48/26
   - 10.10.1.64/25
   - 10.10.1.128/25
