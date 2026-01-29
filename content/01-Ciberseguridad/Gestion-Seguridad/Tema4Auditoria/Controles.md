---
title: "Controles"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Vamos a desarrollar qué son los **controles** en el ámbito de la **seguridad de la información**, su clasificación, ejemplos y cómo se aplican en normativas como **ENS, ISO 27001, NIS2** o **RGPD**.

---

## ️ ¿Qué son los controles en seguridad?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Los **controles de seguridad** (también llamados **medidas de seguridad**) son:

> **Acciones, mecanismos, herramientas o políticas destinadas a reducir riesgos o proteger los activos de información frente a amenazas**.

Su objetivo es **prevenir, detectar, corregir o mitigar incidentes**, asegurando la **confidencialidad, integridad y disponibilidad (CIA)** de la información.

---

##  Clasificación por función

|Tipo de control|Función principal|Ejemplos|
|---|---|---|
|**Preventivo**|Evita que ocurra un incidente|Cortafuegos, control de acceso, formación|
|**Detectivo**|Permite identificar o registrar un incidente|IDS/IPS, SIEM, logs, DLP, alertas|
|**Correctivo**|Reduce impacto o corrige tras el incidente|Backup y restauración, parcheo urgente, plan de respuesta|
|**Disuasorio**|Desincentiva comportamientos no deseados|Avisos legales, cámaras, políticas estrictas|
|**Recuperación**|Restaura servicios tras una crisis|Plan de Continuidad (BCP), DRP, HA|

---

##  Clasificación según naturaleza

###  Controles **técnicos**

- Implementados mediante tecnología.
    
- Ejemplo: cifrado, antivirus, MFA, segmentación de red.
    

###  Controles **organizativos**

- Basados en procedimientos, políticas y estructuras.
    
- Ejemplo: política de seguridad, roles definidos, formación.
    

###  Controles **físicos**

- Protegen los activos tangibles.
    
- Ejemplo: cerraduras, acceso biométrico, videovigilancia.
    

---

##  Controles según normas

###  **ISO/IEC 27001 – Anexo A (2022)**

Clasifica 93 controles en 4 grandes grupos:

1. **Organizativos** (ej: roles y responsabilidades)
    
2. **Personas** (ej: formación, concienciación)
    
3. **Físicos** (ej: control de acceso físico)
    
4. **Tecnológicos** (ej: protección contra malware, cifrado)
    

 Cada control tiene un objetivo, medidas, y a veces referencias cruzadas con otras normas.

---

###  **ENS (Esquema Nacional de Seguridad – RD 311/2022)**

Organiza los controles en:

- **Marco organizativo**: políticas, funciones, concienciación, auditoría
    
- **Marco operacional**: análisis de riesgos, plan de continuidad, monitorización
    
- **Medidas de protección**: accesos, cifrado, seguridad física, gestión de incidentes
    

Cada control tiene nivel **Básico, Medio o Alto** y se implementa según el nivel de criticidad del sistema.

---

###  **NIS2 y DORA**

Ambas normativas **no detallan controles específicos**, pero **exigen que existan controles técnicos y organizativos proporcionados al riesgo**:

- Análisis de riesgos
    
- Autenticación fuerte (MFA)
    
- Control de acceso
    
- Gestión de vulnerabilidades
    
- Registro y auditoría
    

---

###  **RGPD**

Requiere **"medidas técnicas y organizativas apropiadas"**, como:

- Cifrado
    
- Control de accesos
    
- Trazabilidad
    
- Seudonimización
    
- Evaluaciones de impacto (DPIA)
    

---

##  Control ≠ Política

|Elemento|¿Qué es?|Ejemplo|
|---|---|---|
|**Política**|Declaración de alto nivel sobre seguridad|“La información debe estar protegida”|
|**Control**|Acción específica que implementa la política|“Se usará autenticación multifactor (MFA)”|

---

##  Conclusión

> Los **controles** son el corazón operativo de la seguridad de la información.  
> Definen **qué se hace en la práctica para reducir riesgos** y mantener los sistemas protegidos.  
> Toda organización que quiera cumplir ENS, ISO 27001, RGPD, NIS2 o DORA necesita definir, justificar, aplicar y revisar sus **controles** con base en análisis de riesgos.

---

¿Quieres que te prepare una tabla con controles organizativos y técnicos típicos según ENS o ISO? ¿O un modelo de declaración de aplicabilidad (SoA) como parte de un SGSI?