---
title: "2025 01 30 Modelado De Amenazas"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---


## **META: Modelado de Amenazas y Estrategias de Respuesta**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

El **modelado de amenazas** es un proceso clave en la ciberseguridad que permite **identificar, evaluar y priorizar amenazas** en un sistema o infraestructura. Se utiliza para analizar posibles vulnerabilidades y diseñar estrategias de mitigación.

---

## **Actuar ante las amenazas: Estrategias de respuesta (META)**

Cuando se identifican amenazas en un sistema, existen cuatro enfoques principales para gestionarlas:

1. **Mitigate (Mitigar)**
    
    - Reducir la **probabilidad** de que la amenaza ocurra o disminuir su **impacto** en caso de que suceda.
    - Se logra mediante la implementación de **controles de seguridad**, como:
        - Aplicar parches y actualizaciones.
        - Implementar firewalls y segmentación de red.
        - Aplicar restricciones de acceso y privilegios mínimos.
2. **Eliminate (Eliminar)**
    
    - Erradicar completamente la amenaza del sistema.
    - Puede implicar:
        - Deshabilitar servicios o protocolos inseguros.
        - Bloquear direcciones IP o dominios maliciosos.
        - Eliminar software vulnerable o sistemas heredados que no pueden ser protegidos adecuadamente.
3. **Transfer (Transferir)**
    
    - Desviar el riesgo hacia **terceros** mediante:
        - Contratación de seguros de ciberseguridad.
        - Externalización de servicios críticos a proveedores con mejores capacidades de gestión de amenazas.
        - Uso de contratos con cláusulas de seguridad para garantizar responsabilidad compartida.
4. **Accept (Aceptar)**
    
    - En algunos casos, el costo de mitigar o eliminar una amenaza puede ser **mayor que el impacto esperado**.
    - Se decide aceptar el riesgo y monitorizarlo, implementando planes de respuesta en caso de incidente.

---

## **Ejemplo de Aplicación META en un Ataque de Ransomware**

- **Mitigate**: Implementar copias de seguridad frecuentes, aplicar políticas de acceso restringido, y usar detección temprana de anomalías en el tráfico de red.
- **Eliminate**: Prohibir el uso de macros en documentos desconocidos y bloquear correos con archivos adjuntos sospechosos.
- **Transfer**: Contratar un seguro de ciberseguridad que cubra ataques de ransomware.
- **Accept**: Si el sistema afectado no contiene información crítica y se puede restaurar fácilmente, la organización puede decidir no invertir en más medidas de protección y asumir el riesgo.

En el siguiente enlace se muestra el ejemplo a un ejercicio de un árbol de amenazas [[2025-01-30-Arbol-de-ataque]]
