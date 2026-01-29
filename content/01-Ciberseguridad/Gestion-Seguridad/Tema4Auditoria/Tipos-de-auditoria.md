---
title: "Tipos De Auditoria"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Vamos a explicar de forma clara y completa los **tipos de auditoría** en seguridad de la información, basándonos en el material del máster y ampliándolo con contexto profesional real.

---

##  ¿Qué es una auditoría de seguridad?


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/COBIT|COBIT]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]].

Una **auditoría de seguridad** es un proceso sistemático de **revisión, evaluación y verificación** de si una organización:

- Cumple con políticas, normas y buenas prácticas.
    
- Tiene **controles técnicos, organizativos y físicos adecuados**.
    
- Protege correctamente sus activos frente a riesgos reales.
    
- **Genera evidencias objetivas** de su nivel de seguridad.
    

---

##  Tipos de auditoría (según su enfoque)

### 1.  **Auditoría interna**

- La realiza personal propio o dependiente de la organización.
    
- Evalúa procesos y controles con **visión de mejora continua**.
    
- Se integra en el SGSI (ISO 27001 → cláusula 9.2).
    
- Soporte al ciclo PDCA: _Plan-Do-Check-Act_.
    

### 2.  **Auditoría externa**

- La realiza un **tercero independiente**.
    
- Sirve para:
    
    - **Obtener certificación** (ISO 27001, ENS, etc.)
        
    - Cumplir contratos o normativas
        
    - Dar confianza a clientes y reguladores
        

---

##  Tipos según el **objeto auditado**

###  **Auditoría informática**

- Evaluación de activos TIC: hardware, software, redes.
    
- Análisis de seguridad, eficiencia y funcionamiento.
    
- Puede incluir: segregación de entornos, análisis de logs, cumplimiento de políticas técnicas.
    

###  **Auditoría de cumplimiento normativo**

- Verifica si se cumple con leyes y normas:
    
    - RGPD (protección de datos)
        
    - ENS (en AAPP)
        
    - LOPDGDD, NIS2, PCI-DSS, etc.
        

###  **Auditoría de SGSI**

- Evalúa el **Sistema de Gestión de Seguridad de la Información** completo.
    
- ISO 27001 exige realizarla periódicamente.
    
- Se basa en el ciclo de gestión, políticas, riesgos, controles, evidencias, etc.
    

---

## ️ Tipos según **técnicas usadas** (auditoría técnica)

###  **Escaneo de vulnerabilidades**

- Automatizado y frecuente
    
- Herramientas: Nessus, OpenVAS, Nikto, WPSCAN, SCAP…
    
- Detecta software desactualizado, configuraciones inseguras, CVEs…
    

###  **Test de penetración (Pentest)**

- Simula un ataque real.
    
- Semi-manual. Fases:
    
    - Recolección de info
        
    - Reconocimiento
        
    - Explotación
        
    - Post-explotación
        
- Modalidades: caja blanca, negra, gris.
    
- Usado para detectar vulnerabilidades explotables.
    

###  **Red Teaming**

- Ataque controlado realista y extendido en el tiempo.
    
- Incluye ingeniería social, intrusión física, pivoting…
    
- Evalúa la **resiliencia y detección de incidentes**.
    
- Complemento de Blue Team (defensivo) y Purple Team (mixto).
    

---

##  Tipos según **norma o control aplicado**

- Auditoría **en base a norma**: ISO 27001, ENS, NIST, COBIT...
    
- Auditoría **en base a controles**: CIS Controls, OWASP, controles internos definidos
    

Ejemplo:

> Revisión del cumplimiento del control [op.exp.7.1] del ENS (gestión de incidentes).

---

##  Tipos de prueba dentro de la auditoría

|Tipo de prueba|Qué evalúa|Ejemplo|
|---|---|---|
|**Prueba de cumplimiento**|Si el control está implantado|¿Hay un firewall configurado?|
|**Prueba sustantiva**|Si el control **funciona de forma efectiva**|¿Bloquea el firewall tráfico malicioso real?|

---

##  Certificaciones relacionadas

- **CISA (ISACA)** → Auditoría de SI
    
- **ISO 27001 Auditor Jefe (AENOR, TÜV, etc.)**
    
- **OSCP / OSCE (Offensive Security)** → Pentesting
    
- **GPEN (SANS GIAC)** → Ethical Hacking
    

---

##  Conclusión

> Existen múltiples tipos de auditoría según **quién la realiza**, **qué se audita**, **cómo se hace** y **bajo qué estándar**.  
> En conjunto, todas sirven para evaluar y mejorar la seguridad, generar evidencias, garantizar cumplimiento legal y anticiparse a los riesgos reales.

---

¿Te gustaría que te prepare un esquema visual con todos estos tipos y sus relaciones? ¿O una guía práctica para realizar una auditoría interna tipo ISO o ENS?