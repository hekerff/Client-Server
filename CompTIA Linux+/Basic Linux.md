## Basic Linux
### Bash Shell
Shell merupakan program untuk kita para manusia berinteraksi dengan hardware ataupun operating sistem. Shell akan menerjemahkan setiap perintah yang kita masukan lalu akan mengirimnya ke kernel melalui sistem operasi, lalu kernel akan mengeksekusi command tersebut sehingga membuat sebuah output yang nantinya akan dibawa balik oleh shell kepada manusia. 

Shell memiliki banyak jenis, salah satunya adalah Bash.
**Komponen**:
Terdapat 3 point utama dalam shell:
- Command
- Options
- Argument
Shell Bash itu case sensitive yang artinya huruf besar dan hurus kecil sangat berpengaruh.
Contoh Command Bash:
- echo
- ls
- pwd
- cd = For Changing Directory
- cp = For Copying File
- mkdir = For Creating New Directory
- clear = For Clearing CLI on the screen
- cat = for view content of file
- less = lebih bagus dari cat karena bisa discroll kalo file nya panjang
- shutdown -h now
- sudo su = For entering sudoers or root user

**Text Editor:**
- vi(m)
- nano
- gedit

Enaknya bash shell adalah history dari command yang sudah kita lakukan masih tersimpan. Dan bisa auto complete command dengan menggunakan TAB.

### Man Pages
**Man pages** (manual pages) adalah dokumentasi bawaan di sistem operasi berbasis Unix, termasuk Debian Linux, yang menyediakan informasi detail tentang perintah, program, fungsi library, file konfigurasi, dan berbagai aspek sistem lainnya. Man pages adalah sumber referensi penting untuk memahami penggunaan perintah dan fitur tertentu dalam sistem Linux.

Untuk mengakses **man** pages, Anda dapat menggunakan perintah **man** di terminal diikuti dengan nama perintah atau program yang ingin Anda pelajari.

Contoh:
```bash
man ls
```
Selain itu kita bisa melihat dokumentasi bawaan di folder /usr/share/doc, dan untuk yang offline bisa di website https://tldp.org

Jadi pada intinya, man pages lebih berguna dari source source yang lain, kalian bisa menggunakan --help tetapi itu sangat kurang jika terdapat banyak opsi dari command yang ingin kita cari dokumentasinya.
