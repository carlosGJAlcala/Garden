---
title: "Ospf"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### OSPF (Open Shortest Path First) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

**OSPF** es un protocolo de enrutamiento **dinámico** que opera dentro de un **sistema autónomo (AS)**, es decir, dentro de una red gestionada por una única organización, como una empresa o proveedor de servicios. Es uno de los protocolos **IGP (Interior Gateway Protocol)** más usados y está definido en el estándar **RFC 2328 (para IPv4)** y **RFC 5340 (para IPv6 - OSPFv3)**.

---

###  ¿Qué hace OSPF?

OSPF permite que los **routers descubran y mantengan automáticamente** la mejor ruta hacia todos los destinos posibles dentro de su red. Usa un modelo de red basado en **estado de enlace (link state)** en lugar de distancia vectorial (como RIP), lo que le permite tener:

- Convergencia rápida.
    
- Escalabilidad.
    
- Mejor visibilidad de la red.
    

---

###  ¿Cómo funciona?

1. **División en áreas**:
    
    - La red OSPF se divide en "áreas" para facilitar la escalabilidad.
        
    - Todas deben conectarse al **Área 0** (el núcleo/backbone).
        
    - Permite optimizar el cálculo de rutas y reducir el tráfico de control.
        
2. **Descubrimiento de vecinos**:
    
    - Mediante **Hello packets**, los routers detectan otros routers OSPF conectados directamente.
        
    - Se establece una **adyacencia** entre ellos.
        
3. **LSAs (Link State Advertisements)**:
    
    - Cada router crea un mensaje LSA describiendo sus enlaces y coste (ancho de banda, latencia, etc.).
        
    - Todos los LSAs se **inundan (flooding)** a través del área.
        
    - Cada router construye una copia local de la **topología completa de la red**.
        
4. **Algoritmo de Dijkstra**:
    
    - Cada router aplica este algoritmo para calcular el **camino de coste mínimo** hacia cada destino.
        
5. **Encapsulación**:
    
    - Los mensajes OSPF se encapsulan directamente en **paquetes IP** (protocolo IP número 89).
        

---

###  Tipos de routers en OSPF

- **Internal Router**: opera solo dentro de un área.
    
- **Backbone Router**: pertenece al área 0.
    
- **Area Border Router (ABR)**: conecta diferentes áreas.
    
- **Autonomous System Boundary Router (ASBR)**: conecta OSPF con otros protocolos como BGP o RIP.
    

---

### ️ Seguridad en OSPF

OSPF incluye mecanismos básicos de seguridad, pero no son suficientes frente a ataques sofisticados si no se refuerzan:

#### Riesgos principales:

1. **Inyección de LSAs falsos**:
    
    - Un router malicioso puede emitir un LSA incorrecto, manipulando rutas.
        
2. **Suplantación de adyacencias**:
    
    - Como no se requiere confirmación estricta, un router "fantasma" puede hacerse pasar por legítimo.
        
3. **Ataques DoS por inundación**:
    
    - Enviar LSAs falsos o corruptos en bucle consume CPU y memoria.
        
4. **Problemas de integridad de la base de datos LSA**:
    
    - Si un router ve un LSA suyo con un timestamp más reciente que el actual, genera uno nuevo. Esto puede ser abusado.
        

#### Mecanismos de defensa:

- **Autenticación OSPF**:
    
    - Puede ser **simple (clave compartida en claro)** o con **MD5** para integridad de mensajes.
        
    - Cada interfaz puede configurarse con una clave distinta.
        
- **IPsec + OSPFv3**:
    
    - En redes IPv6, se puede usar IPsec para cifrar y autenticar el tráfico OSPF.
        
- **Filtrado de LSAs y límites de rutas**:
    
    - Para evitar la sobrecarga o manipulación de topología.
        

---

###  Ejemplo de ataque (DoS por router fantasma)

Un atacante remoto crea un router falso que establece adyacencias con routers legítimos:

```
Red 1
   |
[Router Víctima] <--- Router Fantasma (Atacante)
   |
   └--> Adyacencia falsa y LSA corruptos
```

- Resultado: el tráfico se desvía, se generan rutas erróneas o se satura el router.
    

---

###  OSPF vs BGP

|Característica|OSPF|BGP|
|---|---|---|
|Alcance|Intra-dominio (IGP)|Inter-dominio (EGP)|
|Algoritmo|Dijkstra (coste mínimo)|Políticas de ruta|
|Velocidad|Muy rápido (convergencia)|Más lento|
|Seguridad base|Autenticación (limitada)|Casi inexistente sin extensiones|
|Protocolo IP|89|TCP/179|

---

### Conclusión

OSPF es eficiente, flexible y adecuado para redes medianas y grandes. No obstante, si no se protege adecuadamente, puede ser manipulado con facilidad por actores maliciosos. Se recomienda siempre activar autenticación, monitorizar la red OSPF y segmentar las áreas para limitar el impacto de un ataque.

---

¿Quieres que te muestre cómo se configura OSPF con autenticación en routers Cisco o simuladores como GNS3 o Packet Tracer?