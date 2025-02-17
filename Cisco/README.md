# 📡 Introducción a las Redes de Computadoras

## 🌐 ¿Qué es una Red de Computadoras?

Una **red de computadoras** es un conjunto de dispositivos interconectados que pueden compartir información y recursos. Su propósito principal es facilitar la comunicación y el acceso a servicios dentro de una organización o entre múltiples ubicaciones.

## 🔹 Tipos de Redes

- **LAN (Local Area Network)**: Red dentro de un área reducida (ej: oficina, hogar).
- **MAN (Metropolitan Area Network)**: Red que cubre una ciudad o región.
- **WAN (Wide Area Network)**: Red de gran alcance, interconectando múltiples LAN y MAN (ej: Internet).
- **WLAN (Wireless Local Area Network)**: Red LAN sin cables.
- **SAN (Storage Area Network)**: Red dedicada para almacenamiento de datos.
- **PAN (Personal Area Network)**: Red de dispositivos personales como Bluetooth.

## 🔹 Tipos de Direcciones IP

Las direcciones IP pueden clasificarse en diferentes tipos según su alcance y función:

- **Privadas**: Solo se usan dentro de redes locales y no pueden ser enrutadas en Internet.
  - Clase A: `10.0.0.0 – 10.255.255.255`
  - Clase B: `172.16.0.0 – 172.31.255.255`
  - Clase C: `192.168.0.0 – 192.168.255.255`

- **Públicas**: Son asignadas por proveedores de Internet y pueden ser accedidas globalmente.
- **Estáticas**: Se configuran manualmente y permanecen fijas en el dispositivo.
- **Dinámicas**: Son asignadas automáticamente mediante **DHCP**.
- **Loopback**: Direcciones reservadas como `127.0.0.1`, usadas para pruebas de red.
- **Broadcast**: Dirección utilizada para enviar mensajes a todos los dispositivos en una red (`192.168.1.255`).

## 🔹 Máscara de Red y Subnetting

Cada dirección IP va acompañada de una **máscara de red**, que define qué parte pertenece a la red y qué parte al host.

Ejemplo de una dirección IP con su máscara:
```plaintext
192.168.1.1 / 24 → Máscara: 255.255.255.0
```

- Un `/24` significa que los primeros 24 bits son de red y los 8 restantes pueden asignarse a hosts.
- Para segmentar una red en subredes más pequeñas, se emplea el **Subnetting**, que permite optimizar el uso de direcciones IP.
- Para determinar cuántos hosts por subred se pueden usar, se utiliza la fórmula:
  ```
  2^(bits de host) - 2
  ```

## 🔹 Full-Duplex y Half-Duplex

En redes, los dispositivos pueden operar en diferentes modos de transmisión:

- **Full-Duplex**: Permite la transmisión y recepción simultánea de datos, mejorando el rendimiento de la red.
- **Half-Duplex**: Solo permite la transmisión o recepción en un momento dado, lo que puede generar colisiones en la red.

## 🔹 NAT (Network Address Translation)

**NAT** traduce direcciones IP privadas a una IP pública para permitir el acceso a Internet. Existen diferentes tipos:

- **NAT Estática**: Asigna una IP pública fija a una IP privada.
- **NAT Dinámica**: Asigna direcciones IP públicas de un pool de direcciones disponibles.
- **PAT (Port Address Translation)**: Permite que múltiples dispositivos compartan una única IP pública utilizando diferentes puertos.

---

# 🏗️ Modelos de Referencia: OSI y TCP/IP

### 📜 Modelo OSI (Open Systems Interconnection)

El modelo OSI es una referencia conceptual de **7 capas** que define cómo se comunican los dispositivos en una red:

1. **Capa Física**: Maneja los cables, señales eléctricas y conectores.
2. **Capa de Enlace de Datos**: Garantiza la entrega confiable entre dispositivos adyacentes (Ej: Ethernet, Wi-Fi).
3. **Capa de Red**: Se encarga del direccionamiento y enrutamiento de paquetes (Ej: IP).
4. **Capa de Transporte**: Proporciona entrega confiable de datos mediante TCP o UDP.
5. **Capa de Sesión**: Administra sesiones de comunicación entre aplicaciones.
6. **Capa de Presentación**: Se encarga del cifrado, compresión y conversión de datos.
7. **Capa de Aplicación**: Interactúa con las aplicaciones del usuario (Ej: HTTP, DNS, FTP).

### 📜 Modelo TCP/IP

El modelo TCP/IP es una versión más práctica y simplificada:

1. **Capa de Acceso a la Red**: Equivalente a las capas física y de enlace de datos del modelo OSI.
2. **Capa de Internet**: Maneja el direccionamiento y enrutamiento de paquetes (Ej: IP, ICMP).
3. **Capa de Transporte**: Define la comunicación de extremo a extremo entre dispositivos (Ej: TCP, UDP).
4. **Capa de Aplicación**: Administra los protocolos de usuario como HTTP, FTP, SMTP.

---

# ⚙️ Configuración de Dispositivos en Cisco Packet Tracer

## 🌍 Configuración de un Switch

1. Ingresar al modo privilegiado:
```cisco
Switch> enable
```

2. Entrar en el modo de configuración global:
```cisco
Switch# configure terminal
```

3. Asignar un nombre al switch:
```cisco
Switch(config)# hostname Switch1
```

4. Configurar VLANs:
```cisco
Switch(config)# vlan 10
Switch(config-vlan)# name Ventas
```

## 🌍 Configuración de un Router

1. Ingresar al modo privilegiado:
```cisco
Router> enable
```

2. Entrar en el modo de configuración global:
```cisco
Router# configure terminal
```

3. Configurar una interfaz con una IP:
```cisco
Router(config)# interface GigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
```

4. Configurar NAT:
```cisco
Router(config)# ip nat inside source list 1 interface GigabitEthernet 0/0 overload
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
```

## 🌍 Configuración de un Hub (teórica)

Los hubs no tienen configuración en CLI, simplemente reenvían tráfico a todos los dispositivos conectados.

