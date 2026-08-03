---
title: "Tecnologias Triple A"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema1principiosbasicossi
---
Las **tecnologías Triple A** en seguridad de la información hacen referencia a tres componentes fundamentales del **control de accesos**:

---

## Tecnologías Triple A: Autenticación, Autorización y Accountability


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Acceso-remoto/Acceso-remoto|Acceso remoto]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Estas tres funciones trabajan en conjunto para **verificar identidades, conceder permisos y dejar trazabilidad de las acciones** realizadas por usuarios en un sistema.

---

### 1.  **Autenticación (Authentication)**

Confirma que el usuario es quien dice ser.

- Se basa en:
    
    - Algo que sabes (contraseña, PIN)
        
    - Algo que tienes (token, tarjeta)
        
    - Algo que eres (biometría)
        
- Puede implementarse con **SSO (Single Sign-On)**, **Kerberos**, o autenticación multifactor (MFA).
    

---

### 2.  **Autorización (Authorization)**

Una vez autenticado, define **a qué recursos puedes acceder y con qué permisos**.

- Modelos comunes:
    
    - **DAC** (Discretionary Access Control)
        
    - **MAC** (Mandatory Access Control)
        
    - **RBAC** (Role-Based Access Control)
        

 RBAC es el más usado en empresas: el acceso se da en función del **rol**, no del individuo.

---

### 3.  **Accountability (Contabilidad / Trazabilidad)**

Permite **atribuir acciones a usuarios concretos** y reconstruir lo que han hecho:

- Bitácoras (logs)
    
- Auditorías
    
- Firma digital
    
- Trazabilidad
    

---

##  Protocolos y tecnologías Triple A más comunes

Según el documento FGSI-T1-Control de accesos:

###  **RADIUS** (Remote Authentication Dial-In User Service)

- Muy usado en redes WiFi, VPN, proxies, etc.
    
- Soporta **autenticación, autorización y contabilidad**
    
- Basado en UDP (rápido pero no cifrado por defecto)
    

###  **TACACS+**

- Protocolo propietario de Cisco
    
- Separa claramente autenticación, autorización y contabilidad
    
- Basado en TCP (más confiable que UDP)
    

###  **DIAMETER**

- Evolución de RADIUS (más robusto y flexible)
    
- Usa TCP/SCTP, permite mejor seguridad
    
- Diseñado para entornos móviles, VoIP, AAA distribuido
    

---

##  ¿Dónde se usan las tecnologías Triple A?

- Redes corporativas (VPN, WiFi empresarial)
    
- Sistemas de acceso remoto (por ejemplo, SSH con 2FA)
    
- Aplicaciones Web con SSO
    
- Plataformas cloud (IAM de AWS, Azure AD, etc.)
    
- Seguridad en redes de telecomunicaciones
    

---

##  Conclusión

> Las tecnologías **Triple A** son la **columna vertebral del control de accesos moderno**, y permiten garantizar que:
> 
> - Solo accede quien está **debidamente autenticado**.
>     
> - Solo ve o hace aquello para lo que está **autorizado**.
>     
> - Todo lo que hace puede ser **auditado o trazado**.
>     

---