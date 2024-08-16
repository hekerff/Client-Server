## SSH
### Konfigurasi SSH Server di LINSRV2
Ini adalah pembahasan pada task SSH untuk soal pre-test lksn 2024
### Install SSH Server
```bash
apt install openssh-server
```
### Create User
Pada LINSRV2 buat user **file** dengan password **Skills39s** dan atur home directory nya ke /data/file/
```bash
useradd -m -d /data/file/ -s /bin/bash file
```
Lalu atur passwordnya
```bash
passwd file
```

Pada LINCLT buat user **user** dengan password Skills39s, lalu atur agar bisa masuk sudo.

---

### Configure SSH from client to server
Pada task ini kita diminta untuk melakukan konfigurasi agar 'user' dari client dapat melakukan ssh ke file@linsrv2.barat.id tanpa perlu memasukan password.
### Step 1 - Generate SSH Key Pair on Client
Di Client, login menggunakan user **user**
```bash
ssh user@linclt
```
lalu generate SSH key pair
```bash
ssh-keygen -t rsa -b 4096
```
- -t : untuk menentukan algoritma menggunakan rsa.
- -b : untuk menentukan banyak bit biner yang digunakan.
Setelah itu Enter sampai selesai (biarkan default).
### Step 2 - Copy the Public Key to LINSRV2
Sekarang kita akan melakukan copy Public Key dari client ke server
```bash
ssh-copy-id file@linsrv2.barat.id
```
### Step 3 - Testing
Coba untuk melakukan ssh dari client menggunakan user **user**, ssh ke file@linsrv2.barat.id
### Troubleshooting
Jika tidak bisa pada step 2 coba lakukan beberapa kemungkinan berikut:
- Pada LINSRV2, coba buat directory .ssh pada directory home dari user file
- Ganti permision untuk folder /data/file/ menjadi punya user file
```bash
chown -R file:file /data/file
```
- -R berfungsi sebagai recursive (folder & file)

### Change SSH port default to 2024
Edit pada file /etc/ssh/sshd_config, setelah itu buka pagar pada port dan ganti ke 2024.
