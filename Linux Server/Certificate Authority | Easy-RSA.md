## How to Create Certificate Authority Using Easy-RSA
### Requirements before creating Certificate Authority
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Pastikan sudah memakai user **root**
---
### Step 1 - Install easy-rsa
- Hal yang pertama adalah melakukan installasi package - package yang dibutuhkan
```bash
apt install easy-rsa -y
```
### Step 2 - Buat directory khusus untuk file Certificate Authority
```bash
mkdir my-ca
```
### Step 3 - Buat link symbolic antara folder easy-rsa dengan CA
```bash
ln -s /usr/share/easy-rsa/* my-ca/
```
### Step 4 - Buat folder PKI
```bash
cd my-ca/
./easyrsa init-pki
```
### Step 5 - Edit file vars
```bash
cd pki
nano vars
#Uncomment + edit pada barisan barisan berikut
#Sesuaikan dengan konfigurasi kalian
set_var EASYRSA_REQ_COUNTRY     "AU"
set_var EASYRSA_REQ_PROVINCE    "NSW"
set_var EASYRSA_REQ_CITY        "Sydbey"
set_var EASYRSA_REQ_ORG         "Requillion Solutions"
set_var EASYRSA_REQ_EMAIL       "info@requillion-solutions.com"
set_var EASYRSA_REQ_OU          "Business"
#Yang di bawah ini wajib diikuti
set_var EASYRSA_ALGO           "ec"
set_var EASYRSA_DIGEST         "sha512"
ctrl + x, Y, ENTER. untuk save file
```
### Step 6 - Bikin CA
```bash
cd ..
./easyrsa build-ca
```
![Screenshot 2024-06-26 095138](https://github.com/hekerff/Client-Server/assets/159868331/68dea171-9484-476d-acef-0b01634cc0b5)

- Ketika disuruh memasukan Password/Key Passphrase, saran saya masukan Password yang sama agar tidak bingung
---
Ketika disuruh memasukan common name, gunakan common name yang sedikit lebih bagus/mudah diingat
![loveurev0108](https://github.com/hekerff/Client-Server/assets/159868331/e4a38532-6061-4c05-b246-8f7b5d44d0b3)

**DONE**
### Preview
CA sudah berhasil dibuat, untuk file ca.crt disimpan di dalam folder /pki. ca.crt sangat penting karena file inilah yang nanti akan dipasangkan di Client.

Fungsinya adalah agar server lain yang certificatenya ditanda tangani oleh CA, service - servicenya dapat ditrust oleh Client.

---
### Tambahan
Beberapa command tambahan untuk Importing dan Signing
### Importing .csr file / Certificate Signing Request
```bash
./easyrsa import-req /YourFolder/NamaFile.csr NamaFile
```
### Signing the Certificate Signing Request
```bash
./easyrsa sign-req server NamaFile
```
Nanti akan diperlihatkan informasi dari file .csr | Pastikan informasi tersebut telah benar dan ketik "yes" untuk melanjutkan
![confirm](https://github.com/hekerff/Client-Server/assets/159868331/0b71a4f6-c736-4691-814d-c64cc4bbe61a)
### DONE
- Setelah selesai, file yang sudah ditanda tangani akan berubah dari .csr menjadi .crt
- File tersebut disimpan dalam folder /pki/issued/.
- Kirim file tersebut ke server yang membutuhkan.

**Referensi**
- [Creating a Certificate Authority](https://medium.com/@martin.hodges/creating-a-ca-with-easyrsa-on-debian-12-59aa6936fea2)
