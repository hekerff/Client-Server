## Configure Web Server with Basic Authentication
### Requirements before Configuring Web Server + Basic Auth
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Siapkan File HTML
- Active Directory sudah terkonfigurasi
---
### Step 1 - Install Service & Feature
Buka "Server Manager", lalu cari **Web Server (IIS)** dan pada bagian **Security** Checklist pada bagian **Basic Authentication**
![Installsss](https://github.com/hekerff/Client-Server/assets/159868331/6b6db3d9-98f4-4cbd-8c8e-a20d103095bc)
**Next And Install**
### Step 2 - Add new site
Pada Server Manager buka "Tools" lalu cari **(IIS)**,
Pergi ke bagian **Site** lalu hapus default website dan pilih **Add New Site**
![addweb1](https://github.com/hekerff/Client-Server/assets/159868331/abf8ee63-2cae-4e9e-a5e2-094240336206)

Setelah itu tambahkan seperti dibawah ini (sesuaikan)
![addwb2](https://github.com/hekerff/Client-Server/assets/159868331/1f0098c2-f43e-405f-af94-28bc06698061)
  1. Masukan nama Site kalian (bebas)
  2. Cari folder yang berisikan file HTML yang sudah disiapkan
  3. Tuliskan fqdn dari Web Server 
### Step 3 - Enable Basic Auth
Pergi ke Menu **Server/Halaman Utama** dan buka **Authentication**
![enable](https://github.com/hekerff/Client-Server/assets/159868331/f4f95e43-1344-4e16-bf7c-0a04dbd234de)
- **Disable pada Anonymous Authentication**
- **Enable pada Basic Authentication**
![enable2](https://github.com/hekerff/Client-Server/assets/159868331/41775f0c-8d56-4469-9d0b-66e6c0452b75)
**RESTART WEB SERVER**

### Test Login
Pergi ke Browser di Client lalu ketikan IP Address/fqdn dari Web Server... Jika ada box login, coba untuk login menggunakan User & Pass yang terdaftar di Active Directory.

![Logimg](https://github.com/hekerff/Client-Server/assets/159868331/afe342a5-f749-41ad-8ae9-26804727d971)
