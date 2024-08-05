## Inventory
### Apa itu Inventory di Ansible?
Ketika kita melakukan otomasi menggunakan **Ansible** pada server yang kita kelola, tentu kita menggunakan Ansible karena Server yang kita kelola lebih dari satu, untuk menyimpan Server atau host/node yang kita sebut di Ansible, kita memerlukan yang namanya Inventory, jadi Inventory ini berfungsi untuk menyimpan informasi dari node node yang kita kontrol dengan Ansible.
### Format penggunaan
Inventory dalam Ansible bisa dibilang terbagi menjadi 2 format file, yang pertama bisa menggunakan format YML dan INI. Inventory Ansible bisa menggunakan format lainnya tapi yang paling sering digunakan adalah YML dan INI.
### Letak dari Inventory
Biasanya Inventory ini terletak di /etc/ansible/hosts (Yap sistem ansible sendiri akan membaca secara default pada Directory dan File tersebut).
### PERINGATAN
Pengetahuan saya baru cuman sampai situ untuk Inventory di Ansible, saran saya agar membaca lebih banyak di sumber yang lain.
