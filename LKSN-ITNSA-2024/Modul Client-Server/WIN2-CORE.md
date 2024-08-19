## Windows Server 2022 Core
### Darurat
Ya darurat

## Basic
### Mengganti Hostname
di cmd.exe ketik angka 2 ==> Masukan Computer Name ==> Pilih yes jika ingin restart, No jika tidak
### Mengatur IP
di cmd.exe ketik angka 8 ==> Ketik 1 ==> Ketik 1 ==> Lalu lanjutkan sesuai tasks
### Allow ICMP
Buka Powershell (15)

Lalu ketikkan seperti berikut
```powershell
New-NetFirewallRule -Displayname "Allow-ICMP" -Protocol ICMPv4 -IcmpType 8 -Direction Inbound -Action Allow
```
---

### Partisi Disk

Untuk Melihat List Available Disk
```powershell
Get-Disk
```
