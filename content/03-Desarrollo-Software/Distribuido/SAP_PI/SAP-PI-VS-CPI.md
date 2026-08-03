---
title: "Sap Pi Vs Cpi"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - sap_pi
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/Salesforce|Salesforce]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/SAP-PI|SAP PI]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]].

SAP **PI** (_Process Integration_, antes llamado SAP XI — Exchange Infrastructure) y **SAP CPI** (_Cloud Platform Integration_, ahora **SAP Integration Suite**) cumplen el mismo objetivo general: integrar aplicaciones y datos entre sistemas SAP y no SAP.  
Pero están diseñados para épocas, arquitecturas y necesidades distintas.

---

**1. Enfoque y arquitectura**

- **SAP PI/PO** (_Process Orchestration_ cuando incluye BPM y BRM) es un middleware **on-premise**. Vive en tus servidores, tú lo instalas, configuras y mantienes. Trabaja muy bien con escenarios internos y redes corporativas cerradas.
    
- **SAP CPI** es un servicio **cloud** en SAP BTP. No requiere instalación física, SAP gestiona la infraestructura, y está pensado para integraciones híbridas y nube-a-nube.
    

---

**2. Modelo de despliegue**

- **SAP PI**: modelo tradicional, requiere hardware, sistema operativo, base de datos y mantenimiento por parte del cliente.
    
- **SAP CPI**: SaaS gestionado por SAP, sin que el cliente se preocupe de servidores o actualizaciones.
    

---

**3. Flexibilidad y escalabilidad**

- **SAP PI**: escalado limitado por tu infraestructura local, los upgrades suelen ser más complejos.
    
- **SAP CPI**: escalado dinámico según demanda, actualizaciones automáticas y acceso inmediato a nuevas funciones.
    

---

**4. Adaptadores y conectividad**

- **SAP PI**: gran soporte para adaptadores SAP clásicos (IDoc, RFC, File, JDBC, SOAP), muy orientado a entornos SAP puros.
    
- **SAP CPI**: además de los adaptadores SAP, trae conectores cloud listos para Salesforce, SuccessFactors, Ariba, Concur, REST, OData, SFTP, y APIs públicas/privadas, más integración nativa con arquitecturas _event-driven_.
    

---

**5. Librerías y contenido preconfigurado**

- **SAP PI**: incluye escenarios preconfigurados, pero la mayoría son para entornos SAP-SAP o SAP-legacy.
    
- **SAP CPI**: gran catálogo en **SAP API Business Hub** con iFlows listos para integraciones SAP-SaaS, APIs públicas y plantillas reutilizables.
    

---

**6. Casos de uso ideales**

- **SAP PI**: cuando toda la integración es interna y la compañía no quiere depender de la nube, o donde hay sistemas SAP antiguos y muchos procesos legacy.
    
- **SAP CPI**: cuando hay que conectar sistemas on-premise con múltiples servicios cloud, o cuando la organización busca flexibilidad y menos mantenimiento de infraestructura.
    

---

**7. Futuro de la plataforma**

- SAP mantiene PI/PO pero no es la apuesta estratégica a largo plazo. La tendencia oficial es migrar a CPI/Integration Suite, sobre todo en entornos S/4HANA y estrategias cloud-first.
    

---

En resumen, **PI es el middleware tradicional on-premise** que todavía se usa en entornos muy controlados, mientras que **CPI es la evolución cloud**, más flexible, escalable y preparada para integraciones híbridas y SaaS.

