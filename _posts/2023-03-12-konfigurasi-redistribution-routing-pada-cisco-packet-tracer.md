---
layout: post
title: Konfigurasi Redistribution Routing pada Cisco Packet Tracer
date: 2023-03-12 00:00 +0000
author: angga
categories: [Konfigurasi]
tags: [cisco, routing]
---

## Ulasan

Redistribution routing adalah proses pengambilan rute dari satu protokol routing dan menyebarkannya ke protokol routing lain. Hal ini memungkinkan perangkat untuk memperluas jangkauan routing dan menyediakan konektivitas antara jaringan yang sebelumnya terisolasi.

Redistribusi routing digunakan ketika ada beberapa protokol routing dalam jaringan yang harus saling terhubung. Misalnya, jika suatu jaringan menggunakan OSPF dan ada perangkat dengan protokol EIGRP yang ingin terhubung, maka administrator dapat menggunakan redistribusi routing untuk membuat koneksi antara kedua protokol tersebut.

## Alat dan Bahan

1. Komputer
2. Cisco Packet Tracer
3. Cisco Skills for All / Akun Cisco NetAcad

## Perintah CLI

| Perintah                                                                                                                                 | Deskripsi                                                    |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------- |
| Router(config-router)#redistribute static metric `metric-number`                                                                         | mengaktifkan redistribusi jaringan routing statis ke RIP     |
| Router(config-router)#redistribute connected metric `metric-number`                                                                      | mengaktifkan redistribusi jaringan directly-connected ke RIP |
| Router(config-router)#redistribute ospf `process-id` metric `Bandwidth-value` `Delay-value` `Reliability-value` `Load-value` `MTU-value` | mengaktifkan redistribusi jaringan OSPF ke EIGRP             |
| Router(config-router)#redistribute eigrp `process-id` metric `metric-value` subnets                                                      | mengaktifkan redistribusi jaringan EIGRP ke OSPF             |
| Router(config-router)#redistribute ospf `process-id` metric `metric-value` subnets                                                       | mengaktifkan redistribusi jaringan OSPF ke RIP               |
| Router(config-router)#redistribute rip subnets                                                                                           | mengaktifkan redistribusi jaringan RIP ke OSPF               |
| Router(config-router)#redistribute eigrp `process-id` metric `metric-value` subnets                                                      | mengaktifkan redistribusi jaringan EIGRP ke RIP              |
| Router(config-router)#redistribute rip `process-id` metric `Bandwidth-value` `Delay-value` `Reliability-value` `Load-value` `MTU-value`  | mengaktifkan redistribusi jaringan RIP ke EIGRP              |

## Langkah Kerja 1 : Static dan RIP

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/01.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/redistribution_routing_unconfig_1_static_rip.pkt){:target="\_blank"}.

### Konfigurasi

#### Router0

1. Konfigurasi alamat ip pada interface

   ```console
    Router(config)#interface gigabitEthernet 0/0
    Router(config-if)#ip address 172.16.10.254 255.255.255.0
    Router(config-if)#no shutdown
    Router(config-if)#exit
    Router(config)#interface serial 0/0/0
    Router(config-if)#ip address 10.100.100.1 255.255.255.252
    Router(config-if)#clock rate 125000
    Router(config-if)#no shutdown
    Router(config-if)#exit
    Router(config)#
   ```

2. Konfigurasi dhcp server

   ```console
    Router(config)#ip dhcp pool lan10
    Router(dhcp-config)#network 172.16.10.0 255.255.255.0
    Router(dhcp-config)#default-router 172.16.10.254
    Router(dhcp-config)#exit
    Router(config)#ip dhcp excluded-address 172.16.10.254
    Router(config)#
   ```

#### Router1

1. Konfigurasi alamat ip pada interface

   ```console
    Router(config)#interface serial 0/0/0
    Router(config-if)#ip address 10.100.100.2 255.255.255.252
    Router(config-if)#no shutdown
    Router(config-if)#exit
    Router(config)#interface serial 0/0/1
    Router(config-if)#ip address 10.200.100.1 255.255.255.252
    Router(config-if)#clock rate 125000
    Router(config-if)#no shutdown
    Router(config-if)#exit
    Router(config)#
   ```

