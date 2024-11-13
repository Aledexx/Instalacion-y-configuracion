# Guía de Instalación de ownCloud en un Servidor Linux

Esta guía te permitirá instalar **ownCloud** en un servidor Linux usando **Apache** como servidor web y **MySQL** como base de datos.

## 1. Actualizar el Sistema
Es recomendable actualizar tu sistema antes de empezar con la instalación:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y apache2
sudo apt install -y mysql-server
sudo apt install -y php libapache2-mod-php php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
sudo systemctl restart apache2
sudo mysql
CREATE DATABASE bbdd;
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON bbdd.* TO 'usuario'@'localhost';
FLUSH PRIVILEGES;
EXIT;
mysql -u usuario -p
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
sudo systemctl restart mysql
CREATE USER 'usuario'@'192.168.22.100' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON bbdd.* TO 'usuario'@'192.168.22.100';
FLUSH PRIVILEGES;
EXIT;
cd /tmp
wget https://download.owncloud.org/community/owncloud-latest.tar.bz2
tar -xjf owncloud-latest.tar.bz2
sudo mv owncloud /var/www/html/
sudo rm -rf /var/www/html/index.html
cd /var/www/html/owncloud
sudo chmod -R 775 .
sudo chown -R www-data:www-data .
sudo nano /etc/apache2/sites-available/owncloud.conf
sudo nano /etc/apache2/sites-available/owncloud.conf
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/owncloud
    ServerName ejemplo.com

    <Directory /var/www/html/owncloud>
        Options +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
sudo a2ensite owncloud.conf
sudo systemctl restart apache2
http://<tu_direccion_ip_o_nombre_de_dominio>/owncloud

En la página de configuración de ownCloud, ingresa los datos de la base de datos:

Nombre de la base de datos: bbdd
Usuario: usuario
Contraseña: password
Servidor: localhost

![ownCloud](https://upload.wikimedia.org/wikipedia/commons/b/b6/OwnCloud2-Logo.svg)
