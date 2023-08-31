---
layout: post
title: Pembagian Jaringan secara Virtual Menggunakan Virtual Local Area Network (VLAN)
date: 2022-03-13 00:00 +0000
author: angga
categories: [Konsep]
tags: [cisco, vlan]
---

## Pengertian

VLAN (Virtual Local Area Network) merupakan metode yang memungkinkan pembagian jaringan fisik menjadi beberapa jaringan virtual yang berdiri secara independen, walaupun masih berada dalam satu rangkaian fisik yang sama.

Teknik konfigurasi VLAN ini mengizinkan pengelompokan perangkat jaringan, seperti komputer, server, dan peralatan lainnya, menjadi beberapa kelompok yang memiliki batas logika yang jelas.

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/01.png){: .normal }

Dengan penerapan VLAN, efisiensi dalam manajemen dan kinerja jaringan bisa ditingkatkan dengan memanfaatkan pengelompokan yang cerdas dan intuitif.

VLAN memegang peranan penting dalam menangani masalah collision pada jaringan dengan pendekatan yang efisien yaitu membagi jaringan menjadi beberapa broadcast domain yang terpisah.

Dalam kerangka VLAN, setiap pesan broadcast hanya disampaikan ke port-port yang tergabung dalam VLAN yang sama. Hasilnya, aliran pesan broadcast yang diterima oleh setiap perangkat jaringan menjadi lebih terkontrol.

Langkah ini memberikan manfaat signifikan dalam mengurangi kemungkinan collision dalam jaringan dan juga mengoptimalkan kinerja jaringan secara keseluruhan. Dengan demikian, jaringan mampu mengelola aliran data dengan lebih efisien, mendukung stabilitas jaringan, dan memberikan kontribusi yang berarti terhadap pengalaman pengguna yang lebih baik.

## Perangkat

Manfaat dari VLAN muncul melalui perangkat manageable switch, yang memungkinkan konfigurasi ini diterapkan dan dikelola dengan lebih efektif.

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/02.png){: .normal }

VLAN berfungsi untuk memisahkan secara logika pada tingkat switch, sedangkan subnetting berperan dalam memisahkan pada tingkat router.

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/03.png){: .normal }

## Karakteristik

Seperti halnya dengan segala teknik pemisahan jaringan lainnya, VLAN juga memiliki kelebihan dan kekurangan yang menjadi ciri khasnya.

### Kelebihan

1. Pemisahan dan Pengaturan yang Lebih Baik

   Dengan VLAN, Anda bisa memisahkan perangkat dalam jaringan secara lebih efisien. Ini memungkinkan Anda untuk mengelompokkan perangkat berdasarkan fungsi, departemen, atau keperluan khusus. Pemisahan ini dapat membantu mengoptimalkan kinerja dan manajemen jaringan.

2. Keamanan yang Ditingkatkan

   VLAN memungkinkan Anda untuk membatasi akses antara kelompok perangkat yang berbeda. Hal ini menjaga keamanan data, karena akses hanya diberikan kepada perangkat yang memang membutuhkan. Sebagai contoh, data sensitif dari departemen keuangan dapat diisolasi dari departemen lain, mengurangi risiko peretasan atau akses tidak sah.

3. Efisiensi Penggunaan Bandwidth

   Dengan memisahkan perangkat ke dalam VLAN berdasarkan kebutuhan dan fungsinya, lalu lintas data dapat dikendalikan dengan lebih baik. Ini menghindarkan lonjakan trafik yang tidak terduga dan memastikan bandwidth tersedia secara optimal untuk setiap kelompok perangkat.

4. Penyederhanaan Manajemen

   VLAN memungkinkan untuk mengelola perangkat secara terpusat dan lebih efisien. Administrasi dan konfigurasi dapat dilakukan pada level VLAN, yang memudahkan dalam mengatur perizinan, kebijakan, dan pembaruan perangkat.

