## Part 6 - Windows
### Pendahuluan
Pada part ini kita disuruh untuk melakukan beberapa tugas diantaranya:
1. Membuat playbook untuk melakukan installasi IIS (Web Server) pada Windows Server.
2. Membuat playbook untuk melakukan installasi DNS pada Windows lalu membuat beberapa record, untuk recordnya:
  awu.lks2024.id to 10.17.8.45

### Number 1
```yml
- name: Installing IIS ( Web Server )
  hosts: windows
  gather_facts: false
  vars_files:
  - '/etc/ansible/.win_cred'

  tasks:
  - name: Installing IIS in Windows Server
    win_feature:
        name: Web-Server
        state: present
        include_management_tools: yes
```

### Number 2
```yml
- name: Installing and Configure DNS in Windows Server 2022
  hosts: windows
  gather_facts: false
  vars_files:
  - '/etc/ansible/.win_cred'

  - name: Installing DNS
    win_feature:
        name: DNS
        state: present
        include_management_tools: yes

  - name: Configure Domain
    win_domain:
      dns_domain_name: lks2024.id
      safe_mode_password: Skills39

  - name: Add Record
    win_dns_record:
        name: awu
        zone: lks2024.id
        type: A
        value: 10.17.8.45
```
