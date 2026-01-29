---
title: "Invicti"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Invicti (Iv)


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/SSRF|SSRF]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/GraphQL|GraphQL]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

- **Nombre completo:** **Invicti Web Application Security Scanner**
    
- **Símbolo en la tabla:** **Iv**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Escáner automático de seguridad para aplicaciones web (DAST)
    
- **Sitio web oficial:** [https://www.invicti.com](https://www.invicti.com/)
    

---

##  ¿Qué es Invicti?

**Invicti** (anteriormente conocido como **Netsparker**) es una herramienta profesional de tipo **DAST (Dynamic Application Security Testing)**, especializada en el **análisis de vulnerabilidades de aplicaciones web**. Permite escanear sitios web, APIs y aplicaciones dinámicas para detectar **fallos de seguridad reales y explotables**, como inyecciones SQL, XSS, CSRF, vulnerabilidades en autenticación, configuración errónea del servidor, y más.

Es muy utilizado en **empresas, gobiernos y grandes organizaciones** como parte de su ciclo de pruebas de seguridad en desarrollo (SDLC) o auditorías regulares.

---

##  ¿Para qué sirve Invicti?

Invicti automatiza el proceso de:

- Detectar **vulnerabilidades** web en sitios reales (DAST).
    
- Validar que las vulnerabilidades encontradas son **explotables**.
    
- Integrar los resultados con flujos de trabajo CI/CD.
    
- Realizar pruebas **no destructivas pero realistas**, sin dañar producción.
    
- Generar **informes técnicos y ejecutivos** detallados, con recomendaciones precisas.
    

---

## ️ Características destacadas

|Funcionalidad|Descripción|
|---|---|
| Detección avanzada|SQLi, XSS, CSRF, SSRF, RCE, LFI, IDOR, etc.|
| Verificación de explotación|Evita falsos positivos probando si la vulnerabilidad es real y explotable.|
| Soporte de autenticación|Forms login, HTTP Auth, OAuth, Bearer tokens, SAML, JWT, etc.|
| Informes automatizados|HTML, PDF, JSON, JIRA, GitHub, GitLab, etc.|
| Integración CI/CD|Jenkins, GitHub Actions, GitLab CI, Azure DevOps, etc.|
| API REST completa|Permite automatizar scans, configuraciones y gestión de resultados.|
| Escaneo de APIs|Soporte para Swagger/OpenAPI, Postman, GraphQL, SOAP.|
| Cobertura de OWASP Top 10|Detecta y justifica todas las categorías OWASP.|
| Machine Learning y heurística|Para detectar aplicaciones SPAs y complejas dinámicas.|

---

##  Flujo de uso típico

1. **Configuración del escaneo**
    
    - Introduces la URL o IP del sitio web.
        
    - Defines las reglas: profundidad, autenticación, exclusiones, frecuencia.
        
2. **Ejecución del escaneo**
    
    - Crawling completo del sitio.
        
    - Simulación de ataques controlados a endpoints.
        
    - Detección y verificación de fallos reales.
        
3. **Resultados e informes**
    
    - Visualización de vulnerabilidades por gravedad.
        
    - Recomendaciones detalladas.
        
    - Evidencias de explotación automatizada.
        
4. **Remediación e integración**
    
    - Crea tickets automáticos en Jira, GitHub, etc.
        
    - Valida si los fallos se han corregido en escaneos posteriores.
        

---

##  Casos de uso

-  **Auditoría interna de seguridad** de portales web y aplicaciones.
    
-  **Testing dinámico automatizado** en pipelines de DevSecOps.
    
-  **Reconocimiento profundo** en campañas de Red Team o Bug Bounty.
    
-  **Validación post-explotación**: comprobar si un endpoint es realmente vulnerable.
    
-  **Cumplimiento de normativas** como PCI DSS, ISO 27001, SOC 2, etc.
    

---

##  Instalación y despliegue

Invicti está disponible en:

|Modalidad|Descripción|
|---|---|
|**Cloud (SaaS)**|No requiere instalación. Acceso vía navegador.|
|**On-Premise**|Se instala en Windows/Linux. Control total.|

Requiere licencia. No es una herramienta open source, pero sí cuenta con versión demo bajo solicitud.

---

##  Defensa y madurez

Invicti se centra en el **ciclo de vida seguro del software**:

- Se integra en etapas tempranas del desarrollo para que los errores de seguridad se corrijan **antes de pasar a producción**.
    
- Su verificación de explotación lo hace especialmente confiable para evitar falsos positivos y **ahorrar tiempo a los desarrolladores**.
    

---

##  Comparación con otras herramientas

|Herramienta|Tipo|Enfoque principal|Verificación de explotación|
|---|---|---|---|
|**Invicti**|DAST|Análisis profundo web| Sí|
|Burp Suite Pro|Interactivo|Manual + semiautomático|️ Parcial (depende del usuario)|
|OWASP ZAP|DAST|Libre y flexible| No|
|Nuclei|SAST-lite|Detección por templates| No|
|Acunetix|DAST|Similar a Invicti| Sí|

---

##  Conclusión

**Invicti** es una herramienta profesional y robusta para asegurar aplicaciones web, APIs y servicios dinámicos. Está diseñada para ser confiable, automatizable y verificable, lo que la hace ideal tanto para empresas que buscan madurez en su SDLC como para equipos Red/Blue que quieren detectar vectores reales de explotación sin ruido innecesario.

---

### ¿Te gustaría?

- Un caso práctico con vulnerabilidades reales escaneadas por Invicti.
    
- Un **flujo CI/CD con escaneo automático de cada despliegue**.
    
- Una **comparativa contra Burp Suite o ZAP** en un entorno real.