#### Router2

1. Konfigurasi alamat ip pada interface

   ```console
   Router(config)#interface serial 0/0/0
   Router(config-if)#ip address 10.200.100.2 255.255.255.252
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#interface gigabitEthernet 0/0
   Router(config-if)#ip address 172.16.20.254 255.255.255.0
   Router(config-if)#no shutdown
   Router(config-if)#exit
   Router(config)#
   ```

1. Konfigurasi dhcp server

   ```console
   Router(config)#ip dhcp pool lan20
   Router(dhcp-config)#network 172.16.20.0 255.255.255.0
   Router(dhcp-config)#default-router 172.16.20.254
   Router(dhcp-config)#exit
   Router(config)#ip dhcp excluded-address 172.16.20.254
   Router(config)#
   ```

#### PC

1. Konfigurasi alamat ip pada interface LAN10

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/02.png){: .normal }

1. Konfigurasi alamat ip pada interface LAN20

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/03.png){: .normal }

#### Router0

1. Konfigurasi routing

   ```console
   Router(config)#ip route 172.16.20.0 255.255.255.0 10.100.100.2
   Router(config)#ip route 10.200.100.0 255.255.255.252 10.100.100.2
   Router(config)#
   ```

#### Router1

2. Konfigurasi routing

   ```console
   Router(config)#ip route 172.16.10.0 255.255.255.0 10.100.100.1
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#no auto-summary
   Router(config-router)#network 10.200.100.0
   Router(config-router)#exit
   Router(config)#
   ```

#### Router2

3. Konfigurasi routing

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#no auto-summary
   Router(config-router)#network 10.200.100.0
   Router(config-router)#network 172.16.20.0
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi retribution routing

   ```console
   Router(config)#router rip
   Router(config-router)#redistribute static metric 1
   Router(config-router)#redistribute connected metric 1
   Router(config-router)#exit
   Router(config)#
   ```

### Pengujian

#### Router0

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/16.png){: .normal }

#### Router1

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/17.png){: .normal }

#### Router2

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/18.png){: .normal }

#### PC

1. Uji jaringan PC dengan kirim packet `Simple PDU`

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/19.png){: .normal }

## Langkah Kerja 2 : RIP dan OSPF

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/20.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/redistribution_routing_unconfig_2_rip_ospf.pkt){:target="\_blank"}.

### Konfigurasi

#### Router0

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/21.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/22.png){: .normal }

#### Router1

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/23.png){: .normal }

#### Router2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/24.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/25.png){: .normal }

#### PC

1. Konfigurasi alamat ip pada interface anggota LAN1

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/26.png){: .normal }

2. Konfigurasi alamat ip pada interface anggota LAN2

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/27.png){: .normal }

#### Router0

1. Konfigurasi routing

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#network 10.1.1.0
   Router(config-router)#network 192.168.1.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#network 10.1.1.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#router ospf 100
   Router(config-router)#network 10.2.1.0 0.0.0.7 area 0
   Router(config-router)#exit
   Router(config)#
   ```

#### Router2

1. Konfigurasi routing

   ```console
   Router(config)#router ospf 100
   Router(config-router)#network 10.2.1.0 0.0.0.7 area 0
   Router(config-router)#network 192.168.2.0 0.0.0.63 area 0
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing retribution

   ```console
   Router(config)#router rip
   Router(config-router)#redistribute ospf 100 metric 1
   Router(config-router)#exit
   Router(config)#router ospf 100
   Router(config-router)#redistribute rip subnets
   Router(config-router)#exit
   Router(config)#
   ```

### Pengujian

#### Router0

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/28.png){: .normal }

#### Router1

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/29.png){: .normal }

#### Router2

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/30.png){: .normal }

#### PC

1. Uji jaringan PC dengan kirim packet `Simple PDU`

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/31.png){: .normal }

## Langkah Kerja 3 : RIP dan EIGRP

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/32.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/redistribution_routing_unconfig_3_rip_eigrp.pkt){:target="\_blank"}.

### Konfigurasi

#### Router0

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/33.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/34.png){: .normal }

#### Router1

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/35.png){: .normal }

#### Router2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/36.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/37.png){: .normal }

#### PC

