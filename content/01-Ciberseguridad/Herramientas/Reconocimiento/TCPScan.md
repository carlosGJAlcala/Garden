---
title: "Tcpscan"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  TCPScan (Tc)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ZMap|ZMap]].

- **Nombre en la tabla:** **TCPScan**
    
- **Símbolo:** **Tc**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Técnica o herramienta de escaneo de puertos TCP
    
- **Clasificación:** Escaneo de red – análisis de puertos abiertos
    

---

##  ¿Qué es TCPScan?

**TCPScan** hace referencia al **escaneo de puertos TCP**, una de las técnicas más comunes y fundamentales en la fase de reconocimiento de una prueba de penetración o auditoría de seguridad. Se utiliza para descubrir qué servicios están activos en un sistema, evaluando qué puertos TCP están abiertos y potencialmente expuestos a Internet o a una red interna.

Aunque en la tabla se presenta como un "elemento", en realidad no es una herramienta específica como Nmap o Masscan, sino una **técnica de escaneo**, generalmente implementada dentro de herramientas como:

- **Nmap** (`-sT` para TCP connect scan o `-sS` para TCP SYN scan).
    
- **Masscan** (para escaneo rápido de grandes redes).
    
- **Hping3** (para escaneo manual y personalizado de puertos).
    
- **Zmap** (cuando se busca escanear rangos inmensos).
    

---

##  Fundamentos del escaneo TCP

El **protocolo TCP** (Transmission Control Protocol) establece conexiones fiables mediante un **handshake de tres pasos** (SYN, SYN-ACK, ACK). Las técnicas de escaneo TCP aprovechan esta característica para detectar la respuesta del servidor en función del estado del puerto:

|Estado del puerto|Comportamiento del host|Interpretación|
|---|---|---|
|`SYN → SYN-ACK → RST`|El puerto está **abierto**.|Activo|
|`SYN → RST`|El puerto está **cerrado**.|Inaccesible|
|Sin respuesta|El puerto está **filtrado** (firewall).|Posible filtro|

---

##  Tipos comunes de escaneo TCP

1. **TCP Connect Scan (`-sT`)**  
    Utiliza el stack TCP del sistema operativo y realiza el handshake completo. Detectable por el sistema objetivo.  
     Ideal cuando no tienes privilegios de root.
    
2. **TCP SYN Scan (`-sS`)**  
    Envía solo el primer paquete SYN. Si recibe un SYN-ACK, responde con RST (no completa la conexión).  
     Requiere privilegios de root, es más sigiloso (stealthy) y menos detectable.
    
3. **TCP FIN/XMAS/NULL Scans**  
    Escaneos más evasivos que violan la especificación estándar de TCP. Algunos firewalls los dejan pasar.
    
4. **Custom TCP Scans con hping3**  
    Puedes enviar paquetes TCP personalizados a cualquier puerto y ver cómo responde el host.
    

---

##  Ejemplo con Nmap

```bash
nmap -sS -p 1-1000 192.168.1.10
```

- `-sS`: escaneo TCP SYN (sigiloso)
    
- `-p 1-1000`: puertos del 1 al 1000
    
- `192.168.1.10`: objetivo
    

Ejemplo de output:

```
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
443/tcp  closed https
```

---

##  Implicaciones de Seguridad

- Un puerto **TCP abierto** indica que un **servicio está escuchando**, lo que puede ser un punto de entrada para un atacante.
    
- El reconocimiento de puertos permite inferir el **tipo de sistema operativo**, servicios y versiones, abriendo camino a la enumeración y explotación.
    
- Un escaneo excesivo sin autorización puede activar sistemas IDS/IPS, como Snort o Suricata.
    

---

##  Herramientas compatibles con TCPScan

|Herramienta|Soporte para TCPScan|Características destacadas|
|---|---|---|
|Nmap||Precisión, fingerprinting, scripts NSE|
|Masscan||Velocidad extrema, escaneos masivos|
|Hping3||Escaneo TCP personalizado|
|Zmap||Escaneos masivos de una sola dirección IP|
|Netcat|️|Conexión a puertos TCP manualmente|

---

##  Integración en un proceso de pentesting

1. **Fase de descubrimiento:** identificar hosts activos.
    
2. **Escaneo TCP:** detectar puertos abiertos.
    
3. **Enumeración de servicios:** identificar versiones de software.
    
4. **Explotación o validación:** buscar vulnerabilidades en los servicios detectados.
    

---

##  Buenas prácticas

- Utiliza escaneos progresivos: primero SYN scan (`-sS`), luego escaneos más específicos.
    
- Acompaña el escaneo con detección de versión: `nmap -sS -sV`.
    
- Respeta la legalidad: **nunca escanees sistemas sin autorización expresa**.
    
- Usa scripts NSE (`--script`) en Nmap para profundizar en los servicios abiertos.
    

---

¿Deseas un **script de escaneo automatizado** para TCP en un rango de IPs? ¿O prefieres ejemplos de cómo usar TCPScan en contextos reales de Red Team y Blue Team?