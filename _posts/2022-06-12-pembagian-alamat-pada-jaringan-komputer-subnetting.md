---
layout: post
title: Pembagian Alamat pada Jaringan Komputer (Subnetting)
date: 2022-06-12 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, routing, subnetting]
---

## Pengertian

Subnetting pada jaringan komputer adalah suatu teknik pembagian jaringan menjadi beberapa sub-jaringan yang masing-masing memiliki alamat IP unik.

Tujuannya adalah untuk membagi jaringan besar menjadi beberapa bagian kecil yang lebih terorganisir dan mudah dikelola.

Subnetting ini dapat membantu mengoptimalkan penggunaan alamat IP, mempermudah manajemen jaringan dan memperkuat keamanan jaringan.

Subnetting menghasilkan sub-jaringan yang terisolasi dan memungkinkan komunikasi antar sub-jaringan melalui router setelah terjadi proses routing.

Analogi jika tanpa subnet,

![](/assets/img/2022-06-12-pembagian-alamat-pada-jaringan-komputer-subnetting/01.png){: .normal }

sedangkan jika dengan subnet,

![](/assets/img/2022-06-12-pembagian-alamat-pada-jaringan-komputer-subnetting/02.png){: .normal }

## Kebutuhan

beberapa alasan mengapa subnetting dibutuhkan pada alamat jaringan

1. Efisiensi Penggunaan Alamat IP

   Subnetting membantu memaksimalkan penggunaan alamat IP dengan membagi alamat IP besar menjadi beberapa sub-jaringan yang lebih kecil.

1. Organisasi Jaringan

   Subnetting membantu mengorganisir jaringan dengan membagi jaringan besar menjadi sub-jaringan yang lebih kecil dan terpisah.

1. Keamanan Jaringan

   Subnetting membantu meningkatkan keamanan jaringan dengan membatasi akses antar sub-jaringan dan membatasi lalu lintas jaringan.

1. Manajemen Jaringan

   Subnetting mempermudah manajemen jaringan dengan membagi jaringan besar menjadi sub-jaringan yang lebih kecil dan mudah dikelola.

1. Troubleshooting

   Subnetting mempermudah troubleshooting jaringan dengan membatasi skala masalah dan mempermudah identifikasi sumber masalah.

## Subnet Mask

Fungsi dari subnet mask adalah untuk membedakan Network ID dengan Host ID dan menentukan alamat tujuan paket data apakah local atau remote.

> **Catatan:**
> N untuk Network ID, H untuk Host ID

| Kelas | Range                          | Porsi   | Subnet Mask   |
| ----- | ------------------------------ | ------- | ------------- |
| A     | 0.0.0.0 s.d. 127.255.255.255   | N.H.H.H | 255.0.0.0     |
| B     | 128.0.0.0 s.d. 191.255.255.255 | N.N.H.H | 255.255.0.0   |
| C     | 192.0.0.0 s.d. 223.255.255.255 | N.N.N.H | 255.255.255.0 |

### Prefix

Prefix digunakan sebagai penunjuk banyak bit dari sebuah IP Address yang merupakan porsi Network ID.

Alamat IP seharusnya ditulis lengkap seperti ini

> IP Address: 192.168.100.10
>
> Subnet Mask: 255.255.255.0

namun, dengan prefix dapat ditulis secara singkat menjadi,

> 192.168.100.10/24

Notasi network prefix juga dikenal dengan sebutan notasi Classless InterDomain Routing (CIDR).

| Kelas | Prefix Length         |
| ----- | --------------------- |
| A     | /8 - /15 (/8 - /30)   |
| B     | /16 - /23 (/16 - /30) |
| C     | /24 - /30             |

CIDR digunakan untuk mempermudah penulisan notasi subnet mask agar lebih ringkas dibandingkan penulisan notasi subnet mask yang sesungguhnya.

#### Contoh Kasus

Berikut contoh langkah menghitung prefix length untuk suatu subnet mask

1. Contoh 1

   Subnet Mask (Desimal): 255.0.0.0

   Subnet Mask (Biner): **11111111**.00000000.00000000.00000000

   Prefix Length: /8

1. Contoh 2

   Subnet Mask (Desimal): 255.255.0.0

   Subnet Mask (Biner): **11111111**.**11111111**.00000000.00000000

   Prefix Length: /16

1. Contoh 3

   Subnet Mask (Desimal): 255.255.255.0

   Subnet Mask (Biner): **11111111**.**11111111**.**11111111**.00000000

   Prefix Length: /24

