---
title: "Urlscan"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  URLScan.io (Us)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

- **Nombre completo:** **URLScan.io**
    
- **Símbolo en la tabla:** **Us**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de análisis de URLs mediante sandboxing y OSINT
    
- **URL oficial:** [https://urlscan.io](https://urlscan.io/)
    

---

###  ¿Qué es URLScan.io?

**URLScan.io** es un servicio web que permite escanear cualquier **URL** para ver cómo se comporta en un navegador real. Captura una imagen, los scripts, recursos cargados, iframes, redirecciones, cookies y más. Es muy útil para analizar enlaces sospechosos, phishing y contenido malicioso.

---

### ️ Funciones clave:

- Captura de **pantalla del sitio web**.
    
- Lista de **todos los recursos cargados** (scripts, CSS, imágenes).
    
- Detección de **URLs maliciosas/redirecciones**.
    
- Geolocalización de dominios y servidores usados.
    
- Clasificación de riesgo según fuentes como VirusTotal, PhishTank, etc.
    
- API para integración y automatización.
    

---

###  Casos de uso:

- **Investigación de phishing**: escanea un enlace antes de abrirlo.
    
- **Detección de malware web**: scripts sospechosos, iframes ocultos, etc.
    
- **OSINT** sobre sitios que usan tecnología evasiva (trackers, cloaking).
    
- **Recogida de IoCs**: analiza qué recursos carga una URL maliciosa.
    
- **Blue Team**: análisis preventivo de enlaces entrantes.
    
- **Red Team**: fingerprinting de objetivos sin interacción directa.
    

---

###  ¿Ejemplo de uso con la API?

Sí, puedes automatizar escaneos con la API. Ejemplo en Python:

```python
import requests

API_KEY = 'TU_API_KEY'
url = 'https://urlscan.io/api/v1/scan/'

data = {
    'url': 'https://example.com',
    'public': 'on'
}

headers = {
    'API-Key': API_KEY,
    'Content-Type': 'application/json'
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```

¿Quieres ver cómo analizar el resultado del escaneo también en código?