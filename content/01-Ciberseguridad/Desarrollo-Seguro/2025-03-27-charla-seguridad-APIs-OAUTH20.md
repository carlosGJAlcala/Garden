---
title: "Seguridad por diseño en APIs web"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---
Perfecto, gracias por compartir esta excelente base de contenido. A continuación te presento **una versión revisada, ordenada y redactada de forma más clara, formal y técnica**, lista para usar como nota, informe o introducción a **seguridad por diseño en APIs web y el rol del arquitecto de seguridad**:

---

# Seguridad por diseño en APIs web


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/Microservicios|Microservicios]]. [[01-Ciberseguridad/Fundamentos/SolarWinds|SolarWinds]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]].

La **seguridad por diseño** es un enfoque proactivo que consiste en **integrar controles de seguridad desde las fases iniciales del ciclo de vida del software**, de manera que la seguridad esté incorporada en los propios principios arquitectónicos y no como un añadido posterior.

En el contexto de **APIs web**, este enfoque es especialmente relevante dado que las APIs suelen ser la superficie de exposición principal de aplicaciones modernas y servicios cloud, y por tanto están en el punto de mira de atacantes.

---

## ¿Qué hace un **arquitecto de seguridad**?

El **arquitecto de seguridad** es el profesional responsable de definir e integrar los requisitos de seguridad en el diseño de sistemas y aplicaciones. Su trabajo consiste en entender las amenazas a las que se enfrenta la organización y garantizar que la arquitectura resultante minimiza los riesgos.

Entre sus principales responsabilidades están:

- Definir los requisitos de seguridad para:
    
    - **Arquitecturas y activos de TI**
        
    - **Procesos de TI y de negocio**
        
- Gestionar el riesgo de seguridad:
    
    - Identificar, evaluar, tratar y en ocasiones mitigar riesgos que puedan afectar a los sistemas y datos.
        
- Colaborar en todas las fases:
    
    - **Diseño**
        
    - **Desarrollo**
        
    - **Explotación**
        
    - Revisión post-incidente (cuando ocurre un incidente grave, se vuelve al diseño para incorporar mejoras).
        

---

## Amenazas relevantes en el entorno europeo actual

El arquitecto de seguridad debe considerar amenazas contemporáneas que afectan a organizaciones en la UE, incluyendo:

- **Amenazas a la disponibilidad**: ataques DDoS que buscan interrumpir servicios.
    
- **Ransomware**: cifrado malicioso de datos y sistemas para pedir rescates.
    
- **Amenazas a datos personales y confidenciales**: filtraciones como la sufrida por El Corte Inglés o recolección masiva de datos para entrenamiento de inteligencia artificial (por ejemplo, "global coin").
    
- **Ingeniería social**: engaño a usuarios o empleados para obtener acceso.
    
- **Malware (como RATs)**: malware que permite a los atacantes tomar control remoto de equipos o robar cookies de sesión (session hijacking).
    
- **Ataques a la cadena de suministro**:
    
    - Ejemplo: ataque a **SolarWinds** en el contexto del conflicto Ucrania-Rusia.
        
    - La globalización y dependencia en terceros hace que muchas organizaciones dependan de componentes, librerías o servicios de proveedores externos.
        
    - **Ataques contra librerías de software son comunes y pueden tener efectos en cascada en todo el ecosistema**.
        

---

## Inventario y gestión de activos

Para un arquitecto de seguridad es esencial contar con un **inventario preciso de activos**, incluyendo:

- APIs desplegadas
    
- Componentes de infraestructura (servidores, bases de datos)
    
- Servicios cloud utilizados (AWS, Azure)
    
- Librerías y dependencias de software de terceros
    

El objetivo es **entender lo que existe para poder protegerlo adecuadamente**, dado que:

- **No se puede proteger lo que no se conoce**.
    
- Permite estimar el coste y esfuerzo de proteger los activos más críticos.
    

Las **sondas de red y herramientas de descubrimiento** permiten automatizar parte de esta tarea, mientras que en plataformas como AWS o Azure parte de la enumeración ya está incluida en sus herramientas de gestión.

---

## Seguridad efectiva

