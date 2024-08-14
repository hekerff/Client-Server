## Active Directory Server
### Konfigurasi Active Directory Server di Windows Server 2022
Pada tugas kali ini, kita disuruh melakukan konfigurasi ADDS pada WINSRV1 & WINSRV2, WINSRV1 sebagai Initial Domain Controller dan WINSRV2 sebagai addition domain controller.
### Step 1 - Installasi WINSRV1
Lakukan installasi seperti biasa, dengan nama domain tengah.id
**NOTE**: Jangan lupa untuk promoting WINSRV1 menjadi domain controller
### Step 2 - Installasi WINSRV2
Installasi seperti biasa, lalu ketika promoting domain controller, pilih opsi paling atas.

lalu masukkan credential seperti ini **administrator@tengah.id**
### Add Group & User
Pada Server Manager, pilih opsi Users and Computer, lalu tambahkan yang bisa ditambahkan.
