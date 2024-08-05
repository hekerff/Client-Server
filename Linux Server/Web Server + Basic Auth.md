## Configure Web Server with Basic Authentication
### Requirements before creating Certificate Authority
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
- Saya menggunakan NGINX
---
### Step 1 - Install packages
Dalam konfigurasi kali ini, kita membutuhkan 2 package utama yaitu nginx dan apache2-utils
```bash
apt install nginx apache2-utils
```
### Step 2 - Membuat HTML file
Sebelum melakukan konfigurasi yang utama, kita perlu menyiapkan file HTML terlebih dahulu
```bash
mkdir /var/www/radeon
```
```bash
nano /var/www/radeon/index.html
```
```bash
<!DOCTYPE html>
<html>
<head>
  <title> HAI </title>
</head>
<body>
  <h1> Web Server </h1>
  <p> Ini adalah website latihan web server + Basic Authentication </p1>
</body>
</html
```
### Step 3 - Membuat file konfigurasi web server
```bash
nano /etc/nginx/sites-available/radeon #nama file bebas
```
```bash
server {
        listen 80;
        server_name www.YourDomain.com;
        location / {
              root /var/www/radeon;
              index index.html;
        }
}
```
### Step 4 - Membuat Symbolic Link
```bash
ln -s /etc/nginx/sites-available/radeon /etc/nginx/sites-enabled/
```
**RESTART SERVICE**
```bash
systemctl restart nginx
```
---
**Note**: Jika Web tidak dapat diakses, coba dengan menghapus package apache2.
```bash
apt purge apache2
```
---
### Step 5 - Membuat Basic Authentication
Basic Authentication adalah sistem keamanan pada website yang ketika seseorang ingin mengakses web akan memerlukan **Username** & **Password**

Edit file konfigurasi NGINX yang sudah dibuat tadi
```bash
nano /etc/nginx/sites-available/radeon
```
```bash
server {
        listen 80;
        server_name www.YourDomain.com;
        location / {
              auth_basic "Restricted";
              auth_basic_user_file /etc/nginx/.radeon;
              root /var/www/radeon;
              index index.html;
        }
}
```
**Setelah itu buat User dan Password untuk Login menggunakan htpasswd**
```bash
htpasswd -c /etc/nginx/.user Username #bebas
```
Setelah itu akan diminta untuk mememasukan Password

***DONE**

### Testing
Buka Browser pada Client lalu ketikan IP Address/Sub Domain dari Web Server
![hayyuk](https://github.com/hekerff/Client-Server/assets/159868331/82bf8518-03b1-403b-a96f-39f336b9af18)
Jika muncul tabel untuk memasukan user dan password artinya sudah berhasil :)

