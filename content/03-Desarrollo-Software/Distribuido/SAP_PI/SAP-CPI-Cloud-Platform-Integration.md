---
title: "Sap Cpi Cloud Platform Integration"
date: 2025-01-01
tags:
  - desarrollo-software
---

### **1. Qué es SAP CPI**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/Salesforce|Salesforce]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

SAP Cloud Platform Integration, actualmente rebautizado como parte de **SAP Integration Suite** dentro de **SAP Business Technology Platform (BTP)**, es un servicio en la nube que permite integrar aplicaciones, datos y procesos empresariales entre sistemas **SAP** y **no SAP**, tanto en entornos _on-premise_ como en la nube.

Es la evolución de la integración empresarial que antes se hacía con **SAP PI/PO** (Process Integration/Process Orchestration), pero ahora con un enfoque **cloud-first**, más ligero, escalable y orientado a integraciones rápidas y seguras.

Podrías verlo como un **“middleware como servicio”** gestionado por SAP, diseñado para que las empresas puedan conectar sistemas de forma ágil y sin tener que mantener la infraestructura física.

---

### **2. Principales capacidades**

SAP CPI cubre varias áreas clave:

- **Integración de aplicaciones (Application Integration)**  
    Permite conectar diferentes aplicaciones, ya sean SAP (S/4HANA, SuccessFactors, Ariba, Concur, etc.) o externas (Salesforce, Microsoft Dynamics, etc.), para que los datos fluyan de forma coherente entre ellas.
    
- **Integración de datos (Data Integration)**  
    Facilita la sincronización, transformación y migración de datos entre plataformas, soportando diferentes formatos como XML, JSON, CSV, IDoc, etc.
    
- **Integración híbrida (Hybrid Integration)**  
    Conecta entornos _on-premise_ con entornos cloud. Por ejemplo, vincular un SAP ECC local con SAP S/4HANA Cloud.
    
- **API Management y Open Connectors**  
    CPI es parte de un ecosistema más amplio de **Integration Suite**, que también incluye API Management para publicar, proteger y monitorizar APIs, y Open Connectors para conectarse fácilmente a cientos de aplicaciones SaaS.
    

---

### **3. Arquitectura general**

La arquitectura de SAP CPI se basa en tres elementos principales:

1. **Entorno cloud en SAP BTP**  
    CPI se ejecuta completamente en la nube de SAP, y tú accedes a él mediante un navegador, usando un cockpit centralizado para configurar y monitorizar integraciones.
    
2. **iFlows (Integration Flows)**  
    Son diagramas de flujo que definen cómo viaja la información:
    
    - De dónde se recibe el dato (origen)
        
    - Cómo se transforma o procesa
        
    - A dónde se envía (destino)
        
3. **Cloud Connector**  
    Componente que se instala en tu red local para permitir que CPI se comunique de forma segura con sistemas on-premise, sin necesidad de abrir puertos críticos a internet.
    

---

### **4. Características técnicas destacadas**

- **Modelado visual**: interfaz gráfica para construir integraciones arrastrando componentes y definiendo mapeos.
    
- **Amplio catálogo de adaptadores**: REST, OData, SOAP, SFTP, JDBC, IDoc, RFC, HTTP, AS2, entre otros.
    
- **Transformación de datos**: herramientas para mapear y transformar datos entre formatos distintos, incluyendo funciones avanzadas y scripts en Groovy/JavaScript.
    
- **Seguridad integrada**: autenticación OAuth 2.0, certificados X.509, cifrado TLS/SSL, firma digital y gestión de credenciales segura.
    
- **Monitorización y alertas**: panel en tiempo real para ver mensajes procesados, errores y métricas de rendimiento.
    
- **Contenido preconfigurado**: cientos de iFlows listos para usar desde **SAP API Business Hub**.
    
- **Soporte para arquitecturas event-driven**: integración con colas y mensajería basada en eventos.
    

---

### **5. Ejemplos de casos de uso reales**

- Sincronizar datos de clientes entre **SAP S/4HANA** y **Salesforce**.
    
- Integrar **SAP Ariba** con SAP ECC para automatizar compras y pagos.
    
- Enviar datos de RRHH desde **SAP SuccessFactors** a un sistema de nóminas externo.
    
- Recibir información de sensores IoT y enviarla a SAP para análisis.
    
- Migrar datos de un ERP local a la nube de forma escalonada.
    

---

### **6. Ventajas de SAP CPI frente a integraciones tradicionales**

- **Menos mantenimiento**: no requiere servidores ni actualizaciones manuales.
    
- **Escalabilidad automática**: ajusta recursos según la carga.
    
- **Integraciones rápidas** gracias a plantillas y conectores prehechos.
    
- **Seguridad y cumplimiento** bajo estándares internacionales.
    
- **Acceso global** desde cualquier lugar con conexión a internet.
    

---

### **7. Relación con SAP PI/PO**

- SAP PI/PO es el equivalente on-premise de CPI, pero requiere instalación y mantenimiento interno.
    
- CPI es la apuesta estratégica de SAP para integraciones en la nube y entornos híbridos.
    
- Muchos escenarios de PI/PO se están migrando a CPI como parte de la transición a S/4HANA Cloud y la estrategia cloud-first.
    

---

### **8. Licenciamiento y disponibilidad**

SAP CPI forma parte de **SAP Integration Suite**, que se licencia según capacidad (número de conexiones, volumen de mensajes, etc.). Al estar en BTP, se contrata como servicio y se paga por uso o por suscripción.

