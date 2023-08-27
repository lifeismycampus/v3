---
layout: post
title: Enhanced Interior Gateway Routing Protocol (EIGRP) sebagai Protokol Routing
date: 2023-02-05 00:00 +0000
author: angga
categories: [ Materi, Teori ]
tags: [ cisco, routing ]
---

## Pengertian

Enhanced Interior Gateway Routing Protocol (EIGRP) adalah protocol routing yang dikembangkan oleh Cisco. 

Protocol ini didasarkan pada pengembangan dari protokol IGRP asli dan digunakan untuk memfasilitasi pertukaran informasi rute antara dua atau lebih router dalam jaringan yang sama. 

EIGRP adalah protokol dengan tipe hybrid, yang artinya merupakan penggabungan fitur routing protocol dengan tipe distance vector dan link state. 

EIGRP dinilai sebagai protokol sangat efisien yang menyediakan waktu konvergensi yang cepat, penggunaan bandwidth yang minimal, dan skalabilitas yang tinggi. 

EIGRP juga memiliki kemampuan pemilihan rute tingkat lanjut, yang memungkinkan pembuatan beberapa jalur antara dua node. 

Protokol ini juga dilengkapi dengan berbagai opsi otentikasi dan enkripsi untuk memastikan transmisi data yang aman. 

EIGRP banyak digunakan dalam jaringan besar, terutama yang menggunakan produk Cisco, dan merupakan alternatif populer selain menggunakan protokol routing OSPF.

## Cara Kerja

EIGRP bekerja dengan membuat dan menjaga informasi tabel berisi router tetangga yang terdiri dari router yang berbagi rute dalam jaringan. 

Setiap kali router mengirimkan pesan update, pesan tersebut dikirim ke semua router di tabel tetangganya. 

Router-router lainnya kemudian menggunakan informasi update tersebut untuk membuat tabel perutean yang berisi rute terbaik untuk setiap tujuan dalam jaringan. 

Informasi ini kemudian digunakan untuk mengirim data ke tujuan yang benar. 

Protokol ini juga mencakup fitur-fitur seperti transmisi yang andal, konvergensi cepat, dan kemampuan pemilihan rute tingkat lanjut untuk memastikan jalur perutean yang optimal. 

Selain itu, EIGRP dapat mendeteksi perubahan dalam topologi jaringan, langsung memperbarui tabel tetangga, dan menghitung ulang rute terbaik untuk setiap tujuan. 

Ini membantu memastikan bahwa data selalu dirutekan di sepanjang jalur terbaik dan bahwa jaringan tetap stabil dan efisien. 

## Algoritma DUAL

Dalam operasinya untuk terhubung dengan router lain, EIGRP menggunakan paket bernama RTP (Reliable Transport Protocol) yang memiliki keandalan yang tinggi. 

Ketika router mengirim pembaruan/update, jika pembaruan tersebut diterima oleh router yang dituju, maka router penerima akan memberikan konfirmasi ACK (Acknowledges). 

Algoritma yang digunakan oleh EIGRP berbeda dari algoritma lainnya karena menggunakan algoritma DUAL (Diffusing Update Algorithm). 

Beberapa istilah yang digunakan dalam algoritma DUAL yang digunakan oleh EIGRP adalah sebagai berikut:

1. Successor

    Merupakan jalur terbaik yang dipilih berdasarkan biaya terendah untuk mencapai network tujuan.

1. Feasible Successor (FS)

    Merupakan rute cadangan yang digunakan ketika Successor mengalami masalah.

1. Feasible Distance (FD)

    Merupakan nilai metric terkecil yang diperoleh untuk mencapai network tujuan.

1. Reported Distance (RD)

    Merupakan nilai metric yang dilaporkan oleh router neighbor ketika jalur utama ke network tujuan mengalami masalah.

1. Feasible Condition (FC)

    Merupakan syarat yang harus dipenuhi agar router neighbor dapat menjadi FS. 
    
    Apabila nilai metric RD dari router neighbor lebih kecil dari FD jalur utama, maka router neighbor tersebut dianggap layak menjadi FS.

## Perhitungan Metric

EIGRP menggunakan berbagai metric untuk menentukan rute terbaik, seperti jumlah hop, bandwidth, delay, dan reliability.

1. Hop count

    Hop count adalah jumlah router yang harus dilewati paket data untuk mencapai tujuannya, dengan cara menghitung jumlah router perantara antara sumber dan tujuan.
    
    Metric ini berguna jika latensi dalam jaringan menjadi perhatian karena jumlah hop dapat memberikan perkiraan berapa lama waktu yang dibutuhkan paket untuk mencapai tujuannya. 
    
    Selain itu, jumlah hop berguna untuk menentukan rute yang paling efisien karena memungkinkan router untuk memilih rute dengan jumlah hop paling sedikit.

