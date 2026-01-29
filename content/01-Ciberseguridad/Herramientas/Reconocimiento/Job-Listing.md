---
title: "Job Listing"
date: 2025-01-01
tags:
  - ciberseguridad
---

###  **Job Listing (en contexto de OSINT y Pentesting)**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/DNSDumpster|DNSDumpster]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/OPSEC|OPSEC]]. [[02-Ciencias-Computacion/Redes/Grafana|Grafana]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

####  **Definición general**

- **Job Listing = anuncios de ofertas de empleo que publica una organización para cubrir vacantes**.
    
- Estos anuncios suelen encontrarse en:
    
    - Portales de empleo (LinkedIn, InfoJobs, Indeed, Glassdoor…).
        
    - Sección de "Trabaja con nosotros" en la web oficial de la empresa.
        
    - Agencias de reclutamiento o consultoras externas.
        

 Aunque su objetivo principal es atraer candidatos, **para un atacante o pentester representan una mina de oro de información pública sobre la infraestructura tecnológica y los recursos internos de la organización**.

---

####  **¿Por qué es útil un Job Listing en un pentest o fase de OSINT?**

 **Job listings pueden revelar datos críticos como:**

- **Tecnologías en uso:**
    
    - "Buscamos desarrollador experto en Django y PostgreSQL".
        
    - "Ingeniero con experiencia en AWS, Kubernetes y Terraform".
        
    - Esto da pistas directas sobre el stack tecnológico actual → potenciales vectores de ataque.
        
- **Sistemas internos y herramientas corporativas:**
    
    - "Conocimiento de sistemas SAP", "Uso avanzado de Jira y Confluence".
        
    - Puede indicar tecnologías implementadas que pueden estar expuestas (VPNs, paneles de administración, APIs internas).
        
- **Versiones y configuraciones:**
    
    - Algunas ofertas detallan explícitamente la versión del software utilizado: "Experiencia en Microsoft Exchange 2016".
        
    - Esto permite a un atacante enfocar su búsqueda en vulnerabilidades específicas (e.g., CVEs relevantes).
        
- **Arquitectura y metodologías:**
    
    - "Experiencia trabajando en entornos DevOps con CI/CD".
        
    - Indica que pueden tener entornos automatizados donde errores de configuración pueden ser explotados.
        
- **Ubicaciones físicas y teletrabajo:**
    
    - "Puesto presencial en sede de Madrid".
        
    - Puede permitir identificar oficinas, centros de datos o localizaciones relevantes para ataques físicos o ingeniería social.
        
- **Contactos clave:**
    
    - El nombre y correo de la persona de RRHH o responsable de la contratación.
        
    - Puede servir como target inicial en campañas de phishing o pretexting.
        

---

####  **Cómo aprovechar Job Listings en pentesting / Red Team / OSINT**

 Técnicas prácticas:  
1️⃣ **Revisión manual:**

- Analizar las publicaciones recientes en portales como LinkedIn o la web oficial del cliente.
    
- Identificar tendencias tecnológicas, herramientas, certificaciones que demandan.
    

2️⃣ **Extracción automatizada:**

- Scrapers en Python que recojan y analicen ofertas de empleo masivamente.
    
- Clasificación de tecnologías mencionadas → creación de un “stack de tecnología de la organización”.
    

3️⃣ **Enriquecimiento con otros datos OSINT:**

- Cruzar información de Job Listings con:
    
    - DNSDumpster → descubrir IPs y subdominios relacionados.
        
    - crt.sh → subdominios con SSL emitidos.
        
    - Shodan → detectar servicios publicados (coincidiendo con tecnologías mencionadas en las ofertas).
        

4️⃣ **Identificación de “target personas”:**

- Contactos que aparecen en ofertas pueden ser empleados con acceso privilegiado o clave para campañas de ingeniería social.
    

---

####  **Ejemplo práctico de extracción de información de un Job Listing**

 **Ejemplo realista de un anuncio:**

```
Buscamos ingeniero DevOps con experiencia en:
- AWS (VPC, EC2, S3, Lambda)
- Docker y Kubernetes (EKS)
- CI/CD con Jenkins y GitLab
- Conocimientos de Linux RedHat y scripting en Bash/Python
- Experiencia en soluciones de monitoreo con Prometheus y Grafana
```

 **Información obtenida útil para un pentester:**

- La organización usa AWS → posible ataque a infraestructura cloud.
    
- Uso de Kubernetes/EKS → se puede buscar panel de administración mal expuesto.
    
- Jenkins/GitLab → objetivo prioritario si existen versiones vulnerables.
    
- Tecnologías monitoreo → puertos típicos: 9090 (Prometheus), 3000 (Grafana).
    
- Linux RedHat y scripting → posibles vectores de ataque vía SSH, scripts inseguros.
    

---

####  **Ventajas de explotar Job Listings**

 **Todo es información pública y legalmente accesible:**

- No requiere técnicas intrusivas.
    
- No genera tráfico hacia el objetivo.
    
- Permite construir un perfil detallado antes de lanzar escaneos activos → mejora OPSEC ofensivo.
    

 **Alta calidad de la información:**

- Las ofertas suelen ser recientes y reflejan el estado actual de la infraestructura y necesidades técnicas.
    

---

####  **Limitaciones**

️ A tener en cuenta:

- No todos los anuncios serán detallados → algunas empresas redactan de forma genérica.
    
- Puede haber tecnología publicada en Job Listings que aún no está desplegada.
    
- Se debe cruzar esta información con otras fuentes para validar su utilidad real.
    

---

####  **Mitigaciones para defensores**

 Cómo mitigar el riesgo asociado a Job Listings:

- **No exponer detalles innecesarios en las descripciones de empleo.**
    
    - Ej.: en lugar de “Experiencia en Jenkins 2.319” → “Experiencia en herramientas de CI/CD”.
        
- Evitar mencionar versiones exactas de software/productos.
    
- Centralizar publicaciones en portales controlados (para evitar fugas en múltiples canales).
    
- Sensibilizar a RRHH sobre lo que constituye información sensible.
    

---

 **Resumen denso para recordar:**

>  **Job Listings son una fuente valiosa y subestimada en OSINT y pentesting que revela tecnologías, herramientas, versiones, metodologías, ubicaciones y contactos clave usados por la organización**.  
> Su análisis permite mapear tecnologías, perfilar infraestructura y planificar ataques con alta precisión antes de realizar interacción activa.

---

Si quieres puedo prepararte:

-  **Checklist avanzada para análisis de Job Listings en fase de reconocimiento.**
    
- ️ **Script en Python que scrapee ofertas de empleo y extraiga tecnologías mencionadas automáticamente.**
    

Solo dime  y lo preparo.