## VPN
### Konfigurasi Site to Site dan Remote Access
### Pendahuluan
Pembahasan VPN ini akan sangat panjang, maka saya akan bagi menjadi 2 yaitu, Site to Site and Remote Access.

Karena OpenVPN sekarang memerlukan Certificate, maka kita perlu menyiapkan root ca dan juga Certificate yang sudah dibuat pada Pembahasan Certificate Authority.

## Site to Site
### Konfigurasi Site to Site menggunakan OpenVPN.
Konfigurasi ini akan dilakukan pada FW-WIB dan FW-WITA, FW-WIB akan selalu menjadi Server dalam konfigurasi VPN.
### Step 1 - Setup
Kita akan melakukan Setup, seperti menyiapkan service dan file yang dibutuhkan.
Pada kedua server:
```bash
apt install openvpn tmux -y
```
Setelah melakukan Installasi, kirim file file yang diperlukan seperti cacert.pem, Certificate dan Key pada masing - masing pemilik Certificate.

**Generate Diffie Hellman (dh)** menggunakan openssl
```bash
openssl dhparam -out /etc/openvpn/server/dh.pem 1024
```
**Generate TLS Key**
```bash
openvpn --genkey --secret ta.key
```
### Step 2 - Konfigurasi Server
Buat file **server.conf**, lalu buat seperti ini:
![server-conf](https://github.com/user-attachments/assets/51e4aab1-afe5-4bf7-91c4-eb26d57c603c)

Taruh semua file yang diperlukan server di dalam directory /etc/openvpn/server/

### Step 3 - Konfigurasi Client
Sebelum itu, kirim file dh.pem yang sudah digenerate di FW-WIB ke FW-WITA. Setelah itu buat file konfigurasi untuk client di FW-WITA dengan nama client.conf. Lalu buat seperti ini:
![site-client](https://github.com/user-attachments/assets/963e7fcd-c895-444a-99c6-331a9f66d8b9)

Jikalau di Server tls-auth ta.key 0, maka di client harus tls-auth ta.key 1.
### Nyalakan VPN
Sekarang kita nyalakan VPN di keduanya.

**FW-WIB**:
```bash
systemctl start openvpn@server
```
**FW-WITA**:
```bash
systemctl start openvpn@client
```
### DONE
## Remote Access VPN
### Konfigurasi Remote Access OpenVPN
Kita akan melakukan konfigurasi Openvpn Remote Access di FW-WIB dan BUDI-CLT.
### Step 1 - Setup
Lakukan Installasi openvpn dan tmux pada BUDI-CLT. Lalu kirim file yang dibutuhkan oleh BUDI-CLT (sama seperti FW-WITA).
### Step 2 - Konfigurasi Server
Copy saja file server.conf lalu rubah namanya menjadi remote.conf, setelah itu lakukan perubahan seperti di bawah:
![Remote-server](https://github.com/user-attachments/assets/6f1f49f9-6bed-48a0-bd8a-7d98f3db4fcf)

Plugin tersebut berfungsi untuk mengaktifkan Authentikasi.

Lalu buat user authentikasi menggunakan htpasswd:
```bash
htpasswd -c /etc/openvpn/budi budi
Skills39
```
### Step 3 - Konfigurasi Client
Buat file baru bernama client.ovpn lalu buat seperti di bawah:
![Client-Remote](https://github.com/user-attachments/assets/9e464a8c-0908-4abe-a21b-7b01b1f46587)

### Step 4 - Mulai Service
Nyalakan Service Openvpn di FW-WIB dan BUDI-CLT

**FW-WIB**:
```bash
systemctl start openvpn@remote
```
**BUDI-CLT**:
```bash
openvpn --config client.ovpn
```

### DONE
