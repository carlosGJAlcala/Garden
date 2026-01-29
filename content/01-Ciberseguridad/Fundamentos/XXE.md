---
title: "Xxe"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
Un **XXE (XML External Entity)** es una vulnerabilidad de seguridad incluida en el [[owasp|OWASP Top 10]] que ocurre cuando una aplicación procesa documentos XML de forma insegura, permitiendo la inclusión de entidades externas definidas en el XML. Esto puede ser aprovechado por un atacante para acceder a archivos sensibles, realizar ataques de denegación de servicio, o interactuar con servicios internos de la red de la víctima (similar a [[SSRF]]).

---

### **¿Cómo funciona un XXE?**

XML permite la definición de **entidades externas**, que son referencias a recursos externos, como archivos locales o URLs. Si el procesador de XML utilizado en la aplicación no está configurado correctamente para deshabilitar estas entidades externas, un atacante podría manipular el contenido XML para explotarlas.

#### **Ejemplo básico de un XML con entidades externas:**

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>
  <data>&xxe;</data>
</root>
```

En este ejemplo:

- `<!ENTITY xxe SYSTEM "file:///etc/passwd">` define una entidad llamada `xxe` que apunta al archivo del sistema `/etc/passwd`.
- Cuando el procesador XML procesa `&xxe;`, incluye el contenido del archivo referenciado en lugar de la entidad.

Si una aplicación que procesa este XML no tiene la validación adecuada, el atacante podría leer el contenido del archivo `/etc/passwd`.

---

### **Tipos de ataques XXE**

1. **Robo de archivos locales:**
    
    - El atacante puede acceder a archivos sensibles en el sistema donde se procesa el XML.
    - Ejemplo:
        
        ```xml
        <!ENTITY xxe SYSTEM "file:///etc/shadow">
        ```
        
2. **Acceso a recursos de red internos:**
    
    - Un XXE puede usarse para interactuar con recursos internos (como servidores internos o APIs) que normalmente no están expuestos al atacante.
    - Ejemplo:
        
        ```xml
        <!ENTITY xxe SYSTEM "http://192.168.1.1/admin">
        ```
        
3. **Denegación de servicio (DoS):**
    
    - Utilizando referencias recursivas o entidades extremadamente grandes, un atacante puede agotar los recursos del sistema.
    - Ejemplo de "Billion Laughs Attack":
        
        ```xml
        <!DOCTYPE lolz [
          <!ENTITY lol "lol">
          <!ENTITY lol1 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
          <!ENTITY lol2 "&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;">
        ]>
        <lolz>&lol2;</lolz>
        ```
        
4. **Ejecución de comandos remotos:**
    
    - En ciertos casos, las entidades externas pueden explotarse para ejecutar comandos en el sistema.

---

### **Consecuencias de un ataque XXE**

- **Fuga de datos sensibles:**
    - Archivos como `/etc/passwd`, `/etc/shadow`, configuraciones de bases de datos o claves privadas pueden ser expuestos.
- **Denegación de servicio:**
    - El ataque puede consumir recursos de CPU y memoria, inutilizando el sistema.
- **Acceso a la red interna:**
    - Un atacante podría utilizar el servidor como punto de entrada para explorar servicios internos.
- **Escalación de privilegios:**
    - En escenarios avanzados, un XXE podría utilizarse para ejecutar código o comandos maliciosos.

---

### **Cómo prevenir un ataque XXE**

1. **Deshabilitar el soporte para entidades externas:**
    
    - Configura el procesador XML para que ignore las entidades externas. Por ejemplo, en Java con **DocumentBuilderFactory**:
        
        ```java
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        factory.setFeature("http://xml.org/sax/features/external-general-entities", false);
        factory.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
        factory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
        ```
        
2. **Validar y sanitizar el XML recibido:**
    
    - Asegúrate de que los datos XML provienen de fuentes confiables y realiza una validación antes de procesarlos.
3. **Usar bibliotecas seguras:**
    
    - Utiliza parsers XML modernos y seguros que tengan configuraciones predeterminadas para prevenir XXE (como Jackson, Xerces, o StAX).
4. **Considerar formatos alternativos:**
    
    - Si no es estrictamente necesario usar XML, considera formatos más seguros como JSON.

---

### **Detección de vulnerabilidades XXE**

Para identificar si una aplicación es vulnerable a XXE, puedes realizar pruebas con herramientas de pentesting como [[Burp-suite|Burp Suite]] u [[owasp-zap|OWASP ZAP]], o manualmente modificando documentos XML enviados a la aplicación.

Ejemplo de prueba:

```xml
<!DOCTYPE test [
  <!ENTITY xxe SYSTEM "file:///etc/hostname">
]>
<root>
  <data>&xxe;</data>
</root>
```

Si la respuesta de la aplicación incluye el contenido del archivo solicitado, es vulnerable.

---

### **Conclusión**

Un **XXE** es una vulnerabilidad peligrosa, pero fácilmente prevenible si se aplican las configuraciones adecuadas al procesador XML. Las mejores prácticas incluyen deshabilitar el soporte para entidades externas, validar la entrada XML y utilizar bibliotecas seguras. Con estas medidas, puedes minimizar significativamente el riesgo de un ataque XXE en tu aplicación.