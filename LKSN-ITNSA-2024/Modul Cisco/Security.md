## Part 1 - SSH
**Pada TMT-1 dan TMT-2:**
```bash
crypto key generate rsa modulus 2048
ip ssh version 2

line vty 0 4
login local
transport input ssh
privilege level 15
exec-timeout 10 0
<exit>
access-list 10 permit 172.16.30.0 0.0.0.255
line vty 0 4
access-class 10 in
<DONE>
```

## Part 2 - Port Security
Lakukan pada SWL2-1 & SWL2-2 dan port yang mengarah ke client.
```bash
Masuk pada interface yang mengarah ke client

switchport port-security
switchport port-security mac-address sticky
switchport port-security maximum 2
switchport port-security violation restrict
<exit>
no errdisable detect cause all
logging trap informational
logging console informational

masuk ke interface host

logging event link-status
```
