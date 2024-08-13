## DNS Server
### Konfigurasi DNS Server di WIB Site.
Akan ada 2 DNS Server pada WIB, LINSRV1 dan LINSRV2. Yang 1 memiliki fungsi sebagai master lalu melakukan Forwarding Request ke 32.12.10.120. dan LINSRV2 menjadi Slave saja.
### Step 1 - Installing DNS Service
Lakukan pada kedua server.
```bash
apt install bind9 dnsutils
```
### Step 2 - Configure DNS Server LINSRV1
Lakukan konfigurasi DNS Server basic seperti biasa.
![FORWARD](https://github.com/user-attachments/assets/7c9e3655-2f78-4437-bd91-004e3f8ae087)
### Step 3 - Configure Forwarder
edit file pada /etc/bind/named.conf.option, lalu lakukan perubahan seperti ini.

nanti gua isi gambar nya.

Setelah itu, restart servicenya.

### Step 4 - Configure DNS Server Slave di LINSRV2
Edit pada file /etc/bind/named.conf.local, lalu rubah seperti ini.
![slave](https://github.com/user-attachments/assets/cf12529b-0064-47af-9a46-507f071fe424)

Setelah itu, save file nya dan restart servicenya

### DONE
