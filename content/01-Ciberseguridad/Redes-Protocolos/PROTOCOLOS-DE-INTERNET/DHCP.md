---
title: "Dhcp"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### DHCP (Dynamic Host Configuration Protocol) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

**DHCP** es un protocolo de red esencial que permite a los dispositivos obtener automáticamente los parámetros necesarios para comunicarse en una red IP, sin intervención manual del usuario. Está definido en el estándar **RFC 2131**.

---

###  Objetivo principal

Evitar la configuración manual de IPs, máscaras de red, gateways y servidores DNS en cada dispositivo de la red. Gracias a DHCP, la red se vuelve **escalable, dinámica y fácil de administrar**.

---

###  ¿Cómo funciona DHCP?

El proceso ocurre generalmente al iniciar un dispositivo o al unirse a una red:

1. **DHCPDISCOVER (Broadcast)**  
    El cliente pregunta: “¿Hay algún servidor DHCP disponible?”
    
2. **DHCPOFFER**  
    El servidor responde con una dirección IP y parámetros de red propuestos.
    
3. **DHCPREQUEST**  
    El cliente confirma que desea la oferta recibida.
    
4. **DHCPACK**  
    El servidor confirma y asigna formalmente la dirección IP al cliente.
    

> El cliente puede renovar la concesión antes de que expire (lease renewal).

---

###  Parámetros típicamente entregados por DHCP

- Dirección IP
    
- Máscara de subred
    
- Gateway por defecto (puerta de enlace)
    
- Servidores DNS
    
- Tiempo de concesión (lease time)
    
- Opcional: WINS, dominio, rutas estáticas, MTU, etc.
    

---

###  Tipos de asignación

|Tipo|Descripción|
|---|---|
|**Dinámica**|El servidor asigna IPs desde un rango predefinido. Las IPs se pueden cambiar con el tiempo.|
|**Manual (estática por MAC)**|Una IP específica se asigna a una MAC concreta. Muy usado para servidores, impresoras, etc.|
|**Automática (reservas)**|Como la dinámica, pero recuerda qué IP usó cada MAC en el pasado.|

---

###  Arquitectura DHCP

- **Cliente DHCP**: el dispositivo que solicita configuración.
    
- **Servidor DHCP**: gestiona y asigna direcciones IP.
    
- **Relay Agent (opcional)**: reenviador que permite usar un solo servidor DHCP para varias subredes (usualmente un router o switch).
    

---

### ️ Vulnerabilidades y problemas de seguridad

DHCP fue diseñado para entornos de confianza, por lo que **no tiene mecanismos de autenticación nativos**, lo que lo expone a varios riesgos:

#### 1. **Rogue DHCP (DHCP no autorizado)**

- Un atacante configura su propio servidor DHCP en la red.
    
- Puede dar configuraciones maliciosas:
    
    - Gateway falso → redirigir tráfico (MITM).
        
    - DNS falso → ataques de spoofing o phishing.
        
    - IPs inválidas → causar denegación de servicio.
        

#### 2. **Exhaustión del pool de direcciones**

- Un atacante solicita miles de direcciones desde distintas MACs falsas.
    
- Resultado: ningún nuevo cliente puede obtener IPs → **DoS**.
    

#### 3. **Spoofing de respuestas DHCP**

- Si dos servidores responden a la vez, el cliente puede elegir la respuesta maliciosa.
    

---

### ️ Medidas de defensa

1. **DHCP Snooping**
    
    - Disponible en switches gestionables (como Cisco).
        
    - Marca puertos confiables (donde sí hay servidores DHCP) y bloquea los demás.
        
    - Genera una base de datos de IP–MAC–puerto (usado luego para IP Source Guard o ARP Inspection).
        
2. **Filtros de puertos**
    
    - En switches o firewalls para permitir solo servidores autorizados.
        
3. **Asignación estática para dispositivos críticos**
    
    - Para servidores, impresoras o dispositivos de red.
        
4. **Control de acceso a red (NAC, 802.1X)**
    
    - Evita que dispositivos no autenticados puedan acceder a la red y usar DHCP.
        

---

###  Caso de uso: Ataque con rogue DHCP

```plaintext
1. El atacante conecta un portátil con su propio servidor DHCP.
2. Ofrece configuraciones falsas a clientes que se conectan.
3. Redirige su tráfico a través de su equipo (puede espiar, alterar o registrar todo).
```

Este ataque es silencioso y especialmente efectivo en redes abiertas o mal segmentadas.

---

###  Herramientas relacionadas

- **dhcpd**: Servidor DHCP en Linux.
    
- **isc-dhcp-server**: Paquete clásico de servidor DHCP.
    
- **dnsmasq**: Ligero, ideal para redes pequeñas.
    
- **Yersinia**, **Ettercap**: Herramientas para auditar redes y lanzar ataques DHCP.
    

---

###  Relación con otros protocolos

- **DHCP vs BOOTP**: DHCP es una evolución de BOOTP (ambos usan UDP/67 y 68).
    
- **DHCP + ARP**: Tras recibir una IP, el cliente puede usar ARP para verificar si la IP está ya en uso (defensa contra duplicación).
    
- **DHCP + DNS**: Muchos servidores DHCP actualizan automáticamente el DNS al asignar una IP.
    

---

### Conclusión

DHCP es un pilar en la administración de redes modernas, pero **su simplicidad es también su punto débil**. Para mantener la seguridad de una red, es vital combinar DHCP con herramientas de protección como **DHCP Snooping, segmentación de red, y control de acceso por MAC o 802.1X**. También es esencial monitorizar el tráfico DHCP para detectar actividades sospechosas.

---

¿Quieres que te muestre cómo configurar un servidor DHCP seguro en Linux o cómo detectar un DHCP malicioso en una red real con Wireshark?