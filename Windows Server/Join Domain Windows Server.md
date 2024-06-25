## How to join domain in Windows Server 2022
---
### Requirements before join domain
- IP Address sudah terkonfigurasi
- DNS sudah disetting, pastikan mengarah ke IP Address si domain controller
- Hostname sudah terkonfigurasi
- Active Directory terkonfigurasi
- Sysprep
---
## Berikut langkah - langkahnya :
- Buka "Server Manager" lalu pilih menu Local Server.
- Pada Local Server, klik pada Computer Name(tulisan warna biru).
- Pilih **Change...**
- Edit Computer Name (Sesuaikan).
- Lalu pada Member of, pilih **Domain** dan masukan nama domain yang sudah dikonfigurasi.
- Ketika diminta memasukan Username dan Password, gunakan user **Administrator** dan masukan passwordnya.
### Selesai
![Screenshot 2024-06-25 150846](https://github.com/hekerff/Client-Server/assets/159868331/2d8857fe-8f8a-47f2-9145-dc4a31664320)
