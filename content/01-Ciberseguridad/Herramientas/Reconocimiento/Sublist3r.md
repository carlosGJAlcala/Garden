---
title: "Sublist3R"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Amass|Amass]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/DNSDumpster|DNSDumpster]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

¡

---

 Sublist3r

 ¿Qué es Sublist3r?

Sublist3r es una herramienta open-source escrita en Python que permite enumerar subdominios de un dominio objetivo utilizando fuentes públicas.

Está orientada a la fase de reconocimiento pasivo, recopilando información sin interactuar directamente con el objetivo (no genera tráfico hacia su infraestructura).



---

 ¿Para qué sirve en pentesting?

 Objetivo:

Descubrir subdominios que podrían estar:

Expuestos públicamente.

Mal configurados.

Sin actualizar o descuidados.

Usados en entornos de desarrollo/staging.



 Utilidad práctica:

Ampliar el alcance de un test de intrusión.

Encontrar nuevos vectores de ataque (e.g., apps web olvidadas, paneles de administración).



---

 Cómo funciona

Sublist3r consulta múltiples fuentes públicas y motores de búsqueda, como:

Google

Bing

Yahoo

Baidu

Ask

Netcraft

DNSdumpster

VirusTotal

ThreatCrowd

SSL certificates

PTR records


 Es rápido y permite complementar con herramientas como Amass, crt.sh o Assetfinder.


---

 Comando básico

sublist3r -d ejemplo.com

 Por defecto:

Devuelve una lista de subdominios encontrados.

No requiere credenciales ni configuración adicional.



---

 Opciones comunes

Guardar resultados en archivo:

sublist3r -d ejemplo.com -o resultado.txt

Especificar número de threads (para mayor velocidad):

sublist3r -d ejemplo.com -t 50

Usar un motor de búsqueda concreto:

sublist3r -d ejemplo.com -e Bing,Google



---

 Instalación

 Requisitos:

Python 2.x o 3.x.

Dependencias:

git clone https://github.com/aboul3la/Sublist3r
cd Sublist3r
pip install -r requirements.txt



---

 Impacto en pentesting

 ¿Qué puedes encontrar?

Subdominios que apuntan a aplicaciones web olvidadas.

Recursos expuestos (e.g., dev.ejemplo.com, test.ejemplo.com, vpn.ejemplo.com).

Activos no protegidos con HTTPS.

Endpoints abandonados que permiten explotación directa.



---

 Limitaciones

Dependencia de fuentes públicas: no encuentra subdominios no indexados o internos.

Algunos motores de búsqueda limitan las peticiones (puede requerir proxies).



---

 Mitigaciones para defensores

 ¿Cómo protegerse?

Revisar registros DNS y limpieza periódica de subdominios no usados.

Controlar el "shadow IT" (activos fuera del control oficial).

Monitorizar dominios y subdominios públicos para evitar exposición no autorizada.



---

 Resumen rápido para recordar:

>  Sublist3r = herramienta ligera y rápida de enumeración de subdominios usando fuentes públicas.
Ideal en la fase de reconocimiento pasivo para identificar activos y ampliar superficie de ataque.




