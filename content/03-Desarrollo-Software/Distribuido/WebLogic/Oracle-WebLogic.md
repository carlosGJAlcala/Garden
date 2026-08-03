---
title: "Oracle Weblogic"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - weblogic
---

## **1. Qué es Oracle WebLogic**


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[02-Ciencias-Computacion/Redes/Kafka|Kafka]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Concurrencia/servlets|servlets]].

Oracle WebLogic Server es un **servidor de aplicaciones Java EE** (hoy Jakarta EE) que proporciona un entorno para **desplegar, ejecutar y gestionar aplicaciones empresariales distribuidas**.  
Es muy usado como **middleware** en arquitecturas SOA y en integraciones corporativas (por ejemplo, como base de Oracle SOA Suite).

---

## **2. Rol en programación distribuida**

En términos de lo que hemos visto:

- Implementa un **contenedor de aplicaciones** que ejecuta **componentes distribuidos**: Servlets, JSP, EJB, Web Services.
    
- Gestiona **comunicación remota** entre capas de aplicación (RMI, JMS, HTTP/S, SOAP, REST).
    
- Controla **transacciones distribuidas** (XA) sobre múltiples recursos (bases de datos, colas de mensajes).
    
- Ofrece **alta disponibilidad** y **balanceo de carga** en clúster.
    
- Soporta **seguridad centralizada** para servicios y aplicaciones.
    

---

## **3. Funciones principales**

- **Contenedor web** → para Servlets, JSP, APIs REST.
    
- **Contenedor EJB** → para lógica de negocio distribuida con Enterprise Java Beans.
    
- **JMS (Java Message Service)** → mensajería asíncrona para integración de sistemas.
    
- **Web Services** → implementación de SOAP y REST.
    
- **Gestión de recursos** → conexiones JDBC, pools de hilos, colas JMS.
    
- **Cluster** → replicación de sesiones, failover automático.
    

---

## **4. Ejemplo en una arquitectura SOA**

Si tienes SAP PI o MuleSoft integrando sistemas, WebLogic podría:

- Servir como **runtime** para servicios SOAP/REST que implementan funciones de negocio.
    
- Albergar el **ESB** (por ejemplo, Oracle Service Bus).
    
- Ejecutar procesos BPMN con Oracle BPM.
    
- Exponer APIs que SAP PI consume o que publican datos a Kafka.
    

---

## **5. Relación con ciberseguridad**

Como cualquier middleware crítico, **WebLogic es un objetivo frecuente** de ataques, especialmente si expone paneles de administración o servicios sin protección.

**Riesgos**:

- Vulnerabilidades RCE (Remote Code Execution) muy conocidas si no está parcheado.
    
- Exposición de consola de administración a internet.
    
- Servicios SOAP/REST inseguros o sin autenticación.
    
- Malas configuraciones en JMS o EJBs remotos.
    

**Controles recomendados**:

- Mantenerlo siempre **parcheado** (WebLogic tiene un historial largo de CVEs críticas).
    
- Restringir acceso a la consola y puertos de administración.
    
- Autenticación fuerte y roles para despliegue y acceso a servicios.
    
- Uso de TLS y cifrado para todo el tráfico (incluido interno del clúster).
    
- Escaneo de configuración con herramientas de seguridad (CIS Benchmarks, Oracle Security Guide).
    

---

## **6. Comparación con SAP PI**

|Característica|WebLogic|SAP PI|
|---|---|---|
|**Función principal**|Servidor de aplicaciones Java EE|ESB/Integrador SOA|
|**Comunicación**|HTTP/S, RMI, JMS, SOAP, REST|SOAP, REST, IDoc, RFC, JMS, SFTP…|
|**Orquestación**|No nativo (necesita Oracle SOA Suite)|Sí, con BPM integrado|
|**Transformación de datos**|A través de librerías o frameworks externos|Nativo en el Integration Engine|
|**Seguridad**|Roles, realms, certificados, TLS|Roles, certificados, WS-Security, cifrado de mensajes|
|**Escalabilidad**|Clúster WebLogic|Clúster PI|

---

