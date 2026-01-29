---
title: "Ciclo De Vida Del Desarrollo Del Software Sdlc"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
### **Ciclo de Vida del Desarrollo del Software (SDLC)**

> **Relacionado**: Ver [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-06-diseno-desarrollo-seguro|Diseño de Desarrollo Seguro]] para integrar seguridad. [[01-Ciberseguridad/Fundamentos/owasp|OWASP]] para vulnerabilidades. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Fases-de-auditoria|Auditoría de seguridad]] para pruebas. [[03-Desarrollo-Software/Paradigmas/PARADIGMAS-DE-PROGRAMACION|Paradigmas de programación]].

El **Ciclo de Vida del Desarrollo del Software (Software Development Life Cycle - SDLC)** es un conjunto de fases que guían el desarrollo de un sistema de software desde su concepción hasta su retiro. Su objetivo es mejorar la calidad, reducir costos y asegurar la entrega de software funcional y seguro.

### **Fases del SDLC**

El SDLC se compone de varias fases, cada una con actividades específicas que garantizan un desarrollo estructurado y eficiente.

#### **1. Planificación**

En esta fase se define el propósito del software, los objetivos del proyecto, los requerimientos del cliente y los recursos necesarios. Se evalúan costos, riesgos y se determina la viabilidad del desarrollo.

Actividades clave:

- Análisis de factibilidad (económica, técnica y operativa).
- Definición de alcance y objetivos.
- Asignación de recursos y tiempos.

#### **2. Análisis de Requisitos**

Se recopilan y documentan las necesidades del usuario y las funcionalidades que debe cumplir el software. Esto puede incluir requisitos funcionales y no funcionales (rendimiento, seguridad, usabilidad).

Actividades clave:

- Entrevistas con stakeholders.
- Creación de casos de uso.
- Especificación de requisitos (SRS - Software Requirements Specification).

#### **3. Diseño**

Se define la arquitectura del software y su estructura. Se crean diagramas y modelos que especifican cómo se implementarán los requisitos.

Actividades clave:

- Diseño de arquitectura (monolítica, microservicios, cliente-servidor, etc.).
- Diseño de base de datos.
- Modelado con UML (diagramas de clases, flujo de datos).
- Definición de interfaces de usuario y API.

#### **4. Desarrollo o Implementación**

Se escribe el código del software siguiendo las especificaciones del diseño. Se utilizan metodologías como desarrollo ágil, cascada o DevOps.

Actividades clave:

- Programación en los lenguajes definidos.
- Aplicación de principios como SOLID, DRY y KISS.
- Uso de control de versiones (Git, SVN).
- Aplicación de pruebas unitarias y revisiones de código.

#### **5. Pruebas**

Se validan la funcionalidad, seguridad, rendimiento y compatibilidad del software antes de su implementación.

Tipos de pruebas:

- **Unitarias:** Verifican componentes individuales del código.
- **Integración:** Comprueban la interacción entre módulos.
- **Funcionales:** Evalúan si el software cumple los requisitos.
- **De seguridad:** Identifican vulnerabilidades.
- **De carga y estrés:** Analizan el rendimiento bajo demanda.

#### **6. Implementación o Despliegue**

El software se libera para su uso en el entorno de producción. Puede implementarse de forma progresiva o completa.

Estrategias de despliegue:

- **Big Bang:** Se lanza el sistema completo de una vez.
- **Fases o iteraciones:** Se implementa en etapas.
- **Blue-Green Deployment:** Dos entornos en paralelo para minimizar interrupciones.
- **Canary Release:** Se libera para un grupo reducido antes del lanzamiento general.

#### **7. Mantenimiento y Soporte**

Se corrigen errores, se actualiza el software y se añaden mejoras basadas en la retroalimentación de los usuarios.

Tipos de mantenimiento:

- **Correctivo:** Solución de errores.
- **Preventivo:** Identificación y mitigación de fallos potenciales.
- **Adaptativo:** Ajuste a cambios en el entorno.
- **Evolutivo:** Adición de nuevas funcionalidades.

---

### **Modelos de SDLC**

Existen diferentes enfoques para aplicar el ciclo de vida del desarrollo:

1. **Modelo en Cascada:** Proceso secuencial donde cada fase comienza cuando la anterior termina.
2. **Modelo en V:** Similar a la cascada, pero con pruebas en cada fase.
3. **Modelo Iterativo:** Se desarrolla en ciclos repetitivos hasta lograr el producto final.
4. **Modelo Ágil:** Basado en iteraciones rápidas con retroalimentación constante (Scrum, Kanban).
5. **Modelo DevOps:** Integración continua entre desarrollo y operaciones con automatización de despliegues.

---

### **Conclusión**

El SDLC es un marco estructurado que permite desarrollar software de calidad mediante una serie de fases bien definidas. La elección del modelo adecuado depende del tipo de proyecto, los requerimientos del cliente y las necesidades del equipo de desarrollo.