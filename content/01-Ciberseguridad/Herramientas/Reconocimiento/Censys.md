---
title: "Censys"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Censys (Ce)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Fofa|Fofa]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Subfinder|Subfinder]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ZMap|ZMap]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

- **Nombre completo:** **Censys**
    
- **Símbolo en la tabla:** **Ce**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Motor de búsqueda de infraestructura expuesta en Internet
    
- **Sitio web oficial:** [https://censys.io](https://censys.io/)
    
- **API oficial:** [https://search.censys.io/api](https://search.censys.io/api)
    

---

##  ¿Qué es Censys?

**Censys** es una plataforma avanzada de **inteligencia de superficie de ataque**, que indexa continuamente todos los hosts accesibles en Internet mediante escaneos activos. Su objetivo es ofrecer una visión **completa, en tiempo real y contextualizada** de la infraestructura expuesta de cualquier organización, país o dirección IP pública.

Es una alternativa a Shodan, pero con un enfoque más orientado a **seguridad ofensiva, cumplimiento y gobernanza**, permitiendo búsquedas específicas sobre:

- Puertos abiertos
    
- Certificados TLS/SSL
    
- Servicios vulnerables
    
- Tecnologías web
    
- Metadatos de infraestructura
    

---

##  ¿Para qué sirve Censys en ciberseguridad?

|Aplicación|Descripción|
|---|---|
| Mapeo global de infraestructura|Visualizar todo lo expuesto en una organización o red pública|
| Identificación de servicios inseguros|Detectar puertos abiertos, servicios obsoletos o cifrados débiles|
| Análisis de certificados TLS|Buscar emisores, errores de configuración, fingerprint duplicados|
|️ OSINT avanzado|Reconocimiento pasivo y activo en campañas Red Team|
| Gobernanza y cumplimiento|Control de shadow IT y superficies expuestas sin autorización|

---

## ️ ¿Qué información ofrece?

Censys proporciona información técnica de bajo nivel, como:

- **Banner completo del servicio**
    
- **Versión del protocolo o software**
    
- **Certificados SSL/TLS (Common Name, SANs, CA emisora, fechas)**
    
- **Geolocalización e ISP**
    
- **Sistemas operativos detectados**
    
- **Puertos y servicios activos**
    
- **Reputación de seguridad (exposición, errores, anomalías)**
    

---

##  Ejemplos de uso

###  Búsqueda web sencilla:

```
https://search.censys.io/hosts?q=services.service_name%3A%22http%22+AND+location.country%3A%22Spain%22
```

Esto buscará servidores HTTP en España.

---

###  Búsqueda de dominios con TLS emitido por Let's Encrypt:

```
services.tls.certificates.leaf_data.issuer.common_name: "Let's Encrypt"
```

---

###  Desde la línea de comandos con la CLI oficial

```bash
pip install censys
censys config
```

Luego puedes ejecutar:

```bash
censys search "services.service_name: 'ssh'" --view
```

---

###  Con la API en Python:

```python
from censys.search import CensysHosts
h = CensysHosts()

results = h.search("services.service_name: 'http' AND location.country: 'ES'", per_page=5)
for r in results:
    print(r["ip"], r["services"])
```

---

##  Casos de uso ofensivo (Red Team)

- Descubrir **subdominios y activos expuestos** no conocidos por el cliente.
    
- Identificar **certificados TLS** con nombres internos (como `intranet.empresa.local`).
    
- Verificar qué infraestructura ha sido expuesta por error (por ejemplo, staging, test).
    
- Obtener **servicios inseguros (telnet, FTP, SMB sin cifrar)** accesibles desde Internet.
    
- Detectar servidores con **firmas de software vulnerables**.
    

---

##  Casos de uso defensivo (Blue Team)

- Auditoría continua de **infraestructura de red expuesta** públicamente.
    
- Identificación de activos de **shadow IT** (servidores olvidados o sin control).
    
- Validación del cumplimiento de políticas de cifrado TLS.
    
- Supervisión de infraestructura multicloud (AWS, Azure, GCP, servidores propios).
    
- Revisión de exposición de puertos abiertos e inconsistencias de configuración.
    

---

##  Comparativa con otras plataformas OSINT

|Plataforma|Tipo de escaneo|Enfoque principal|API disponible|Especialidad|
|---|---|---|---|---|
|**Censys**|Activo (ZMap + ZGrab)|Seguridad avanzada||Certificados, puertos, banners|
|Shodan|Activo (próximo a real-time)|IoT, banners generales||Dispositivos, interfaces web|
|ZoomEye|Activo + pasivo|Ciberinteligencia china||Servicios, dispositivos|
|FOFA|Activo + pasivo|Infraestructura web||China, subdominios, CMS|

---

##  Recomendaciones de uso

- Censys tiene una **cuota gratuita generosa** pero limitada: ideal para investigaciones puntuales o pruebas.
    
- Usa filtros específicos (`organization.name`, `location.country`, `services.port`) para reducir el volumen de datos.
    
- A diferencia de Shodan, puedes acceder al **certificado completo** y a detalles estructurados de cada campo TLS.
    

---

##  Conclusión

**Censys** es una herramienta clave para cualquier profesional que quiera tener una **visión completa y en tiempo real de lo expuesto en Internet**. Su enfoque en seguridad ofensiva, defensa proactiva, cumplimiento y visibilidad global lo convierte en una herramienta OSINT de referencia para:

- Analistas de amenazas
    
- Equipos de Red y Blue Team
    
- Equipos de gobernanza y GRC
    
- Certs, CSIRTs y gobiernos
    

---

¿Te gustaría que te cree un script que combine Subfinder + Censys + HTTPX para detectar servicios y tecnologías activas de una organización real? ¿O una guía paso a paso para analizar tus propios dominios en Censys con la CLI y la API?