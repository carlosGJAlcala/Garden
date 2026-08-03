---
title: "Enunciado"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
---

# Enunciado 

> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Plantear un caso práctico de gestión de riesgos y contestar a las cuestiones de las actividades 2.2_1, 2.2_2, 2.2_3 y 2.2_4 de las transparencias.

Presentar el trabajo individual, en el cual cada uno debe elegir un caso único.

Se recomienda usar principalmente la metodología Magerit, aunque puede usar otras o copiar aspectos que vea interesante de otras.
# **Caso Práctico de Gestión de Riesgos en una Empresa de Comercio Electrónico**

Se analizará la gestión de riegos de una empresa de correo de comercio electrónico  que maneja de datos sensibles clientes.

# **2. Actividad 2.2_1: Evaluación de Activos**

La metodología seleccionada es margarit , escogido dicha metodología porque  la hemos dado en el curso pasado y tengo experiencia con ella.

 Considero que el activo principal es la  base de datos de clientes, porque la empresa maneja datos sensibles de clientes.

Los activos dependientes de la base de datos son los siguientes:

- Servidor de bases de datos
    
- Plataforma de pagos
    
- Servidor web
    
- Sistemas de almacenamiento en la nube
    

**Procedimiento de Evaluación:** Se evaluará la amezanas sabiendo que es la probabilidad de un posibles impacto por la vulnerabilidad ,midiendo como afecta a la confidencialidad , la integridad y la disponibilidad.

---

# **3. Actividad 2.2_2: Listas de Amenazas y Análisis de Riesgos**

**Amenazas Identificadas:**

1. Ataques de inyección SQL
    
2. Robo de credenciales mediante phishing
    
3. Ataques de denegación de servicio (DDoS)
    
4. Filtración de datos por empleados internos
    
5. Fugas de datos en servicios en la nube
    

**Metodología de Análisis de Riesgos:** Se empleará un análisis semicuantitativo, asignando valores del 1 al 5 para la probabilidad e impacto de cada amenaza.

**Gestión del Análisis de Riesgos:** El director de seguridad evaluará los riesgos en coordinación con los responsables de cada activo. Se asignará un nivel de riesgo final en base a la combinación de probabilidad e impacto.

Ejemplo:

|Amenaza|Probabilidad (1-5)|Impacto (1-5)|Nivel de Riesgo|
|---|---|---|---|
|Inyección SQL|4|5|20|
|Phishing|3|4|12|
|DDoS|4|3|12|

---

**4. Actividad 2.2_3: Tratamiento de Riesgos**

**Controles Propuestos:**

1. Implementación de validaciones en la base de datos para evitar inyecciones SQL.
    
2. Autenticación multifactor (MFA) para evitar robos de credenciales.
    
3. Firewall de aplicación web (WAF) para mitigar ataques DDoS.
    
4. Políticas de control de acceso para minimizar fugas de datos internas.
    
5. Cifrado y auditoría de datos almacenados en la nube.
    

**Riesgo Residual:** Luego de aplicar los controles, se reevalúa el riesgo y se mantiene la monitorización constante.

**Decisiones sobre el Tratamiento del Riesgo:** El equipo de seguridad tomará decisiones basadas en la aceptabilidad del riesgo residual y el presupuesto disponible.

---

**5. Actividad 2.2_4: Registro de Riesgos**

**Modelo de Registro de Riesgos:**

|     |                      |         |              |                         |                 |
| --- | -------------------- | ------- | ------------ | ----------------------- | --------------- |
| ID  | Riesgo               | Impacto | Probabilidad | Controles Implementados | Riesgo Residual |
| 01  | Inyección SQL        | Alto    | Alta         | Validaciones y WAF      | Bajo            |
| 02  | Robo de credenciales | Alto    | Media        | MFA y sensibilización   | Bajo            |
| 03  | DDoS                 | Medio   | Alta         | Firewall y mitigación   | Medio           |

Este registro se actualizará periódicamente para reflejar cambios en el entorno de amenazas y efectividad de los controles.

---

**6. Conclusión**

La gestión de riesgos basada en Magerit ha permitido identificar, analizar y mitigar amenazas relevantes para la empresa de comercio electrónico. El uso de un análisis cuantitativo ha facilitado la toma de decisiones, asegurando la protección de los activos más críticos.

