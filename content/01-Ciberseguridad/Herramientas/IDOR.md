---
title: "Idor"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
.

---

###  **IDOR (Insecure Direct Object Reference)**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[03-Desarrollo-Software/Distribuido/Microservicios|Microservicios]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Herramientas/Burp-suite|Burp suite]].

####  **Definición formal**

- **IDOR = Insecure Direct Object Reference (Referencia Directa a Objetos Insegura).**
    
- Vulnerabilidad de control de acceso donde la aplicación expone identificadores de recursos **directamente a los usuarios** y permite su manipulación **sin validar adecuadamente si el usuario tiene autorización sobre ese recurso**.
    

 **El origen de IDOR está en que la aplicación confía en que los usuarios solo accederán a los objetos que deberían, basándose en identificadores que suelen ser predecibles o fácilmente manipulables.**

---

####  **Contexto técnico**

 **Tipos comunes de "objetos" que suelen ser expuestos:**

- Identificadores numéricos (`user_id=1001`, `order_id=5001`).
    
- Nombres de archivos (`GET /download?file=report_123.pdf`).
    
- Códigos UUID (`/users/9a8b7c6d-1234-5678-9101-abcdefabcdef`).
    
- Direcciones de correo o nombres de usuario (`/profile?username=john`).
    

 **Cómo se manifiesta:**

- La aplicación permite acceder a `/profile?id=1001` → atacante modifica a `/profile?id=1002` y obtiene datos de otro usuario.
    
- No existe validación correcta de propiedad o autorización: **se confunde autenticación con autorización**.
    

---

####  **Ejemplo práctico sencillo**

Supongamos una aplicación vulnerable:

```http
GET /invoice?id=1001 HTTP/1.1
Host: vulnerable.com
Cookie: session=abcd1234
```

Si el atacante modifica `id=1001` a `id=1002` y logra ver o descargar la factura de otro cliente:  
 **Vulnerabilidad IDOR confirmada.**

---

####  **Tipos de recursos vulnerables a IDOR**

- Perfiles de usuario (`GET /user?id=...`).
    
- Documentos privados (`/docs?docid=...`).
    
- Tickets de soporte (`/ticket/12345`).
    
- Fotos privadas (`/gallery/photo/filename.jpg`).
    
- API REST (sobre todo en microservicios donde se usa `UUID` en paths y params).
    

---

####  **Impacto**

 **Impacto puede ser crítico:**

- Filtrado de datos personales (PII → Personal Identifiable Information).
    
- Acceso a facturas, historiales médicos, datos bancarios.
    
- Acceso a configuraciones privadas de usuarios.
    
- Exposición de recursos privados como archivos o imágenes.
    

 Cuando la aplicación maneja datos sensibles:

- IDOR puede violar regulaciones como **GDPR** o **HIPAA**.
    
- Potencial escalada horizontal (entre usuarios normales) o vertical (usuario normal → admin).
    

---

####  **IDOR en APIs modernas**

 **RESTful APIs son muy susceptibles a IDOR**:

- URLs limpias:
    
    ```
    GET /api/v1/accounts/123
    ```
    
    Sin validación: modificar `123` a `124` accede a otra cuenta.
    

 **Por diseño REST**, los identificadores están en la URL → **ataque más natural y más crítico si no hay control de acceso robusto en backend**.

---

####  **Cómo detectar IDOR en pentesting**

 **Metodología manual:**  
1️⃣ Identificar recursos que aceptan parámetros de entrada con identificadores:

- `id=`, `user_id=`, `docid=`, `/users/{userId}`, etc.
    

2️⃣ Modificar los valores de esos parámetros:

- Incrementar/decrementar números.
    
- Usar IDs de usuarios conocidos o predecibles.
    
- Fuzzing de UUIDs conocidos.
    

3️⃣ Analizar respuesta:

- ¿Devuelve datos del objeto ajeno?
    
- ¿Permite modificación (PUT, DELETE) de recursos ajenos?
    

 **Fuzzing automatizado:**

- Usar herramientas como:
    
    - **Burp Suite Intruder** para iterar IDs numéricos.
        
    - **Autorize extension (Burp)**: automatiza detección de problemas de autorización → muy eficaz en detección masiva de IDOR.
        
    - **Postman / scripts Python** → manipular requests masivamente y comparar resultados.
        

---

####  **Limitaciones en detección**

️ IDOR puede ser:

- **Horizontal:** acceso a datos de otro usuario igual que el atacante (ej.: dos clientes).
    
- **Vertical:** acceso a recursos de mayor privilegio (ej.: cliente accediendo a configuración de administrador).
    

️ **Blind IDOR:** aplicación no devuelve datos pero permite alterar recursos internos (por ejemplo, cambiar la dirección de envío de otro cliente silenciosamente).

---

####  **Mitigaciones recomendadas**

 **Controles fundamentales:**

- **Autorización robusta en servidor:**
    
    - No confiar en parámetros del cliente.
        
    - Validar siempre que el usuario autenticado tiene permiso sobre el objeto solicitado.
        
    - **Autorización contextual**: `currentUser.id == resource.ownerId`.
        
- **Diseño defensivo:**
    
    - No exponer identificadores sensibles o fácilmente predecibles.
        
    - Utilizar identificadores aleatorios no secuenciales (UUID → pero **ojo: no es suficiente por sí solo**).
        
- **Segregación por roles y permisos:**
    
    - Revisar todos los endpoints donde existan recursos específicos a un usuario.
        

 Importante:

> **Control de acceso siempre en backend** → nunca depender de controles ocultos en frontend.

---

####  **Casos reales de impacto**

 Ejemplos históricos:

- Vulnerabilidad IDOR en aplicaciones de banca online → permitió a atacantes acceder a cuentas de clientes simplemente incrementando `account_id`.
    
- IDOR en apps de mensajería → acceso a mensajes privados ajenos.
    
- IDOR en servicios de facturación → descarga masiva de facturas de otros usuarios.
    

---

####  **Diferencia clave: IDOR vs inseguridad de sesión**

 IDOR no requiere robar cookies ni tokens:

- **La sesión puede ser válida y autorizada, pero la aplicación no verifica que el recurso consultado pertenece a ese usuario.**
    

 **Es un fallo en lógica de autorización, no en autenticación.**

---

 **Resumen denso para recordar:**

>  **IDOR = vulnerabilidad lógica donde la aplicación permite al usuario referenciar directamente recursos mediante identificadores modificables (ID, UUID, nombre archivo), sin comprobar si ese usuario tiene permiso sobre ellos.**  
> Impacto crítico en apps con datos sensibles, altamente prevalente en APIs REST y microservicios mal protegidos.  
> **Mitigación: controles de autorización sólidos en backend + no confiar nunca en parámetros manipulables por el cliente.**

---

 Si quieres puedo prepararte:

-  **Checklist avanzada para detección de IDOR en APIs REST.**
    
- ️ **Laboratorio práctico: detección manual y automatizada con Burp Suite (Autorize + Intruder).**
    

Solo dime  y lo preparo.