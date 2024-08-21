## Part 2 - Idempotency
### Pendahuluan
Pada tasks ini kita disuruh untuk membuat beberapa playbook diantaranya adalah merubah /etc/hosts record di semua hosts.
### Number 1
```yml
- name: Update /etc/hosts on all Linux hosts
  hosts: linux
  become: yes
  vars_files:
  - '/etc/ansible/.lin_cred'

  tasks:
    - name: Ensure /etc/hosts contains unique records
      lineinfile:
        path: /etc/hosts
        line: "{{ ansible_host }} {{ hostname }}"
        state: present
        create: yes
```

### Number 2

Install Haproxy pada localhost, lalu bikin template nya menggunakan file .j2
```yml
- name: Install and Configure Reverse Proxy and Apache2
  hosts: linux
  gather_facts: false
  become: yes
  vars_files: 
  - '/etc/ansible/.lin_cred'

  tasks:
  - name: Install Haproxy
    apt:
      name:
      - haproxy
      - apache2
      state: present

  - name: Configure Haproxy
    template:
      src: /root/ansible/haproxy.cfg.j2
      dest: /etc/haproxy/haproxy.cfg

  - name: Restart Service
    service:
      name: haproxy
      state: restarted
```
      
