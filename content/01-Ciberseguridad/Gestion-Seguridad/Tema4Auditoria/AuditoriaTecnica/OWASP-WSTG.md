---
title: "Owasp Wstg"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---

# OWASP WSTG (Web Security Testing Guide)


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/Nikto|Nikto]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Amass|Amass]].

###  ¿Qué es?

**OWASP WSTG** es una **metodología completa y estandarizada para realizar auditorías de seguridad sobre aplicaciones web**, desarrollada y mantenida por la comunidad OWASP (Open Worldwide Application Security Project).

Su objetivo es guiar a pentesters, desarrolladores, analistas y auditores en **cómo identificar, probar y validar vulnerabilidades** de aplicaciones web mediante técnicas manuales y automatizadas.

 Repositorio oficial:  
[https://github.com/OWASP/wstg](https://github.com/OWASP/wstg)

 Versión estable más reciente:  
**WSTG v4.2 (2023)**

---

###  ¿Para qué se usa?

- Auditorías técnicas web (black, grey o white box)
    
- Validación de controles durante el ciclo de vida seguro del software (SDLC)
    
- Pruebas en cumplimiento de normativas (ISO 27001, ENS, PCI-DSS, etc.)
    
- Entrenamiento en entornos como HackTheBox, WebGoat o CTFs
    

---

###  Estructura del WSTG

Está dividido en **categorías temáticas** que cubren todos los aspectos de una aplicación web. Cada prueba tiene:

- Un identificador (ej. `WSTG-INPV-01`)
    
- Objetivo de la prueba
    
- Requisitos previos
    
- Procedimiento detallado
    
- Herramientas recomendadas
    
- Referencias adicionales
    

Ejemplos de categorías clave:

|Categoría|Descripción|
|---|---|
|`WSTG-INFO`|Recolección de información|
|`WSTG-CONF`|Configuración e implementación|
|`WSTG-ATHN`|Autenticación|
|`WSTG-AUTH`|Control de acceso/autorización|
|`WSTG-SESS`|Gestión de sesiones|
|`WSTG-INPV`|Validación de entrada|
|`WSTG-CLNT`|Seguridad del lado cliente|
|`WSTG-BUSL`|Lógica de negocio|
|`WSTG-CRYP`|Gestión criptográfica|
|`WSTG-API`|Seguridad en APIs|

---

###  Ejemplo real de prueba con OWASP WSTG

**Ejemplo**: `WSTG-ATHN-01 – Testing for Credentials Transport over an Encrypted Channel`

 **Objetivo**: Verificar si las credenciales se transmiten cifradas (HTTPS)  
 **Procedimiento**:

- Capturar tráfico con Wireshark/Burp Suite
    
- Revisar si se usa HTTP en login
    
- Intentar mitm con sslstrip
    

 **Riesgo**: Exposición de credenciales por canal inseguro  
️ **Herramientas**: Burp Suite, OWASP ZAP, Wireshark

---

### ️ Herramientas recomendadas en WSTG

- **Burp Suite / ZAP** (análisis de peticiones, fuzzing, intercepción)
    
- **Nmap + NSE scripts** (fingerprinting, escaneo de puertos)
    
- **Amass, Sublist3r** (recolección de subdominios)
    
- **Nikto** (testing de configuraciones inseguras)
    
- **wfuzz / gobuster** (fuerza bruta de rutas)
    
- **Postman** (pruebas manuales de APIs)
    

---

###  Beneficios de aplicar WSTG

- Estandarización: garantiza que las pruebas sean **repetibles y completas**
    
- Documentación: sirve como base para informes y checklist
    
- Actualización: está alineado con OWASP Top 10 y otras buenas prácticas
    
- Comunidad: utilizado por pentesters y auditores de todo el mundo
    

---

###  WSTG vs OWASP Top 10

|OWASP WSTG|OWASP Top 10|
|---|---|
|Es una **metodología de testing**|Es una **clasificación de riesgos**|
|Tiene instrucciones paso a paso|Resume las vulnerabilidades más comunes|
|Usado para hacer pentests web|Usado como guía de concienciación|

 Se complementan: puedes usar WSTG para **detectar** vulnerabilidades del OWASP Top 10 (como XSS, SQLi, CSRF, etc.).

---

###  Cómo usarlo en un pentest o auditoría técnica

1. **Define el alcance** (aplicaciones, rutas, APIs, roles de usuario)
    
2. **Crea tu checklist personalizada WSTG**
    
3. **Ejecuta pruebas por categorías relevantes**
    
4. **Documenta hallazgos con evidencias (capturas, logs, CVEs)**
    
5. **Incluye referencias WSTG en el informe final**
    

---

###  Recursos útiles

-  [OWASP WSTG](https://github.com/OWASP/wstg)
    
-  [WSTG online viewer](https://owasp.org/www-project-web-security-testing-guide/)
    
-  [Web Security Academy – PortSwigger](https://portswigger.net/web-security)
    
-  [HackTricks Web Testing](https://book.hacktricks.xyz/)
    

---