---
title: "Port Scanning"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Port Scanning – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Reconocimiento/Scanning|Scanning]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

**Port scanning** (escaneo de puertos) es una técnica de reconocimiento activo utilizada para **detectar qué puertos están abiertos en un sistema y qué servicios los están usando**. Es una fase fundamental tanto en **ciberataques** como en **auditorías de seguridad** y pruebas de penetración.

Los puertos representan **puertas de entrada** al sistema. Si una está abierta y expone un servicio vulnerable (por ejemplo, FTP sin autenticación), puede convertirse en el punto de entrada de un ataque.

---

### ¿Qué es un puerto?

- En una máquina con IP, los **puertos (0–65535)** permiten que múltiples servicios escuchen en paralelo.
    
- Los protocolos como TCP y UDP utilizan estos puertos para multiplexar comunicaciones.
    

|Rango de puertos|Tipo|Ejemplos|
|---|---|---|
|0–1023|Bien conocidos|22 (SSH), 80 (HTTP), 443 (HTTPS)|
|1024–49151|Registrados|3306 (MySQL), 3389 (RDP)|
|49152–65535|Dinámicos/efímeros|Asignados temporalmente|

---

### Objetivos del escaneo de puertos

- Identificar puertos **abiertos** (accepting connections).
    
- Determinar **servicios en ejecución**.
    
- Verificar **versiones del software**.
    
- Evaluar la **exposición** del sistema.
    
- Descubrir posibles vectores de ataque.
    

---

###  Tipos de escaneo de puertos

|Tipo de escaneo|Descripción|
|---|---|
|**TCP Connect (`-sT`)**|Completa la conexión (3-way handshake). Fácil de detectar, pero fiable.|
|**TCP SYN (`-sS`)**|Envía solo el paquete SYN (half-open scan). Menos detectable.|
|**UDP (`-sU`)**|Envía paquetes UDP. Difícil de interpretar (muchos puertos UDP no responden).|
|**NULL, FIN, Xmas (`-sN/-sF/-sX`)**|Manipulan flags TCP para evadir detección o firewalls. Útiles contra sistemas sin stack TCP estricto.|
|**ACK scan (`-sA`)**|Detecta reglas de firewall o filtrado de puertos.|
|**Window scan (`-sW`)**|Variante del ACK para sistemas Windows antiguos.|

---

###  Herramientas comunes para escaneo de puertos

| Herramienta     | Características principales                                     |
| --------------- | --------------------------------------------------------------- |
| **Nmap**        | Herramienta más usada. Potente, versátil, con motor de scripts. |
| **Netcat (nc)** | Para verificar puertos manualmente.                             |
| **Masscan**     | Escaneo muy rápido de rangos grandes (hasta millones de IPs).   |
| **Hping**       | Escaneo de puertos y manipulación de paquetes TCP/IP.           |
| **Unicornscan** | Escaneo avanzado de red y fingerprinting.                       |

---

###  Ejemplo práctico con Nmap

```bash
nmap -sS -p 1-1000 -T4 -v 192.168.1.100
```

- `-sS`: escaneo SYN
    
- `-p 1-1000`: puertos del 1 al 1000
    
- `-T4`: velocidad agresiva
    
- `-v`: modo verbose
    

> Salida típica:

```text
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
139/tcp  closed netbios-ssn
445/tcp  filtered microsoft-ds
```

---

### ️ Posibles resultados del escaneo

|Estado|Significado|
|---|---|
|**open**|El puerto está abierto y responde. Hay un servicio escuchando.|
|**closed**|El puerto está accesible, pero no hay servicio activo.|
|**filtered**|No se puede saber si está abierto o cerrado; puede haber un firewall bloqueando la conexión.|
|**unfiltered**|El puerto está accesible, pero no se puede determinar su estado.|
|**open|filtered**|

---

### ️ Medidas defensivas contra escaneo de puertos

1. **Firewalls y ACLs**:
    
    - Bloquear puertos innecesarios.
        
    - Usar reglas de filtrado estrictas.
        
    - Detectar y bloquear patrones de escaneo.
        
2. **IDS/IPS (Intrusion Detection/Prevention Systems)**:
    
    - Herramientas como Snort o Suricata pueden detectar escaneos SYN, NULL, XMAS…
        
3. **Port knocking / servicios detrás de VPN**:
    
    - Abrir puertos solo cuando se recibe una secuencia secreta de paquetes.
        
4. **Rate limiting y conexión inversa**:
    
    - Limitar el número de intentos de conexión.
        
    - Invertir la conexión para proteger servicios internos.
        
5. **Honeypots**:
    
    - Simular puertos abiertos para atraer escaneos y obtener inteligencia del atacante.
        

---

###  Técnicas ofensivas adicionales

