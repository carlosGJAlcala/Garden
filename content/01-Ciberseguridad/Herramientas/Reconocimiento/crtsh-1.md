---
title: "Crtsh 1"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  crt.sh (Ct)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/Amass|Amass]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Crtsh|Crtsh]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/DNSDumpster|DNSDumpster]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Naabu|Naabu]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]].

- **Nombre completo:** **crt.sh – Certificate Transparency Log Search**
    
- **Símbolo en la tabla:** **Ct**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Buscador de certificados SSL/TLS públicos (OSINT)
    
- **Sitio oficial:** [https://crt.sh](https://crt.sh/)
    

---

##  ¿Qué es crt.sh?

**crt.sh** es un buscador gratuito que permite consultar los registros públicos de **transparencia de certificados** (CT logs). Estos registros contienen todos los **certificados digitales TLS/SSL emitidos por autoridades certificadoras públicas**, con el objetivo de **evitar fraudes y emitir alertas tempranas** si se generan certificados no autorizados.

Para profesionales de la ciberseguridad, crt.sh es una **fuente valiosa de información OSINT**, ya que permite descubrir **dominios, subdominios, organizaciones y relaciones de infraestructura** a partir de los certificados SSL expuestos.

---

##  ¿Para qué sirve en ciberseguridad?

|Aplicación|Descripción|
|---|---|
| Enumeración de subdominios|Subdominios usados en certificados públicos, incluso los que no aparecen en DNS|
| Reconocimiento temprano|Detectar dominios recién creados antes de que sean indexados por buscadores|
| Caza de phishing|Encontrar certificados emitidos para dominios similares o suplantados|
| Auditoría de seguridad|Verificar qué dominios están cubiertos por certificados válidos|
| Blue Team defensivo|Detectar si alguien ha generado certificados para tu organización sin permiso|

---

## ️ ¿Cómo funciona crt.sh?

crt.sh consume información de **Certificate Transparency Logs**, una especie de blockchain público donde se registran todos los certificados emitidos. Los registros provienen de:

- Let's Encrypt
    
- DigiCert
    
- GlobalSign
    
- Sectigo
    
- Cloudflare
    
- Google CA
    
- etc.
    

Permite buscar por:

-  Nombre de dominio (ejemplo.com)
    
-  SHA1/SHA256 hash del certificado
    
-  Nombre de la organización emisora
    
-  CA emisora del certificado
    
-  Fecha de emisión y expiración
    

---

##  Ejemplo de búsqueda en crt.sh

###  Buscar subdominios asociados a `example.com`

Entra en:

```
https://crt.sh/?q=%25.example.com
```

El `%25` representa `%` codificado en URL, lo que hace una búsqueda de **cualquier subdominio** de `example.com`.

#### Ejemplo de resultados:

|Nombre común (CN)|Subdominios encontrados|
|---|---|
|*.dev.example.com|dev.example.com|
|portal.admin.example.com|portal.admin.example.com|
|stage-api.example.com|stage-api.example.com|

---

##  ¿Qué información útil devuelve crt.sh?

-  Common Name (CN)
    
-  Subject Alternative Names (SANs)
    
-  Fecha de emisión / expiración
    
-  Algoritmo de firma
    
-  CA emisora
    
-  Número de serie y hash del certificado
    
-  Enlace al PEM (certificado descargable)
    

---

##  Casos reales de uso

1. **Reconocimiento en campañas de Red Team**  
    Encuentras `vpn-interno.example.com` emitido por Let's Encrypt, lo que revela que es accesible desde fuera.
    
2. **Detección de typosquatting o phishing**  
    Buscas certificados de `g00gle.com` o `m1crosoft-support.com` para ver si alguien ha emitido SSL para dominios similares.
    
3. **Auditoría defensiva**  
    Descubres que un proveedor ha emitido certificados a nombre de tu empresa sin tu conocimiento.
    

---

##  Consideraciones de defensa

Desde el **Blue Team**, crt.sh es útil para:

- Establecer alertas automáticas con servicios como [Facebook's CertWatcher](https://github.com/facebook/certwatcher) o [Certstream](https://certstream.calidog.io/).
    
- Detectar **registro no autorizado** de dominios o subdominios.
    
- **Responder rápidamente** ante la aparición de certificados sospechosos.
    
- Verificar si los certificados cumplen las **políticas de seguridad TLS** de la organización (expiración, cifrado, etc.).
    

---

##  Uso en scripts o automatización

Aunque crt.sh no tiene una API oficial documentada, es posible hacer **scraping sencillo** del HTML o usar proyectos como:

- `crtsh.py` (wrapper en Python)
    
- `Subfinder` (de ProjectDiscovery) que puede usar crt.sh como fuente
    
- `Sublist3r` y `Amass` también pueden integrar crt.sh
    

Ejemplo básico con curl:

```bash
curl "https://crt.sh/?q=%25.example.com&output=json"
```

Devuelve los resultados en JSON si se especifica `&output=json`.

---

##  Comparación con otras herramientas de subdominios

|Herramienta|Fuente principal|Incluye subdominios de CT logs|
|---|---|---|
|crt.sh|Certificate Transparency||
|Subfinder|OSINT + APIs||
|Amass|DNS, CT logs, web||
|DNSDumpster|DNS y passive DNS||
|Shodan|Escaneo activo||

---

##  Conclusión

**crt.sh** es una herramienta fundamental en el reconocimiento de dominios, tanto para equipos ofensivos (Red Team, Bug Bounty) como defensivos (Blue Team, SOC). Gracias a los logs públicos de transparencia de certificados, puedes detectar rápidamente **subdominios expuestos, dominios recién creados, y posibles fraudes de identidad digital**.

---

¿Quieres que prepare un **script en Bash o Python** para obtener subdominios de un dominio objetivo usando crt.sh y filtrarlos por fecha? ¿O que integremos esto en un pipeline de reconocimiento completo junto a Naabu, HTTPX y Nuclei?