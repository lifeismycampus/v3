---
layout: post
title: Konfigurasi EIGRP pada Cisco Packet Tracer
date: 2023-02-12 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing]
---

## Ulasan

EIGRP memanfaatkan algoritma DUAL yang unik dan efektif untuk menentukan rute terbaik untuk paket data.

Algoritma DUAL memungkinkan EIGRP untuk menghitung rute yang paling efisien dan mengurangi lalu lintas yang dihasilkan.

Selain itu, EIGRP juga dapat melakukan load balancing pada beberapa jalur dengan biaya yang sama, yang dapat meningkatkan kinerja jaringan dan mencegah kemungkinan terjadinya bottleneck pada rute tertentu.

EIGRP dilengkapi dengan fitur-fitur seperti autentikasi, dukungan untuk jaringan IPv4 dan IPv6, serta kemampuan untuk mendukung konvergensi jaringan yang cepat dan stabil.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                    | Deskripsi                                                                                                                                                          |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Router(config)#router eigrp `as-number`                                     | Mengaktifkan EIGRP pada router dengan nomor Autonomous System (AS) tertentu.                                                                                       |
| Router(config)#key chain `key-chain`                                        | Membuat key-chain yang berfungsi untuk menyimpan daftar kunci yang digunakan untuk otentikasi.                                                                     |
| Router(config-keychain)#key `number`                                        | Membuat nomor kunci (key number) pada key-chain yang telah dibuat sebelumnya.                                                                                      |
| Router(config-keychain-key)#key-string `password`                           | Mengatur password yang akan digunakan untuk otentikasi.                                                                                                            |
| Router(config-if)#ip authentication key-chain eigrp `as-number` `key-chain` | Mengaktifkan otentikasi pada interface dengan menggunakan key-chain yang telah dibuat, dan digunakan pada protokol EIGRP dengan suatu nomor autonomus system (AS). |
| Router(config-if)#ip authentication mode eigrp `as-number` md5              | Mengatur mode otentikasi EIGRP dengan menggunakan metode hash Message Digest 5 (MD5) untuk mengamankan data yang dikirim melalui protokol EIGRP pada suatu AS.     |
| Router(config)#username `username` password `password`                      | Membuat akun pengguna (username) dan mengatur kata sandi (password) untuk pengguna router                                                                          |
| Router(config)#ip domain-name `domain-name`                                 | Mengkonfigurasi nama domain pada router                                                                                                                            |
| Router(config)#crypto key generate rsa                                      | Menghasilkan pasangan kunci RSA (Rivest-Shamir-Adleman) pada konfigurasi router                                                                                    |
| Router(config)#line vty `0` `4`                                             | Menetapkan terminal line virtual (vty) dari 0 hingga 4 sebagai target konfigurasi                                                                                  |
| Router(config-line)#transport input telnet                                  | Menetapkan hanya protokol telnet untuk akses vty                                                                                                                   |
| Router(config-line)#transport input ssh                                     | Menetapkan hanya protokol ssh untuk akses vty                                                                                                                      |
| Router(config-line)#transport input all                                     | Menetapkan semua protokol baik telnet maupun ssh untuk akses vty                                                                                                   |
| Router(config-line)#password `password`                                     | Menetapkan password untuk masuk ke vty                                                                                                                             |
| Router(config-line)#login                                                   | Menetapkan login sebagai opsi untuk mengharuskan pengguna memasukkan kata sandi sebelum masuk ke vty                                                               |
| Router(config)#enable secret `secret`                                       | Menetapkan password enable secret untuk akses privileged mode                                                                                                      |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, Pengujian, Konfigurasi Ulang, dan Pengujian Ulang.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/01.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/eigrp-praktikum-kosong.pkt){:target="\_blank"}.

#### Spesifikasi

