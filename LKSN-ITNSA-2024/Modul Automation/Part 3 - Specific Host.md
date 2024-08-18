## Part 3 - Specific Host
### Pendahuluan!!!
Pada part 3 kita disuruh membuat beberapa playbook untuk menjalankan beberapa tugas seperti:
- 1. membuat playbook untuk merestart semua hosts dengan role dns
- 2. membuat playbook untuk merestart semua hosts dengan role web
- 3. membuat playbook untuk memberhentikan service dns di semua host dengan role dns.

### Number 1
```yml
- name: Restart hosts with dns role
  hosts: dns
  become: yes
  gather_facts: false
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Restart dns host
    reboot:
```
### Number 2
```yml
- name: Restart Web Host
  hosts: web
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'
  
  tasks:
  - name: Restarting host with web role
    reboot:
```
### Number 3
```yml
- name: Stopping DNS Service in hosts with DNS Role
  hosts: dns
  gather_facts: false
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Stopping DNS Service
    service:
      name: bind9
      state: stopped
```