La seguridad debe estar en equilibrio:  
**Una seguridad efectiva es aquella que proporciona el nivel justo de protección sin sacrificar excesivamente la disponibilidad ni la usabilidad del sistema**.

Por ejemplo, aplicar controles como **mecanismos passwordless**, utilizando autenticación basada en OTP (HOTP y TOTP), puede aumentar la seguridad de acceso a las APIs sin hacer la experiencia del usuario innecesariamente compleja.

---

## Flujo de trabajo recomendado

El flujo de trabajo que debe guiar el enfoque de seguridad por diseño en APIs web sería:

1️⃣ **Requerimientos del negocio** →  
2️⃣ **Arquitectura de seguridad** (actúa como puente y garante de la seguridad) →  
3️⃣ **Arquitectura de software e implementación**, incluyendo el diseño de las APIs web seguras.

---




El flujo de trabajo sería: negocio -> arquitectura de seguridad (es como un puente mirando el tema de la seguridad) -> arquitectura de software.  
**Mecanismos passwordless** tipo **OTP** [[HOTP-Y-TOTP]].  
Hay curso de **cloud Azure**.  

# Principios de seguridad por diseño  

## Vulnerabilidad, amenaza, riesgo  
Cómo se prioriza: se utiliza criterio de riesgos. ¿Qué me puede pasar si no hago tal cosa utilizando X metodología (que es muy estructurada) para saber en qué centrarme?  

¿Qué es un **riesgo**?  
**Threats exploit vulnerability, the result is exposure which is risk, which is mitigated by safeguard, which protect assets which are endangered by threats.**  

# Mapa de riesgos  
A veces no se quiere que sea la probabilidad muy mínima y el impacto muy bajo porque puede afectar a la disponibilidad. Tienes que ver qué tan importante es.  

# Principios seguridad por diseño: **ZERO TRUST**  
- **Comprobar explícitamente**: accesos basado en identidad, meter más comprobaciones. Este concepto con **zero-trust** (defensa en profundidad) es la desconfianza. Verificar en todos los puntos de la cadena (perímetro, red, aplicación, acceso al dato, etc.).  
- **Privilegios mínimos**: Acceso **just in time** (solo en un tiempo determinado).  
- **Asumir vulneración**: Supervisión continua de la seguridad (puedes tener un **info stealer**).  
En **hardware** se mira tema de análisis e integridad con la **BIOS**.  

# Seguridad por diseño en APIs web  
Un servicio a la hora de desarrollar sería las **tripas**, y cómo se usa es la **API**. También te da un manual de cómo se utiliza. La clave es que esté bien **documentado**.  

**HHS API Flaw Exposes Critical Mobile Security Risks**  

## ¿Por qué proteger las APIs?  
**Past single API call: seconds to minutes**.  
**Known attacks: SQLi, XSS, etc.**  
**Today**: Secuencia de API call se busca mal funcionamiento antes que los ataques previamente dichos.  
**Business logic attacks** requiere contexto.  

## Mecanismos control de acceso en API  
- **Nada API SECRET**  
- **IP origen**  
- **API KEY**  
- **API KEY + KEY**  
Lo que aplica más hoy en día en autenticación es tema de los **tokens**.  

## **OAuth Agent**: la aplicación que usas  
- **IdP** = Identity Provider  
- **PAP** = Policy Administration Point  
- **PDP** = Policy Decision Point  
- **PEP** = Policy Enforcement Point  
- **Los recursos** son los datos que quiere consultar.  
- **Resource Server**  
- **User Agent**: aplicación.  
- **Authorization Server (IdP)**: es el proveedor de identidad.  
- **PAP**: Punto de administración de políticas.  
- **PDP**: Punto de decisión de políticas.  

La clave está utilizando **JWS/JWT**.  

### Tokens y credenciales  
Los tipos de token son:  
- **Access_token**: llave de puerta para los datos del usuario.  
- **Opaco**: identificador de base datos.  
- **JWT**  
- **Refresh token**  
- **Client-id**  
- **Client-secret**  
- **Claves pública/privada**  
- **JWKS key set**  

