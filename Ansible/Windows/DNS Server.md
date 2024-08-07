## Configure DNS Server
### Configure DNS Server on Windows Server 2022 using Ansible.
Saya mencoba untuk membuat playbook yang berisikan tasks untuk melakukan konfigurasi DNS Server mulai dari Installasi, menambahkan Zone, dan menambahkan record.

**PERHATIAN!!!**

Perlu diperhatikan bahwa semua tasks tersebut berada dalam 1 Playbook. Untuk masing - masing task saya bagi ke dalam Step.

### Step 1 - Installing DNS Server on Windows Server 2022
```yml
 tasks:
  - name: Installing DNS
    win_feature:
        name: DNS
        state: present
        include_management_tools: yes
```

'win_feature' adalah module untuk melakukan installasi service pada windows

### Step 2 - Configuring Zone & Add Record
```yml
  - name: Installing DNS
    win_feature:
        name: DNS
        state: present
        include_management_tools: yes

  - name: Configure Zone
    win_domain:
        dns_domain_name: example.com
        safe_mode_password: Password

  - name: Create DNS Record
    win_dns_record:
        name: www
        zone: example.com
        type: A
        value: 192.168.1.1
```
### DONE
