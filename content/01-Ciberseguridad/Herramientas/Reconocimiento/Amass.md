---
title: "Amass"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/DICCIONARIOS|DICCIONARIOS]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Sublist3r|Sublist3r]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]].

¡


Amass es una herramienta open-source desarrollada por OWASP para realizar enumeración avanzada de subdominios y mapeo de infraestructura en red.

Permite descubrir activos expuestos mediante técnicas de OSINT (Open Source Intelligence) y escaneo activo.


 Es mucho más completa que herramientas simples como Sublist3r o Subfinder porque combina fuentes pasivas, resolución DNS activa y descubrimiento de relaciones entre dominios.


---

 ¿Para qué sirve en pentesting?

 Fase de reconocimiento:

Enumeración de subdominios.

Identificación de rangos IP utilizados por el objetivo.

Descubrimiento de relaciones entre dominios corporativos.

Exportación de resultados para análisis posterior o integración en workflows (bug bounty, Red Team, etc.).


 Ideal para ampliar la superficie de ataque antes de realizar análisis más intrusivos.


---

 Principales funcionalidades

 Modos de operación: 1️⃣ Passive: Solo fuentes OSINT → no interactúa directamente con el objetivo.
2️⃣ Active: Realiza consultas DNS activas y escaneos de infraestructura.
3️⃣ Brute-force: Permite enumerar subdominios mediante diccionarios.
4️⃣ Reverse DNS: Descubre hosts en rangos IP utilizando resoluciones inversas.
5️⃣ Visualization: Genera grafos (amass viz) para analizar relaciones entre dominios.


---

 Cómo instalar

Linux/macOS (con Go):

go install -v github.com/owasp-amass/amass/v4/...@latest

Binarios listos para descargar:  https://github.com/owasp-amass/amass/releases



---

 Comandos básicos

Enumeración pasiva:

amass enum -passive -d ejemplo.com

Enumeración activa + pasiva:

amass enum -d ejemplo.com

Guardar resultados en archivo:

amass enum -d ejemplo.com -o resultado.txt

Añadir diccionario (brute-force):

amass enum -brute -d ejemplo.com -w wordlist.txt

Visualización de relaciones:

amass viz -d3 -o grafico.html



---

 Fuentes utilizadas

Amass utiliza muchas más fuentes que Sublist3r o Subfinder:

APIs públicas: VirusTotal, AlienVault OTX, crt.sh, etc.

Motores de búsqueda: Google, Bing, Baidu, etc.

Consultas DNS activas y registros DNS inversos.

Datos históricos y de caché.


 Si configuras las API keys adecuadas en ~/.config/amass/config.ini, amplías significativamente su potencia.


---

 Impacto en pentesting

 ¿Qué permite encontrar?

Subdominios expuestos.

Servicios asociados a diferentes IPs.

Activos olvidados o mal configurados.

Infraestructura externa de terceros vinculada al dominio objetivo.



---

 Limitaciones

Más lento que herramientas puramente pasivas (por su profundidad).

Consumo alto de recursos en modo active.

Requiere configuración de API keys para sacar el máximo partido.



---

 Mitigaciones para defensores

 ¿Cómo protegerse?

Auditar registros DNS públicos y limpiar subdominios innecesarios.

Monitorizar qué expone Certificate Transparency (crt.sh).

Revisar y minimizar servicios expuestos bajo subdominios históricos o de desarrollo.



---

 Resumen rápido para recordar:

>  Amass = herramienta avanzada de enumeración de subdominios e infraestructura, combinando OSINT + escaneo activo + relaciones entre dominios.
Ideal para pentesters que necesitan un mapeo completo antes de explotar vulnerabilidades.



