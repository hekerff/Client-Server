## Inventory - INI
### Membuat Inventory dengan format file INI.
Sekarang kita akan mencoba membuat sebuah Inventory sederhana di Ansible menggunakan format file INI.
```ini
[linux]
server1 ansible_host=192.168.1.1 hostname=server1
server2 ansible_host=192.168.1.2 hostname=server2
[dns]
server1
[web]
server1 webcolor=blue webport=8080
server2 webcolor=green webport=9090
[windows]
WIN1 ansible_host=192.168.1.100 hostname=WIN1
WIN2 ansible_host=192.168.1.200 hostname=WIN2
```
Itu adalah contoh sederhana dari Inventory dengan format file INI. **Sekarang mari kita breakdown**

- **[linux]** : Ini merupakan Group dengan nama Linux, lalu dibawah nya ada server1 & server2, server1 & server2 adalah member dari group linux, lalu **ansible_host** adalah untuk memberi tahu IP dari member/host/node tersebut dan **hostname** adalah variabel custom.
- **[web]**
di dalam group web juga ada server1 dan server2, ini diambil dari group linux, lalu disamping nya ada **webcolor dan webport** ini adalah variabel custom yang nanti akan ditarik/digunakan oleh ansible dan si host.
- **[windows]**
Lalu ada group windows, ini sama saja seperti group linux tapi dengan host windows.
