---
title: "Burp Suite"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Burp Suite: Herramienta de Pentesting Web**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Burp Suite es una de las herramientas más utilizadas para realizar **pruebas de seguridad en aplicaciones web**. Desarrollada por PortSwigger, permite a los pentesters interceptar, analizar y modificar el tráfico entre un navegador y un servidor web. Es ampliamente utilizada para detectar **vulnerabilidades como [[SQLMap|inyección SQL]], cross-site scripting ([[XXE|XSS]]) y fallos en autenticación** (ver [[owasp|OWASP Top 10]]).

> **Alternativa gratuita**: [[owasp-zap|OWASP ZAP]] es una alternativa de código abierto con funcionalidades similares.

---

## **1. Características Principales de Burp Suite**

- **Interceptación de tráfico HTTP/S**: Actúa como un proxy para capturar y modificar solicitudes antes de enviarlas al servidor.
- **Burp Scanner**: Escanea automáticamente aplicaciones en busca de vulnerabilidades.
- **Fuzzing y manipulación de parámetros**: Permite probar entradas con datos maliciosos.
- **Gestión de sesiones y autenticación**: Permite analizar y modificar tokens de sesión, cookies y cabeceras HTTP.
- **Análisis de respuestas del servidor**: Permite ver respuestas completas, incluidas cabeceras y cuerpos de respuesta.
- **Extensibilidad**: Compatible con scripts en Python y Java mediante Burp Extender.
- **Modo automático y manual**: Puede ser usado para escaneo automatizado o pruebas manuales avanzadas.

---

## **2. Versiones de Burp Suite**

- **Burp Suite Community Edition**: Gratuita, con funciones limitadas (sin escaneo automatizado).
- **Burp Suite Professional**: Versión de pago con escáner automático y más funcionalidades avanzadas.
- **Burp Suite Enterprise**: Orientada a empresas con automatización de pruebas en CI/CD.

---

## **3. Instalación de Burp Suite**

### En Windows y macOS

1. Descargar desde la web oficial:  
    [https://portswigger.net/burp](https://portswigger.net/burp)
2. Instalar y ejecutar el archivo descargado.

### En Linux (Debian/Kali/Ubuntu)

1. Descargar Burp Suite:
    
    ```bash
    wget https://portswigger.net/burp/releases/download?product=community&version=latest&type=Linux
    ```
    
2. Dar permisos de ejecución:
    
    ```bash
    chmod +x burpsuite_community_linux.sh
    ```
    
3. Instalar Burp Suite:
    
    ```bash
    ./burpsuite_community_linux.sh
    ```
    
4. Ejecutarlo desde el menú o con:
    
    ```bash
    burpsuite &
    ```
    

---

## **4. Cómo Usar Burp Suite**

1. **Configurar el navegador** para que use Burp Suite como proxy en `127.0.0.1:8080`.
2. **Interceptar tráfico HTTP/S** para analizar solicitudes y respuestas.
3. **Modificar peticiones** en tiempo real para probar vulnerabilidades.
4. **Usar Burp Scanner** (versión Pro) para encontrar fallos automáticamente.
5. **Exportar reportes** con hallazgos de seguridad.

---

## **5. Casos de Uso**

- **Pruebas de seguridad en aplicaciones web**.
- **Análisis de tráfico para detección de vulnerabilidades**.
- **Manipulación de parámetros en formularios y API REST**.
- **Explotación de sesiones y tokens de autenticación**.
- **Pruebas de fuzzing en entradas de usuario**.

---

## **6. Diferencias entre Burp Suite y OWASP ZAP**

|Característica|Burp Suite|OWASP ZAP|
|---|---|---|
|**Licencia**|Comercial (versión gratuita limitada)|Open Source|
|**Escaneo Automático**|Solo en versión Pro|Sí (gratis)|
|**Facilidad de uso**|Más avanzado|Más accesible|
|**Extensibilidad**|Java y Burp Extender|Python, JS y Groovy|
|**Integración en CI/CD**|Solo en versión Enterprise|Sí|

Burp Suite es la opción preferida por pentesters profesionales debido a su potencia, mientras que **OWASP ZAP es más accesible y completamente gratuito**.

---

## **7. Conclusión**

Burp Suite es una herramienta esencial en el pentesting web, permitiendo interceptar, modificar y analizar tráfico HTTP/S. Su versión gratuita es útil para análisis manuales, pero la versión Pro agrega capacidades avanzadas de escaneo automatizado. Es una opción robusta para profesionales de seguridad que buscan detectar y explotar vulnerabilidades en aplicaciones web.