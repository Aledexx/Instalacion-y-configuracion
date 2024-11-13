Instalación de los Componentes Básicos

1. Abre tu sistema Linux y accede al terminal.

2. Dirígete al repositorio de GitHub de "rusben". Una vez allí, accede a la sección titulada "Instal·lacions i configuració de clouds" y abre el manual de instalación de aplicaciones web.

3. Actualización de Paquetes del Sistema:
   Primero, necesitarás actualizar los paquetes del sistema. Para hacer esto, introduce el siguiente código en el terminal. Este proceso puede pedirte una contraseña, la cual es "usuario".

   Comando para actualizar:
   ```bash
   sudo apt update
   
   sudo apt upgrade -y
   ```

4. Instalación del Servidor Web y Base de Datos:
   - Instala Apache2 (servidor web) con el siguiente comando:
     ```bash
     sudo apt install -y apache2
     ```
   - Luego, instala MySQL (servidor de base de datos) con el siguiente comando:
     ```bash
     sudo apt install -y mysql-server
     ```

5. Instalación de PHP y Librerías Necesarias:
   Instala PHP y sus librerías necesarias con los siguientes comandos:
   ```bash
   sudo apt install -y php libapache2-mod-php
   sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
   ```

   Estas librerías son esenciales para el correcto funcionamiento de las aplicaciones web.

6. Reiniciar Apache2:
   Después de instalar PHP, es necesario reiniciar Apache2 para aplicar los cambios:
   ```bash
   sudo systemctl restart apache2
   ```