2. Bandwidth

    Bandwidth adalah jumlah data yang dapat ditransmisikan melalui koneksi jaringan dalam jangka waktu tertentu. 
    
    Saat menghitung rute terbaik untuk suatu tujuan, EIGRP memperhitungkan bandwidth maksimum yang tersedia dari koneksi antara dua router.
    
    Metric ini berguna untuk jaringan yang memerlukan throughput tinggi, seperti streaming video atau transfer file besar. 
    
    Proses ini memastikan bahwa data ditransmisikan dengan cepat dan andal dengan memilih rute dengan bandwidth tertinggi yang tersedia. 
    
    Semakin besar bandwidth yang tersedia di sepanjang rute, semakin baik kinerja jaringan.
    
3. Delay

    Delay adalah jumlah waktu yang dibutuhkan paket data untuk mencapai tujuannya. 
    
    Delay dihitung dengan mengukur jumlah total waktu yang dibutuhkan untuk setiap router perantara untuk memproses paket. 
    
    Metric ini berguna untuk jaringan yang memerlukan latensi rendah, seperti Voice over IP atau streaming video real-time. 
    
    Semakin rendah delay di sepanjang rute, semakin baik kinerja jaringan. 
    
4. Reliability

    Reliability adalah ukuran keandalan suatu link (media penghubung antar node), keandalan yang dimaksud adalah dengan mempertimbangkan jumlah error pada suatu link serta berapa lama waktu yang dibutuhkan untuk memulihkan suatu link setelah terjadi error. 
    
    Semakin andal/reliable suatu link, maka semakin andal pula koneksinya. 
    
    EIGRP memperhitungkan keandalan suatu link saat menghitung rute terbaik untuk suatu tujuan, memastikan bahwa data dirutekan dengan andal dan efisien. 
    
    Reliability berguna untuk jaringan yang membutuhkan tingkat keandalan yang tinggi, seperti perbankan dan keuangan, di mana data perlu ditransfer dengan aman dengan gangguan minimal.

## Karakteristik

Walau sangat populer digunakan, bahkan dapat dikatakan sebagai alternatif dari OSPF, tentu saja EIGRP mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Kelebihan

Berikut ini adalah beberapa kelebihan dari penerapan EIGRP sebagai routing protocol

1. Waktu konvergensi yang cepat

    EIGRP dapat dengan cepat menemukan alternatif path setelah perubahan jaringan, sehingga menghasilkan gangguan minimal pada jaringan. 

2. Penggunaan bandwidth rendah

    EIGRP menggunakan bandwidth lebih sedikit daripada protokol perutean lainnya, yang membantu mengurangi lalu lintas jaringan dan menghemat sumber daya.

3. Kemampuan untuk mengikuti skala jaringan

    EIGRP mampu menangani jaringan besar dan menskalakan dengan mudah seiring pertumbuhan jaringan. 

4. Otentikasi yang aman

    EIGRP memiliki fitur keamanan bawaan yang melindungi dari akses tidak sah dan serangan berbahaya. 

5. Pemilihan rute yang dinamis

    EIGRP dapat secara dinamis memilih rute terbaik ke tujuan berdasarkan metric. 

6. Penerapan fleksibel

    EIGRP dapat digunakan dalam jaringan hybrid, menjadikannya protokol perutean yang fleksibel dan serbaguna.

### Kekurangan

Berikut merupakan daftar lengkap kekurangan dari implementasi EIGRP sebagai routing protocol

1. Kompleksitas

    EIGRP lebih kompleks daripada protokol perutean lainnya karena pemilihan rute dinamis dan fitur otentikasinya.

2. Skalabilitas terbatas

    EIGRP terbatas dalam hal skalabilitas, karena hanya dapat menangani hingga 255 router dalam satu jaringan.

3. Tidak ada dukungan untuk VPN

    EIGRP tidak mendukung jaringan pribadi virtual, sehingga tidak dapat digunakan di lingkungan VPN.

4. Tidak didukung secara luas

    EIGRP tidak didukung oleh banyak vendor, jadi mungkin tidak menjadi pilihan untuk beberapa jaringan.

5. Kerentanan keamanan
    
    EIGRP rentan terhadap serangan man-in-the-middle dan ancaman keamanan lainnya. 

6. Kemampuan perutean yang terbatas

    EIGRP terbatas dalam hal kemampuan peruteannya, karena tidak dapat merutekan di beberapa sistem otonom.

7. Kurangnya dukungan untuk jenis paket tertentu

    EIGRP tidak mendukung jenis paket tertentu, seperti IPv6.

8. Ketidakmampuan untuk mendukung protokol perutean tertentu

    EIGRP tidak dapat mendukung protokol perutean tertentu, seperti OSPF dan RIP.

9.  Efisiensi yang lebih rendah dalam hal penggunaan bandwidth

    EIGRP kurang efisien dalam hal penggunaan bandwidth dibandingkan protokol perutean lainnya.
    
10. Rentan terhadap packet loss

    EIGRP dapat rentan terhadap packet loss dalam skenario tertentu.