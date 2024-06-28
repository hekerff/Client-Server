## Configure Load Balance using HAProxy
---
### Pendahuluan
Pada konfigurasi ini akan sedikit menguras otak dan tenaga karena menurut saya konfigurasi Load Balancing kali ini butuh pemahaman yang cukup mendalam untuk melakukan konfigurasinya, jadi saran saya agar menonton/membaca materi atau penjalasan mengenai load balancing terlebih dahulu.
Baiklah, untuk study kasusnya... saya ingin melakukan load balancing antara 2 web server.
Web Server Left & Web Server Right.
Left akan ditandai dengan warna merah dan Right berwarna biru.
Konfigurasi kali ini akan sangat panjang jadi saran saya adalah untuk membaca dan memahaminya dengan pelan - pelan.

---
### Requirements before configuring HAProxy
- Pastikan sudah memakai user **root**
- Sudah terkonfigurasi web server NGINX dikedua server (Left & Right).
- Sudah terkonfigurasi DNS Server (optional)
- Masing - Masing Web Server harus menggunakan port yang berbeda satu sama lain untuk setiap Web
- Masing - Masing Web Server tidak boleh menggunakan port 80 untuk Web nya. Ini terkhusus pada konfigurasi saya (tidak tau yang lain)
- Web untuk server **Left** akan menggunakan port 9090 dan untuk **Right** menggunakan port 8080
---
### Konfigurasi NGINX
Saya menggunakan konfigurasi Web Server yang sama pada tutorial **Web Server + Basic Auth**.

**SERVER "RIGHT":**
![right](https://github.com/hekerff/Client-Server/assets/159868331/5d311f50-d33a-4840-b089-7bd45b3fc6f0)


**SERVER "LEFT":**
![left](https://github.com/hekerff/Client-Server/assets/159868331/11280977-2fb5-4abe-be24-b3b3a6ff58c4)

---

### Konfigurasi file HTML
**Server RIGHT:**
![blue](https://github.com/hekerff/Client-Server/assets/159868331/bbba648c-0f89-4122-a020-07aa006c5173)

**Server LEFT:**
![red](https://github.com/hekerff/Client-Server/assets/159868331/d77a7042-ec8a-4f56-926e-dc4147936248)

---
### Step 1 - Installing HAProxy
Install pada ke dua server **Left & Right**
```bash
apt install haproxy -y
```

### Step 2 - Configure Haproxy
Konfigurasi pada ke 2 server
```bash
cd /etc/haproxy/
nano haproxy.cfg
#Pada bagian paling bawah tambahkan seperti berikut:
frontend radeon-front  <--- #(radeon-front) boleh diganti bebas (Optional)
        bind *:80
        mode http
        option forwardfor
        default_backend radeon-backend  <--- #radeon-backend boleh bebas diganti
backend radeon-backend  <--- #nama nya disamakan sama yang diatas
        balance roundrobin  
        server right 172.xxx.xxx.1:8080
        server left 172.xxx.xxx.2:9090
```
![haproxy](https://github.com/hekerff/Client-Server/assets/159868331/bd4101ca-4659-4267-973f-18d4cbf8ddc2)

**SAVE FILE & RESTART HAPROXY SERVICE**

---
### DONE - TESTING TIME :)
Pengujian dapat dilakukan dengan mencoba mengakses Web Server lalu coba dengan **Refresh** web tersebut berkali - kali, jika konfigurasi berhasil maka tampilan web akan berubah-ubah.
Ini karena Algoritma Roundrobin yang membagi traffic ke 2 server (Left & Right).

https://github.com/hekerff/Client-Server/assets/159868331/8e9f0d2a-baf1-4c1f-b838-9cf55b866ab3
