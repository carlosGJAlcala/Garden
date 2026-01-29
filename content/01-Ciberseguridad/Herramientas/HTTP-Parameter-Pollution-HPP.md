---
title: "Http Parameter Pollution Hpp"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
¡Excelente elección! Vamos a explicar **HTTP Parameter Pollution (HPP)** de forma **muy extensa, densa y técnica**, ideal para tus apuntes avanzados de pentesting y como recurso de estudio profesional.

---

###  **HTTP Parameter Pollution (HPP)**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[03-Desarrollo-Software/Concurrencia/servlets|servlets]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

####  **Definición formal**

- **HTTP Parameter Pollution (HPP)** es una técnica de ataque web que **consiste en inyectar múltiples parámetros con el mismo nombre en una solicitud HTTP**, con el objetivo de:
    
    - Manipular el comportamiento del servidor.
        
    - Bypassear validaciones de seguridad en aplicaciones vulnerables.
        
    - Alterar lógica de negocio.
        
    - Posiblemente desencadenar otros ataques (como XSS, SQLi, etc.).
        

---

####  **Fundamento técnico**

 **Las aplicaciones web procesan parámetros HTTP procedentes de distintos puntos:**

- Query String: `?user=admin&user=guest`
    
- Cuerpo de la petición (POST parameters).
    
- Headers HTTP (`Cookie` headers, por ejemplo).
    

 **El estándar HTTP/1.1 no especifica un comportamiento único cuando un cliente envía parámetros duplicados**, por lo que el tratamiento depende de:

- Framework/lenguaje backend utilizado (PHP, Python, Java, .NET...).
    
- Web servers o reverse proxies (Apache, Nginx, etc.).
    

 Ejemplo de HPP simple:

```http
GET /login?user=admin&user=guest HTTP/1.1
```

- ¿Qué valor toma `user`? Depende de la implementación:
    
    - Algunos frameworks usan **el primero** (`admin`).
        
    - Otros usan **el último** (`guest`).
        
    - Otros pueden construir **una lista/array** (`[admin, guest]`).
        

---

####  **Superficie de ataque**

HPP puede explotarse en distintos contextos:  
1️⃣ **En validaciones de lado cliente/server:**

- La aplicación revisa `user=admin` pero luego usa `user=guest` en lógica interna.
    

2️⃣ **Bypasseo de filtros de seguridad:**

- Un WAF o proxy puede validar el primer parámetro pero no todos.
    
- Ejemplo:
    
    - WAF ve: `amount=10&amount=1000` → permite `10`.
        
    - Backend usa `1000`.
        

3️⃣ **Combinado con ataques multi-vectoriales:**

- Inyección SQL: `id=1&id=1 UNION SELECT ...`
    
- XSS: `q=hello&q=<script>`
    

4️⃣ **HPP en cookies:**

- `Cookie: session=abc; session=malicious`
    

5️⃣ **Path parameter pollution:**

- No solo querystring: puede ser usado en `POST`, `PUT` o incluso `multipart/form-data`.
    

---

####  **Ejemplo práctico**

Supongamos que tenemos un formulario de cambio de contraseña:

```http
POST /change-password
Content-Type: application/x-www-form-urlencoded

user=juan&role=user
```

Un atacante podría enviar:

```http
POST /change-password
Content-Type: application/x-www-form-urlencoded

user=juan&role=user&role=admin
```

 Posibles efectos:

- La validación podría verificar `role=user`, pero si la lógica de autorización utiliza `role=admin` más adelante, el atacante consigue escalar privilegios.
    

---

####  **Comportamiento típico de tecnologías backend ante parámetros duplicados**

|Tecnología/Framework|Comportamiento ante parámetros duplicados|
|---|---|
|**PHP**|Devuelve el **último valor recibido**.|
|**Python (Flask, Django)**|Puede devolver **el primero o lista**.|
|**Java (Servlets)**|Devuelve el **primer valor**.|
|**.NET**|Devuelve el **primero o todos en lista**.|
|**Node.js (Express)**|Depende de configuración (`req.query`).|

---

####  **Cómo detectar vulnerabilidad HPP**

 **Metodología en pentesting:**

- Revisar puntos donde la aplicación recibe parámetros repetibles (login, filtros de búsqueda, formularios, API endpoints).
    
- Enviar manualmente parámetros repetidos con diferentes valores:
    
    - `param=value1&param=value2`
        
    - `param=value1&another=value2&param=value3`
        
- Analizar respuesta del servidor:
    
    - Diferencias en procesamiento (ver si cambia resultado en base al orden de los parámetros).
        
    - Comportamiento anómalo en headers HTTP devueltos.
        
- Revisar logs o interfaces administrativas si se pueden observar efectos secundarios.
    

 **Herramientas útiles:**

- Burp Suite:
    
    - **Extensiones como "Param Miner" ayudan a detectar HPP automáticamente.**
        
- OWASP ZAP.
    
- Pruebas manuales con `curl` o `Postman`.
    

---

####  **Impacto**

 El impacto depende del contexto:

- **Bypass de autorizaciones**: actuar como otro usuario.
    
- **Modificación de transacciones financieras**: cambiar montos.
    
- **Facilitador de inyecciones**: XSS, SQLi si combinado con input mal filtrado.
    
- **Salto de restricciones de filtros WAF / validadores intermedios**.
    

---

####  **Mitigaciones recomendadas**

 **Buenas prácticas para prevenir HPP:**

- **Normalizar parámetros antes de usarlos en lógica de negocio:**
    
    - Elegir explícitamente si se toma el primer valor, el último o si está permitido recibir listas.
        
- Validación estricta del lado servidor:
    
    - No asumir que solo llegará un valor.
        
    - Rechazar peticiones con parámetros duplicados cuando no se esperan listas.
        
- Hardening de proxies y WAF:
    
    - Configurar para inspeccionar **todos los valores de parámetros duplicados**, no solo el primero.
        
- Logging de anomalías:
    
    - Monitorizar entradas con repetición sospechosa de parámetros.
        

---

####  **Casos reales y referencias**

 **Casos conocidos:**

- Vulnerabilidades HPP detectadas en aplicaciones web críticas donde los atacantes pudieron manipular roles de usuario o saltarse validaciones de pago.
    
- Algunos frameworks antiguos son particularmente vulnerables si no se usa una validación explícita de parámetros repetidos.
    

 **OWASP referencia:**

- OWASP clasifica HPP como **ataque indirecto que permite bypass de filtros y validaciones de seguridad, a menudo combinable con vulnerabilidades principales (SQLi, XSS, auth bypass).**
    

---

 **Resumen denso para recordar:**

>  **HTTP Parameter Pollution = inyección intencionada de múltiples parámetros con el mismo nombre para manipular cómo el backend procesa la petición.**  
> Es una técnica peligrosa porque explota inconsistencias entre componentes de infraestructura (proxy, app, framework), facilitando bypasses y ataques secundarios.  
> Detalle clave: comportamiento ante duplicados varía según backend/framework/proxy → obliga al pentester a probar de forma exhaustiva.

---

Si quieres puedo prepararte:

-  **Checklist avanzada de pasos prácticos para detectar HPP en un engagement real.**
    
- ️ **Script en Python para enviar solicitudes con parámetros duplicados automáticamente y analizar respuestas.**
    

Solo dime  y lo preparo.