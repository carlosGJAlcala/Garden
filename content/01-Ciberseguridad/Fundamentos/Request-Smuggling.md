---
title: "Request Smuggling"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
**Request Smuggling** (o "engullido de solicitudes") es una técnica de ataque en la que un atacante explota las diferencias de interpretación de las solicitudes HTTP entre los servidores intermediarios (como **proxies** o **balanceadores de carga**) y los servidores finales para **inyectar solicitudes maliciosas**. El atacante puede **“mezclar”** o **"ocultar"** una solicitud HTTP dentro de otra para que el servidor final procese la solicitud maliciosa sin que los servidores intermedios la detecten.

Este tipo de ataque puede tener consecuencias graves, como **elevación de privilegios**, **ejecución de código malicioso**, **desbordamiento de búferes** o **elusión de mecanismos de seguridad**.

###  **¿Cómo funciona el Request Smuggling?**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

En **Request Smuggling**, los atacantes aprovechan las diferencias en cómo los servidores **intermediarios** y los servidores **finales** procesan las **cabezas de solicitud HTTP** y la **secuencia de las solicitudes**. Estos ataques ocurren cuando los diferentes componentes de la infraestructura HTTP (como **proxy inverso**, **balanceadores de carga**, etc.) **interpretan de manera diferente** los encabezados HTTP o los límites de la solicitud.

La técnica se basa en manipular las **cabeceras HTTP** (como **Content-Length** o **Transfer-Encoding**) para crear una solicitud maliciosa que se "oculta" o "encapsula" dentro de una solicitud válida.

###  **Ataque típico de Request Smuggling:**

1. **Solicitud 1**: Un atacante envía una solicitud HTTP que parece ser **válida** a un **proxy o balanceador de carga**. Esta solicitud es generalmente interpretada correctamente por el proxy, pero el **servidor final** la procesa de manera diferente.
    
2. **Solicitud 2 (encapsulada)**: En la misma conexión HTTP, el atacante envía una segunda solicitud **dentro** de la primera. El servidor final, al recibir la solicitud, puede **desempaquetar y procesar la solicitud adicional** (la solicitud maliciosa) sin que el proxy intermedio la detecte.
    
3. **Resultado**: El servidor final ejecuta la solicitud maliciosa que originalmente fue **ocultada** en la solicitud legítima. Esto puede tener como resultado la **ejecución de comandos** no autorizados o la **elusión de controles de seguridad**.
    

###  **Ejemplo básico de Request Smuggling:**

Imagina una situación donde un balanceador de carga y un servidor web final interpretan de manera diferente las cabeceras `Content-Length` o `Transfer-Encoding`.

1. El atacante envía una solicitud que contiene dos cabeceras de `Content-Length` o **Transfer-Encoding** conflictivas. Por ejemplo:
    
    - **Primera solicitud (envía una cabecera `Content-Length` con un valor incorrecto)**:
        
        ```
        POST / HTTP/1.1
        Host: victim.com
        Content-Length: 13
        Transfer-Encoding: chunked
        
        0\r\n\r\n
        POST / HTTP/1.1
        Host: victim.com
        Content-Length: 13
        ```
        
2. El **proxy** puede interpretar solo la primera parte (el primer `Content-Length` o `Transfer-Encoding`), mientras que el **servidor final** interpreta la segunda solicitud incrustada dentro de la primera.
    
3. El **servidor final** procesa la segunda solicitud, que puede ser un **comando malicioso**.
    

###  **Tipos de Request Smuggling:**

1. **Smuggling por `Content-Length` y `Transfer-Encoding`**:
    
    - Este es uno de los tipos más comunes de **Request Smuggling**. Un atacante puede manipular las cabeceras **`Content-Length`** y **`Transfer-Encoding`** para crear solicitudes conflictivas que causen que el servidor y el proxy las procesen de manera diferente.
        
