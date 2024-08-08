## Setup LAB
### Menyiapkan LAB untuk praktik Ansible Automation.
Pada setup LAB Ansible kali ini, saya akan membuat beberapa konfigurasi ansible seperti membuat file berisi credential login linux & Windows lalu dienkripsi dan mengatur ansible.cfg untuk mencari file yang berisi password dari vault.
### 1 - Membuat File Credential untuk Linux & Windows
**LINUX**:
Kita buat sebuah file dengan nama bebas, saya akan beri nama lin_cred agar mudah diingat.
```yaml
ansible_ssh_user: User
ansible_ssh_pass: Password
ansible_sudo_pass: Password_sudo
```
**WINDOWS**:
Selanjutnya kita buat file credential untuk Windows.
```yaml
ansible_user: User
ansible_password: Password

#Untuk Mengatur Koneksi ke Windows

ansible_port: 5986
ansible_connection: winrm
ansible_winrm_transport: basic
ansible_winrm_server_cert_validation: ignore
```
### 2 - Melakukan Ecrypting & Decrypting file credential.
Enkripsi dilakukan agar file credential kita tetap aman dari hacker😈.
**Encrypt**
```bash
ansible-vault encrypt lin_cred
Password: Password_kalian
```
**Decrypt**
```bash
ansible-vault decrypt lin_cred
```
### Mengatur file ansible.cfg
Kita akan mengatuh ansible.cfg untuk membaca file yang berisi password, oleh karena itu kita perlu membuat file biasa yang berisi password dari vault kita.
```cfg
[defaults]
ansible_password_file = 
