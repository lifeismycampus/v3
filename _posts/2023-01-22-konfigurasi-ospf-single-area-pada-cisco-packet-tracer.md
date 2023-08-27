---
layout: post
title: Konfigurasi OSPF Single Area pada Cisco Packet Tracer
date: 2023-01-22 00:00 +0000
author: angga
categories: [Materi, Praktikum]
tags: [cisco, routing, subnetting]
---

## Ulasan

Ada beberapa pilihan routing protocol yang bisa diimplementasikan pada jaringan routing dinamis, salah satunya yaitu routing protocol Open Shortest Path First (OSPF).

OSPF adalah routing protokol yang mengaplikasikan algoritma Dijkstra yaitu algoritma yang digunakan untuk menentukan jarak terpendek.

Pada praktikum kali ini akan ditampilkan langkah konfigurasi Open Shortest Path First single area menggunakan hanya backbone area atau area 0.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                    | Deskripsi                                                                                   |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Router(config)#router ospf `process-id`                                     | memasukkan router ke dalam proses OSPF dengan menentukan ID proses OSPF yang akan digunakan |
| Router(config-router)#router-id `router-id`                                 | menentukan ID unik yang akan digunakan oleh router tersebut dalam proses OSPF               |
| Router(config-router)#network `dest-network` `wildcard-mask` area `area-id` | meng-advertise alamat jaringan dalam proses OSPF                                            |
| Router#show ip route                                                        | menampilkan informasi routing table                                                         |
| Router#show ip ospf                                                         | menampilkan informasi process id, lsa authentication                                        |
| Router#show ip ospf interface `interface`                                   | menampilkan informasi cost, hello, dead interval, state, process id                         |
| Router#show ip ospf neighbor                                                | menampilkan router tetangga pada proses ospf                                                |

## Langkah Kerja

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, Pengujian, Konfigurasi Ulang, dan Pengujian Ulang.

### Persiapan

#### Topologi jaringan

Susun topologi jaringan routing sebagai berikut

![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/01.png){: .normal }

#### Spesifikasi

1. Spesifikasi jaringan OSPF

   | Routing Protocol    | OSPF                   |
   | ------------------- | ---------------------- |
   | Area                | 0                      |
   | R1                  | Router ID: 1.1.1.1     |
   | R2                  | Router ID: 2.2.2.2     |
   | R3                  | Router ID: 3.3.3.3     |
   | Email Server Domain | `username`@kebumail.id |

2. Spesifikasi data email client

   | Name           | Username | Password |
   | -------------- | -------- | -------- |
   | Administrator  | adm      | pwdadm   |
   | Hari Nugroho   | user1    | pwd1     |
   | Iwan Safrudin  | user2    | pwd2     |
   | Meli Poncowati | user3    | pwd3     |
   | Wisnu Wardoyo  | user4    | pwd4     |

#### Tabel pengalamatan

| Device     | Interface | IP Address    | Prefix | Gateway       |
| ---------- | --------- | ------------- | ------ | ------------- |
| R1         | se0/0/0   | 10.10.1.1     | /30    | -             |
| R1         | se0/0/1   | 10.10.2.1     | /30    | -             |
| R1         | fa0/0     | 192.168.1.254 | /24    | -             |
| R2         | se0/0/0   | 10.10.1.2     | /30    | -             |
| R2         | se0/0/1   | 10.10.3.1     | /30    | -             |
| R2         | fa0/0     | 172.16.100.1  | /29    | -             |
| R3         | se0/0/0   | 10.10.2.2     | /30    | -             |
| R3         | se0/0/1   | 10.10.3.2     | /30    | -             |
| R3         | fa0/0     | 192.168.2.254 | /24    | -             |
| PC-server  | fa0       | 172.16.100.2  | /29    | -             |
| PC-admin   | fa0       | 172.16.100.3  | /29    | -             |
| PC-client1 | fa0       | dhclient      | /24    | 192.168.1.254 |
| PC-client2 | fa0       | dhclient      | /24    | 192.168.1.254 |
| PC-client3 | fa0       | dhclient      | /24    | 192.168.2.254 |
| PC-client4 | fa0       | dhclient      | /24    | 192.168.2.254 |

