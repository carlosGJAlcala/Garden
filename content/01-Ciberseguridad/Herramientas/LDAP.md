---
title: "Ldap"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
Perfecto . Vamos a elaborar **notas muy extensas, densas y técnicas sobre inyecciones LDAP (LDAP Injection)**, ideales para incluir en tus apuntes avanzados de pentesting.

---

###  **Inyección LDAP (LDAP Injection)**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

####  **Definición formal**

- **LDAP Injection** es una vulnerabilidad que ocurre cuando una aplicación **construye consultas LDAP dinámicamente usando datos suministrados por el usuario sin sanitizarlos adecuadamente**, permitiendo que el atacante **modifique la lógica de la consulta LDAP enviada al servidor de directorio**.
    

 Esto es **análogo a SQL Injection**, pero aplicado a servicios LDAP (Lightweight Directory Access Protocol), que gestionan datos jerárquicos como usuarios, grupos, permisos o cualquier recurso organizacional.

---

####  **¿Qué es LDAP? Contexto técnico**

 **LDAP = Lightweight Directory Access Protocol**:

- Protocolo estándar abierto para consultar y modificar servicios de directorio.
    
- Usado habitualmente en:
    
    - **Active Directory** (Microsoft).
        
    - OpenLDAP.
        
    - Otros directorios de usuarios.
        

Ejemplo de estructura típica en LDAP:

```
dn: uid=juan,ou=usuarios,dc=empresa,dc=com
cn: Juan Pérez
mail: juan@empresa.com
uid: juan
```

 Las consultas LDAP permiten:

- Autenticar usuarios.
    
- Consultar atributos.
    
- Gestionar permisos.
    

---

####  **Ejemplo básico de consulta LDAP vulnerable**

Supongamos una aplicación que autentica así:

```java
String filtro = "(uid=" + userInput + ")";
```

Si el usuario envía:

```
userInput = juan
```

El filtro generado sería:

```
(uid=juan)
```

Pero si envía:

```
userInput = *)(|(uid=*)
```

El filtro resultante sería:

```
(uid=*)(|(uid=*))
```

 **Esto podría devolver todos los registros existentes (`uid=*` → todos los usuarios).**

---

####  **Tipos de ataques LDAP Injection**

 **1️⃣ Bypass de autenticación:**

- Manipular filtros LDAP usados en login:
    
    - Entrada normal:
        
        ```ldap
        (&(uid=juan)(password=secreto))
        ```
        
    - Entrada maliciosa:
        
        ```
        user=*)(|(uid=*
        password=loquesea
        ```
        
    
    Resultado:
    
    ```ldap
    (&(uid=*)(|(uid=*))(password=loquesea))
    ```
    
    ️ **La consulta siempre devuelve `TRUE` y permite acceso no autorizado.**
    

---

 **2️⃣ Enumeración de usuarios:**

- Probar valores maliciosos que revelen información en mensajes de error:
    
    - `user=juan` → "Usuario válido, contraseña incorrecta".
        
    - `user=admin` → "Usuario válido, contraseña incorrecta".
        

---

 **3️⃣ Modificación de lógica en búsquedas:**

- Cambiar condiciones para incluir registros que normalmente estarían excluidos:
    
    - Inyectar operadores `|`, `&`, `!`.
        

---

 **4️⃣ Filtrado / Manipulación de grupos:**

- Si la aplicación usa LDAP para comprobar pertenencia a grupos:
    
    - `(&(memberOf=grupo1)(uid=usuario))` → manipular `uid` para devolver `TRUE`.
        

---

####  **Ejemplos prácticos de payloads LDAP Injection**

 Payloads típicos:

```
*)(uid=*)
*()|*
admin*)(password=*)
```

 **Bypass completo de login:**

```
usuario = *)(uid=*)
contraseña = cualquier valor
```

---

####  **Comportamiento según tecnologías backend**

