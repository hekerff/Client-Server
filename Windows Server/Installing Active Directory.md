## Installing Active Directory / ADDS in Windows Server 2022
![windows server](https://github.com/hekerff/ITNSA-2024/assets/159868331/1ab9f344-2909-4a03-bf73-99562f2a102b)
### Requirements before starting the installation
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
### Step 1 - Buka "Server Manager"
Biasanya automatis terbuka ketika server baru dihidupkan
### Step 2 - Add Roles and Features
Pada menu dashboard click pada tulisan "Add Roles and Features". Click next sampai pada bagian "Server Roles"
![Screenshot 2024-06-25 131057](https://github.com/hekerff/ITNSA-2024/assets/159868331/f67b0400-d361-4d0c-971c-442416123d36)
### Step 3 - Choose the roles
Centang pada pilihan "Active Directory Domain Services" ==> Click Add Feature ==> Next ==> Next ==> Install.
![Screenshot 2024-06-25 131922](https://github.com/hekerff/ITNSA-2024/assets/159868331/a46ff9ab-e31b-4150-bc6f-5c4c23420747)
Tunggu sampai installasi selesai
### Step 4 - Promote Server
Setelah installasi selesai, sekarang promote server menjadi domain controller. Click pada tulisan biru "Promote this server to a domain controller"
![dkjkfaj17](https://github.com/hekerff/ITNSA-2024/assets/159868331/e533cad8-01a1-49bc-9d33-09bc08a06f41)
### Step 5 - New Forest
Pada tahap ini, pilih "New Forest". dan tambahkan nama root domain (sesuaikan)
![fore](https://github.com/hekerff/ITNSA-2024/assets/159868331/8f912cf7-1f2d-41fd-b1c2-7daeec4635a3)
"Next"
Pada menu "domain controller option" masukan password untuk recovery nanti.

"Next" sampai bagian NetBios. Masukan nama netbios nya ( bebas ) lalu **Next** sampai selesai dan **Install** dan tunggu sampai selesai.

**Nanti Windows Server akan otomatis reboot setelah installasi selesai.**
Lalu coba login dengan Administrator.

Sekarang lihat apakah sudah berhasil dengan cara masuk ke Command Prompt dan ketik sconfig "enter"
![Uji coba](https://github.com/hekerff/ITNSA-2024/assets/159868331/ef5e00ec-ddba-4c19-a7df-82bcef8e12b3)

Jika konfigurasi benar, maka pada bagian domain akan berubah sesuai konfigurasi.


*Note: Setelah installasi dan konfigurasi selesai maka DNS Server akan otomatis terinstall dan terkonfigurasi dengan Zone yang sama dengan Active Directory.


Referensi:
- [Active Directory Windows Server 2022](https://www.easeus.com/todo-backup-guide/how-to-install-active-directory-on-windows-server-2022.html)
