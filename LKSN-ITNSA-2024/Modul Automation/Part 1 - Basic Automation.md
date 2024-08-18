## Part 1 - Basic Automation
### Pendahuluan
Pada part ini kita disuruh melakukan beberapa tasks diantaranya:
- Membuat basic inventory di /etc/ansible/all-linux berisikan semua linux-host
- Membuat inventory role pada file /etc/ansible/site-1 dengan setup: Sinabung as DNS, Rinjani & Serua as Web.
- Membuat inventory role pada file /etc/ansible/site-2 dengan setup: Rinjani as dns, sinabung as web.
- membuat playbook dengan nama hostname-all.yml untuk merubah hostname di semua linux host.
- Membuat playbook dengan nama dns-install.yml untuk menginstall DNS Service pada semua linux hosts
- Membuat playbook dengan nama dns-config untuk melakukan konfigurasi DNS Service pada semua linux host, disuruh hanya untuk mendengarkan ke IP address yang mereka punya tapi tidak ke 0.0.0.0

### Membuat basic inventory all-linux
```yml
linux:
      hosts:
            sarua:
              ansible_host: 192.168.0.11
              hostname: sarua
            sinabung:
              ansible_host: 192.168.0.12
              hostname: sinabung
            rinjani:
              ansible_host: 192.168.0.13
              hostname: rinjani
```
### Membuat inventory site-1
```yml
all:
    children:
        dns:
          hosts:
              sinabung:
                  ansible_host: 192.168.0.12
        web:
          hosts:
              serua:
                  ansible_host: 192.168.0.11
              rinjani:
                  ansible_host: 192.168.0.13
```

### Membuat inventory site-2
```yml
all:
    children:
        dns:
          hosts:
              rinjani:
                  ansible_host: 192.168.0.13
        web:
          hosts:
              sinabung:
                  ansible_host: 192.168.0.12
```
### Membuat Playbook hostname-all.yml
```yml
- name: Change all linux hostname
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Change hostname
    hostname:
        name: "{{ hostname }}"
```
### Membuat Playbook dns-install.yml
```yml
- name: Installing DNS Service
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Uninstalling dependencies
    apt:
      name: bind9-libs
      state: absent

  - name: Installing Bind9
    apt:
      name: bind9
      state: present
```
### Membuat playbook dns-config.yml
```yml
- name: Configure Listen On in DNS Service
  hosts: linux
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:

  - name: Inserting line in file configuration
    lineinfile:
      path: /etc/bind/named.conf.options
      line: "\tlisten-on { {{ ansible_host }}; };"
      insertafter: "listen-on-v6"

  - name: Restart Service
    service:
      name: bind9
      state: restarted
```
Untuk melihat apakah konfigurasi sudah berjalan dengan benar, ketikan command berikut:
```bash
netstat -tulnp | grep :53
```
**DONE**