### Flujos grant types  
- **Authorization Code**  
- **PKCE**  
- **Device Code**  
- **Client Credentials**  
- **Refresh Token**  
Y el **Authorization Server** le devuelve un **access_token**.  



---

### **OAuth Authorization Code Grant**

Es el flujo más completo y seguro para aplicaciones con _backend confidencial_, como aplicaciones web o móviles que pueden proteger un `client_secret`. Se utiliza cuando el cliente necesita acceso a los recursos del usuario, y se requiere una autorización explícita por parte del mismo.

#### **Pasos del flujo:**

1. **El usuario quiere iniciar sesión** en una aplicación que actúa como cliente OAuth.
    
2. La aplicación **redirecciona al usuario** a una **URI de autorización (redirect URI)** en el **Authorization Server** (por ejemplo, el servidor de Microsoft o Google), incluyendo el `client_id`, `redirect_uri`, `scope`, `state`, y `response_type=code`.
    
3. El usuario **inicia sesión en el Identity Provider (IdP)** y da su **consentimiento**.
    
4. El Authorization Server redirige de nuevo a la `redirect_uri` de la aplicación **con un Authorization Code** (lo que tú llamas “pre-token”).
    
5. El cliente **intercambia ese código** (Authorization Code) por un **Access Token** y opcionalmente un **Refresh Token**, enviando su `client_secret`.
    
6. Con el Access Token, el **user agent (cliente)** se conecta al **Resource Server** para acceder a los recursos protegidos del usuario.
    

> **Ventajas:** flujo seguro, no expone credenciales ni tokens directamente al navegador, ideal para aplicaciones que manejan información sensible.

---

### **OAuth Authorization Code Grant con PKCE** (Proof Key for Code Exchange)

Es una variante del Authorization Code Grant pensada para aplicaciones públicas como **Single Page Applications (SPA)** o apps móviles, donde **no se puede guardar de forma segura un client secret**.

#### **Diferencias clave:**

- No requiere `client_secret`.
    
- Se utiliza un **PKCE challenge/verifier**:
    
    - La app genera un `code_verifier` aleatorio y calcula un `code_challenge` (una versión en hash).
        
    - Durante el primer paso (autorización), se envía el `code_challenge`.
        
    - Al pedir el Access Token con el código, se debe enviar el `code_verifier`.
        
    - El servidor compara el `verifier` con el `challenge` original.
        


---

### **OAuth Refresh Token Grant**

Permite obtener un **nuevo Access Token** sin que el usuario tenga que volver a autenticarse, utilizando un **Refresh Token** previamente emitido.  
Esto es útil para mantener sesiones largas de forma segura sin tener que solicitar el login repetidamente.

- El Refresh Token se almacena de forma segura en el cliente (idealmente en el backend).
    
- El cliente lo envía al Authorization Server para obtener un nuevo Access Token.
    
- Se puede usar hasta que expire o sea revocado.
    

> **Ventajas:** mejora la experiencia de usuario, reduce el número de inicios de sesión, y permite control centralizado de expiración de sesiones.

---

### **OAuth Client Credentials Grant**

Este flujo es utilizado cuando una **aplicación necesita acceder a recursos protegidos que no pertenecen a un usuario final**, sino que están bajo el control de la propia aplicación (por ejemplo, APIs internas, servicios entre máquinas, microservicios, etc.).

- No hay intervención del usuario (por eso se le llama flujo de **dos patas**).
    
- El cliente envía su `client_id` y `client_secret` al Authorization Server.
    
- Recibe un Access Token para acceder al Resource Server.
    

> **Ventajas:** simple y directo, ideal para servicios automatizados y _backend-to-backend_.

---

### **OAuth JWT Assertion (Bearer)**

Este flujo permite que el cliente obtenga un Access Token **utilizando un JWT firmado con una clave privada**.  
Se usa especialmente en integraciones _server-to-server_ en las que:

- Se requiere alta seguridad.
    
- El cliente prefiere **usar una clave asimétrica** en lugar de un `client_secret`.
    

#### **Pasos clave:**

1. El cliente construye un JWT con información sobre la solicitud (audiencia, emisor, tiempo de expiración…).
    
2. Firma el JWT con su clave privada.
    
3. Envía ese JWT como `assertion` al Authorization Server.
    