#### Berlatih

Tentukan nilai subnet mask jika diketahui prefix length berikut

1. /9
1. /18
1. /23
1. /26
1. /30

### Total Subnet

Jumlah subnet suatu prefix length dapat diperoleh dengan rumus:

**= 2<sup>y</sup>, di mana y = jumlah bit 1** pada:

- oktet ke-4 biner subnet mask untuk kelas C,
- oktet ke-3 biner subnet mask untuk kelas B,
- oktet ke-2 biner subnet mask untuk kelas A.

#### Contoh Kasus

Berikut contoh menghitung jumlah subnet untuk suatu prefix length

1. Contoh: Prefix /25

   Kelas: C

   Subnet Mask (Biner): `11111111`.`11111111`.`11111111`.**1**0000000

   Bit 1 pada oktet ke-4 berjumlah 1, maka

   Jumlah subnet: 2<sup>1</sup> = 2 subnet

1. Contoh: Prefix /18

   Kelas: B

   Subnet Mask (Biner): `11111111`.`11111111`.**11**000000.`00000000`

   Bit 1 pada oktet ke-3 berjumlah 2, maka

   Jumlah subnet: 2<sup>2</sup> = 4 subnet

1. Contoh: Prefix /11

   Kelas: A

   Subnet Mask (Biner): `11111111`.**111**00000.`00000000`.`00000000`

   Bit 1 pada oktet ke-2 berjumlah 3, maka

   Jumlah subnet: 2<sup>3</sup> = 8 subnet

#### Berlatih

Tentukan jumlah subnet jika diketahui prefix berikut!

1. /9
1. /17
1. /22
1. /27
1. /29

### Lebar Blok Subnet

Ukuran blok adalah rentang alamat suatu subnet yang ditandai dengan kelipatan angka.

Kelipatan angka ini akan mengisi pada oktet pertama untuk porsi Host ID sekaligus IP pertama suatu subnet, yaitu

- oktet ke-4 untuk kelas C,
- oktet ke-3 untuk kelas B,
- oktet ke-2 untuk kelas A.

Blok subnet dapat dihitung dengan rumus:

**= 256 - z, di mana z = nilai oktet terakhir subnet mask**.

> **Catatan:**
> Oktet yang perlu diamati dapat dilihat pada perhitungan Jumlah Subnet.

#### Contoh Kasus

Berikut contoh menghitung besar blok subnet untuk suatu prefix length

1. Contoh: Prefix /27

   Kelas: C

   Subnet Mask (Biner): `11111111`.`11111111`.`11111111`.**111**00000

   Subnet Mask (Desimal): `255`.`255`.`255`.**224**

   Blok Subnet: 256 - 224 = 32

   Maka blok subnet merupakan kelipatan 32, yaitu: 0, 32, 64, 96, 128, 160, 192, 224

1. Contoh: Prefix /18

   Kelas: B

   Subnet Mask (Biner): `11111111`.`11111111`.**11**000000.`00000000`

   Subnet Mask (Desimal): `255`.`255`.**192**.`0`

   Blok Subnet: 256 - 192 = 64

   Maka blok subnet merupakan kelipatan 64, yaitu: 0, 64, 128, 192

1. Contoh: Prefix /12

   Kelas: A

   Subnet Mask (Biner): `11111111`.**1111**0000.`00000000`.`00000000`

   Subnet Mask (Desimal): 255.**240**.0.0

   Blok Subnet: 256 - 240 = 16

   Maka blok subnet merupakan kelipatan 16, yaitu: 0, 16, 32, 48, 64, ..., 240

#### Berlatih

Tentukan jumlah dan blok subnet jika diketahui prefix berikut!

1. /10
1. /17
1. /22
1. /24
1. /29

## Total IP

Total IP adalah rentang alamat dalam suatu subnet, termasuk di dalamnya ada alamat Network ID, rentang alamat Host (Host Range), dan alamat Broadcast

Total IP pada suatu subnet dapat diperoleh dengan rumus:

**= 2<sup>x</sup>, di mana x = jumlah bit 0**.

### Contoh

1. Contoh: Prefix /24

   Kelas: C

   Subnet Mask (Biner): `11111111`.`11111111`.`11111111`.**00000000** (bit 0: 8)

   Total IP pada subnet: 2<sup>8</sup> = 256 alamat

