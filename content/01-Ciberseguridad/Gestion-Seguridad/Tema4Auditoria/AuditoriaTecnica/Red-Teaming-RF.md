---
title: "Red Teaming Rf"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---

# Red Teaming (RF) — Simulación real de ataques avanzados


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/AuditoriaTecnica/Pivoting|Pivoting]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/GanarAcceso/Rootkits|Rootkits]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Escalada-de-Privilegios|Escalada de Privilegios]].

###  ¿Qué es Red Teaming?

El **Red Teaming** es una **simulación controlada y autorizada de un ataque realista** contra una organización. A diferencia de un test de intrusión convencional (pentest), su objetivo **no es solo encontrar vulnerabilidades técnicas, sino también medir la capacidad de detección y respuesta del equipo defensor (Blue Team)** y **evaluar la resiliencia global del entorno**.

 Es el tipo de auditoría más completo y agresivo, muy cercano a cómo actuaría un atacante real avanzado (APT).

---

###  Objetivos del Red Teaming

- Evaluar el nivel de exposición de la organización ante amenazas persistentes avanzadas.
    
- Testar la **eficacia de los controles de detección, respuesta y contención.**
    
- Medir el tiempo de compromiso (_Time to Breach_), detección (_Time to Detect_) y reacción (_Time to Respond_).
    
- Evaluar la **coordinación entre áreas de seguridad, IT, RRHH, SOC, etc.**
    
- Identificar **deficiencias técnicas, organizativas y humanas**.
    

---

###  ¿Qué significa “(RF)” en el documento?

El documento menciona:  
**"Red Teaming (RF)"**

Probablemente se refiere a la **versión “Red Forensics” o “Red Force”** (nombres comunes en ejercicios tácticos militares y ciberseguridad), o bien a **Red Team con enfoque Forense**, donde se busca **dejar rastros controlados para evaluar la capacidad forense** del Blue Team.

En algunos contextos, "RF" también se usa como abreviación informal de **“Realistic Framework”**, indicando que el Red Team opera bajo condiciones similares a las reales.

---

### 🆚 Red Team vs Pentest vs Blue Team

|Característica|Pentest|Red Team|Blue Team|
|---|---|---|---|
|Alcance|Técnico específico|Completo y multidominio|Defensa y monitorización|
|Duración|Semanas|Meses (hasta 90 días)|Continuo|
|Visibilidad|Coordinado con el cliente|Oculto al equipo defensor|Reacciona sin saber|
|Objetivo|Encontrar vulnerabilidades|Simular compromiso real|Detectar y responder|
|Metodología|Técnicas de hacking|TTPs avanzadas (MITRE ATT&CK)|Detección / análisis|

---

### ️ Fases de un ejercicio de Red Team

1. **Reconocimiento**
    
    - OSINT, footprinting, reconocimiento físico (si aplica), social engineering.
        
2. **Vector de entrada**
    
    - Spear phishing, maliciosos USBs, explotación de vulnerabilidades, acceso físico.
        
3. **Movimiento lateral y pivoting**
    
    - Escalada de privilegios, explotación de credenciales, acceso a nuevos activos.
        
4. **Acceso a objetivos críticos**
    
    - Base de datos, backups, credenciales de administración, sistemas de control.
        
5. **Persistencia y evasión**
    
    - Técnicas para mantenerse sin ser detectado: servicios ocultos, DLL injection, rootkits.
        
6. **Extracción o impacto**
    
    - Exfiltración de datos simulada, modificación de sistemas, pruebas de ransomware controlado.
        
7. **Informe + Debriefing**
    
    - Informe técnico y reunión “debrief” para explicar paso a paso lo ocurrido.
        

---

###  Marcos y estándares aplicables

- **MITRE ATT&CK**: referencia de tácticas, técnicas y procedimientos de APTs.
    
- **TIBER-EU**: marco europeo para Red Teaming en infraestructuras críticas y financieras.
    
- **CBEST** (UK), **CORIE** (Australia), **TLPT** (EEUU): marcos nacionales similares.
    

---

###  El informe del Red Team

Debe incluir:

- Descripción narrativa de la campaña: cómo se consiguió el acceso, qué acciones se realizaron.
    
- Líneas temporales detalladas: pasos realizados y si fueron detectados.
    
- Técnicas ATT&CK utilizadas.
    
- Valoración del desempeño del Blue Team (opcional).
    
- Recomendaciones técnicas y estratégicas.
    
- “Lessons Learned” y plan de mejora.
    

---

###  Ejemplos reales de vectores usados por equipos Red Team

- Crear una web idéntica al portal interno del cliente para capturar credenciales.
    
- Enviar un archivo Excel con macro obfuscated por correo desde una cuenta falsa.
    
- Dejar un USB con payload en el aparcamiento de la empresa.
    
- Acceder físicamente disfrazado de proveedor y conectar una Raspberry Pi a la red.
    

---

###  Recursos y referencias

- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)
    
- [Red Team Field Manual (RTFM)](https://www.amazon.com/Red-Team-Field-Manual-RTFM/dp/1494295504)
    
- [TIBER-EU framework](https://www.ecb.europa.eu/pub/pdf/other/ecb.tiber_eu_framework.en.pdf)
    
- [https://github.com/redcanaryco/atomic-red-team](https://github.com/redcanaryco/atomic-red-team)
    

---

---