| Jaringan | Network ID    | Prefix |
| -------- | ------------- | ------ |
| WAN1     | 10.11.1xx.0   | /30    |
| WAN2     | 10.22.1xx.0   | /30    |
| WAN3     | 10.33.1xx.0   | /30    |
| WAN4     | 10.44.1xx.0   | /30    |
| WAN5     | 10.55.1xx.0   | /30    |
| LAN1     | 172.16.xx.224 | /27    |
| LAN2     | 172.16.xx.192 | /27    |
| LAN3     | 172.16.xx.160 | /27    |

Nomor autonomous system (AS) yang digunakan adalah xx.

> **Catatan:**
> Kode `xx` diganti dengan nomor presensi masing-masing, dalam contoh ini akan digunakan nomor 99.

#### Tabel Pengalamatan

| Device     | Interface | IP Address    | Prefix | Gateway       |
| ---------- | --------- | ------------- | ------ | ------------- |
| R1         | Lo0       | 99.99.99.1    | /32    | -             |
| R1         | Se0/0/0   | 10.11.199.1   | /30    | -             |
| R1         | Se0/1/1   | 10.55.199.1   | /30    | -             |
| R1         | Gig0/0    | 172.16.99.225 | /27    | -             |
| R2         | Lo0       | 99.99.99.2    | /32    | -             |
| R2         | Se0/0/0   | 10.11.199.2   | /30    | -             |
| R2         | Se0/0/1   | 10.22.199.1   | /30    | -             |
| R2         | Se0/1/0   | 10.44.199.2   | /30    | -             |
| R2         | Gig0/0    | 172.16.99.193 | /27    | -             |
| R3         | Lo0       | 99.99.99.3    | /32    | -             |
| R3         | Se0/0/0   | 10.33.199.2   | /30    | -             |
| R3         | Se0/0/1   | 10.22.199.2   | /30    | -             |
| R3         | Se0/1/1   | 10.55.199.2   | /30    | -             |
| R3         | Gig0/0    | 172.16.99.161 | /27    | -             |
| R4         | Lo0       | 99.99.99.4    | /32    | -             |
| R4         | Se0/0/0   | 10.33.199.1   | /30    | -             |
| R4         | Se0/1/0   | 10.44.199.1   | /30    | -             |
| PC-Admin   | Fa0       | DHCP Client   | /27    | 172.16.99.225 |
| PC-Client1 | Fa0       | DHCP Client   | /27    | 172.16.99.193 |
| PC-Client2 | Fa0       | DHCP Client   | /27    | 172.16.99.193 |
| PC-Client3 | Fa0       | DHCP Client   | /27    | 172.16.99.161 |
| PC-Client4 | Fa0       | DHCP Client   | /27    | 172.16.99.161 |

### Konfigurasi

#### R1

