## Configure Certificate Authority Using OpenSSL
### Requirements before configuring Static DHCP Lease
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
---
### Pendahuluan
Yaaa begitulah, Certificate Authority pake OpenSSL, kalo kemarin Easy-RSA. hampir sama tapi keknya agak susah idk menurut kalian aja.
### Step 1 - Preparing Installation and Directory
Yap kita perlu install OpenSSL
```bash
apt install openssl
```
Trus kita siapin Directory untuk menaruh Certificate nya
```bash
mkdir /root/ca
```
Gua bikin di dalam root Directory yak.

### Step 2 - Create Root Certificate
Selanjutnya kita akan bikin **Root Certificate** <=== Inilah yang nanti akan menandatangani semua file .csr yang ada.
```bash
openssl req -x509 -new -nodes -out root.crt -keyout root.key
```
- Country Name: ID --> Indonesia
- Province Name: Bali --> Provinsi
- Locality Name: Singaraja --> Kota
Untuk Selanjutnya isi sendiri bebas. Setelah selesai akan muncul 2 File yaitu **root.crt dan root.key**

**Sudah Selesai :)**, tapi akan saya lanjutkan sampai membuat dan menandatangani sebuah Certificate yang akan digunakan pada Server nanti.

### Step 3 - Create and Sign a Certificate
Yang pertama kita perlu membuat file .csr terlebih dahulu yang nanti akan ditandatangani oleh Root Certificatenya. Contoh saya akan buat untuk layanan web.
```bash
openssl req -new -nodes -days 365 -out www.csr -keyout www.key
```
Sebelum menandatangani certificatenya, jika file .csr tersebut berada diluar server CA maka perlu dikirim ke Server CA terlebih dahulu menggunakan scp.

Jika sudah langsung saja kita tandatangani.
```bash
openssl x509 -req -CA root.crt -CAkey root.key -set_serial 01 -in www.csr -out www.crt
```
Setelah selesai, maka file yang tadinya berupa .csr sekarang menjadi **www.crt**

### Selesai
Sudah selesai dan Certificate sudah siap digunakan.
