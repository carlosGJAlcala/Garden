---
title: "Metodos De Autorizacion Rbac"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema1principiosbasicossi
---

# RBAC – Role-Based Access Control

Uno de los **métodos de autorización** más extendidos y robustos en seguridad de la información: **Control de Acceso Basado en Roles**.

---

## ¿Qué es RBAC?


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/SAP_PI/Salesforce|Salesforce]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**RBAC** es un modelo de autorización que **asigna permisos a roles**, y luego **asigna roles a usuarios**.

> En lugar de dar permisos directamente a cada usuario, se gestionan a través de los **roles que representan funciones laborales**.

---

##  Objetivo de RBAC

Simplificar y asegurar la administración de accesos al:

- Reducir el riesgo de privilegios excesivos o erróneos
    
- Facilitar auditorías y cumplimiento normativo
    
- Adaptarse a los **principios de mínimo privilegio y separación de funciones**
    

---

##  Componentes clave de RBAC

1. **Usuarios**: personas, servicios o identidades digitales (ej. `usuario123`)
    
2. **Roles**: representan funciones del negocio (ej. `Gestor de cuentas`, `Administrador`)
    
3. **Permisos**: autorizaciones sobre recursos (ej. `leer`, `editar`, `borrar` un fichero o una base de datos)
    
4. **Sesiones** (opcional): instancia activa de acceso de un usuario bajo ciertos roles
    

---

##  Ejemplo simple

Supón una aplicación con los recursos: **Clientes**, **Facturas** y **Usuarios**.

|Rol|Permisos|
|---|---|
|`Vendedor`|Ver Clientes, Crear Facturas|
|`Finanzas`|Ver Facturas, Modificar Facturas|
|`Administrador`|Todos los permisos|

 Un usuario `Luis` que pertenece al rol `Vendedor` solo podrá trabajar con clientes y crear facturas, pero **no podrá modificar las de otros** ni gestionar usuarios.

---

##  Tipos de RBAC

|Tipo|Descripción|
|---|---|
|**Flat RBAC**|Usuarios ↔ Roles ↔ Permisos, sin jerarquía|
|**Hierarchical RBAC**|Los roles se heredan (ej. un rol `Manager` hereda los permisos de `Empleado`)|
|**Constrained RBAC**|Se aplica **separación de funciones** y restricciones específicas|
|**Dynamic RBAC**|Roles pueden cambiar en tiempo real según contexto (sesiones, atributos, etc.)|

---

##  Comparativa con otros modelos

|Modelo|¿Quién define los permisos?|Ventajas|
|---|---|---|
|**DAC**|El propietario del recurso|Flexible, pero difícil de controlar|
|**MAC**|Autoridad central y etiquetas|Muy seguro, usado en gobiernos/militar|
|**RBAC**|Basado en roles del negocio|Escalable, fácil de auditar y mantener|

---

##  Normativa relacionada

- **ISO/IEC 27001**: recomienda el uso de RBAC como buen control de acceso.
    
- **ENS (Esquema Nacional de Seguridad)**: también promueve RBAC como método organizativo eficaz.
    
- **NIST 800-162**: guía oficial del NIST sobre RBAC.
    

---

##  Beneficios de usar RBAC

- ️ **Centralización** de permisos (menos error humano)
    
-  **Trazabilidad y auditoría** clara
    
-  **Escalabilidad** en organizaciones grandes
    
-  **Cumplimiento del principio de mínimo privilegio**
    

---

##  Aplicaciones reales

- Sistemas operativos (Linux: sudoers, SELinux)
    
- Aplicaciones corporativas (SAP, Salesforce)
    
- Bases de datos (Oracle, SQL Server)
    
- Sistemas en la nube (Azure RBAC, IAM de AWS)
    

---

##  Conclusión

> **RBAC** es el método más adoptado en entornos corporativos porque **alinea la seguridad con la estructura organizativa**.  
> Al delegar los permisos en roles, se vuelve **más fácil de gestionar, auditar y escalar** sin comprometer la seguridad.

---