2. **Smuggling por múltiples conexiones**:
    
    - Este tipo de ataque se basa en dividir la solicitud HTTP en múltiples conexiones, lo que puede permitir que un atacante manipule cómo se gestionan las solicitudes en diferentes puntos de la infraestructura.
        
3. **Smuggling por manipulación de cabeceras**:
    
    - Manipulando las cabeceras HTTP, un atacante puede insertar datos adicionales en las solicitudes que **el servidor final** procesa como una solicitud separada, mientras que el **proxy o balanceador de carga** no lo hace.
        

###  **Consecuencias de un ataque de Request Smuggling**:

- **Bypass de seguridad**: Los atacantes pueden **eludir mecanismos de seguridad** como **firewalls** o **determinadas validaciones** de entradas, lo que permite realizar acciones no autorizadas.
    
- **Ejecución de código malicioso**: Si el ataque es exitoso, el atacante podría ejecutar **código malicioso** en el servidor final que procesa la solicitud oculta.
    
- **Acceso no autorizado**: Los atacantes pueden aprovechar estas vulnerabilidades para obtener acceso no autorizado a recursos o ejecutar **acciones privilegiadas** en el servidor.
    
- **Denegación de servicio (DoS)**: Si se manipulan adecuadamente las solicitudes, un atacante podría generar solicitudes maliciosas que sobrecarguen o hagan que los servidores se comporten de manera inesperada, provocando **fallos** o **denegaciones de servicio**.
    

###  **Cómo protegerse contra Request Smuggling:**

1. **Configuración de proxies y balanceadores de carga**:
    
    - Los servidores **proxy** o **balanceadores de carga** deben ser configurados para manejar correctamente los encabezados HTTP y evitar que los atacantes puedan insertar solicitudes maliciosas dentro de otras solicitudes.
        
    - Deshabilitar **Transfer-Encoding: chunked** y **Content-Length** en las mismas solicitudes puede ayudar a evitar que los atacantes manipulen los valores.
        
2. **Validación estricta de encabezados**:
    
    - Los proxies y servidores deben validar correctamente los encabezados **`Content-Length`**, **`Transfer-Encoding`** y otros encabezados relacionados con el procesamiento de solicitudes.
        
    - **Descartar solicitudes malformadas**: Las solicitudes con múltiples valores de `Content-Length` o `Transfer-Encoding` deben ser descartadas inmediatamente.
        
3. **Manejo de solicitudes multipartes**:
    
    - Es recomendable evitar la **recepción de múltiples solicitudes multipartes** en una sola conexión HTTP o validar adecuadamente la consistencia de estas solicitudes antes de procesarlas.
        
4. **Actualización de software**:
    
    - Mantén **actualizados** los **servidores web**, **balanceadores de carga** y **proxies** para asegurarte de que las últimas vulnerabilidades relacionadas con Request Smuggling sean corregidas.
        
5. **Auditoría y monitoreo**:
    
    - Implementa **monitoreo** de las solicitudes HTTP y analiza patrones inusuales o maliciosos. Las herramientas de detección de intrusos pueden identificar tráfico sospechoso asociado con ataques de Request Smuggling.
        
6. **Uso de cabeceras seguras**:
    
    - Implementa tecnologías de seguridad como **HTTP Strict Transport Security (HSTS)** y **Content Security Policy (CSP)**, que también pueden ayudar a prevenir ataques de este tipo.
        

###  **Resumen:**

El **Request Smuggling** es un tipo de ataque que explota las diferencias en cómo los proxies y servidores finales interpretan las solicitudes HTTP, lo que permite al atacante ocultar una solicitud maliciosa dentro de una solicitud válida. Esto puede dar lugar a **ejecución de código malicioso**, **elusión de controles de seguridad** y **acceso no autorizado**. Para protegerse, es fundamental **validar adecuadamente las cabeceras HTTP**, **configurar correctamente los proxies** y **realizar auditorías constantes** en las aplicaciones y servidores web.