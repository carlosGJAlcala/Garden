---
title: "Hemos encontrado lo siguiente"
date: 2026-01-26
tags:
  - ciberseguridad
  - practicas
---

### **Análisis de seguridad en un sitio WordPress**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/WPScan|WPScan]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Herramientas/Burp-suite|Burp suite]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Durante la revisión del sitio, se identificaron múltiples puntos de exposición y vulnerabilidades potenciales. A continuación, se detallan los hallazgos:

---

### **1. Archivos y rutas críticas encontradas**

- **`wp-cron.php`**
    
    - Función: se utiliza para ejecutar **tareas programadas** en WordPress.
        
    - Riesgo: se pueden realizar múltiples peticiones simultáneas (DoS), lo que puede **saturar el servidor** y dejar el sitio inaccesible.
        
    - Recomendación: deshabilitar el acceso público a este archivo o configurar su ejecución a través de **cron jobs** del servidor.
        
- **`wp-admin/`**
    
    - Riesgo: es la **ruta de administración por defecto**.
        
    - Vulnerabilidad: puede ser objetivo de **ataques de fuerza bruta** para obtener credenciales de administrador.
        
    - Recomendación:
        
        - Restringir acceso por IP o mediante autenticación adicional.
            
        - Cambiar la URL por defecto usando un plugin como _Hide My WP Ghost_.
            
- **`xmlrpc.php`**
    
    - Función: permite ejecutar funciones remotas, como publicación y administración de contenido.
        
    - Riesgo: si se tienen los parámetros correctos, se puede **ejecutar comandos críticos**, enviar contenido masivo o realizar ataques de fuerza bruta.
        
    - Recomendación: deshabilitar este archivo si no es estrictamente necesario o protegerlo con reglas en el firewall.
        
- **`wp-json/`** (REST API)
    
    - Permite visualizar la estructura completa de la API del sitio.
        
    - Ejemplo: `/wp-json/wp/v2/users` revela información de **usuarios registrados**, facilitando ataques de enumeración.
        
    - Recomendación: restringir el acceso a usuarios autenticados y configurar permisos adecuados.
        
- **`wp-activate.php`**
    
    - Riesgo: permite registrar o activar usuarios, lo que podría explotarse si no está controlado.
        
    - Recomendación: revisar su configuración y permisos.
        
- **`wp-includes/`**
    
    - Carpeta interna de WordPress que contiene código base.
        
    - Riesgo: exposición de información sensible y posible **path traversal**.
        
    - Recomendación: bloquear el acceso directo desde el navegador.
        
- **`admin-ajax.php`**
    
    - Punto de entrada legítimo para peticiones AJAX.
        
    - Riesgo: puede ser usado para ataques automatizados si no se valida correctamente la entrada.
        
- **Otros archivos analizados:**
    
    - `readme.html`: encontrado, revela la **versión exacta de WordPress** y detalles de la instalación.
        
    - `robots.txt`: contiene información sensible sobre rutas internas que no deberían ser públicas.
        
    - `sitemap.xml`: lista todas las URLs indexadas, útil para reconocimiento.
        
    - `log.php`: no encontrado (positivo, pero debe revisarse en caso de existencia).
        
    - `wpinfo.php`: no encontrado.
        
    - `wp-login.php`: encontrado, permite **enumeración de usuarios** a través de mensajes de error.
        

---

### **2. Enumeración y descubrimiento**

- Mediante escaneo manual y herramientas se identificaron rutas y patrones:
    
    - **Plugins y temas:**
        
        - El tema instalado **no está en su última versión**, lo que puede ser un vector de ataque.
            
        - **Elementor plugin:** detectado y **desactualizado**, lo que representa un alto riesgo.
            
    - **Versión de PHP expuesta:**
        
        - Encabezado `X-Powered-By` revela que el servidor usa PHP 5.6, versión obsoleta y con vulnerabilidades conocidas.
            
    - **Apache versionado:**
        
        - El archivo `xmlrpc.php` responde con un error _403 Forbidden_, pero revela la versión de **Apache 2.4.10 (Debian)**.
            

---

### **3. Herramientas utilizadas en el análisis**

- **WPScan:**
    
    - Utilizado para la enumeración de usuarios y detección de versiones vulnerables.
        
    - Ejemplo de comando:
        
        ```
        wpscan --url https://www.ejemplo.com
        ```
        
