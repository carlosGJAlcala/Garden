---
title: "Openvas"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

Perfecto, vamos a explicarlo de forma clara y detallada para tus notas de pentesting:


---

 OpenVAS

 ¿Qué es OpenVAS?

OpenVAS (Open Vulnerability Assessment Scanner) es una plataforma open-source para escaneo de vulnerabilidades, ampliamente usada en auditorías de seguridad y pentesting.

Es parte del proyecto Greenbone Vulnerability Management (GVM), que incluye varios componentes (scanner, manager, feed de vulnerabilidades, etc.).


 Es una alternativa libre a herramientas comerciales como Nessus.


---

 ¿Para qué sirve en pentesting?

Detecta vulnerabilidades conocidas en sistemas y aplicaciones:

Sistemas operativos (Windows, Linux, etc.).

Servicios (HTTP, FTP, SSH, SMB, etc.).

Aplicaciones web mal configuradas o desactualizadas.

Certificados caducados o configuraciones débiles.


Permite realizar escaneos automáticos y generar informes detallados, ideal para descubrir rápidamente superficies de ataque.



---

 Cómo funciona

Escanea hosts especificados y compara los resultados contra su base de datos de vulnerabilidades (NVTs = Network Vulnerability Tests).

Incluye pruebas:

Autenticadas (con credenciales → acceso profundo).

No autenticadas (externas → vista desde un atacante sin privilegios).




---

 Componentes principales

 OpenVAS está integrado dentro de GVM, que incluye:

openvas-scanner: el motor de escaneo.

gvmd: daemon que gestiona los resultados y configuración.

gsad: interfaz web para gestionar los escaneos e informes.

Feed de vulnerabilidades: actualizaciones periódicas de firmas/pruebas (similar a las definiciones de virus en un antivirus).



---

 Instalación básica en Linux (ejemplo en Kali Linux)

sudo apt update
sudo apt install openvas
sudo gvm-setup
sudo gvm-check-setup

Para ejecutar:

sudo gvm-start

 Acceso vía navegador:

https://127.0.0.1:9392


---

 Escaneo típico

1️⃣ Configurar target (objetivo):

IP única o rango.

Permitir escaneo autenticado si tienes credenciales.


2️⃣ Elegir política de escaneo:

Fast.

Full and deep.

Full and very deep.


3️⃣ Ejecutar escaneo y revisar resultados:

Vulnerabilidades se categorizan por severidad (CVSS score):

Critical.

High.

Medium.

Low.

Log.



4️⃣ Exportar informe:

PDF, HTML o XML para documentación y remediación.



---

 Ventajas

 Open-source y gratuito.
 Base de datos de vulnerabilidades constantemente actualizada (si mantienes el feed).
 Permite escaneos muy detallados incluyendo autenticados.
 Interfaz web intuitiva (gsad).


---

 Limitaciones

️ Puede consumir muchos recursos en escaneos grandes.
️ El feed gratuito tiene retraso frente a los comerciales.
️ Genera mucho tráfico → puede disparar alertas de IDS/EDR durante el pentest.


---

 Mitigaciones para defenderse

Revisar y aplicar las recomendaciones que identifica OpenVAS en informes.

Actualizar software y servicios expuestos.

Segmentar red para reducir superficie de exposición.

Aplicar hardening general (por ejemplo, deshabilitar servicios innecesarios).



---

 Resumen rápido para recordar:

>  OpenVAS = escáner de vulnerabilidades open-source, muy útil en auditorías técnicas para descubrir sistemas y servicios vulnerables, configuraciones débiles y software desactualizado.




---

Si quieres puedo prepararte:

 Checklist paso a paso para ejecutar OpenVAS en laboratorio.

️ Guía práctica de interpretación de informes y priorización de vulnerabilidades.


Solo dime .

