## Dynamic Domain Name System
### Konfigurasi Dynamic Domain Name System
Melakukan konfigurasi Dynamic Domain System atau DDNS memerlukan 2 komponen, yaitu konfigurasi tambahan pada DNS Server dan DHCP Server, LINSRV1 sebagai DNS server dan FW-WIB sebagai DHCP Server.
### Step 1 - Konfigurasi DNS Server
Pada file konfigurasi /etc/bind/named.conf.local kita tambahkan seperti ini:

**allow-update { 10.10.10.254; };** 

### Step 2 - Konfigurasi DHCP Server
Selanjutnya kita tambahkan konfigurasi seperti berikut di dalam file /etc/dhcp/dhcpd_conf:

```bash
ddns-update-style interim;
update-static-leases on;
ddns-updates on;

zone barat.id. {
        primary 10.10.10.10:
}
zone 10.10.10.in-addr.arpa. {
        primary 10.10.10.10;
}
```

**RESTART KEDUA SERVICE**
