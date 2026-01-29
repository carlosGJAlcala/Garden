---
title: "Hotp Y Totp"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---
 
### **¿Qué son HOTP y TOTP?**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

HOTP (**HMAC-Based One-Time Password**) y TOTP (**Time-Based One-Time Password**) son dos algoritmos de generación de **contraseñas de un solo uso (OTP, One-Time Password)** utilizados en sistemas de autenticación para aumentar la seguridad de los accesos.

Ambos métodos generan un código temporal que el usuario debe introducir para autenticarse, pero funcionan de manera distinta.

### **1. HOTP (HMAC-Based One-Time Password, RFC 4226)**

**¿Cómo funciona?**

- HOTP se basa en una **clave secreta compartida** entre el servidor y el usuario, junto con un **contador** que se incrementa en cada intento de autenticación.
- Cada vez que el usuario genera una OTP, el servidor valida el código y **aumenta el contador**, evitando que el mismo código pueda usarse dos veces.
- Se calcula usando la función: HOTP(K,C)=Truncate(HMAC−SHA1(K,C))HOTP(K, C) = Truncate(HMAC-SHA1(K, C)) donde:
    - **K** es la clave secreta.
    - **C** es el contador (un número que se incrementa con cada autenticación).
    - **HMAC-SHA1** es la función hash criptográfica utilizada.

**Ventajas y desventajas de HOTP**  
️ No depende del tiempo, por lo que se puede utilizar incluso si el reloj del usuario y el servidor están desincronizados.  
️ Funciona bien en **tokens físicos** (hardware tokens).  
 Puede generar problemas si el usuario genera varias OTP sin usarlas, ya que el contador puede desincronizarse con el servidor.  
 Menos seguro que TOTP, ya que los códigos pueden permanecer válidos hasta que se utilicen.

### **2. TOTP (Time-Based One-Time Password, RFC 6238)**

**¿Cómo funciona?**

- TOTP es una evolución de HOTP que **sustituye el contador por un valor basado en el tiempo**.
- En lugar de un número de secuencia, se utiliza un **timestamp** que cambia en intervalos regulares (normalmente cada 30 segundos).
- La fórmula es similar a HOTP, pero con el tiempo en lugar del contador: TOTP(K,T)=Truncate(HMAC−SHA1(K,T))TOTP(K, T) = Truncate(HMAC-SHA1(K, T)) donde:
    - **K** es la clave secreta.
    - **T** es el número de intervalos de tiempo transcurridos desde la época Unix (ej. `floor(Tiempo actual / 30s)`).
    - **HMAC-SHA1** genera el código OTP.

**Ventajas y desventajas de TOTP**  
️ Más seguro que HOTP, ya que los códigos expiran en segundos y no pueden reutilizarse.  
️ Es más fácil de sincronizar, ya que solo depende del reloj del usuario y del servidor.  
 Puede haber problemas si los relojes del usuario y del servidor están desincronizados.  
 No es ideal para tokens físicos sin reloj integrado.

---

## **3. Diferencias entre HOTP y TOTP**

|**Característica**|**HOTP**|**TOTP**|
|---|---|---|
|**Factor de autenticación**|Contador secuencial|Timestamp (ej. cada 30 segundos)|
|**Validez del código**|Hasta que se utilice|Expira después de unos segundos|
|**Sincronización**|Puede desincronizarse si el usuario genera muchos códigos sin usarlos|Solo depende del tiempo del servidor y el usuario|
|**Seguridad**|Menos seguro porque un código puede usarse hasta que se invalide|Más seguro porque los códigos expiran rápidamente|
|**Ideal para**|Tokens físicos y entornos sin conexión a internet|Aplicaciones móviles, autenticación en línea|

---

## **4. Aplicaciones actuales de HOTP y TOTP**

### ** Aplicaciones de HOTP**

HOTP se usa en dispositivos donde la sincronización con un servidor en tiempo real puede ser difícil. Ejemplos:

- **Tokens físicos de hardware** (ej. RSA SecurID, YubiKey en modo HOTP).
- **Autenticación en cajeros automáticos y tarjetas inteligentes**.
- **Sistemas bancarios offline**, donde se generan códigos OTP en tarjetas de coordenadas o dispositivos sin conexión.

### ** Aplicaciones de TOTP**

TOTP es más popular en aplicaciones modernas, especialmente en autenticación de dos factores (**2FA, Two-Factor Authentication**). Ejemplos:

- **Aplicaciones de autenticación móvil**:
    - Google Authenticator
    - Microsoft Authenticator
    - FreeOTP
    - Authy
- **Seguridad en plataformas en línea**:
    - Autenticación en Gmail, Facebook, Twitter, Instagram y WhatsApp.
    - Acceso seguro a cuentas en servicios en la nube (ej. AWS, GitHub).
- **Acceso a VPNs y redes corporativas**:
    - OpenVPN, Cisco AnyConnect.
- **Autenticación en sistemas de banca en línea**.
- **Integración con OAuth2 y JWT para MFA (autenticación multifactor)**.

---

## **5. Relación con OAuth2 y JWT**

- **OAuth2** es un protocolo que permite a los usuarios autorizar aplicaciones para acceder a sus datos sin compartir sus credenciales.
- **JWT (JSON Web Token)** es un estándar para representar información de autenticación de manera segura.
- **TOTP y HOTP se pueden combinar con OAuth2 y JWT** para agregar autenticación de dos factores en sistemas modernos:
    1. Un usuario inicia sesión con su contraseña y recibe un **token JWT**.
    2. Se le solicita ingresar un código **TOTP** generado en su app autenticadora.
    3. Si el código es válido, OAuth2 concede acceso con un **token de acceso**.
    4. El usuario puede acceder a los recursos protegidos con su **JWT**.

Esta integración aumenta la seguridad, ya que incluso si un atacante roba el JWT, **no podrá autenticarse sin el código TOTP**.

---

## **6. Conclusión**

- **HOTP y TOTP son métodos de generación de contraseñas de un solo uso para mejorar la autenticación.**
- **TOTP es más seguro y ampliamente usado en aplicaciones modernas debido a su expiración rápida.**
- **Se utilizan en autenticación de dos factores (2FA), VPNs, bancos, plataformas en línea y seguridad corporativa.**
- **Pueden integrarse con OAuth2 y JWT para reforzar la seguridad en entornos de autenticación web y APIs.**

Si estás configurando un sistema de autenticación segura, **TOTP es la mejor opción para aplicaciones en línea**, mientras que **HOTP sigue siendo útil en tokens físicos y entornos desconectados**.