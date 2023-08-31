---
layout: post
title: Menghubungkan VLAN Berbeda dengan InterVLAN Routing
date: 2022-05-08 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, routing, vlan]
---

## Pengertian

Inter-VLAN routing adalah proses memungkinkan komunikasi antar VLAN (Virtual LAN) pada jaringan.

Tanpa inter-VLAN routing, setiap VLAN hanya dapat berkomunikasi dengan VLAN lain pada switch saja, tidak dapat berkomunikasi dengan VLAN lain pada jaringan.

## Karakteristik

Seperti teknik konfigurasi routing yang lain, tentu saja intervlan routing mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Kelebihan

Kelebihan yang didapat jika mengaplikasikan teknik konfigurasi Inter-VLAN Routing

1. Fleksibilitas

   Inter-VLAN routing memungkinkan administrator jaringan untuk memisahkan lalu lintas jaringan berdasarkan kebutuhan, sehingga memungkinkan jaringan yang lebih fleksibel.

1. Ekonomis

   Inter-VLAN routing memungkinkan pengelolaan jaringan yang lebih efisien dan mengurangi biaya investasi dalam peralatan jaringan.

1. Scalability

   Inter-VLAN routing memungkinkan jaringan untuk dapat berkembang dan bertambah besar sesuai dengan kebutuhan.

1. Peningkatan Keamanan

   Inter-VLAN routing memungkinkan administrator jaringan untuk membatasi lalu lintas jaringan dan memastikan bahwa lalu lintas jaringan tidak terkendali.

### Kekurangan

Kekurangan yang didapat jika mengaplikasikan teknik konfigurasi Inter-VLAN Routing

1. Komplikasi Konfigurasi

   Konfigurasi Inter-VLAN routing dapat menjadi rumit dan membutuhkan waktu dan usaha untuk memastikan bahwa konfigurasi benar.

1. Latensi Tinggi

   Inter-VLAN routing dapat mengakibatkan latensi yang lebih tinggi dibandingkan dengan switch VLAN standar, karena data harus melewati router sebelum sampai pada tujuan akhir.

1. Keamanan yang Kurang

   Inter-VLAN routing dapat meningkatkan risiko keamanan jika tidak diterapkan dengan benar, seperti memperkenalkan risiko akses yang tidak sah.

1. Biaya Tinggi

   Implementasi Inter-VLAN routing dapat menjadi mahal, terutama jika membutuhkan peralatan jaringan baru atau perangkat lunak yang kompleks.

## Metode

Inter-VLAN routing dapat diterapkan dengan beberapa metode termasuk menggunakan Layer 3 switch, menggunakan router dengan interface berbeda untuk setiap vlan yang ada, maupun menggunakan Router-on-a-Stick (ROAS).

### Menggunakan Layer 3 Switch

Inter-VLAN routing menggunakan konfigurasi ini dilakukan pada perangkat multilayer switch atau layer 3 switch.

Selain bisa melakukan proses switching (level 2 pada data link layer) seperti switch pada umumnya, perangkat ini mampu menangani proses routing (level 3 pada network layer) atau pengiriman paket antar jaringan, dalam hal ini jaringan VLAN.

Contoh topologi intervlan routing menggunakan layer 3 switch sebagai berikut

![](/assets/img/2022-05-08-menghubungkan-vlan-berbeda-menggunakan-intervlan-routing/01.png){: .normal }

### Menggunakan Router dengan Interface Berbeda-beda

Inter-VLAN routing menggunakan konfigurasi ini dilakukan pada perangkat router.

Konfigurasi ini secara umum dilakukan dengan menyediakan koneksi beberapa physical interface antara router dan switch sebagai trunk link.

Jumlah link yang disediakan haruslah sejumlah VLAN ID yang butuh untuk di-routing.

![](/assets/img/2022-05-08-menghubungkan-vlan-berbeda-menggunakan-intervlan-routing/02.png){: .normal }

### Router-on-a-Stick (ROAS)

Inter-VLAN routing menggunakan konfigurasi ini dilakukan juga pada perangkat router.

Konfigurasi dilakukan dengan menyediakan sebuah physical interface pada router sebagai trunk link yang terhubung ke sebuah port pada switch dalam mode trunk.

Router dikonfigurasi untuk mengaktifkan subinterface/interface virtual sesuai dengan physical interface yang digunakan.

jumlah subinterface yang diaktifkan haruslah sejumlah VLAN ID yang butuh untuk di-routing.

![](/assets/img/2022-05-08-menghubungkan-vlan-berbeda-menggunakan-intervlan-routing/03.png){: .normal }

## Keamanan

Inter-VLAN routing membutuhkan pengelolaan keamanan untuk memastikan bahwa jaringan aman dan terlindungi dari ancaman keamanan seperti serangan jaringan, akses yang tidak sah, dan lainnya.

Berikut adalah beberapa konsep keamanan yang penting dalam Inter-VLAN routing:

1. Access Control List (ACL)

   ACL adalah daftar kontrol akses yang menentukan bagaimana paket jaringan diterima atau ditolak oleh perangkat jaringan.

   ACL menggunakan aturan khusus untuk menentukan apakah paket diterima atau ditolak.

   Ini digunakan untuk memastikan bahwa jaringan terlindung dari serangan dan akses yang tidak sah.

1. Firewall

   Firewall adalah perangkat yang memantau dan mengendalikan akses jaringan.

   Firewall memiliki kemampuan untuk menganalisis traffic jaringan dan membuat keputusan apakah traffic tersebut harus diterima atau ditolak.

   Firewall biasanya digunakan untuk memblokir serangan jaringan dan membatasi akses yang tidak sah.

1. VLAN Access Control

   Menentukan VLAN mana yang dapat diakses oleh host atau perangkat tertentu.

   Ini membatasi akses yang tidak sah dan memastikan bahwa hanya perangkat yang sah yang dapat mengakses jaringan.

1. Port Security

   Menentukan perangkat apa saja yang dapat mengakses switch melalui port tertentu.

   Ini membatasi akses yang tidak sah dan memastikan bahwa hanya perangkat yang sah yang dapat mengakses jaringan.

1. Virtual Router Redundancy Protocol (VRRP)

   VRRP memastikan bahwa router tetap aktif dan memberikan solusi backup jika salah satu router gagal.

   Ini memastikan bahwa jaringan tetap berfungsi selama ada gangguan.

1. Encryption

   Menggunakan enkripsi untuk memproteksi data yang dikirimkan melalui jaringan.

   Ini memastikan bahwa data tidak dapat dicuri atau dibaca oleh pihak yang tidak sah.

1. Virtual Routing and Forwarding (VRF)

   VRF adalah teknologi yang memungkinkan jaringan memiliki beberapa routing domain yang terisolasi secara logika dalam satu perangkat.

   VRF memastikan bahwa jaringan dapat memiliki routing domain yang terisolasi dan tidak berdampak pada routing domain lainnya.

   Ini memastikan bahwa jaringan tetap stabil dan aman meskipun ada perubahan yang terjadi dalam jaringan.
