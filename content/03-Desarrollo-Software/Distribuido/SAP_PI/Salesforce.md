---
title: "Salesforce"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - sap_pi
---
Perfecto, vamos con una explicación detallada de **Salesforce** para que tengas una visión completa, desde su concepto hasta cómo se usa y por qué es tan popular.

---

## **1. Qué es Salesforce**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[03-Desarrollo-Software/Distribuido/MuleSoft|MuleSoft]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]].

Salesforce es una **plataforma en la nube de CRM (Customer Relationship Management)** y un ecosistema de aplicaciones empresariales que ayudan a **gestionar las relaciones con clientes, prospectos y socios**.  
Fue fundada en 1999 y fue pionera en ofrecer un CRM completamente **SaaS (Software as a Service)**, sin necesidad de instalar nada localmente.

Su filosofía es **"Customer 360"**: reunir toda la información y las interacciones con un cliente en un único lugar accesible para ventas, marketing, atención al cliente y otros departamentos.

---

## **2. Componentes principales de Salesforce**

Salesforce no es solo un CRM básico; está dividido en **"nubes"** (_clouds_) que cubren diferentes áreas de negocio:

- **Sales Cloud**  
    CRM enfocado en ventas: gestión de leads, oportunidades, cuentas, contactos, pronósticos de ventas y pipeline.
    
- **Service Cloud**  
    Gestión de servicio y atención al cliente: casos, tickets, chat, call center, bases de conocimiento, SLA.
    
- **Marketing Cloud**  
    Automatización de marketing: segmentación, campañas por email/SMS, journeys personalizados, analítica de campañas.
    
- **Commerce Cloud**  
    Comercio electrónico B2B y B2C: catálogos, carritos, pagos, promociones.
    
- **Experience Cloud** (antes Community Cloud)  
    Creación de portales y comunidades para clientes, partners o empleados.
    
- **Analytics Cloud (Tableau CRM)**  
    Visualización y análisis avanzado de datos con IA.
    
- **Integration & Platform (Salesforce Platform)**  
    Desarrollo de apps personalizadas sobre la plataforma usando **Apex** (lenguaje propio similar a Java), **Lightning Components**, y herramientas low-code como Flow Builder.
    
- **Industries (Vlocity)**  
    Soluciones verticales preconfiguradas para sectores como salud, telecomunicaciones, banca o sector público.
    
- **Slack (integrado)**  
    Comunicación interna con integración directa de datos y procesos de Salesforce.
    

---

## **3. Características técnicas clave**

- **100% en la nube**: accesible desde cualquier dispositivo con conexión a internet.
- **Arquitectura multi-tenant**: múltiples clientes comparten la misma infraestructura pero con datos completamente aislados.
- **Personalización**:
    - _Declarativa_: sin código, mediante configuraciones (campos, flujos, reglas, reportes).
    - _Programática_: con **Apex** (back-end) y **Lightning Web Components** (front-end).
- **Integración**: APIs REST/SOAP, conectores predefinidos, MuleSoft (propiedad de Salesforce) para integración avanzada.
- **AppExchange**: marketplace con miles de aplicaciones y extensiones.
- **Seguridad**: autenticación multifactor, control granular de permisos, cifrado en tránsito y reposo.

---

## **4. Beneficios para las empresas**

- Visión **360º del cliente** en un solo lugar.
- Mejora la productividad de ventas y servicio al cliente.
- Automatización de procesos repetitivos.
- Escalabilidad sin preocuparse por infraestructura.
- Gran ecosistema de integraciones y aplicaciones.
- Actualizaciones automáticas (tres veces al año).

---

## **5. Ejemplo de uso real**

Una empresa de tecnología usa Salesforce así:

1. Marketing Cloud capta leads a través de campañas digitales.
2. Los leads entran automáticamente a Sales Cloud, donde un comercial hace seguimiento.
3. Cuando se convierte en cliente, el contrato y el historial quedan registrados.
4. Service Cloud gestiona tickets de soporte con SLA definidos.
5. Analytics Cloud genera reportes de ventas, satisfacción y efectividad de campañas.

---

## **6. Diferencias con SAP CRM**

- **Salesforce**: nativo en la nube, especializado en experiencia del cliente, muy fuerte en personalización y apps rápidas.
- **SAP CRM**: más integrado con procesos internos de ERP, ideal para empresas que ya usan todo el ecosistema SAP.

---

Si quieres, puedo prepararte **un mapa visual de todas las nubes de Salesforce y cómo se conectan entre sí**, para que veas el ecosistema entero en un solo diagrama.  
¿Quieres que te lo haga?