1. Contoh: Prefix /18

   Kelas: B, ubah ke Kelas C dengan + 8, maka seolah menjadi /26

   Subnet Mask (Biner): `11111111`.`11111111`.`11111111`.11**000000** (bit 0: 6)

   Total IP pada subnet: 2<sup>6</sup> x 256 = 64 x 256 = 16.384 alamat

   > **Catatan:**
   > Pengali (x 256) sesuai berapa kali penambahan angka 8 pada langkah konversi.

1. Contoh: Prefix /13

   Kelas: A, ubah ke Kelas C dengan + 8 lalu + 8, maka seolah menjadi /29

   Subnet Mask (Biner): `11111111`.`11111111`.`11111111`.11111**000** (bit 0: 3)

   Total IP pada subnet: 2<sup>3</sup> x 256 x 256 = 8 x 256 x 256 = 524.288 alamat

### Berlatih

Tentukan total ip pada suatu subnet jika diketahui prefix berikut!

1. /10
1. /20
1. /23
1. /26
1. /30

### Total Host (Alamat Valid) pada Subnet

Host Range merupakan sederet IP address yang tersedia dalam suatu subnet dan bukan IP yang merupakan Network ID maupun Broadcast.

Total host pada suatu subnet dapat diperoleh dengan rumus:

**= Total IP - 2, di mana 2 adalah untuk alamat Network ID (1) dan alamat Broadcast (1)**.

Total host ini adalah alamat IP valid dapat dikonfigurasikan (baik manual maupun otomatis) pada perangkat yang terhubung ke jaringan (seperti PC, Laptop, Smartphone, dll).

## Perhitungan Subnetting

Berikut contoh melakukan perhitungan subnet untuk suatu alamat IP acuan

### Contoh

Lakukan perhitungan subnetting:

1. subnet mask (dalam desimal),
1. jumlah subnet,
1. besar blok subnet,
1. total ip,
1. total host, dan
1. alamat jaringan (network id)

jika diketahui sebuah IP Address yaitu **192.168.2.172/26**!

### Solusi

1. Subnet Mask

   CIDR: Kelas C

   Prefix: /26

   Biner: `11111111`.`11111111`.`11111111`.**11**000000

   Desimal: `255`.`255`.`255`.**192**

1. Jumlah Subnet

   Bit 1 pada oktet ke-4: 2

   2<sup>2</sup> = 4 subnet

1. Blok Subnet

   256 - 192 = 64

   Maka blok subnet merupakan kelipatan 64, yaitu: 0, 64, 128, 192

1. Total IP

   Bit 0 pada oktet ke-4: 6

   2<sup>6</sup> = 64 buah IP

1. Total Host

   = Total IP - 2

   = 64 - 2

   = 62 alamat host

1. Alamat Jaringan

   Tersedia 4 subnet dengan kelipatan 64, yaitu: 0, 64, 128, 192

   |            | Subnet Ke-1  | Subnet Ke-2   | Subnet Ke-3   | Subnet Ke-4   |
   | ---------- | ------------ | ------------- | ------------- | ------------- |
   | Network ID | 192.168.2.0  | 192.168.2.64  | 192.168.2.128 | 192.168.2.192 |
   | First Host | .2.1         | .2.65         | 2.129         | 2.193         |
   | ...        | ...          | ...           | ...           | ...           |
   | Last Host  | .2.62        | 2.126         | 2.190         | 2.254         |
   | Broadcast  | 192.168.2.63 | 192.168.2.127 | 192.168.2.191 | 192.168.2.255 |

   maka untuk alamat jaringan yang tersedia yaitu

   1. Subnet Ke-1: 192.168.2.0/26
   2. Subnet Ke-2: 192.168.2.64/26
   3. Subnet Ke-3: 192.168.2.128/26
   4. Subnet Ke-4: 192.168.2.192/26

### Pertanyaan Lanjutan

1. Bagaimana hasilnya, jika prefix length digeser menjadi /10?
1. Dengan prefix length baru, alamat acuan awal masuk ke dalam subnet/jaringan mana?

### Berlatih

Lakukan perhitungan subnetting:

1. subnet mask (dalam desimal),
1. jumlah subnet,
1. besar blok subnet,
1. total ip,
1. total host, dan
1. alamat jaringan (network id)

untuk alamat IP berikut!

1. 172.16.20.10/22
1. 10.200.100.25/16
1. 192.168.1.20/10
1. 172.25.200.1/25

### Tabel Subnetting

Informasi tentang perhitungan subnetting secara cepat dapat diperolah dari tabel berikut.

![](/assets/img/2022-06-12-pembagian-alamat-pada-jaringan-komputer-subnetting/03.png){: .normal }
