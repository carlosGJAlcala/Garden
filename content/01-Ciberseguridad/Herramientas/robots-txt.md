---
title: "Robots Txt"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Cómo los Atacantes Utilizan `robots.txt` en Ciberseguridad**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]].

El archivo **`robots.txt`** es un archivo de texto utilizado en sitios web para indicar a los motores de búsqueda qué partes del sitio deben o no ser indexadas. Aunque su propósito principal es controlar la indexación de contenido por parte de los **web crawlers (bots de búsqueda como Googlebot)**, los atacantes pueden **abusar de este archivo** para obtener información sensible y posibles vectores de ataque.

---

## **1. ¿Qué es `robots.txt` y cómo funciona?**

El archivo **`robots.txt`** se encuentra en la raíz de un sitio web (por ejemplo, `https://ejemplo.com/robots.txt`) y sigue el estándar **Robots Exclusion Protocol (REP)**.

Ejemplo básico de `robots.txt`:

```txt
User-agent: *
Disallow: /admin/
Disallow: /backup/
Disallow: /private/
```

Este archivo indica que los **web crawlers** no deben acceder a `/admin/`, `/backup/` y `/private/`. Sin embargo, **esto no impide que un atacante acceda manualmente a esas rutas**.

---

## **2. ¿Cómo lo Usan los Atacantes?**

### **1️⃣ Enumeración de Rutas Sensibles**

Los atacantes buscan archivos `robots.txt` para descubrir rutas que podrían contener información sensible o acceso restringido.

Ejemplo de ataque:

1. Un atacante accede a `https://ejemplo.com/robots.txt` y encuentra:
    
    ```txt
    Disallow: /admin/
    Disallow: /db_backup/
    Disallow: /config.php
    ```
    
2. Luego intenta acceder manualmente a:
    
    ```
    https://ejemplo.com/admin/
    https://ejemplo.com/db_backup/
    https://ejemplo.com/config.php
    ```
    
3. Si el servidor no tiene controles de acceso adecuados, el atacante podría descubrir **paneles de administración, copias de seguridad de bases de datos o archivos de configuración** con credenciales.

---

### **2️⃣ Búsqueda de Paneles de Administración**

Muchos sitios bloquean directorios administrativos en `robots.txt`, lo que ayuda a los atacantes a encontrarlos.

Ejemplo de rutas que suelen aparecer en `robots.txt`:

```txt
Disallow: /wp-admin/
Disallow: /admin/
Disallow: /cpanel/
Disallow: /login/
```

El atacante simplemente intenta acceder a estas rutas para verificar si el sitio expone paneles de administración sin autenticación fuerte.

---

### **3️⃣ Descubrimiento de Archivos de Configuración y Backups**

Algunas empresas intentan evitar la indexación de archivos de configuración sensibles usando `robots.txt`, pero los atacantes los buscan directamente.

Ejemplo de archivos que pueden aparecer en `robots.txt`:

```txt
Disallow: /backup.zip
Disallow: /config.old
Disallow: /database.sql
```

Si estos archivos existen y no tienen restricciones de acceso adecuadas, un atacante podría **descargar bases de datos, configuraciones o archivos de código fuente**.

---

### **4️⃣ Extracción de información con OSINT y Google Dorks**

Los atacantes usan **Google Dorks** para encontrar archivos `robots.txt` expuestos en múltiples sitios.

Ejemplo de búsqueda en Google:

```
inurl:"robots.txt" site:ejemplo.com
```

Esto muestra directamente el archivo `robots.txt` de un sitio web específico.

Otra búsqueda para encontrar sitios con posibles rutas sensibles:

```
filetype:txt inurl:"robots.txt" -github
```

Esto busca archivos `robots.txt` en la web excluyendo GitHub, donde muchas configuraciones pueden estar indexadas.

---

## **3. Cómo Protegerse contra el Abuso de `robots.txt`**

1. **No incluir información sensible en `robots.txt`**
    
    - No uses `Disallow:` para ocultar rutas administrativas o archivos confidenciales.
    - Usa `robots.txt` solo para bloquear contenido irrelevante para motores de búsqueda.
2. **Usar autenticación y permisos adecuados**
    
    - Protege `/admin/`, `/cpanel/` y `/login/` con autenticación fuerte.
    - Configura permisos de acceso en el servidor para evitar accesos no autorizados.
3. **Bloquear escaneos no deseados**
    
    - Usa reglas en `htaccess`, `nginx.conf` o `firewall` para restringir acceso a `robots.txt` desde direcciones IP sospechosas.
    - Configura `fail2ban` para detectar accesos repetidos a rutas sensibles.
4. **Monitoreo de accesos a `robots.txt`**
    
    - Usa herramientas de monitoreo como **SIEM (Splunk, ELK Stack)** para detectar accesos sospechosos.
    - Revisa los logs con `grep`:
        
        ```bash
        cat /var/log/nginx/access.log | grep "robots.txt"
        ```
        
        Si ves múltiples accesos seguidos desde la misma IP, puede ser un escaneo malicioso.

---

## **4. Conclusión**

`robots.txt` es útil para controlar qué contenido indexan los motores de búsqueda, pero **no debe utilizarse como un mecanismo de seguridad**. Un atacante puede abusar de este archivo para descubrir rutas sensibles y acceder a información confidencial. **La mejor defensa es evitar listar rutas sensibles en `robots.txt`, implementar autenticación fuerte y monitorear accesos sospechosos**.