5. Fleksibilitas dalam Pengaturan

   Anda bisa merancang konfigurasi jaringan yang fleksibel dan mudah diubah-ubah sesuai kebutuhan. Anda dapat menambah, menghapus, atau memodifikasi VLAN dengan mudah tanpa harus mengubah struktur fisik jaringan.

6. Penghematan Biaya

   Dengan pemisahan yang cerdas menggunakan VLAN, Anda tidak perlu menginstal kabel fisik baru untuk memisahkan perangkat secara fisik. Ini dapat menghemat biaya instalasi dan perawatan infrastruktur fisik.

### Kekurangan

1. Kompleksitas Konfigurasi

   Konfigurasi awal dan pengelolaan VLAN bisa menjadi kompleks terutama untuk jaringan yang lebih besar dan rumit. Membutuhkan pemahaman yang baik tentang struktur jaringan dan konfigurasi perangkat.

1. Penggunaan Sumber Daya

   Dalam beberapa kasus, pembagian perangkat ke dalam VLAN yang terlalu detail dapat memerlukan penggunaan sumber daya yang lebih besar. Ini dapat mengakibatkan overhead administratif dan peningkatan beban kerja.

1. Isolasi Berlebihan

   Pemisahan perangkat ke dalam VLAN yang berlebihan dapat mengakibatkan isolasi berlebihan antara perangkat. Hal ini bisa menghambat komunikasi yang seharusnya terjadi untuk tujuan kerja sama dan berbagi informasi.

1. Kesulitan dalam Pemecahan Masalah

   Pada jaringan yang rumit dengan banyak VLAN, memecahkan masalah dapat menjadi lebih sulit. Melacak masalah lintas VLAN atau mengidentifikasi masalah dalam pengaturan konfigurasi mungkin memerlukan waktu lebih lama.

1. Overhead Pengelolaan

   Mengelola banyak VLAN dengan pengaturan yang rumit bisa memerlukan upaya administratif yang signifikan. Perubahan atau pembaruan pada struktur VLAN dapat memerlukan koordinasi yang cermat dan waktu tambahan.

1. Penggunaan Tidak Efisien

   Jika tidak dirancang dengan baik, VLAN bisa saja tidak memberikan efisiensi yang diharapkan. Misalnya, jika pengelompokan perangkat tidak sesuai dengan kebutuhan sebenarnya, hal ini bisa menghambat aliran informasi yang seharusnya terjadi.

1. Keterbatasan Peralatan

   Tidak semua perangkat jaringan mendukung atau dapat diintegrasikan dengan konfigurasi VLAN. Beberapa perangkat mungkin memerlukan upgrade atau penggantian untuk mendukung implementasi ini.

## Macam

1. Default VLAN (VLAN 1)

   Ini adalah VLAN bawaan dari perangkat switch yang mencakup semua port pada switch tersebut. Meskipun seringkali disarankan untuk mengubah VLAN default untuk keamanan, VLAN ini tetap berperan dalam komunikasi dasar di dalam switch.

1. VLAN Data

   VLAN ini digunakan untuk mengelompokkan perangkat berdasarkan lalu lintas data. Ini membantu dalam memisahkan dan mengelola lalu lintas dari berbagai departemen atau fungsi dalam jaringan.

1. Voice VLAN

   VLAN suara memprioritaskan dan mengelompokkan lalu lintas suara, seperti pada sistem IP telefoni. Ini membantu memastikan kualitas panggilan dan layanan suara yang optimal.

1. Management VLAN

   VLAN pengelolaan digunakan untuk mengelompokkan perangkat administratif dan manajemen jaringan. Ini memungkinkan administrator untuk mengakses perangkat jaringan secara terpisah dari lalu lintas data biasa.

1. Native VLAN

   VLAN asli digunakan pada port trunk untuk menetapkan VLAN default yang digunakan untuk lalu lintas yang tidak ditag atau yang datang tanpa tag.

## Keanggotaan

Terdapat beberapa cara efektif untuk mendaftarkan perangkat dalam suatu VLAN:

