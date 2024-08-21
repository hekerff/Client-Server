## Part 1 - Routing EIGRP
Lakukan pada server TMT dan SWL3

ketikan command ip routing.

lanjut:
```bash
router eigrp 39
passive-interface default
no passive-interface g0/0
masukan lagi interface lainnya yang mengarah tidak mengarah ke luar site, seperti ke isp atau ke swl2.

network 172.16.30.0 0.0.0.255

masukan semua network yang memang seharusnya di advertise.
```
## Part 2 - Routing OSPF
Konfigurasi Routing OSPF hampir sama seperti EIGRP, kita hanya akan melakukan advertise ke network yang menuju ke ISP saja.

Hidupkan Passive-Interface
```bash
router ospf 11
passive-interface default
```
lalu matikan passive interface di interface yang mengarah ke ISP
```bash
no passive-interface int g0/2
```
Setelah itu advertise public IP Only
```bash
network <public ip> <wildcard> area 0
```
## Part 3 - Default Route
**SWL3**
```bash
ip route 0.0.0.0 0.0.0.0 <ip dari TMT>
```
**Write Memory**



