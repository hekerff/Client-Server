## Konfigurasi OpenVPN Site to Site
### Requirements before configuring Failover
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
- 2 Server Linux
Dalam konfigurasi kali akan membutuhkan setidaknya 2 Server, dan untuk versi OpenVPN nya adalah versi 3.
---
### Pendahuluan
Pada konfigurasi ini menggunakan topologi 2 server saja, Server 1 dan Server 2, Server 1 akan menjadi Server dari VPN dan Server 2 akan menjadi Clientnya.
### Step 1 - Installing OpenVPN & Easy-RSA
Yoilah yang pertama pasti kita perlu install package nya ye kan
```bash
apt install openvpn easy-rsa
```
### Step 2 - Configure Local Certificate Authority
Yap untuk Site to Site di OpenVPN versi terbaru ini, kita perlu menggunakan Certificate tidak seperti dulu lagi. Konfigurasi pada Server 1.
```bash
#Buat Directory untuk CA
mkdir ca
```
Lalu bikin Symbolic Link
```bash
ln -s /usr/share/easy-rsa/* ca
```
Lalu masuk ke Folder ca yang telah kita bikin dan lakukan beberapa konfigurasi seperti berikut
```bash
cd ca
```
Buat folder PKI
```bash
./easyrsa init-pki
```
Setelah itu kita bikin CA nya dengan command berikut:
```bash
./easyrsa build-ca nopass
```
Certificate Authority telah selesai dibuat, selanjutnya kita akan membuat Certificate untuk Server dan Client.
### Step 3 - Membuat Certificate untuk Server
Masih pada directory yang sama, gunakan command seperti berikut:
```bash
./easyrsa gen-req server nopass
```
Lalu kita langsung tanda tangani
```bash
./easyrsa sign-req server server
```
Setelah itu kita Generate DH
```bash
./easyrsa gen-dh
```
Setelah semua diatas, sekarang copy semua file yang telah tergenerate ke folder /etc/openvpn/server/
```bash
cp pki/ca.crt pki/dh.pem pki/issued/server.crt pki/private/server.key /etc/openvpn/server/
```
Sertifikat untuk server sudah selesai, selanjutnya kita akan membuat sertifikat untuk client
### Step 4 - Membuat sertifikat untuk Client
```bash
./easyrsa gen-req client nopass
```
Selanjutnya kita tanda tangani
```bash
./easyrsa sign-req client client
```
Setelah itu kita copy ke directory /etc/openvpn/client
```bash
cp pki/ca.crt pki/issued/server.crt pki/private/server.key /etc/openvpn/client/
```
Selesai, selanjutnya kita akan membuat private key antara server dan client, sekarang balik ke folder /etc/openvpn/
```bash
cd /etc/openvpn

openvpn --genkey --secret ta.key
```
DONE
### Step 5 - Membuat File Konfigurasi Untuk Server
```bash
nano server.conf
```
lalu isi seperti di bawah ini:
![serverconf](https://github.com/user-attachments/assets/da2d2800-01d9-4c41-91ac-4531b9093efb)

Untuk ke Step selanjutnya, kirim file yang ada pada file /etc/openvpn/client/ ke Server 2
```bash
scp /etc/openvpn/client/* debian@ip_server_2:/home/debian/
scp /etc/openvpn/ta.key debian@ip_server_2:/home/debian/
```
### Step 6 - Membuat File Konfigurasi Untuk Client
Sebelum itu kita harus memindahkan semua file yang sudah kita kirim dari server 1 ke server 2. kita akan taruh di /etc/openvpn/client/
dan untuk ta.key kita taruh di /etc/openvpn/.

Lakukan pada Server 2
```bash
mv /home/debian/* /etc/openvpn/client/
mv /etc/openvpn/client/ta.key /etc/openvpn/
```
Sekarang kita buat file konfigurasinya.
```bash
nano client.conf
---
client
dev tun
proto udp
remote ip_server_1 1195

ca /etc/openvpn/client/ca.crt
cert /etc/openvpn/client/client.crt
key /etc/openvpn/client/client.key
tls-auth ta.key 1

comp-lzo
persist-tun
persist-key
log /etc/openvpn/client.log
verb 3
```
Save File.
**DONE**
### Step 7 - Menjalankan VPN
Pada Server 1 jalankan Openvpn dengan Command berikut
```bash
systemctl start openvpn@server
```
Dan pada Server 2 jalankan Openvpn dengan Command berikut
```bash
systemctl start openvpn@client
```
### Testing
Bisa ditest dengan melakukan ping ke Network pada masing - masing Server, atau check dengan command ip a, dan melakukan ping antara Server 1 dan 2.
