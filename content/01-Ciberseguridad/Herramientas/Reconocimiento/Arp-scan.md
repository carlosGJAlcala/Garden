---
title: "Arp Scan"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  arp-scan (Ar)


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

- **Nombre en la tabla:** **arp-scan**
    
- **Símbolo:** **Ar**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de descubrimiento de hosts a nivel de red local (capa 2)
    
- **Repositorio oficial:** [https://github.com/royhills/arp-scan](https://github.com/royhills/arp-scan)
    
- **Sitio web:** [https://linux.die.net/man/1/arp-scan](https://linux.die.net/man/1/arp-scan)
    

---

##  ¿Qué es arp-scan?

**arp-scan** es una herramienta de descubrimiento de red que envía solicitudes **ARP (Address Resolution Protocol)** para identificar dispositivos activos en una red local. A diferencia de herramientas como Nmap o ping, que operan sobre **IP o puertos**, arp-scan trabaja directamente en la **capa 2 (enlace de datos)**, lo que lo hace más fiable en redes donde los pings están bloqueados o filtrados.

Ideal para **enumerar todos los dispositivos conectados a una red local**, incluso aquellos que no responden a ICMP o escaneos TCP/UDP tradicionales.

---

## ️ Funcionalidades clave

-  Envía paquetes ARP personalizados a toda una subred (ej. `192.168.1.0/24`).
    
-  Detecta **IPs activas**, **direcciones MAC** y su posible fabricante (vendor).
    
-  Permite escaneo rápido incluso cuando el firewall bloquea otros métodos.
    
-  Funciona en redes Ethernet con IPv4 (no soporta Wi-Fi sin modo monitor).
    
-  Salida clara y exportable (texto plano o CSV).
    
-  Ideal para fases iniciales de reconocimiento interno en entornos Red Team.
    

---

##  Ejemplos de uso

###  Escanear una red local completa

```bash
sudo arp-scan 192.168.1.0/24
```

Ejemplo de salida:

```
192.168.1.1   00:11:22:33:44:55   Cisco Systems
192.168.1.100 00:aa:bb:cc:dd:ee   Dell Inc
192.168.1.101 00:ff:cc:11:22:33   Apple, Inc.
```

---

###  Detectar todos los dispositivos conectados en la misma subred

```bash
sudo arp-scan --interface=eth0 --localnet
```

Detecta todos los dispositivos que comparten la red con la interfaz `eth0`.

---

###  Guardar la salida en archivo

```bash
sudo arp-scan 192.168.0.0/24 > resultados.txt
```

---

###  Cambiar la dirección MAC de origen (técnicas avanzadas)

```bash
sudo arp-scan --arpspa=192.168.1.1 --arpsha=00:11:22:33:44:55 192.168.1.0/24
```

Esto envía paquetes ARP con IP/MAC falsas, útil para pruebas de spoofing.

---

##  ¿Por qué usar arp-scan?

|Ventaja|Descripción|
|---|---|
| Rápido|Puede escanear 255 hosts en pocos segundos.|
| Silencioso|No genera tráfico TCP/UDP detectable fácilmente.|
| Más fiable|Descubre hosts que no responden a ping o escaneo de puertos.|
| Detección temprana|Útil en entornos donde el tiempo de acceso es limitado.|
| A nivel interno|Ideal para pruebas en redes corporativas internas.|

---

##  Implicaciones de seguridad

Desde el punto de vista del **Blue Team**, arp-scan puede usarse para:

- Auditar qué dispositivos están conectados realmente a una red.
    
- Detectar dispositivos no autorizados (BYOD, IoT sospechoso).
    
- Comparar contra la base de datos de direcciones MAC aprobadas.
    
- Monitorear cambios inesperados en la tabla ARP.
    

️ Un atacante puede usar `arp-scan` para descubrir dispositivos críticos antes de lanzar técnicas como ARP poisoning o Man-in-the-Middle (MitM).

---

##  Instalación

### En Debian/Ubuntu:

```bash
sudo apt install arp-scan
```

### En Fedora:

```bash
sudo dnf install arp-scan
```

### En Arch:

```bash
sudo pacman -S arp-scan
```

---

##  Integración en pipelines

arp-scan puede actuar como paso **inicial en escaneos de red interna**, antes de lanzar Nmap o herramientas de explotación. Ejemplo de flujo:

```bash
sudo arp-scan --localnet | awk '{print $1}' | grep '^192' | xargs -I{} nmap -sV {}
```

Este script escanea con Nmap solo las IPs activas detectadas por arp-scan.

---

##  Conclusión

**arp-scan** es una herramienta ligera pero poderosa para detectar **todos los dispositivos conectados en una red local** sin necesidad de escaneo IP tradicional. Es especialmente útil en **auditorías internas, pentesting de redes corporativas, análisis de activos y defensa proactiva**.

---

¿Te gustaría que prepare un script que combine `arp-scan`, `nmap`, `ffuf` y `nuclei` para un pipeline completo de descubrimiento y análisis en una red interna? ¿O prefieres un caso práctico con mapa de red generado a partir de los resultados?