## CONFIGURE ISCSI
### Konfigurasi ISCSI di WINSRV2
Pada tasks ini, kita disuruh melakukan konfigurasi ISCSI di Windows Server 2022, lalu kita disuruh menambahkan disk sebesar 10GB tetapi untuk virtual disk ISCSI menggunakan 10GB.

Selanjutnya kita disuruh melakukan konfigurasi ISCSI Target pada Virtual Disk tersebut, lalu beri nama BACKUP-TG, lalu kita disuruh melakukan konfigurasi agar ISCSI Target tersebut hanya bisa diaccess oleh WINSRV1 sebagai initator.

### Step 1 - Setup
Tambahkan Disk sebesar 10GB pada WINSRV2, lalu aktifkan pada **Create and format hard disk partitions**. Lalu tanda volume nya ganti menjadi G.
### Step 2 - ISCSI Configuration
Buka Server Manager >> Dashboard >> Pilih pada tampilan paling kiri ada menu **FIle and Storage Services** >> ISCSI >> New ISCSI Virtual Disk >> Select Volume "G" >> Name : BACKUP-TG >> Size : 5 GB | Fixed size | >> Next >> Pada Access Servers | Add : WINSRV1 >> Next >> Next.
### Step 3 - ISCSI Initiator WINSRV1
Buka Server Manager >> ISCSI Initiator >> Ketikan nama server/IP Address dari WINSRV2 :
![Initiator](https://github.com/user-attachments/assets/428e091c-80f0-4230-9c89-59fbacc41b2d)

Setelah itu setting pada **Create and format hard disk partitions**.
### DONE
