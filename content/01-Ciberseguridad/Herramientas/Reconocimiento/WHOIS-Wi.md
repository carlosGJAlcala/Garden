---
title: "WHOIS (Wi)"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
# WHOIS (Wi)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]]. [[01-Ciberseguridad/Comunicaciones-Seguras/2024-12-19-REDES-WIFI|2024 12 19 REDES WIFI]].

**Categoría:** Reconnaissance

**Descripción:**

WHOIS es una herramienta y protocolo que permite consultar información registrada sobre dominios de Internet, direcciones IP y ASN (Sistemas Autónomos). Se utiliza para obtener datos como:

- Propietario del dominio
- Datos de contacto del registrante
- Servidores DNS utilizados
- Fechas de registro y expiración

Es útil en ciberseguridad para realizar:

- Investigaciones de amenazas (identificando responsables de dominios sospechosos)
- Reconocimiento pasivo sobre objetivos
- Trazabilidad de ataques relacionados con dominios o IPs

Se puede usar desde línea de comandos (`whois dominio.com`) o mediante servicios web.

**Ejemplo de uso:**
```bash
whois example.com
