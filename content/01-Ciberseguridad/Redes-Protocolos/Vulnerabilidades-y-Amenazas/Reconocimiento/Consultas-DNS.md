---
title: "Consultas Dns"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Consultas DNS – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/ZEEK|ZEEK]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

Las **consultas DNS** (Domain Name System) son el mecanismo mediante el cual un cliente solicita información a servidores DNS para resolver un nombre de dominio en una dirección IP (y viceversa). Estas consultas son **la base del acceso a servicios en Internet**, y su análisis es clave tanto para atacantes como para defensores en ciberseguridad.

---

###  ¿Qué es una consulta DNS?

Cuando escribes `www.ejemplo.com` en tu navegador:

1. El **resolver DNS local** (generalmente proporcionado por tu ISP o red corporativa) consulta si ya tiene esa información en caché.
    
2. Si no, contacta con los servidores DNS jerárquicos:
    
    - **Raíz (root servers)**
        
    - **TLD** (`.com`, `.org`, `.es`…)
        
    - **Autoritativo** del dominio (`ejemplo.com`)
        

Cada uno responde con información parcial hasta que se obtiene la **dirección IP del dominio solicitado**.

---

### ️ Tipos de consultas DNS

|Tipo de consulta|Descripción|
|---|---|
|**Recursiva**|El resolver local realiza todas las consultas necesarias y devuelve la respuesta completa al cliente.|
|**Iterativa**|Cada servidor DNS devuelve la mejor respuesta que conoce (por ejemplo, el siguiente servidor a consultar).|
|**Inversa (PTR)**|Consulta que traduce una dirección IP en un nombre de dominio (resolución inversa).|

---

###  Tipos de registros DNS comunes

- `A`: dirección IPv4
    
- `AAAA`: dirección IPv6
    
- `MX`: servidor de correo
    
- `NS`: servidores de nombres
    
- `CNAME`: alias de otro nombre
    
- `PTR`: resolución inversa (IP → nombre)
    
- `TXT`: datos arbitrarios (SPF, DKIM, verificación)
    

---

###  Herramientas para realizar consultas DNS

#### Línea de comandos (CLI)

1. **nslookup** (Windows/Linux):
    

```bash
nslookup www.ejemplo.com
nslookup -type=MX ejemplo.com
```

2. **dig** (Linux, más completo):
    

```bash
dig www.ejemplo.com
dig +short ejemplo.com MX
dig -x 192.168.1.1  # resolución inversa
```

3. **host** (Linux/macOS):
    

```bash
host www.ejemplo.com
```

---

### ️ Riesgos de seguridad en las consultas DNS

#### 1. **Transferencias de zona (Zone Transfer)**

- Si un servidor DNS está mal configurado, puede permitir transferencias completas de la zona DNS (`AXFR`).
    
- Esto expone todos los nombres de hosts internos o servicios.
    

```bash
dig @dns.ejemplo.com ejemplo.com AXFR
```

#### 2. **DNS cache poisoning**

- Un atacante inyecta respuestas DNS falsas en la caché del resolver.
    
- Resultado: redirección de tráfico a servidores maliciosos.
    

#### 3. **DNS Hijacking**

- Manipulación del tráfico DNS en el camino (por parte de ISPs, gobiernos o malware).
    
- El cliente recibe IPs falsas sin saberlo.
    

#### 4. **Exposición de consultas (privacidad)**

- Las consultas DNS tradicionales (UDP/53) **no están cifradas**.
    
- Pueden ser espiadas, modificadas o redirigidas en redes públicas o por atacantes MITM.
    

---

### ️ Mecanismos de defensa

1. **DNSSEC**
    
    - Verifica la **integridad y autenticidad** de las respuestas DNS mediante firmas digitales.
        
    - Evita cache poisoning, pero no cifra el tráfico.
        
2. **DoT (DNS over TLS)** y **DoH (DNS over HTTPS)**
    
    - **Cifran las consultas DNS** entre cliente y resolver.
        
    - DoH oculta las consultas dentro del tráfico HTTPS habitual (puerto 443).
        
    - Usado por navegadores modernos (Firefox, Chrome) y servicios como Cloudflare (1.1.1.1), Google (8.8.8.8), Quad9.
        
3. **Separación DNS interno y externo**
    
    - En redes corporativas, usar servidores DNS distintos para servicios internos y públicos.
        
    - Impedir que información sensible (por ejemplo, nombres de máquinas) sea accesible desde fuera.
        
4. **Evitar transferencias AXFR abiertas**
    
    - Restringirlas solo a servidores secundarios autorizados.
        
    - Comprobar configuración en BIND, Windows DNS, etc.
        
5. **Monitorización de consultas DNS**
    
    - Detección de comportamiento anómalo (exfiltración de datos, C2, beaconing, tunneling).
        
    - Uso de herramientas como **Zeek (Bro)**, **Security Onion**, **Splunk**, **Sysmon + DNS logging**.
        

---

###  Casos de uso ofensivos (pentesting / ciberataques)

- Obtener subdominios: `sub.ejemplo.com`, `mail.ejemplo.com`, `vpn.ejemplo.com`.
    
- Identificar tecnologías y estructuras internas.
    
- Detección de emails corporativos para campañas de phishing.
    
- Explotación de resoluciones incorrectas, dominios typosquatted o mal configurados.
    

---

###  Ejemplo de consulta maliciosa (zona mal configurada)

```bash
dig @dns.objetivo.com objetivo.com AXFR
```

 _Resultado:_ lista completa de todos los subdominios y registros DNS → útil para enumeración y detección de servicios vulnerables.

---

### Conclusión

Las **consultas DNS son esenciales para el funcionamiento de Internet**, pero también pueden ser utilizadas como vector de ataque, fuga de información o canal encubierto de comunicación. Por ello, tanto en tareas de pentesting como en defensa, **entender y controlar el tráfico DNS es una prioridad crítica**.

---

¿Quieres que te prepare ejemplos de prácticas ofensivas (enumeración de subdominios o uso de dig/nslookup) o defensivas (configurar DNSSEC o monitorización)?