### Konfigurasi

#### R1

1. Konfigurasi alamat ip

   ```console
   Router(config)#interface serial 0/0/0
   Router(config-if)#ip address 10.10.1.1 255.255.255.252
   Router(config-if)#clock rate 125000
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface serial 0/0/1
   Router(config-if)#ip address 10.10.2.1 255.255.255.252
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface fastEthernet 0/0
   Router(config-if)#ip address 192.168.1.254 255.255.255.0
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#
   ```

   > **Catatan:**
   > Konfigurasikan clock rate pada setiap interface DCE (icon jam).

2. Konfigurasi dhcp server

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/02.png){: .normal }

3. Konfigurasi routing ospf

   ```console
   Router(config)#router ospf 1
   Router(config-router)#router
   Router(config-router)#router-id 1.1.1.1
   Router(config-router)#network 10.10.1.0 0.0.0.3 area 0
   Router(config-router)#network 10.10.2.0 0.0.0.3 area 0
   Router(config-router)#network 192.168.1.0 0.0.0.255 area 0
   Router(config-router)#exit
   Router(config)#
   ```

   > **Catatan:**
   > Lihat kembali cara menghitung wildcard mask.

#### R2

1. Konfigurasi alamat ip

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/03.png){: .normal }

2. Konfigurasi routing ospf

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/04.png){: .normal }

#### R3

1. Konfigurasi alamat ip

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/05.png){: .normal }

1. Konfigurasi dhcp server

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/06.png){: .normal }

1. Konfigurasi routing ospf

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/07.png){: .normal }

#### PC-server

1.  Konfigurasi alamat ip

    ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/08.png){: .normal }

2.  Konfigurasi mail server

    ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/09.png){: .normal }

#### PC-admin

1. Konfigurasi alamat ip

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/10.png){: .normal }

2. Konfigurasi mail client

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/11.png){: .normal }

#### PC-client

1. Konfigurasi alamat ip

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/12.png){: .normal }

2. Konfigurasi mail client

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/13.png){: .normal }

### Pengujian

1. Menampilkan routing table di router R1, R2, R3

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/14a.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/14b.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/14c.png){: .normal }

   > **Catatan:**
   > Kode `O` merupakan indikator jaringan dari router lain yang mengaktifkan protocol routing OSPF.

2. Mengirim perintah ping dari PC client1 ke PC mail server dan client3

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/15.png){: .normal }

3. Mengirim perintah ping dari PC client4 ke PC admin dan client2

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/16.png){: .normal }

4. Mengirim email dari PC client1 ke PC admin

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/17a.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/17b.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/17c.png){: .normal }

5. Membalas email dari PC admin ke dan client1

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/18a.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/18b.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/18c.png){: .normal }

6. Lakukan langkah yang sama untuk menguji jaringan dari PC yang lain

### Konfigurasi Ulang

#### PC-server

1. Konfigurasi dns server

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/19.png){: .normal }

1. Tambahkan alamat dns server

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/20.png){: .normal }

#### PC-admin

1. Tambahkan alamat dns server

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/21.png){: .normal }

1. Gunakan domain pada konfigurasi mail client

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/22.png){: .normal }

#### R1

1. Tambahkan alamat dns server pada dhcp pool

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/23.png){: .normal }

#### R3

1. Tambahkan alamat dns server pada dhcp pool

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/24.png){: .normal }

#### PC-client

1. Request ulang alamat ip, dhcp->static->dhcp

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/25.png){: .normal }

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/25a.png){: .normal }

1. Gunakan domain pada konfigurasi mail client

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/26.png){: .normal }

### Pengujian Ulang

1. Lakukan langkah yang sama pada bagian Pengujian sebelumnya

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi OSPF dengan instruksi sebagai berikut

