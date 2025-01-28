
# Guía para Instalar Ubuntu Desktop 24.04 y Quitar la Interfaz Gráfica

## Introducción
Este documento detalla cómo instalar Ubuntu Desktop 24.04 desde cero utilizando Rufus en un sistema Windows, configurar SSH para administración remota y eliminar la interfaz gráfica si se requiere un entorno solo de línea de comandos.

## Requisitos Previos
- Un ordenador o máquina virtual compatible.
- Un sistema Windows para preparar el medio de instalación.
- Una imagen ISO de Ubuntu Desktop 24.04.
- Una unidad USB booteable (mínimo 8 GB de capacidad).
- Acceso a Internet.

---

## Paso 1: Descargar Ubuntu Desktop 24.04

1. Accede al sitio oficial de Ubuntu: [Descargar Ubuntu Desktop](https://ubuntu.com/download/desktop).
2. Descarga la imagen ISO correspondiente a la versión Ubuntu Desktop 24.04 LTS.

---

## Paso 2: Crear un Medio de Instalación con Rufus (Windows)

### 2.1 Descargar Rufus
1. Descarga Rufus desde su página oficial: [Rufus](https://rufus.ie).
2. Instala Rufus en tu sistema Windows o ejecuta su versión portable.

### 2.2 Crear el USB Booteable
1. Conecta la unidad USB al ordenador.
2. Abre Rufus y selecciona:
   - **Dispositivo:** tu unidad USB.
   - **Seleccionar:** carga la imagen ISO de Ubuntu descargada.
   - **Esquema de partición:** GPT (para sistemas modernos) o MBR (si usas BIOS legacy).
   - **Sistema de archivos:** FAT32.
3. Haz clic en **Iniciar** y espera a que se complete el proceso.

---

## Paso 3: Instalar Ubuntu Desktop

### 3.1 Arrancar desde el USB
1. Inserta el USB booteable en el equipo donde instalarás Ubuntu.
2. Accede al menú de arranque (generalmente presionando `F12`, `F2`, `Del`, o una tecla específica según tu sistema).
3. Selecciona el USB como dispositivo de inicio.

### 3.2 Seguir el Asistente de Instalación
1. Selecciona el idioma de instalación.
2. Configura la red y el teclado.
3. Define las particiones (puedes optar por el particionado automático si no tienes experiencia).
4. Completa el asistente y espera a que la instalación termine.

---

## Paso 4: Configurar SSH para Administración Remota

### 4.1 Instalar el Servidor SSH
1. Inicia sesión en el sistema instalado y abre una terminal.
2. Instala OpenSSH Server con el siguiente comando:

```bash
sudo apt install openssh-server -y
```

### 4.2 Verificar el Estado del Servicio SSH
Asegúrate de que el servicio SSH esté activo:

```bash
sudo systemctl status ssh
```

Si no está activo, inícialo:

```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

### 4.3 Configurar el Firewall para Permitir SSH
Si el firewall está habilitado, permite conexiones SSH:

```bash
sudo ufw allow ssh
sudo ufw enable
```

### 4.4 Obtener la Dirección IP
Obtén la dirección IP del sistema para conectarte remotamente:

```bash
ip addr show
```

Conecta al sistema desde otro dispositivo usando un cliente SSH como PuTTY (en Windows) o la terminal (`ssh usuario@ip-del-servidor`).

---

## Paso 5: Actualizar el Sistema

Una vez instalado y configurado el SSH, actualiza el sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Paso 6: Quitar la Interfaz Gráfica

Si prefieres un entorno de línea de comandos, elimina la interfaz gráfica.

### 6.1 Cambiar al Modo Texto
Cambia el target predeterminado al modo multiusuario (texto):

```bash
sudo systemctl set-default multi-user.target
```

### 6.2 Desinstalar Paquetes Gráficos
Elimina los paquetes relacionados con el escritorio:

```bash
sudo apt purge ubuntu-desktop gnome-shell gdm3 -y
sudo apt autoremove --purge -y
sudo apt autoclean
```

### 6.3 Reiniciar el Sistema
Reinicia el sistema para aplicar los cambios:

```bash
sudo reboot
```

---

## Paso 7: Verificar Conexión SSH y Modo Texto

1. Conéctate al sistema usando SSH para verificar que funciona correctamente.
2. Confirma que el sistema inicia en modo texto tras el reinicio.

--- 

## Conclusión

Con esta guía, has instalado Ubuntu Desktop 24.04, configurado SSH para administración remota y eliminado la interfaz gráfica para un entorno minimalista. Este proceso es ideal para sistemas que actúan como servidores o para reducir el consumo de recursos.

---

## Recursos y Descargas

- [Ubuntu Desktop ISO](https://ubuntu.com/download/desktop)
- [Rufus](https://rufus.ie)
- [Cliente PuTTY para SSH](https://www.putty.org)
