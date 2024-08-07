## Active Directory
### Konfigurasi Active Directory Service melalui Ansible Playbook
Ini adalah konfigurasi Active Directory menggunakan playbook, seperti biasa tasks akan menjadi dalam 1 playbook tapi dipisah oleh step 1 dan selanjutnya

Konfigurasi meliputi:
- Installasi ADDS
- Promote Domain Controller
- Menambahkan OU
- Menambahkan AD User

### Step 1 - Installasi
```yml
tasks:
- name: Install Active Directory
  win_feature:
    name: AD-Domain-Service
    state: present
    include_management_tools: yes
    include_sub_features: yes
```
### Step 2 - Promoting Domain Controller
```yml
tasks:
- name: Install Active Directory
  win_feature:
    name: AD-Domain-Service
    state: present
    include_management_tools: yes
    include_sub_features: yes

- name: Promoting to Domain Controller
  win_domain:
    dns_domain_name: example.com
    safe_mode_password: password
  register: promotion

- name: Reboot System
  win_reboot:
  when: promotion.reboot_required
```
