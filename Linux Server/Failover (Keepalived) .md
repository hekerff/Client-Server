## Configure Failover using Keepalived
### Requirements before configuring Failover
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
- 2 Server Linux
Dalam konfigurasi kali ini, saya memakai 2 server linux yang saya beri nama Left & Right. Right akan bertugas sebagai master dan jika Right mati maka akan digantikan oleh Left.
---
### Step 1 - Install the package
Install keepalived pada kedua server
```bash
apt install keepalived -y
```
### Step 2 - Masuk ke directory keepalived
```bash
cd /etc/keepalived/
```
### Step 3 - Copy dan rubah nama file keepalived.conf.sample
```bash
cp keepalived.conf.sample keepalived.conf
```
### Step 4 - Edit file
- Edit file keepalived.conf
```bash
nano keepalived.conf
```
- Hapus bagian - bagian yang tidak terpakai.
- Sisakan seperti yang dibawah ini.
  
**Untuk server Right:**
![vrrp101](https://github.com/hekerff/Client-Server/assets/159868331/191dee70-a3ca-430c-94ac-e2482e7d7feb)


  Rubah pada bagian yang ditandai.
- Sesuaikan dengan interfacenya
- Untuk server right gunakan priority 101 dan untuk server left gunakan priority 100
- Rubah password pada auth_pass (sesuaikan)
- Terakhir, tentukan IP Address Virtual

Save dan Restart service

---
**Untuk memudahkan**, kirim file yang sudah diedit di Server Right ke Server Left.
```bash
scp /etc/keepalived/keepalived.conf user@172.xxx.xxx.xxx:/home/debian/
```
Lalu di server Left, pindahkan file dari directory /home/debian/ menuju /home/keepalived/
```bash
mv /home/debian/keepalived.conf /etc/keepalived/
```
---
**Untuk server Left:**
- Edit file keepalived.conf
```bash
nano /etc/keepalived/keepalived.conf
```
Lalu edit pada bagian priority ubah menjadi 100.
![vrrp100](https://github.com/hekerff/Client-Server/assets/159868331/e7cb5a92-6699-411e-a12e-c187992f87df)

**Save and Restart kedua server**
## Pengujian
Ketika konfigurasi sudah berhasil, nanti akan muncul IP Address virtual di Server Right - Karena priority dia lebih tinggi.
Check dengan:
```bash
ip a
```
![berhasilcuy](https://github.com/hekerff/Client-Server/assets/159868331/07da54a9-53ab-4609-b984-879d193dc6d4)


**DONE**
