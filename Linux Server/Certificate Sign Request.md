## Certificate Sign Request
### Cara membuat Certificate Request/.csr
Certificate Request/.csr adalah Certificate yang belum ditanda tangani oleh Certificate Authority sehingga ketika kita menjalankan Web Service tanpa ini, maka Web kita akan dianggap **unsecure** oleh Client yang mengakses Web tersebut.
### Step 1 - Install Openssl
```bash
apt install openssl
```
### Step 2 - Req for certificate
```bash
openssl req -new -nodes -out example.csr -newkey rsa:2048 -keyout example.key
```
Nanti akan diminta informasi seperti ini... isi yang diperlukan saja
![certi](https://github.com/hekerff/Client-Server/assets/159868331/16a11f09-45ca-4bf3-89b4-3906b161738c)
- Nanti akan muncul 2 file: example.csr & example.key.
- Kedua file tersebut akan muncul di folder di mana kita sedang berada.
- example.csr, hanya file ini saja yang akan dikirim ke CA untuk ditanda tangani.
- gunakan scp untuk mengirim file tersebut ke CA
```bash
scp example.csr YourCA@192.xxx.xxx.xxx:/YourFolder/
```
