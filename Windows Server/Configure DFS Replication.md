## Configuring DFS Replication in Windows Server 2022
---
### Requirements before starting the configuration
- IP Address sudah terkonfigurasi
- Hostname sudah terkonfigurasi
- Active Directory terkonfiguras
- 2 Windows Server dan keduanya berada dalam 1 Domain yang sama
---
### Step 1 - Install DFS Replication
Make sure to install DFS Replication in both server. Click "Roles and Features" and Click Next until Server Roles.
![install-06-25 143321](https://github.com/hekerff/Client-Server/assets/159868331/d71cff5a-e081-48f8-9fb3-fbd2f42b837f)

**File and Storage Services ==> File and iSCSI Services ==> DFS Replication.**

**"Add Feature" --> "Next" --> "Install"**

### Step 2 - Configure DFS Replication
- Buka "Tools" lalu pilih DFS Management
- Lalu pilih **Replication**, di bagian **Action** pilih **New Replication Group**
![sdfdsaf](https://github.com/hekerff/Client-Server/assets/159868331/1912bf4b-4ffb-48f6-830b-5095c917d7de)
- Karena hanya menggunakan 2 server, pilih **Replication group for data collection**
![ratatata](https://github.com/hekerff/Client-Server/assets/159868331/0dfd00aa-043b-4223-a0ef-c630ab37c620)
- Beri nama untuk replication groupnya (sesuaikan), dan pilih domain yang sesuai.
- Pada menu Branch Server, masukan hostname komputer yang data nya ingin direplikasi. Pastikan komputer tersebut sudah dalam 1 domain.
- Pada Menu **Replicated Folders**, klik **Add** untuk menambahkan folder/path yang ingin direplikasi.
- Pada Menu **Hub Server**, masukan hostname dari komputer yang menjadi target untuk destinasi dari replikasi Branch Server.
- Selanjutnya tambahkan folder yang akan menjadi tempat dari data yang akan direplikasi. "Next"
- Opsi selanjutnya pilih "Replicate Continuously..." and "Next"
- Lalu **Create**
**DONE**
### Testing
- Uji dengan cara menaruh file pada Folder yang direplikasi di Branch Server dan lihat pada folder yang menjadi target di Hub Server.
- Jika tidak muncul, coba restart Hub Servernya.

Referensi:
- [DFS Replication](https://mshub.co.uk/how-to-configure-dfs-replication-setup-dfs-share/)
