# **Lapres Praktikum Jarkom Modul 3 Kelompok D15**

### **Anggota Kelompok**

| **Nama**                  | **NRP**    |
| ------------------------- | ---------- |
| Rayhan Arvianta Bayuputra | 5025211217 |
| Yehezkiel Wiradhika       | 5025201086 |

## Daftar Isi

- [Prerequisites](#Prerequisites)
    - [Setup Topologi](#SetupTopologi)
    - [Konfigurasi Network](#KonfigurasiNetwork)
- [Soal 0](#Soal-0)
- [Setup DHCP](#Setup-DHCP)
- [PHP Worker](#PHP-Worker)
    - [Soal 6](#Soal-6)
    - [Soal 7](#Soal-7)
    - [Soal 8](#Soal-8)
    - [Soal 9](#Soal-9)
    - [Soal 10](#Soal-10)
    - [Soal 11](#Soal-11)
    - [Soal 12](#Soal-12)
- [Laravel Worker](#Laravel-Worker)
    - [Soal 13](#Soal-13)
    - [Soal 14](#Soal-14)
    - [Soal 15](#Soal-15)
    - [Soal 16](#Soal-16)
    - [Soal 17](#Soal-17)
    - [Soal 18](#Soal-18)
    - [Soal 19](#Soal-19)
    - [Soal 20](#Soal-20)

## Prerequisites

Terdapat beberapa hal yang harus disiapkan sebelum terjun ke soal-soal praktikum, yaitu setup topologi dan network configurations yang ada. _**(Soal 1)**_

### Setup Topologi

Topologi disiapkan sesuai dengan ketentuan pada praktikum, seperti pada gambar dan tabel berikut.

![topology](./assets/topology.png)

| Node               | Kategori         | Image Docker                        | Konfigurasi IP | 
|--------------------|------------------|-------------------------------------|----------------| 
| Aura               | Router (DHCP Relay)| danielcristh0/debian-buster:1.1   | Dynamic        | 
| Himmel             | DHCP Server      | danielcristh0/debian-buster:1.1   | Static         | 
| Heiter             | DNS Server       | danielcristh0/debian-buster:1.1   | Static         | 
| Denken             | Database Server  | danielcristh0/debian-buster:1.1   | Static         | 
| Eisen              | Load Balancer    | danielcristh0/debian-buster:1.1   | Static         | 
| Frieren            | Laravel Worker   | danielcristh0/debian-buster:1.1   | Static         | 
| Flamme             | Laravel Worker   | danielcristh0/debian-buster:1.1   | Static         | 
| Fern               | Laravel Worker   | danielcristh0/debian-buster:1.1   | Static         | 
| Lawine             | PHP Worker       | danielcristh0/debian-buster:1.1   | Static         | 
| Linie              | PHP Worker       | danielcristh0/debian-buster:1.1   | Static         | 
| Lugner             | PHP Worker       | danielcristh0/debian-buster:1.1   | Static         | 
| Revolte            | Client           | danielcristh0/debian-buster:1.1   | Dynamic        | 
| Richter            | Client           | danielcristh0/debian-buster:1.1   | Dynamic        | 
| Sein               | Client           | danielcristh0/debian-buster:1.1   | Dynamic        | 
| Stark              | Client           | danielcristh0/debian-buster:1.1   | Dynamic        | 

### Konfigurasi Network

Dengan ketentuan yang ada, berikut adalah list IP dan network configuration dari tiap node.

#### IPs

```
Aura: Dynamic DHCP
Himmel: 10.29.1.1
Heiter: 10.29.1.2
Denken: 10.29.2.1
Elsen: 10.29.2.2
Frieren: 10.29.4.1
Flamme: 10.29.4.2
Fern: 10.29.4.3
Lawine: 10.29.3.1
Linie: 10.29.3.2
Lugner: 10.29.3.3
Revolte: Dynamic DHCP
Richter: Dynamic DHCP
Sein: Dynamic DHCP
Stark: Dynamic DHCP
```

#### Aura (Router/DHCP Relay)

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.29.1.254
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.29.2.254
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.29.3.254
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.29.4.254
	netmask 255.255.255.0
```

#### Himmel (DHCP Server)

```
auto eth0
iface eth0 inet static	
address 10.29.1.1
netmask 255.255.255.0
gateway 10.29.1.254
```

#### Heiter (DNS Server)

```
auto eth0
iface eth0 inet static	
address 10.29.1.2
netmask 255.255.255.0
gateway 10.29.1.254
```

#### Denken (Database Server)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether d2:5b:49:77:c6:53
```

#### Eisen (Load Balancer)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 2e:14:fa:49:d4:26
```

#### Frieren (Laravel Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 62:85:dc:12:6a:e1
```

#### Flamme (Laravel Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 0a:c9:e8:93:9a:99
```

#### Fern (Laravel Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 56:68:5d:5c:05:38
```

#### Lawine (PHP Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 26:5f:26:7d:8f:93
```

#### Linie (PHP Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether a2:22:e8:fa:6f:3d
```

#### Lugner (PHP Worker)

```
auto eth0
iface eth0 inet dhcp
hwaddress ether 26:88:d2:3f:d6:34
```

#### Revolte (Client)

```
auto eth0
iface eth0 inet dhcp
```

#### Ritcher (Client)

```
auto eth0
iface eth0 inet dhcp
```

#### Sein (Client)

```
auto eth0
iface eth0 inet dhcp
```

#### Stark (Client)

```
auto eth0
iface eth0 inet dhcp
```

## Soal 0
Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa **riegel.canyon.yyy.com** untuk worker Laravel dan **granz.channel.yyy.com** untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.

Sebelumnya kita harus menginstall bind9 sebelum nantinya dikonfigurasi seperti keinginan soal.

```sh
apt-get update
apt-get install bind9 -y
```

Kemudian kita konfigurasi Bind9 seperti keinginan soal, mulai dari ``named.conf.local``, ``named.conf.options``, hingga bind zone file dari setiap zone.

_named.conf.local_

```
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "riegel.canyon.d15.com" {
        type master;
        file "/etc/bind/jarkom/riegel.canyon.d15.com";
};

zone "granz.channel.d15.com" {
        type master;
        file "/etc/bind/jarkom/granz.channel.d15.com";
};
```

Pada file tersebut dideklarasikan dua zone untuk setiap domain.

_named.conf.options_

```
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        forwarders {
                192.168.122.1;
        };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;

        allow-query{any;};
        listen-on-v6 { any; };
};
```

Disini kita forward nameserver dari router supaya client atau server yang connect ke DNS Server mendapatkan internet.

**/etc/bind/jarkom/riegel.canyon.d15.com**

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.d15.com. root.riegel.canyon.d15.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.d15.com.
@       IN      A       10.29.4.1       ; IP Frieren
www     IN      CNAME   riegel.canyon.d15.com.
```

**/etc/bind/jarkom/granz.channel.d15.com**

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.d15.com. root.granz.channel.d15.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.d15.com.
@       IN      A       10.29.3.1       ; IP Lawine
www     IN      CNAME   granz.channel.d15.com.
```

Setelah mengkonfigurasi setiap zone dengan mengarahkan ke IP worker tujuan, hasilnya dapat diperiksa di client dengan menggunakan **ping** dan **nslookup**.

![soal0](./assets/soal0.png)

## Setup DHCP
Setup DHCP akan meliputi soal 2 hingga soal 5.
- Semua **CLIENT** harus menggunakan konfigurasi dari DHCP Server.
- Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 **(2)**
- Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 **(3)**
- Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut **(4)**
- Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit **(5)**

Untuk memenuhi kebutuhan soal, kita install isc-dhcp-server pada Himmel dan isc-dhcp-relay.

**Instalasi di Aura**

```
apt-get update
apt-get install isc-dhcp-relay -y
```

**Instalasi di Himmel**

```
apt-get update
apt-get install isc-dhcp-server -y
```

Kemudian kita lakukan konfigurasi pada **Himmel**

**/etc/dhcp/dhcpd.conf**

```
subnet 10.29.1.0 netmask 255.255.255.0 {
}

subnet 10.29.2.0 netmask 255.255.255.0 {
    option routers 10.29.2.254;
    option broadcast-address 10.29.2.255;
    option domain-name-servers 10.29.1.2;
    default-lease-time 7200;
    max-lease-time 7200;
}

#Client Switch 3
subnet 10.29.3.0 netmask 255.255.255.0 {
    range 10.29.3.16 10.29.3.32;
    range 10.29.3.64 10.29.3.80;
    option routers 10.29.3.254;
    option broadcast-address 10.29.3.255;
    option domain-name-servers 10.29.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

#Client Switch 4
subnet 10.29.4.0 netmask 255.255.255.0 {
    range 10.29.4.12 10.29.4.20;
    range 10.29.4.160 10.29.4.168;
    option routers 10.29.4.254;
    option broadcast-address 10.29.4.255;
    option domain-name-servers 10.29.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}

#Database Server
host Denken {
    hardware ethernet d2:5b:49:77:c6:53;
    fixed-address 10.29.2.1;
}

#Load Balancer
host Eisen {
    hardware ethernet 2e:14:fa:49:d4:26;
    fixed-address 10.29.2.2;
}

#Laravel Workers
host Frieren {
    hardware ethernet 62:85:dc:12:6a:e1;
    fixed-address 10.29.4.1;
}

host Flamme {
    hardware ethernet 0a:c9:e8:93:9a:99;
    fixed-address 10.29.4.2;
}

host Fern {
    hardware ethernet 56:68:5d:5c:05:38;
    fixed-address 10.29.4.3;
}

#PHP Workers
host Lawine {
    hardware ethernet 26:5f:26:7d:8f:93;
    fixed-address 10.29.3.1;
}

host Linie {
    hardware ethernet a2:22:e8:fa:6f:3d;
    fixed-address 10.29.3.2;
}

host Lugner {
    hardware ethernet 26:88:d2:3f:d6:34;
    fixed-address 10.29.3.3;
}
```

**/etc/default/isc-dhcp-dhcp-server**

```
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#       Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#       Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="eth0"
INTERFACESv6=""
```

Kemudian kita lakukan konfigurasi pada **Aura**

**/etc/default/isp-dhcp-relay**

```
# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="10.29.1.1"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

Dan un-comment ``net.ipv4.ip_forward=1`` pada **/etc/sysctl.conf**.

Jangan lupa untuk restart service DHCP pada setiap node setelah melakukan konfigurasi dengan menggunakan command ``service dhcp-(relay/server)-restart``.

Berikut adalah hasil dari sisi client

![dhcp-client](./assets/dhcp-client.png)

## PHP Worker

Segala konfigurasi dan testing pada PHP Worker memenuhi soal 6 hingga 12. Sebagai persiapan, kita harus menginstall nginx, php7.3, php7.3-fpm, htop, wget, dan zip/unzip pada setiap worker.
```sh
apt-get update -y
apt-get install nginx php7.3 php7.3-fpm htop wget unzip -y
```

### Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website <a href="https://drive.google.com/file/d/1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1/view?usp=sharing">berikut</a> dengan menggunakan php 7.3.

Hal-hal yang kita harus penuhi adalah mendownload dan unzip source code website, hingga configure nginx agar bisa diaccess client.

Download dan unzip source code website dengan menggunakan wget dan unzip pada /var/www
```sh
wget --no-check-certificate 'https://drive.usercontent.google.com/download?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download&authuser=0&confirm=t&uuid=0e499712-8150-42d4-a474-b29dfb026ab6&at=APZUnTVBse4ducwDDntmAkLSWB1_:1699949521984' -O  granz.channel.d15.com
unzip granz.channel.d15.com
```

setting nginx masing-masing worker di **/etc/nginx/sites-available/default**

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        index index.php index.html index.htm;

        server_name _;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.3-fpm.sock;
        }
}
```

aktifkan php7.3-fpm dan nginx pada masing-masing worker

```
service php7.3-fpm start
service nginx start
```

setelah itu, kita melakukan setting di load balancer Eisen

untuk menjadikan Eisen load balancer sekaligus untuk keperluan testing, kita perlu menginstall beberapa hal, yakni nginx, php7.3. php7.3-fpm, htop, dan apache2-utils

```
$ apt-get update -y
$ apt-get install nginx php7.3 php7.3-fpm htop apache2-utils -y
```

kita lalu melakukan konfigurasi load balancer untuk **granz.channel.d15.com**

```
upstream backend  {
    hash $request_uri consistent;
    server 10.29.3.1; #IP Lawine
    server 10.29.3.2; #IP Linie
    server 10.29.3.3; #IP Lugner
}

server {
        listen 80;
        server_name granz.channel.d15.com;

        location / {
                proxy_pass http://backend;
                proxy_set_header    X-Real-IP $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header    Host $http_host;
        }

        location ~ /\.ht {
                deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}
```

### Soal 7
disini kita akan mengatur agar Eisen dapat bekerja dengan maksimal, lalu melakukan testing dengan 1000 request dan 100 request/second

command yang kita gunakan untuk melakukan testing:

```
$ ab -n 1000 -c 100 http://granz.channel.d15.com/
```

berikut merupakan hasil testing dengan menggunakan algoritma load balancing round robin, least connection, ip hash, dan generic hash

**roundrobin**

Complete requests:      1000

Failed requests:        0

Requests per second:    1130.87 [#/sec] (mean)

**least connection**

Complete requests:      1000

Failed requests:        0

Requests per second:    1143.11 [#/sec] (mean)

**ip hash**

Complete requests:      1000

Failed requests:        0

Requests per second:    1254.86 [#/sec] (mean)

**generic hash**

Complete requests:      1000

Failed requests:        0

Requests per second:    1232.61 [#/sec] (mean)

dari sini kita menyimpulkan bahwa algoritma terbaik adalah ip hash karena tidak ada request yang gagal dan dengan kecepatan request per detik yang paling tinggi dibanding dengan algoritma lainnya

### Soal 8
analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer

command untuk testing:

```
$ ab -n 200 -c 10 http://granz.channel.d15.com/
```

**Round Robin**

Report hasil testing apache benchmark:

<img src="assets/round_robin.png" />

Hasil testing grafik htop:

<img src="assets/round_robin_graph.png" />

**Least Connection**

Report hasil testing apache benchmark:

<img src="assets/least_conn.png" />

Hasil testing grafik htop:

<img src="assets/least_conn_graph.png" />

**IP Hash**

Report hasil testing apache benchmark:

<img src="assets/ip_hash.png" />

Hasil testing grafik htop:

<img src="assets/ip_hash_graph.png" />

**Generic Hash**

Report hasil testing apache benchmark:

<img src="assets/generic_hash.png" />

Hasil testing grafik htop:

<img src="assets/generic_hash_graph.png" />

**Grafik request per second masing-masing algoritma**

<img src="assets/graph.png" />

**Analisis**

Berdasarkan dari data hasil testing dengan menggunakan Apache Benchmark dan grafik request per second, kita dapat menyimpulkan bahwa algoritma load balancing paling cepat adalah generic hash, tetapi kecepatannya relatif sama dengan algoritma Round Robin dan IP Hash, sedangkan algoritma yang paling lambat (request per secondnya) adalah Least Connection, tetapi dua algoritma yang paling banyak mengalami failed requests adalah Round Robin dan Least Connection, sedangkan algoritma IP Hash dan Generic Hash tidak mengalami failed requests sama sekali.

### Soal 9
Disini kita akan melakukan testing dengan menggunakan algoritma Round Robin dengan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian kita akan melihat perbandingan mereka dengan membuat grafik

command untuk testing
```
$ ab -n 100 -c 10 http://granz.channel.d15.com/
```

**3 Worker**

apache benchmark:

<img src="assets/3_workers.png" />

grafik htop:

<img src="assets/3_workers_graph.png" />

**2 Worker**

apache benchmark:

<img src="assets/2_workers.png" />

grafik htop:

<img src="assets/2_workers_graph.png" />

**1 Worker**

apache benchmark:

<img src="assets/1_workers.png" />

grafik htop:

<img src="assets/1_workers_graph.png" />

Berikut merupakan grafik perbandingannya

<img src="assets/graph_1.png" />

### Soal 10
Di sini, kita akan melakukan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

untuk autentikasi, kita perlu membuat file berisi username dan password dengan command sebagai berikut

```
$ htpasswd -b -c /etc/nginx/rahasisakita/.htpasswd netics ajkd15
```

kemudian, kita perlu menambahkan konfigurasi berikut pada ``/etc/nginx/sites-available/lb-jarkom``

```
auth_basic "Administrator's Area";
auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;
```

### Soal 11
Di sini kita membuat setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id

untuk melakukannya, kita perlu menambahkan beberapa konfigurasi pada Eisen, tepatnya di ``/etc/nginx/sites-available/lb-jarkom`` dengan konfigurasi sebagai berikut:

```
location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
}
```

### Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168

untuk melakukannya, kita perlu menambahkan beberapa konfigurasi pada Eisen, tepatnya di ``/etc/nginx/sites-available/lb-jarkom`` dengan konfigurasi sebagai berikut:

```
allow 10.29.3.69;
allow 10.29.3.70;
allow 10.29.4.167;
allow 10.29.4.168;
deny all;
```

Berikut merupakan konfigurasi lengkap ``/etc/nginx/sites-available/lb-jarkom`` dengan algoritma Round Robin (default)

```
upstream backend  {
server 10.29.3.1; #IP Lawine
server 10.29.3.2; #IP Linie
server 10.29.3.3; #IP Lugner
}

server {
listen 80;
server_name granz.channel.d15.com;

        location / {
                proxy_pass http://backend;
                proxy_set_header    X-Real-IP $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header    Host $http_host;

                auth_basic "Administrator's Area";
                auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

                allow 10.29.3.69;
                allow 10.29.3.70;
                allow 10.29.4.167;
                allow 10.29.4.168;
                deny all;
        }

        location ~ /its {
                proxy_pass https://www.its.ac.id;
                proxy_set_header Host www.its.ac.id;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
        }

        location ~ /\.ht {
                deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}
```