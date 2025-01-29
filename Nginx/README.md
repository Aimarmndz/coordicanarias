# Guía para Instalar Nginx en Ubuntu Server 24.04 y Configurar Puertos

## Introducción
Esta guía describe paso a paso cómo instalar, configurar y solucionar problemas comunes de Nginx en un servidor con Ubuntu Server 24.04.1 LTS.

## Requisitos Previos
- Servidor Ubuntu 24.04 instalado y actualizado. [Instalar](../Ubuntu22.04LTS/README.md)
- Acceso con permisos de superusuario con el comando (`sudo su`).

## Instalación de Nginx
1. **Actualizar el repositorios y sistema:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Instalar Nginx:**
   ```bash
   sudo apt install nginx -y
   ```

3. **Verificar la instalación:**
   ```bash
   nginx -v
   ```

## Configuración Inicial

1. **Iniciar y habilitar el servicio de Nginx:**
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

2. **Configurar el cortafuegos para permitir tráfico HTTP:**
   ```bash
   sudo ufw allow 80
   sudo ufw allow 443
   sudo ufw enable
   sudo ufw status
   ```

3. **Verificar que Nginx esté funcionando correctamente:**
   Accedemos a la dirección IP del servidor en un navegador: `http://173.16.0.90:80

## Configuración de Nginx

1. **Editar el archivo de configuración principal:**
   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```

   Configuración básica:
   ```nginx
	user www-data;
	worker_processes auto;
	pid /run/nginx.pid;
	error_log /var/log/nginx/error.log;
	include /etc/nginx/modules-enabled/*.conf;
   events {
        worker_connections 768;
        # multi_accept on;}
   http {

        server {
            listen       80;
            server_name  _;
            root         /usr/share/nginx/html;
        }

        server {
            server_name  example.com;
            root         /usr/share/nginx/html;
            access_log   /var/log/nginx/example.com/access.log;
            error_log    /var/log/nginx/example.com/error.log;
        }
   ```

Tendremos que especificar el puerto, en este caso el **80** y las rutas de los logs y del archivo HTML de inicio

2. **Verificar la configuración:**
   ```bash
   sudo nginx -t
   ```

3. **Reiniciar Nginx para aplicar los cambios:**
   En caso de que no hayan errores, podemos reiniciar el servicio para que se apliquen los cambios.
   ```bash
   sudo systemctl restart nginx
   ```

## Resolución de Problemas Comunes

### Error: Logs inexistentes

#### Problema:
```
open() "/var/log/nginx/example.com/access.log" failed (2: No such file or directory)
```

#### Solución:
1. Crear el directorio necesario:
   ```bash
   sudo mkdir -p /var/log/nginx/example.com/
   sudo chown www-data:www-data /var/log/nginx/example.com/
   ```
2. Cambiar las rutas de los logs si es necesario:
   ```nginx
   access_log /var/log/nginx/example.com/access.log;
   error_log /var/log/nginx/example.com/error.log;
   ```
3. Verificar la configuración y reiniciar:
   ```bash
   sudo nginx -t
   sudo systemctl restart nginx
   ```

---

### Nginx carga el HTML de Apache

#### Problema:
Acceder a la IP con el puerto del Nginx muestra la página de inicio de Apache.

#### Solución:
1. **Detener Apache:**
   ```bash
   sudo systemctl stop apache2
   ```

2. **Comprobar que Apache escuche en un puerto diferente:**
   ```bash
   sudo nano /etc/apache2/ports.conf
   ```
   Verificar que ponga: `Listen 8080`.

   También verificar los virtual hosts en `/etc/apache2/sites-available/`:
   ```apache
   <VirtualHost *:8080>
   ```

3. **Reiniciar Apache:**
   ```bash
   sudo systemctl restart apache2
   ```

4. **Configurar Nginx para manejar el tráfico HTTP:**
   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```
   Asegúrate de que el bloque `server` esté configurado correctamente con el puerto 80:
   ```nginx
   server {
            listen       80;
            server_name  _;
            root         /usr/share/nginx/html;
        }
   ```

5. **Reiniciar Nginx:**
   ```bash
   sudo systemctl restart nginx
   ```

6. **Verificar servicios:**
   ```bash
   sudo systemctl status nginx
   sudo systemctl status apache2
   ```

7. **Comprobar ruta del HTML predeterminado de Nginx:**
```bash
   sudo nano /etc/nginx/sites-available/default
```

```bash
   server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /usr/share/nginx/html;
        }
``` 
Una vez con los puertos bien configurados y las rutas de los HTML, ya podremos ver el HTML de bienvenida de Nginx

---
## Prueba Final

1. Acceder a la IP del servidor en un navegador: `http://173.16.0.90
2. Deberíamos ver la página de inicio de Nginx. Si todo funciona correctamente, podemos reemplazar el contenido del directorio `/usr/share/nginx/html/` con nuestro propio contenido.


