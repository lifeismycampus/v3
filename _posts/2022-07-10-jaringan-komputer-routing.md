---
layout: post
title: Routing pada Jaringan Komputer
date: 2022-07-10 00:00 +0000
author: angga
categories: [Konsep]
tags: [cisco, routing]
---

## Pengertian

Dalam aturan OSI model, layer ke-3 yaitu Network yang memiliki fungsi utama pengalamatan dan routing.

![](/assets/img/2022-07-10-jaringan-komputer-routing/01.png){: .normal }

Routing pada jaringan berarti teknik konfigurasi yang memungkinkan komunikasi lebih dari satu jaringan, artinya terjadi pengiriman paket dari suatu jaringan ke jaringan yang lain.

## Router

Perangkat jaringan yang dapat bekerja pada layer Network ini salah satunya adalah perangkat Router.

Router sederhananya merupakan sebuah komputer yang sudah ter-install IOS (Internetwork Operating System) sebagai sistem operasinya guna mendukung proses routing di atas dengan cara mencari jalur terbaik (best path).

## Mekanisme Routing

Routing merupakan proses perangkat router meneruskan paket data dari suatu jaringan ke jaringan lain.

![](/assets/img/2022-07-10-jaringan-komputer-routing/02.png){: .normal }

Proses routing pada jaringan dapat dilakukan bila syarat berikut terpenuhi yaitu

1. alamat jaringan tujuan diketahui dengan jelas
2. adanya penentuan jalur terbaik (tercepat, paling efisien)
3. adanya identifikasi terhadap sumber informasi/asal paket data beserta jalur yang dipilih selanjutnya
4. adanya penentuan jalur yang mungkin dilewati yang dapat ditempuh untuk sampai ke tujuan
5. adanya konfirmasi jalur yang ditempuh apakah terpercaya atau tidak, dapat diandalkan atau tidak
6. terciptanya routing table yang bertugas mendefinisikan suatu proses paket data harus di-forward dari jaringan maupun alamat sumber ke tujuan.

Perilaku yang terjadi pada end device yaitu

1. jika alamat IP pengirim dan penerima merupakan dalam jaringan yang sama, maka paket data langsung dikirimkan ke perangkat Switch, sedangkan

2. jika jaringan berbeda, maka paket data akan dikirimkan ke gateway jaringan lokal alamat IP pengirim (interface perangkat router yang terhubung langsung) terlebih dahulu sebelum di kirim ke alamat IP penerima.

## Macam Routing

Ada beberapa metode melakukan konfigurasi routing, antara lain

1. Default Routing
1. Static Routing
1. Dynamic Routing

### Default Routing

Routing Default yaitu proses routing di mana router dikonfigurasi untuk dapat mengirim paket data ke jaringan tujuan yang tidak ada dalam routing table.

Contoh dari pemanfaatan jenis routing ini adalah network administrator melakukan konfigurasi routing suatu jaringan lokal supaya bisa terhubung ke jaringan internet.

![](/assets/img/2022-07-10-jaringan-komputer-routing/03.png){: .normal }

### Static Routing

Routing Statis yaitu proses routing di mana penyusunan routing table dilakukan oleh network administrator secara manual.

Pendaftaran jaringan dari/pada setiap perangkat router dikonfigurasi satu per satu.

Jika ada perubahan topologi jaringan (perangkat, pengalamatan), maka network administrator harus melakukan konfigurasi ulang.

![](/assets/img/2022-07-10-jaringan-komputer-routing/04.png){: .normal }

### Dynamic Routing

Routing Dinamis yaitu proses routing dengan memanfaatkan routing protocol untuk penemuan dan penentuan jaringan maupun jalur terbaik (best path).

Dengan routing protocol maka jalur terkini pada routing table akan selalu ter-update secara otomatis, seperti ketika terjadi perubahan topologi.

Selanjutnya, jika suatu saat jalur utama bermasalah maka otomatis berpindah menggunakan jalur alternatif.

![](/assets/img/2022-07-10-jaringan-komputer-routing/05.png){: .normal }

## Tipe Jaringan

Ada 2 macam, yaitu:

1. Directly-Connected Network

   jaringan ini merupakan jaringan yang terhubung secara langsung. Sedangkan

1. Remote Network

   jaringan ini merupakan jaringan yang tidak terhubung secara langsung, namun harus dilakukan konfigurasi routing.

![](/assets/img/2022-07-10-jaringan-komputer-routing/06.png){: .normal }

Jika dilihat dari router R1, maka

1. LAN 1 dan LAN 2

   merupakan directly-connected network, sedangkan

1. LAN 3 dan LAN 4

   merupakan remote network.

Bagaimana tipe jaringan bila dilihat dari router R2?

## Administrative Distance

Administrative distance merupakan parameter yang menunjukkan keterpercayaan maupun reliabilitas suatu rute menuju jaringan tertentu.

Semakin kecil nilai administrative distance maka protokol tersebut akan semakin dipercaya untuk dipilih.

Beberapa nilai administrative distance sebagai berikut

| Routing Protocol   | Administrative Distance |
| ------------------ | ----------------------- |
| Directly-connected | 0                       |
| Static route       | 1                       |
| Internal EIGRP     | 90                      |
| OSPF               | 110                     |
| RIP                | 120                     |
| External EIGRP     | 170                     |
| Unknown            | 255                     |
