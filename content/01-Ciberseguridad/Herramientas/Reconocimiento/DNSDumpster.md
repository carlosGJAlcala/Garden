---
title: "Dnsdumpster"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

Perfecto, vamos a explicar en detalle DNSDumpster, otra herramienta muy valiosa para reconocimiento pasivo en pentesting. Aquí tienes unas notas detalladas y claras para tus apuntes:


---

 DNSDumpster

 ¿Qué es DNSDumpster?

DNSDumpster es un servicio online gratuito que ofrece reconocimiento DNS avanzado y visualización de la infraestructura DNS de un dominio objetivo.

Permite a cualquier persona recolectar datos públicos sobre dominios y subdominios a partir de registros DNS.


 Es muy utilizado en la fase de reconocimiento pasivo de pentesting y bug bounty.


---

 ¿Para qué sirve?

 Funciones principales:

Enumerar registros DNS:

A (direcciones IP).

MX (Mail Exchange).

TXT (incluye SPF/DKIM).

NS (Name Server).


Encontrar:

Subdominios públicos.

IPs asociadas a servicios y servidores.

Rangos de red utilizados por el dominio objetivo.


Intentar automáticamente zone transfers (AXFR) si hay configuraciones incorrectas en los servidores autoritativos.



---

 Cómo funciona

DNSDumpster consulta fuentes públicas y bases de datos externas:

Escanea registros DNS disponibles.

Busca direcciones IP públicas relacionadas con esos registros.

Muestra un mapa gráfico de la infraestructura DNS, útil para visualizar cómo están organizados los sistemas del dominio.



 No requiere autenticación ni API key para uso básico.


---

 Cómo usarlo

1️⃣ Acceder al portal:
 https://dnsdumpster.com/

2️⃣ Introducir el dominio objetivo (ejemplo.com).

3️⃣ Consultar resultados:

Listado detallado de subdominios encontrados.

Registros DNS asociados.

IPs y rangos CIDR vinculados.

Posible mapa de red.



---

 Impacto en pentesting

 ¿Qué permite descubrir?

Subdominios útiles para ampliar la superficie de ataque:

vpn.ejemplo.com

test.ejemplo.com

mail.ejemplo.com

admin.ejemplo.com


Servidores de correo potencialmente vulnerables.

Información sobre el proveedor de infraestructura (e.g., AWS, Azure, Cloudflare).

Servicios con configuraciones incorrectas (ej.: zone transfer permitido).


 Es especialmente valioso cuando se quiere obtener una visión rápida de todos los activos expuestos públicamente de un dominio.


---

 Limitaciones

Solo muestra datos públicos → si el dominio tiene configuraciones privadas o subdominios internos, no serán revelados.

Puede incluir resultados antiguos o desactualizados, siempre es recomendable validar con herramientas adicionales (dig, httpx, dnsx).



---

 Mitigaciones para defensores

 Cómo protegerse:

Bloquear zone transfer (AXFR) en todos los servidores DNS → nunca permitir transferencia a hosts no autorizados.

Minimizar exposición de registros DNS innecesarios o sensibles.

Monitorizar qué subdominios e IPs son visibles públicamente usando herramientas similares para evaluación interna.



---

 Resumen rápido para recordar:

>  DNSDumpster = servicio online gratuito para enumeración DNS y visualización gráfica de infraestructura DNS pública.
Ideal para fase de reconocimiento pasivo en pentesting, rápido y sin generar tráfico directo hacia los sistemas objetivo.




---

Si quieres puedo prepararte:

 Checklist de pasos para complementar DNSDumpster con otras herramientas (Subfinder, crt.sh, dig).

️ Guía práctica de validación de resultados obtenidos con DNSDumpster.


Solo dime .

