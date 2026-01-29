---
title: "Actividad 1.8  Análisis de recursos de la estrategia"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
---

## Actividad 1.7: Marcos de gestión IT



> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/COBIT|COBIT]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Actividad 1.7: Marcos de gestión IT
Revisa uno de los siguientes marcos de gestión IT y resúmelo en tres minutos
(Origen, año, en qué aspectos IT se enfoca, esquema general…..).

### **COBIT (Control Objectives for Information and Related Technologies)**

- **Origen y año:** Creado por ISACA en 1996.
- **Enfoque:** Gobernanza y gestión de TI, asegurando que la tecnología esté alineada con los objetivos estratégicos de la organización.
- **Esquema general:** Basado en principios de planificación, adquisición, implementación, entrega, monitoreo y evaluación.
- **Relaciones:** Se integra con **ISO 27001/27002** y **NIST SP 800-53** para control de seguridad y gestión de riesgos.

---

### **ISO/IEC 27002**

- **Origen y año:** Publicado por la **ISO** e **IEC** en 2005 (basado en el estándar BS 7799).
- **Enfoque:** Seguridad de la información mediante controles específicos para garantizar **confidencialidad, integridad y disponibilidad**.
- **Esquema general:** Proporciona un conjunto de **controles de seguridad** agrupados en áreas como gestión de activos, control de acceso, seguridad física, criptografía, etc.
- **Relaciones:**
    - Complementa **ISO 27001**, que define el Sistema de Gestión de Seguridad de la Información (SGSI).
    - Base para otros estándares como **CIS 20** y **PCI-DSS**.
    - Equivalente en EE.UU.: **NIST SP 800-53**.

---

### **ISO/IEC 27001**

- **Origen y año:** Publicado por la ISO en 2005, con actualizaciones posteriores.
- **Enfoque:** Gestión de la seguridad de la información mediante un sistema estructurado de políticas, procedimientos y auditorías.
- **Esquema general:** Define requisitos para establecer, implementar, mantener y mejorar un SGSI.
- **Relaciones:**
    - **CIS 20** es una **reducción de ISO 27001** que se centra en los controles más efectivos, permitiendo **reducir el 80% de los riesgos** con las primeras medidas.
    - **PCI-DSS** es una especialización de ISO 27001, pero enfocado en el sector financiero y los datos de tarjetas de pago.
    - **ENS (Esquema Nacional de Seguridad)** en España tiene mapeos con **ISO 27001** para adaptar los controles a la normativa nacional.

---

### **NIST SP 800-171**

- **Origen y año:** Publicado por el **NIST** en 2015.
- **Enfoque:** Protección de información no clasificada controlada (CUI) en entidades privadas que trabajan con el gobierno de EE.UU.
- **Esquema general:** Controles de seguridad agrupados en 14 familias, como control de acceso, autenticación, seguridad física, monitoreo continuo, etc.
- **Relaciones:**
    - Derivado de **NIST SP 800-53**, pero simplificado para empresas privadas con contratos gubernamentales.
    - Compatible con **ISO 27001**.

---

### **HIPAA (Health Insurance Portability and Accountability Act)**

- **Origen y año:** EE.UU., 1996.
- **Enfoque:** Protección de datos de salud electrónicos en hospitales, clínicas y aseguradoras.
- **Esquema general:** Se compone de reglas de privacidad, seguridad y notificación de incumplimientos.
- **Relaciones:**
    - Comparte principios con **ISO 27001/27002** en seguridad de la información.
    - Similar a **NIST SP 800-53** en cuanto a controles técnicos.

---

### **NIST SP 800-53**

- **Origen y año:** Publicado por el **NIST** en 2005, actualizado continuamente.
- **Enfoque:** Seguridad y privacidad en sistemas de información del gobierno de EE.UU.
- **Esquema general:** Proporciona un catálogo detallado de controles de seguridad organizados en familias como control de acceso, auditoría, identificación y autenticación, etc.
- **Relaciones:**
    - Es la base de **NIST SP 800-171**.
    - Se alinea con **ISO 27002** en términos de controles de seguridad.
    - **ENS en España** es el equivalente a **NIST SP 800-53**, pero adaptado al contexto europeo.

