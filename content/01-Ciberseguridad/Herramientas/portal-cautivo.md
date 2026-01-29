---
title: "Portal Cautivo"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Portal Cautivo: Control de Acceso en Redes**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/LDAP|LDAP]]. [[01-Ciberseguridad/Herramientas/PFSENSE|PFSENSE]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

Un **portal cautivo** es un sistema que **monitorea el tráfico HTTP y restringe el acceso a Internet** hasta que el usuario pase por una página de autenticación o acepte términos de uso. Es común en redes públicas como aeropuertos, hoteles y empresas.

---

## **1. ¿Cómo Funciona un Portal Cautivo?**

1. **El usuario se conecta a la red Wi-Fi o cableada.**
2. **El portal cautivo intercepta la primera solicitud HTTP** y redirige al usuario a una página de inicio de sesión o aceptación de términos.
3. **El usuario se autentica o acepta los términos.**
4. **Si la autenticación es exitosa, el portal cautivo permite el acceso a Internet.**

Este sistema funciona como un **proxy de acceso** que controla quién puede navegar en la red.

---

## **2. Características Principales**

- **Control de acceso:** Restringe el uso de la red hasta que se cumplan ciertas condiciones.
- **Autenticación de usuarios:** Puede usar contraseñas, integración con Active Directory o redes sociales.
- **Registro de actividad:** Puede almacenar logs de acceso según políticas de seguridad.
- **Filtrado de contenido:** Puede bloquear ciertos sitios o categorías.
- **Tiempo de sesión:** Puede limitar el tiempo de conexión por usuario.

---

## **3. Casos de Uso del Portal Cautivo**

- **Wi-Fi en hoteles y aeropuertos:** Redirige a una página donde el usuario debe ingresar su número de habitación o comprar acceso.
- **Redes corporativas:** Permite a empleados autenticarse antes de acceder a Internet.
- **Escuelas y universidades:** Controla el acceso de estudiantes a ciertos recursos.

---

## **4. Portal Cautivo en pfSense**

pfSense incorpora un **portal cautivo** que permite:

- Redirigir a los usuarios a una página de autenticación.
- Usar bases de datos locales o externas para validar credenciales.
- Integrarse con RADIUS o LDAP para autenticación centralizada.
- Limitar ancho de banda y tiempo de sesión por usuario.

---

## **5. Seguridad y Consideraciones**

- **Debe implementarse con HTTPS** para evitar ataques MITM.
- **Puede ser vulnerable a bypass** si el usuario cambia DNS o usa VPNs.
- **Debe integrarse con logs y SIEM** para auditoría en redes empresariales.

---

## **6. Conclusión**

El portal cautivo es una solución efectiva para **controlar y monitorear el acceso a redes públicas y privadas**. Se usa en entornos donde se necesita autenticación previa antes de navegar, asegurando cumplimiento de políticas de seguridad y gestión de ancho de banda.