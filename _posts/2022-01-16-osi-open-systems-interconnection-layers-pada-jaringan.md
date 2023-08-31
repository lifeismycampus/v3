---
layout: post
title: OSI (Open Systems Interconnection) Layers sebagai Standarisasi Jaringan Komputer
date: 2022-01-16 00:00 +0000
author: angga
categories: [Teori]
tags: [osi]
---

## Pengertian

OSI (Open Systems Interconnection) Layers mewakili kerangka arsitektur jaringan komputer yang dikembangkan oleh ISO (Organisasi Internasional untuk Standardisasi).

Fungsi sistem ini adalah mengkoordinasikan interaksi serta pengiriman data melalui jaringan komputer.

Lebih dari itu, Model OSI juga mencerminkan standar pada perangkat jaringan komputer. Artinya, ini adalah panduan yang mengatur bagaimana produk-produk perangkat jaringan dari berbagai pemasok dapat saling berkomunikasi, memastikan kesesuaian dan kegunaan yang saling mendukung.

Model ini berperan sebagai alat dasar, menguraikan tugas dan tanggung jawab masing-masing lapisan dalam proses jaringan. Hal ini tidak hanya meningkatkan pemahaman tentang pengiriman data, tetapi juga berkontribusi pada manajemen jaringan yang efisien dan perbaikan masalah.

Secara esensial, Lapisan OSI mencakup kompleksitas komunikasi jaringan modern, memfasilitasi interoperabilitas dan koherensi dalam dunia yang luas dari jaringan komputer.

## Standarisasi

Protokol adalah serangkaian aturan yang menentukan cara data dikirimkan antara perangkat yang berbeda dalam jaringan.

Sebelum adanya standar jaringan yang terstruktur seperti Model OSI, dunia jaringan komputer berada dalam kekacauan. Setiap penyedia mengembangkan model jaringan sesuai kebijakan mereka sendiri, tanpa koordinasi yang efektif. Hasilnya, komunikasi antara perangkat dari vendor yang berbeda sering kali rumit, tidak efisien, dan seringkali tidak kompatibel. Kegelisahan ini mencakup pembuatan protokol unik dan pemahaman yang rumit tentang bagaimana perangkat dari berbagai vendor bisa berkomunikasi.

Namun, setelah standar jaringan seperti Model OSI diterapkan, terjadi perubahan signifikan. Model ini memberikan panduan yang terstruktur, membagi komunikasi jaringan menjadi lapisan-lapisan yang terdefinisi dengan jelas. Ini membantu dalam pemahaman yang lebih baik tentang cara data dikirim dan diterima antara perangkat yang berbeda. Setiap lapisan memiliki peran unik dalam proses komunikasi, yang memungkinkan pengembangan perangkat dan protokol yang saling berkompatibilitas dengan mudah. Ini mengurangi kompleksitas, memfasilitasi interoperabilitas, dan menghasilkan jaringan yang lebih teratur, efisien, dan mudah dikelola.

Dengan adopsi Model OSI, standarisasi menjadi pijakan untuk kolaborasi antar vendor dan integrasi yang lebih baik antara perangkat jaringan. Ini mengubah lanskap jaringan komputer secara menyeluruh, membuka pintu bagi pengembangan teknologi dan aplikasi yang lebih maju dan efisien.

## Lapisan

Berikut adalah penjelasan masing-masing layer pada Model OSI

### Lapisan Fisik (Physical Layer)

Lapisan Fisik adalah fondasi dari Model OSI, bertanggung jawab atas transmisi sinyal fisik melalui media komunikasi. Ini mencakup aspek teknis seperti tegangan, frekuensi, dan tipe kabel yang digunakan. Lapisan ini mirip dengan dasar dalam pembangunan gedung - tanpa pondasi yang kuat, semua lapisan di atasnya tidak akan berfungsi dengan baik.

Berikut contoh perangkat/layanan pada physical layer

1. Kabel UTP (Unshielded Twisted Pair)
2. Kabel Coaxial
3. Kabel Serat Optik
4. Hub (Repeater Hubs)
5. NIC (Network Interface Card)

### Lapisan Data Link (Data Link Layer)

Lapisan Data Link memastikan pengiriman data yang andal melalui media fisik. Ini mengatur aliran data dalam bentuk frame serta mengenali dan memperbaiki kesalahan pada level fisik. Kita dapat mengibaratkan ini sebagai 'pengawal' yang memeriksa paket data sebelum dikirimkan, mirip dengan petugas keamanan di gerbang masuk.

Berikut contoh perangkat/layanan pada data link layer

1. Switch
2. Bridge
3. MAC Address (Media Access Control Address)
4. Frame
5. Ethernet

### Lapisan Jaringan (Network Layer)

Lapisan Jaringan mengarahkan dan mengelola aliran data antar jaringan. Fungsi utamanya adalah menemukan jalur terbaik untuk mengirim data dari titik A ke titik B melalui berbagai jaringan. Ini adalah bagian 'navigator' dari Model OSI, menentukan jalur yang paling efisien untuk paket data.

