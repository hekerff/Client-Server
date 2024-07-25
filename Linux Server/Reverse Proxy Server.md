## Configure Reverse Proxy Server
### Requirements before configuring Reverse Proxy Server
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
- Kalau bisa sudah paham teori tentang Forward Proxy & Reverse Proxy, what's the different between those both
---
### Pendahuluan Konfigurasi
Pada konfigurasi ini saya akan menggunakan topologi seperti berikut:
![Tologi_PRoxy](https://github.com/user-attachments/assets/bee216a8-8e4b-46ab-be4a-c7de0bb6e6ce)

- Saya akan menggunakan 2 Web Server dan 1 Server sebagai Proxy Server.
- Jika dimungkinkan sudah melakukan konfigurasi Web Server ke dua server tersebut menggunakan NGINX.
- Jika dimungkinkan sudah melakukan konfigurasi DNS Server.
- Perlu diperhatikan bahwa saya akan berfokus pada konfigurasi pada **Reverse Proxy Server** saja, karena saya akan berasumsi bahwa anda sudah melakukan konfigurasi Web Server.

IP ADDRESS :
- Reverse Proxy Server : 10.10.0.1 | 192.168.10.1
- Web Server 1 : 10.10.0.10
- Web Server 2 : 10.10.0.20
- Client : 192.168.10.10
- www.ikn.com : 10.10.0.1 | 192.168.10.1

**Anda perlu memperhatikan catatan Pendahuluan Konfigurasi di atas!!!**


---
### Step 1 - Installing NGINX
Untuk melakukan konfigurasi Reverse Proxy, kita bisa menggunakan NGINX
```bash
apt install nginx -y
```
### Step 2 - Konfigurasi File NGINX
Edit default file NGINX
```bash
nano /etc/nginx/sites-available/default
```
Lalu hapus semua konfigurasinya. Dan buat seperti ini.
![nginx_proxy](https://github.com/user-attachments/assets/a95d3e5b-dd5b-40da-9edf-30560c2b2b99)
Save File & Restart the Service.

**Penjelasan untuk masing - masing command di atas ada di bawah**

---
### Penjelasan!
- proxy_pass :
  
  **Deskripsi**: Mengarahkan semua permintaan yang masuk ke server backend yang didefinisikan dalam blok upstream.
  
  **Fungsi**: NGINX akan meneruskan (proxy) semua permintaan dari klien ke server yang terdaftar dalam grup backend_servers.

- proxy_set_header Host $host :
  
  **Deskripsi**: Mengatur header Host dengan nilai dari variabel $host.

  **Fungsi**: Mengirim header Host dari permintaan asli klien ke server backend. Ini penting untuk memastikan bahwa server backend menerima informasi tentang host yang diminta oleh klien.

- X-Real-IP $remote_addr :
  
  **Deskripsi**: Mengatur header X-Real-IP dengan alamat IP asli dari klien ($remote_addr).

  **Fungsi**: Memungkinkan server backend mengetahui alamat IP asli dari klien yang melakukan permintaan. Ini berguna untuk logging, analitik, atau keputusan terkait keamanan.

- proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for :

  **Deskripsi**: Menambahkan atau memperbarui header X-Forwarded-For dengan alamat IP klien.
  
  **Fungsi**: Menyediakan daftar alamat IP dari semua proxy yang dilalui oleh permintaan klien, dimulai dari IP klien asli. Ini memungkinkan server backend untuk melacak jalur yang diambil oleh permintaan melalui berbagai proxy.

- proxy_set_header X-Forwarded-Proto $scheme :

  **Deskripsi**: Mengatur header X-Forwarded-Proto dengan skema permintaan (HTTP atau HTTPS).

  **Fungsi**: Menginformasikan server backend apakah permintaan asli dari klien dilakukan melalui HTTP atau HTTPS. Ini berguna untuk pengaturan logika aplikasi atau redirect yang tergantung pada protokol yang digunakan oleh klien.

- upstream backend_servers : Ini adalah command untuk kita mendefinisikan backend web server kita, sehingga Proxy Server Server tau alamat web server kita.
- least_conn : Ini adalah protokol untuk melakukan Loud Balancing antara 2 Web Server ( optional )
- server : Untuk mendefinisikan alamat web server kita.
---
### PENGUJIAN
Pengujian dapat dilakukan di Client dengan cara mencoba mengakses websitenya, masukan IP/sub-domain dari Reverse Proxy Server kita pada kolom pencaharian di Browser. www.ikn.com atau 10.10.0.1
