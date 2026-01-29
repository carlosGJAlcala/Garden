---
title: "Ip"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### IP (Internet Protocol) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/DHCP|DHCP]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[02-Ciencias-Computacion/Lenguajes-Programacion/Python/Scapy|Scapy]].

El **Protocolo de Internet (IP)** es el pilar de la comunicación en redes. Su principal función es **encaminar paquetes de datos desde un origen hasta un destino**, aunque estos estén en redes distintas y geográficamente separadas. Es un protocolo de la **capa de red** en la pila TCP/IP y actúa como intermediario entre la capa de transporte (TCP/UDP) y la de enlace (Ethernet, Wi-Fi...).

---

###  Características principales del Protocolo IP

1. **No orientado a conexión**
    
    - No se establece una conexión previa entre emisor y receptor. Cada paquete es independiente.
        
    - Esto permite escalabilidad, pero **no garantiza entrega ni orden**.
        
2. **Best-effort (mejor esfuerzo)**
    
    - IP no asegura que los paquetes lleguen, ni que lo hagan sin errores o en orden.
        
    - Delega el control de errores y reenvíos a capas superiores como TCP.
        
3. **Encapsulamiento**
    
    - El protocolo IP encapsula los datos de la capa de transporte en **paquetes IP**.
        
    - A su vez, estos se encapsulan en tramas de capa de enlace para ser transmitidos.
        

---

###  Estructura de un paquete IP (IPv4)

|Campo|Descripción breve|
|---|---|
|Versión|IPv4 o IPv6|
|Header Length|Tamaño de la cabecera IP|
|Type of Service|Prioridad del paquete|
|Total Length|Longitud total del paquete|
|Identification|ID para fragmentación|
|Flags|Control de fragmentación|
|Fragment Offset|Posición de fragmento|
|TTL (Time to Live)|Vida útil del paquete|
|Protocol|Tipo de protocolo en capa superior (TCP=6, UDP=17, ICMP=1)|
|Header Checksum|Verifica errores en la cabecera|
|IP Origen/Destino|Direcciones IP de origen y destino|

>  El campo TTL se reduce en cada salto entre routers. Si llega a 0, el paquete se descarta (protege de bucles infinitos).

---

### ️ Funciones esenciales del protocolo IP

1. **Encaminamiento (routing)**
    
    - Cada host conoce la IP de su puerta de enlace (router).
        
    - Los routers usan algoritmos (como OSPF, BGP) para decidir el mejor camino.
        
2. **Fragmentación y Reensamblado**
    
    - Si un paquete es más grande que el tamaño máximo permitido en una red intermedia (MTU), se divide en fragmentos.
        
    - El receptor los reensambla basándose en los campos de identificación y fragment offset.
        
3. **Gestión de errores mediante ICMP**
    
    - Si algo va mal (por ejemplo, TTL agotado o destino inalcanzable), se envía un mensaje **ICMP** al emisor para informarle.
        

---

###  Problemas de seguridad del IP

1. **Falsificación de IP (IP Spoofing)**
    
    - El emisor puede mentir sobre su IP de origen.
        
    - Se usa en ataques **DoS**, **reflejo** o para evitar ser rastreado.
        
2. **Falta de autenticación**
    
    - Cualquiera puede enviar paquetes con direcciones IP falsas.
        
    - No hay verificación de identidad en el nivel IP.
        
3. **Fragmentación maliciosa**
    
    - Algunos ataques envían paquetes fragmentados de forma maliciosa para evadir firewalls o explotar errores de reensamblado.
        

---

### ️ Seguridad para IP: IPsec

**IPsec** es una extensión de IP que añade seguridad directamente en la capa de red:

- **Modo transporte**: solo cifra la carga útil (el contenido del paquete).
    
- **Modo túnel**: cifra todo el paquete IP original, útil para VPNs.
    
- **Protocolos**:
    
    - **AH (Authentication Header)**: proporciona integridad y autenticación.
        
    - **ESP (Encapsulating Security Payload)**: proporciona confidencialidad, autenticación e integridad.
        

IPsec se utiliza en VPNs, en tráfico entre routers o servidores, y en implementaciones seguras de IPv6.

---

###  IPv4 vs IPv6

|Característica|IPv4|IPv6|
|---|---|---|
|Longitud de dirección|32 bits (ej: 192.168.0.1)|128 bits (ej: 2001:db8::1)|
|Número de direcciones|~4 mil millones|~3.4×10³⁸|
|Seguridad|Opcional (IPsec)|Recomendado por defecto|
|Configuración|Manual o DHCP|Automática (stateless autoconfig)|
|Fragmentación|Realizada por el emisor o router|Solo por el emisor|

---

### Conclusión

El protocolo IP es la base de la comunicación entre redes, pero su diseño original **no contempla la seguridad**. Por ello, se complementa con otras tecnologías como **IPsec**, **firewalls**, y controles a nivel de red. La transición a IPv6 ofrece mejoras estructurales, aunque no soluciona todos los problemas de seguridad por sí sola.

---

¿Quieres que te amplíe con ejemplos de ataques IP spoofing o que te muestre cómo analizar paquetes IP con Wireshark o scapy?