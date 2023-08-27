---
layout: post
title: Open Shortest-Path First (OSPF) sebagai Protokol Routing pada Jaringan Komputer
date: 2023-01-15 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, routing]
---

## Pengertian

Protokol routing OSPF (Open Shortest Path First) adalah salah satu jenis protokol routing yang digunakan untuk menentukan jalur terpendek yang harus ditempuh data untuk mencapai tujuannya di jaringan komputer.

OSPF digunakan untuk mengelola tabel routing secara dinamis di jaringan yang menggunakan Internet Protocol (IP).

Protokol routing OSPF (Open Shortest Path First) adalah protokol routing yang dikembangkan oleh Internet Engineering Task Force (IETF).

OSPF sangat cocok digunakan pada jaringan yang besar dan kompleks, seperti jaringan internet atau jaringan korporat.

OSPF juga merupakan salah satu routing protocol yang paling banyak digunakan di dunia.

## Cara Kerja

OSPF bekerja dengan membuat abstraksi dari topologi jaringan menjadi area-area yang terkoneksi.

Setiap router di jaringan tersebut bertukar informasi dengan router-router lainnya mengenai jalur terpendek yang dapat dilalui data.

Dengan demikian, OSPF memungkinkan jaringan untuk secara otomatis mengadaptasi perubahan topologi dan mengupdate tabel routing sesuai dengan perubahan tersebut.

### Link State

Maksud dari istilah `link state` pada OSPF merujuk pada informasi mengenai topologi jaringan yang disimpan oleh setiap router di jaringan.

Setiap router di jaringan OSPF akan menyimpan informasi mengenai semua router, link, dan subnet yang terhubung ke area yang bersangkutan.

Informasi ini disimpan dalam sebuah database yang disebut dengan link state database.

### Algoritma Dijkstra

Algoritma Dijkstra adalah salah satu algoritma pencarian jalur terpendek yang dikembangkan oleh seorang ilmuwan komputer Belanda bernama Edsger W. Dijkstra pada tahun 1959.

Algoritma ini sangat berguna untuk mencari jalur terpendek dari satu titik ke titik lainnya di jaringan yang memiliki beragam bobot atau biaya untuk setiap sambungan.

OSPF (Open Shortest Path First) menggunakan algoritma Dijkstra untuk menemukan jalur terpendek yang harus dilalui data agar sampai ke tujuannya di jaringan.

### Perhitungan Metric

OSPF menghitung metric atau biaya untuk setiap jalur yang mungkin dilalui, dan kemudian menggunakan algoritma Dijkstra untuk memilih jalur terpendek berdasarkan metric tersebut.

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/01.png){: .normal }

Pada umumnya, OSPF menggunakan salah satu dari dua cara menghitung metric, yaitu:

1. metric berdasarkan bandwidth

   OSPF menghitung metric berdasarkan bandwidth terkecil dari link yang terhubung ke router.

   Semakin besar bandwidth suatu link, maka semakin kecil metric yang dihitung untuk link tersebut.

1. metric berdasarkan delay

   OSPF menghitung metric berdasarkan delay terbesar dari link yang terhubung ke router.

   Semakin kecil delay suatu link, maka semakin kecil metric yang dihitung untuk link tersebut.

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/02.png){: .normal }

Setelah metric dari setiap link dihitung, OSPF kemudian menggunakan algoritma Dijkstra untuk menemukan jalur terpendek yang harus dilalui data.

Jalur terpendek ini merupakan jalur dengan metric terkecil yang ditemukan oleh algoritma Dijkstra.

## Routing Table

Berikut adalah beberapa tipe tabel yang dibangun oleh OSPF, antara lain

1. Neighbor Table

   dikenal juga sebagai adjacency database yang berguna untuk menampilkan informasi directly connected router (neighbors).

2. Database Table

   yang dapat disebut juga sebagai LSDB (Link State Database) yang berguna untuk menampilkan semua kemungkinan informasi.

3. Routing Table

   berguna untuk menampilkan best route menuju network destination.

### Update pada Routing Table

Untuk melakukan update tabel routing, OSPF menggunakan beberapa tipe paket yang disebut dengan LSA (Link State Advertisement).

LSA ini berisi informasi tentang topologi jaringan di area yang bersangkutan, termasuk informasi mengenai router, link, dan subnet yang terhubung ke area tersebut.

Setiap router di jaringan OSPF akan mengirimkan LSA ke semua router lainnya di area yang sama, sehingga setiap router akan memiliki informasi yang sama mengenai topologi jaringan di area tersebut.

Kemudian, setiap router akan menggunakan informasi yang dikumpulkan dari LSA untuk membangun tabel routing yang menunjukkan jalur terpendek yang harus dilalui data agar sampai ke tujuannya.

Jika terjadi perubahan topologi jaringan, OSPF akan mengirimkan LSA baru ke semua router lainnya di area yang sama, sehingga setiap router dapat memperbarui tabel routingnya sesuai dengan perubahan tersebut.