1. Rancang topologi jaringan routing OSPF sebagai berikut

   ![](/assets/img/2023-01-22-konfigurasi-ospf-single-area-pada-cisco-packet-tracer/27.png){: .normal }

   dengan spesifikasi sebagai berikut

   | Routing Protocol    | OSPF                  |
   | ------------------- | --------------------- |
   | Jaringan Acuan      | 172.16.0.0/23         |
   | Web Server Domain   | https://web.kalpa.com |
   | Email Server Domain | mail.kalpa.com        |
   | Email Client Domain | `user`@kalpa.com      |
   | SSID                | kalpa.wifi            |
   | WPA2-PSK            | P@ssw0rd!             |
   | Encryption          | AES                   |

   serta jaringan subnetting vlsm sebagai berikut

   | ID  | Subnet Name | Number of Hosts |
   | --- | ----------- | --------------- |
   | 1   | WAN1        | 2               |
   | 2   | WAN2        | 2               |
   | 3   | WAN3        | 2               |
   | 4   | WAN4        | 2               |
   | 5   | LAN1        | 4               |
   | 6   | LAN2        | 4               |
   | 7   | LAN3        | 4               |
   | 8   | LAN4        | 250             |
   | 9   | LAN5        | 50              |
   | 10  | LAN6        | 100             |

1. Gunakan perhitungan vlsm berikut untuk memberi pengalamatan pada topologi jaringan yang dibangun

   | Name | Hosts Needed | Network Address | Slash | Subnet Mask     | Usable Range    | Broadcast    | Wildcard  |
   | ---- | ------------ | --------------- | ----- | --------------- | --------------- | ------------ | --------- |
   | LAN4 | 250          | 172.16.0.0      | /24   | 255.255.255.0   | .0.1 - .0.254   | 172.16.0.255 | 0.0.0.255 |
   | LAN6 | 100          | 172.16.1.0      | /25   | 255.255.255.128 | .1.1 - .1.126   | 172.16.1.127 | 0.0.0.127 |
   | LAN5 | 50           | 172.16.1.128    | /26   | 255.255.255.192 | .1.129 - .1.190 | 172.16.1.191 | 0.0.0.63  |
   | LAN1 | 4            | 172.16.1.192    | /29   | 255.255.255.248 | .1.193 - .1.198 | 172.16.1.199 | 0.0.0.7   |
   | LAN2 | 4            | 172.16.1.200    | /29   | 255.255.255.248 | .1.201 - .1.206 | 172.16.1.207 | 0.0.0.7   |
   | LAN3 | 4            | 172.16.1.208    | /29   | 255.255.255.248 | .1.209 - .1.214 | 172.16.1.215 | 0.0.0.7   |
   | WAN1 | 2            | 172.16.1.216    | /30   | 255.255.255.252 | .1.217 - .1.218 | 172.16.1.219 | 0.0.0.3   |
   | WAN2 | 2            | 172.16.1.220    | /30   | 255.255.255.252 | .1.221 - .1.222 | 172.16.1.223 | 0.0.0.3   |
   | WAN3 | 2            | 172.16.1.224    | /30   | 255.255.255.252 | .1.225 - .1.226 | 172.16.1.227 | 0.0.0.3   |
   | WAN4 | 2            | 172.16.1.228    | /30   | 255.255.255.252 | .1.229 - .1.230 | 172.16.1.231 | 0.0.0.3   |

1. Setiap Router, PC maupun client lain dapat saling terhubung melalui jaringan OSPF.

1. Setiap Router, PC maupun client lain dapat mengenali domain dari web server.

1. Daftarkan 1 buah akun untuk setiap client dan admin, minimal ada 2

   | Name            | Username                           | Password |
   | --------------- | ---------------------------------- | -------- |
   | [nama1-lengkap] | [nama1-panggilan][urut1]@kalpa.com | !H1dd3n  |
   | [nama2-lengkap] | [nama2-panggilan][urut2]@kalpa.com | !R@has14 |

1. Setiap PC maupun client lain dapat berkomunikasi dengan email sesuai akun yang ditentukan.
