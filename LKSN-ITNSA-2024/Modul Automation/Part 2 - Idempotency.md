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
```yml
