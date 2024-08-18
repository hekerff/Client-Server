## Connection
### Mengatur koneksi ssh dan winrm antar control node dan managed node.
Agar kita tidak perlu memasukan inventory saat menjalankan playbook, lakukan hal berikut:
- Buat file ansible.cfg di /etc/ansible/ lalu tambahkan seperti berikut:
```ini
[defaults]
inventory = /etc/ansible/all-linux, /etc/ansible/site-1, /etc/ansible/site-2
```
Selanjutnya kita akan membuat file kredential dari host linux, buat dengan nama file .lin_cred, lalu edit seperti berikut:
```bash
ansible_ssh_user: user
ansible_ssh_pass: P@ssw0rd
ansible_sudo_pass: P@ssw0rd
```

Untuk windows:
```bash
ansible_user: Administrator
ansible_password: P@ssw0rd

ansible_port: 5986
ansible_connection: winrm
ansible_winrm_transport: basic
ansible_winrm_server_cert_validation: ignore
```
Dengan kedua hal diatas akan memudahkan kita dalam menjalankan sebuah playbook.
