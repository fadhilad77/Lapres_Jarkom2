# Jarkom-Modul-2-E03-2023

## Anggota Kelompok
- Shaloom David Togu (5025211242)
- M Fadhil Abhista Daniswara (5025221208)
## Daftar Isi
- [Topologi](#topologi)
- [Configure](#configure) 
- [Soal 1](#soal-1)
  - [Jawaban](#jawaban)
- [Soal 2](#soal-2)
  - [Jawaban](#jawaban)
- [Soal 3](#soal-3)
  - [Jawaban](#jawaban)
- [Soal 4](#soal-4)
  - [Jawaban](#jawaban)
- [Soal 5](#soal-5)
  - [Jawaban](#jawaban)
- [Soal 6](#soal-6)
  - [Jawaban](#jawaban)
- [Soal 7](#soal-7)
  - [Jawaban](#jawaban)
- [Soal 8](#soal-8)
  - [Jawaban](#jawaban)
- [Soal 9](#soal-9)
  - [Jawaban](#jawaban)
- [Soal 10](#soal-10)
  - [Jawaban](#jawaban)
- [Soal 11](#soal-11)
  - [Jawaban](#jawaban)
- [Soal 12](#soal-12)
  - [Jawaban](#jawaban)
- [Soal 13](#soal-13)
  - [Jawaban](#jawaban)
- [Soal 14](#soal-14)
  - [Jawaban](#jawaban)
- [Soal 15](#soal-15)
  - [Jawaban](#jawaban)
- [Soal 16](#soal-16)
  - [Jawaban](#jawaban)
- [Soal 17](#soal-17)
  - [Jawaban](#jawaban)
- [Soal 18](#soal-18)
  - [Jawaban](#jawaban)
- [Soal 19](#soal-19)
  - [Jawaban](#jawaban)
- [Soal 20](#soal-20)
  - [Jawaban](#jawaban)

## Topologi


## Configure
Router
!(https://github.com/fadhilad77/Lapres_Jarkom2/blob/main/Jarkom-Modul-2-E03-2023.png)

WerkudaraDNSSlave



YudhistiraDNSMaster



WisanggeniWebServer



AbimanyuWebServer



PrabukusumaWebServer


ArjunaLoadBalancer



SadewaClient


Nakula Client


## Soal 1
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian seperti di soal. Folder topologi dapat diakses pada drive yang sudah disediakan pada platform praktikum jarkom.

### Jawaban
NakulaClient

Lakukan `ping google.com -c 5` pada NakulaClient

Hasil 



SadewaClient

Lakukan `ping google.com -c 5` pada SadewaClient

Hasil



## Soal 2
Buatlah website utama pada node arjuna dengan akses ke **arjuna.yyy.com** dengan alias **www.arjuna.yyy.com** dengan yyy merupakan kode kelompok.

### Jawaban
Yudhistira

Lakukan `nano no2.sh` pada YudhistiraClient

```
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo '
zone "arjuna.e03.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.e03.com";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/arjuna.e03.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.e03.com. root.arjuna.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.e03.com.
@       IN      A       10.38.1.4     ; IP Arjuna
www     IN      CNAME   arjuna.e03.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/arjuna.e02.com

service bind9 restart
```

NakulaClient

Gunakan IP Node Yudhistira dengan `nano /etc/resolv.conf` pada NakulaClient  



Lakukan `ping arjuna.e03.com -c 5` pada NakulaClient  

Hasil



Lakukan `ping www.arjuna.e03.com -c 5` pada NakulaClient  

Hasil



## Soal 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke **abimanyu.yyy.com** dan alias **www.abimanyu.yyy.com**.

### Jawaban
Yudhistira

Lakukan `nano no3.sh` pada YudhistiraClient

```
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo '
zone "arjuna.e03.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.e03.com";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/arjuna.e03.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.e03.com. root.arjuna.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.e03.com.
@       IN      A       192.207.1.4     ; IP Arjuna
www     IN      CNAME   arjuna.e03.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/arjuna.e03.com

service bind9 restart
```

NakulaClient

Gunakan IP Node Yudhistira dengan `nano /etc/resolv.conf` pada NakulaClient  



Lakukan `ping abimanyu.e03.com -c 5` pada NakulaClient

Hasil



Lakukan `ping www.abimanyu.e03.com -c 5` pada NakulaClient

Hasil



## Soal 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain **parikesit.abimanyu.yyy.com** yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

### Jawaban
Yudhistira

Lakukan `nano no4.sh` pada YudhistiraClient

```
#!/bin/bash

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.e03.com. root.abimanyu.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.e03.com.
@       IN      A       10.38.3.3     ; IP Abimanyu
www     IN      CNAME   abimanyu.e03.com.
parikesit IN    A       10.38.3.3     ; IP Abimanyu
@       IN      AAAA    ::1
' > /etc/bind/jarkom/abimanyu.e03.com

service bind9 restart
```

Lakukan `ping parikesit.abimanyu.e03.com -c 5` pada NakulaClient

Hasil



## Soal 5
Buat juga reverse domain untuk domain utama. (*Abimanyu saja yang direverse*)

### Jawaban

Yudhistira

Lakukan `nano no5.sh` pada YudhistiraClient

```
#!/bin/bash

echo '
zone "3.38.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.38.10.in-addr.arpa";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/3.38.10.in-addr.arpa

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.e03.com. root.abimanyu.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.38.10.in-addr.arpa. IN      NS      abimanyu.e03.com.
3                       IN      PTR     abimanyu.e03.com.       ; Byte ke-4 IP Abimanyu' > /etc/bind/jarkom/3.38.10.in-addr.arpa

service bind9 restart
```

Lakukan pengecekan pada addres yang dimiliki abimanyu



Lakukan `host -t PTR 10.38.3.3` pada NakulaClient

Hasil



## Soal 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

### Jawaban
Yudhistira

Lakukan `nano no6.sh` pada YudhistiraClient

```
#!/bin/bash

echo '
zone "arjuna.e03.com" {
        type master;
        also-notify { 10.38.2.2; }; // IP WerkudaraDNSSlave
        allow-transfer { 10.38.2.2; }; // IP WerkudaraDNSSlave
        file "/etc/bind/jarkom/arjuna.e03.com";
};

zone "abimanyu.e02.com" {
    type master;
    notify yes;
    also-notify { 10.38.2.2; }; // IP WerkudaraDNSSlave
    allow-transfer { 10.38.2.2; }; // IP WerkudaraDNSSlave
    file "/etc/bind/jarkom/abimanyu.e03.com";
};

zone "2.38.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.38.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

service bind9 restart
```

Werkudara

Lakukan `nano no6.sh` pada WerkudaraDNSSlave

```
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo '
zone "arjuna.e03.com" {
    type slave;
    masters { 10.38.2.3; }; // IP Yudhis
    file "/var/lib/bind/arjuna.e03.com";
};

zone "abimanyu.e12.com" {
    type slave;
    masters { 10.38.2.3; }; // IP Yudhis
    file "/var/lib/bind/abimanyu.e03.com";
};
' > /etc/bind/named.conf.local

service bind9 restart
```

Atur `service bind9` pada YudhistiraDNSMaster

Hasil



Lakukan `ping arjuna.e03.com -c 5` pada NakulaClient

Hasil



Lakukan `ping www.arjuna.e03.com` pada NakulaClient

Hasil



## Soal 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu **baratayuda.abimanyu.yyy.com** dengan alias **www.baratayuda.abimanyu.yyy.com** yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

### Jawaban
Yudhistira

Lakukan `nano no7.sh` pada YudhistiraClient

```
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.e03.com. root.abimanyu.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.e03.com.
@       IN      A       10.38.3.3     ; IP Abimanyu
www     IN      CNAME   abimanyu.e03.com.
parikesit IN    A       10.38.3.3     ; IP Abimanyu
ns1     IN      A       10.38.2.2     ; IP Werkudara
baratayuda IN   NS      ns1
@       IN      AAAA    ::1' > /etc/bind/jarkom/abimanyu.e03.com

service bind9 restart

echo 'options {
       directory "/var/cache/bind";

       // If there is a firewall between you and nameservers you want
       // to talk to, you may need to fix the firewall to allow multiple
       // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

       // If your ISP provided one or more IP addresses for stable
       // nameservers, you probably want to use them as forwarders.
       // Uncomment the following block, and insert the addresses replacing
       // the all-0'\''s placeholder.
       // forwarders {
       //      0.0.0.0;
       // };

       //========================================================================
       // If BIND logs error messages about the root key being expired,
       // you will need to update your keys.  See https://www.isc.org/bind-keys
       //========================================================================
       //dnssec-validation auto;
       allow-query{any;};

       auth-nxdomain no;    # conform to RFC1035
       listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

echo '
zone "arjuna.e03.com" {
       type master;
       file "/etc/bind/jarkom/arjuna.e03.com";
};

zone "abimanyu.e03.com" {
    type master;
    file "/etc/bind/jarkom/abimanyu.e03.com";
    allow-transfer { 10.38.2.2; }; // IP Werkudara
};

zone "2.38.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.38.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

service bind9 restart
```

Werkudara

Lakukan `nano no7.sh` pada WerkudaraDNSSlave

```
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo 'options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0'\''s placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

echo '
zone "arjuna.e03.com" {
    type slave;
    masters { 10.38.2.3; }; // IP Yudhis
    file "/var/lib/bind/arjuna.e02.com";
};

zone "abimanyu.e03.com" {
    type slave;
    masters { 10.38.2.3; }; // IP Yudhis
    file "/var/lib/bind/abimanyu.e03.com";
};

zone "baratayuda.abimanyu.e03.com" {
    type master;
    file "/etc/bind/baratayuda/baratayuda.abimanyu.e03.com";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/baratayuda
cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.e03.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.e03.com. root.baratayuda.abimanyu.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.e03.com.
@       IN      A       10.38.3.3     ; IP Abimanyu
www     IN      CNAME   baratayuda.abimanyu.e03.com.' > /etc/bind/baratayuda/baratayuda.abimanyu.e03.com

service bind9 restart
```

Lakukan `ping baratayuda.abimanyu.e03.com` pada Nakulaclient

Hasil



Lakukan `ping www.baratayuda.abimanyu.e03.com` pada Nakulaclient

Hasil



Lakukan `host -t CNAME www.baratayuda.abimanyu.e03.com` pada Nakulaclient

Hasil



## Soal 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses **rjp.baratayuda.abimanyu.yyy.com** dengan alias **www.rjp.baratayuda.abimanyu.yyy.com** yang mengarah ke Abimanyu.

### Jawaban
Werkudara

Lakukan `nano no8.sh` pada WerkudaraDNSSlave

```
#!/bin/bash

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.e03.com. root.baratayuda.abimanyu.e03.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.e03.com.
@       IN      A       10.38.3.3     ; IP Abimanyu
www     IN      CNAME   baratayuda.abimanyu.e03.com.
rjp     IN      A       10.38.3.3     ; IP Abimanyu
www.rjp IN      CNAME   rjp.baratayuda.abimanyu.e03.com.' > /etc/bind/baratayuda/baratayuda.abimanyu.e03.com

service bind9 restart
```

Lakukan `ping rjp.baratayuda.abimanyu.e03.com` pada Nakulaclient

Hasil



Lakukan `ping www.rjp.baratayuda.abimanyu.e03.com -c 5 ` pada NakulaClient

Hasil



## Soal 9
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.

### Jawaban
Pada node Arjuna, install nginx dan ubah konfigurasi file `/etc/nginx/sites-available/lb-jarkom` seperti berikut.

```
#!/bin/bash

 apt-get update
 apt-get install bind9 nginx

echo '
 # Default menggunakan Round Robin
 upstream myweb  {
        server 10.38.3.2; #IP Prabukusuma
        server 10.38.3.3; #IP Abimanyu
        server 10.38.3.4; #IP Wisanggeni
 }

 server {
        listen 80;
        server_name arjuna.e03.com www.arjuna.e03.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

 ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled

service nginx restart
```

Pada tiap node worker, buat direktori `/var/www/jarkom` lalu buat file **index.php** yang berisi pesan untuk menandakan worker mana yang sedang berjalan. Lakukan juga konfigurasi pada file `/etc/nginx/sites-available/jarkom` seperti berikut.

**Prabukusuma**
```
#!/bin/bash

apt-get update && apt install nginx php php-fpm -y

mkdir -p /var/www/jarkom

echo '<?php
 echo "Halo, Kamu berada di Prabukusuma";
 ?>' > /var/www/jarkom/index.php

echo '
 server {

        listen 80;

        root /var/www/jarkom/;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

 location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default
service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

**Abimanyu**
```
#!/bin/bash

apt-get update && apt install nginx php php-fpm -y

mkdir -p /var/www/jarkom

echo '<?php
 echo "Halo, Kamu berada di Abimanyu";
 ?>' > /var/www/jarkom/index.php

echo '
 server {

        listen 80;

        root /var/www/jarkom;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default
service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

**Wisanggeni**
```
#!/bin/bash

apt-get update && apt install nginx php php-fpm -y

mkdir -p /var/www/jarkom

echo '<?php
 echo "Halo, Kamu berada di Wisanggeni";
 ?>' > /var/www/jarkom/index.php

echo '
 server {

        listen 80;

        root /var/www/jarkom;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default
service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

*Catatan*:
- `ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled` digunakan untuk membuat symlink (link simbolik) dari file konfigurasi Nginx yang berada di direktori /etc/nginx/sites-available ke direktori /etc/nginx/sites-enabled
- `rm -rf /etc/nginx/sites-enabled/default` digunakan untuk menghapus file default agar default page nginx tidak muncul saat dilakukan lynx
- Jangan lupa untuk melakukan `service php7.0-fpm restart` dan `service nginx restart` setiap kali melakukan konfigurasi.

Untung testing, lakukan **lynx** ke setiap node worker dari **NakulaClient**.

`lynx 10.38.3.2` (IP Prabukusuma)<br>


`lynx 10.38.3.3` (IP Abimanyu)<br>


`lynx 10.38.3.4` (IP Wisanggeni)<br>


## Soal 10
Kemudian gunakan algoritma **Round Robin** untuk Load Balancer pada **Arjuna**. Gunakan *server_name* pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
- *Prabakusuma:8001*
- *Abimanyu:8002*
- *Wisanggeni:8003*

### Jawaban
Ubah konfigurasi file `/etc/nginx/sites-available/lb-jarkom` pada node Arjuna agar IP address dari setiap node workernya menyertakan port yang digunakan.

```
#!/bin/bash

echo '
 # Default menggunakan Round Robin
 upstream myweb  {
        server 10.38.3.2:8001; #IP Prabukusuma
        server 10.38.3.3:8002; #IP Abimanyu
        server 10.38.3.4:8003; #IP Wisanggeni
 }

 server {
        listen 80;
        server_name arjuna.e03.com www.arjuna.e03.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

 ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled

service nginx restart
```

Ubah juga konfigurasi file `/etc/nginx/sites-available/jarkom` pada setiap worker agar masing-masing worker mendengarkan (listen) port mereka sendiri.

**Prabukusuma**
```
#!/bin/bash

echo '
 server {

        listen 8001;

        root /var/www/jarkom/;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

 location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled

service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

**Abimanyu**
```
#!/bin/bash

echo '
 server {

        listen 8002;

        root /var/www/jarkom/;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

 location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled

service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

**Wisanggeni**
```
#!/bin/bash

echo '
 server {

        listen 8003;

        root /var/www/jarkom/;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }

 location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/jarkom

ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled

service php7.0-fpm start
service php7.0-fpm restart
service nginx restart
```

Untuk testing, lakukan lynx IP tiap worker disertai dengan port masing-masing pada NakulaClient.

`lynx 10.38.3.2:8001`<br>


`lynx 10.38.3.3:8002`<br>


`lynx 10.38.3.4:8003`<br>


`curl arjuna.e03.com`<br>


## Soal 11
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server **www.abimanyu.yyy.com**. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy

### Jawaban
Install command wget, unzip, dan juga apache2 pada node Abimanyu.
```
#!/bin/bash

apt-get install wget -y
apt-get install unzip -y
apt-get install apache2
```

Kemudian download dan unzip file abimanyu dari link google drive yang diberikan menggunakan command berikut.
```
wget -O '/var/www/abimanyu.e03.com' 'https://drive.usercontent.google.com/download?id=1a4V23hwK9S7hQEDEcv9FL14UkkrHc-Zc'
unzip -o /var/www/abimanyu.e03.com -d /var/www/
mv /var/www/abimanyu.yyy.com /var/www/abimanyu.e03
rm /var/www/abimanyu.e03.com
rm -rf /var/www/abimanyu.e03/abimanyu.yyy.com
```

Lakukan konfigurasi pada file `/etc/apache2/sites-available/abimanyu.e03.com.conf` seperti berikut.
```
echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.e02

  ServerName abimanyu.e02.com
  ServerAlias www.abimanyu.e03.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.e03.com.conf

service apache2 start
a2ensite abimanyu.e03.com.conf
service apache2 restart
```

Untuk testing, lakukan `lynx abimanyu.e03.com` pada NakulaClient.

Kami menemui permasalahan di mana `lynx abimanyu.e03.com` tidak memunculkan apa-apa, sementara `lynx abimanyu.e03.com/home.html` memunculkan pesan "Akulah Abimanyu".

`lynx abimanyu.e03.com`

`lynx abimanyu.e03.com/home.html`

## Soal 12
Setelah itu ubahlah agar url **www.abimanyu.yyy.com/index.php/home** menjadi **www.abimanyu.yyy.com/home**.

### Jawaban
Lakukan konfigurasi pada file `/etc/apache2/sites-available/abimanyu.e03.com.conf` dengan menambahkan
```
<Directory /var/www/abimanyu.e03/index.php/home>
        Options +Indexes
</Directory>

Alias "/home" "/var/www/abimanyu.e03/index.php/home"```
```

Seperti berikut
```
#!/bin/bash

service apache2 start

echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.e03

  ServerName abimanyu.e03.com
  ServerAlias www.abimanyu.e03.com

  <Directory /var/www/abimanyu.e03/index.php/home>
          Options +Indexes
  </Directory>

  Alias "/home" "/var/www/abimanyu.e03/index.php/home"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.e03.com.conf

service apache2 restart
```

Untuk testing, lakukan `lynx abimanyu.e03.com/home` pada NakulaClient. Pada nomor ini kami juga menemui permasalahan berupa 404 Not Found.


## Soal 13
Selain itu, pada subdomain **www.parikesit.abimanyu.yyy.com**, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy

### Jawaban
Download dan unzip file parikesit.abimanyu.
```
#!/bin/bash

wget -O '/var/www/parikesit.abimanyu.e03.com' 'https://drive.usercontent.google.com/download?id=1LdbYntiYVF_NVNgJis1GLCLPEGyIOreS'
unzip -o /var/www/parikesit.abimanyu.e03.com -d /var/www/
mv /var/www/parikesit.abimanyu.yyy.com /var/www/parikesit.abimanyu.e03
rm /var/www/parikesit.abimanyu.e03.com
rm -rf /var/www/parikesit.abimanyu.yyy.com
``` 

Lalu konfigurasi file `/etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf` seperti berikut.
```
echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.e03

  ServerName parikesit.abimanyu.e03.com
  ServerAlias www.parikesit.abimanyu.e03.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf

a2ensite parikesit.abimanyu.e03.com.conf
service apache2 restart
```

Untuk testing, lakukan `lynx parikesit.abimanyu.e03.com` pada NakulaClient.



## Soal 14
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).

### Jawaban
Tambahkan konfigurasi berikut untuk mengaktifkan directory listing pada folder /public dan mematikan directory listing pada folder /secret.
```
  <Directory /var/www/parikesit.abimanyu.e03/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.e03/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.e03/secret"
```

Sehingga konfigurasi file `/etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf` menjadi seperti berikut.
```
#!/bin/bash

mkdir -p /var/www/parikesit.abimanyu.e02/secret

echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.e03

  ServerName parikesit.abimanyu.e03.com
  ServerAlias www.parikesit.abimanyu.e03.com

  <Directory /var/www/parikesit.abimanyu.e03/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.e03/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.e03/secret"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf

service apache2 restart
```

Untuk testing, lakukan `lynx parikesit.abimanyu.e03.com/public` dan `lynx parikesit.abimanyu.e03.com/secret` pada NakulaClient.

`lynx parikesit.abimanyu.e03.com/public`<br>


`lynx parikesit.abimanyu.e03.com/secret`<br>


## Soal 15
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

### Jawaban
Tambahkan `ErrorDocument 404 /error/404.html` dan `ErrorDocument 403 /error/403.html` pada konfigurasi file `/etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf` seperti berikut.
```
#!/bin/bash

echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.e03

  ServerName parikesit.abimanyu.e03.com
  ServerAlias www.parikesit.abimanyu.e03.com

  <Directory /var/www/parikesit.abimanyu.e03/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.e03/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.e03/secret"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf

service apache2 restart
```

Untuk testing, lakukan `lynx parikesit.abimanyu.e03.com/testerror` dan `lynx parikesit.abimanyu.e03.com/secret` pada NakulaClient.

`lynx parikesit.abimanyu.e03.com/testerror` (Test 404 Not Found)



`lynx parikesit.abimanyu.e03.com/secret` (Test 403 Forbidden)


## Soal 16
Buatlah suatu konfigurasi virtual host agar file asset **www.parikesit.abimanyu.yyy.com/public/js** menjadi 
**www.parikesit.abimanyu.yyy.com/js** 

### Jawaban
Tambahkan konfigurasi alias untuk direktori /js pada file `/etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf` seperti berikut.

```
#!/bin/bash

echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.e03

  ServerName parikesit.abimanyu.e03.com
  ServerAlias www.parikesit.abimanyu.e03.com

  <Directory /var/www/parikesit.abimanyu.e03/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.e03/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.e03/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.e03/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf

service apache2 restart
```

Untuk testing, lakukan `lynx parikesit.abimanyu.e03.com/js` pada NakulaClient.



## Soal 17
Agar aman, buatlah konfigurasi agar **www.rjp.baratayuda.abimanyu.yyy.com** hanya dapat diakses melalui port 14000 dan 14400.

### Jawaban
Download dan unzip file rjp.baratayuda.abimanyu.

```
#!/bin/bash

wget -O '/var/www/rjp.baratayuda.abimanyu.e03.com' 'https://drive.usercontent.google.com/download?id=1pPSP7yIR05JhSFG67RVzgkb-VcW9vQO6'
unzip -o /var/www/rjp.baratayuda.abimanyu.e03.com -d /var/www/
mv /var/www/rjp.baratayuda.abimanyu.yyy.com /var/www/rjp.baratayuda.abimanyu.e03
rm /var/www/rjp.baratayuda.abimanyu.e03.com
rm -rf /var/www/rjp.baratayuda.abimanyu.yyy.com
```

Kemudian ubah konfigurasi file `/etc/apache2/sites-available/rjp.baratayuda.abimanyu.e03.com.conf` seperti berikut.

```
echo '
<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.e03

  ServerName rjp.baratayuda.abimanyu.e03.com
  ServerAlias www.rjp.baratayuda.abimanyu.e03.com

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.e03.com.conf
```

Dan tambahkan `Listen 14000` serta `Listen 14400` pada file `/etc/apache2/ports.conf` seperti berikut.

```
echo '
# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default.conf

Listen 80
Listen 14000
Listen 14400

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet' > /etc/apache2/ports.conf

a2ensite rjp.baratayuda.abimanyu.e02.com.conf
service apache2 restart
```

Untuk testing, lakukan `lynx rjp.baratayuda.abimanyu.e03.com:14000` atau `lynx rjp.baratayuda.abimanyu.e03.com:14400` pada NakulaClient.



Apabila menggunakan port selain 14000 atau 14400, maka website tidak dapat terhubung.



## Soal 18
Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.

### Jawaban
Ubah konfigurasi file `/etc/apache2/sites-available/rjp.baratayuda.abimanyu.e03.com.conf` seperti berikut.

```
#!/bin/bash

echo '
<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.e03

  ServerName rjp.baratayuda.abimanyu.e03.com
  ServerAlias www.rjp.baratayuda.abimanyu.e03.com

  <Directory /var/www/rjp.baratayuda.abimanyu.e03>
          AuthType Basic
          AuthName "Restricted Content"
          AuthUserFile /etc/apache2/.htpasswd
          Require valid-user
  </Directory>

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.e03.com.conf
```

Lalu panggil command `htpasswd` berikut untuk mengautentikasi username dan password.
```
htpasswd -c -b /etc/apache2/.htpasswd Wayang baratayudae02
```

Untuk testing, lakukan `lynx rjp.baratayuda.abimanyu.e03.com:14000` atau `lynx rjp.baratayuda.abimanyu.e03.com:14400` pada NakulaClient.




## Soal 19
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke **www.abimanyu.yyy.com (alias)**

### Jawaban
Ubah konfigurasi file `/etc/apache2/sites-available/000-default.conf` seperti berikut.

```
#!/bin/bash

echo '
<VirtualHost *:80>
    ServerAdmin webmaster@abimanyu.e03.com
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    Redirect / http://www.abimanyu.e03.com/
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

service apache2 restart
```

Untuk testing, lakukan lynx IP address Abimanyu (`lynx 10.38.3.3`). Dalam soal ini kami menemukan permasalahan yang sama dengan nomor 11, di mana `lynx 10.38.3.3` tidak memunculkan apa-apa, sementara `lynx 10.38.3.3/home.html` memunculkan pesan "Akulah Abimanyu".

`lynx 10.38.3.3`<br>


`lynx 10.38.3.3/home.html`<br>


## Soal 20
Karena website **www.parikesit.abimanyu.yyy.com** semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.

### Jawaban
Pertama jalankan comman `a2enmod rewrite` untuk mengaktifkan module rewrite.

Buat file `.htaccess` pada direktori `/var/www/parikesit.abimanyu.e03/` dan isi dengan konfigurasi berikut.
```
echo '
RewriteEngine On
RewriteCond %{REQUEST_URI} ^/public/images/(.*)abimanyu(.*)
RewriteCond %{REQUEST_URI} !/public/images/abimanyu.png
RewriteRule abimanyu http://parikesit.abimanyu.e03.com/public/images/abimanyu.png$1 [L,R=301]' > /var/www/parikesit.abimanyu.e03/.htaccess
```

Kemudian tambahkan

```
<Directory /var/www/parikesit.abimanyu.e03>
        Options +FollowSymLinks -Multiviews
        AllowOverride All
</Directory>
```

pada file `/etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf` seperti berikut.

```
echo '
<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.e03

  ServerName parikesit.abimanyu.e03.com
  ServerAlias www.parikesit.abimanyu.e03.com

  <Directory /var/www/parikesit.abimanyu.e03/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03/secret>
          Options -Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.e03>
          Options +FollowSymLinks -Multiviews
          AllowOverride All
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.e03/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.e03/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.e03/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.e03.com.conf

service apache2 restart
```

Untuk testing, lakukan command-command berikut.

`lynx parikesit.abimanyu.e03.com/public/images/not-abimanyu.png`

`lynx parikesit.abimanyu.e03.com/public/images/abimanyu-student.jpg`

`lynx parikesit.abimanyu.e03.com/public/images/abimanyu.png`

`lynx parikesit.abimanyu.e03.com/public/images/notabimanyujustmuseum.177013`



