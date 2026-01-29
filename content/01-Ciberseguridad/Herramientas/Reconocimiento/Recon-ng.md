---
title: "Recon Ng"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Recon-ng (ng)


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

- **Nombre completo:** **Recon-ng**
    
- **Símbolo en la tabla:** **ng**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Framework modular de reconocimiento OSINT en consola
    
- **Repositorio oficial:** [https://github.com/lanmaster53/recon-ng](https://github.com/lanmaster53/recon-ng)
    

---

###  ¿Qué es Recon-ng?

**Recon-ng** es una herramienta de **reconocimiento pasivo y activo** escrita en Python, que proporciona un entorno de trabajo tipo consola interactiva similar a Metasploit. Está pensada para recopilar datos desde múltiples fuentes públicas (APIs, web scraping, WHOIS, etc.) con una estructura modular y automatizable.

---

### ️ Funciones principales:

- Framework modular: cada funcionalidad es un **módulo** que puedes cargar, configurar y ejecutar.
    
- Soporta integración con **APIs externas** (Google, Bing, Shodan, HaveIBeenPwned, etc.).
    
- Permite **automatizar tareas de reconocimiento** en campañas de Red Team.
    
- Base de datos integrada: guarda resultados automáticamente.
    
- Salida exportable en múltiples formatos (CSV, JSON, XML, etc.).
    
- Comandos similares a un CLI profesional (como `use`, `set`, `run`, `show modules`...).
    

---

###  Casos de uso:

- Recopilar subdominios y direcciones IP de un dominio objetivo.
    
- Buscar emails públicos asociados a una organización.
    
- Verificar leaks con HaveIBeenPwned.
    
- Extraer metadatos de documentos expuestos.
    
- Enumerar cuentas de redes sociales, relaciones entre dominios, etc.
    

---

###  Ejemplo básico de uso:

```bash
recon-ng
```

Luego, en el prompt:

```bash
> marketplace install recon/domains-hosts/bing_domain_web
> use recon/domains-hosts/bing_domain_web
> set SOURCE example.com
> run
```

Este módulo buscará hosts asociados al dominio `example.com` usando Bing.

---

###  Salida y exportación:

```bash
> show tables
> show hosts
> export csv /tmp/resultados.csv
```

---

### ️ Requisitos:

- Python 3
    
- Algunas funciones requieren claves API (puedes configurarlas con `keys add`).
    

---

¿Te gustaría que te prepare un flujo completo de reconocimiento con Recon-ng para un dominio específico o una plantilla de automatización?