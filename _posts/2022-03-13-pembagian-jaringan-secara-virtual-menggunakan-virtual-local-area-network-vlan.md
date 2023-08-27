---
layout: post
title: Pembagian Jaringan secara Virtual Menggunakan Virtual Local Area Network (VLAN)
date: 2022-03-13 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, switching, vlan]
---

## Pengertian

VLAN (Virtual Local Area Network) adalah suatu cara membagi jaringan fisik menjadi beberapa jaringan virtual yang independen, meskipun berada dalam satu jaringan fisik yang sama.

Teknik konfigurasi VLAN ini memungkinkan pengelompokan device jaringan seperti komputer, server, dan peralatan lain menjadi beberapa grup yang terpisah secara logika.

Perangkat jaringan yang mendukung untuk dikonfigurasi protokol tersebut adalah manageable switch.

VLAN menyediakan pemisahan logika pada tingkat switch, sementara subnetting melakukan pemisahan pada tingkat router.

## Karakteristik

Seperti teknik pemisahan jaringan yang lain, tentu saja VLAN mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Keuntungan

1. Fleksibilitas

   VLAN memungkinkan pengelompokan user berdasarkan kesamaan departemen, divisi, atau pekerjaan, bukan lokasi fisik.

1. Segmentasi LAN

   VLAN memperkecil ukuran jaringan dengan mengelompokkan user-user ke dalam VLAN-VLAN yang lebih kecil.

1. Keamanan

   VLAN memisahkan user-user yang bekerja menggunakan data-data yang sensitif pada VLAN yang terpisah, sehingga meningkatkan tingkat keamanan jaringan.

1. Prioritas Traffic

   VLAN memisahkan trafik VoIP dan Data, memungkinkan prioritas diterapkan pada jenis trafik tertentu untuk memastikan kualitas layanan yang baik.

### Kelemahan

1. Kompleksitas

   Konfigurasi VLAN cenderung kompleks dan membutuhkan keterampilan dan pemahaman yang baik akan jaringan.

1. Biaya

   Implementasi VLAN membutuhkan perangkat tambahan, seperti switch VLAN-enabled, yang memperbesar biaya total proyek jaringan.

1. Dukungan Perangkat

   VLAN hanya dapat bekerja dengan baik pada perangkat yang kompatibel dan support VLAN.

1. Latensi

   Terdapat penambahan latensi pada jaringan ketika VLAN digunakan karena paket harus melalui proses tagging dan untagging VLAN.

## Macam

Secara umum ada beberapa jenis VLAN

1. Default VLAN

   VLAN default adalah VLAN bawaan dari perangkat switch yang mencakup semua port pada switch tersebut.

1. Data VLAN

   VLAN data digunakan untuk mengklasifikasikan paket data pada jaringan.

1. Voice VLAN

   VLAN suara digunakan untuk mengklasifikasikan paket suara pada jaringan IP telefoni.

1. Management VLAN

   VLAN pengelolaan digunakan untuk mengkonfigurasi dan memantau perangkat jaringan.

1. Native VLAN

   VLAN asli digunakan untuk menentukan VLAN default yang digunakan pada trunk port.

## Keanggotaan

Berikut pengelompokan VLAN berdasarkan kriteria keanggotaan

1. Port-based VLAN

   VLAN berdasarkan port adalah VLAN yang pengelompokannya didasarkan pada port switch. Setiap port pada switch dapat dikonfigurasi untuk termasuk dalam VLAN tertentu.

1. Protocol-based VLAN

   VLAN berdasarkan protokol adalah VLAN yang pengelompokannya didasarkan pada jenis protokol jaringan seperti IP, IPX, atau AppleTalk.

1. MAC-based VLAN

   VLAN berdasarkan MAC adalah VLAN yang pengelompokannya didasarkan pada alamat MAC perangkat jaringan.

1. IP subnet-based VLAN

   VLAN berdasarkan subnet IP adalah VLAN yang pengelompokannya didasarkan pada subnet jaringan IP.

1. Authentication-based VLAN

   VLAN berdasarkan otentikasi adalah VLAN yang pengelompokannya didasarkan pada hasil otentikasi pengguna atau perangkat jaringan.

## Cara Kerja

Mekanisme kerja VLAN adalah sebagai berikut:

1. Pengelompokan

   User atau perangkat dalam jaringan dikelompokkan berdasarkan kesamaan departemen, divisi, pekerjaan, atau aplikasi yang digunakan, bukan berdasarkan lokasi fisik.

1. Tagging

   Setiap paket data yang dikirim oleh user atau perangkat akan diberikan tag identifikasi VLAN. Tag ini menentukan VLAN mana paket data tersebut berasal dan diterima.

1. Switching

   Switch akan memeriksa tag VLAN pada setiap paket data yang masuk, dan hanya mengalirkan paket data yang memiliki tag VLAN yang sesuai ke user atau perangkat yang berada dalam VLAN yang sama.

1. Bridging

   Setelah paket data diterima oleh switch, ia akan melakukan bridging antar VLAN untuk memastikan bahwa paket data dapat diteruskan ke tujuannya.

1. Un-tagging

   Setelah paket data sampai pada tujuannya, tag identifikasi VLAN akan dihapus sehingga paket data dapat diterima dan diproses oleh user atau perangkat yang menerimanya.

## Protokol

Ada dua jenis protokol utama yang digunakan dalam konfigurasi VLAN

1. Dot1Q

   Dot1Q adalah protokol VLAN standar yang diterima oleh IEEE dan banyak digunakan dalam jaringan LAN.

   Dot1Q menambahkan tag 4-byte pada header frame untuk menandai frame dengan ID VLAN tertentu.

   Ini memungkinkan frame untuk diteruskan melalui jaringan dan dipisahkan ke VLAN yang berbeda sesuai dengan tag yang diterima.

   IEEE 802.1Q mendukung hingga 4096 VLAN.

2. ISL (Inter-Switch Link)

   ISL adalah protokol VLAN yang dikembangkan oleh Cisco Systems.

   ISL menambahkan header sepanjang 26 byte pada setiap frame untuk menandai frame dengan ID VLAN tertentu.

   Ini memungkinkan switch untuk mengenali dan memisahkan frame ke VLAN yang berbeda sesuai dengan header ISL yang diterima.

   ISL mendukung hingga 1000 VLAN.

## Ilustrasi

Sebuah perangkat Cisco Switch dikonfigurasi VLAN baru dengan keterangan sebagai berikut

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/01.png){: .normal }

| VLAN ID | VLAN Name  | VLAN Member     | Ket    |
| ------- | ---------- | --------------- | ------ |
| 10      | Jaringan A | Port 1 s.d. 6   | Merah  |
| 20      | Jaringan B | Port 7 s.d. 12  | Kuning |
| 30      | Jaringan C | Port 13 s.d. 18 | Hijau  |

Maka, ada berapakah jumlah VLAN yang tersedia?

VLAN dapat membantu dalam mengatasi masalah colision pada jaringan dengan cara membagi jaringan menjadi beberapa broadcast domain yang terpisah.

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/02.png){: .normal }

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/03.png){: .normal }

Dalam VLAN, setiap broadcast dikirim hanya ke port-port yang termasuk dalam VLAN yang sama, sehingga mengurangi jumlah broadcast yang diterima oleh setiap perangkat jaringan.

Hal ini membantu mengurangi kemungkinan colision pada jaringan dan meningkatkan kinerja jaringan secara keseluruhan.

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/04.png){: .normal }
