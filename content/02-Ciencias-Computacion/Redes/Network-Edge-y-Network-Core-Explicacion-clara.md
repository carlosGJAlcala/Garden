---
title: "Network Edge Y Network Core Explicacion Clara"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
### Network Edge y Network Core – Explicación clara


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

En el contexto de redes de computadoras, como se explica en el libro **"Computer Networking: A Top-Down Approach" de Kurose y Ross**, los conceptos de **network edge** y **network core** definen **las dos partes principales de la arquitectura de Internet**:

---

## 1. Network Edge (el borde de la red)

Es **donde están los dispositivos finales**, es decir, **los sistemas que usan los usuarios** para acceder a la red.

###  ¿Qué incluye?

- **End systems**: laptops, móviles, servidores web, PCs, tablets...
    
- **Aplicaciones**: HTTP, SMTP, FTP, VoIP, etc.
    
- **Redes de acceso**: conexiones domésticas (fibra, ADSL), redes móviles (4G/5G), Wi-Fi.
    
- **ISP de acceso**: operadores que te conectan a Internet.
    

###  Función principal

- Enviar y recibir datos desde/hacia otros dispositivos a través de la red.
    
- Generar tráfico de usuario (correo, navegación, streaming...).
    

---

##  Ejemplo de network edge

- Tu portátil conectado por Wi-Fi.
    
- El router doméstico.
    
- El servidor de Google al que accedes desde Chrome.
    

---

## 2. Network Core (el núcleo de la red)

Es la **infraestructura central de interconexión** que transporta los datos de un lado a otro del mundo. Es decir, **el "sistema de transporte" de Internet**.

###  ¿Qué incluye?

- **Routers troncales (core routers)**: enrutan paquetes entre diferentes redes.
    
- **Backbones de operadores de red (ISP Tier 1 y Tier 2)**.
    
- **Switches de alto rendimiento**.
    
- **Infraestructura física de transporte**: fibra óptica, enlaces troncales, cableado submarino.
    

###  Métodos de conmutación en el core

- **Conmutación de paquetes (packet switching)**: los datos se dividen en paquetes y se envían por rutas independientes.
    
- **Conmutación de circuitos (circuit switching)**: menos común en Internet, pero usada históricamente en telefonía.
    

---

##  Función principal del core

- **Transportar los paquetes de datos** desde el origen hasta el destino.
    
- Elegir la mejor ruta disponible para cada paquete.
    
- Adaptarse a la congestión o fallos mediante reencaminamiento dinámico.
    

---

##  Analogía simple

- **Network Edge** = Los dispositivos personales y redes de acceso (tu casa, oficina).
    
- **Network Core** = Las autopistas de datos que conectan ciudades (el backbone de Internet).
    

---

##  Seguridad: diferencia clave

- El **edge** es donde se producen la mayoría de los ataques (phishing, malware, acceso no autorizado).
    
- El **core** está más protegido, pero si es atacado (DoS a routers troncales), el impacto es global.
    

---

## Conclusión

La arquitectura de Internet se divide en:

1. **Network Edge**: donde están los usuarios y dispositivos finales.
    
2. **Network Core**: la red interna de routers y enlaces que **transmite datos** entre dispositivos en diferentes partes del mundo.
    

Esta distinción ayuda a entender cómo fluye la información y cómo se diseñan los mecanismos de **encaminamiento, control de tráfico y seguridad**.

---