---
title: "2024 12 26 El Libro Del Hacker"
date: 2025-01-01
tags:
  - general
---

hola cdv

# NOTAS LIBRO HACKER

##  1. **Archivos PDF como vectores de ataque**

Los archivos PDF pueden **contener código malicioso**, incluyendo:

- **JavaScript embebido** que se ejecuta al abrir el archivo en ciertos visores.
    
- **Objetos incrustados** (Flash, imágenes) con payloads.
    
- **Explotación de vulnerabilidades** específicas de Adobe Reader u otros lectores (buffer overflows, RCE...).
    

 **Ejemplo de ataque**:  
Un PDF con JavaScript puede ejecutar shellcode en memoria para descargar e instalar malware, o explotar una CVE específica del lector PDF.

###  Mitigación:

- Desactivar ejecución automática de JavaScript en lectores PDF.
    
- Utilizar visores seguros (por ejemplo, Evince, Okular).
    
- Analizar en sandbox (como Cuckoo o Any.Run) dentro de **máquinas virtuales aisladas**.
    

---

##  2. **Análisis de comportamiento con herramientas**

###  Process Hacker:

- Alternativa avanzada a Task Manager.
    
- Permite:
    
    - Ver procesos, hilos, handles, conexiones de red.
        
    - Identificar procesos anómalos con conexiones HTTP o DNS sospechosas.
        
    - Ver **librerías DLL cargadas por cada proceso**.
        

Se complementa con:

- **Wireshark**: inspección de tráfico.
    
- **Procmon (Sysinternals)**: seguimiento de llamadas al sistema y cambios en registro/archivos.
    
- **Autoruns**: visualización de persistencia.
    

---

##  3. **Proceso `svchost.exe` como vector de ataque**

### Qué es:

- `svchost.exe` es un **proceso contenedor de servicios** del sistema Windows (como DHCP, DNS Client, etc.).
    
- Varios servicios comparten la misma instancia del proceso para optimizar recursos.
    

### Uso malicioso:

- Malware puede **inyectar código o cargar DLLs** maliciosas dentro de instancias legítimas de `svchost.exe`.
    
- Técnicas:
    
    - **Reflective DLL injection**
        
    - **Process hollowing**
        
    - **Mascarado (masquerading)** para evitar detección.
        

 Un proceso `svchost.exe`:

- No debe ejecutarse fuera de `%SystemRoot%\System32`.
    
- No debería tener acceso directo a red en muchos casos (excepto para servicios que lo requieran explícitamente).
    

---

##  4. **Protocolo ICMP y su uso en ataques MitM**

### ICMP (Internet Control Message Protocol):

- Usado para mensajes de diagnóstico (ping, traceroute).
    
- Tipo 5 (Redirect) se utiliza para **sugerir al host una nueva puerta de enlace**.
    

### ️ ICMP Redirect en ataques:

- Un atacante en la red lanza un mensaje ICMP Redirect para **decirle al host que la mejor ruta es a través del atacante**.
    
- Permite desviar el tráfico: **Man-in-the-Middle (MitM)**.
    

 Condiciones:

- El atacante debe estar en la misma red o suplantar el gateway.
    
- Afecta redes mal configuradas (sin validación de rutas).
    

### Mitigación:

- **Desactivar ICMP Redirects** en routers y SO.
    
- Usar **ARP inspection** o switches con protección contra suplantación.
    
- Aplicar políticas de red estrictas (ACL, segmentación).
    

---

##  5. **IPv6, NDP, SLAAC y seguridad**

### a) **NDP (Neighbor Discovery Protocol)**:

- Equivalente a **ARP en IPv4**, pero más avanzado.
    
- Usa **ICMPv6** para:
    
    - Descubrir direcciones MAC.
        
    - Detectar routers (Router Advertisement).
        
    - Detectar vecinos activos (Neighbor Solicitation/Advertisement).
        

### b) **SLAAC (Stateless Address Autoconfiguration)**:

- Similar al DHCP, pero sin servidor.
    
- El host genera su IP automáticamente a partir del prefijo del router y su dirección MAC (EUI-64 o privacidad extendida).
    

### c) **Multicast en IPv6**:

- En lugar de **broadcast** como en IPv4, IPv6 usa **multicast** para descubrir dispositivos o enviar mensajes a grupos específicos:
    
    - `ff02::1` → todos los nodos locales.
        
    - `ff02::2` → todos los routers locales.
        

### d) **IPsec nativo**:

- IPv6 fue diseñado con **IPsec obligatorio** (aunque en la práctica es opcional).
    
- Permite encriptación y autenticación en capa 3:
    
    - AH (Authentication Header).
        
    - ESP (Encapsulating Security Payload).
        

---

## ️ Herramientas de escaneo IPv6

- `nmap -6` → escaneo de hosts IPv6.
    
- `thc-ipv6`: suite avanzada de pentesting para IPv6.
    
- `ping6`, `traceroute6` → comandos de diagnóstico.
    

---

##  Conclusión

El análisis del comportamiento malicioso requiere una **visión transversal del sistema operativo, red y procesos**. PDF y `svchost.exe` representan vectores clásicos de ataque que, si no se analizan correctamente, pasan desapercibidos. Protocolos como ICMP o IPv6 ofrecen funcionalidad legítima, pero también **superficies de ataque** si se abusa de su diseño. Para investigarlos y comprenderlos, es esencial usar entornos controlados, instrumentación adecuada, y conocer en profundidad los mecanismos involucrados.

¿Quieres que te prepare una guía paso a paso para montar un entorno de análisis en máquina virtual o sandbox?