---
title: "Optionsbleed"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
**OptionsBleed** es una vulnerabilidad de seguridad relacionada con el servidor **HTTP OPTIONS**. En general, la vulnerabilidad **OptionsBleed** permite a un atacante obtener información sensible sobre la configuración del servidor web **a través de la respuesta al encabezado `OPTIONS`**, especialmente cuando no se gestionan adecuadamente las respuestas del servidor para esta solicitud.

###  **¿Qué es el encabezado HTTP OPTIONS?**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

El encabezado **HTTP OPTIONS** es un método que un cliente puede usar para **consultar las capacidades de un servidor web** sin enviar realmente una solicitud completa. La solicitud **OPTIONS** se utiliza para descubrir qué métodos HTTP son soportados por el servidor (por ejemplo, `GET`, `POST`, `PUT`, `DELETE`, etc.), y también se puede usar para consultar **otros parámetros de configuración** del servidor.

Por ejemplo, una solicitud **OPTIONS** típica podría verse así:

```http
OPTIONS / HTTP/1.1
Host: example.com
```

El servidor respondería con los métodos HTTP que soporta para esa URL o recurso específico. Un ejemplo de respuesta podría ser:

```http
HTTP/1.1 200 OK
Allow: GET, POST, HEAD, OPTIONS
```

Esto indica que el servidor soporta los métodos **GET**, **POST**, **HEAD** y **OPTIONS** para ese recurso.

###  **¿Cómo funciona OptionsBleed?**

La vulnerabilidad **OptionsBleed** se refiere a un tipo de **fuga de información** que ocurre cuando un servidor responde a una solicitud **OPTIONS** proporcionando más detalles de los que debería. Específicamente, **OptionsBleed** explota el hecho de que el encabezado **`Allow`** de la respuesta del servidor puede contener información que **revela detalles sobre los recursos y configuraciones del servidor** que podrían ser **no deseados** o **involuntarios**.

En situaciones donde no se manejan adecuadamente las solicitudes **OPTIONS**, un atacante podría realizar una **petición OPTIONS** a varias URLs o recursos en el servidor y obtener información detallada sobre qué métodos HTTP están habilitados, así como **otros recursos** que podrían ser accesibles o no protegidos.

###  **¿Cómo funciona un ataque OptionsBleed?**

1. **El atacante realiza una solicitud OPTIONS**:
    
    - El atacante realiza solicitudes **OPTIONS** a diferentes URL del servidor, buscando respuestas que revelen métodos y configuraciones adicionales sobre el servidor.
        
2. **Fuga de información sensible**:
    
    - Si la configuración del servidor no está correctamente restringida, la respuesta a la solicitud OPTIONS podría revelar información sensible, como:
        
        - Métodos HTTP disponibles en el servidor.
            
        - Recursos no protegidos o URLs específicas del servidor que no deberían ser accesibles o visibles.
            
        - Información sobre la configuración de **CORS (Cross-Origin Resource Sharing)**, lo que podría ser aprovechado en ataques de **cross-site scripting** o **cross-origin attacks**.
            
3. **Explotación**:
    
    - El atacante podría usar esta información para **mapear** los recursos expuestos en el servidor y luego intentar atacarlos mediante otros métodos, como **inyección SQL**, **XSS (Cross-Site Scripting)**, **fuerza bruta** de contraseñas, o **escalamiento de privilegios**.
        

###  **Impacto de OptionsBleed:**

- **Divulgación de recursos y configuraciones sensibles**: Los servidores que responden de manera excesiva a las solicitudes OPTIONS pueden revelar recursos adicionales que no deberían estar expuestos, lo que facilita que un atacante mapee la infraestructura del servidor.
    
- **Filtración de políticas de seguridad**: Un servidor podría **filtrar información sobre las políticas de seguridad** (como configuraciones de CORS) a través de la respuesta a una solicitud OPTIONS, lo que puede ayudar a un atacante a encontrar vulnerabilidades adicionales para explotar.
    
- **Ataques dirigidos más efectivos**: Si un atacante conoce qué métodos HTTP están habilitados en un servidor (por ejemplo, `PUT`, `DELETE`), podría intentar realizar ataques específicos aprovechando esos métodos, como **carga de archivos no autorizados**, **eliminación de archivos** o **modificación de datos**.
    

###  **Prevención de OptionsBleed:**

1. **Deshabilitar respuestas OPTIONS innecesarias**:
    
    - Asegúrate de que el servidor solo responda a solicitudes **OPTIONS** cuando sea necesario. Si no es necesario, puedes **deshabilitar la respuesta OPTIONS** en la configuración del servidor.
        
2. **Restricción de métodos HTTP**:
    
    - Configura el servidor para que solo permita los métodos HTTP que sean realmente necesarios. Si no necesitas que los usuarios puedan hacer **`PUT`**, **`DELETE`**, o cualquier otro método que implique modificación de datos, **deshabilítalos**.
        
3. **No revelar información sensible**:
    
    - Configura los servidores para que no **revelen detalles internos innecesarios** en la respuesta `Allow` del encabezado `OPTIONS`. Por ejemplo, solo devuelve los métodos realmente permitidos sin incluir configuraciones adicionales que podrían ser sensibles.
        
4. **Revisar configuraciones de seguridad**:
    
    - Asegúrate de que el servidor esté configurado adecuadamente para manejar solicitudes de tipo OPTIONS, y que las respuestas no revelen información sensible como los recursos internos.
        
5. **Uso de firewalls de aplicaciones web (WAF)**:
    
    - Los **WAFs** pueden ayudar a bloquear o filtrar solicitudes **OPTIONS** maliciosas, proporcionando una capa adicional de seguridad para prevenir la exposición de información no deseada.
        
6. **Verificar configuraciones CORS**:
    
    - En el caso de **CORS**, asegúrate de que las respuestas de las solicitudes **OPTIONS** no incluyan información que permita a un atacante explotar vulnerabilidades de **Cross-Origin**.
        

###  **¿Qué hacer si se está afectado por OptionsBleed?**

Si un servidor o sistema está afectado por **OptionsBleed**, es importante realizar las siguientes acciones:

- **Aplica parches y actualizaciones de seguridad**: Si la vulnerabilidad ha sido corregida en una nueva versión del servidor o software, actualiza el sistema a la última versión disponible.
    
- **Revisar configuraciones de seguridad**: Evalúa las configuraciones del servidor para asegurarte de que no se esté filtrando información sensible a través de respuestas **OPTIONS**.
    
- **Realizar auditorías de seguridad**: Realiza pruebas de penetración o auditorías de seguridad para verificar si hay otros puntos débiles en la infraestructura que puedan ser explotados por un atacante.
    

###  **Resumen:**

**OptionsBleed** es un tipo de **vulnerabilidad de fuga de información** en servidores web que puede ser explotada mediante solicitudes **OPTIONS** maliciosas. Cuando no se configuran correctamente, las respuestas de estos encabezados pueden revelar información sensible sobre los recursos del servidor, lo que facilita ataques dirigidos. Para protegerse contra esta vulnerabilidad, se recomienda **restringir la respuesta OPTIONS**, **revisar las configuraciones de seguridad** y **aplicar parches y buenas prácticas de configuración de servidores**.