---
title: "Sap Pi"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - sap_pi
---

## **1. Qué es SAP PI**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/LDAP|LDAP]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

SAP PI (**Process Integration**, hoy integrado como parte de **SAP Process Orchestration**) es la **capa de middleware distribuido** de SAP que actúa como **Enterprise Service Bus (ESB)** y motor de orquestación de procesos.

Su función principal es **integrar sistemas heterogéneos** (SAP y no SAP) que pueden estar en distintas localizaciones físicas, ejecutando distintos sistemas operativos y tecnologías, mediante un **modelo de mensajería estructurada**.

---

## **2. Rol en la arquitectura distribuida**

En términos de **programación distribuida**, SAP PI:

- Implementa **paso de mensajes** sobre múltiples protocolos (HTTP/S, SOAP, IDoc, RFC, JMS, SFTP…).
    
- Trabaja en **modo síncrono y asíncrono**.
    
- Ofrece **canales tipados** (adapters) que encapsulan la lógica de conexión.
    
- Proporciona **transformación de datos** (mapeo gráfico, Java Mapping, XSLT) para que sistemas con formatos distintos puedan comunicarse.
    
- Funciona en **entorno cluster**, con instancias distribuidas que se comunican y comparten estado (base de datos, colas internas).
    
- Gestiona **concurrencia** usando pools de hilos para procesar mensajes simultáneamente.
    

---

## **3. Componentes clave**

- **Enterprise Service Repository (ESR)** → donde se definen interfaces, mensajes, mapeos y procesos.
    
- **Integration Directory (ID)** → donde se configuran escenarios reales: qué sistemas hablan entre sí, qué adaptadores usan y cómo se enrutan mensajes.
    
- **Adaptadores** → módulos que implementan la lógica de conexión a un tipo de protocolo o sistema.
    
- **Integration Engine** → núcleo que procesa y enruta mensajes.
    
- **BPM (Business Process Management)** → motor para modelar flujos complejos de integración.
    

---

## **4. Ejemplo de flujo**

Si lo piensas con lo que vimos de _cliente-servidor multicapa_:

1. **Sistema A** envía un mensaje XML (por ejemplo, vía HTTP o IDoc).
    
2. **Adapter sender** de PI recibe el mensaje y lo normaliza al formato interno.
    
3. **Mapping** transforma los datos al formato que necesita el destino.
    
4. **Adapter receiver** envía el mensaje al **Sistema B** (puede ser otra instancia SAP o un sistema externo).
    
5. Todo esto es **transparente** para A y B; PI se encarga de la lógica de transporte, transformación y orquestación.
    

---

## **5. Relación con conceptos que ya vimos**

- **Canal de comunicación** → el adapter (síncrono o asíncrono).
    
- **Tipo del canal** → el esquema del mensaje (XSD, IDoc, JSON Schema).
    
- **Paso de mensajes** → el motor Integration Engine con colas internas.
    
- **Orquestación** → BPM para coordinar varias interacciones en un flujo.
    
- **Persistencia** → garantiza que si un nodo falla, el mensaje no se pierde (mensajería confiable).
    

---

## **6. Por qué se considera programación distribuida**

Porque:

- Cada sistema que se conecta a PI es un **proceso independiente** (en su propia máquina/VM).
    
- La comunicación entre sistemas es **remota** (por red, sin memoria compartida).
    
- PI implementa mecanismos de **serialización de datos**, **protocolos de transporte** y **gestión de concurrencia** para que múltiples integraciones funcionen simultáneamente.
    
- Tiene tolerancia a fallos y **alta disponibilidad** como cualquier sistema distribuido crítico.
    
---

## **1. SAP PI como activo crítico**

- Es el **hub de integración** entre sistemas SAP y no SAP.
    
- Maneja datos confidenciales (financieros, RRHH, proveedores, clientes, etc.).
    
- Si se compromete, el atacante puede:
    
    - Acceder a información sensible en tránsito.
        
    - Alterar mensajes para inyectar operaciones falsas.
        
    - Desestabilizar procesos críticos de negocio.
        

Por eso, **la superficie de ataque es alta** y su protección es estratégica.

---

## **2. Seguridad en las comunicaciones**

En **programación distribuida**, la capa de transporte es la primera línea de defensa:

- **TLS/SSL** en adaptadores HTTP/S, SOAP, REST → protege contra _sniffing_ y _man-in-the-middle_.
    
- **SSH/SFTP** en transferencia de ficheros.
    
- **Certificados y keystores** en NetWeaver para cifrado de extremo a extremo.
    
- **Firmas digitales** en mensajes XML para garantizar integridad y autenticidad.
    

---

## **3. Autenticación y autorización**

- Integración con **SAP NetWeaver User Management** y directorios LDAP/Active Directory.
    
- Autenticación **X.509**, **Basic Auth**, **OAuth 2.0** (según adaptador).
    
- Autorizaciones a nivel de **Integrated Configuration Objects (ICO)**, adaptadores y canales → control granular sobre quién puede desplegar, modificar o consumir interfaces.
    

---

## **4. Validación y filtrado de datos**

- Uso de **Content-based filtering** y validaciones de esquema (XSD) para bloquear mensajes malformados o no autorizados.
    
- Prevención de ataques como:
    
    - **XML External Entity (XXE)** en parsers XML.
        
    - **SQL Injection** en integraciones JDBC.
        
    - **Command Injection** en llamadas a sistemas externos.
        

---

## **5. Monitorización y auditoría**

- **Message Monitoring** y **Audit Log** en PI para detectar comportamientos anómalos (volumen inusual, patrones sospechosos).
    
- Integración con **SIEM** corporativo (Splunk, QRadar, ELK…) para correlación de eventos de seguridad.
    
- Activar **Change Logs** para trazabilidad de cambios en ESR y ID.
    

---

## **6. Resiliencia y continuidad**

- Diseño en alta disponibilidad y _failover_ → mitiga DoS accidental o intencionado.
    
- Estrategias de **store-and-forward** para no perder mensajes en caídas.
    
- Segmentación de red (DMZ) para separar adaptadores expuestos a internet del core interno.
    

---

## **7. Controles que aplicarías en un marco de referencia**

Si lo miras con marcos como **ISO 27001**, **NIST CSF** o **ENS**:

- **Protección de datos en tránsito** (A.10 en ISO 27001).
    
- **Control de acceso** (A.9).
    
- **Registro y monitorización** (A.12).
    
- **Seguridad en desarrollo e integración** (A.14).
    
- **Gestión de vulnerabilidades** en el middleware y adaptadores.
    

---

 **Ejemplo práctico**:  
Si en SAP PI tienes una interfaz SOAP expuesta a terceros:

1. La publicas a través de un **Reverse Proxy** con WAF (p. ej. SAP Web Dispatcher + reglas de seguridad).
    
2. Obligas a usar **TLS mutuo** con certificados de cliente.
    
3. Validas el XML contra su esquema XSD.
    
4. Monitorizas el canal para detectar picos de tráfico o patrones de error.
    
5. Registras toda llamada en un SIEM para correlacionar con otros eventos.