```
Tugas Proyek Komdat P3
kelompok 6
anggota :
- Dzikri Ananda
- Muhammad Daffa Fakhi I.
- Muhammad Naufal A.
```

# Instalasi urlShortener di Server virtual

untuk aplikasi web yang coba kami instalasi adalah web url shortener, yang ada pada link berikut, dan ini adalah hasil instalasi aplikasi web tersebut. aplikasi web ini dapat diakses pada http://34.125.194.140/

Tahapannya :

1. Create vm. kami menggunakan google cloud dan hosting milik teman kami

2. login ke ssh nya, masukkan password dan uname

3. update server terlebih dahulu

4. install apache sebagai web server nya, dan setting firewall

5. install php dan jangan lupa di update 

6. install juga composer sebagai dependency manager pada php dilanjutkan dengan install curl, nodejs, dan MySQL server. karena web app ini menggunakan database, maka jangan lupa buat project di home, setting apache 2, dan setting permission dan selesai. 

7. web dapat digunakan dengan restart service apache2 terlebih dahulu.

## Code :
```cmd
sudo apt-get update
sudo apt-get upgrade

//install apache
sudo apt-get install apache2
sudo systemctl status apache2

//setting firewall
//sudo ufw enable
//sudo ufw allow 'Apache Full'


//install php
sudo apt-get install php libapache2-mod-php php-common php-gmp php-mbstring php-xmlrpc php-soap php-gd php-xml php-cli php-zip php-bcmath php-tokenizer php-json php-pear php-intl php-curl php-mysql
sudo apt-get update

//install composer
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
composer -v

//install  curl
sudo apt-get install curl

//install nodejs
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
node -v
npm -v

//install mysql-server
sudo apt-get install mysql-server

//buat database
sudo mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'linlaz';
create database bagisto
exit

//create project di home
composer create-project bagisto/bagisto

//seting apache2 
/* pada file /etc/apache2/apache2.conf */
sudo nano /etc/apache2/apache2.conf
<Directory /home/lazuardilintang/bagisto/public>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>

/* pada file /etc/apache2/sites-available/000-default */
sudo nano /etc/apache2/sites-available/000-default.conf
DocumentRoot /home/lazuardilintang/bagisto/public

//seting permission
sudo chmod -R 755 /home/lazuardilintang/bagisto
sudo chown -R www-data /home/lazuardilintang/bagisto

sudo systemctl restart apache2.service
or
sudo service apache2 restart
```