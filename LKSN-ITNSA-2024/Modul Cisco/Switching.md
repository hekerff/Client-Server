## Part 1 - VTP
### Konfigurasi VTP pada semua switch

**SWL3-1**
```bash
conf t
vtp mode server
vtp domain lksn2024.id
vtp version 3
# vtp primary
vlan 30
name MANAGEMENT

teruskan sesuai soal
```

**SWL Client**
```bash
vtp mode client
vtp domain lksn2024.id
vtp version 3
```

## Part 2 - Etherchannel
**SWL3-1 & SWL2-1** etherchannel only
```bash
int r g0/2-3
channel-group 1 mode on
int po1
swit trunk enc dot1
swit mod trunk
```
**SWL3-1 & SWL3-2** Lacp
```bash
int r g2/0-1
channel-group 2 mode active -> 1, passive -> 2.
int po2
swit trunk enc dot1
swit mod trunk
```
**SWL3-2 & SWL2-2** Cisco Proprietary
```bash
int r g0/2-3
channel-group 3 mode desirable -> swl3, auto -> swl2
int po3
swit trunk enc dot
swit mod trunk
```

## Part 3 - Portfast
**Pada setiap port yang mengarah ke end device**
```bash
Masuk ke interfacenya masing masing
spanning-tree postfast
```


## Part 4 - Trunking
Lakukan pada Port yang mengarah ke Switch
```bash
masuk ke interfacecnya

switchport trunk enc dot1
switchport mode trunk
switchport nonegotiate
switch trunk allow vlan 30,40,50
switch trunk native vlan 99
```
