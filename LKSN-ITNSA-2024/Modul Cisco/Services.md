## Part 1 - NAT
Pada bagian router TMT:
```bash
masuk ke interface yang mengarah ke Client
ip nat inside
masuk ke interface yang mengarah ke ISP
ip nat outside

access-list 10 permit 172.16.30.0 0.0.0.255
access-list 10 permit 172.16.40.0 0.0.0.255
access-list 10 permit 172.16.50.0 0.0.0.255

ip nat inside source list 10 interface g0/2 (yang mengarah ke ISP)
```
## Part 2 - FHRP

**VLAN 30**

**SWL3-1**
```bash
int vlan 30
standby version 2
standby 30 ip 172.16.30.0
standby 30 preempt
```
**SWL3-2**
```bash
int vlan 30
standby version 2
standby 30 ip 172.16.30.0
standby priority 99
standby 30 preempt
```

**VLAN 40**

**SWL3-1**
```bash
int vlan 40
standby version 2
standby 40 ip 172.16.40.254
standby 40 priority 99
standby 40 preempt
```

**SWL3-2**
```bash
int vlan 40
standby version 2
standby 40 ip 172.16.40.254
standby preempt
```

**VLAN 50**

**SWL3-1**
```bash
int vlan 50
standby version 2
standby 50 ip 172.16.50.254 
standby 50 preempt
```

**SWL3-2**
```bash
int vlan 50
standby version 2
standby 50 ip 172.16.50.254
standby 50 priority 99
standby preempt
```

## Part 3 - DHCP
Pada Router TMT-2

**VLAN 30**
```bash
ip dhcp excluded-address 172.16.30.1 172.16.30.100
ip dhcp excluded-address 172.16.30.201 172.16.30.254
ip dhcp pool VLAN30
network 172.16.30.0 255.255.255.0
default-router 172.16.30.254
domain-name lksn2024.id
```
lakukan hal yang sama untuk VLAN 40
## Part 4 - SNMP
lakukan pada TMT-1 dan TMT-2
```bash
snmp-server location Jakarta, Indonesia
snmp-server contact admin@lksn2024.id
```
## Part 5 - NTP
Lakukan pada semua Cisco Device
```bash
ntp-server <ip dari perangkat yang ada diatas perangkat tersebut yang mengarah ke BR-SRV.>
```
