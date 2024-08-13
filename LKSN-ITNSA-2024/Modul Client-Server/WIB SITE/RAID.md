### RAID
### Melakukan konfigurasi RAID 1 pada LINSRV2
### Step 1 - Install MDADM
```bash
apt install mdadm -y
```
### Step 2 - Partisi 2 disk
```bash
fdisk /dev/sdb
n
p
1
enter
enter
t
fd
w
```
lakukan pada /dev/sdc juga.
### Step 3 - Configure RAID 1
```bash
mdadm -C /dev/md0 --verbose --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```
Setelah itu lakukan seperti ini:
```bash
mkfs.ext4 /dev/md0
```
### Step 4 - Mounting RAID to Directory /data
Yang pertama, bikin directory /data. lalu mounting dengan cara berikut
```bash
mount /dev/md0 /data
```
setelah dimounting, edit pada file /etc/fstab agar mounting nya permanent. lalu tambahkan pada line paling bawah. seperti ini:
![nftab](https://github.com/user-attachments/assets/a8615e7a-4bec-4478-b6a2-364712afac66)

Setelah nya update mdadm
```bash
update-initramfs -u
```
### DONE
