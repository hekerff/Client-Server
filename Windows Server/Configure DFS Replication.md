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
Buka "Tools" lalu pilih DFS Management
