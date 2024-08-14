## DNS Server
### Konfigurasi DNS Server di Windows Server 2022
Pada tugas ini, kita disuruh membuat Zone tengah.id dan Reverse Zone untuk ip network 172.31.16.0/24, lalu kita konfigurasi DNS Forward yang mengarah ke FW-WIB atau barat.id
### Step 1 - Create New Zone
DNS akan otomatis terinstall dan domain otomatis muncul juga setelah menginstall ADDS dan sekarang kita hanya perlu melakukan membuat Reverse Zone + Menambahkan Record dan konfigurasi DNS FORWARDER.

**CREATE REVERSE ZONE**
Buka DNS Manager >> Klik kanan pada Reverse Lookup Zones >> New Zone >> Primary Zone >> To All Server in this domain >> IPV4 >> 172.31.16 >> Next Until Finish.

**ADD RECORD**
Masuk pada directory Forward Zones >> tengah.id >> klik kanan - New Host >> lalu isi sesuai task.

**FORWARDER**
Masuk pada directory Conditional Forwarders lalu klik kanan >> New Conditional Forwarder >> DNS Domain: barat.id | IP Address: 32.12.10.110 >> OK

### Uji Coba
Coba untuk melakukan nslookup ke semua domain mulai dari tengah.id dan barat.id.
