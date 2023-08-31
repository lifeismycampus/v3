---
layout: post
title: Pengelolaan VLAN antar Switch dengan VLAN Trunking Protocol (VTP)
date: 2022-04-10 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, switching, vlan]
---

## Pengertian

VLAN Trunking Protocol (VTP) adalah protokol jaringan yang digunakan untuk mengelola dan mengkonfigurasi Virtual LAN (VLAN) pada beberapa switch dalam jaringan.

VTP memungkinkan administrator jaringan untuk membuat, menghapus, atau memodifikasi VLAN dari satu switch dan secara otomatis menyebarkan perubahan tersebut ke switch lain dalam jaringan.

VTP bekerja dengan membagi informasi tentang VLAN antar switch dalam jaringan dan menyimpan informasi tersebut dalam basis data VTP.

Informasi ini kemudian diterima oleh switch lain dan digunakan untuk mengelola konfigurasi VLAN mereka.

Dengan VTP ini, administrator jaringan dapat mengelola VLAN secara efisien dan mengurangi risiko kesalahan konfigurasi.

## Mode Port pada Switch

1. Access Link

   Link mode ini dapat mengirim frame hanya pada sebuah VLAN ID yang sama antara perangkat Switch dan PC client. Sedangkan,

1. Trunk Link

   Link mode ini dapat mengirim frame untuk lebih dari 1 VLAN ID yang sama antar perangkat Switch.

## Hubungan antar Switch

1. Stocking,

   yaitu teknik konfigurasi penghubung antar perangkat Switch yang berbeda di mana butuh satu interface penghubung untuk setiap satu buah VLAN ID pada perangkat-perangkat Switch tersebut.

   Misalnya seperti ini

   ![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/01.png){: .normal }

   ataupun juga begini

   ![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/02.png){: .normal }

   sedangkan,

1. Trunking,

   yaitu teknik konfigurasi penghubung antar perangkat Switch yang berbeda di mana butuh hanya sebuah interface penghubung untuk dapat meng-handle lebih dari satu VLAN ID.

   Contohnya seperti ini

   ![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/03.png){: .normal }

   maupun begini

   ![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/04.png){: .normal }

## Mode pada VTP

VLAN Trunking Protocol (VTP) memiliki 3 mode operasi

1. Mode Server

   Mode ini memungkinkan switch untuk membuat, menghapus, atau memodifikasi VLAN dan membagikan informasi VLAN ke switch lain dalam jaringan.

   Switch yang beroperasi dalam mode server VTP dapat menjadi sumber informasi VLAN untuk switch lain.

2. Mode Client

   Mode ini memungkinkan switch untuk menerima informasi VLAN dari switch server VTP dan menggunakannya untuk mengelola konfigurasi VLAN.

   Switch yang beroperasi dalam mode client VTP tidak dapat membuat, menghapus, atau memodifikasi VLAN.

3. Mode Transparent

   Mode ini memungkinkan switch untuk mengelola konfigurasi VLAN secara lokal, tanpa menerima atau membagikan informasi VLAN dengan switch lain dalam jaringan.

   Switch yang beroperasi dalam mode transparent VTP tidak mempengaruhi atau terpengaruh oleh switch lain dalam jaringan.

Berikut perbandingan kemampuan antar mode operasi

|                            | VTP Server | VTP Client | VTP Trans  |
| -------------------------- | ---------- | ---------- | ---------- |
| Create/ Modify/Delete VLAN | Yes        | No         | Only local |
| Synchronize itself         | Yes        | Yes        | No         |
| Forwards advertisements    | Yes        | Yes        | Yes        |

## Domain

Domain VTP adalah nama unik yang diberikan pada jaringan switch yang menggunakan VLAN Trunking Protocol (VTP).

Setiap switch dalam jaringan harus memiliki domain yang sama agar dapat berkomunikasi dan berbagi informasi tentang VLAN.

VTP memungkinkan administrator jaringan untuk membatasi jangkauan pembagian informasi VLAN hanya pada switch yang berada dalam domain yang sama.

Ini memastikan bahwa hanya switch yang berada dalam domain yang sama yang akan memperbarui konfigurasi VLAN mereka berdasarkan informasi yang diterima dari server VTP.

Pembatasan domain VTP juga membantu dalam memisahkan jaringan switch yang berbeda agar tidak saling mempengaruhi.

Misalnya, jika ada dua jaringan switch yang berbeda dengan domain VTP yang berbeda, maka mereka tidak akan saling mempengaruhi dan saling berbagi informasi tentang VLAN.

![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/05.png){: .normal }

## Advertisement

Advertisement VTP adalah pengiriman informasi VLAN dari satu switch ke switch lain dalam jaringan yang menggunakan VLAN Trunking Protocol (VTP).

Informasi ini diterima oleh switch lain dan digunakan untuk memperbarui konfigurasi VLAN mereka.

Advertisement VTP dapat berupa perubahan pada VLAN, seperti penambahan, penghapusan, atau modifikasi VLAN.

Berikut adalah beberapa jenis paket yang dikirimkan dalam proses Advertisement VTP:

1. Summary Advertisement

   paket ini berisi informasi ringkas tentang VLAN yang ada dalam jaringan dan digunakan untuk memperbarui konfigurasi VLAN pada switch.

2. Subset Advertisement

   paket ini berisi informasi detil tentang VLAN dan digunakan untuk memperbarui konfigurasi VLAN pada switch yang memerlukan informasi lebih detail.

3. Request Advertisement

   paket ini digunakan oleh switch untuk meminta informasi VLAN dari switch lain dalam jaringan.

4. Join/Leave Advertisement

   paket ini berisi informasi tentang switch yang bergabung atau keluar dari jaringan dan digunakan untuk memperbarui informasi tentang switch dalam jaringan.

5. Mismatch Advertisement

   paket ini berisi informasi tentang perbedaan informasi VLAN pada switch dalam jaringan dan digunakan untuk memperbarui konsistensi informasi VLAN.

Packet pada VTP di atas akan dikirimkan keluar masuk melalui trunk link / media transmisi yang digunakan antar perangkat Switch.

![](/assets/img/2022-04-10-pengelolaan-vlan-antar-switch-menggunakan-vlan-trunking-protocol-vtp/06.png){: .normal }

## Sinkronisasi Database

Proses sinkronisasi database VTP dilakukan melalui pengiriman advertisement VTP dari switch ke switch lain dalam jaringan.

Setiap kali perubahan dilakukan pada VLAN, switch akan mengirimkan advertisement VTP ke switch lain dalam jaringan untuk memperbarui konfigurasi VLAN mereka.

Setelah menerima advertisement VTP, switch akan memperbarui database VLAN mereka sesuai dengan informasi yang diterima.

Proses ini akan berulang hingga semua switch dalam jaringan memiliki database VLAN yang sama dan konsisten.

## Configuration Revision Number

Configuration Revision Number adalah nomor yang unik yang digunakan untuk mengidentifikasi versi terbaru dari konfigurasi VLAN pada jaringan.

Setiap kali perubahan dilakukan pada konfigurasi VLAN, Configuration Revision Number akan bertambah.

Proses ini memastikan bahwa setiap switch dalam jaringan memiliki informasi konfigurasi VLAN yang terbaru dan konsisten.

Ketika switch menerima advertisement VTP, switch akan membandingkan Configuration Revision Number yang diterima dengan Configuration Revision Number yang mereka miliki.

Jika Configuration Revision Number yang diterima lebih tinggi, switch akan memperbarui database VLAN mereka sesuai dengan informasi yang diterima.
