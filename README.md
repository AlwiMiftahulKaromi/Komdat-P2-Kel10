# Komdat-P2-Kel10
README.md

Ampache
Sekilas Tentang
Ampache adalah Aplikasi streaming audio atau video berbasis web dan pengelolaan file yang memungkinkan penggunanya mengakses musik dan video dari mana saja. Ampache dapat digunakan oleh hampir semua perangkat yang terhubung jaringan internet.

Instalasi
Kebutuhan Sistem :
Unix, Linux atau Windows.
Web-Server :
Apache (Versi paling sering digunakan pada lebih banyak pada fase testing)
lighttpd
nginx
IIS
PHP 5.4 atau versi lebih baru.
Modul PHP :
PDO
PDO_MYSQL
hash
session
JSON
MySQL 5.x
Proses Instalasi :
Dengan asumsi SSH sudah terpasang di server, lakukan login kedalam server menggunakan SSH. Untuk pengguna windows bisa menggunakan aplikasi PuTTY atau dengan menggunakan variasi dari linux shell yang tersedia untuk windows ( Contoh : Git Bash ).

Jika ssh belum terpasang

sudo apt install ssh
Jika ssh sudah terpasang, lanjut ke proses di bawah ini

$ ssh [server-username]@[server-ip-address] -p [port-number]

Contoh :

$ ssh student@127.0.0.1 -p 2222
Pastikan seluruh paket sistem kita ter-update, dan install seluruh kebutuhan dasar sistem seperti Apache, PHP, dan MySQL. Kemudian install tools bantuan lainnya, yaitu git dan composer yang berguna dalam proses instalasi Ampache.

$ sudo apt-get update
$ sudo apt-get install apache2
$ sudo apt-get install mysql-server
$ sudo apt-get install php
$ sudo apt-get install libapache2-mod-php
$ sudo apt-get install php-mysql
$ sudo apt-get install php-gd php-mcrypt php-mbstring php-xml php-ssh2 php-curl php-zip php-intl
$ sudo apt install git
$ sudo apt install composer
$ sudo service apache2 restart
Clone Ampache dengan Git ke dalam direktori var/ww/html/ .

$ sudo git clone https://github.com/ampache/ampache.git
Masuk ke dalam direktori var/www/html/ampacheyang merupakan hasil dari clone, lalu ubah permission dari folder config menjadi 777 (semua user dapat mengakses, menulis dan menjalankan) agar composer dan ampache dapat mengakses serta merubah isi file yang terdapat di dalam folder tersebut

$ sudo chmod 777 -R config
Kembali ke root folder ampache kemudian lakukan instalasi dependency yang diperlukan oleh ampache agar dapat berjalan di server dengan bantuan composer

$ sudo composer install
Ubah otorisasi kepemilikan ke webserver yang berjalan (Apache2).

//lakukan pada direktori /var/www/http untuk mengurangi resiko error
$ sudo chown -R www-data:www-data ampache
Konfigurasi web server Apache agar Ampache dapat berjalan .

$ sudo a2enmod rewrite
$ sudo nano /etc/apache2/apache2.conf
Pada file /etc/apache2/apache2.conf, ubah AllowOverride none menjadi AllowOverrie All pada bagian

<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
</Directory>
Menjadi

<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>
Kemudian lakukan restart Apache

sudo service apache2 restart
Mengubah maksimal ukuran file yang bisa di upload oleh apache. Edit file etc/php/7.0/apache2/php.ini dan ubah baris kode yang bersesuaian menjadi baris kode berikut :

upload_max_filesize = 300M
post_max_size = 300M
Restart kembali Apache web server.

$ sudo service apache2 restart
Buka halaman IP web server yang kita gunakan di browser dan akses folder dimana kita melakukan instalasi Ampache . (Misal jika menggunakan IP localhost) : 127.0.0.1:8888/ampache

Kemudian akan muncul halaman untuk melakukan pengecekan apakah seluruh requirements sudah terpenuhi

1

Jika requirements sudah terpenuhi, maka seluruh status akan mengembalikan Nilai OK

2

Konfigurasi database yang akan digunakan oleh Ampache

3

Konfigurasi pembuatan config file

4

5

6

Pada tabs file insight, dapat dilihat error-error seperti di gambar di bawah. Jika semua instalasi telah dilakukan dengan benar, ketika tombol create config diklik, maka file konfigurasi akan langsung tersimpan dan semua error tersebut akan teratasi. 7

Membuat user account untuk administrator
8

Setelah proses instalasi selesai, akan tampil halaman informasi versi dari Ampache, dan informasi update. Apabila ampache yang terinstall adalah versi terbaru dari github, maka tidak perlu dilakukan update. 9 Tombol update now hanya akan menampilkan bahwa ampache telah berada dalam versi yang terbaru.

Login ke dalam Ampache dengan menggunakan akun administrator yang telah dibuat sebelumnya. 10

Ampache telah berhasil terinstall 11

Cara Pemakaian
Sebelum menggunakan Ampache, pertama lakukanlah Login pada halaman awal dengan menggunakan akun yang sudah tersedia: 11 Hubungi Admin jika anda belum terdaftar dan ingin mendaftar ke ampache.
Pembahasan
Ampache dalam kemampuan untuk mengakses seluruh perpustakaan musik dari jarak jauh dan digunakan menggunakan PHP,HTML5 dan MySQL.

Kelebihan:

Terhubung ke layanan seperti LyricsWiki untuk mendapatkan lirik lagu.
Mendukung untuk dimainkan secara lokal untuk VLC dan Kodi
Multidevice di satu akun, dapat digunakan di banyak device berbeda dengan akun yang sama secara bersamaan.
Kekurangan:

Interfacenya kurang menarik
Tidak memiliki pemutaran cepat
Tidak ada fitur bookmark yang memungkinkan Anda melanjutkan dari tempat Anda tinggalkan.
Referensi
Github Official Installation Guide - Ampache