Dengan demikian, OSPF dapat secara otomatis mengelola perubahan topologi jaringan dan mengupdate tabel routing secara dinamis.

### Paket

Berikut ini adalah beberapa tipe paket yang dipertukarkan oleh OSPF, antara lain

1. Hello

   Paket Hello digunakan untuk menyatakan keberadaan router di jaringan OSPF.

   Setiap router akan terus-menerus mengirimkan paket Hello ke semua router lainnya di jaringan untuk menjaga koneksi.

1. DD (Database Description)

   Paket DD digunakan untuk menyatakan kepada router lain apa yang terdapat dalam link state database masing-masing.

   Setiap router akan mengirimkan paket DD ke semua router lainnya untuk memperkenalkan link state database yang dimilikinya.

1. LSR (Link State Request)

   Paket LSR digunakan untuk meminta informasi mengenai link state database dari router lain.

   Jika ada informasi yang tidak lengkap atau tidak sesuai dengan yang dimiliki oleh router tersebut, maka router akan mengirimkan paket LSR untuk meminta informasi tersebut.

1. LSA (Link State Advertisement)

   Paket LSA merupakan paket yang mengandung informasi mengenai link state database yang dimiliki oleh router tersebut.

   Paket LSA ini akan dikirimkan ke semua router lainnya di jaringan untuk memperbarui link state database yang dimiliki oleh masing-masing router.

1. LSAck (Link State Acknowledgment)

   Paket LSAck merupakan paket yang digunakan untuk mengkonfirmasi penerimaan paket LSA oleh router lain.

   Setiap router akan mengirimkan paket LSAck kepada router yang sudah menerima paket LSA tersebut, untuk memberikan konfirmasi bahwa paket tersebut telah diterima dengan baik.

1. LSUpd (Link State Update)

   Paket LSUpd merupakan paket yang digunakan untuk memperbarui link state database yang dimiliki oleh router.

   Setiap router akan mengirimkan paket LSUpd kepada semua router lainnya di jaringan, untuk memperbarui link state database yang dimiliki masing-masing router.

1. LSReq (Link State Request)

   Paket LSReq merupakan paket yang digunakan untuk meminta informasi mengenai link state database dari router lain.

   Jika ada informasi yang tidak lengkap atau tidak sesuai dengan yang dimiliki oleh router tersebut, maka router akan mengirimkan paket LSReq untuk meminta informasi tersebut.

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/03.png){: .normal }

## Area

Berikut adalah beberapa tipe area yang ada dalam jaringan OSPF, ialah

1. Standar Area

   adalah area standar yang digunakan oleh OSPF. Area ini dapat
   menerima link update intra-area, route summaries, inter-area dan rute external

1. Backbone Area

   adalah pusat dari OSPF, dimana semua area akan terkoneksi langsung pada area ini. Area ini akan selalu diberi label area 0 (zero). Pertukaran informasi routing network terjadi pada area ini.

1. Stub Area

   disebut ujung dari Network. Database nya berisi rute network internal dan sebuah rute default.

1. Totally Stub Area

   adalah area yang mirip dengan Stub Area. Database nya berisi rute untuk area sendiri dan sebuah rute default.

1. Not-So-Stubby-Area (NSSA)

   adalah area yang database nya berisi rute internal dan sebuah optional route default. Rute-rute didistribusikan ulang dari sebuah proses routing yang terkoneksi.

1. Totally NSSA

   adalah Area yang hanya didesain untuk perangkat Cisco

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/04.png){: .normal }

## Router

Beberapa jenis router yang dapat digunakan dalam jaringan OSPF, yaitu

1. Internal Router

   router yang terhubung ke satu area saja dalam jaringan OSPF.

1. Area Border Router (ABR)

   router yang terhubung ke lebih dari satu area dalam jaringan OSPF. ABR ini berfungsi sebagai penghubung antar area dalam jaringan.

1. Autonomous System Boundary Router (ASBR)

   router yang terhubung ke jaringan OSPF di satu sisi, dan ke jaringan lain di sisi lain. ASBR ini berfungsi sebagai penghubung antar jaringan yang menggunakan routing protocol yang berbeda.

1. Backbone Router

   router yang terhubung ke backbone area dalam jaringan OSPF. Backbone area merupakan area yang terhubung ke semua area lain dalam jaringan.

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/05.png){: .normal }

### Router Utama

Router-router selalu berusaha adjacent dengan router tetangganya berdasarkan paket hello yang diterima.

![](/assets/img/2023-01-15-protokol-routing-open-shortest-path-first-ospf/06.png){: .normal }

Dalam jaringan multi access, router memilih Designated Router (DR) dan Backup Designated Router (BDR) dan mencoba adjacent dengan kedua router tersebut.

1. Designated Router (DR)

   Router ini dipilih dengan berbagai tahapan, yaitu mulai dari nilai priority tertinggi, router id tertinggi, loopback tertinggi ataupun interface dengan IPv4 tertinggi.

   DR bertugas sebagai pengumpul paket dari seluruh router. DR bertanggung jawab mendistribusikan informasi routing (mensinkronisasi) untuk semua router baik intra area (area yang sama) maupun inter area (area yang berbeda).