4. Recibe un Access Token como respuesta.
    

> **Ventajas:** autenticación robusta, escalable y segura sin necesidad de secretos compartidos. Ampliamente usado por plataformas como Google Cloud y Azure.

---

¿Quieres que te prepare una tabla comparativa de estos flujos o que amplíe los flujos que faltan como Device Code y CIBA?

## **OAuth Resumen**  
- **Authorization Code**: cliente confidencial, 3 patas.  
- **Authorization Code PKCE**: público, 3 patas.  
- **Device Code**: Capacidad I/O restringida, 3 patas.  
- **Refresh Token**: todos, 2 y 3 patas.  
- **Client Credentials**: Confidencial, 2 patas.  
- **JWT Bearer/Assertion**: Confidencial, 2 y 3 patas.  
**Público**: es que no tiene backend.  

## **OAuth Buenas Prácticas de Seguridad**  
- Comparación exacta de **redirect_URI**.  
- Generación y validación de **state**.  
- **PKCE** siempre mejor, se recomienda.  
- Evitar **grant types** obsoletos.  
- Custodia de secretos.  
- Rotado de claves.  
- Duración de tokens.  
- **Single logout**.  
- No se guarden los tokens en el **user agent**.  
- Uso de **mTLS** o **DPoP** (Demonstrating Proof of Possession).  
- Asignar mínimo privilegios.  
- **IETF Draft: OAuth 2.0**.  
Esto es una herramienta muy valiosa para privilegios.  

Hay un ataque en el que pide una aplicación que te pide de permisos.  

---

## **OpenID Connect**

Añade una capa de identidad sobre **OAuth** mediante el **ID Token**.  
El **ID Token** permite saber quién es el usuario.  
A diferencia de OAuth puro, en OpenID Connect se incluye un **ID Token** que identifica al usuario, y se lo entrega al **user agent**.

## **OpenID Connect CIBA Grant**

**CIBA** (_Client-Initiated Backchannel Authentication Flow_)  
Utiliza un **canal secundario (backchannel)**. Es el flujo usado, por ejemplo, en sistemas de pagos bancarios.

---

## Desarrollo Seguro: Top 10 Vulnerabilidades de Seguridad

Del proyecto **OWASP**.

### **BOLA (Broken Object Level Authorization)**

Permite acceder a los objetos de otro usuario. Ejemplo típico: **Path Traversal**.

### **BOPLA (Broken Object Property Level Authorization)**

Permite modificar propiedades que el usuario no debería poder modificar.

### **Broken Function Level Authorization**

Permite a usuarios sin privilegios acceder a funciones protegidas.

### **Security Misconfiguration**

Malas configuraciones de seguridad, especialmente en cabeceras CORS.  
Depende de cómo se configuren las cabeceras en el servidor para impedir que sitios maliciosos llamen a la API.

Cabeceras clave:

- `Access-Control-Allow-Origin`
    
- `Access-Control-Allow-Methods`
    
- `Access-Control-Allow-Headers`
    
- `Access-Control-Allow-Credentials`
    

---

## Protección de APIs: Deserialización

Es importante proteger los datos que se deserializan, ya que pueden ser vectores de ataque.

- Los datos son objetos que deben serializarse/deserializarse en memoria del servidor.
    
- Hace falta aplicar protecciones específicas.
    
- Un WAF tradicional no detecta problemas de deserialización en APIs.
    
- En cambio, un **API WAF** (por ejemplo, WAAP o WAF con soporte para APIs) sí puede detectar estos ataques.
    

---

## Construir una buena definición de la API

Una de las estrategias clave es crear un fichero **Swagger/OpenAPI** que describa cómo es la API.  
Esto permite:

- Definir los endpoints disponibles.
    
- Especificar métodos, parámetros, tipos de datos.
    
- Generar documentación automática.
    
- Realizar validación estructural de las peticiones y respuestas.
    

---

# **Software 2.0**

**Vibe coding**

Para proteger los **modelos generativos** se puede utilizar tecnología como **Microsoft Semantic Kernel**, que evalúa probabilísticamente la salida del modelo y permite integrar protecciones contextuales.

---











