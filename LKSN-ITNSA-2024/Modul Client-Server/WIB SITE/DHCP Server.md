## Configure DHCP Server on WIB Site
## Konfigurasi DHCP Server pada WIB Site berdasarkan soal pra test.
**Tasks**:
![DHCP](https://github.com/user-attachments/assets/40ec636e-7a1a-42ab-8d62-4d1addfa9888)
### Step 1 - Installing Service
In FW-WIB
```bash
apt install isc-dhcp-server
```
### Step 2 - Configuring DHCP Server
Konfigurasi seperti biasa
### Step 3 - Konfigurasi DHCP IP Static
```bash
host LINSRV2 {
      hardware ethernet(mac address client);
      fixed-address 10.10.10.20;
}
