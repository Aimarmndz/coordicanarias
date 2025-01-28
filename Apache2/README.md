
# Guía para Instalar Apache2 en Ubuntu Server 24.04 y Configurar Puertos

## Introducción
Este documento explica cómo instalar Apache2 en un servidor Ubuntu 24.04 que ya tiene Nginx instalado. Además, se incluye cómo cambiar los puertos predeterminados de Apache2 a `8080` para HTTP y `8443` para HTTPS.

## Requisitos Previos
- Servidor Ubuntu 24.04 instalado y actualizado. [Instalar](../Ubuntu22.04LTS/README.md)
- Nginx configurado y funcionando en los puertos predeterminados [Configurar](../Nginx/README.md).
- Acceso con permisos de superusuario con el comando (`sudo su`).

---

## Paso 1: Actualizar el Sistema

Primero, asegúrate de que el sistema esté actualizado:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Paso 2: Instalar Apache2

Instala Apache2 con el siguiente comando:

```bash
sudo apt install apache2 -y
```

> **Nota:** Es probable que Apache2 no pueda iniciarse automáticamente porque los puertos 80 y 443 ya están ocupados por Nginx.

---

## Paso 3: Cambiar los Puertos de Apache2

Por defecto, Apache2 utiliza los puertos 80 y 443. Los cambiaremos a 8080 y 8443.

### 3.1 Modificar `ports.conf`

Edita el archivo `ports.conf` para definir los nuevos puertos:

```bash
sudo nano /etc/apache2/ports.conf
```

Cambia las líneas:

```plaintext
Listen 80
Listen 443
```

Por:

```plaintext
Listen 8080
Listen 8443
```

### 3.2 Actualizar Configuración de VirtualHosts

Edita el archivo de configuración del sitio predeterminado:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

Modifica la línea:

```plaintext
<VirtualHost *:80>
```

Por:

```plaintext
<VirtualHost *:8080>
```

Para configuraciones SSL, edita también:

```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf
```

Modifica:

```plaintext
<VirtualHost *:443>
```

Por:

```plaintext
<VirtualHost *:8443>
```

---

## Paso 4: Habilitar el Módulo SSL (Opcional)

Si necesitas HTTPS, hay que habilitar el módulo SSL:

```bash
sudo a2enmod ssl
```

Activa la configuración SSL predeterminada:

```bash
sudo a2ensite default-ssl.conf
```

---

## Paso 5: Reiniciar Apache2

Aplica los cambios reiniciando Apache2:

```bash
sudo systemctl restart apache2
```

---

## Paso 6: Verificar que Apache2 Esté Funcionando

Confirma que Apache2 está corriendo y escuchando en los nuevos puertos:

```bash
sudo ss -tuln | grep ':80\|:443'
```

Deberías ver algo como esto:

```plaintext
tcp        0      0 0.0.0.0:8080        0.0.0.0:*          LISTEN
tcp        0      0 0.0.0.0:8443        0.0.0.0:*          LISTEN
```

---

## Paso 7: Configurar el Firewall

Como estamos en localhost no es necesario estos pasos, pero si quisieramos abrir el servidor cara al público se deberá usar estos comandos que permite los nuevos puertos:

```bash
sudo ufw allow 8080/tcp
sudo ufw allow 8443/tcp
sudo ufw reload
```

---

## Conclusión

Apache2 ahora está configurado para utilizar los puertos 8080 y 8443, evitando conflictos con Nginx. Puedes acceder a Apache2 en `http://<tu_ip>:8080` o `https://<tu_ip>:8443`.

---




