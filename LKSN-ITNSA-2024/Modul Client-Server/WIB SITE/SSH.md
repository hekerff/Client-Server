## SSH
### Konfigurasi SSH Server di LINSRV2
Ini adalah pembahasan pada task SSH untuk soal pre-test lksn 2024
### Install SSH Server
```bash
apt install openssh-server
```
### Create User
Buat user **file** dengan password **Skills39s** dan atur home directory nya ke /data/file/
```bash
useradd -m -d /data/file/ -s /bin/bash file
```
Lalu atur passwordnya
```bash
passwd file
```
### Change SSH port default to 2024
Edit pada file /etc/ssh/sshd_config, setelah itu buka pagar pada port dan ganti ke 2024.
