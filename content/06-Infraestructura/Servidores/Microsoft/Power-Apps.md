---
title: "Power Apps"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - microsoft
---



> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

**1. Qué es exactamente Power Apps**  
Power Apps es parte de la **Microsoft Power Platform**, que incluye:

- **Power BI** (análisis y visualización de datos)
    
- **Power Automate** (automatización de procesos)
    
- **Power Virtual Agents** (chatbots)
    
- **Power Pages** (antes Portals, para crear sitios web externos)
    

Dentro de ese ecosistema, Power Apps es la pieza que se encarga de **crear aplicaciones empresariales personalizadas** sin tener que desarrollar desde cero en un lenguaje de programación tradicional.

---

**2. Cómo funciona a nivel técnico**

- **Base de datos y datos conectados**: Power Apps puede trabajar con datos alojados en **Dataverse** (su base de datos nativa en la nube) o conectarse a más de 500 fuentes externas mediante **connectors** (SharePoint, SQL Server, Dynamics, SAP, APIs REST, etc.).
    
- **Diseño visual**: en las Canvas apps, el desarrollo es 100% visual (arrastrar y soltar controles), con lógica definida mediante fórmulas parecidas a Excel. En las Model-driven apps, la app se genera automáticamente a partir del modelo de datos.
    
- **Ejecución multiplataforma**: la app que creas se ejecuta directamente en el navegador o en la app oficial de Power Apps para iOS/Android. No hay que compilar versiones separadas.
    
- **Integración con Power Automate**: puedes conectar la app con flujos automáticos (ejemplo: un formulario de inspección envía datos, dispara un flujo que envía un correo y guarda un registro en SharePoint).
    
- **Seguridad y permisos**: usa la misma identidad y control de accesos de Microsoft Entra ID (antes Azure AD), por lo que se integra con los permisos de Microsoft 365.
    

---

**3. Tipos de Power Apps y sus usos típicos**

- **Canvas Apps**: control total sobre el diseño; útiles para apps con interfaces personalizadas, como formularios de inspección, inventarios, seguimiento de incidencias.
    
- **Model-driven Apps**: menos flexibles visualmente, pero ideales para aplicaciones centradas en datos estructurados, como CRM o gestión de activos.
    
- **Portals / Power Pages**: páginas web accesibles a usuarios externos que pueden consultar o introducir datos (por ejemplo, clientes enviando solicitudes o consultando estado de pedidos).
    

---

**4. Ejemplos de uso en la práctica**

- App móvil para que el equipo de campo registre visitas técnicas y sincronice datos al instante.
    
- Sistema interno para solicitudes de vacaciones, aprobaciones y control de ausencias.
    
- Herramienta de seguimiento de stock en un almacén con lectura de códigos QR.
    
- Portal para clientes donde consultan sus facturas y envían incidencias.
    

---

**5. Ventajas clave**

- **Rapidez de desarrollo** comparado con programación tradicional.
    
- **Integración nativa** con todo el ecosistema Microsoft 365.
    
- **Mantenimiento centralizado** (una única versión de la app para todos).
    
- **Seguridad empresarial** integrada con Microsoft Entra ID.
    

---

Si quieres, puedo hacerte ahora un **mapa visual de cómo Power Apps se conecta con el resto de Microsoft Power Platform y con servicios externos**, para que entiendas su arquitectura completa. Creo que ahí es donde de verdad se ve su potencia.