# Manual Simple para Configurar ownCloud

Este manual te guiará paso a paso para configurar **ownCloud** desde su  web, de forma **sencilla**.

## 1. Acceso a ownCloud

- Abre tu navegador y ve a la URL donde instalaste ownCloud, por ejemplo: `http://localhost/owncloud` 
- Inicia sesión con el usuario administrador que creaste durante la instalación.

## 2. Configuración Inicial

- Haz clic en el icono de tu usuario (arriba a la derecha) y selecciona **Configuración**.
- Ajusta el idioma o lo que tu quieras cambiar.

## 3. Almacenamiento y Archivos

- Ve a **Configuración de administración** > **Almacenamiento externo**.
- Si necesitas, agrega servicios de almacenamiento como Amazon S3, Google Drive o WebDAV.

## 4. Seguridad Básica

- Asegúrate de que tu servidor use HTTPS para conexiones seguras.
- Ve a **Configuración de administración** > **Seguridad** y:
  - Configura la lista de dominios permitidos.
  - Activa políticas de contraseñas seguras (longitud mínima y complejidad).

## 5. Usuarios y Grupos

- En el menú **Usuarios**, puedes:
  - Crear nuevos usuarios.
  - Agruparlos para gestionar permisos de forma más sencilla.
  - Integrar ownCloud con LDAP/Active Directory si es necesario.

## 6. Mejorar el Rendimiento

- Configura la **caché de memoria**:
  - Instala `APCu` o `Redis` en tu servidor.
  - Agrégalo en el archivo `config.php` de ownCloud.
- Configura tareas programadas con `cron`:
  ```bash
  crontab -u www-data -e
  ```
  Agrega la línea:
  ```bash
  */15 * * * * php -f /var/www/html/owncloud/occ system:cron
  ```

## 7. Instalar Aplicaciones

- Accede al **Marketplace de ownCloud** desde la interfaz para instalar herramientas adicionales como editores de documentos.

## 8. Copias de Seguridad

- Realiza copias de seguridad regulares:
  ```bash
  rsync -Aax /var/www/html/owncloud /ruta/de/respaldo
  mysqldump -u usuario -p bbdd > /ruta/de/respaldo/owncloud_bbdd.sql
  ```

## 9. Actualizaciones

- Revisa periódicamente las actualizaciones en **Configuración de administración** > **Actualización**.
- Haz siempre una copia de seguridad antes de actualizar.


Con estos pasos, tu ownCloud estará listo y configurado 

