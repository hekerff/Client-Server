## Konfigurasi DHCP Lease
### Requirements before configuring Static DHCP Lease
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
---
### Apa itu Static DHCP Lease
Static DHCP Lease adalah service DHCP biasa yang mana Server (yang memberikan IP) akan memberikan IP Static ke pada client ( jadi ip nya gak berubah berubah dia gitu looohhh ). Server nantinya hanya perlu memasukan ethernet address/MAC Address dari Client dan IP Static yang akan diberikan.
### Step 1 - Konfigurasi DHCP Server
Lakukan konfigurasi seperti biasanya pada bagian server ( karena sudah ada tutor nya oleh mas Dio, jadi saya akan mencantumkan link nya saja)
- [Tutorial Konfigurasi DHCP Server by Mas Dio](https://github.com/diotriandika/learn-networking/blob/main/Linux/Basic%20Configuration/DHCP-Server.md)
### Step 2 - Konfigurasi Static DHCP Lease
Jadi kita perlu mencatat Ethernet Address / Mac Address dari Client. Kita bisa melihatnya dengan mengetikan :
```bash
ip a
```
![ethernet](https://github.com/user-attachments/assets/65456c8b-ae5c-4eeb-8c9c-8840b85a7ff9)
Setiap client pasti akan berbeda.

Setelah itu kita edit konfigurasi yang sebelumnya, yaitu pada file **dhcpd.conf** dan tambahkan command seperti berikut:
![lease](https://github.com/user-attachments/assets/13a3b34c-f143-4b01-b6b4-424ad85c7fd4)

Setelah itu save konfigurasi dan restart servicenya.

Lalu pada bagian client kalian hanya perlu konfigurasi dhcp client seperti biasa.
### DONE
