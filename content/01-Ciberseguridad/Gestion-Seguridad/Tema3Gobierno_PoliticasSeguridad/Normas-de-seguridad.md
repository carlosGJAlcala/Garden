---
title: "Normas De Seguridad"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema3gobierno_politicasseguridad
---
Perfecto. Vamos a desarrollar a fondo el concepto de **normas de seguridad**, su papel dentro de un sistema de gestión (como un SGSI basado en ISO 27001), sus características y su relación con políticas y procedimientos.

---

##  ¿Qué son las normas de seguridad?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

Las **normas de seguridad de la información** son **documentos internos que especifican reglas obligatorias** que los miembros de una organización deben seguir para cumplir con las políticas de seguridad aprobadas.

> Responden a la pregunta: **“¿Qué debemos hacer exactamente para cumplir la política de seguridad?”**

---

##  Ubicación en la jerarquía documental del SGSI

En un SGSI típico, la jerarquía de documentos es:

```
 Políticas → qué queremos ser
    ↳  Normas → qué hay que hacer
        ↳ ️ Procedimientos → cómo hacerlo
            ↳  Registros y evidencias
```

- **Política**: visión estratégica, compromiso de la dirección.
    
- **Norma**: reglas operativas obligatorias (de aplicación general o específica).
    
- **Procedimiento**: explica paso a paso cómo aplicar la norma.
    
- **Registro**: prueba de cumplimiento (evidencia documental).
    

---

##  Ejemplos de normas de seguridad

###  Normas organizativas:

- Norma de control de accesos
    
- Norma de clasificación de la información
    
- Norma de gestión de activos
    
- Norma de uso aceptable (correo, web, dispositivos móviles)
    

###  Normas técnicas:

- Norma de configuración segura de servidores y endpoints
    
- Norma de gestión de vulnerabilidades y parches
    
- Norma de backup y restauración
    
- Norma de gestión de identidades
    

###  Normas legales y de cumplimiento:

- Norma de protección de datos personales (RGPD)
    
- Norma de retención de logs y trazabilidad (ENS, ISO)
    
- Norma de respuesta ante incidentes
    

---

##  Características de una buena norma

Una norma de seguridad debe ser:

|Criterio|Descripción|
|---|---|
|**Clara**|Lenguaje comprensible, directo, sin ambigüedades|
|**Obligatoria**|De cumplimiento exigible, no meramente orientativa|
|**Aplicable**|Adaptada al entorno real de la organización|
|**Alineada**|Debe responder directamente a una política superior|
|**Auditada**|Sus resultados deben poder verificarse y dejar evidencia|
|**Versionada**|Control de cambios, fechas, responsables y revisiones periódicas|

---

##  Normas como instrumento de cumplimiento

Las normas ayudan a cumplir:

- **ENS (Esquema Nacional de Seguridad)**: exige disponer de medidas organizativas y técnicas regladas (MP, OP, PR…)
    
- **ISO/IEC 27001 y 27002**: en los controles del Anexo A (ej. A.9.1.1 Control de acceso basado en política)
    
- **RGPD**: sobre privacidad y deber de información
    
- **NIS2 y DORA**: exigencias de gobernanza y control formal
    

---

##  Diferencia entre norma y procedimiento

|Elemento|Contenido|Nivel de detalle|Obligatorio|
|---|---|---|---|
|**Norma**|Qué hacer y qué está permitido|Medio| Sí|
|**Procedimiento**|Cómo hacerlo paso a paso|Alto| Sí|
|**Guía**|Recomendaciones o buenas prácticas|Bajo (orientativo)| Opcional|

---

##  Conclusión

> Las **normas de seguridad** son reglas internas formales que **convierten las políticas estratégicas en acciones obligatorias** y medibles.  
> Son la **pieza clave** para asegurar la coherencia, el cumplimiento y la mejora continua en un SGSI maduro.

---

¿Te gustaría que te prepare un modelo editable de una norma de seguridad (por ejemplo, control de accesos, uso aceptable o clasificación de activos) según ISO 27001 o ENS?