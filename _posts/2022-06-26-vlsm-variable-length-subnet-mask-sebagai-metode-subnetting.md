---
layout: post
title: VLSM (Variable Length Subnet Mask) sebagai Metode Subnetting
date: 2022-06-26 00:00 +0000
author: angga
categories: [Materi, Teori]
tags: [cisco, routing, subnetting]
---

## Pengertian

VLSM (Variable Length Subnet Mask) adalah metode subnetting di mana ukuran mask subnet berbeda-beda untuk setiap subnet karena tergantung kebutuhan jumlah host pada masing-masing subnet tersebut.

## Kebutuhan

rhitungan subnet ini diawali dengan mengurutkan mulai dari jaringan dengan kebutuhan host dari yang paling banyak sampai dengan paling sedikit.

Oleh karena itu, hal pertama yang dilakukan guna menganalisis kebutuhan host suatu network adalah paham terhadap cara menghitung total ip/total host suatu subnet berdasarkan prefix length.

Gunakan kembali [tabel subnetting](/posts/pembagian-alamat-pada-jaringan-komputer-subnetting/#tabel-subnetting){:target="\_blank"} untuk menemukan prefix length (subnet mask) yang tepat sesuai host yang dibutuhkan.

> **Catatan:**
> Untuk mempelajari subnetting metode VLSM, anda harus memahami terlebih dahulu tentang subnetting metode CIDR.

## Contoh Kasus

Sebuah jaringan dirancang untuk digunakan dalam sebuah gedung kantor yang terdiri dari beberapa departemen dengan kebutuhan host yang beragam.

![](/assets/img/2022-06-26-vlsm-variable-length-subnet-mask-sebagai-metode-subnetting/01.png){: .normal }

Tentukan pembagian jaringan (subnet) menggunakan metode VLSM bila diberikan IP Address **192.168.10.0/24** sebagai acuan!

## Solusi

1. Urutkan berdasarkan kebutuhan host paling banyak sampai dengan paling sedikit.

   - Departemen B; kebutuhan 40 host.
   - Departemen A; kebutuhan 23 host`.
   - Departemen C; kebutuhan 14 host`.
   - LAN 1; kebutuhan 2 host.
   - LAN 2; kebutuhan 2 host.

1. Tentukan prefix length (subnet mask) dengan nilai total host paling mendekati di atas host kebutuhan dalam jaringan. Gunakan tabel subnetting kembali untuk memudahkan pencarian total ip/host sesuai prefix length.

   - Kebutuhan 40 host, maka prefix /26 (total host 62 buah)
   - Kebutuhan 23 host, maka prefix /27 (total host 30 buah)
   - Kebutuhan 14 host, maka prefix /28 (total host 14 buah)
   - Kebutuhan 2 host, maka prefix /30 (total host 2 buah)
   - Kebutuhan 2 host, maka prefix /30 (total host 2 buah)

1. Tentukkan subnet mask, jumlah subnet, blok subnet, total host dan ip valid pada setiap jaringan sesuai prefix length.

   - **Departemen B (/26)**

     - Subnet Mask

       = 11111111.111111111.11111111.11000000

       = 255.255.255.192

     - Jumlah Subnet

       = 2<sup>2</sup> subnet

       = 4 subnet

     - Blok Subnet

       = 256 - 192

       = 64, blok yaitu: **0**, 64, 128, 192

       blok yang diambil 0 s.d. 63

     - Total IP

       = 2<sup>6</sup> buah

       = 64 buah

     - Total Host

       = Total IP - 2 (Network & Broadcast)

       = 64 - 2

       = 62 buah

     - IP Valid

       Kelas C, maka porsi N.N.N.H

       |            | Subnet | Subnet  | Subnet  | Subnet  |
       | ---------- | ------ | ------- | ------- | ------- |
       | Network ID | .10.0  | .10.64  | .10.128 | .10.192 |
       | First Host | .10.1  | .10.65  | .10.129 | .10.193 |
       | Last Host  | .10.62 | .10.126 | .10.190 | .10.254 |
       | Broadcast  | .10.63 | .10.127 | .10.191 | .10.255 |

   - **Departemen A (/27)**

     - Subnet Mask

       = 11111111.111111111.11111111.11100000

       = 255.255.255.224

     - Jumlah Subnet

       = 2<sup>3</sup> subnet

       = 8 subnet

     - Blok Subnet

       = 256 - 224

       = 32, blok yaitu: ~~0, 32~~, **64**, 96, 128, ..., 224

     - Total IP

       = 2<sup>5</sup> buah

       = 32 buah

     - Total Host

       = Total IP - 2 (Network & Broadcast)

       = 32 - 2

       = 30 buah

     - IP Valid

       Kelas C, maka porsi N.N.N.H

       |            | Subnet | Subnet  | Subnet  | Subnet  |
       | ---------- | ------ | ------- | ------- | ------- |
       | Network ID | .10.0  | .10.64  | .10.128 | .10.192 |
       | First Host | .10.1  | .10.65  | .10.129 | .10.193 |
       | Last Host  | .10.62 | .10.126 | .10.190 | .10.254 |
       | Broadcast  | .10.63 | .10.127 | .10.191 | .10.255 |

   - **Departemen C (/28)**

     - Subnet Mask

       = 11111111.111111111.11111111.11110000

       = 255.255.255.240

     - Jumlah Subnet

       = 2<sup>4</sup> subnet

       = 16 subnet

     - Blok Subnet

       = 256 - 240

       = 16, blok yaitu: ~~0, 16, 32, 48, ...~~, **96**, 112, 128, ..., 240

     - Total IP

       = 2<sup>4</sup> buah

       = 16 buah

     - Total Host

       = Total IP - 2 (Network & Broadcast)

       = 16 - 2

       = 14 buah

     - IP Valid

       Kelas C, maka porsi N.N.N.H

       |            | Subnet | Subnet  | Subnet  | Subnet |
       | ---------- | ------ | ------- | ------- | ------ |
       | Network ID | …      | .10.96  | .10.112 | …      |
       | First Host | …      | .10.97  | .10.113 | …      |
       | Last Host  | …      | .10.110 | .10.126 | …      |
       | Broadcast  | …      | .10.111 | .10.127 | …      |

   - **LAN 1, LAN 2 (/30)**

     - Subnet Mask

       = 11111111.111111111.11111111.11111100

       = 255.255.255.252

     - Jumlah Subnet

       = 2<sup>6</sup> subnet

       = 64 subnet

     - Blok Subnet

       = 256 - 252

       = 4, blok yaitu: ~~0, 4, 8, 12, 16, ...~~, **112, 116**, 120, ..., 252

     - Total IP

       = 2<sup>2</sup> buah

       = 4 buah

     - Total Host

       = Total IP - 2 (Network & Broadcast)

       = 4 - 2

       = 2 buah

     - IP Valid

       Kelas C, maka porsi N.N.N.H

       |            | Subnet | Subnet  | Subnet  | Subnet |
       | ---------- | ------ | ------- | ------- | ------ |
       | Network ID | …      | .10.112 | .10.116 | …      |
       | First Host | …      | .10.113 | .10.117 | …      |
       | Last Host  | …      | .10.114 | .10.118 | …      |
       | Broadcast  | …      | .10.115 | .10.119 | …      |

## Kesimpulan

Hasil subnetting pada jaringan di atas menggunakan metode VLSM sebagai berikut

| No  | Subnet | Kebutuhan Host | Network ID        | Host Range                      | Broadcast      | Total Host | Host Tidak Terpakai |
| --- | ------ | -------------- | ----------------- | ------------------------------- | -------------- | ---------- | ------------------- |
| 1   | Dep B  | 40             | 192.168.10.0/26   | 192.168.10.1 - 192.168.10.62    | 192.168.10.63  | 62         | 22                  |
| 2   | Dep A  | 23             | 192.168.10.64/27  | 192.168.10.65 - 192.168.10.94   | 192.168.10.95  | 30         | 7                   |
| 3   | Dep C  | 14             | 192.168.10.96/28  | 192.168.10.97 - 192.168.10.110  | 192.168.10.111 | 14         | 0                   |
| 4   | LAN 1  | 2              | 192.168.10.112/30 | 192.168.10.113 - 192.168.10.114 | 192.168.10.115 | 2          | 0                   |
| 5   | LAN 2  | 2              | 192.168.10.116/30 | 192.168.10.117 - 192.168.10.118 | 192.168.10.119 | 2          | 0                   |

## Berlatih

Anda merupakan seorang network administrator suatu perusahaan yang sedang merencakan pembagian jaringan untuk masing-masing bidang kerja.

![](/assets/img/2022-06-26-vlsm-variable-length-subnet-mask-sebagai-metode-subnetting/02.png){: .normal }

Perusahaan tersebut memiliki 4 bidang kerja dengan berbagai jumlah kebutuhan alamat host sebagai berikut

1. Bidang Pemasaran dengan kebutuhan 100 host,
1. Bidang Keuangan dengan kebutuhan 25 host,
1. Bidang Administrasi dengan kebutuhan 10 host,
1. Bidang Sumberdaya dengan kebutuhan 35 host, dan
1. 3 buah LAN dengan kebutuhan masing-masing 2 host.

Tentukan pembagian jaringan (subnet) menggunakan metode VLSM bila diberikan IP Address **172.16.0.0/24** sebagai acuan!
