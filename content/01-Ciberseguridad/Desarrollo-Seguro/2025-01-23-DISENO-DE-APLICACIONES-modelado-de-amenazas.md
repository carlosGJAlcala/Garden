---
title: "Estrategias de modelado de amenazas"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---
El **modelado de amenazas** es una técnica esencial en el desarrollo seguro que permite identificar, entender y mitigar los riesgos de seguridad antes de que se materialicen, protegiendo así los activos más valiosos de un sistema.

---

### Principios fundamentales del desarrollo seguro


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

Estos principios guían el diseño y construcción de sistemas resistentes frente a amenazas y fallos:

- **Mínimo privilegio**: cada entidad (usuario, proceso) solo debe tener los permisos estrictamente necesarios para realizar su función.
    
- **Fallo a estado seguro**: en caso de fallo, el sistema debe adoptar un estado que no comprometa la seguridad.
    
- **Defensa en profundidad**: implementar múltiples capas de seguridad que se complementen para proteger frente a fallos en cualquiera de ellas.
    
- **Mediación completa**: verificar todos los accesos y operaciones, sin suponer que una autorización previa sigue siendo válida.
    
- **Separación de privilegios**: dividir funciones críticas para que no sean ejecutadas por una sola entidad o proceso.
    
- **Economía de mecanismos**: mantener los diseños simples y reducidos en complejidad para facilitar auditorías y minimizar errores.
    
- **Usabilidad**: un sistema seguro también debe ser fácil de usar, evitando que los usuarios intenten eludir controles de seguridad por su complejidad.
    
- **Reticencia a confiar**: nunca asumir que los actores externos o incluso internos son confiables sin una validación adecuada.
    

---

### Conceptos básicos en modelado de amenazas

- **Nodos**: elementos que representan actores, procesos, servidores, bases de datos, etc., en un sistema.
    
- **Aristas**: relaciones o flujos entre nodos:
    
    - **Arista de datos**: describe el flujo de datos.
        
    - **Arista de control**: describe el flujo de instrucciones o decisiones.
        
- **Assets / recursos**: representan los datos sensibles o componentes valiosos que deben protegerse o que podrían ser objetivo de ataque.
    
- **Fronteras de confianza**: límites dentro del sistema a partir de los cuales ya no se puede garantizar la integridad, confidencialidad o autenticidad de datos y acciones (por ejemplo, la separación entre sistemas internos y redes externas). Permiten identificar sistemas autónomos bajo nuestro control y aquellos que no.
    

> Nota: **Todos los modelos de amenazas son útiles, aunque estén incompletos o incorrectos**, porque ayudan a estructurar el pensamiento y encontrar debilidades en etapas tempranas del desarrollo.

---

### STRIDE

**STRIDE** es uno de los marcos más utilizados para clasificar amenazas en sistemas y aplicaciones. Cada letra corresponde a un tipo de amenaza:

- **S: Spoofing (Suplantación de identidad)**  
    Ocurre cuando un atacante se hace pasar por otro usuario o entidad para obtener acceso no autorizado. Está directamente relacionado con fallos en los mecanismos de autenticación.
    
- **T: Tampering (Manipulación de datos)**  
    Consiste en alterar datos, aplicaciones o configuraciones de forma maliciosa, afectando su integridad.
    
- **R: Repudiation (Repudio)**  
    Situación en la que un usuario niega haber realizado una acción, y el sistema no tiene capacidad de probar lo contrario (por ejemplo, falta de logs adecuados).
    
- **I: Information Disclosure (Divulgación de información)**  
    Acceso o revelación no autorizada de información confidencial. Impacta directamente en la confidencialidad.
    
- **D: Denial of Service (Denegación de servicio)**  
    Ataques diseñados para interrumpir la disponibilidad de un servicio o sistema, agotando sus recursos e impidiendo su uso legítimo.
    
- **E: Elevation of Privilege (Escalada de privilegios)**  
    Un atacante obtiene permisos o privilegios más elevados de los que debería tener, comprometiendo la seguridad general del sistema.



---

# Estrategias de modelado de amenazas

El **modelado de amenazas** permite identificar y analizar los riesgos de seguridad desde las fases tempranas del diseño de un sistema. Existen distintas estrategias para abordar este análisis:

### Estrategia basada en **assets o recursos**

Se centra en identificar los **recursos valiosos del sistema** (por ejemplo, datos sensibles, servidores, bases de datos) y analizar las amenazas que podrían afectarlos directamente. Esta estrategia permite focalizar los esfuerzos de protección en los elementos de mayor valor para la organización.

### Estrategia funcional

Consiste en analizar el **comportamiento funcional del sistema**: cómo interactúan sus componentes, qué funciones expone y cómo fluyen los datos entre ellos. Esta aproximación permite identificar amenazas relacionadas con procesos y funcionalidades del sistema más allá de los recursos puramente técnicos, como fallos lógicos o errores de implementación.

---

## Escenario de ejemplo

**Aplicación web bancaria**:  
Portal online que permite a los usuarios registrarse, iniciar sesión y consultar información personal y financiera.

---

## Modelado de amenazas STRIDE aplicado al escenario

### **S: Spoofing (Suplantación de identidad)**

- **Amenaza**: Un atacante intenta iniciar sesión como otro usuario sin conocer su contraseña.
    
- **Riesgo**: Acceso no autorizado a cuentas de clientes.
    
- **Contramedidas**:
    
    - Autenticación robusta: contraseñas fuertes.
        
    - Autenticación multifactor (MFA).
        
    - Protección frente a ataques de fuerza bruta (rate limiting y bloqueos temporales).
        

