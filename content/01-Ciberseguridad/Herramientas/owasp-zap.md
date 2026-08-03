---
title: "Owasp Zap"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **OWASP ZAP (Zed Attack Proxy): Herramienta de Seguridad para Aplicaciones Web**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**OWASP ZAP (Zed Attack Proxy)** es una herramienta de seguridad gratuita y de código abierto desarrollada por **OWASP (Open Web Application Security Project)**. Su principal objetivo es ayudar a **identificar vulnerabilidades en aplicaciones web** mediante pruebas de penetración automatizadas y manuales.

Se considera una alternativa a [[Burp-suite|Burp Suite]], aunque con un enfoque más accesible para principiantes y con una gran comunidad de soporte. Basado en los principios de [[owasp|OWASP Top 10]].

---

## **1. Características Principales de OWASP ZAP**

 **Intercepta y modifica tráfico HTTP/S**: Permite analizar y manipular las peticiones y respuestas entre el navegador y el servidor.  
 **Escaneo automatizado de vulnerabilidades**: Identifica fallos como inyección SQL, XSS, CSRF, fallos en autenticación, etc.  
 **Fuzzing de parámetros**: Prueba entradas con valores inesperados para detectar posibles vulnerabilidades.  
 **Modo proxy y man-in-the-middle (MITM)**: Intercepta y analiza tráfico entre el navegador y la aplicación.  
 **Plugins y extensibilidad**: Compatible con scripts en Python, JavaScript y Groovy para personalizar pruebas.  
 **Integración con CI/CD**: Compatible con Jenkins, GitHub Actions y otros pipelines de seguridad.  
 **Modo "Spider" para descubrimiento de URLs ocultas**: Rastrea enlaces y parámetros en la aplicación web.

---

## **2. Instalación de OWASP ZAP**

### ** En Windows y macOS**

1. Descarga la última versión desde la web oficial:  
     [https://www.zaproxy.org/download/](https://www.zaproxy.org/download/)
2. Instala y ejecuta la aplicación.

### ** En Linux (Debian/Kali/Ubuntu)**

1. Descarga el paquete desde OWASP:
    
    ```bash
    wget https://github.com/zaproxy/zaproxy/releases/download/v2.11.1/ZAP_2_11_1_unix.sh
    ```
    
2. Dale permisos de ejecución:
    
    ```bash
    chmod +x ZAP_2_11_1_unix.sh
    ```
    
3. Instálalo y ejecútalo:
    
    ```bash
    ./ZAP_2_11_1_unix.sh
    zaproxy &
    ```
    

También puedes instalarlo con **Snap**:

```bash
sudo snap install zaproxy --classic
```

---

## **3. Modos de Uso de OWASP ZAP**

### **1. Modo Interceptador (Proxy MITM)**

- Configura tu navegador para usar **OWASP ZAP como proxy**.
- Captura y edita solicitudes antes de que lleguen al servidor.
- Permite modificar parámetros y headers para probar vulnerabilidades.

### **2. Escaneo Automático**

- Detecta vulnerabilidades comunes en la aplicación con un solo clic.
- Recomendado para **pruebas rápidas** de seguridad.

### **3. Escaneo Manual (Modo Avanzado)**

- Permite a los pentesters realizar pruebas más detalladas.
- Se pueden modificar peticiones, hacer ataques de fuerza bruta y pruebas específicas.

### **4. Integración en DevSecOps (CI/CD)**

- Se puede integrar con herramientas como **Jenkins, GitHub Actions o GitLab CI**.
- Permite realizar escaneos de seguridad en pipelines de desarrollo.

---

## **4. Ejemplo de Escaneo Automático con ZAP**

1. **Iniciar OWASP ZAP**.
2. **Ingresar la URL de la aplicación web** en la barra de "Quick Scan".
3. **Ejecutar el escaneo** y revisar los resultados.
4. **Analizar las vulnerabilidades detectadas** y exportar un informe.

---

## **5. OWASP ZAP vs Burp Suite**

|**Característica**|**OWASP ZAP**|**Burp Suite**|
|---|---|---|
|**Licencia**|Open Source|Comercial (versión gratuita limitada)|
|**Facilidad de uso**|Fácil para principiantes|Más avanzado|
|**Automatización de escaneo**|Sí|Sí (versión Pro)|
|**Extensibilidad con scripts**|Sí (Python, Groovy, JS)|Sí (Java, Burp Extender)|
|**Integración en CI/CD**|Sí|Solo en versión Pro|

 **Conclusión:** ZAP es ideal para quienes buscan una herramienta gratuita y potente para pruebas de seguridad web, mientras que **Burp Suite** es más robusto en la versión de pago.

---

## **6. Conclusión**

- **OWASP ZAP es una de las mejores herramientas gratuitas para pentesting web**.
- **Permite detectar vulnerabilidades en aplicaciones web** de manera automática y manual.
- **Es ideal para principiantes y profesionales**, con una gran comunidad y documentación.
- **Se integra en DevSecOps**, permitiendo escaneos en **CI/CD** para mejorar la seguridad en desarrollo.

Si buscas una alternativa gratuita a Burp Suite con grandes capacidades, **OWASP ZAP es la mejor opción**. 