---
title: "La Red Sara"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

> **Relacionado**: [[03-Desarrollo-Software/Distribuido/SAP_PI/Facturae|Facturae]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

La **Red SARA** (Sistema de Aplicaciones y Redes para las Administraciones) es, en esencia, la **columna vertebral de las comunicaciones electrónicas entre las Administraciones Públicas españolas**. Su misión no es solo “conectar” técnicamente, sino también estandarizar, securizar y agilizar el intercambio de información para trámites administrativos y servicios electrónicos.

Te lo desgloso en profundidad:

**1. Origen y finalidad**  
Fue creada por el Ministerio de Administraciones Públicas (hoy Ministerio para la Transformación Digital y de la Función Pública) para dar cumplimiento a la Ley 11/2007 y, posteriormente, a la Ley 39/2015 y la Ley 40/2015, que establecen el derecho y obligación de relacionarse electrónicamente con la Administración y el principio de “una sola vez” (no pedir al ciudadano datos que ya obran en poder de la Administración).

**2. Qué es realmente**  
Es una **red privada de ámbito nacional**, aislada de Internet y con un conjunto de **servicios comunes** para las Administraciones. Estos servicios incluyen:

- Intercambio seguro de datos (cifrado y autenticado).
    
- Catálogo de servicios y aplicaciones compartidas.
    
- Mecanismos de interoperabilidad semántica y técnica (basados en el Esquema Nacional de Interoperabilidad – ENI).
    
- Acceso a plataformas horizontales como **Cl@ve**, **Notific@**, **SIR** (Sistema de Interconexión de Registros), **DIR3** (directorio común de unidades administrativas), **SIA** (sistema de inventario de procedimientos) o **PSIS** (Plataforma de Servicios de Intermediación).
    

**3. Cobertura y conexiones**  
Todas las Administraciones (AGE, CCAA, diputaciones, cabildos, ayuntamientos) están conectadas a esta red, ya sea directamente o a través de nodos intermedios. El acceso está restringido a organismos públicos y entidades con convenio específico. No es una red abierta para cualquier empresa.

**4. Relación con los ciudadanos y empresas**  
Las empresas no se “conectan” a Red SARA de forma directa. Lo que hacen es interactuar con plataformas públicas que están **detrás** de Red SARA. Por ejemplo, cuando una empresa envía facturas electrónicas (Facturae) al punto general de entrada de facturas de una Administración, esta transmisión puede viajar internamente por Red SARA. Lo mismo ocurre con notificaciones electrónicas, verificaciones de datos en la AEAT o en la Seguridad Social, etc.

**5. Seguridad**  
La Red SARA aplica el **Esquema Nacional de Seguridad (ENS)**, con segmentación de redes, cifrado de extremo a extremo, autenticación fuerte, monitorización y trazabilidad. Las conexiones se realizan desde centros de datos certificados, normalmente a través de líneas dedicadas o túneles cifrados IPsec gestionados por el Centro de Soporte de Red SARA.

**6. Ventajas**

- Evita duplicidades en la petición de documentos.
    
- Reduce plazos y costes administrativos.
    
- Aumenta la seguridad frente a la exposición en Internet.
    
- Facilita la automatización de procesos interadministrativos.
    
- Cumple con las leyes de interoperabilidad y seguridad de la información.
    

En la práctica, **Red SARA es para las Administraciones lo que una red corporativa privada es para una gran empresa**, pero a escala nacional y con interoperabilidad garantizada entre entidades muy diferentes.

Si quieres, puedo prepararte un **esquema técnico de cómo fluye la comunicación desde una empresa, pasando por un portal público, hasta un servicio que está detrás de Red SARA** para que visualices cómo se integra todo.