1. Backup Designated Router (BDR)

   BDR dipilih secara umum sama dengan DR namun nilai tertinggi setelahnya, misal priority tertinggi kedua, router id tertinggi kedua, loopback tertinggi kedua ataupun interface dengan IPv4 tertinggi kedua.

   Inti peran dari BDR adalah selalu memeriksa keadaan DR dan memastikannya tetap dalam keadaan hidup. Lalu, menggantikan peran DR jika DR terdeteksi dalam kondisi down atau mati.

## Karakteristik

Walau sangat populer digunakan, tentu saja OSPF mempunyai kelebihan dan kekurangan sebagai karakteristiknya

### Kelebihan

Routing protocol OSPF (Open Shortest Path First) memiliki beberapa kelebihan dibandingkan dengan protocol routing lainnya, seperti

1. Mampu mengelola jaringan yang besar

   OSPF mampu mengelola jaringan yang besar dengan baik, karena dapat membagi jaringan menjadi beberapa area yang terkoneksi.

   Dengan demikian, topologi jaringan menjadi lebih mudah dikelola, sehingga tidak terjadi kemacetan data.

1. Menggunakan algoritma Dijkstra

   Algoritma Dijkstra merupakan salah satu algoritma yang paling efisien untuk mencari jalur terpendek dalam jaringan.

1. Mampu menangani perubahan topologi jaringan secara dinamis

   OSPF mampu menangani perubahan topologi jaringan secara dinamis, sehingga tabel routing dapat diupdate sesuai dengan perubahan tersebut.

1. Mampu menangani traffic engineering

   OSPF memiliki fitur traffic engineering yang memungkinkan pengaturan traffic di jaringan dengan lebih baik.

   Traffic engineering ini dapat digunakan untuk mengontrol pembagian beban traffic di jaringan, sehingga dapat meningkatkan performa jaringan secara keseluruhan.

   Traffic engineering juga dapat digunakan untuk mengalokasikan bandwidth dengan lebih efisien, serta meminimalkan terjadinya kemacetan data di jaringan.

### Kekurangan

Routing protocol OSPF (Open Shortest Path First) tentunya juga memiliki beberapa kekurangan, di antaranya

1. Membutuhkan resource yang cukup besar

   OSPF membutuhkan resource yang cukup besar untuk dapat beroperasi dengan baik, terutama dalam jaringan yang besar.

   Resource yang dibutuhkan seperti CPU, memory, dan bandwidth.

1. Konfigurasi yang cukup rumit

   OSPF memiliki konfigurasi yang cukup rumit dibandingkan dengan protocol routing lainnya.

1. Update tabel routing yang lambat

   OSPF memiliki waktu update tabel routing yang cukup lambat dibandingkan dengan protocol routing lainnya

   Hal ini dapat menyebabkan terjadinya delay dalam proses pengiriman data di jaringan.

1. Tidak dapat digunakan di jaringan yang terpisah

   OSPF tidak dapat digunakan di jaringan yang terpisah, contohnya jaringan yang terhubung ke internet melalui VPN (Virtual Private Network).

1. Membutuhkan koneksi yang stabil

   OSPF membutuhkan koneksi yang stabil agar dapat beroperasi dengan baik.

   Jika terjadi gangguan koneksi, maka proses pengiriman data di jaringan dapat terhambat.

## Wildcard Mask

Wildcard mask adalah deret angka (pola 8 oktet, 32 bit) yang digunakan untuk menentukan akses ke suatu range IP address apakah diijinkan atau ditolak.

Selain digunakan pada protokol routing seperti OSPF dan EIGRP, wildcard mask juga biasanya digunakan pada Access Control List (ACL).

Melakukan perhitungan wildcard mask, mudahnya didapatkan dengan cara membalik nilai pada Subnet Mask.

Jika pada subnet mask nilai biner bernilai 1 maka pada wildcard mask diubah menjadi nilai biner bernilai 0, begitupun untuk subnet mask nilai biner 0 maka diubah menjadi wildcard mask nilai biner 1.

| Prefix | Subnet Mask (Decimal) | Subnet Mask (Biner)                 | Wildcard Mask (Biner)               | Wild Card Mask (Desimal) |
| ------ | --------------------- | ----------------------------------- | ----------------------------------- | ------------------------ |
| /24    | 255.255.255.0         | 11111111.11111111.11111111.00000000 | 00000000.00000000.00000000.11111111 | 0.0.0.255                |
| /30    | 255.255.255.252       | 11111111.11111111.11111111.11111100 | 00000000.00000000.00000000.00000011 | 0.0.0.3                  |
| /27    | ...                   | ...                                 | ...                                 | ...                      |
| /22    | ...                   | ...                                 | ...                                 | ...                      |
| /13    | ...                   | ...                                 | ...                                 | ...                      |