|Tecnología|Comportamiento habitual|
|---|---|
|**Java (JNDI)**|Vulnerable si no sanitiza input antes de crear filtro LDAP.|
|**.NET (DirectoryServices)**|Similar: vulnerable si concatena input directamente.|
|**PHP (ldap_search)**|Vulnerable si construye dinámicamente el filtro sin validación.|

---

####  **Cómo detectar LDAP Injection en pentesting**

 **Metodología práctica:**  
1️⃣ **Identificar puntos donde se usan entradas para búsquedas o autenticación:**

- Formularios de login.
    
- Formularios de búsqueda de usuarios o contactos.
    
- Endpoints API que devuelven resultados basados en input del cliente.
    

2️⃣ **Enviar payloads controlados para comprobar si la lógica cambia:**

- `*)(uid=*)`
    
- `*()|*`
    
- `admin*)(password=*)`
    

3️⃣ **Analizar respuestas:**

- ¿Devuelve resultados cuando no debería?
    
- ¿Mensaje de error diferente al esperado?
    
- ¿Inconsistencia en conteo de resultados?
    

 Herramientas útiles:

- Burp Suite.
    
- Manual `curl`/`Postman`.
    
- Scripts Python personalizados.
    

---

####  **Impacto**

 **Impacto crítico dependiendo del contexto:**

- **Bypass total de autenticación.**
    
- Acceso a información sensible de todos los usuarios almacenados en el directorio.
    
- Manipulación de lógica de autorización basada en LDAP.
    
- Filtrado y robo de información PII (Personally Identifiable Information).
    

---

####  **Mitigaciones robustas**

 **Mejores prácticas defensivas:**

- **Nunca concatenar datos del usuario en filtros LDAP.**
    
- Usar APIs seguras con parámetros precompilados (si existen en el lenguaje/framework):
    
    - Ejemplo en Java (usar `DirContext.search` con `SearchControls` configurados correctamente).
        
- Escapar caracteres peligrosos antes de incluir input del usuario en filtros:
    
    - Caracteres peligrosos:
        
        - `*`
            
        - `(`
            
        - `)`
            
        - `\`
            
        - `|`
            
        - `&`
            

 Ejemplo de función de escape (Java):

```java
public static String escapeLDAPSearchFilter(String filter) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < filter.length(); i++) {
        char curChar = filter.charAt(i);
        switch (curChar) {
            case '\\':
                sb.append("\\5c");
                break;
            case '*':
                sb.append("\\2a");
                break;
            case '(':
                sb.append("\\28");
                break;
            case ')':
                sb.append("\\29");
                break;
            case '\0':
                sb.append("\\00");
                break;
            default:
                sb.append(curChar);
        }
    }
    return sb.toString();
}
```

- Validar sintáctica y semánticamente los inputs antes de pasarlos al backend LDAP.
    

 Seguridad por diseño:

- Implementar lógica de autorización adicional en backend, no solo confiar en resultados LDAP.
    

---

####  **Casos reales**

 **Casos documentados:**

- **Aplicaciones legacy en Java/JNDI** vulnerables por construir dinámicamente consultas LDAP usando datos sin sanitizar.
    
- **Portales web empresariales** donde LDAP Injection permitió autenticarse como administrador sin credenciales válidas.
    

---

 **Resumen denso para recordar:**

>  **LDAP Injection = vulnerabilidad que permite al atacante manipular consultas LDAP enviadas al servidor de directorio, alterando su lógica original para acceder a datos no autorizados o bypassar autenticaciones.**  
> Muy crítica cuando se usa para autenticación centralizada (ej.: Active Directory + aplicaciones web empresariales).  
> **Mitigación esencial: evitar concatenación directa + escape estricto de caracteres especiales + controles de acceso sólidos.**

---

 Si quieres puedo prepararte:

-  **Checklist avanzada de detección manual de LDAP Injection.**
    
-  **Ejemplos prácticos en varios lenguajes (Java, PHP, Python) de cómo implementar mitigaciones seguras.**
    

Solo dime  y lo preparo.