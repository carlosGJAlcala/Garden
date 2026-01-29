---
title: "Synchor Scada"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - dispositivosot
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[06-Infraestructura/Servidores/DispositivosOT/Abb-red670|Abb red670]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

**SYNCHOR SCADA** es un sistema de sincronización horaria que garantiza que todos los dispositivos y equipos conectados a la red SCADA de una planta fotovoltaica mantengan exactamente la misma referencia de tiempo con una precisión de milisegundos.

Este sistema funciona como un director de orquesta temporal que coordina todos los relojes internos de los equipos distribuidos por la instalación. Utiliza típicamente señales de GPS, IRIG-B o protocolos de red como NTP para distribuir una referencia de tiempo absolutamente precisa desde una fuente central hacia todos los dispositivos de campo, incluyendo inversores, medidores, relés de protección, registradores de eventos y servidores del sistema de control.

La necesidad de SYNCHOR surge de la naturaleza crítica de la correlación temporal en sistemas eléctricos complejos. Cuando ocurre una falla o perturbación en la planta fotovoltaica, los eventos se propagan a través del sistema eléctrico en cuestión de milisegundos, afectando múltiples equipos casi simultáneamente. Sin una sincronización horaria precisa, sería imposible determinar la secuencia exacta de eventos, identificar el origen de una falla, o entender cómo se propagó a través del sistema.

En tu planta específica, cuando el relé ZIV o el ABB RED670 detectan una anomalía y generan registros oscilográficos, estos datos deben estar perfectamente sincronizados con las mediciones de los inversores, las lecturas de los medidores de energía y cualquier otro evento registrado por el SCADA. Esta sincronización permite realizar análisis post-falla precisos, determinar si las protecciones actuaron correctamente en la secuencia temporal adecuada, y cumplir con los requisitos regulatorios que exigen reportes con timestamps exactos para eventos críticos del sistema eléctrico.