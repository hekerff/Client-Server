## Windows Server 2022 Core
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

## Advance
## Active Directory 
### Join Domain
```powershell
Add-Computer -DomainName "lks2024.id" -Credential
Restart-Computer
````
### Install ADDS
```powershell
Install-WindowsFeature -Name AD-Domain-Service -IncludeManagementTools
```
### Configure ADDS Domain Controller
```powershell
Import-Module ADDSDeployment

Install-AddsDomainController -DomainName "lks2024.id" -Credential
```
Masukkan Credential Administrator 
### Restar Computer (Wajib)
```powershell
Restart-Computer
```
### Verifikasi
```powershell
Get-ADDomainController
```

Konfigurasi ADDS akan memudahkan untuk melakukan konfigurasi ISCSI.

---

## ISCSI
### Partisi Disk
Untuk Melihat List Available Disk
```powershell
Get-Disk
```
### Initialize Disk
Setelah kita sudah tau nomor dari disk yang ingin kita partisi, sekarang kita initialize terlebih dahulu.
```powershell
Initialize-Disk -Number 1 -PartitionStyle GPT
```
### Create Partition
Setelah diinitialize kita akan partisi disk nya
```powershell
New-Partition -DiskNumber 1 -UseMaximumSize -DriveLetter G
```
### Format Partisi
```powershell
Format-Volume -DriveLetter G -FileSystem NTFS -NewFileSystemLabel "ISCSI"
```
### Verifikasi
```powershell
Get-Volume -DriveLetter G
```

## Konfigurasi ISCSI
### Install Feature ISCSI Target
```powershell
Install-WindowsFeature -name FS-iSCSITarget-Server
```
### Create Virtual Disk
```powershell
New-IscsiVirtualDisk -Path "G:\iSCSIVirtualHarddisk.vhdx" -Size 5GB
```
### Create Target ISCSI
```powershell
New-IscsiServerTarget -TargetName "BACKUP-TG" -InitiatorIds "IQN:iqn.2024-08.com.example:WINSRV1"
```
### Adding Virtual Disk to the Target
```powershell
Add-IscsiVirtualDiskTargetMapping -TargetName "BACKUP-TG" -Path "G:\iSCSIVirtualHarddisk.vhdx"
```

**Setelah itu kita Restart Service nya***
```powershell
Restart-Service -Name WinTarget
```

### Verifikasi
```powershell
Get-IscsiServerTarget
```
