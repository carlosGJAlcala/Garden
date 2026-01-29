---
title: "dig (Dg)"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
# dig (Dg)


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]]. [[01-Ciberseguridad/Comunicaciones-Seguras/2024-12-19-REDES-WIFI|2024 12 19 REDES WIFI]]. [[01-Ciberseguridad/Comunicaciones-Seguras/La-Red-SARA|La Red SARA]].

**Categoría:** Reconnaissance

**Descripción:**

`dig` (Domain Information Groper) es una herramienta de línea de comandos para realizar consultas DNS. Permite obtener información detallada sobre cómo se resuelven nombres de dominio a direcciones IP y otros registros.

Se utiliza ampliamente en:

- Auditorías DNS
- Resolución de problemas de conectividad
- Enumeración de subdominios
- Comprobación de registros específicos (A, MX, TXT, NS, CNAME…)

**Ejemplo de uso:**
```bash
dig example.com
dig MX example.com
dig @8.8.8.8 example.com
