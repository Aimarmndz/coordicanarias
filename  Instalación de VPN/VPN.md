# Instalación y Configuración de WireGuard en Ubuntu Server y Cliente Windows

## Instalación de WireGuard en Ubuntu Server

### 1. Instalar el paquete WireGuard
```bash
sudo apt update && sudo apt install -y wireguard
```

### 2. Generar claves privadas y públicas para el servidor
```bash
wg genkey | tee /etc/wireguard/server_private.key | wg pubkey > /etc/wireguard/server_public.key
```
```bash
chmod 600 /etc/wireguard/server_private.key
```

### 3. Configurar el archivo de configuración del servidor
Crear el archivo `/etc/wireguard/wg0.conf` y añadir:
```ini
[Interface]
PrivateKey = <clave_privada_del_servidor>
Address = 10.0.0.1/24
ListenPort = 51820
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o ens18 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o ens18 -j MASQUERADE
SaveConfig = true
```

### 4. Habilitar el reenvío de IPs
```bash
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### 5. Configurar iptables para permitir tráfico de VPN
```bash
sudo iptables -A INPUT -p udp --dport 51820 -j ACCEPT
sudo iptables -A FORWARD -i wg0 -j ACCEPT
sudo iptables -A FORWARD -o wg0 -j ACCEPT
```

### 6. Asegurar la persistencia de reglas de iptables
```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

### 7. Habilitar y arrancar WireGuard
```bash
sudo systemctl enable wg-quick@wg0
sudo systemctl start wg-quick@wg0
```

---

## Instalación y Configuración del Cliente WireGuard en Windows

### 1. Instalar la interfaz gráfica de WireGuard
Descargar e instalar desde: [WireGuard](https://www.wireguard.com/install/)

### 2. Generar claves privadas y públicas del cliente
Al crear un nuevo túnel en WireGuard, se nos genera automáticamente las claves necesarias, aunque tambíen podemos usar PowerShell:

```powershell
wg genkey | Out-File -Encoding ascii client_private.key; Get-Content client_private.key | wg pubkey
```

### 3. Configurar el archivo del cliente
Abrir WireGuard y cponer la siguienteconfiguración:
```ini
[Interface]
PrivateKey = <clave_privada_del_cliente>
Address = 10.0.0.2/24
DNS = 8.8.8.8

[Peer]
PublicKey = <clave_publica_del_servidor>
Endpoint = <IP_Publica_Servidor>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```

Guardamos y reinciamos el servicio:
```bash 
sudo systemctl restart wg-quick@wg0
```

### 4. Conectar el cliente al servidor
Abrir la aplicación WireGuard y activar la conexión.

---

## Redirección de Puertos en el Router
Para poder salir a internet, debemos activar los puertos en el router.

### 1. Configurar el reenvío de puertos
Ingresar al router y añadir una regla para:
- Protocolo: UDP
- Puerto externo: 51820
- IP destino: Dirección IP local del servidor
- Puerto interno: 51820

### 2. Verificar que el puerto está abierto
```bash
nc -zv <IP_Publica_Servidor> 51820
```

---

## Solución de Problemas
Comandos que pueden ser utiles a la hora de solucionar problemas en el proceso de instalación.

### 1. Verificar que WireGuard está corriendo
```bash
sudo systemctl status wg-quick@wg0
```

### 2. Comprobar el reenvío de paquetes
```bash
sysctl net.ipv4.ip_forward
```
Debe devolver `net.ipv4.ip_forward = 1`

### 3. Revisar reglas de iptables
```bash
sudo iptables -L -v -n
```

### 4. Verificar conexión desde el cliente
```powershell
ping 10.0.0.1
tracert 8.8.8.8
```
Si falla, revisar la configuración `AllowedIPs` en el cliente y servidor.

### 5. Log
```bash
sudo journalctl -u wg-quick@wg0 --no-pager | tail -20
```

