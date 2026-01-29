---
title: "Pfsense"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---


**pfSense** es un firewall y router de código abierto basado en **FreeBSD** que proporciona una solución de seguridad avanzada para redes empresariales y domésticas. Es altamente configurable e incluye funciones como **VPN, IDS/IPS, balanceo de carga, alta disponibilidad y portal cautivo**.

---

## **1. Características Principales de pfSense**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Hydra|Hydra]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

### **1️⃣ Firewall y NAT**

- Controla el tráfico de red mediante reglas de filtrado avanzadas.
- Soporta **Alias** para facilitar la gestión de reglas de firewall.
- Incluye NAT (Network Address Translation) para redes internas.

### **2️⃣ IDS/IPS Integrado (Snort y Suricata)**

- **Snort y Suricata** pueden activarse en pfSense para detectar y prevenir ataques.
- Permite configurar listas de bloqueo y análisis de paquetes en tiempo real.

### **3️⃣ VPN (IPsec, OpenVPN, WireGuard)**

- Soporta VPNs para conexiones seguras entre redes o accesos remotos.
- Compatible con **IPsec, OpenVPN y WireGuard**.

### **4️⃣ Portal Cautivo**

- Permite controlar el acceso a la red mediante autenticación web.
- Ideal para redes públicas, hoteles y empresas con acceso restringido.

### **5️⃣ Balanceo de Carga y Alta Disponibilidad (HA)**

- Soporta **CARP (Common Address Redundancy Protocol)** para failover automático.
- Puede distribuir el tráfico entre múltiples conexiones WAN.

### **6️⃣ Bloqueo de IPs con pfBlockerNG**

- Permite bloquear tráfico no deseado mediante listas negras.
- Filtra contenido basado en geolocalización y reputación de IPs.

---

## **2. Seguridad en pfSense**

### **1️⃣ Usuario y Contraseña por Defecto**

El usuario por defecto es:

- **Usuario:** `admin`
- **Contraseña:** `pfsense` (aunque puede cambiar en versiones recientes)

Para verificar la contraseña por defecto en un ataque, se pueden probar listas de credenciales por defecto con herramientas como `hydra`:

```bash
hydra -l admin -P rockyou.txt 192.168.1.1 http-post-form "/index.php:username=^USER^&password=^PASS^:F=incorrect"
```

Esto intentará hacer fuerza bruta sobre el login de pfSense.

### **2️⃣ Protección contra ataques**

- Es recomendable cambiar la contraseña de administrador inmediatamente.
- Configurar reglas estrictas de acceso al **puerto 443 o 80** si la interfaz web está expuesta.
- Habilitar **2FA** para mayor seguridad.

---

## **3. Administración y Buenas Prácticas**

### **1️⃣ Uso de Alias en las Reglas de Firewall**

- Permiten **agrupar direcciones IP, redes o puertos** con nombres amigables.
- Si un alias cambia, se actualiza en todas las reglas automáticamente.

Ejemplo:

- Alias `RED_EMPRESA = 192.168.1.0/24`
- Reglas usando `RED_EMPRESA` en lugar de escribir la subred manualmente.

### **2️⃣ Monitoreo y Registro de Eventos**

- pfSense permite exportar logs a un **SIEM como Splunk o ELK**.
- Se puede habilitar **NetFlow o Syslog** para auditoría avanzada.

---

## **4. Conclusión**

pfSense es un **firewall de última generación** que combina funcionalidades avanzadas de seguridad con flexibilidad y facilidad de gestión. Su integración con **Snort, Suricata, VPNs y portal cautivo** lo convierte en una solución ideal para proteger redes. **Configurar adecuadamente reglas de firewall, cambiar credenciales por defecto y usar alias son prácticas clave para mantener la seguridad**.