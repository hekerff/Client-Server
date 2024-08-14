## Web Server
### Konfigurasi Web Server di Windows Server 2022
Ini adalah pembahasan untuk task Web Server, yang mana kita perlu melakukan konfigurasi IIS di WINSRV1 dan Reverse Proxy pada FW-WITA.
### Step 1 - Installasi IIS
Install IIS di Windows Server lalu tambahkan sub feature berupa basic authentication.
### Step 2 - Konfigurasi Website untuk www.tengah.id

Buka Server Manager >> Tools >> IIS >> Sites >> Default Web Site >> Bindings >> Host name : www.tengah.id >> OK.

**EDIT FILE HTML**
Sekarang tinggal buat file index.html di folder C:\inetpub\wwwroot\index.html | Hapus file default nya jangan lupa.

### Step 3 - Konfigurasi Website untuk manager.tengah.id
Buka IIS Manager >> pada Sites klik kanan >> add Website >> 
- Site name : Manager
- Physical path: C:\inetpub\manager\
- Host name: manager.tengah.id
Oke Save.

**BASIC AUTHENTICATION**
Pilih Site yang baru kita pilih >> Authentication >> Anonymous : disable | Basic Auth : enable

**Mengatur Group Manager**
Klik kanan pada website manager >> Edit Permissions >> Security >> Edit >> Add : Manager.

### Step 4 - Buat Directory Manager
Buat directory di dalam folder C:\inetpub\ buat folder manager lalu buat file HTML nya.

## Reverse Proxy
### Konfigurasi Reverse Proxy di FW-WTIA
