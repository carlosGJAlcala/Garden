---
title: "Desarrollo de un Plan de Continuidad de Negocio (PCN)"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
---
Aquí tienes la información corregida y expandida:

---

**Security.txt**
  
El archivo `security.txt` es un estándar utilizado para proporcionar información de contacto y directrices sobre cómo reportar vulnerabilidades de seguridad en un sistema o aplicación. Su propósito es facilitar la comunicación entre investigadores de seguridad y las organizaciones para garantizar que las vulnerabilidades sean reportadas de manera eficiente y adecuada. La raíz del archivo contiene la información básica, como los detalles de contacto para que los investigadores puedan notificar sobre las vulnerabilidades descubiertas.

**Caso SolarWinds:**

En el caso de SolarWinds, se produjo un ataque significativo a través de un trojano. La vulnerabilidad fue detectada por un empleado, quien alertó sobre la infección. Este incidente destacó la importancia de contar con protocolos efectivos de reporte y gestión de vulnerabilidades para minimizar el impacto de las brechas de seguridad.

**Cumplimiento de la Seguridad en el Desarrollo:**

El cumplimiento de normas y estándares de seguridad es crucial en cualquier proceso de desarrollo de software. No basta con implementar medidas de seguridad de forma aislada, sino que es necesario integrar controles de seguridad a lo largo de todo el ciclo de vida del desarrollo. De esta forma, se aseguran las actividades del Plan de Continuidad de Negocio (PCN).

---

# **Desarrollo de un Plan de Continuidad de Negocio (PCN)**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/SolarWinds|SolarWinds]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

El Plan de Continuidad de Negocio (PCN) es esencial para garantizar que una organización pueda continuar operando durante y después de un incidente crítico. Para desarrollar un PCN efectivo, se deben establecer políticas que aseguren la continuidad de las actividades del negocio en caso de un evento disruptivo.

**Políticas del PCN y el SGSI:**

Las políticas que forman parte del Sistema de Gestión de Seguridad de la Información (SGSI) deben estar alineadas con los controles necesarios para garantizar que las actividades relacionadas con el PCN se lleven a cabo correctamente. Estos controles son fundamentales para gestionar y mitigar los riesgos asociados con la interrupción de servicios.

**Análisis de Impacto:**

Es importante realizar un análisis de impacto para evaluar las consecuencias de una interrupción en las operaciones de la organización. Este análisis permite identificar qué procesos son críticos y cómo la falta de continuidad en estos procesos puede afectar a la empresa.

---

**Indicadores Clave del PCN:**

El PCN debe incluir una serie de indicadores clave para medir el rendimiento y la efectividad de la recuperación y continuidad. Algunos de los principales indicadores son:

1. **RTO (Recovery Time Objective)**: Es el tiempo máximo permitido para que un proceso se recupere después de una interrupción. Se debe definir de manera clara el objetivo de recuperación para cada proceso crítico de la organización.
    
2. **RPO (Recovery Point Objective)**: Es el punto de restauración de los datos. Define cuánto tiempo de datos puede perderse antes de que la interrupción se considere inaceptable.
    
3. **RCAP (Recovery Capability)**: Es la capacidad de recuperación de la organización, es decir, qué tan rápido puede recuperar un servicio o proceso tras una interrupción.
    
4. **MTD (Maximum Tolerable Downtime)**: Es el tiempo máximo durante el cual la organización puede tolerar la interrupción de un servicio sin que se vean comprometidos los resultados fundamentales del negocio.
    
5. **MTO (Maximum Tolerable Outage)**: Similar al MTD, pero se enfoca más en el tiempo máximo durante el cual un servicio puede estar fuera de servicio antes de que impacte gravemente en la operación de la organización.
    

**Intervalos de Recuperación:**

Es importante definir dos intervalos:

- **Primer intervalo**: El tiempo durante el cual la organización ha sido capaz de reactivar parcialmente el servicio. Durante este tiempo, las operaciones de la empresa aún pueden continuar, pero no de manera completamente normal.
    
- **Segundo intervalo**: El tiempo necesario para que la empresa vuelva a la normalidad total después de un incidente. Esto incluye la restauración completa de los servicios y la resolución de cualquier daño causado por la interrupción.
    

Estos indicadores ayudan a garantizar que el PCN sea lo suficientemente robusto para abordar cualquier interrupción, minimizando el impacto y asegurando una recuperación adecuada.

**Relación entre RTO y MTD:**

El **RTO** debe ser siempre menor que el **MTD**. Si el RTO es superior al MTD, la organización estaría expuesta a un riesgo significativo de que la interrupción afecte de manera irreversible sus operaciones críticas.

---

# Desarrollo del plan de continuidad
