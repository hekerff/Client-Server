## File & Directory Management
### Memanjemen File & Directory di Windows Server 2022 menggunakan Ansible Playbook
Pada kali ini saya akan membuat playbook untuk mengelola file dan directory mulai dari:
- Membuat File
- Membuat Directory
- Copy File
- Membuat File yang berisikan Value didalamnya.

Langsung aja :)
```yml
tasks:
- name: Membuat file
  win_file:
    path: C:\Folder\IniFIle.txt
    state: touch

- name: Membuat Directory
  win_file:
    path: C:\IniDirectory
    state: directory

- name: Membuat File Berisi Tulisan
  win_copy:
    content: Ini itu Tulisan
    dest: C:\IniDirectory\Tulisan.txt

- name: Copy File dari Remote ke Host
  win_copy:
    src: /home/user/contoh.txt
    dest: C:\IniDirectory\contoh.txt
```
