---
title: "Cis Top 18"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Vamos a explicar qué es el marco **CIS Controls Top 18**, su estructura, objetivos y por qué es uno de los marcos de **ciberseguridad técnica más prácticos, priorizados y reconocidos internacionalmente**.

---

##  ¿Qué es CIS?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**CIS (Center for Internet Security)** es una organización sin ánimo de lucro que desarrolla **guías, controles y benchmarks de seguridad** para proteger sistemas frente a amenazas reales.

Su publicación más importante es:

> **CIS Critical Security Controls v8** – conocidos como **CIS Top 18**

---

##  ¿Qué son los CIS Controls Top 18?

Son un conjunto de **18 controles prioritarios de ciberseguridad** que representan **las mejores prácticas técnicas y operativas** que una organización debería aplicar para reducir su **superficie de ataque y exposición al riesgo**.

> Se enfocan en proteger activos, redes, usuarios, aplicaciones y datos **contra amenazas conocidas**, como malware, ransomware, accesos indebidos y brechas.

---

##  Estructura de los CIS Top 18

Organizados en **tres grupos según nivel de madurez**:

###  **IG1 (Implementation Group 1)** → Nivel básico (pymes, esenciales)

###  **IG2** → Nivel intermedio (TI medianamente gestionada)

### **IG3** → Nivel avanzado (entornos regulados, alta criticidad)

Cada control se desglosa en **salidas específicas (Safeguards)** que se implementan según el grupo.

---

##  Lista de los 18 CIS Controls v8

|Nº|Control|
|---|---|
|01|**Inventario y control de activos hardware**|
|02|**Inventario y control de activos software**|
|03|**Protección de datos**|
|04|**Gestión segura de configuraciones**|
|05|**Gestión de cuentas y acceso (identidades)**|
|06|**Gestión de accesos (privilegios)**|
|07|**Protección de endpoints de usuario**|
|08|**Protección de dispositivos y redes (firewalls, routers)**|
|09|**Gestión de vulnerabilidades**|
|10|**Capacitación en seguridad (concienciación)**|
|11|**Seguridad de servicios de red**|
|12|**Defensa contra malware**|
|13|**Copia de seguridad y recuperación (resiliencia)**|
|14|**Seguridad en aplicaciones**|
|15|**Control de acceso a servicios**|
|16|**Monitoreo y auditoría de actividad**|
|17|**Capacidad de respuesta ante incidentes**|
|18|**Pruebas de seguridad y ejercicios continuos (Red Team)**|

---

##  Ventajas de los CIS Controls

-  Priorizados según amenazas reales (datos de ataques, MITRE ATT&CK…)
    
-  Muy **prácticos y accionables**
    
-  Escalables según el tamaño de la organización
    
-  Compatibles con ENS, ISO 27001, NIST CSF, DORA, NIS2…
    
-  Usados en entornos públicos, privados y en gobiernos
    

---

##  Relación con otros marcos

|Marco|Relación con CIS Controls|
|---|---|
|**ISO 27001**|CIS puede usarse para implementar controles técnicos del Anexo A|
|**ENS**|Muchos controles CIS coinciden con medidas organizativas y operativas|
|**NIST CSF**|CIS es más táctico y técnico, y encaja como capa inferior|
|**MITRE ATT&CK**|CIS protege frente a técnicas específicas de adversarios reales|
|**DORA / NIS2**|Apoyan el uso de controles prácticos como CIS en entornos críticos|

---

##  Ejemplo práctico

Una pequeña empresa puede comenzar por implementar:

- CIS 01 → Inventario básico de dispositivos
    
- CIS 05 → Control de accesos y MFA
    
- CIS 07 → Antivirus y protección EDR
    
- CIS 10 → Formación básica de usuarios
    
- CIS 13 → Backups verificados
    

Con esto ya cubre la mayoría de los ataques comunes como phishing, ransomware o accesos no autorizados.

---

##  Conclusión

> Los **CIS Top 18** son un marco de referencia técnico y priorizado que permite **implementar seguridad de forma gradual, eficiente y demostrable**, desde las capas más básicas hasta estrategias avanzadas.  
> Son ideales para **empresas en crecimiento, AAPP pequeñas, proveedores TIC** o proyectos que necesitan una guía clara sin depender exclusivamente de normas complejas.

---

¿Te gustaría que te prepare una tabla comparativa entre los controles CIS y los del ENS o ISO 27001? ¿O una checklist editable con los controles CIS IG1 para autoevaluación rápida?