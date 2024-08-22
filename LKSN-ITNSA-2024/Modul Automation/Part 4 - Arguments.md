## Part 4 - Arguments
### Pendahuluan
Pada part 4 ini kita disuruh untuk melakukan 2 tugas saja yaitu:
1. Membuat Playbook untuk menambahkan user natuna di semua linux hosts dengan password Skills39
2. Membuat Playbook untuk melakukan installasi beberapa package, dan list package tersebut sudah disediakan dalam bentuk file .txt | jadi kita disuruh untuk membuat playbook, dan dalam playbook tersebut kita membuat tasks installasi, dan package yang ingin diinstall tersebut berada dalam sebuah text file.

### Number 1
```yml
- name: Add User in All Linux Host
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Adding User Natuna
    user:
      name: natuna
      comment: natuna
      password: "{{ 'Skills39' | password_hash('sha512')}}"
      shell: /bin/bash
      state: present
```
### Number 2
```yml
tasks:
- name: Baca txt file
  set_fact:
     package: "{{ lookup('file', '/etc/ansible/packages.txt').splitlines() }}"

- name: Install Packages
  apt:
   name: "{{ item }}"
   state: present
  loop: "{{ package }}"
```