---

### **T: Tampering (Manipulación de la integridad)**

- **Amenaza**: Un atacante intercepta peticiones HTTP y modifica parámetros críticos, como cambiar un `userID` en la URL para acceder a datos de otro usuario.
    
- **Riesgo**: Acceso o alteración de información de otros clientes.
    
- **Contramedidas**:
    
    - Validación estricta en el lado servidor: nunca confiar en datos enviados por el cliente.
        
    - Control de acceso basado en sesión autenticada.
        
    - Uso de HTTPS para proteger datos en tránsito.
        

---

### **R: Repudiation (Repudio)**

- **Amenaza**: Un usuario niega haber realizado transacciones o acciones críticas.
    
- **Riesgo**: Falta de trazabilidad y posibilidad de fraudes o conflictos legales.
    
- **Contramedidas**:
    
    - Generación de logs seguros y completos.
        
    - Trazabilidad de operaciones sensibles.
        
    - Firmas digitales para acciones críticas.
        

---

### **I: Information Disclosure (Divulgación de información confidencial)**

- **Amenaza**: Un atacante intercepta comunicaciones para obtener datos sensibles (como números de cuenta, datos personales).
    
- **Riesgo**: Pérdida de confidencialidad y posibles fraudes.
    
- **Contramedidas**:
    
    - Cifrado de comunicaciones mediante HTTPS/TLS.
        
    - Protección de datos en reposo (bases de datos cifradas).
        
    - Políticas de mínimo privilegio para limitar el acceso interno a información sensible.
        

---

### **D: Denial of Service (Denegación de servicio)**

- **Amenaza**: Un atacante envía un alto volumen de peticiones para saturar el servidor web.
    
- **Riesgo**: Los usuarios legítimos no pueden acceder al servicio.
    
- **Contramedidas**:
    
    - Protección frente a ataques DoS/DDoS.
        
    - Implementación de límites de tasa (rate limiting).
        
    - Uso de servicios especializados en mitigación DDoS (CDN, WAF).
        

---

### **E: Elevation of Privilege (Escalada de privilegios)**

- **Amenaza**: Un usuario normal explota vulnerabilidades para obtener permisos de administrador.
    
- **Riesgo**: Compromiso total de la aplicación y acceso a datos de todos los usuarios.
    
- **Contramedidas**:
    
    - Aplicación estricta del principio de mínimo privilegio.
        
    - Revisiones de código y auditorías de seguridad.
        
    - Pruebas de seguridad regulares para detectar vulnerabilidades conocidas como inyecciones SQL o fallos en el control de acceso.
        

---

Si quieres, puedo preparar una **tabla resumen** de este análisis STRIDE o un **diagrama visual del flujo del modelado de amenazas para este escenario bancario**. Solo dime. 

---

## Cómo aplicar estrategias de modelado en este caso

Para aplicar correctamente el **modelado de amenazas** al escenario de la aplicación web bancaria, podemos adoptar dos estrategias complementarias: la **estrategia basada en assets** y la **estrategia funcional**.

---

### Estrategia basada en **assets**

Esta estrategia se centra en **identificar y proteger los activos más importantes del sistema**. Los pasos serían:

1️⃣ **Identificación de activos clave:**

- **Datos personales de los usuarios**: nombres, direcciones, datos financieros, etc.
    
- **Credenciales de acceso**: contraseñas, tokens de autenticación, claves de sesión.
    
- **Infraestructura tecnológica**: servidores web, bases de datos, redes y servicios que soportan la aplicación.
    

2️⃣ **Análisis de amenazas STRIDE sobre cada activo:**

- Para **datos personales**: Information Disclosure (ID), Tampering (T).
    
- Para **credenciales**: Spoofing (S), Information Disclosure (ID).
    
- Para la **infraestructura**: Denial of Service (DoS), Elevation of Privilege (EoP).
    

De esta forma, el análisis se orienta a garantizar la **confidencialidad, integridad y disponibilidad** de los activos más críticos.

---

### Estrategia **funcional**

Esta estrategia analiza el **comportamiento de las funciones principales del sistema**, evaluando qué amenazas pueden materializarse en cada paso funcional. El proceso sería:

1️⃣ **Identificación de funciones principales:**

- **Registro de usuarios**: proceso mediante el cual los usuarios crean sus cuentas.
    
- **Inicio de sesión**: autenticación y autorización de usuarios.
    
- **Consultas de datos personales**: acceso a información financiera e historial de operaciones.
    
- **Transferencias bancarias**: operaciones críticas que mueven fondos.
    

2️⃣ **Análisis de amenazas STRIDE por función:**

- **Registro de usuarios**: posible spoofing (S) si no hay controles sólidos de validación de identidad.
    
- **Inicio de sesión**: spoofing (S) y brute force si no hay MFA ni protección contra intentos masivos.
    
- **Consultas de datos**: tampering (T) e information disclosure (ID) si no se validan correctamente las sesiones y no se cifran las comunicaciones.
    
- **Transferencias bancarias**: tampering (T) y elevation of privilege (EoP) si existen fallos en la validación de roles y privilegios.
    

---

 **Conclusión:**  
Ambas estrategias son **complementarias**:

- La **estrategia basada en assets** prioriza la protección de los componentes más valiosos del sistema.
    
- La **estrategia funcional** garantiza la protección de los procesos críticos desde el punto de vista del flujo de trabajo y uso del sistema.
    

Aplicadas juntas, permiten un modelado de amenazas más completo, facilitando el diseño de controles que protejan tanto los datos como las funcionalidades del sistema.

---
