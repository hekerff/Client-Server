## Firewall
### Konfigurasi Firewall di FW-WIB
Konfigurasi Firewall yang dilakukan adalah DNAT atau Destination NAT, jadi ketika ada request masuk ke IP Source maka akan diteruskan ke IP Destination.
### Step 1 - Installasi Iptables
pada FW-WIB lakukan installasi iptables
```bash
apt install iptables
```
### Step 2 - Konfigurasi DNAT
Kita akan membuat 2 konfigurasi jika untuk DNS, yang pertama untuk protokol UDP dan TCP.

**TCP**:
```bash
iptables -t nat -A PREROUTING -d 32.12.10.110 -p tcp --dport 53 -j DNAT --to-destination 10.10.10.10:53
```
**UDP**:
```bash
iptables -t nat -A PREROUTING -d 32.12.10.110 -p udp --dport 53 -j DNAT --to-destination 10.10.10.10:53
```
**LALU BUAT KONFIGURASI UNTUK POSTROUTING**
```bash
iptables -t nat -A POSTROUTING -j MASQUERADE
```
### Step 3 - Save Rules secara permanent
Agar Rules tetap permanent atau tidak hilang setelah direboot kita perlu melakukan installasi iptables-persistent
```bash
apt install iptables-persistent
```
Selanjutnya kita save rules
```bash
netfilter-persistent save
```

**CHECK RULES**
```bash
iptables -t nat -L -n -v
```
### DONE