- **ZAP Proxy y Burp Suite:**
    
    - Herramientas utilizadas para mapeo manual y análisis de peticiones y respuestas.
        
    - ZAP permite _spidering_ manual para descubrir rutas ocultas.
        

---

### **4. Riesgos encontrados**

- Enumeración de usuarios mediante:
    
    - `/wp-json/wp/v2/users`
        
    - Mensajes de error en `wp-login.php`
        
- Plugins y temas desactualizados, como Elementor.
    
- Uso de versiones obsoletas:
    
    - PHP 5.6
        
    - Apache 2.4.10
        
- Rutas críticas accesibles públicamente:
    
    - `wp-cron.php`
        
    - `wp-admin/`
        
    - `xmlrpc.php`
        
- Información sensible revelada en:
    
    - `readme.html`
        
    - `robots.txt`
        
    - `sitemap.xml`
        

---

### **5. Recomendaciones**

1. **Actualizar WordPress, plugins y temas** a sus últimas versiones.
    
2. **Restringir acceso a archivos críticos** mediante reglas en el servidor o firewall.
    
3. **Deshabilitar XML-RPC** si no se utiliza.
    
4. **Ocultar la versión de WordPress y PHP** en los encabezados.
    
5. **Cambiar la URL por defecto de wp-admin** mediante plugins como _Hide My WP Ghost_.
    
6. Migrar a una versión **segura y soportada de PHP**, idealmente PHP 8.x.
    
7. Implementar medidas de protección contra fuerza bruta, como:
    
    - CAPTCHA en el login.
        
    - Limitación de intentos fallidos.
        
    - Autenticación multifactor (MFA).
        

---

# Hemos encontrado lo siguiente
wpa-admin encontrado, tenemos que dar las creadeciancel wp-admin es el path por defecto así que mal también.

log.php no encontrado

readme.html encontrado te da información de varios paht y las versiones que tiene

fichero robot.txt encontrado  Revelación de información sensible en el robots
wp-admin/admin-ajax.php

sitemap encontrado ( te da la información de las url que tiene)

xmlrpc.php forbidden pero te da la version del Apache 2.4.10 (Debian)

wp-jnso encontrado se diferencia del sitemap que muestra la estructura interna te da los métodos de las url

en el inspector  de código ver laversion buscar WordPress  plugins también  en los temas también puede haber vulnerabilidades .

wp-activate.php para meter usuario esta disponible
wp-includes encontrado  (path traversal) información sensible
 wp-cron.php hay acceso a este da un 200 
x -powered-by versión de php.5.6 
el tema no es la versión ultima 
elementor es un plugin no se recomienda y no está actualizada 

---

### **1. Acceso a VMware**

- **VMware**:
    
    - Riesgo: es posible acceder a máquinas virtuales de **VMware** a través de la **red** si la configuración de seguridad no es adecuada, exponiendo las máquinas a accesos no autorizados.
        
    - Recomendación:
        
        - **Asegurar las redes internas** donde se encuentra VMware, restringiendo el acceso solo a usuarios o sistemas de confianza.
            
        - Usar medidas como **VPNs** y segmentación de redes para limitar el acceso no autorizado.
            
        - Realizar un control de acceso adecuado a las interfaces de administración (por ejemplo, **vSphere Web Client**).
            

---

### **2. Uso de CDATA en HTML**

- **CDATA**:
    
    - **CDATA** (Character Data) es una sección en XML donde se pueden insertar caracteres especiales sin que sean interpretados como parte del código. Esta técnica también puede ser utilizada en **HTML** en situaciones específicas.
        
    - Riesgo: si se utilizan **CDATAs** en HTML, es posible que el contenido sea manipulado o ejecutado de forma no deseada si no se validan correctamente los datos, lo que podría ser aprovechado para inyectar scripts o realizar pruebas de **comprobación de seguridad** en formularios, comentarios o entradas.
        
    - Recomendación:
        
        - Asegurarse de que el contenido insertado en áreas críticas, como formularios o campos de entrada, esté adecuadamente **sanitizado** para evitar inyecciones o ataques XSS.
            
        - Evitar el uso innecesario de **CDATA** en HTML para mantener una correcta interpretación de los datos.
            

