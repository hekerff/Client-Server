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

