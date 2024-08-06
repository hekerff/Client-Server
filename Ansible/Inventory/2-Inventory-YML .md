## Inventory YML
### Membuat Inventory dengan format YML
Sekarang kita akan membuat Inventory sederhana dengan format YML.
```yml
linux:
  hosts:
      LIN1:
        ansible_host: 192.168.1.1
        hostname: LIN1
      LIN2:
        ansible_host: 192.168.1.2
        hostname: LIN2

web:
  hosts:
      LIN1:
        webcolor: blue
        webport: 80

windows:
    hosts:
      WIN1:
        ansible_host: 192.168.1.100
      WIN2:
        ansible_host: 192.168.1.200
```