Berikut contoh perangkat/layanan pada network layer

1. Router
2. IP Address (Internet Protocol Address)
3. ICMP (Internet Control Message Protocol)
4. Routing Protocols (OSPF, BGP, RIP)
5. Subnetting

### Lapisan Transport (Transport Layer)

Lapisan Transport mengatur komunikasi antara dua perangkat akhir. Ini memastikan pengiriman data yang dapat diandalkan, tersegmentasi, dan diurutkan. Mirip dengan 'pengendara kendaraan pengantar', lapisan ini mengawal paket data agar tiba di tujuan dengan tepat dan teratur.

Berikut contoh perangkat/layanan pada transport layer

1. TCP (Transmission Control Protocol)
2. UDP (User Datagram Protocol)
3. Port Number
4. Flow Control
5. Error Checking

### Lapisan Sesi (Session Layer)

Lapisan Sesi bertanggung jawab atas pembuatan, pengendalian, dan penghentian sesi komunikasi antara dua perangkat. Ini seperti 'manajer rapat' dari Model OSI, memastikan interaksi berjalan lancar dan dapat dikelola antara pengirim dan penerima.

Berikut contoh perangkat/layanan pada session layer

1. API (Application Programming Interface)
1. NetBIOS (Network Basic Input/Output System)
1. Named Pipes
1. RPC (Remote Procedure Call)
1. Sockets

### Lapisan Presentasi (Presentation Layer)

Lapisan Presentasi bertugas menerjemahkan data ke format yang dapat dimengerti oleh penerima. Ini juga mengenkripsi dan mendekripsi data jika diperlukan. Kita bisa memandang ini sebagai 'penerjemah' di Model OSI, memastikan bahwa pesan yang dikirimkan dan diterima dapat dimengerti dengan jelas.

Berikut contoh perangkat/layanan pada presentation layer

1. Encryption/Decryption
1. Data Compression
1. ASCII (American Standard Code for Information Interchange)
1. JPEG (Joint Photographic Experts Group)
1. MIME (Multipurpose Internet Mail Extensions)

### Lapisan Aplikasi (Application Layer)

Lapisan Aplikasi adalah lapisan paling atas, yang berinteraksi langsung dengan pengguna akhir. Ini adalah pintu gerbang bagi aplikasi dan layanan yang digunakan pengguna, seperti peramban web dan surel elektronik. Seperti 'resepsionis' di Model OSI, lapisan ini menyambut permintaan pengguna dan mengatur akses ke layanan yang diperlukan.

Berikut contoh perangkat/layanan pada application layer

1. HTTP (Hypertext Transfer Protocol)
1. FTP (File Transfer Protocol)
1. SMTP (Simple Mail Transfer Protocol)
1. SSH (Secure Shell)
1. DNS (Domain Name System)

Model OSI merupakan kerangka teoritis yang digunakan sebagai acuan dalam memahami komunikasi jaringan secara umum. Namun, dalam implementasinya di dunia nyata, jaringan sering kali menghadirkan kompleksitas yang lebih tinggi. Implementasi ini bisa melibatkan berbagai lapisan secara simultan atau mengadopsi protokol serta teknologi spesifik yang sesuai dengan kebutuhan yang ada.

![](/assets/img/2022-01-16-osi-open-systems-interconnection-layers-pada-jaringan/01.png){: .normal }

Dalam dunia yang terus berkembang ini, Model OSI tetap menjadi landasan penting, memberikan pemahaman mendalam tentang komunikasi jaringan. Meskipun implementasi jaringan bisa jauh lebih kompleks, pemahaman tentang prinsip-prinsip Model OSI tetap menjadi kunci untuk mengelola dan mengoptimalkan koneksi jaringan.

## Pengingat Nama Layers

Berikut kalimat lelucon yang bisa dipakai untuk kemudahan mengingat nama layer pada OSI Model.

dari Layer 1 ke Layer 7

| No      | Nama         | Inisial | Pengingat |
| ------- | ------------ | ------- | --------- |
| Layer 1 | Physical     | P       | Please    |
| Layer 2 | Data Link    | D       | Do        |
| Layer 3 | Network      | N       | Not       |
| Layer 4 | Transport    | T       | Throw     |
| Layer 5 | Session      | s       | Sausage   |
| Layer 6 | Presentation | P       | Pizza     |
| Layer 7 | Application  | A       | Away      |

maupun Layer 7 ke Layer 1

| No      | Nama         | Inisial | Pengingat |
| ------- | ------------ | ------- | --------- |
| Layer 7 | Application  | A       | Anak      |
| Layer 6 | Presentation | P       | Pak       |
| Layer 5 | Session      | S       | Soleh     |
| Layer 4 | Transport    | T       | Tidak     |
| Layer 3 | Network      | N       | Nakal     |
| Layer 2 | Data Link    | D       | Dan       |
| Layer 1 | Physical     | P       | Pintar    |
