---
title: "Scanning"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Scanning – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/ZEEK|ZEEK]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ZMap|ZMap]].

**Scanning** es la segunda subfase del reconocimiento activo en un ataque, tras el **footprinting**. Consiste en **interactuar directamente con los sistemas objetivos** para identificar qué dispositivos están activos, qué servicios ofrecen y cómo están configurados. Su objetivo es **detectar vectores de entrada** potenciales.

Es una fase fundamental tanto en **ciberataques ofensivos** como en **auditorías de seguridad o pentesting**.

---

###  Objetivos del scanning

- Identificar **hosts activos**.
    
- Detectar **puertos abiertos**.
    
- Determinar **servicios activos y versiones**.
    
- Obtener información adicional como sistema operativo, configuración de red, firewalls o IDS.
    
- Determinar si el sistema es vulnerable a ataques específicos.
    

---

###  Tipos de scanning

#### 1. **Host Discovery (Ping sweep)**

Detectar qué máquinas están activas en una red.

- Herramientas:
    
    - `nmap -sn 192.168.1.0/24`
        
    - `ping`, `arp-scan`, `fping`
        

> A menudo bloqueado por firewalls, por lo que se utilizan técnicas alternativas (como enviar SYN o paquetes UDP a puertos comunes).

---

#### 2. **Port Scanning**

Enumerar los **puertos abiertos**, y por tanto, los servicios activos en un host.

##### Tipos de escaneo:

- **TCP connect scan**: establece conexión completa (SYN → SYN/ACK → ACK). Más detectable.
    
    ```bash
    nmap -sT 192.168.1.1
    ```
    
- **SYN scan (Stealth scan)**: envía solo SYN, no completa la conexión.
    
    ```bash
    nmap -sS 192.168.1.1
    ```
    
- **UDP scan**: escanea puertos UDP (más lento y menos fiable).
    
    ```bash
    nmap -sU 192.168.1.1
    ```
    
- **Xmas, Null, FIN scans**: pruebas con flags TCP inusuales para evadir detección.
    
    ```bash
    nmap -sX 192.168.1.1
    ```
    

>  Los puertos comunes incluyen: 22 (SSH), 80 (HTTP), 443 (HTTPS), 21 (FTP), 25 (SMTP), 53 (DNS), 3389 (RDP), etc.

---

#### 3. **Service/version detection**

Identificar qué servicios se ejecutan en los puertos y qué versiones exactas.

```bash
nmap -sV 192.168.1.1
```

- Esto permite al atacante buscar vulnerabilidades específicas (CVE) de esas versiones.
    

---

#### 4. **OS Detection**

Descubre qué sistema operativo usa un host analizando características del stack TCP/IP.

```bash
nmap -O 192.168.1.1
```

- Se basa en TTL, tamaño de ventana, flags, etc.
    
- Puede combinarse con fingerprinting activo o pasivo.
    

---

### ️ Herramientas de scanning

|Herramienta|Descripción|
|---|---|
|**Nmap**|Estándar de facto para scanning. Soporta escaneos de red, detección de OS, scripts NSE|
|**Masscan**|Mucho más rápido que Nmap (hasta millones de paquetes/segundo), pero más básico|
|**Netcat (nc)**|Herramienta de bajo nivel para probar puertos TCP/UDP manualmente|
|**Zmap**|Escaneos de Internet a gran escala|
|**Hping**|Escaneo personalizado basado en TCP/IP|
|**Angry IP Scanner**|GUI para ping sweep y escaneo simple|

---

### ️ Riesgos y consideraciones éticas

- **Los escaneos pueden ser detectados** por sistemas IDS/IPS.
    
- **Pueden generar alertas legales o de seguridad** si se hacen sin permiso.
    
- En entornos corporativos, deben realizarse desde entornos controlados y con autorización.
    

---

### ️ Contramedidas y detección

1. **Firewalls bien configurados**:
    
    - Bloquear puertos innecesarios.
        
    - Filtrar paquetes SYN no válidos o sin ACK.
        
    - Filtrar ICMP para evitar ping sweep.
        
2. **Honeypots**:
    
    - Capturan y alertan ante escaneos y comportamientos sospechosos.
        
3. **IDS/IPS**:
    
    - Sistemas como Snort, Suricata, Zeek pueden detectar patrones de escaneo.
        
    - Alertan si un host realiza múltiples conexiones sospechosas en poco tiempo.
        
4. **Herramientas de detección local**:
    
    - `scanlogd`, `PortSentry`, `OSSEC`.
        

---

###  Ejemplo real: escaneo típico con Nmap

```bash
nmap -sS -sV -O -T4 -p 1-1000 192.168.1.10
```

- `-sS`: SYN scan
    
- `-sV`: detectar versión de los servicios
    
- `-O`: detectar sistema operativo
    
- `-T4`: velocidad agresiva
    
- `-p 1-1000`: puertos del 1 al 1000
    

 Resultado: qué servicios hay activos, qué versiones, qué sistema operativo y si hay posibles vulnerabilidades.

---

### Conclusión

El **scanning es una de las fases más críticas del reconocimiento activo**. Permite construir un mapa completo de los servicios expuestos y es la antesala para lanzar exploits. Al mismo tiempo, es una de las fases **más detectables**, por lo que también es clave para establecer **mecanismos de defensa temprana**.

---

¿Quieres que te prepare una guía práctica paso a paso con `nmap`, `masscan`, y detección de escaneos en Wireshark o Snort?