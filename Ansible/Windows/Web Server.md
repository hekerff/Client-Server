## Configure Web Server
### Configure Web Server on Windows Server 2022 using Ansible Playbook
Membuat Playbook untuk konfigurasi Web Server di Windows Server 2022 mulai dari Installasi, membuat Pool baru, membuat HTML file, sampai membuat Web Site baru.

Seperti biasa, masing - masing task akan dipisah ke dalam Step yang berbeda tapi tetap dalam 1 Playbook yang sama.

### Step 1 - Installasi
Untuk melakukan installasi service pada Windows Server kita menggunakan Modul win_feature
```yml
tasks:
- name: Installasi
  win_feature:
    name: Web-Server
    state: present
    include_management_tools: yes
```
### Step 2 - Adding New App Pool
```yml
- name: Adding New App Pool
  win_iis_webapppool:
    name: Web Pool
    state: present
```
### Step 3 - Making Directory and HTML File
Sekarang kita buat directory untuk menaruh File HTML nya, lalu kita buat file HTML.
```yml
- name: Make Directory
  win_file:
    path: C:\inetpub\wwwroot\Website
    state: directory

- name: Create HTML File
  win_copy:
    content: "<html><body><h1> HELLO WORLD </h1></body></html>"
    dest: C:\inetpub\wwwroot\Website\index.html
```
### Step 5 - Create New Website
Sekarang membuat Website baru
```yml
- name: Create New Website
  win_iis_website:
    name: Web Site
    hostname: www.example.com
    application_pool: Web Pool
    physical_path: C:\inetpub\wwwroot\Website
    port: 80
    ip: 192.168.1.1
    state: started
```

### DONE
  
