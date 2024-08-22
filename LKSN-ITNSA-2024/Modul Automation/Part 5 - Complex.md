## Part 5 - Complex
### Pendahuluan
Pada part ini kita akan disuruh untuk melakukan beberapa tugas yang complex seperti
-  Membuat Playbook untuk melakukan installasi web server apache2 lalu membuat virtual host dengan menggunakan username
-  Membuat Playbook untuk untuk menambahkan DNS Record yang ada pada list di textfile.

Karena ini terlalu komplex maka setiap playbook akan saya bagi.

### Part 1 - Apache2
Pada tasks awal kita disuruh untuk melakukan installasi Web Server Apache2 lalu disuruh untuk mengedit file default nya. Selanjutnya kita disuruh untuk membuat beberapa webpage untuk user user yang ada.
### Installasi and Configurasi File Default
```yml
- name: Install and Configure Web Server Apache2
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'



  tasks:
  - name: Install Apache2
    apt:
      name: apache2
      state: present

  - name: Configure File Default
    copy:
      content: "<html> <h1> Welcome {{ hostname }} </html> </h1>"
      dest: /var/www/html/index.html

  - name: Restart Service
    service:
      name: apache2
      state: restarted
```