1. Keanggotaan Berdasarkan Port (Port Based)

   Metode ini umum digunakan dimana setiap port pada switch dikonfigurasi dengan atribut yang menentukan keanggotaan VLAN. Koneksi perangkat ke port tertentu akan otomatis mengalokasikan keanggotaan perangkat dalam VLAN yang sesuai. Ini mempermudah pengelompokan berdasarkan letak fisik atau tujuan jaringan perangkat.

1. Keanggotaan Berdasarkan Alamat MAC (MAC Based)

   Keanggotaan VLAN dapat ditentukan melalui alamat MAC perangkat. Switch akan memantau alamat MAC yang terhubung ke suatu port dan menentukan VLAN yang sesuai sesuai dengan konfigurasi yang telah ditetapkan. Metode ini cocok untuk perangkat yang sering berpindah-pindah port tetapi tetap harus berada dalam VLAN yang sama.

1. Keanggotaan Berdasarkan Protokol (Protocol Based)

   Protokol seperti IP dapat digunakan untuk menentukan keanggotaan VLAN. Misalnya, perangkat yang menggunakan protokol IP tertentu dapat ditempatkan dalam VLAN yang sesuai, seperti penggunaan VLAN khusus untuk VoIP.

1. Keanggotaan Berdasarkan Subnet IP (IP Subnet Based)

   Pengelompokan perangkat dalam VLAN juga bisa didasarkan pada alamat subnet IP. Perangkat dalam subnet yang sama ditempatkan dalam VLAN yang sesuai, memungkinkan pemisahan lalu lintas berdasarkan lokasi fisik atau fungsi.

1. Keanggotaan Berdasarkan Otentikasi (Authentication Based)

   VLAN juga dapat dikelompokkan berdasarkan hasil otentikasi. Setelah pengguna atau perangkat melewati proses otentikasi, mereka ditempatkan dalam VLAN sesuai aturan yang telah ditetapkan. Ini membantu memisahkan lalu lintas berdasarkan tingkat akses dan keamanan.

## Cara Kerja

Proses kerja VLAN dapat diuraikan sebagai berikut:

1. Pengelompokan

   Langkah awal melibatkan pengelompokan pengguna atau perangkat dalam jaringan berdasarkan kesamaan fungsi, tujuan, atau departemen yang bersangkutan. Ini memungkinkan pemisahan lalu lintas berdasarkan karakteristik tertentu daripada hanya berdasarkan lokasi fisik.

1. Penandaan (Tagging)

   Setiap kali data dikirim oleh pengguna atau perangkat, paket tersebut diberi tanda identifikasi khusus yang dikenal sebagai tag VLAN. Tag ini berfungsi sebagai label yang mengindikasikan asal VLAN paket dan tujuan VLAN yang dituju.

1. Pengalihan (Switching)

   Switch akan memeriksa tag VLAN pada setiap paket data yang tiba. Hanya paket dengan tag VLAN yang sesuai yang akan diarahkan ke pengguna atau perangkat yang tergabung dalam VLAN yang sama. Ini memastikan bahwa lalu lintas hanya dikirim ke penerima yang dimaksudkan.

1. Penghubungan (Bridging)

   Setelah switch menerima paket data, ia akan melakukan bridging atau penghubungan data antara VLAN yang berbeda. Hal ini memastikan bahwa paket data dapat bergerak dengan benar di seluruh jaringan dan mencapai tujuannya.

1. Penghapusan Tanda (Un-tagging)

   Ketika paket data mencapai tujuannya, tanda identifikasi VLAN akan dihapus. Ini memungkinkan paket data diterima dan diolah oleh pengguna atau perangkat tanpa hambatan.

## Standarisasi

