---
title: "Cmm"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Vamos a explicar qué es **CMM (Capability Maturity Model)**, su estructura, para qué se usa en seguridad de la información y cómo se relaciona con la mejora continua y la evaluación de procesos.

---

##  ¿Qué es el CMM?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/COBIT|COBIT]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

**CMM** significa **Capability Maturity Model** o **Modelo de Madurez de Capacidades**.  
Es un modelo que permite **evaluar el grado de madurez de los procesos de una organización**, indicando **cómo de bien definidos, gestionados y optimizados están**.

> Se usa para guiar la **mejora continua** de procesos y determinar **en qué nivel de madurez** se encuentra una empresa u organización.

Fue desarrollado originalmente por el **Software Engineering Institute (SEI)** de Carnegie Mellon para procesos de desarrollo de software, pero **hoy se aplica también a ciberseguridad, gestión de riesgos, SGSI, cumplimiento normativo, etc.**

---

##  Niveles del CMM (clásico de 5 niveles)

|Nivel|Nombre|Descripción breve|
|---|---|---|
|1|**Inicial (ad hoc)**|Procesos caóticos o inexistentes. Reacción por necesidad. Sin previsión.|
|2|**Repetible (estable básico)**|Algunos procesos definidos y repetibles. Gestión reactiva. Documentación mínima.|
|3|**Definido**|Procesos documentados, estandarizados y aplicados de forma consistente.|
|4|**Gestionado (medido)**|Se miden los procesos, se usan métricas, se detectan desviaciones.|
|5|**Optimizado**|Mejora continua, uso de indicadores, innovación, automatización, lecciones aprendidas.|

---

##  ¿Dónde se aplica el CMM en seguridad de la información?

En entornos como:

- **SGSI basados en ISO/IEC 27001**
    
- Evaluación de cumplimiento del **ENS (Esquema Nacional de Seguridad)**
    
- Programas de gestión de riesgos (ej. NIST RMF)
    
- Procesos de continuidad de negocio
    
- Modelos de madurez ENS, COBIT, CMMC o NIST CSF
    

---

##  Ejemplo aplicado a seguridad de accesos

|Nivel|Control de accesos|
|---|---|
|1|Accesos abiertos, sin control ni monitoreo|
|2|Contraseñas por usuario, cambios manuales|
|3|Gestión centralizada, uso de roles (RBAC)|
|4|Logs auditados, autenticación multifactor (MFA)|
|5|Automatización IAM, revisión continua, anomalías detectadas por IA|

---

##  Relación con la mejora continua (PDCA)

El modelo CMM **facilita la implantación progresiva** del ciclo **Plan – Do – Check – Act**:

- **Plan** → Definir procesos
    
- **Do** → Implementarlos
    
- **Check** → Medir, auditar, analizar
    
- **Act** → Corregir, optimizar, innovar
    

---

##  Beneficios de usar CMM

-  Permite hacer un **diagnóstico claro** del estado de los procesos
    
-  Establece **objetivos medibles** de mejora
    
-  Justifica **inversiones en seguridad**
    
-  Demuestra **madurez ante clientes, reguladores y auditorías**
    
-  Facilita la **priorización de recursos**
    

---

## ️ Ejemplos de modelos derivados

- **CMMI**: evolución de CMM para múltiples áreas (desarrollo, servicios, adquisiciones…)
    
- **CMMC (Cybersecurity Maturity Model Certification)**: modelo del Departamento de Defensa de EE.UU.
    
- **CMM de seguridad según NIST CSF o COBIT**: usados para evaluar ciberseguridad empresarial
    
- **Modelo de madurez del ENS (España)**: permite categorizar el cumplimiento de medidas básicas, medias o altas
    

---

##  Conclusión

> El modelo **CMM** permite **medir, entender y mejorar la madurez de los procesos de seguridad**, desde niveles improvisados hasta modelos optimizados.  
> Aplicarlo es clave para construir una **seguridad sostenible, auditable y alineada con los objetivos del negocio**.

---

¿Quieres que te prepare una plantilla tipo Excel para autoevaluar el nivel de madurez CMM en tu SGSI o un área concreta (como gestión de accesos, incidentes o continuidad)?