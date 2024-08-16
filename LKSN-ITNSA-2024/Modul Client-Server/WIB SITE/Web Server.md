## WEB SERVER
### Konfigurasi Web Server pada LINSRV1 dan LINSRV2
Konfigurasi ini akan menjadi sangat panjang, jadi saya akan bagi untuk LINSRV1 dan LINSRV2.
## LINSRV 1
### Pendahuluan
Untuk LINSRV 1 akan menggunakan Apache2 sebagai Web Server nya lalu perlu ditambahkan HTTP header "X-Served-By" dengan value hostnamenya sendiri.
### Step 1 - Configure Apache2 File Configuration
Saya akan menggunakan File Defaultnya hanya diubah sedikit sesuai dengan soal.
![apache2](https://github.com/user-attachments/assets/135afdda-370c-4291-a59b-260fbd278b05)

Tambahkan seperti berikut untuk menambahkan HTTP Header : "Header set X-Served-By LINSRV1.barat.id"

Setelah itu save file konfigurasi dan aktifkan module header apache2 dengan cara masukan command berikut:
```bash
a2enmod headers
```
### Step 2 - File Index HTML
Lalu buat file HTML sesuaikan dengan tasks, edit saja pada file /var/www/html/index.html

Jikalau sudah, Restart Apache2.
**Selesai**

## LINSRV2
### Pendahuluan!!!
Kita akan melakukan konfigurasi Web Server pada LINSRV2 menggunakan NGINX dan kita akan melakukan hosting 2 virtual host. Untuk www.barat.id dan file.barat.id.
### Step 1 - Setup
Karena Apache2 otomatis terinstall maka kita akan stop terlebih dahulu servicenya, bisa gunakan systemctl stop apache2. Setelah itu kita akan melakukan installasi NGINX dan apache2-utils untuk basic authenticationnya.
```bash
apt install nginx apache2-utils
```
### Step 2 - Konfigurasi untuk www.barat.id
Untuk website www.barat.id, kita edit saja pada file default dari NGINXnya.
```bash
nano /etc/nginx/sites-available/default
```
Hapus semuanya dan buat yang baru dari awal, seperti ini:
![NGINX](https://github.com/user-attachments/assets/c0f5f44f-6843-40a4-a77b-0ac9b3af0c2a)

(Jangan Lupa tambahkan tanda ; pada akhir baris. itu gambar di atas lupa gwehj isi)

Hampir sama seperti konfigurasi dasar namun ditambahkan **add_header X-Served-By "LINSRV2.barat.id"**

Untuk file HTML, lakukan hal yang sama seperti LINSRV1 yaitu edit pada file /var/www/html/index.html

Jikalau sudah semuanya, restart nginx.

### Step 3 - Konfigurasi untuk file.barat.id
Hal pertama yang perlu disiapkan adalah file .crt untuk mengaktifkan protokol HTTPS, kirim file tersebut dari Server CA ke LINSRV2.

Buat file baru bernama "file" di /etc/nginx/sites-available/ Setelah itu buatlah Symbolic Link dari sites-available/file ke sites-enabled/
```bash
touch /etc/nginx/sites-available/file
ln -s /etc/nginx/sites-available/file /etc/nginx/sites-enabled/
```

Setelah itu kita edit file
```bash
nano /etc/nginx/sites-available/file
```
![linsrv_file](https://github.com/user-attachments/assets/a2e9ae14-4e69-42f3-83a6-75b1c3376a65)

Untuk mengaktifkan Redirect dari HTTP ke HTTPS, tambahkan:

**return 301 https://$host$request_uri;**

dan untuk mengaktifkan HTTPS nya tambahkan seperti di tanda panah dalam server { listen 443 ssl.

**autoindex on;** 

Berfungsi untuk menampilkan isi dari directory /data/file/ | Sehingga ini menjadikan file.barat.id sebagai file server melalui web.

### Step 4 - Konfigurasi Basic Authentication
Konfigurasinya menggunakan htpasswd
```bash
htpasswd -c /etc/nginx/rahasia rahasia
Skills39
```
Jika sudah selesai, restart service nginx.

- **NOTE**: Task untuk Web Server LINSRV2 agak nguawor yak, disuruh konfigurasi 2 Virtual Host yang sama sama menggunakan 1 port yang sama yaitu 80 (http), lalu record untuk www.barat.id malah ke Server FW-WIB, nguawor. Masuk akal bila dikonfigurasi Proxy Server di sana, tapi di sini enggak disuruh.
