## Connection
### Cara agar semua Site bisa terkoneksi satu sama lain.
### IP FORWARD
Kita perlu mengaktifkan IP FORWARD di Setiap Device FW.
### Gateway
- Untuk masing - masing device pada masing masing site memiliki gateway yang mengarah ke FW nya masing - masing

- Lalu untuk FW:
  -  FW-WIB : Arahkan Gateway nya menuju FW-WIT
  -  FW-WITA : FW-WITA tidak perlu dikonfigurasi Gatewaynya karena gateway nya akan otomatis ada ketika melakukan konfigurasi VPN Site to Site.
  -  FW-WIT : Arahkan Gateway nya menuju FW-WITA
 
- Untuk BUDI-CLT: Dia akan bisa mengakses semua Site ketika sudah dikonfigurasi Remote Access VPN.

### DONE
