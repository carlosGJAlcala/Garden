---
title: "Soa"
date: 2025-01-01
tags:
  - desarrollo-software
---

## **1. Qué es SOA**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[03-Desarrollo-Software/Distribuido/Microservicios|Microservicios]]. [[03-Desarrollo-Software/Distribuido/MuleSoft|MuleSoft]]. [[02-Ciencias-Computacion/Redes/Kafka|Kafka]].

**SOA** (_Service-Oriented Architecture_, Arquitectura Orientada a Servicios) es un estilo de arquitectura para sistemas distribuidos donde la funcionalidad de negocio se expone como **servicios independientes**, con **interfaces bien definidas** y **protocolos estándar** para comunicarse.

El objetivo es **desacoplar**:

- Quién ofrece el servicio (**proveedor**) y quién lo usa (**consumidor**).
    
- Dónde está implementado y cómo está programado.
    

---

## **2. Principios clave**

1. **Interoperabilidad**  
    Los servicios deben poder hablar entre sí sin importar el lenguaje o la plataforma (Java, .NET, SAP, Python…).
    
2. **Interfaces contractuales**  
    Cada servicio define un contrato (p. ej., WSDL en SOAP, OpenAPI en REST) que especifica cómo invocarlo.
    
3. **Bajo acoplamiento**  
    Cambios internos en el servicio no deben afectar al consumidor si la interfaz no cambia.
    
4. **Reutilización**  
    Un mismo servicio puede ser usado por múltiples aplicaciones.
    
5. **Composición**  
    Servicios simples se pueden orquestar para formar procesos más complejos.
    

---

## **3. Relación con programación distribuida**

- **Modelo cliente–servidor multicapa**:  
    El servicio actúa como **servidor**, el consumidor como **cliente**.
    
- **RPC remoto**:  
    Invocar un servicio es como hacer un **Remote Procedure Call** (RPC), solo que con protocolos estandarizados (SOAP/HTTP, REST/HTTP).
    
- **Paso de mensajes**:  
    La invocación y la respuesta se serializan como mensajes estructurados (XML, JSON, etc.) que viajan por la red.
    

---

## **4. Tecnologías típicas**

- **SOAP (Simple Object Access Protocol)**  
    Basado en XML, muy usado en SOA empresarial. Contratos definidos en WSDL.
    
- **REST (Representational State Transfer)**  
    Usa HTTP con JSON/XML, más ligero que SOAP.
    
- **ESB (Enterprise Service Bus)**  
    Middleware (como SAP PI, MuleSoft, WSO2) que interconecta servicios, hace transformación de mensajes y orquestación.
    
- **BPEL/BPMN**  
    Lenguajes para definir procesos que orquestan múltiples servicios.
    

---

## **5. Ejemplo de arquitectura SOA**

1. **Servicio de facturación** expone una API SOAP.
    
2. **Servicio de inventario** expone una API REST.
    
3. **Servicio de clientes** expone una API SOAP.
    
4. Un **orquestador ESB** (como SAP PI o MuleSoft) coordina:
    
    - Llama a inventario para confirmar stock.
        
    - Llama a facturación para emitir factura.
        
    - Llama a clientes para enviar confirmación.
        
5. Todo se hace vía mensajes XML/JSON sobre HTTP.
    

---

## **6. Comparación con otros modelos**

- **SOA vs. Kafka (event-driven)**  
    SOA suele ser _request–response_, orientado a procesos; Kafka es _publish–subscribe_, orientado a eventos.
    
- **SOA vs. microservicios**  
    Microservicios son una evolución de SOA más ligera, con despliegue independiente y generalmente usando REST/JSON y mensajería ligera.
    

---

Si quieres, puedo prepararte **un esquema visual** donde muestre SOA, sus servicios, y cómo encajan SAP PI, MuleSoft y Kafka dentro de una arquitectura SOA moderna.  
¿Quieres que lo arme?