---
title: "Builtwith"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  BuiltWith (Bu)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Censys|Censys]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

- **Nombre completo:** **BuiltWith Technology Profiler**
    
- **Símbolo en la tabla:** **Bu**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de análisis tecnológico web y perfilado de infraestructura
    
- **Sitio oficial:** [https://builtwith.com](https://builtwith.com/)
    
- **API oficial:** [https://api.builtwith.com](https://api.builtwith.com/)
    

---

##  ¿Qué es BuiltWith?

**BuiltWith** es una plataforma OSINT (Open Source Intelligence) que permite identificar **las tecnologías que utiliza un sitio web**, incluyendo:

- Frameworks web (ej: React, Angular, Django)
    
- Servidores web (Apache, Nginx, IIS)
    
- Sistemas de gestión de contenido (CMS como WordPress, Joomla)
    
- Herramientas de analítica (Google Analytics, Matomo)
    
- Librerías JavaScript, CDN, fuentes de terceros
    
- Plataformas de comercio electrónico, protección web, scripts de seguimiento y más
    

Es utilizada tanto por **hackers éticos y analistas de seguridad**, como por **equipos de ventas y marketing** para segmentar mercados por tecnología.

---

## ️ ¿Qué detecta BuiltWith?

|Categoría tecnológica|Ejemplos que puede identificar|
|---|---|
| CMS y frameworks|WordPress, Drupal, Joomla, Laravel, Flask, Next.js|
| Servidores web|Apache, Nginx, Microsoft-IIS, Cloudflare|
| E-commerce|Shopify, Magento, WooCommerce|
| Analítica|Google Analytics, Hotjar, Yandex Metrica|
| Seguridad|reCAPTCHA, Sucuri, Imperva, Cloudflare WAF|
| Publicidad|Google Ads, Facebook Pixel, Taboola|
| CDN y recursos estáticos|Amazon CloudFront, Akamai, jsDelivr, Fastly|
| JS y librerías frontend|jQuery, React, Bootstrap, Angular|

---

##  Ejemplo de uso básico

###  Desde el sitio web:

1. Accede a [https://builtwith.com](https://builtwith.com/)
    
2. Introduce una URL, por ejemplo: `https://microsoft.com`
    
3. Recibes un perfil detallado de toda la tecnología detectada.
    

---

###  Desde la línea de comandos con su API:

```bash
curl "https://api.builtwith.com/v20/api.json?KEY=tu_api_key&LOOKUP=example.com"
```

Esto devolverá un JSON estructurado con las tecnologías detectadas por categoría, versión, primera y última detección, etc.

---

##  Casos de uso ofensivos (Red Team)

- Detectar CMS o frameworks vulnerables: si un sitio usa WordPress sin proteger, es un punto de entrada común.
    
- Descubrir servidores con tecnologías antiguas o inseguras.
    
- Encontrar tecnologías específicas para crear ataques dirigidos (phishing o explotación de librerías conocidas).
    
- Recoger inteligencia tecnológica de una empresa para construir campañas de ingeniería social creíbles.
    

---

##  Casos de uso defensivos (Blue Team)

- Auditorías de exposición tecnológica: verificar si la infraestructura web muestra más información de la deseada.
    
- Comparar lo que BuiltWith detecta vs lo que debería estar oculto.
    
- Identificar posibles puntos de fuga de información (trackers externos, cookies, fuentes externas).
    
- Observar cambios no autorizados en la capa de presentación del sitio web.
    

---

##  Comparación con otras herramientas similares

|Herramienta|Método de análisis|API|Enfoque principal|
|---|---|---|---|
|**BuiltWith**|Análisis pasivo (HTTP)||Perfilado tecnológico|
|Wappalyzer|Headers + JS + HTML||Extensión y API|
|WhatRuns|JS + visual web frontend||Solo plugin visual|
|Netcraft|Información de hosting||DNS, hosting, certificados|
|Censys/Shodan|Escaneo activo||Infraestructura general|

---

##  Ejemplo de salida (resumida)

Para `example.com`:

```
- Hosting: Cloudflare
- Web Server: nginx
- CMS: WordPress 6.1.1
- CDN: Cloudflare CDN
- Analytics: Google Analytics
- Widgets: reCAPTCHA, YouTube Embed
- JS Libraries: jQuery 3.5.1, Bootstrap 4
```

Esto puede ser usado como base para preparar un informe técnico o iniciar una enumeración automatizada.

---

##  Recomendaciones de uso ético

Aunque BuiltWith usa información pública (cabeceras HTTP, scripts, metadatos), se recomienda:

- No abusar de la API gratuita ni automatizar consultas masivas sin permiso.
    
- Usar esta información solo en contextos autorizados (pentesting, auditorías internas).
    
- Combinarla con otras fuentes como Wappalyzer, Netcraft o FOCA para obtener una imagen completa.
    

---

##  Conclusión

**BuiltWith** es una herramienta esencial para entender **la superficie tecnológica expuesta de una organización**. Proporciona inteligencia contextual que puede ser utilizada tanto para fortalecer la seguridad (Blue Team), como para preparar un ataque o reconocimiento en pruebas de penetración (Red Team).

---

¿Te gustaría que prepare un script que use la API de BuiltWith junto con Subfinder y HTTPX para descubrir tecnologías de todos los subdominios de una organización? ¿O que lo integre en un flujo CI/CD para verificar tecnologías expuestas antes de pasar a producción?