##How to configure Windows Backup Once
---
### Requirements before starting the configuration
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Active Directory terkonfigurasi
- Setidaknya terdapat 2 Windows Server dan keduanya berada dalam 1 Domain yang sama
- Siapkan Folder yang akan menjadi tempat backup, pastikan sudah dibuat menjadi Public/Share Anonymously.
- Siapkan Folder yang akan dibackup dan pastikan sudah dibuat menjadi Public/Share Anonymously.
---
### Step 1 - Install Windows Backup
Install Windows Backup pada Server Utama / Server yang datanya akan dibackup.

Buka "Server Manager" ==> Add Roles and Features ==> Lalu "Next" sampai menu **Features**.
Centang pada **Windows Server Backup**
![Ins](https://github.com/hekerff/Client-Server/assets/159868331/943813bc-1b77-4653-830b-c5726c446f2f)
Lalu "Next" sampai ke Mars🐨💀.

### Step 2 - Configure Windows Backup
- Buka **Tools** lalu pilih **Windows Server Backup**
- Klik kiri/kanan pada bagian **Local Backup**, lalu pilih **Backup Once**
![dor-dor-dor](https://github.com/hekerff/Client-Server/assets/159868331/ffed9776-d624-46de-9952-ba93f4085343)
- Pilih "Next" sampai bagian berikut dan pilih **Custom**
![revisukidesu](https://github.com/hekerff/Client-Server/assets/159868331/d85ff1b9-f1bb-4d2c-98ce-5f0343c25b5a)
- Selanjutnya Klik **Add Items** untuk menambahkan Folder/File yang ingin kita backup.
- Selanjutnya pilih **Remote Shared Folder**
- Lalu pada Location:\\Nama Komputer Target Backup\Nama Folder yang sudah di konfigurasi menjadi Shared,
  Contoh: \\\REPLI\Backup
  ![china-baik](https://github.com/hekerff/Client-Server/assets/159868331/a0216a08-f488-48ad-a716-d583d2dfcb86)
- "Next" --> "Backup"
**DONE**
### Pengujian
Pengujian dapat dilakukan dengan cara menghapus file yang ada dalam Folder yang sudah dibackup lalu **direcover**

![Recover](https://github.com/hekerff/Client-Server/assets/159868331/2cee6140-da22-4272-9137-643e2d29c702)
