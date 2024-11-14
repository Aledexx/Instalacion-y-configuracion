Instalación de los Componentes Básicos

1. Abre tu sistema Linux y accede al terminal.

2. Dirígete al repositorio de GitHub de "rusben". Una vez allí, accede a la sección titulada "Instal·lacions i configuració de clouds" y abre el manual de instalación de aplicaciones web.


Este manual es para intstalar OwnCloud

## Paso 1: Instalación de paquetes necesarios 

Ejecuta los siguientes comandos para instalar las dependencias y configurar 

### Instalación de software-properties-common
```bash
sudo apt install software-properties-common -y
```

### Agregar el repositorio 
```bash
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```

### Actualizar los paquetes
```bash
sudo apt update
```

### Instalar 
```bash
sudo apt install php7.4 -y
```

### Instalar módulos 
```bash
sudo apt install -y php libapache2-mod-php7.4
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```

## Paso 2: Configuración 

### Configurar la versión 
```bash
sudo update-alternatives --config php
```

### Habilitar módulos de Apache
```bash
sudo a2enmod proxy_fcgi setenvif
```

### Habilitar la configuración 
```bash
sudo a2enconf php7.4-fpm
```

### Reiniciar Apache
```bash
sudo service apache2 restart
```

## Paso 3: Actualizar e instalar Apache y MySQL

### Actualizar paquetes
```bash
sudo apt update
```

### Actualizar todo el sistema
```bash
sudo apt upgrade -y
```

### Instalar Apache
```bash
sudo apt install -y apache2
```

### Instalar MySQL
```bash
sudo apt install -y mysql-server
```

### Instalar PHP y sus extensiones
```bash
sudo apt install -y php libapache2-mod-php
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

### Reiniciar Apache
```bash
sudo systemctl restart apache2
```

## Paso 4: Configuración de la base de datos MySQL

### Ingresar a MySQL
```bash
sudo mysql
```

### Crear la base de datos
```sql
CREATE DATABASE bbdd;
```

### Crear el usuario y asignarle privilegios
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON bbdd.* TO 'usuario'@'localhost';
```

### Salir de MySQL
```sql
exit
```

### Verificar la conexión a la base de datos
```bash
mysql -u usuario -p
```

## Paso 5: Despliegue de los archivos de OwnCloud

### Copiar el archivo comprimido a la carpeta web
```bash
sudo cp ~/Baixades/app-web.zip /var/www/html
```

### Navegar al directorio web
```bash
cd /var/www/html
```

### Descomprimir el archivo
```bash
sudo unzip owncloud.zip
```

### Copiar el contenido descomprimido
```bash
sudo cp -R owncloud/. /var/www/html
```

### Eliminar la carpeta y archivo sobrantes
```bash
sudo rm -rf owncloud/
sudo rm -rf /var/www/html/index.html
```

## Paso 6: Configuración de permisos

### Cambiar permisos y propietario
```bash
cd /var/www/html
sudo chmod -R 775 .
sudo chown -R usuario:www-data .
```
