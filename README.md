# Langkah-langkah-install-DNS-server-di-Debian-10
Langkah Kerja

Masukkan cd 2 dan 3

# apt-cdrom add

# apt-get update

Instalasi aplikasi DNS server

root@smkmanusa:~# apt-get install bind9 dnsutils

➔ masukkan cd 1 dan cd 2


Konfigurasi DNS server (file named.conf)

root@smkmanusa:~# nano /etc/bind/named.conf.default-zones Edit pada baris:


zone "smkmanusa.sch.id" {

type master;

file "/etc/bind/db.manusa";

};

zone "1.30.172.in-addr.arpa" {

type master;

file "/etc/bind/db.172";

};

zone "kompas.com" {

type master;

file "/etc/bind/db.kompas";

};

zone " tiktok.com " {

type master;

file "/etc/bind/db. tiktok ";

};


Keluar dan simpan. Ctrl x | y

Keluar dan simpan. Ctrl x | y


Kopi db.local menjadi db.manusa dan db.127 menjadi db.10

root@smkmanusa:~# cp /etc/bind/db.255 /etc/bind/db.manusa

root@smkmanusa:~# cp /etc/bind/db.127 /etc/bind/db.172

root@smkmanusa:~# cp /etc/bind/db.127 /etc/bind/db.kompas

root@smkmanusa:~# cp /etc/bind/db.127 /etc/bind/db.tiktok


Konfigurasi db.manusa dan db.10 db.kompas db.tiktok


root@smkmanusa:~# nano /etc/bind/db.manusa

• Kemudian ubah kata “localhost.” menjadi “smkmanusa.sch.id.” ➔ctrl W+R

@          IN    NS    smkmanusa.sch.id.

@          IN     A     172.30.1.1

@          IN     MX  10 mail.smkmanusa.sch.id

www   IN     A     172.30.1.1
mail     IN     A     172.30.1.1


Keluar dan simpan. Ctrl x | y

root@smkmanusa:~# nano /etc/bind/db.172

Kemudian ubah kata “localhost.” menjadi “smkmanusa.sch.id.” ➔ctrl W+R

• ubah “localhost.” menjadi “smkmanusa.sch.id.” dan tambahkan

@    IN     NS     smkmanusa.sch.id.

1     IN     PTR     smkmanusa.sch.id.


Keluar dan simpan. Ctrl x | y


root@smkmanusa:~# nano /etc/bind/db.kompas

• Kemudian ubah kata “localhost.” menjadi “Kompas.com.” ➔ctrl W+R

@     IN    NS     Kompas.com.

@     IN     A     96.96.96.96


Keluar dan simpan. Ctrl x | y


root@smkmanusa:~# nano /etc/bind/db.tiktok

• Kemudian ubah kata “localhost.” menjadi “tiktok.com.” ➔ctrl W+R

@     IN     NS     tiktok.com

@     IN     A     95.95.95.95


Keluar dan simpan. Ctrl x | y


#/etc/init.d/bind9 restart
