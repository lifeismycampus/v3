---
layout: post
title: Routing Statis pada Jaringan Komputer
date: 2022-08-07 00:00 +0000
author: angga
categories: [ Materi, Teori ]
tags: [ cisco, routing ]
---

## Pengertian

Routing statis adalah mekanisme routing yang routing table-nya dikonfigurasi oleh network administrator secara manual.

## Kebutuhan

Berikut adalah beberapa alasan mengapa suatu jaringan perlu dikonfigurasi dengan routing statis

1. Kontrol atas lalu lintas jaringan
    
    Routing statis memungkinkan administrator jaringan untuk memilih secara spesifik rute mana yang ingin diterima dan diteruskan paket data, sehingga memungkinkan kontrol yang lebih baik atas lalu lintas jaringan.

2. Keamanan
    
    Routing statis tidak memerlukan pertukaran informasi antar perangkat jaringan, sehingga meminimalisir risiko serangan atau masalah keamanan.

3. Jaringan yang tidak terlalu kompleks
    
    Routing statis cocok untuk jaringan yang tidak terlalu kompleks dan tidak memiliki perubahan yang sering pada topologi jaringan.

4. Keandalan
    
    Routing statis tidak terpengaruh oleh masalah koneksi atau kerusakan pada perangkat jaringan, sehingga dapat memastikan keandalan jaringan.

5. Pembatasan bandwith
    
    Routing statis dapat membatasi bandwith yang digunakan oleh jaringan, membuat penggunaan sumber daya jaringan lebih efisien.

## Cara Kerja

Routing statis bekerja dengan memasukkan informasi rute yang dikonfigurasi secara manual ke dalam routing table perangkat router.

Saat paket data harus diteruskan dari satu jaringan ke jaringan lain, perangkat router menggunakan informasi rute pada routing table untuk memutuskan rute mana yang harus diambil.

Setelah rute dipilih, paket data akan diteruskan melalui rute tersebut.

Ini berbeda dengan routing dinamis, di mana perangkat router memperoleh informasi rute secara otomatis melalui pertukaran informasi dengan perangkat jaringan lain.

Konsekuensinya, routing statis memungkinkan kontrol yang lebih baik atas lalu lintas jaringan dan meminimalisir risiko masalah keamanan, tetapi juga membatasi fleksibilitas jaringan dan membutuhkan lebih banyak interaksi manual dari administrator jaringan.

## Terminologi

Beberapa istilah yang penting untuk mengonfigurasi routing statis pada jaringan, yaitu

1. Routing Table

    Merupakan tabel berisi semua data jaringan terdaftar yang digunakan sebagai acuan paket harus dikirim ke suatu jaringan tujuan. 
    
    Routing table hanya terdiri dari jalur terbaik untuk masing-masing destination network.

1. Destination Network

    Merupakan alamat ip suatu jaringan yang disertakan pada routing table sehingga butuh untuk melakukan advertise pada jaringan tersebut.

    Untuk routing statis, jaringan yang dianggap sebagai destination network yaitu jaringan tidak langsung/remote network.

    ![](/assets/img/2022-08-07-routing-statis-pada-jaringan-komputer/01.png){: .normal }

1. Next Hop

    Merupakan interface pada router lain yang terhubung langsung, berperan sebagai penerima paket yang dikirimkan dan penerus ke jaringan tujuan/destination network. 
    
    Konsep interface Next Hop sama dengan Default Gateway ketika melakukan konfigurasi suatu PC Client.

    ![](/assets/img/2022-08-07-routing-statis-pada-jaringan-komputer/02.png){: .normal }

## Karakteristik

Seperti teknik konfigurasi routing yang lain, tentu saja routing statis mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Kelebihan

Berikut adalah beberapa kelebihan dari routing statis

1. Konfigurasi yang lebih mudah
   
    Routing statis memiliki konfigurasi yang lebih sederhana dan mudah dipahami dibandingkan dengan routing dinamis.

2. Lebih stabil
    
    Routing statis tidak terpengaruh oleh kondisi jaringan yang berubah-ubah, sehingga lebih stabil dibandingkan dengan routing dinamis.

3. Fleksibilitas
    
    Routing statis memungkinkan administrator jaringan untuk memilih secara spesifik rute mana yang ingin diterima dan diteruskan paket data.

4. Peningkatan kinerja
   
    Karena tidak ada overhead proses dalam melakukan update tabel routing, maka kinerja perangkat router menjadi lebih baik.

5. Kemampuan prediksi

    Routing statis memungkinkan administrator jaringan untuk memprediksi bagaimana paket data akan berpindah melalui jaringan.

6. Meningkatkan keamanan

    Karena tidak ada informasi tentang rute jaringan yang diterima dan diteruskan secara dinamis, maka resiko keamanan jaringan menjadi lebih rendah.

### Kekurangan

Berikut adalah beberapa kekurangan dari routing statis

1. Kurang efisien
    
    Routing statis tidak mampu menyesuaikan diri dengan perubahan kondisi jaringan, sehingga dapat menyebabkan paket data terblokir atau terakumulasi di satu titik.

2. Konfigurasi yang berulang
   
    Jika ada perubahan pada jaringan, administrator jaringan harus melakukan konfigurasi ulang untuk setiap perubahan tersebut.

3. Sulit untuk mengatasi masalah
    
    Jika terjadi masalah pada jaringan, sulit untuk mengatasinya karena administrator jaringan harus mengkonfigurasi ulang rute-rute yang ada.

4. Kurang fleksibel
    
    Routing statis hanya memungkinkan administrator jaringan untuk memilih satu rute saja untuk mengirim paket data, sehingga kurang fleksibel dibandingkan dengan routing dinamis.

5. Membutuhkan banyak waktu
    
    Konfigurasi routing statis membutuhkan waktu yang lebih lama dibandingkan dengan routing dinamis, karena harus melakukan konfigurasi satu per satu untuk setiap rute yang ada.

## Berlatih

Suatu jaringan disusun seperti topologi jaringan routing statis berikut,

![](/assets/img/2022-08-07-routing-statis-pada-jaringan-komputer/03.png){: .normal }

Tentukan routing table untuk setiap perangkat Router

| Router | Destination Network | Subnet Mask | Next Hop |
| - | - | - | - |
| R1 | ... | ... | ... |
| ... | ... | ... | ... |
| R2 | ... | ... | ... |
| ... | ... | ... | ... |
| R3 | ... | ... | ... |
| ... | ... | ... | ... |