---
title: "Maltego"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Maltego (Ma)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

- **Nombre completo:** **Maltego**
    
- **Símbolo en la tabla:** **Ma**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de OSINT y análisis de relaciones e inteligencia
    
- **URL oficial:** [https://www.maltego.com](https://www.maltego.com/)
    

---

###  ¿Qué es Maltego?

**Maltego** es una poderosa herramienta de **reconocimiento y análisis de inteligencia** que permite visualizar relaciones entre personas, direcciones de correo electrónico, dominios, direcciones IP, redes sociales, empresas y más. Se basa en un enfoque de **gráficas relacionales**, lo que la hace ideal para OSINT y ciberinvestigación avanzada.

---

### ️ Funciones principales:

- Recopilación automatizada de datos desde múltiples fuentes públicas y privadas (DNS, WHOIS, Shodan, VirusTotal, etc.).
    
- Visualización en forma de **grafos interactivos** de relaciones entre entidades.
    
- Soporte para **transforms personalizadas** (consultas automáticas a fuentes externas).
    
- Integración con APIs públicas y privadas (LinkedIn, HaveIBeenPwned, etc.).
    
- Versiones para uso personal, profesional y corporativo.
    

---

###  Casos de uso:

- **Investigación de amenazas**: relación entre infraestructuras maliciosas (IP, dominios, correos).
    
- **Análisis forense**: visualización de relaciones entre actores y dispositivos.
    
- **Red Team / Blue Team**: identificación de vectores de ataque y huellas digitales.
    
- **Investigación de fraude**: trazado de relaciones entre entidades sospechosas.
    
- **Investigación en redes sociales y deep web**.
    
- **Ciberinteligencia corporativa o gubernamental.**
    

---

###  Ejemplo práctico:

Quieres investigar el dominio `example.com`. Con Maltego puedes:

1. Arrastrar un nodo tipo “Domain” al grafo.
    
2. Aplicar “transforms” como:
    
    - Obtener subdominios.
        
    - Asociar correos electrónicos públicos.
        
    - Identificar IPs relacionadas.
        
    - Buscar leaks en bases de datos públicas.
        

Esto te da un **mapa visual de todas las relaciones** posibles con `example.com`, ideal para informes o detección temprana de amenazas.

---

¿Te gustaría un ejemplo de caso práctico completo o una guía para usar Maltego en una investigación real?