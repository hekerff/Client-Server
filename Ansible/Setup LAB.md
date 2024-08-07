## Setup LAB
### Menyiapkan LAB untuk praktik Ansible Automation.
Pada setup LAB Ansible kali ini, saya akan membuat beberapa konfigurasi ansible seperti membuat file berisi credential login linux & Windows lalu dienkripsi dan mengatur ansible.cfg untuk mencari file yang berisi password dari vault.
### 1 - Membuat File Credential untuk Linux & Windows
**LINUX**:
Kita buat sebuah file dengan nama bebas, saya akan beri nama lin_cred agar mudah diingat.
```ini
ansible_ssh_user: User
ansible_ssh_pass: Password
ansible_sudo_pass: Password_sudo
```
**WINDOWS**:
Selanjutnya kita buat file credential untuk Windows.
```INI
ansible_user: User
ansible_password: Password

#Untuk Mengatur Koneksi ke Windows

ansible_port: 5986
ansible_connection: winrm
ansible_winrm_transport: basic
ansible_winrm_server_cert_validation: ignore
```
