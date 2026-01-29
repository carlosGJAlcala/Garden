---
title: "Bgp"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### BGP (Border Gateway Protocol) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

**BGP** es el protocolo de enrutamiento **interdominio** de Internet. Su función principal es **interconectar distintos sistemas autónomos (AS)**, que pueden ser ISPs, grandes empresas o instituciones, permitiendo que el tráfico fluya de forma eficiente entre redes que tienen políticas independientes.

Es definido en el estándar **RFC 4271** y es esencial para que Internet funcione tal como lo conocemos.

---

###  ¿Qué es un Sistema Autónomo (AS)?

Un **AS** es un conjunto de redes IP bajo una misma política de enrutamiento y una única administración técnica. Cada AS se identifica con un número único (ASN, **Autonomous System Number**).

- Ejemplo: Google (AS15169), Cloudflare (AS13335), etc.
    

---

###  ¿Qué hace BGP?

BGP permite que los routers en diferentes AS **anuncien rutas** a prefijos IP. Así, otros routers pueden decidir cómo alcanzar cualquier red del mundo.

#### Principales funciones:

- Publicar y recibir rutas IP.
    
- Seleccionar la mejor ruta hacia un destino.
    
- Aplicar **políticas de enrutamiento**, como rechazar ciertas rutas o priorizar otras.
    

---

###  ¿Cómo funciona?

BGP utiliza una arquitectura **path-vector**, donde cada ruta incluye:

- El **prefijo IP de destino** (ej: 8.8.8.0/24)
    
- El **camino AS-PATH**: lista de ASs que deben atravesarse.
    
- Otros atributos como: **MED**, **LOCAL_PREF**, **NEXT_HOP**, **COMMUNITY**, etc.
    

#### Establecimiento de sesión:

- Utiliza **TCP puerto 179** para garantizar la fiabilidad.
    
- Se forma una **sesión BGP** entre dos routers (peers o vecinos).
    
- Intercambian rutas en formato **UPDATE**.
    

---

### ️ Tipos de BGP

1. **eBGP (External BGP)**:
    
    - Entre routers de AS diferentes.
        
    - Usado para conectar ISPs y organizaciones.
        
2. **iBGP (Internal BGP)**:
    
    - Dentro del mismo AS, para propagar rutas recibidas desde el exterior.
        
    - Requiere una malla completa de vecinos o un sistema con route reflectors.
        

---

### ️ Problemas de seguridad en BGP

BGP fue diseñado en una época en la que la confianza entre operadores de red era mayor. Hoy, su diseño abierto lo hace **vulnerable a múltiples amenazas**:

#### 1. **Falsificación de rutas (Route Hijacking)**

- Un AS anuncia erróneamente que controla un bloque IP legítimo de otro.
    
- El tráfico destinado al propietario real se redirige al AS atacante.
    
- Ejemplo: En 2008, Pakistán anunció rutas hacia YouTube, haciendo que el sitio dejara de funcionar en todo el mundo durante horas.
    

#### 2. **Falta de autenticación**

- No hay forma en BGP básico de verificar si una ruta es legítima.
    
- Las sesiones TCP entre routers pueden ser secuestradas o falsificadas.
    

#### 3. **Denegación de servicio (BGP DoS)**

- Un atacante puede enviar gran cantidad de mensajes BGP (mal formateados o no deseados) para saturar la CPU del router receptor.
    

#### 4. **Ataques por error humano**

- Un error de configuración puede propagar rutas incorrectas a todo Internet.
    

---

###  Ejemplo: Secuestro BGP (BGP Hijack)

```plaintext
1. Atacante configura su router BGP para anunciar 8.8.8.0/24 (Google DNS).
2. Sus peers aceptan el anuncio y lo reenvían a sus propios peers.
3. Internet empieza a redirigir tráfico hacia la red del atacante.
```

---

### ️ Mecanismos de defensa

#### 1. **Prefix filtering**

- Solo aceptar rutas que se sabe que debe anunciar un vecino.
    

#### 2. **AS-PATH filtering**

- Verificar que la ruta ha pasado por ASes esperados.
    

#### 3. **TCP MD5 Signature (RFC 2385)**

- Añade una firma MD5 a las sesiones TCP BGP. No es infalible, pero ayuda contra falsificaciones.
    

#### 4. **RPKI (Resource Public Key Infrastructure)**

- Infraestructura criptográfica que permite a los propietarios de bloques IP firmar los AS autorizados a anunciarlos.
    
- Los routers que soportan **RPKI validation** pueden rechazar rutas inválidas.
    

#### 5. **BGP Monitoring Tools**

- Herramientas como **BGPmon**, **RIPE RIS**, **RouteViews** permiten detectar anomalías en anuncios globales.
    

---

###  S-BGP: Secure BGP

S-BGP es una propuesta para asegurar BGP mediante:

- **IPsec** para cifrar y autenticar la sesión BGP.
    
- Infraestructura de clave pública (PKI) para verificar la identidad de routers y propietarios de rutas.
    
- Rutas firmadas digitalmente.
    

**Problema:** Su adopción es limitada debido a la complejidad, coste y necesidad de coordinación global.

---

###  Comparación BGP vs OSPF

|Característica|BGP|OSPF|
|---|---|---|
|Tipo de protocolo|Interdominio (EGP)|Intra-dominio (IGP)|
|Algoritmo|Path-vector|Estado de enlace (Dijkstra)|
|Fiabilidad|TCP|IP directo|
|Seguridad base|Pobre (salvo extensiones)|Autenticación básica|
|Convergencia|Lenta|Rápida|

---

### Conclusión

**BGP es esencial para el funcionamiento de Internet**, pero su diseño original no contempla la seguridad. Hoy se confía en la cooperación entre operadores, filtros y nuevas tecnologías como RPKI para mitigar los riesgos. Su complejidad y poder lo convierten tanto en una herramienta crítica como en un vector de ataque si se gestiona mal.

---

¿Te gustaría que te prepare una simulación de un secuestro BGP con GNS3 o que te muestre cómo se ve un UPDATE BGP real en Wireshark?