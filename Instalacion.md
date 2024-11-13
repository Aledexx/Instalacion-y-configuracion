Abre tu sistema Linux.

1. **Abre el terminal**.
2. Dirígete al repositorio de GitHub de "rusben".
3. Accede a la sección titulada "Instal·lacions i configuració de clouds".
4. Entra en el manual de instalación de aplicaciones web.

### Comienzo de la Instalación
Primero, introduce el código de actualización de paquetes. Te solicitará una contraseña, la cual es "usuario".

Ejecuta el siguiente comando para actualizar tu sistema:
```
sudo apt update && sudo apt upgrade -y
```

### Instalación del Servidor Web

1. Una vez completada la actualización, instala Apache2 con el comando:
```
sudo apt install -y apache2
```
Esto instalará el servidor web Apache.

2. Procede a instalar el servidor de base de datos MySQL:
```
sudo apt install -y mysql-server
```

### Instalación de PHP y Librerías

1. Instala PHP y sus librerías necesarias ejecutando:
```
sudo apt install -y php libapache2-mod-php
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```
Estas librerías son esenciales para el correcto funcionamiento de las aplicaciones web.

2. Reinicia Apache2 para aplicar los cambios:
```
sudo systemctl restart apache2
```

### Configuración de MySQL

1. Accede a la consola de MySQL:
```
sudo mysql
```
2. Crea la base de datos con el nombre que prefieras (en este ejemplo, “bbdd”):
```
CREATE DATABASE bbdd;
```
3. Crea un usuario con permisos para la base de datos:
```
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
4. Otorga los privilegios al usuario:
```
GRANT ALL ON bbdd.* TO 'usuario'@'localhost';
```
5. Actualiza los privilegios y sal de MySQL:
```
FLUSH PRIVILEGES;
EXIT;
```

### Descarga y Preparación de OwnCloud

1. Descarga el archivo comprimido de OwnCloud:
```
wget https://download.owncloud.org/community/owncloud-latest.tar.bz2
```
2. Descomprime el archivo:
```
tar -xjf owncloud-latest.tar.bz2
```
3. Mueve el contenido a la carpeta de Apache:
```
sudo mv owncloud /var/www/html/
```
4. Elimina el archivo `index.html` predeterminado:
```
sudo rm -rf /var/www/html/index.html
```

### Configuración de Permisos

1. Cambia los permisos y la propiedad de los archivos:
```
sudo chmod -R 775 /var/www/html/owncloud
sudo chown -R www-data:www-data /var/www/html/owncloud
```

### Configuración de Apache

1. Edita el archivo de configuración de Apache:
```
sudo nano /etc/apache2/sites-available/owncloud.conf
```
2. Agrega la siguiente configuración:
```
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
```
3. Habilita el archivo de configuración y reinicia Apache:
```
sudo a2ensite owncloud.conf
sudo systemctl restart apache2
```

### Acceso a OwnCloud
Accede a tu instalación de OwnCloud a través de tu navegador con:
```
http://<tu_direccion_ip_o_nombre_de_dominio>/owncloud
```

### Configuración Final
En la página de configuración de OwnCloud, introduce los detalles de la base de datos:
- **Nombre de la base de datos**: bbdd
- **Usuario**: usuario
- **Contraseña**: password
- **Servidor**: localhost

Con estos pasos, tendrás OwnCloud instalado y configurado en tu servidor Linux.

