---
title: "Nmap"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
### ¿Qué es Nmap y cómo usarlo?

> **Relacionado**: Ver [[01-Ciberseguridad/Herramientas/Reconocimiento/TheHarvester|TheHarvester]] para OSINT. [[01-Ciberseguridad/Herramientas/Reconocimiento/DNSEnum|DNSEnum]] para enumeración DNS. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Reconocimiento/Port-Scanning|Port Scanning]]. [[02-Ciencias-Computacion/Lenguajes-Programacion/Python/socket/Nmap-en-python|Nmap en Python]].

**Nmap** (Network Mapper) es una herramienta de código abierto muy poderosa, utilizada principalmente para escanear redes y sistemas en busca de vulnerabilidades, puertos abiertos, dispositivos activos y aplicaciones en ejecución. Es ampliamente utilizada en pruebas de penetración, auditorías de seguridad, y para la administración de redes. Fue desarrollada por **Gordon Lyon** (conocido como Fyodor), y se ha convertido en una de las herramientas esenciales en ciberseguridad, especialmente en el ámbito de la exploración de redes y la evaluación de sistemas.

#### **¿Por qué usar Nmap?**

Nmap es útil para administradores de red, pentesters y profesionales de seguridad por varias razones:

1. **Escaneo de Dispositivos Activos**: Permite identificar rápidamente los dispositivos conectados a una red.
2. **Detección de Puertos Abiertos y Servicios**: Identifica los puertos abiertos y los servicios que se están ejecutando en los dispositivos de la red.
3. **Detección de Sistema Operativo**: Proporciona información sobre el sistema operativo que está utilizando el dispositivo, lo cual es clave en la planificación de ataques durante un test de penetración.
4. **Motor de Secuencias de Comandos (NSE)**: Permite la automatización de tareas complejas y escaneos personalizados mediante scripts escritos en **Lua**.
5. **Interfaz Gráfica (Zenmap)**: Aunque Nmap es una herramienta de línea de comandos, también dispone de Zenmap, una interfaz gráfica de usuario que facilita su uso, especialmente para principiantes.

---

### **Comandos Básicos de Nmap**

A continuación, veremos algunos de los comandos más utilizados con Nmap para realizar distintos tipos de escaneos y análisis.
### 0. Escanear de forma rápida equipos de red
```bash
nmap -f 192.168.1.0/24
```

#### **1. Escanear Dispositivos Activos en una Red**

- **Escaneo de Ping**: Para detectar dispositivos activos en una red, puedes realizar un escaneo de ping. Esto verificará qué dispositivos están respondiendo en una subred.

```bash
nmap -sn 192.168.1.0/24
```

Este comando escaneará todos los dispositivos en la subred `192.168.1.0/24`.

- **Escanear un solo Host**: Para escanear un solo dispositivo y obtener información de los puertos más comunes:

```bash
nmap scanme.nmap.org
```

Este comando escaneará el host `scanme.nmap.org` y proporcionará información sobre los puertos más comunes.

#### **2. Escaneo Sigiloso (Stealth Scan)**

Un escaneo sigiloso envía paquetes SYN sin completar el protocolo TCP de tres vías. Esto hace que sea menos detectable en comparación con otros tipos de escaneo.

```bash
nmap -sS scanme.nmap.org
```

El **`-sS`** realiza un escaneo sigiloso (SYN scan). Es útil para evitar que el objetivo se dé cuenta de que está siendo escaneado.

#### **3. Escaneo de Versiones de Servicios**

Con Nmap puedes identificar no solo qué servicios están disponibles, sino también las versiones exactas que están ejecutando. Esto es crucial para detectar vulnerabilidades conocidas asociadas con ciertas versiones de software.

```bash
nmap -sV scanme.nmap.org
```

El **`-sV`** realiza un escaneo para detectar las versiones de los servicios que se ejecutan en los puertos abiertos.

#### **4. Escaneo del Sistema Operativo**

