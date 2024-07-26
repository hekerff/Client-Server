## Configure ProFTPD
### Requirements before configuring Proftpd
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
---
### Pendahuluan
Saya akan melakukan konfigurasi File Server menggunakan ProFTPD karena katanya lebih mudah and simpel so lets gooo
---
### Step 1 - Installing Package
Ya seperti biasa, install package nya dolo
```bash
apt install proftpd -y
```
### Step 2 - Edit the Configuration File
Ya selanjutnya kita perlu melakukan perubahan sedikit pada file konfigurasi dari proftpd-nya.
```bash
sudo nano /etc/proftpd/proftpd.conf
```
Lalu cari bagian - bagian berikut dan uncomment ( Hapus tanda #-nya )
- ServerName "Debian FTP Server"
- DefaultRoot ~  
- RequireValidShell off

Untuk DefaultRoot kalian bisa menggunakan DefaultRoot ~ atau DefaultRoot /

**DefaultRoot** ~ : Digunakan agar para user ftp hanya bisa mengakses directory default nya sendiri.
**DefaultRoot** / : Digunakan agar para user ftp dapat mengakses semua Directory.

Jika sudah, Save File & Restart the Service
```bash
sudo systemctl restart proftpd
sudo systemctl enable proftpd
```
### Step 2 - Management User & Directory
Selanjutnya kita perlu memanajemen User & Directory, agar tidak sembarang user dapat melakukan pengubahan file di server.
```bash
adduser ftpuser
```
itu untuk menambahkan user baru. Setelah itu kita perlu mengatur izin dari user tersebut.
```bash
sudo chown ftpuser:ftpuser /home/ftpuser
sudo chmod 755 /home/ftpuser
```
**DONE**
### PENGUJIAN
Selanjutnya kita uji dengan cara login bos dari client.

Pada sisi client kalian perlu juga menginstall package proftpd. lalu coba login dengan menggunakan command berikut:
```bash
ftp ip_file_server
```
Lalu masukan Username & Password-nya. DONE. berikut cheatsheet command di proftpd.
```bash
ls                 # List files in the current directory
cd [directory]     # Change directory
get [file]         # Download file from the server
put [file]         # Upload file to the server
bye                # Disconnect from the server
```

### Sumber saya ambil dari ChatGPT
