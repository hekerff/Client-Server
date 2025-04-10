## Part 4 - Arguments
### Pendahuluan
Pada part 4 ini kita disuruh untuk melakukan 2 tugas saja yaitu:
1. Membuat Playbook untuk menambahkan user natuna di semua linux hosts dengan password Skills39
2. Membuat Playbook untuk melakukan installasi beberapa package, dan list package tersebut sudah disediakan dalam bentuk file .txt | jadi kita disuruh untuk membuat playbook, dan dalam playbook tersebut kita membuat tasks installasi, dan package yang ingin diinstall tersebut berada dalam sebuah text file.

### Number 1
```yml
- name: bla bla ble blublu
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/home/user/ansible/.lin_cred'

  tasks:
  - name: Baca file username dan password
    slurp:
      src: /root/usernames.txt
    register: user_file_raw
    delegate_to: localhost

  - name: Decode isi file usernames.txt
    set_fact:
      user_lines: "{{ user_file_raw.content | b64decode | split('\n') }}"

  - name: Ambil user dan password, buang header + trim
    set_fact:
      user_list: >-
        {{ user_lines[1:] | map('split', ',') | map('map', 'trim') | list }}

  - name: Filter hanya baris yang valid
    set_fact:
      user_list: "{{ user_list | selectattr(1, 'defined') | list }}"

  - name: Buat user dan set password
    user:
      name: "{{ item.0 }}"
      password: "{{ item.1 | password_hash('sha512', 'salt123') }}"
      state: present
    loop: "{{ user_list }}"
```
### Number 2
```yml
- name: Install packages from text list
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/home/user/ansible/.lin_cred'

  tasks:

  - name: Baca isi /root/packages.txt
    slurp:
      src: /root/packages.txt
    register: packages_raw
    delegate_to: localhost

  - name: Ubah isi file jadi list
    set_fact:
      packages_list: "{{ packages_raw.content | b64decode | split('\n') | reject('equalto', '') | list }}"

  - name: Install semua package dari file
    apt:
      name: "{{ packages_list }}"
      state: present
```
