---
title: "Infraestructura De Internet"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### Infraestructura de Internet – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/DHCP|DHCP]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

La infraestructura de Internet es el conjunto de componentes físicos y lógicos que permiten la conectividad global entre dispositivos, sistemas y usuarios. Esta infraestructura está organizada en capas, según el modelo TCP/IP, y cuenta con diversos protocolos que permiten que la comunicación ocurra de manera eficiente y escalable. A continuación se detallan los elementos clave, ampliando lo que aparece en el documento:

---

#### 1. **Domain Name System (DNS)**

- **Función**: Traduce nombres de dominio (como `www.ejemplo.com`) en direcciones IP (como `192.168.1.1`), necesarias para que los routers localicen los dispositivos en la red.
    
- **Arquitectura**: Es jerárquica. Incluye servidores raíz, TLD (como `.com`, `.org`), servidores autoritativos (que tienen la información definitiva sobre un dominio) y resolvers (habitualmente gestionados por ISPs o empresas).
    
- **Seguridad**: El sistema DNS tradicional no fue diseñado con seguridad en mente. Es susceptible a ataques como envenenamiento de caché, spoofing, y MITM. Para mitigarlos, existen extensiones como DNSSEC y mecanismos como DANE.
    

---

#### 2. **Protocolo de Enrutamiento Local (OSPF)**

- **OSPF (Open Shortest Path First)**: Se utiliza dentro de un sistema autónomo (AS), como la red de una empresa o proveedor de servicios.
    
- **Funcionamiento**: Usa LSAs (Link-State Advertisements) para que cada router tenga una visión completa de la red. Cada cambio de estado se propaga a todos los routers para mantener la coherencia de la topología.
    
- **Seguridad**: Puede sufrir ataques si un router malicioso introduce información falsa. La autenticación de LSAs con claves compartidas o IPsec es una defensa posible.
    

---

#### 3. **Protocolo de Enrutamiento Entre Dominios (BGP)**

- **BGP (Border Gateway Protocol)**: Maneja el enrutamiento entre diferentes sistemas autónomos (interdominios), es decir, entre redes de proveedores de Internet.
    
- **Importancia**: BGP es fundamental para que Internet funcione, pues permite que el tráfico viaje entre países, organizaciones y continentes.
    
- **Problemas**: Es vulnerable a secuestro de rutas (route hijacking), anuncios falsos y falta de autenticación. Para protegerlo se han propuesto mecanismos como S-BGP y RPKI (Resource Public Key Infrastructure).
    

---

#### 4. **Protocolo ARP (Address Resolution Protocol)**

- **Función**: Resuelve direcciones IP a direcciones MAC dentro de una red local (LAN). Cuando una máquina necesita enviar datos a otra en la misma red, usa ARP para conocer su dirección física.
    
- **Ataques**: ARP Spoofing o envenenamiento ARP permite a un atacante interceptar o modificar tráfico en la red.
    
- **Defensas**: Incluyen ARP estático, herramientas como ARPWatch, inspección DHCP, o el uso de switches que verifican las relaciones IP-MAC.
    

---

#### 5. **Pila de Protocolos TCP/IP**

- **Capas**:
    
    - **Aplicación**: HTTP, SMTP, DNS, FTP, etc.
        
    - **Transporte**: TCP (confiable, orientado a conexión), UDP (rápido pero no confiable)
        
    - **Red**: IP, ICMP
        
    - **Enlace**: Ethernet, Wi-Fi
        
- Cada capa encapsula la información de la anterior, lo que permite modularidad y eficiencia en la transmisión de datos.
    

---

#### 6. **ISPs (Proveedores de Servicios de Internet)**

- Son actores clave de la infraestructura de Internet. Poseen grandes redes (backbones), routers BGP, y conexiones con otros ISPs. Están organizados jerárquicamente: Tier 1 (backbones globales), Tier 2 (nacionales/regionales), Tier 3 (locales).
    

---

#### 7. **Medio físico**

- Incluye cables de cobre, fibra óptica, ondas de radio (Wi-Fi, 4G/5G), satélites, etc. El medio físico es la base donde ocurre toda la comunicación, y está expuesto a vulnerabilidades físicas, escuchas, sabotaje, etc.
    

---

### Conclusión

La infraestructura de Internet es un entramado complejo y distribuido, compuesto por sistemas interdependientes que permiten el enrutamiento, resolución de nombres, y acceso eficiente a los recursos. Sin embargo, su diseño original no contemplaba la seguridad como prioridad, lo que obliga a añadir capas de protección mediante estándares, protocolos seguros y vigilancia continua para mitigar riesgos crecientes.

---