Nmap también puede intentar identificar el sistema operativo de los dispositivos escaneados utilizando huellas dactilares TCP/IP. Esto puede ser útil para los pentesters que necesitan obtener más información sobre el sistema objetivo.

```bash
nmap -O scanme.nmap.org
```

El **`-O`** activa la detección del sistema operativo. Nmap intentará identificar el sistema operativo del dispositivo objetivo basándose en las respuestas TCP/IP.

#### **5. Escaneo Agresivo**

El escaneo agresivo realiza múltiples pruebas al mismo tiempo: escaneo de puertos, detección del sistema operativo, detección de versiones, ejecución de scripts y trazado de rutas.

```bash
nmap -A scanme.nmap.org
```

El **`-A`** habilita el escaneo agresivo. Este tipo de escaneo genera más tráfico y puede ser detectado con mayor facilidad por sistemas de defensa como firewalls y sistemas de detección de intrusiones (IDS).

#### **6. Escaneo de Múltiples Hosts**

Si necesitas escanear varios dispositivos al mismo tiempo, puedes especificar múltiples direcciones IP.

- **Escanear direcciones IP específicas**:

```bash
nmap 192.168.1.1 192.168.1.2 192.168.1.3
```

- **Escanear un rango de direcciones IP**:

```bash
nmap 192.168.1.1-50
```

- **Escanear toda una subred**:

```bash
nmap 192.168.1.*
```

#### **7. Escaneo de Puertos Específicos**

Puedes realizar un escaneo de puertos para encontrar cuáles están abiertos y en qué servicios están escuchando.

- **Escanear un solo puerto**:

```bash
nmap -p 80 192.168.1.1
```

- **Escanear un rango de puertos**:

```bash
nmap -p 1-1000 192.168.1.1
```

- **Escanear los puertos más comunes**:

```bash
nmap --top-ports 20 scanme.nmap.org
```

#### **8. Exportar Resultados de Nmap**

Es útil guardar los resultados de los escaneos para su posterior análisis o generación de informes.

- **Guardar salida en un archivo de texto**:

```bash
nmap -oN resultados.txt scanme.nmap.org
```

- **Guardar salida en formato XML**:

```bash
nmap -oX resultados.xml scanme.nmap.org
```

- **Guardar en múltiples formatos (XML, Nmap y GNmap)**:

```bash
nmap -oA resultados scanme.nmap.org
```

#### **9. Uso del Motor de Secuencias de Comandos Nmap (NSE)**

Nmap incluye un motor de secuencias de comandos que permite realizar escaneos más avanzados, como detección de vulnerabilidades, análisis de protocolos y ataques. Existen numerosos scripts predefinidos disponibles con Nmap.

Para ejecutar un script específico, usa:

```bash
nmap --script=http-vuln* scanme.nmap.org
```

Este comando ejecuta todos los scripts que comienzan con `http-vuln` para buscar vulnerabilidades en servidores web.

---

### **Zenmap: Interfaz Gráfica de Usuario para Nmap**

Si prefieres no usar la línea de comandos, **Zenmap** es la interfaz gráfica oficial de Nmap. Zenmap facilita la creación de mapas visuales de la red y la gestión de escaneos, además de almacenar el historial de los escaneos realizados. Es útil tanto para principiantes como para expertos.

---

### **Conclusión**

Nmap es una herramienta esencial para cualquier profesional de la seguridad de redes. Gracias a su versatilidad y poder, se utiliza tanto en auditorías de seguridad como en pruebas de penetración, análisis de redes y administración de sistemas. Con una amplia gama de opciones y configuraciones, Nmap te permite obtener información detallada sobre la infraestructura de red y detectar posibles vulnerabilidades antes de que los atacantes las exploten.

Si eres nuevo en Nmap, comienza con los escaneos básicos y luego avanza hacia funciones más complejas como la detección de versiones o el uso de scripts de Nmap para detectar vulnerabilidades.