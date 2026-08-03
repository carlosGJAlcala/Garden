---
title: "Riesgo De La Auditoria"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---

# Riesgo de la Auditoría

Nota técnica que combina lo explicado en el documento `MUCS-FGSI-T4.pdf` con buenas prácticas internacionales (ISO, NIST, ISACA).


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/COBIT|COBIT]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

###  ¿Qué es?

El **riesgo de auditoría** es la **posibilidad de que los auditores no detecten errores, deficiencias o incumplimientos significativos** en el sistema evaluado, y que por tanto emitan **una conclusión incorrecta**, como declarar una conformidad cuando en realidad hay una no conformidad grave.

Este concepto es crítico porque **una auditoría nunca puede garantizar el 100% de seguridad o cumplimiento**, pero sí busca reducir los riesgos asociados a un error de diagnóstico.

---

###  Tipos de riesgo que componen el riesgo de auditoría

El riesgo total se calcula como:

Riesgo de Auditorıˊa=Riesgo de Control×Riesgo de Deteccioˊn\text{Riesgo de Auditoría} = \text{Riesgo de Control} \times \text{Riesgo de Detección}

#### 1.  **Riesgo de Control**

Es el **riesgo inherente al sistema auditado**. Se refiere a la posibilidad de que los **controles existentes no sean eficaces o estén mal diseñados**, y por tanto **no prevengan o detecten** desviaciones importantes. Ejemplos:

- Políticas de seguridad sin aplicar
    
- Falta de segregación de funciones
    
- Firewalls mal configurados
    

 No depende del auditor, sino del entorno que audita.

#### 2.  **Riesgo de Detección**

Es la **posibilidad de que el auditor no detecte una no conformidad** que sí existe, **a pesar de que realice pruebas**. Puede deberse a:

- Muestreo insuficiente
    
- Falta de profundidad en el análisis
    
- Falta de experiencia o formación del auditor
    
- Uso inadecuado de herramientas
    

 Este sí **depende directamente del auditor y su metodología**.

---

###  Objetivo del auditor

El auditor debe **minimizar el riesgo de detección** todo lo posible, mediante:

- Buen diseño del plan de auditoría
    
- Selección adecuada de muestras
    
- Uso de herramientas de escaneo y automatización
    
- Aplicación de pruebas sustantivas y de cumplimiento
    
- Trabajo colaborativo con expertos técnicos
    

 _“Una auditoría no busca eliminar el riesgo, sino reducirlo a un nivel aceptable y documentado.”_

---

###  Cómo se gestiona en la práctica

- Se aplican **criterios de materialidad**: no todo fallo es crítico. Se evalúa el **impacto y la probabilidad**.
    
- Se justifica por escrito el enfoque: “no se detectaron hallazgos significativos bajo las condiciones analizadas”.
    
- En entornos como ISO 27001, la **gestión del riesgo** es el eje principal, y esto se traslada también a la auditoría.
    

---

###  Riesgo residual en la auditoría

Incluso con todo el proceso bien hecho, siempre puede quedar un **riesgo residual**, por ejemplo:

- Cambios realizados después de la auditoría
    
- Fallos humanos no detectables en la muestra
    
- Controles que funcionan pero no están documentados
    

Por eso, los informes de auditoría **no suelen decir “todo está bien”, sino que “no se detectaron desviaciones importantes según el alcance y criterios establecidos”.**

---

###  En normas y marcos

- **ISO 19011**: guía de auditoría, trata el riesgo de auditoría desde la planificación.
    
- **COBIT**: relaciona riesgos de negocio y TI; incluye evaluación del riesgo como parte de su dominio APO12.
    
- **ISACA (CISA)**: en su formación sobre auditores de sistemas, trata el riesgo de auditoría como un pilar.
    

---