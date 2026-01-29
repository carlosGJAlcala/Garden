---
title: "Crtsh"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]].

Excelente, vamos a explicar crt.sh, una herramienta clave para reconocimiento y enumeración de subdominios en la fase de OSINT en pentesting. Aquí tienes las notas detalladas:


---

 crt.sh

 ¿Qué es crt.sh?

crt.sh es un servicio público de Certificate Transparency (CT) operado por Comodo (ahora Sectigo).

Permite consultar todos los certificados SSL/TLS públicos emitidos para cualquier dominio o subdominio.


 Muy útil para pentesters y bug hunters porque revela subdominios que fueron incluidos en certificados SSL y que podrían estar olvidados o no registrados en DNS común.


---

 ¿Por qué es importante en pentesting?

Las empresas suelen emitir certificados SSL/TLS para sus dominios y subdominios:

Ejemplo: mail.ejemplo.com, api.ejemplo.com, dev.ejemplo.com.


Estos subdominios pueden aparecer en crt.sh incluso si no están indexados en Google, Bing u otros motores de búsqueda.




Identificar activos ocultos.

Detectar nuevos subdominios en tiempo real (porque los logs CT son públicos y en continuo crecimiento).

Enumerar potenciales vectores de ataque.



---

 Cómo usar crt.sh

Uso manual: 1️⃣ Ir a: https://crt.sh/
2️⃣ Buscar:

%.ejemplo.com

 El símbolo % actúa como comodín para subdominios (SQL LIKE wildcard).

También puede usarse para identificar certificados emitidos históricamente, incluso si ya han expirado.



---

 Ejemplo de búsqueda:

%.target.com

 Resultado:

Lista de todos los certificados emitidos para target.com y sus subdominios, incluyendo:

Fecha de emisión.

Autoridad certificadora (CA).

Subdominios incluidos en el campo CN o SAN.




---

 Integración con otras herramientas

Herramientas modernas como Subfinder ya incluyen integración con crt.sh mediante API, lo que permite automatizar la consulta y extracción de subdominios en un proceso masivo.



---

 Impacto en pentesting

 Permite descubrir:

Subdominios olvidados (dev., test., staging.).

Aplicaciones de prueba accesibles públicamente.

Activos de terceros que usan certificados emitidos por la organización.



---

 Limitaciones

crt.sh solo muestra certificados emitidos públicamente → subdominios sin certificado o certificados auto-firmados no aparecerán.

No verifica que el subdominio aún resuelva o exista → es necesario combinarlo con herramientas como httpx o dnsx.



---

 Mitigaciones para defensores

 ¿Cómo protegerse?

Monitorizar proactivamente logs de Certificate Transparency sobre dominios propios.

Revisar qué subdominios están expuestos públicamente.

Revocar certificados antiguos innecesarios.

Eliminar servicios y subdominios que ya no deberían estar en producción.



---

 Resumen rápido para recordar:

>  crt.sh = servicio público para consultar certificados SSL/TLS emitidos, muy útil para descubrir subdominios expuestos a través de logs de transparencia.
Potente herramienta de reconocimiento pasivo OSINT en pentesting y bug bounty.




---

Si quieres puedo prepararte:

 Mini-guía sobre cómo extraer resultados de crt.sh con scripts.

️ Laboratorio: enumeración de subdominios combinando crt.sh + Subfinder + httpx.


Solo dime .