1. IEEE 802.1Q (Dot1Q)

   IEEE 802.1Q atau lebih dikenal dengan Dot1Q adalah protokol tagging yang paling umum digunakan dalam implementasi VLAN. Ini adalah standar yang diakui secara internasional yang mengatur cara menandai dan memproses paket data yang terkait dengan VLAN di jaringan Ethernet.

   - Bagaimana Dot1Q Bekerja

     Ketika paket data diteruskan dari switch ke switch, dan dari switch ke router atau host lainnya, paket data diberi tag VLAN yang menyertakan informasi tentang VLAN asalnya. Tag ini mengidentifikasi VLAN yang terlibat dan memungkinkan perangkat di ujung penerimaan untuk memahami VLAN apa yang relevan dengan paket tersebut.

   - Batasan Jumlah VLAN pada Dot1Q

     IEEE 802.1Q memiliki dukungan yang lebih luas dalam hal jumlah VLAN yang dapat diinisiasi. Protokol ini mendukung hingga 4096 VLAN dalam satu jaringan fisik.

1. Cisco ISL (Inter-Switch Link)

   Cisco ISL adalah protokol tagging yang digunakan khusus dalam lingkungan perangkat Cisco. Namun, Cisco ISL sudah tidak lagi umum digunakan karena IEEE 802.1Q (Dot1Q) telah menjadi standar yang lebih umum dan diadopsi secara luas.

   - Bagaimana Cisco ISL Bekerja

     Cisco ISL mengenkapsulasi seluruh paket data asli dalam sebuah frame baru yang berisi informasi tentang VLAN yang terlibat. Frame ini mengangkut paket data asli beserta tag VLAN dalam satu kesatuan, dan frame ini kemudian dikirimkan dalam jaringan.

   - Batasan Jumlah VLAN pada Cisco ISL

     Sebelumnya, Cisco ISL memiliki batas 1005 VLAN dalam satu jaringan fisik.

Perbedaan utama antara keduanya adalah bahwa Dot1Q adalah standar yang diakui secara internasional dan kompatibel dengan berbagai perangkat, sedangkan Cisco ISL khusus digunakan dalam perangkat Cisco dan tidak kompatibel dengan perangkat dari vendor lain.

## Ilustrasi

Sebuah perangkat Cisco switch dikonfigurasi Port Based VLAN sebagai berikut

![](/assets/img/2022-03-13-pembagian-jaringan-secara-virtual-menggunakan-virtual-local-area-network-vlan/04.png){: .normal }

| VLAN ID | VLAN Name  | VLAN Member     | Ket    |
| ------- | ---------- | --------------- | ------ |
| 10      | Jaringan A | Port 1 s.d. 6   | Merah  |
| 20      | Jaringan B | Port 7 s.d. 12  | Kuning |
| 30      | Jaringan C | Port 13 s.d. 18 | Hijau  |

sehingga, dari keterangan di atas berapakah jumlah keanggotaan VLAN?

## Masalah Umum

Masalah umum yang biasa ditemui ketika mengaplikasikan VLAN pada jaringan komputer

1. Koneksi tidak terbentuk

   Masalah ini dapat terjadi karena salah satu atau kedua port tidak dikonfigurasi sebagai trunk port. Untuk mengatasi masalah ini, periksa mode trunk dan VLAN yang diaktifkan pada kedua port.

2. Lalu lintas tidak dapat mengalir

   Masalah ini dapat terjadi karena VLAN yang benar tidak diaktifkan pada port. Untuk mengatasi masalah ini, periksa apakah VLAN yang benar telah diaktifkan pada port.

3. VLAN tidak dapat diakses

   Masalah ini dapat terjadi karena port tidak dikonfigurasi untuk mengakses VLAN yang diinginkan. Untuk mengatasi masalah ini, periksa apakah port telah dikonfigurasi untuk mengakses VLAN yang diinginkan.

## Troubleshoot

Berikut adalah beberapa langkah umum untuk troubleshooting VLAN trunking

1. Periksa fisik

   Pastikan kabel dan koneksi fisik berfungsi dengan baik.

2. Verifikasi konfigurasi

   Pastikan mode trunk dan VLAN yang diaktifkan pada kedua port sesuai.

3. Gunakan perintah show

   Perintah show dapat digunakan untuk memeriksa status trunking pada switch.
