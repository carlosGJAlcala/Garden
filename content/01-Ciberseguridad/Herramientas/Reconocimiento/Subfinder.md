---
title: "Subfinder"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/Sublist3r|Sublist3r]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

Perfecto, vamos a explicar Subfinder, otra herramienta imprescindible para enumeración de subdominios en la fase de reconocimiento en pentesting. Aquí tienes las notas detalladas:


---

 Subfinder

 ¿Qué es Subfinder?

Subfinder es una herramienta rápida y moderna para descubrir subdominios de forma pasiva.

Desarrollada en Go por ProjectDiscovery (los creadores de nuclei).

Diseñada para ser eficiente, ligera y fácil de integrar en pipelines automatizados (ej.: en bug bounty y pentests profesionales).



---

 ¿Para qué sirve?

 Su objetivo es enumerar subdominios utilizando fuentes OSINT (Open Source Intelligence), al igual que Sublist3r, pero de manera más optimizada y extensible.

 Utilidad en pentesting:

Identificar superficies de ataque adicionales.

Encontrar activos olvidados o poco protegidos.

Reconocimiento pasivo (sin interactuar directamente con la infraestructura objetivo).



---

 Cómo funciona

Consulta múltiples fuentes públicas y APIs:

AlienVault OTX

CertSpotter

ThreatCrowd

VirusTotal

crt.sh (transparencia de certificados SSL)

DNSDB, etc.



 Subfinder está pensado para ser extensible:
Puedes añadir y configurar fuentes adicionales en el archivo ~/.config/subfinder/provider-config.yaml.


---

 Instalación

 En sistemas Linux/Mac/Windows con Go:

go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

Binarios precompilados disponibles:
https://github.com/projectdiscovery/subfinder/releases



---

 Comando básico

subfinder -d ejemplo.com

 Guarda la lista de subdominios encontrados directamente en consola.


---

 Opciones útiles

Guardar resultados en archivo:

subfinder -d ejemplo.com -o resultado.txt

Mostrar solo subdominios resolvibles (con IP):

subfinder -d ejemplo.com -nR

Usar configuraciones personalizadas de API keys:

subfinder -d ejemplo.com -config ~/.config/subfinder/provider-config.yaml

Enumeración masiva:

subfinder -dL domains.txt -o todos.txt



---

 Comparativa con Sublist3r

Aspecto	Sublist3r	Subfinder

Lenguaje	Python	Go
Velocidad	Rápida	Muy rápida
Actualización	Menos mantenida	Activa y moderna
Extensibilidad	Limitada	Alta, configurable
Fuentes soportadas	Varias	Muchas, APIs modernas


 Subfinder suele preferirse en auditorías actuales debido a su rendimiento y mantenimiento activo.


---

 Impacto en pentesting

 ¿Qué puedes encontrar?

Subdominios olvidados (staging.ejemplo.com, old.ejemplo.com).

Subdominios mal configurados o expuestos (dev.ejemplo.com).

Información que amplía considerablemente la superficie de ataque.



---

 Limitaciones

Dependencia de fuentes públicas: no descubre subdominios internos o sin presencia OSINT.

Algunos servicios requieren API keys y pueden imponer límites si no se configuran correctamente.



---

 Mitigaciones para defensores

 ¿Cómo protegerse?

Auditar registros DNS y limpiar subdominios antiguos.

Supervisar continuamente subdominios públicos usando herramientas similares (Subfinder es útil incluso para los defensores).

Configurar correctamente registros DNS para evitar exposición innecesaria.



---

 Resumen rápido para recordar:

>  Subfinder = herramienta rápida, extensible y moderna para enumeración pasiva de subdominios a partir de fuentes OSINT.
Ideal en la fase de reconocimiento pasivo en pentesting profesional.




---

Si quieres puedo prepararte:

 Checklist de comandos avanzados con Subfinder.

️ Ejemplo práctico paso a paso: enumeración + resolución DNS + integración con otras herramientas (ej.: httpx).


Solo dime .

