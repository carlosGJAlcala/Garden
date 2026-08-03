---
title: "Mitre Attck"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---
El **MITRE ATT&CK** (Adversarial Tactics, Techniques, and Common Knowledge) es un marco de referencia ampliamente utilizado en ciberseguridad para describir las tácticas, técnicas y procedimientos (TTPs) empleados por actores maliciosos. Fue desarrollado por la organización sin fines de lucro **MITRE** y es utilizado globalmente para mejorar la detección, respuesta y defensa contra amenazas cibernéticas.

### **Estructura de MITRE ATT&CK**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

El marco ATT&CK se organiza en **matrices** que representan diferentes entornos operativos en los que los atacantes pueden actuar, incluyendo:

- **Enterprise ATT&CK**: Se enfoca en ataques dirigidos a sistemas empresariales, incluyendo Windows, Linux y macOS.
- **Mobile ATT&CK**: Describe tácticas y técnicas utilizadas contra dispositivos móviles (iOS y Android).
- **ICS ATT&CK**: Se centra en amenazas dirigidas a sistemas de control industrial (ICS).

Cada matriz está estructurada en **tácticas**, **técnicas** y **subtécnicas**:

1. **Tácticas**: Representan los objetivos que los atacantes intentan lograr (por ejemplo, "Evasión de Defensa" o "Persistencia").
2. **Técnicas**: Son los métodos específicos utilizados para alcanzar esos objetivos (por ejemplo, "Uso de PowerShell" o "Modificación de registros de inicio").
3. **Subtécnicas**: Detallan variantes dentro de cada técnica para proporcionar mayor granularidad.

### **Ejemplo de Uso**

Por ejemplo, si un atacante desea evadir defensas, podría usar la técnica **T1036 - Masquerading**, que implica camuflar archivos o procesos maliciosos como legítimos.

### **Aplicaciones del MITRE ATT&CK**

El marco es ampliamente utilizado por equipos de ciberseguridad para:

- **Caza de amenazas**: Identificación proactiva de amenazas dentro de una red.
- **Simulación de ataques (Red Teaming)**: Pruebas de seguridad ofensiva basadas en técnicas reales de adversarios.
- **Defensa y detección**: Desarrollo de estrategias de seguridad basadas en técnicas conocidas de ataque.
- **Evaluación de seguridad**: Medición de la eficacia de herramientas de seguridad existentes.

### **Beneficios del MITRE ATT&CK**

- Proporciona un lenguaje común para describir amenazas.
- Permite correlacionar técnicas de ataque con actores específicos de amenazas (APT).
- Facilita el desarrollo de estrategias de seguridad más efectivas basadas en inteligencia sobre amenazas reales.

El **MITRE ATT&CK** es una herramienta clave en la ciberseguridad moderna, ayudando a empresas y gobiernos a comprender mejor las amenazas y a mejorar su capacidad de defensa frente a ciberataques.