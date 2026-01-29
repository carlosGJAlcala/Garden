---
title: "Fofa"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---




> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Censys|Censys]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

**Categoría:** Reconnaissance

**Descripción:**

FOFA (Fingerprint of All) es un motor de búsqueda especializado en recolectar información sobre dispositivos conectados a Internet, similar a Shodan o Censys. Fue desarrollado por la empresa china Knownsec y es ampliamente utilizado en el ámbito de la ciberseguridad ofensiva para reconocimiento pasivo y descubrimiento de superficies de ataque.

A través de técnicas de fingerprinting, FOFA indexa banners de servicios, encabezados HTTP, certificados SSL/TLS, puertos abiertos y otras características expuestas por los dispositivos accesibles en la red. Su base de datos se actualiza constantemente a partir de escaneos activos realizados por sus sensores distribuidos globalmente.

**Principales usos en ciberseguridad:**

- **Reconocimiento pasivo:** Obtener información sin interactuar directamente con los sistemas objetivo.
- **Enumeración de activos:** Descubrir servidores, cámaras, routers, dispositivos IoT y otros sistemas en una red.
- **Detección de tecnologías:** Identificar software y versiones (por ejemplo, Apache, nginx, Tomcat).
- **Detección de vulnerabilidades:** Buscar dispositivos que utilizan versiones vulnerables o configuraciones inseguras.
- **Análisis geográfico:** Filtrar activos por país, región, ciudad o ISP.

**Características destacadas:**

- Búsqueda avanzada mediante operadores lógicos (`&&`, `||`, `==`)
- Filtros por IP, dominio, puertos, ASN, certificados, tecnologías, país, etc.
- API RESTful para automatización y herramientas de scraping.
- Interfaz disponible en inglés y chino.
- Visualización de datos en dashboards personalizables.
- Resultados exportables en formatos como CSV o JSON.

**Ejemplos de búsqueda:**

- Buscar todos los servidores Apache en Estados Unidos:
  ```text
  app="Apache" && country="US"
