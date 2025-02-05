# Instalación de WordPress en Ubuntu Server 24.04 LTS

## Requisitos previos
Antes de comenzar, asegúrate de que tienes acceso a un servidor con Ubuntu Server 24.04 LTS y permisos de usuario con privilegios `sudo`.

## Paso 1: Actualizar el sistema
```sh
sudo apt update && sudo apt upgrade -y
```

## Paso 2: Instalar Apache
```sh
sudo apt install apache2 -y
```
Habilita Apache para que inicie automáticamente:
```sh
sudo systemctl enable apache2
```
Verifica que el servicio está corriendo:
```sh
sudo systemctl status apache2
```

## Paso 3: Instalar MySQL
```sh
sudo apt install mysql-server -y
```
Asegura la instalación ejecutando el siguiente comando y siguiendo las instrucciones:
```sh
sudo mysql_secure_installation
```

Inicia sesión en MySQL:
```sh
sudo mysql -u root -p
```
Crea una base de datos y usuario para WordPress:
```sql
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'contraseña_segura';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Paso 4: Instalar PHP y extensiones necesarias
```sh
sudo apt install php libapache2-mod-php php-mysql php-cli php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y
```
Verifica la instalación de PHP:
```sh
php -v
```

## Paso 5: Descargar WordPress
```sh
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
```
Extrae los archivos y muévelos al directorio de Apache:
```sh
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/html/
```
Otorga los permisos correctos:
```sh
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

## Paso 6: Configurar Apache para WordPress
Crea un nuevo archivo de configuración para WordPress:
```sh
sudo nano /etc/apache2/sites-available/wordpress.conf
```
Si cuentas con un dominio, añade el siguiente contenido:
```apache
<VirtualHost *:80>
    ServerAdmin admin@tudominio.com
    DocumentRoot /var/www/html/wordpress
    ServerName tudominio.com
    ServerAlias www.tudominio.com

    <Directory /var/www/html/wordpress/>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Si deseas usar WordPress en local sin un dominio, usa:
```apache
<VirtualHost *:80>
    ServerAdmin admin@localhost
    DocumentRoot /var/www/html/wordpress
    ServerName localhost

    <Directory /var/www/html/wordpress/>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Guarda y cierra el archivo. Luego habilita el sitio y el módulo `rewrite`:
```sh
sudo a2ensite wordpress.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

## Paso 7: Configurar WordPress
Renombra el archivo de configuración predeterminado:
```sh
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
```
Edita el archivo:
```sh
sudo nano wp-config.php
```
Modifica las siguientes líneas con los datos de la base de datos:
```php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'contraseña_segura');
define('DB_HOST', 'localhost');
```
Guarda y cierra el archivo.

## Paso 8: Completar la instalación desde el navegador
Abre tu navegador y accede a:
```
http://ip_del_equipo
```
Sigue el asistente de instalación de WordPress para completar la configuración.

## Paso 9: Habilitar HTTPS (Opcional en el caso de tener un dominio)
Si deseas usar HTTPS, instala y configura Let’s Encrypt con Certbot:
```sh
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
```
Sigue las instrucciones para obtener y configurar un certificado SSL.

## Conclusión
Ahora tienes un servidor Ubuntu 24.04 LTS con WordPress instalado y listo para usar, ya sea con un dominio o en un entorno local.
