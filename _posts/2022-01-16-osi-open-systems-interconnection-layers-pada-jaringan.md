---
layout: post
title: OSI (Open Systems Interconnection) Layers sebagai Standarisasi Jaringan Komputer
date: 2022-01-16 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [osi]
---

## Pengertian

OSI (Open Systems Interconnection) Layers adalah sistem arsitektur jaringan komputer yang dikembangkan oleh ISO (International Organization for Standardization).

Sistem ini mengatur bagaimana data harus berinteraksi dan diteruskan melalui jaringan komputer.

OSI Model juga bisa merujuk ke suatu standarisasi pada perangkat jaringan komputer, artinya dapat dikatakan juga merupakan sebuah standar yang mengatur tentang bagaimana produk perangkat jaringan dari berbagai vendor dapat saling berkomunikasi/kompatibel/dapat digunakan bersama-sama.

## Standarisasi

Protokol adalah seperangkat aturan yang menentukan bagaimana data ditransmisikan antara perangkat yang berbeda dalam jaringan.

Sebelum adanya standarisasi OSI model, setiap vendor menggunakan standar networking model mereka sendiri, acak-acakan.

![](/assets/img/2022-01-16-osi-open-systems-interconnection-layers-pada-jaringan/02.png){: .normal }

Setelah diterapkannya OSI model, maka setiap perangkat mauapun jaringan komputer berjalan berdasarkan sesuai aturan yang disepakati bersama dan saling kompatibel.

![](/assets/img/2022-01-16-osi-open-systems-interconnection-layers-pada-jaringan/01.png){: .normal }

## Lapisan

Berikut adalah aplikasi masing-masing layer pada jaringan:

1. Fisik (Physical)

   Berkaitan dengan transmisi data melalui media fisik seperti kabel atau frekuensi radio.

2. Data Link

   Berkaitan dengan pengiriman paket data melalui jaringan dan memastikan integritas data pada tingkat bit.

3. Jaringan (Network)

   Berkaitan dengan pemetaan jalur dan pengalihan trafik data dalam jaringan.

4. Transport

   Berkaitan dengan transmisi data yang aman dan terintegritas antar aplikasi dalam jaringan.

5. Sesi (Session)

   Berkaitan dengan kontrol sesi komunikasi antar aplikasi.

6. Presentasi (Presentation)

   Berkaitan dengan enkapsulasi dan enkripsi data sebelum diteruskan ke lapisan aplikasi.

7. Aplikasi (Application)

   Berkaitan dengan interaksi antar aplikasi dan pemrosesan permintaan dan respon antar aplikasi.

![](/assets/img/2022-01-16-osi-open-systems-interconnection-layers-pada-jaringan/03.png){: .normal }

Berikut adalah contoh perangkat/layanan nyata yang terdapat pada masing-masing lapisan (layer) pada OSI model, mulai dari Physical Layer hingga Application Layer:

1. Lapisan Fisik (Physical Layer):

   1. Kabel UTP (Unshielded Twisted Pair)
   1. Kabel Coaxial
   1. Kabel Serat Optik
   1. Hub (Repeater Hubs)
   1. NIC (Network Interface Card)

1. Lapisan Data Link (Data Link Layer):

   1. Switch
   1. Bridge
   1. MAC Address (Media Access Control Address)
   1. Frame
   1. Ethernet

1. Lapisan Jaringan (Network Layer):

   1. Router
   1. IP Address (Internet Protocol Address)
   1. ICMP (Internet Control Message Protocol)
   1. Routing Protocols (OSPF, BGP, RIP)
   1. Subnetting

1. Lapisan Transport (Transport Layer):

   1. TCP (Transmission Control Protocol)
   1. UDP (User Datagram Protocol)
   1. Port Number
   1. Flow Control
   1. Error Checking

1. Lapisan Session (Session Layer):

   1. API (Application Programming Interface)
   1. NetBIOS (Network Basic Input/Output System)
   1. Named Pipes
   1. RPC (Remote Procedure Call)
   1. Sockets

1. Lapisan Presentasi (Presentation Layer):

   1. Encryption/Decryption
   1. Data Compression
   1. ASCII (American Standard Code for Information Interchange)
   1. JPEG (Joint Photographic Experts Group)
   1. MIME (Multipurpose Internet Mail Extensions)

1. Lapisan Aplikasi (Application Layer):

   1. HTTP (Hypertext Transfer Protocol)
   1. FTP (File Transfer Protocol)
   1. SMTP (Simple Mail Transfer Protocol)
   1. SSH (Secure Shell)
   1. DNS (Domain Name System)

OSI model ini adalah referensi teoritis yang digunakan untuk memahami komunikasi jaringan secara umum.
Sedangkan biasanya implementasi nyata dalam jaringan bisa lebih kompleks dan dapat melibatkan beberapa lapisan sekaligus ataupun menggunakan protokol dan teknologi khusus yang sesuai dengan kebutuhan.

## Pengingat

Berikut kalimat lelucon yang bisa dipakai untuk menghafal/mengingat nama layer pada OSI Model.

Bisa dari layer 1 ke layer 7

| No      | Nama             | Inisial | Pengingat   |
| ------- | ---------------- | ------- | ----------- |
| Layer 1 | **P**hysical     | P       | **P**lease  |
| Layer 2 | **D**ata Link    | D       | **D**o      |
| Layer 3 | **N**etwork      | N       | **N**ot     |
| Layer 4 | **T**ransport    | T       | **T**hrow   |
| Layer 5 | **S**ession      | s       | **S**ausage |
| Layer 6 | **P**resentation | P       | **P**izza   |
| Layer 7 | **A**pplication  | A       | **A**way    |

maupun dari layer 7 ke layer 1,

| No      | Nama             | Inisial | Pengingat  |
| ------- | ---------------- | ------- | ---------- |
| Layer 7 | **A**pplication  | A       | **A**nak   |
| Layer 6 | **P**resentation | P       | **P**ak    |
| Layer 5 | **S**ession      | S       | **S**oleh  |
| Layer 4 | **T**ransport    | T       | **T**idak  |
| Layer 3 | **N**etwork      | N       | **N**akal  |
| Layer 2 | **D**ata Link    | D       | **D**an    |
| Layer 1 | **P**hysical     | P       | **P**intar |
