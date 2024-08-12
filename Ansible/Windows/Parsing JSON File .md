## Parsing File JSON
### Konfigurasi Playbook untuk melakukan parsing pada file json
Saya mencoba membuat playbook untuk melakukan parsing pada file json, yang nantinya akan digunakan untuk membuat Active Directory User.
### Alur Melakukan Parsing
(1) Langkah Pertama: Kita membuat playbook untuk localhost (control node), didalam playbook tersebut kita akan melakukan parsing file json lalu menyimpan hasil parsingan ke dalam sebuah file baru.
(2) Langkah kedua: Buat tasks baru pada playbook yang sama, atau buat pada playbook bar(bowlehh), dan definisikan file yang telah kita parsing pada **vars_files**

Langsung kita gaskan praktekan dan untuk file json yang akan diparsing isinya seperti ini
```json
{
"customers": [
    {
        "name": "Art Fade",
        "domain_prefix": "art",
        "username": "designer1",
        "password": "a$sd21aldGm-3A",
        "message": "Welcome to my art site"
    },
    {
        "name": "Management Corporation",
        "domain_prefix": "management",
        "username": "admin-mgr",
        "password": "SecureManagPassword$123",
        "message": "Management Corporation Website - Please contact manager@management.customer.com for more infos"
    },
    {
        "name": "Transport Bus Stations",
        "domain_prefix": "transport",
        "username": "transport-admin",
        "password": "FastFromA-to-B4",
        "message": "This site is currently under maintenance. Please visit later"
    },
    {
        "name": "Wood Works",
        "domain_prefix": "wood",
        "username": "daniel",
        "password": "Wo_Do_Wood_Work1",
        "message": "Are you looking for a carpenter? Please hire us via info@woodworks.com"
    },    
    {
        "name": "Smart Fitness",
        "domain_prefix": "fit",
        "username": "sport-man-1",
        "password": "WorkOut36$13",
        "message": "We will get your fitness to the next level, visit us at baker street 5 in california"
    }
]
}
```
### Step 1 - Parsing file json