1. Konfigurasi alamat ip pada interface

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R1
   R1(config)#interface loopback 0
   R1(config-if)#ip address 99.99.99.1 255.255.255.255
   R1(config-if)#exit
   R1(config)#interface gigabitEthernet 0/0
   R1(config-if)#no shutdown
   R1(config-if)#ip address 172.16.99.225 255.255.255.224
   R1(config-if)#exit
   R1(config)#interface serial 0/0/0
   R1(config-if)#no shutdown
   R1(config-if)#clock rate 125000
   R1(config-if)#ip address 10.11.199.1 255.255.255.252
   R1(config-if)#exit
   R1(config)#interface serial 0/1/1
   R1(config-if)#no shutdown
   R1(config-if)#clock rate 125000
   R1(config-if)#ip address 10.55.199.1 255.255.255.252
   R1(config-if)#exit
   R1(config)#
   ```

1. Konfigurasi dhcp server

   ```console
   R1(config)#ip dhcp pool net1
   R1(dhcp-config)#network 172.16.99.224 255.255.255.224
   R1(dhcp-config)#default-router 172.16.99.225
   R1(dhcp-config)#exit
   R1(config)#ip dhcp excluded-address 172.16.99.225
   R1(config)#
   ```

1. Konfigurasi routing eigrp

   ```console
   R1(config)#router eigrp 99
   R1(config-router)#network 99.99.99.1
   R1(config-router)#network 172.16.99.224
   R1(config-router)#network 10.11.199.0
   R1(config-router)#network 10.55.199.0
   R1(config-router)#no auto-summary
   R1(config-router)#exit
   R1(config)#
   ```

#### PC-Admin

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/02.png){: .normal }

#### R2

1. Konfigurasi alamat ip pada interface

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R2
   R2(config)#interface loopback 0
   R2(config-if)#ip address 99.99.99.2 255.255.255.255
   R2(config-if)#exit
   R2(config)#interface gigabitEthernet 0/0
   R2(config-if)#no shutdown
   R2(config-if)#ip address 172.16.99.193 255.255.255.224
   R2(config-if)#exit
   R2(config)#interface serial 0/0/0
   R2(config-if)#no shutdown
   R2(config-if)#ip address 10.11.199.2 255.255.255.252
   R2(config-if)#exit
   R2(config)#interface serial 0/0/1
   R2(config-if)#no shutdown
   R2(config-if)#clock rate 125000
   R2(config-if)#ip address 10.22.199.1 255.255.255.252
   R2(config-if)#exit
   R2(config)#interface serial 0/1/0
   R2(config-if)#no shutdown
   R2(config-if)#ip address 10.44.199.2 255.255.255.252
   R2(config-if)#exit
   R2(config)#
   ```

1. Konfigurasi dhcp server

   ```console
   R2(config)#ip dhcp pool net2
   R2(dhcp-config)#network 172.16.99.192 255.255.255.224
   R2(dhcp-config)#default-router 172.16.99.193
   R2(dhcp-config)#exit
   R2(config)#ip dhcp excluded-address 172.16.99.193
   R2(config)#
   ```

1. Konfigurasi routing eigrp

   ```console
   R2(config)#router eigrp 99
   R2(config-router)#network 99.99.99.2
   R2(config-router)#network 172.16.99.192
   R2(config-router)#network 10.11.199.0
   R2(config-router)#network 10.22.199.0
   R2(config-router)#network 10.44.199.0
   R2(config-router)#no auto-summary
   R2(config-router)#exit
   R2(config)#
   ```

#### PC-Client1, PC-Client2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/03.png){: .normal }

2. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/04.png){: .normal }

#### R3