- **Escaneo de puertos encubierto (slow scan)**:
    
    - Se realiza a ritmo muy lento para evitar ser detectado (`nmap -T0`).
        
- **Uso de puertos inusuales**:
    
    - Algunos servicios se configuran en puertos no estándar (por ejemplo, SSH en 2222).
        
- **Escaneo inverso desde sistemas comprometidos**:
    
    - Desde dentro de la red para evitar el firewall perimetral.
        

---

### Conclusión

El **escaneo de puertos es una técnica sencilla pero poderosa**. Bien utilizada, permite construir un mapa detallado de servicios expuestos y posibles puntos de entrada. Por eso mismo, **es una de las actividades más vigiladas** por defensores. Su comprensión es esencial tanto para auditores como para atacantes éticos o maliciosos.

---
### Port Scanning con Netcat (nc) – Nota expandida

**Netcat** (o `nc`) es una herramienta de red sencilla pero extremadamente poderosa. Es conocida como el "cuchillo suizo" de la red, y aunque no fue diseñada exclusivamente para escanear puertos, **puede usarse para hacer port scanning básico**, además de muchas otras tareas (transferencia de archivos, backdoors, shells inversas, etc.).

---

###  ¿Para qué usar Netcat en port scanning?

Aunque `nmap` es la herramienta más completa para escaneo de puertos, `netcat` es útil cuando:

- Quieres escanear rápidamente un pequeño rango de puertos.
    
- Trabajas en un sistema muy limitado o sin herramientas avanzadas.
    
- Necesitas **no llamar la atención** (por ejemplo, si `nmap` es detectado).
    

---

### ️ Sintaxis básica para escaneo de puertos con Netcat

```bash
nc -zv <IP_objetivo> <puerto(s)>
```

- `-z`: modo "zero I/O" (no envía datos, solo comprueba si el puerto está abierto).
    
- `-v`: modo verbose, muestra los resultados.
    
- Se pueden escanear rangos con `{}` o guiones `-`.
    

---

###  Ejemplos de uso

#### 1. Escanear un único puerto

```bash
nc -zv 192.168.1.10 22
```

> Verifica si el puerto SSH está abierto.

---

#### 2. Escanear varios puertos

```bash
nc -zv 192.168.1.10 22 80 443
```

> Revisa SSH, HTTP y HTTPS.

---

#### 3. Escanear un rango de puertos

```bash
nc -zv 192.168.1.10 1-1000
```

> Escanea los primeros 1000 puertos TCP del host.

---

#### 4. Escaneo UDP (no disponible en todas las versiones)

Algunas versiones de Netcat (como **ncat** de Nmap o GNU Netcat) permiten escaneo UDP con `-u`, pero no todas lo soportan:

```bash
nc -zvu 192.168.1.10 53
```

> Verifica si el puerto DNS (UDP 53) está abierto.

---

###  Salida típica de Netcat

```text
Connection to 192.168.1.10 22 port [tcp/ssh] succeeded!
nc: connect to 192.168.1.10 21 (port 21) failed: Connection refused
```

- **"succeeded!"** → puerto abierto.
    
- **"Connection refused"** → puerto cerrado.
    
- **Sin respuesta** → puede estar filtrado o bloqueado por firewall.
    

---

###  Consideraciones de seguridad

#### Desde el punto de vista ofensivo:

- `nc` es **discreto** y puede usarse en situaciones donde `nmap` es detectado por IDS.
    
- Muy útil en sistemas comprometidos donde no se quiere instalar software.
    

#### Desde el punto de vista defensivo:

- Se debe monitorizar conexiones anómalas a múltiples puertos.
    
- IDS como **Snort** pueden detectar intentos de escaneo con `nc` si no se ocultan correctamente.
    

---

###  Limitaciones de Netcat como port scanner

|Limitación|Implicación|
|---|---|
|No detecta versiones de servicios|A diferencia de `nmap -sV`|
|Sin técnicas evasivas|Fácil de detectar|
|Sin soporte para scripting|No extensible sin herramientas extra|
|No maneja respuestas complejas|Solo detecta si el puerto responde|

---

###  Alternativa más avanzada: Nmap con Netcat integrado

Si necesitas un escaneo más avanzado, puedes usar `nmap` y luego interactuar manualmente con un puerto abierto usando `nc`, por ejemplo:

```bash
nc 192.168.1.10 80
GET / HTTP/1.1
Host: 192.168.1.10
```

> Esto permite analizar respuestas HTTP manualmente.

---

### Conclusión

`Netcat` es una herramienta **sencilla pero eficaz** para realizar escaneos de puertos rápidos y discretos, ideal para situaciones donde otras herramientas no están disponibles. Aunque no sustituye a `nmap` en capacidades, es una gran opción en entornos limitados o para pruebas específicas.

---