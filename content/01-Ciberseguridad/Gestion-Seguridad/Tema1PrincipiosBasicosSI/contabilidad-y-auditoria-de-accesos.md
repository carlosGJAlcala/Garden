---
title: "Contabilidad Y Auditoria De Accesos"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema1principiosbasicossi
---

# Contabilidad y Auditoría de Accesos

Los conceptos de **contabilidad** y **auditoría de accesos** en seguridad de la información forman parte de la "A" final del modelo **Triple A** (Authentication, Authorization, **Accounting**).

## ¿Qué es la contabilidad de accesos (Accounting)?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Rutinas/Horario|Horario]].

La contabilidad de accesos (también llamada **registro o trazabilidad**) es el proceso mediante el cual se **registra quién accede a qué, cuándo, desde dónde, cómo y con qué resultado**.

 Su objetivo es generar evidencia y trazabilidad sobre las actividades realizadas en los sistemas.

---

##  ¿Qué se registra en la contabilidad de accesos?

- **Identidad del usuario** o servicio
    
- **Fecha y hora** del acceso o intento
    
- **Tipo de acceso** (inicio de sesión, modificación, eliminación…)
    
- **Recurso accedido** (fichero, base de datos, aplicación)
    
- **Resultado** (acceso concedido o denegado)
    
- **IP origen / dispositivo / ubicación**
    

Estos datos se guardan en **logs o bitácoras**, que pueden almacenarse localmente o centralizarse en sistemas como:

- **SIEM** (Security Information and Event Management)
    
- **Syslog** o servicios como **AuditD**, **Windows Event Viewer**
    
- **CloudTrail** (en AWS), **Azure Monitor**, etc.
    

---

## ¿Qué es la auditoría de accesos?

La auditoría de accesos es la **revisión periódica o reactiva de esos registros** de actividad para:

- Detectar **comportamientos anómalos o no autorizados**
    
- Verificar el cumplimiento de políticas y controles de seguridad
    
- Investigar **incidentes de seguridad**
    
- Cumplir con normativas (ENS, ISO 27001, RGPD, NIS2…)
    

---

##  Ejemplo típico de auditoría

> Un auditor revisa los logs del sistema y detecta que el usuario `admin_db` accedió fuera de horario desde una IP externa. Se analiza si fue una actividad legítima, un fallo de configuración o un compromiso de credenciales.

---

##  Normativas que exigen contabilidad y auditoría

- **ENS**: exige medidas de trazabilidad y conservación de registros (MP.LO.3, OP.MON.1)
    
- **ISO/IEC 27001**: control A.12.4 (registro y supervisión)
    
- **GDPR**: artículo 32 exige registro de accesos a datos personales
    
- **NIS2 y DORA**: exigen mecanismos de monitoreo, evidencia y respuesta
    

---

##  Buenas prácticas

- Centralizar logs (SIEM, EDR, XDR)
    
- Activar el **registro detallado** en sistemas críticos
    
- Proteger la **integridad de los logs** (WORM, hash, firmas)
    
- Establecer políticas de **retención y revisión periódica**
    
- Automatizar alertas sobre **comportamientos anómalos**
    

---

## Riesgos si no se audita

- No detectar accesos indebidos
    
- No poder **reconstruir un incidente**
    
- Incumplimiento legal o normativo
    
- No disponer de pruebas en caso de fraude o filtración
    

---

##  Conclusión

> La **contabilidad y auditoría de accesos** son componentes **críticos para garantizar la seguridad, el cumplimiento normativo y la respuesta ante incidentes**.  
> Sin trazabilidad adecuada, una organización **pierde visibilidad** y capacidad de defensa ante amenazas internas o externas.

---