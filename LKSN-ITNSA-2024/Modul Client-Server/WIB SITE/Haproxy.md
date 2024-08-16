## HAPROXY
### Konfigurasi Haproxy untuk Load Balancer pada FW-WIB
Tugas ini tidak ada dalam soal pre-test tetapi saya tetap membuat ini karena beberapa hal, yang pertama agar konfigurasi Web Server untuk wwww.barat.id bisa berjalan, yang kedua karena agar saya ingat.
### Step 1 - Setup
Install haproxy pada FW-WIB.
### Step 2 - Konfigurasi
Lakukan konfigurasi pada directory /etc/haproxy/ | Saran saya agar melakukan copy pada file sample yang sudah disediakan

Dan buat tambahkan di bawah seperti di bawah:
```bash
frontend barat-frontend
        bind *:80
        option forwardfor
        mode http
        default_backend barat-backend
backend barat-backend
        balance roundrobin
        server linsrv1 10.10.10.10:80 check
```
Lalu save filenya dan restart service nya.
