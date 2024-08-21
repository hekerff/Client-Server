## Basic Configuration
### Basic Configuration of cisco
Untuk konfigurasi ini saya akan berpatokan pada soal Pre-Test Modul Cisco LKSN 2024.

**NOTE: masukan command: "no switchport" pada SWL3 di port yang akan ditambahkan IP.**

**LAKUKAN PADA SETIAP DEVICE CISCO**
```bash
en
conf t
hostname <sesuaikan>
ip domain-name lksn2024.id
enable secret P@ssw0rd
username admin priv 15 secret P@ssw0rd

banner motd ! <enter>
Unauthorized Access is Strictly Prohibited
!

clock timezone GMT +7
```
### IP ADDRESS

**IPV6**
Masuk pada Interfacenya masing masing.
```bash
ipv6 enable
ipv6 address xxx:xxx:xxx:xxx/64
```