---

### **CIS 20 (Center for Internet Security Critical Security Controls)**

- **Origen y año:** Publicado por el **CIS** en 2008.
- **Enfoque:** Controles de seguridad esenciales para mitigar las amenazas cibernéticas más comunes.
- **Esquema general:** 20 controles agrupados en controles **básicos, fundacionales y organizacionales**, que incluyen gestión de activos, control de acceso, protección de datos y detección de amenazas.
- **Relaciones:**
    - **Reducción de ISO 27001**, enfocándose en los controles más efectivos para reducir **el 80% de los riesgos iniciales**.
    - Se complementa con **NIST SP 800-53** y **ISO 27002**, proporcionando una **implementación más práctica** de seguridad.

---

### **PCI-DSS (Payment Card Industry Data Security Standard)**

- **Origen y año:** Creado por el **PCI Security Standards Council** en 2004.
- **Enfoque:** Protección de datos de tarjetas de pago y transacciones electrónicas.
- **Esquema general:** 12 requisitos principales, como mantener una red segura, proteger los datos del titular de la tarjeta, implementar medidas de control de acceso y monitoreo continuo.
- **Relaciones:**
    - **Especialización de ISO 27001**, enfocada en bancos y entidades financieras.
    - Coincide con **ISO 27002** en gestión de seguridad y con **NIST SP 800-53** en controles técnicos.

---

### **ENS (Esquema Nacional de Seguridad - España)**

- **Origen y año:** Publicado por el Gobierno de España en 2010.
- **Enfoque:** Seguridad en la administración pública y en organizaciones que manejan datos del gobierno español.
- **Esquema general:** Define medidas de seguridad en tres niveles (básico, medio y alto), con controles organizativos, operacionales y técnicos.
- **Relaciones:**
    - **Equivalente a NIST SP 800-53 en EE.UU.**, pero adaptado a la normativa europea.
    - **Tiene mapas de relación con ISO 27001**, facilitando su implementación en empresas que operan en Españ

# Actividad 1.8  Análisis de recursos de la estrategia


###  Cultura

La cultura es importante porque las empresas están formados por personas y son estas las que lo llevan acabo los procesos y manejan dichas tecnologías.
El estratega que es aquel que va llevar la estrategia para reducir el riesgo, tiene que tener en cuenta los siguientes aspectos. En cuento a liderazgo  si la dirección da ejemplo de dichas de políticas, rendición de cuentas ante posibles consecuencias e incumpliese. Empoderar a los trabajadores pero sin sacrificar la seguridad y trabajar en campañas de concienciación.  
###  Servicios externos 

Se centra en los servicios terceros basados en (IaaS, PaaS, SaaS), que se terciarían y destacan la importancia en manejar los riesgos que se consiguen al tener que tratar con terceros.
Es útil porque plantea el concepto de third-party risk management, que permite mitigar las amenazas de los proveedores externos, haciendo que la compañía o sector terciario cumpla los requisitos de seguridad de dicha compañía para poder interactuar.
Un aspecto interesante es que hace diferencia entre terceros, las organizaciones contratadas, y los cuartos, que son empresas contratadas por las empresas terciarias. Tomando esto en cuenta, se puede tener una visión más profunda en seguridad de las empresas tanto subcontratadas como las subcontratadas de estas, haciendo una cadena de seguridad.
### Auditoría 

Es importante tener información del estado anterior y del estado actual de la situación para tener una visión de los resultados de los procedimientos y ver las vulnerabilidad existentes  para poder prepararse a situaciones criticas.

Es útil como establece el marco en el que el estratega tiene que conocer que a continuación, explicaré cuales son los cuatros puntos que siguen. Primero, el objetivo, que por el cual se hace la auditoria, la situación en actual y anterior. Segundo, la capacidad que tienen los auditores su experiencia y su nivel de conocimiento. Por último la metodología que se lleva a cabo.