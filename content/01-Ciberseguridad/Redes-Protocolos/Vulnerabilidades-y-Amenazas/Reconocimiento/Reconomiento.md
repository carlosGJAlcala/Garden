---
title: "Reconomiento"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Reconocimiento – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[01-Ciberseguridad/Herramientas/Nikto|Nikto]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Maltego|Maltego]].

El **reconocimiento** es la **primera fase en la cadena de un ataque estructurado**. Equivale a la “fase de inteligencia” en una operación militar: se recopila toda la información posible del objetivo antes de lanzar cualquier ataque activo. Esta etapa es crítica para minimizar riesgos y maximizar efectividad.

---

###  Objetivos del reconocimiento

1. **Valorar el interés del objetivo**: saber si merece la pena atacarlo.
    
2. **Descubrir vulnerabilidades**: identificar puntos débiles potenciales.
    
3. **Planificar el ataque**: preparar el enfoque más eficiente, silencioso y seguro.
    

> Analogía típica: si atacar un banco, el reconocimiento sería mirar planos, horarios, cámaras y entradas, **sin tocar aún nada**.

---

###  Subfases del reconocimiento

#### 1. **Footprinting** – Huellas externas

- Recolección pasiva: sin interactuar directamente con el objetivo.
    
- Fuentes:
    
    - Páginas web oficiales.
        
    - WHOIS: información del dominio, IPs, emails de contacto.
        
    - DNS: estructura de zonas, subdominios, registros públicos.
        
    - Búsquedas en Google, redes sociales, leaks y bases de datos públicas.
        

 _Objetivo:_ trazar un mapa de la red, saber qué está expuesto, nombres de hosts, emails, tecnologías utilizadas (CMS, lenguajes, etc.)

---

#### 2. **Scanning** – Sondeo activo

- Recolección activa: hay interacción con el objetivo (riesgo de ser detectado).
    
- Se comprueba:
    
    - Qué hosts están activos (`ping`, `nmap -sn`, `arp-scan`, etc.).
        
    - Qué puertos están abiertos (`nmap -sS`, `nmap -sU`).
        
    - Qué servicios están disponibles (`nc`, `nmap -sV`, `banner grabbing`).
        

 _Objetivo:_ identificar puertas de entrada: servicios inseguros, versiones antiguas, configuraciones débiles.

---

#### 3. **Enumeration** – Explotación de servicios para extraer información

- Interacción profunda con servicios descubiertos:
    
    - **Banner grabbing**: capturar encabezados que revelan versión del software.
        
    - **Enumeración de NetBIOS/SNMP/SMTP**: obtener nombres de usuarios, equipos, recursos compartidos.
        
    - **OS fingerprinting**: detectar el sistema operativo mediante firmas TCP/IP (como TTL o comportamiento de flags).
        

 _Objetivo:_ conseguir detalles internos que normalmente no serían públicos. Esto alimenta la búsqueda de vulnerabilidades específicas.

---

#### 4. **Vulnerability Mapping** – Mapeo de vulnerabilidades

- Con la información obtenida se:
    
    - Correlacionan servicios y versiones con bases de datos de vulnerabilidades conocidas (CVE, CERT, Bugtraq).
        
    - Se prueban herramientas automáticas como **OpenVAS**, **Nessus**, **Nikto**, etc.
        
    - Se prueban exploits manuales o se desarrollan propios.
        

 _Objetivo:_ preparar el exploit exacto para la siguiente fase (acceso remoto).

---

### ️ Medidas defensivas ante reconocimiento

1. **Reducir la superficie expuesta**:
    
    - Ocultar información sensible de la web y WHOIS.
        
    - Desactivar servicios innecesarios.
        
    - Segregar DNS público e interno.
        
2. **Limitar el escaneo**:
    
    - Firewalls que bloqueen ICMP, puertos no utilizados, SYNs sospechosos.
        
    - Segmentación de red (zonas DMZ, VLANs).
        
    - Usar NAT para ocultar estructura interna.
        
3. **Detectar intentos de reconocimiento**:
    
    - IDS (como Snort, Suricata) para escaneos.
        
    - HIDS (scanlogd, OSSEC) para ataques en sistemas.
        
    - Honeypots para atraer y registrar comportamiento del atacante.
        

---

###  Herramientas comunes en reconocimiento

|Fase|Herramientas comunes|
|---|---|
|Footprinting|Google, Whois, nslookup, theHarvester, Maltego|
|Scanning|nmap, Masscan, Netcat, hping|
|Enumeration|enum4linux, SNMPwalk, Telnet, FTP, nmap -sV|
|Vuln. mapping|Nessus, OpenVAS, Nikto, Searchsploit, ExploitDB|

---

### Conclusión

El **reconocimiento es silencioso, crítico y muchas veces subestimado**. Un atacante experto puede invertir más tiempo en esta fase que en lanzar el ataque en sí. Del mismo modo, un buen defensor puede detectar y bloquear una intrusión antes de que comience, si sabe reconocer las señales de exploración y limitar la exposición de la red.

---

¿Quieres que te prepare una guía práctica de reconocimiento paso a paso con herramientas reales o con ejemplos específicos en un entorno de laboratorio?