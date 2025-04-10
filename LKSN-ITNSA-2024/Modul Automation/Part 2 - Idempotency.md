## Part 2 - Idempotency
### Pendahuluan
Pada tasks ini kita disuruh untuk membuat beberapa playbook diantaranya adalah merubah /etc/hosts record di semua hosts, disuruh menambahkan dua baris sesuai appendix.
### Number 1
```yml
- name: Adding Appendix in hosts file
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/home/user/ansible/.lin_cred'

  tasks:
  - name: Tambahkan baris lksn ke /etc/hosts (1)
    lineinfile:
      path: /etc/hosts
      line: "10.17.10.17 lksn2024.local"
      state: present

  - name: Tambahkan baris lksn ke /etc/hosts (2)
    lineinfile:
      path: /etc/hosts
      line: "10.19.45.19 pic.lksn2024.local"
      state: present
```