1. Konfigurasi alamat ip pada interface anggota LAN101

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/38.png){: .normal }

2. Konfigurasi alamat ip pada interface anggota LAN102

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/39.png){: .normal }

#### Router0

1. Konfigurasi routing

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#network 172.16.1.0
   Router(config-router)#network 192.168.101.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing

   ```console
   Router(config)#router rip
   Router(config-router)#version 2
   Router(config-router)#network 172.16.1.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#router eigrp 100
   Router(config-router)#network 172.16.2.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router2

1. Konfigurasi routing

   ```console
   Router(config)#router eigrp 100
   Router(config-router)#network 172.16.2.0
   Router(config-router)#network 192.168.102.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing retribution

   ```console
   Router(config)#router rip
   Router(config-router)#redistribute eigrp 100 metric 1
   Router(config-router)#exit
   Router(config)#router eigrp 100
   Router(config-router)#redistribute rip metric 1 1 1 1 1
   Router(config-router)#exit
   Router(config)#
   ```

### Pengujian

#### Router0

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/40.png){: .normal }

#### Router1

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/41.png){: .normal }

#### Router2

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/42.png){: .normal }

#### PC

1. Uji jaringan PC dengan kirim packet `Simple PDU`

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/43.png){: .normal }

## Langkah Kerja 4 : OSPF dan EIGRP

Pada praktikum kali ini akan terbagi menjadi beberapa langkah yaitu Persiapan, Konfigurasi, dan Pengujian.

### Persiapan

#### Topologi Jaringan

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/04.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/redistribution_routing_unconfig_4_ospf_eigrp.pkt){:target="\_blank"}.

### Konfigurasi

#### Router0

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/05.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/06.png){: .normal }

#### Router1

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/07.png){: .normal }

#### Router2

1. Konfigurasi alamat ip pada interface

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/08.png){: .normal }

2. Konfigurasi dhcp server

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/09.png){: .normal }

#### PC

1. Konfigurasi alamat ip pada interface anggota LAN10

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/10.png){: .normal }

2. Konfigurasi alamat ip pada interface anggota LAN20

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/11.png){: .normal }

#### Router0

1. Konfigurasi routing

   ```console
   Router(config)#router ospf 10
   Router(config-router)#network 192.168.100.0 0.0.0.31 area 0
   Router(config-router)#network 172.16.10.0 0.0.0.3 area 0
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing

   ```console
   Router(config)#router ospf 10
   Router(config-router)#network 172.16.10.0 0.0.0.3 area 0
   Router(config-router)#exit
   Router(config)#router eigrp 100
   Router(config-router)#router eigrp 100
   Router(config-router)#network 172.16.100.0
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router2

1. Konfigurasi routing

   ```console
   Router(config)#router eigrp 100
   Router(config-router)#network 172.16.100.0
   Router(config-router)#network 192.168.100.32
   Router(config-router)#no auto-summary
   Router(config-router)#exit
   Router(config)#
   ```

#### Router1

1. Konfigurasi routing retribution

   ```console
   Router(config)#router eigrp 100
   Router(config-router)#redistribute ospf 10 metric 1 1 1 1 1
   Router(config-router)#exit
   Router(config)#router ospf 10
   Router(config-router)#redistribute eigrp 100 subnets
   Router(config-router)#exit
   Router(config)#
   ```

### Pengujian

#### Router0

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/12.png){: .normal }

#### Router1

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/13.png){: .normal }

#### Router2

1. Konfirmasi routing table

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/14.png){: .normal }

#### PC

1. Uji jaringan PC dengan kirim packet `Simple PDU`

   ![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/15.png){: .normal }

## Berlatih

Sebagai bahan latihan, lakukan konfigurasi redistribution routing dengan topologi jaringan sebagai berikut

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/44.png){: .normal }

![](/assets/img/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/45.png){: .normal }

Topologi jaringan dapat diunduh [di sini](/assets/pkt/2023-03-12-konfigurasi-redistribution-routing-pada-cisco-packet-tracer/redistribution_routing_dinamis_latihan.pka){:target="\_blank"}.

Pengujian jaringan terkonfigurasi dapat dilakukan sebagai berikut

{% include embed/youtube.html id='YT9RVdppaFY' %}
