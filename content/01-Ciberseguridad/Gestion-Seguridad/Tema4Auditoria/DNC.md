---
title: "Dnc"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. A continuación te presento una **nota explicativa expandida sobre la Declaración de No Conformidad (DNC)**, combinando lo que aparece en el documento y añadiendo información clave desde el punto de vista profesional y normativo:

---

##  Declaración de No Conformidad (DNC)


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]].

###  ¿Qué es una DNC?

La **Declaración de No Conformidad (DNC)** es un **documento formal que recoge una desviación respecto a un requisito establecido**, ya sea una norma, un control de seguridad, una política interna o una regulación aplicable. Se trata de uno de los elementos más relevantes que puede generar una auditoría, ya que **marca las áreas donde se ha detectado un incumplimiento claro**.

###  Componentes fundamentales

Una DNC debe contener, como mínimo:

1. **Identificador**: Un código único que permita su seguimiento (por ejemplo: `NC-001-2025`).
    
2. **Referencia al requisito** incumplido (ISO 27001, ENS, políticas internas, etc.).
    
3. **Descripción del hallazgo**: Qué se ha detectado exactamente, de forma clara y objetiva.
    
4. **Nivel de criticidad**: Alto, medio o bajo, en función del impacto en la seguridad.
    
5. **Evidencia que lo respalda**: Documentación, observaciones, logs, entrevistas, etc.
    
6. **Recomendación o acción correctiva sugerida** (puede ser propuesta por el auditado o por el auditor).
    
7. **Estado de resolución**: Si está pendiente, resuelto, en revisión, etc.
    

---

###  Ejemplo (extraído y ampliado del documento):

> **NC-01: Sistema operativo obsoleto en equipos de usuario**  
> **Norma afectada**: ISO/IEC 27001 - Control 8.1.3 (Uso aceptable de activos)  
> **Evidencia**: Se observó que varios equipos continúan operando bajo Windows XP, sistema sin soporte oficial desde 2014.  
> **Nivel de criticidad**: ALTO  
> **Recomendación**: Migrar a una versión soportada del sistema operativo (mínimo Windows 10) y establecer un proceso para asegurar la actualización de los activos.  
> **Estado**: No resuelto

---

###  ¿Por qué es importante?

Las DNC:

- **Obligan a tomar medidas correctoras** documentadas y verificables.
    
- Permiten establecer un **ciclo de mejora continua**, clave en sistemas como ISO 27001 (Plan-Do-Check-Act).
    
- **Tienen un seguimiento posterior**: no basta con reportarlas, hay que validar si fueron resueltas eficazmente.
    

---

###  ¿Qué ocurre después?

Una vez emitida una DNC:

1. Se **notifica al cliente** y se registra formalmente.
    
2. Se **abre un proceso de seguimiento** (que puede implicar acciones correctoras, mitigaciones temporales o justificaciones).
    
3. En una **auditoría de seguimiento**, se verifica si la DNC ha sido cerrada correctamente.
    

En casos de certificación, una DNC grave puede implicar la **suspensión o no concesión de la certificación**.

---

###  DNC vs Observación

|Elemento|DNC|Observación|
|---|---|---|
|¿Existe incumplimiento?|Sí (objetivo y demostrable)|No (pero podría haber un riesgo futuro)|
|¿Requiere acción?|Sí, debe resolverse o mitigarse|Recomendable, pero no obligatorio|
|¿Tiene seguimiento formal?|Sí (código, verificación posterior)|No necesariamente|

---

###  Normativa de referencia

- **ISO/IEC 19011**: Directrices para auditorías de sistemas de gestión. Establece cómo emitir no conformidades.
    
- **ISO/IEC 27001**: Define qué controles son auditables y cuáles son los requisitos mínimos.
    
- **ENS (Esquema Nacional de Seguridad)**: En el contexto español, identifica criterios de conformidad para sistemas públicos.
    

---

Si quieres, también puedo redactarte una **plantilla de DNC** en formato tabla para usar en informes o generar un documento tipo para auditorías reales. ¿Te interesa eso?