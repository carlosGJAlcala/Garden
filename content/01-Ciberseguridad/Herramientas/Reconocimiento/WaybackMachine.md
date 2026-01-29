---
title: "Waybackmachine"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

wayback_markdown = """# Wayback Machine (Wy)

**Categoría:** Reconnaissance

**Descripción:**

Wayback Machine es un servicio ofrecido por Internet Archive que permite consultar versiones históricas de sitios web. Captura y almacena copias periódicas de páginas web a lo largo del tiempo, creando un archivo accesible públicamente.

En ciberseguridad ofensiva, es una herramienta muy útil durante la fase de reconocimiento pasivo, ya que permite:

- Analizar cómo ha evolucionado un sitio web
- Recuperar información que ha sido eliminada o modificada
- Encontrar endpoints, subdominios, formularios o scripts obsoletos
- Identificar tecnologías antiguas o vulnerables que pudieron haber sido expuestas
- Ver contenido que podría revelar estructura interna o credenciales por error

**Principales usos en seguridad:**

- **Descubrimiento de endpoints ocultos:** URLs antiguas que no están enlazadas actualmente, pero que aún podrían estar activas.
- **Recuperación de información eliminada:** Archivos robots.txt, páginas de login o documentos que fueron expuestos por error.
- **Reconocimiento pasivo:** No genera tráfico hacia el objetivo; útil para evitar detección por IDS/IPS.
- **Auditorías OSINT:** Investigar qué datos históricos fueron públicos en un sitio objetivo.

**Cómo usar:**

Desde navegador:
- Visitar: [https://web.archive.org](https://web.archive.org)
- Introducir la URL deseada y seleccionar una fecha de captura

Desde línea de comandos (con herramientas como `waybackurls`):
```bash
echo "example.com" | waybackurls

