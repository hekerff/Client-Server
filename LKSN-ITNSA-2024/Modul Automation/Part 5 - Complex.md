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
- name: Configure Web Server
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/home/user/ansible/.lin_cred'

  tasks:
  - name: Install apache2
    apt:
      name: apache2
      state: present

  - name: edit default html file
    copy:
      dest: /var/www/html/index.html
      content: "Welcome to {{ hostname }}"

  - name: restart apache2
    service:
      name: apache2
      state: restarted
```
### Number 2
```yml
- name: Configure DNS Record
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/home/user/ansible/.lin_cred'

  tasks:
  - name: Tambah record kalau dnsmasq terpasang
    block:
      - name: Baca file dnslist.txt
        slurp:
          src: /root/dnslist.txt
        register: dnslist_raw
        delegate_to: localhost

      - name: Tulis ke /etc/dnsmasq.d/custom.conf
        copy:
          dest: /etc/dnsmasq.d/custom.conf
          content: |
            {% for line in dnslist_raw.content | b64decode | split('\n') %}
            {% if line %}
            address=/{{ line.split()[0] }}/{{ line.split()[-1] }}
            {% endif %}
            {% endfor %}
        notify: restart dnsmasq
    when: ansible_facts.packages['dnsmasq'] is defined

  handlers:
  - name: restart dnsmasq
    service:
      name: dnsmasq
      state: restarted
```
