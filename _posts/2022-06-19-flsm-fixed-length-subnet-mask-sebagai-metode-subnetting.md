---
layout: post
title: FLSM (Fixed Length Subnet Mask) sebagai Metode Subnetting
date: 2022-06-19 00:00 +0000
author: angga
categories: [ Materi, Teori ]
tags: [ cisco, routing, subnetting ]
---

## Pengertian

FLSM (Fixed Length Subnet Mask) adalah metode subnetting di mana ukuran mask subnet tetap sama untuk setiap subnet dalam jaringan.

## Kebutuhan

Perhitungan diawali dengan menentukan berapa jumlah subnet yang dibutuhkan.

Selanjutnya menentukan besaran blok subnet yang dapat mencukupi subnet dengan kebutuhan subnet dengan jumlah host terbesar.

Gunakan kembali [tabel subnetting](/posts/pembagian-alamat-pada-jaringan-komputer-subnetting/#tabel-subnetting){:target="_blank"} untuk menemukan prefix length (subnet mask) yang tepat sesuai jumlah subnet, blok subnet, dan host yang dibutuhkan.

> **Catatan:**
> Untuk mempelajari subnetting metode FLSM, anda harus memahami terlebih dahulu tentang subnetting metode CIDR.

## Contoh Kasus

Sebuah jaringan dirancang untuk digunakan dalam sebuah gedung kantor yang terdiri dari beberapa pembagian jaringan.

![](/assets/img/2022-06-19-flsm-fixed-length-subnet-mask-sebagai-metode-subnetting/01.png){: .normal }

Tentukan pembagian jaringan (subnet) menggunakan metode FLSM bila diberikan IP Address **10.1.1.0/24** sebagai acuan!

## Solusi

1. Kebutuhan jaringan ada 3, yaitu

    1. WAN1 dengan kebutuhan 2 hosts, 
    1. LAN1 dengan kebutuhan 10 hosts, dan
    1. LAN2 dengan kebutuhan 45 hosts
    
    Untuk dapat memenuhi kebutuhan semua jaringan, maka dibutuhkan prefix length yang punya jumlah subnet yang mencukupi (sama atau lebih). 
    
    Jumlah subnet yang tepat yaitu 4, sisa 1 subnet.

1. Prefix length yang menghasilkan jumlah subnet 4, yaitu

    1. /26 (kelas C) dengan total 62 host
    1. /18 (kelas B) dengan total 16.382 host
    1. /10 (kelas C) dengan total 4.194.302 host

    Prefix length yang digunakan juga harus dapat memenuhi kebutuhan host terbanyak di antara jaringan yang ada.

    Kebutuhan host terbanyak yaitu LAN2 dengan 45 hosts, maka prefix length yang sudah dapat memenuhi yaitu /26.

1. Alamat jaringan

    1. Prefix length /26
        
        - CIDR Kelas C
        - Porsi N.N.N.H

    1. Subnet mask /26
        
        - 11111111.11111111.11111111.11000000
        - 255.255.255.192

    1. Jumlah subnet /26
        
        - 11111111.11111111.11111111.11000000
        - 2<sup>2</sup>
        - 4 subnet

    1. Blok subnet /26
        
        - 256 - 192 = 64
        - Maka blok kelipatan 0, 64, 128, 192

    1. Alamat acuan 10.1.1.0, nilai pada blok subnet dimasukkan sebagai alamat pertama subnet atau bisa disebut sebagai alamat jaringan

        - Subnet Ke-1: 10.1.1.0/26, untuk WAN1
        - Subnet Ke-2: 10.1.1.64/26, untuk LAN1 
        - Subnet Ke-3: 10.1.1.128/26, untuk LAN2
        - Subnet Ke-4: 10.1.1.192/26, untuk persiapan jaringan baru di masa depan.

## Kesimpulan

Hasil subnetting pada jaringan di atas menggunakan metode FLSM sebagai berikut

![](/assets/img/2022-06-19-flsm-fixed-length-subnet-mask-sebagai-metode-subnetting/02.png){: .normal }

Jika dimasukkan ke dalam topologi jaringan maka menjadi

![](/assets/img/2022-06-19-flsm-fixed-length-subnet-mask-sebagai-metode-subnetting/03.png){: .normal }

## Berlatih

Anda merupakan seorang network administrator suatu perusahaan yang sedang merencakan pembagian jaringan.

![](/assets/img/2022-06-19-flsm-fixed-length-subnet-mask-sebagai-metode-subnetting/04.png){: .normal }

Tentukan pembagian jaringan (subnet) menggunakan metode FLSM jika diberikan IP Address **172.16.0.0/16** sebagai acuan!