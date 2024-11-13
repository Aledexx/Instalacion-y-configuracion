Configuración de la Base de Datos y OwnCloud

1. Configuración de MySQL:
   - Accede a la consola de MySQL con el siguiente comando:
     ```bash
     sudo mysql
     ```

   - Crea la base de datos con el nombre que prefieras (en este ejemplo, “bbdd”):
     ```bash
     CREATE DATABASE bbdd;
     ```

   - Crea un usuario con permisos para la base de datos:
     ```bash
     CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
     ```

   - Otorga los privilegios al usuario para que pueda gestionar la base de datos:
     ```bash
     GRANT ALL ON bbdd.* TO 'usuario'@'localhost';
     ```

   - Actualiza los privilegios y sal de MySQL:
     ```bash
     FLUSH PRIVILEGES;
     EXIT;
     ```

2. Descarga y Preparación de OwnCloud:
   - Descarga el archivo comprimido de OwnCloud:
     ```bash
     wget https://download.owncloud.org/community/owncloud-latest.tar.bz2
     ```

   - Descomprime el archivo descargado:
     ```bash
     tar -xjf owncloud-latest.tar.bz2
     ```

   - Mueve el contenido de OwnCloud a la carpeta correspondiente de Apache:
     ```bash
     sudo mv owncloud /var/www/html/
     ```

   - Elimina el archivo `index.html` predeterminado de Apache:
     ```bash
     sudo rm -rf /var/www/html/index.html
     ```

3. Configuración de Permisos:
   - Cambia los permisos y la propiedad de los archivos de OwnCloud:
     ```bash
     sudo chmod -R 775 /var/www/html/owncloud
     sudo chown -R www-data:www-data /var/www/html/owncloud
     ```

4. Configuración de Apache:
   - Edita el archivo de configuración de Apache para OwnCloud:
     ```bash
     sudo nano /etc/apache2/sites-available/owncloud.conf
     ```

   - Agrega la siguiente configuración en el archivo:
     ```bash
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

   - Habilita el archivo de configuración y reinicia Apache para aplicar los cambios:
     ```bash
     sudo a2ensite owncloud.conf
     sudo systemctl restart apache2
     ```

5. Acceso y Configuración Final de OwnCloud:
   - Accede a tu instalación de OwnCloud a través de tu navegador utilizando la dirección IP o nombre de dominio:
     ```bash
     http://<tu_direccion_ip_o_nombre_de_dominio>/owncloud
     ```

   - En la página de configuración de OwnCloud, introduce los detalles de la base de datos:
     - Nombre de la base de datos: bbdd
     - Usuario: usuario
     - Contraseña: password
     - Servidor: localhost