1. Konfigurasi alamat ip pada interface

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R3
   R3(config)#interface loopback 0
   R3(config-if)#ip address 99.99.99.3 255.255.255.255
   R3(config-if)#exit
   R3(config)#interface gigabitEthernet 0/0
   R3(config-if)#no shutdown
   R3(config-if)#ip address 172.16.99.161 255.255.255.224
   R3(config-if)#exit
   R3(config)#interface serial 0/0/0
   R3(config-if)#no shutdown
   R3(config-if)#ip address 10.33.199.2 255.255.255.252
   R3(config-if)#exit
   R3(config)#interface serial 0/0/1
   R3(config-if)#no shutdown
   R3(config-if)#ip address 10.22.199.2 255.255.255.252
   R3(config-if)#exit
   R3(config)#interface serial 0/1/1
   R3(config-if)#no shutdown
   R3(config-if)#ip address 10.55.199.2 255.255.255.252
   R3(config-if)#exit
   R3(config)#
   ```

1. Konfigurasi dhcp server

   ```console
   R3(config)#ip dhcp pool net3
   R3(dhcp-config)#network 172.16.99.160 255.255.255.224
   R3(dhcp-config)#default-router 172.16.99.161
   R3(dhcp-config)#exit
   R3(config)#ip dhcp excluded-address 172.16.99.161
   R3(config)#
   ```

1. Konfigurasi routing eigrp

   ```console
   R3(config)#router eigrp 99
   R3(config-router)#network 99.99.99.3
   R3(config-router)#network 10.33.199.0
   R3(config-router)#network 10.22.199.0
   R3(config-router)#network 10.55.199.0
   R3(config-router)#network 172.16.99.160
   R3(config-router)#no auto-summary
   R3(config-router)#exit
   R3(config)#
   ```

#### PC-Client3, PC-Client4

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/05.png){: .normal }

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/06.png){: .normal }

#### R4

1. Konfigurasi alamat ip pada interface

   ```console
   Router>enable
   Router#configure terminal
   Router(config)#hostname R4
   R4(config)#interface loopback 0
   R4(config-if)#ip address 99.99.99.4 255.255.255.255
   R4(config-if)#exit
   R4(config)#interface serial 0/0/0
   R4(config-if)#no shutdown
   R4(config-if)#clock rate 125000
   R4(config-if)#ip address 10.33.199.1 255.255.255.252
   R4(config-if)#exit
   R4(config)#interface serial 0/1/0
   R4(config-if)#no shutdown
   R4(config-if)#clock rate 125000
   R4(config-if)#ip address 10.44.199.1 255.255.255.252
   R4(config-if)#exit
   R4(config)#
   ```

1. Konfigurasi routing eigrp

   ```console
   R4(config)#router eigrp 99
   R4(config-router)#network 99.99.99.4
   R4(config-router)#network 10.33.199.0
   R4(config-router)#network 10.44.199.0
   R4(config-router)#no auto-summary
   R4(config-router)#exit
   R4(config)#
   ```

### Pengujian

#### R1

1. Konfirmasi hasil konfigurasi alamat pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/07.png){: .normal }

2. Konfirmasi hasil konfigurasi dhcp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/08.png){: .normal }

3. Konfirmasi hasil konfigurasi routing eigrp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/09.png){: .normal }

#### R2

1. Konfirmasi hasil konfigurasi alamat pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/10.png){: .normal }

2. Konfirmasi hasil konfigurasi dhcp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/11.png){: .normal }

3. Konfirmasi hasil konfigurasi routing eigrp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/12.png){: .normal }

#### R3

1. Konfirmasi hasil konfigurasi alamat pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/13.png){: .normal }

2. Konfirmasi hasil konfigurasi dhcp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/14.png){: .normal }

3. Konfirmasi hasil konfigurasi routing eigrp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/15.png){: .normal }

#### R4

1. Konfirmasi hasil konfigurasi alamat pada interface

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/16.png){: .normal }

2. Konfirmasi hasil konfigurasi routing eigrp

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/17.png){: .normal }

#### PC-Admin

1. Konfirmasi hasil konfigurasi routing eigrp ke jaringan lain menggunakan perintah `ping`

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/18.png){: .normal }

#### PC-Client1

1. Konfirmasi hasil konfigurasi routing eigrp ke jaringan lain menggunakan perintah `tracert`

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/19.png){: .normal }

#### PC-Client3

1. Konfirmasi hasil konfigurasi routing eigrp ke jaringan lain menggunakan perintah `tracert`

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/20.png){: .normal }

### Konfigurasi Ulang

Untuk menambah keamanan, maka dapat dilakukan konfigurasi EIGRP Authentication pada interface router yang terhubung langsung ke router lain menggunakan mode `md5`.

#### R1

1. Konfigurasi pembuatan authentication

   ```console
   R1(config)#key chain keychain1
   R1(config-keychain)#key 1
   R1(config-keychain-key)#key-string !Password1
   R1(config-keychain-key)#exit
   R1(config-keychain)#exit
   R1(config)#
   ```

2. Konfigurasi penerapan authentication pada interface

   ```console
   R1(config)#interface gigabitEthernet 0/0
   R1(config-if)#ip authentication key-chain eigrp 99 keychain1
   R1(config-if)#ip authentication mode eigrp 99 md5
   R1(config-if)#exit
   R1(config)#interface serial 0/0/0
   R1(config-if)#ip authentication key-chain eigrp 99 keychain1
   R1(config-if)#ip authentication mode eigrp 99 md5
   R1(config-if)#exit
   R1(config)#interface serial 0/1/1
   R1(config-if)#ip authentication key-chain eigrp 99 keychain1
   R1(config-if)#ip authentication mode eigrp 99 md5
   R1(config-if)#exit
   R1(config)#
   ```

#### R2

1. Konfigurasi pembuatan authentication

   ```console
   R2(config)#key chain keychain1
   R2(config-keychain)#key 1
   R2(config-keychain-key)#key-string !Password1
   R2(config-keychain-key)#exit
   R2(config-keychain)#exit
   R2(config)#
   ```

2. Konfigurasi penerapan authentication pada interface

   ```console
   R2(config)#interface gigabitEthernet 0/0
   R2(config-if)#ip authentication key-chain eigrp 99 keychain1
   R2(config-if)#ip authentication mode eigrp 99 md5
   R2(config-if)#exit
   R2(config)#interface serial 0/0/0
   R2(config-if)#ip authentication key-chain eigrp 99 keychain1
   R2(config-if)#ip authentication mode eigrp 99 md5
   R2(config-if)#exit
   R2(config)#interface serial 0/0/1
   R2(config-if)#ip authentication key-chain eigrp 99 keychain1
   R2(config-if)#ip authentication mode eigrp 99 md5
   R2(config-if)#exit
   R2(config)#interface serial 0/1/0
   R2(config-if)#ip authentication key-chain eigrp 99 keychain1
   R2(config-if)#ip authentication mode eigrp 99 md5
   R2(config-if)#exit
   R2(config)#
   ```

#### R3

1. Konfigurasi pembuatan authentication

   ```console
   R3(config)#key chain keychain1
   R3(config-keychain)#key 1
   R3(config-keychain-key)#key-string !Password1
   R3(config-keychain-key)#exit
   R3(config-keychain)#exit
   R3(config)#
   ```

2. Konfigurasi penerapan authentication pada interface

   ```console
   R3(config)#interface gigabitEthernet 0/0
   R3(config-if)#ip authentication key-chain eigrp 99 keychain1
   R3(config-if)#ip authentication mode eigrp 99 md5
   R3(config-if)#exit
   R3(config)#interface serial 0/0/0
   R3(config-if)#ip authentication key-chain eigrp 99 keychain1
   R3(config-if)#ip authentication mode eigrp 99 md5
   R3(config-if)#exit
   R3(config)#interface serial 0/0/1
   R3(config-if)#ip authentication key-chain eigrp 99 keychain1
   R3(config-if)#ip authentication mode eigrp 99 md5
   R3(config-if)#exit
   R3(config)#interface serial 0/1/1
   R3(config-if)#ip authentication key-chain eigrp 99 keychain1
   R3(config-if)#ip authentication mode eigrp 99 md5
   R3(config-if)#exit
   R3(config)#
   ```

#### R4

1. Konfigurasi pembuatan authentication

   ```console
   R4(config)#key chain keychain1
   R4(config-keychain)#key 1
   R4(config-keychain-key)#key-string !Password1
   R4(config-keychain-key)#exit
   R4(config-keychain)#exit
   R4(config)#
   ```

2. Konfigurasi penerapan authentication pada interface

   ```console
   R4(config)#interface serial 0/0/0
   R4(config-if)#ip authentication key-chain eigrp 99 keychain1
   R4(config-if)#ip authentication mode eigrp 99 md5
   R4(config-if)#exit
   R4(config)#interface serial 0/1/0
   R4(config-if)#ip authentication key-chain eigrp 99 keychain1
   R4(config-if)#ip authentication mode eigrp 99 md5
   R4(config-if)#exit
   R4(config)#
   ```

Selanjutnya, agar dalam mengonfigurasi router dapat dilakukan secara remote (dari perangkat PC-Admin maupun PC-Client), maka dapat dilakukan konfigurasi telnet (pada R1) maupun ssh (pada R2, R3).

#### R1

1. Konfigurasi telnet

   ```console
   R1(config)#line vty 0 4
   R1(config-line)#transport input telnet
   R1(config-line)#password !Telnet1
   R1(config-line)#login
   R1(config-line)#exit
   R1(config)#enable secret !Open1
   R1(config)#
   ```

#### R2

1. Konfigurasi ssh

   ```console
   R2(config)#username r2admin password !R2admin1
   R2(config)#ip domain-name eigrp.com
   R2(config)#crypto key generate rsa
   How many bits in the modulus [512]: 512
   R2(config)#line vty 0 4
   R2(config-line)#transport input ssh
   R2(config-line)#login local
   R2(config-line)#exit
   R2(config)#enable secret !Open1
   R2(config)#
   ```

#### R3

1. Konfigurasi ssh

   ```console
   R3(config)#username r3admin password !R3admin1
   R3(config)#ip domain-name eigrp.com
   R3(config)#crypto key generate rsa
   How many bits in the modulus [512]: 512
   R3(config)#line vty 0 4
   R3(config-line)#transport input ssh
   R3(config-line)#login local
   R3(config-line)#exit
   R3(config)#enable secret !Open1
   R3(config)#
   ```

### Pengujian Ulang

#### PC-Admin

1. Konfirmasi remote telnet

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/21.png){: .normal }

2. Konfirmasi masuk router

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/22.png){: .normal }

#### PC-Client2

1. Konfirmasi remote ssh

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/23.png){: .normal }

2. Konfirmasi masuk router

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/24.png){: .normal }

#### PC-Client4

1. Konfirmasi remote ssh

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/25.png){: .normal }

2. Konfirmasi masuk router

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/26.png){: .normal }

#### R4

1. Konfirmasi terjadi lalu lintas paket data

   memulai pengujian dengan ketik perintah `debug eigrp packet`

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/27.png){: .normal }

   menghentikan pengujian dengan ketik perintah `no debug all`

   ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/28.png){: .normal }

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi routing EIGRP dengan instruksi sebagai berikut

1.  Rancang topolog jaringan routing EIGRP sebagai berikut

    ![](/assets/img/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/29.png){: .normal }

    dengan spesifikasi sebagai berikut

    | Routing Protocol             | EIGRP        |
    | ---------------------------- | ------------ |
    | autonomous system number     | 1xx          |
    | authentication mode          | md5          |
    | keychain                     | myKeyChain   |
    | key-string                   | !Keystringxx |
    | ip Lo0 pada R1               | 1.1.1.xx/32  |
    | ip Lo0 pada R2               | 2.2.2.xx/32  |
    | ip Lo0 pada R3               | 3.3.3.xx/32  |
    | ip Lo0 pada R4               | 4.4.4.xx/32  |
    | ip Lo0 pada R5               | 5.5.5.xx/32  |
    | kode enable setiap router    | !Enablexx    |
    | ssh username pada R1         | r1master     |
    | ssh username pada R2         | r2master     |
    | ssh username pada R3         | r3master     |
    | ssh username pada R4         | r4master     |
    | ssh password pada R1 s.d. R4 | !Sshxx       |
    | ssh domain pada R1           | r1-ssh.net   |
    | ssh domain pada R2           | r2-ssh.net   |
    | ssh domain pada R3           | r3-ssh.net   |
    | ssh domain pada R4           | r4-ssh.net   |
    | rsa modulus bits             | 1024         |
    | telnet password pada R5      | !TelnetR5    |

    > **Catatan:**
    > Kode `xx` diganti dengan nomor presensi masing-masing.

    Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-02-12-konfigurasi-eigrp-pada-cisco-packet-tracer/eigrp-latihan-kosong.pkt){:target="\_blank"}.

2.  Setiap Router dapat mencetak informasi routing table seluruh jaringan.
3.  Setiap PC dapat saling terhubung melalui jaringan routing.
4.  Setiap PC dapat mengenali dan mengakses setiap ssh server.
