---
title: "Naabu"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Naabu (na)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Reconocimiento/Scanning|Scanning]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]].

- **Nombre completo:** **Naabu**
    
- **Símbolo:** **na**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de escaneo de puertos TCP
    
- **Desarrollador:** [ProjectDiscovery](https://github.com/projectdiscovery/naabu)
    
- **Repositorio oficial:** [https://github.com/projectdiscovery/naabu](https://github.com/projectdiscovery/naabu)
    

---

##  ¿Qué es Naabu?

**Naabu** es una herramienta de escaneo de puertos **rápida, ligera y escrita en Go**, que permite realizar **port scanning TCP** sobre grandes rangos de IPs o dominios, centrándose en rendimiento y simplicidad. Fue creada por el equipo de **ProjectDiscovery**, conocido por herramientas como **Nuclei**, **Subfinder** o **HTTPX**, y está diseñada para integrarse fácilmente en pipelines de reconocimiento automático y OSINT.

---

##  ¿Para qué sirve Naabu?

Naabu se utiliza principalmente para:

- Detectar **puertos abiertos TCP** en una o múltiples IPs/domínios.
    
- Realizar escaneos masivos de forma **rápida y silenciosa**.
    
- Integrarse con otras herramientas para descubrimiento y enumeración de servicios.
    
- **Automatizar la fase de descubrimiento de superficie de ataque** en entornos reales o simulados.
    

---

## ️ Funcionalidades principales

-  **Multihilo por defecto**, permitiendo escaneos en paralelo.
    
- 🪄 Soporta **input desde archivos** o stdin (ideal para pipelines).
    
-  **Retry automático** y control de timeout.
    
-  Compatible con **rangos CIDR**, IPs sueltas o listas completas.
    
-  Soporte para escaneos stealthy: evita detección o bloqueo.
    
-  Exportación en múltiples formatos (`stdout`, JSON, archivo).
    
-  Totalmente integrable con **Subfinder, HTTPX, Nuclei, etc.**
    

---

##  Ejemplos de uso

###  Escaneo básico de puertos comunes en una IP

```bash
naabu -host 192.168.1.1
```

Escaneará los puertos comunes predefinidos en la herramienta.

---

###  Escaneo de puertos específicos

```bash
naabu -host 10.10.10.10 -p 80,443,8080,8443
```

Escaneo solo de los puertos 80, 443, 8080 y 8443.

---

###  Escaneo de todo el rango TCP (1-65535)

```bash
naabu -host 192.168.0.1 -p -  # el guión representa todos los puertos
```

---

###  Escaneo desde una lista de hosts (dominios o IPs)

```bash
naabu -list targets.txt
```

---

###  Salida en formato JSON

```bash
naabu -host 192.168.0.1 -json -o salida.json
```

---

###  Integración en pipelines con otras herramientas

```bash
subfinder -d ejemplo.com | naabu -p 80,443 | httpx
```

Este pipeline:

1. Encuentra subdominios con `subfinder`.
    
2. Escanea puertos web con `naabu`.
    
3. Lanza `httpx` para enumerar tecnologías, título, status code, etc.
    

---

##  ¿Por qué usar Naabu frente a Nmap?

|Característica|Naabu|Nmap|
|---|---|---|
|Velocidad|Muy alta (concurrente)|Media (más exhaustivo)|
|Peso|Muy ligera|Más pesada|
|Lenguaje|Go|C/C++|
|Scripts NSE| No| Sí|
|Integración OSINT| Sí (Subfinder, HTTPX...)| Limitada|
|Personalización|Alta|Muy alta (pero compleja)|
|Ideal para|Recon rápido y automatizado|Escaneo detallado manual|

 Naabu no reemplaza a Nmap, sino que lo **complementa**: primero escaneas puertos con Naabu, luego pasas IPs/puertos a Nmap con `-sV` para detectar versiones.

---

##  Instalación rápida

### Con `go install` (recomendado si tienes Go):

```bash
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
```

### O con `snap` o descarga de binarios en GitHub.

---

##  Consideraciones de seguridad

### Desde el punto de vista del Red Team:

- Naabu es ideal para escanear objetivos en campañas de pentest, bounty hunting o Red Team con poco ruido.
    
- Permite detectar servicios ocultos sin enviar payloads.
    

### Desde el Blue Team:

- Debes configurar IDS/IPS para detectar escaneos TCP rápidos.
    
- Firewalls deben limitar el número de conexiones por IP.
    
- Monitorear puertos abiertos inesperados puede revelar la actividad del atacante.
    

---

##  Integración recomendada

-  Subfinder → para subdominios.
    
-  Naabu → para escaneo rápido de puertos.
    
-  HTTPX → para detección de servicios web.
    
-  Nuclei → para escaneo de vulnerabilidades web.
    
-  Notify → para recibir notificaciones al detectar servicios vivos.
    

---

##  Conclusión

**Naabu** es una herramienta de escaneo TCP moderna, rápida y centrada en la automatización. No pretende sustituir herramientas como Nmap, sino agilizar y optimizar la detección inicial de servicios como parte de un flujo OSINT más amplio. Es **ideal para pentesters, bug bounty hunters, red teamers y analistas de ciberinteligencia**.

¿Te gustaría que te prepare un **script completo de reconocimiento automático** con Naabu + Subfinder + HTTPX? ¿O quieres que integremos Naabu en un flujo de escaneo con salida en Power BI o Splunk?