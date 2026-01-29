---
title: "Owasp"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
​El **OWASP** (Open Web Application Security Project) es una organización sin ánimo de lucro dedicada a mejorar la seguridad del software. Uno de sus proyectos más reconocidos es el **OWASP Top 10**, una lista que identifica las diez vulnerabilidades más críticas en aplicaciones web, actualizada periódicamente para reflejar las amenazas más relevantes.​[es.wikipedia.org](https://es.wikipedia.org/wiki/Open_Web_Application_Security_Project)

> **Herramientas relacionadas**: [[Burp-suite|Burp Suite]] y [[owasp-zap|OWASP ZAP]] son las principales herramientas para detectar estas vulnerabilidades. También se puede usar [[SQLMap]] para inyección SQL automatizada.

### **OWASP Top 10: Principales Vulnerabilidades en Aplicaciones Web**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]].

La edición más reciente del OWASP Top 10, publicada en 2021, destaca las siguientes vulnerabilidades:​

1. **Pérdida de control de acceso**: Ocurre cuando las restricciones sobre lo que los usuarios pueden hacer no se implementan correctamente, permitiendo acciones no autorizadas.​
    
2. **Fallos criptográficos**: Se refiere a problemas relacionados con la protección inadecuada de datos sensibles, como el uso de algoritmos de cifrado débiles o la falta de cifrado.​
    
3. **[[SQLMap|Inyección]]**: Sucede cuando datos no confiables se envían a un intérprete como parte de un comando o consulta, lo que puede llevar a la ejecución de comandos no intencionados. Ver también [[XXE]] para inyección en XML.​
    
4. **Diseño inseguro**: Implica la falta de controles de seguridad efectivos en la fase de diseño de la aplicación, lo que puede resultar en vulnerabilidades inherentes.​
    
5. **Configuración de seguridad incorrecta**: Se produce cuando la configuración de seguridad no se implementa correctamente, dejando la aplicación vulnerable a ataques.​
    
6. **Componentes vulnerables y desactualizados**: Uso de bibliotecas, frameworks u otros módulos con vulnerabilidades conocidas que podrían ser explotadas.​
    
7. **Fallos de identificación y autenticación**: Problemas en la gestión de credenciales y sesiones que pueden permitir a atacantes suplantar a otros usuarios.​
    
8. **Fallos en la integridad del software y de los datos**: Ocurren cuando no se protegen adecuadamente las actualizaciones de software, bibliotecas críticas o datos, permitiendo manipulaciones maliciosas.​
    
9. **Fallos en el registro y monitoreo de seguridad**: La falta de registros adecuados y monitoreo puede dificultar la detección de ataques y la respuesta oportuna.​
    
10. **Falsificación de solicitudes del lado del servidor ([[SSRF]])**: Se produce cuando una aplicación web recupera un recurso remoto sin validar la URL proporcionada por el usuario, lo que puede llevar a la exposición de información interna.​[Wikipedia](https://en.wikipedia.org/wiki/OWASP)
    

### **OWASP Top 10 Controles Proactivos**

Además de identificar vulnerabilidades, OWASP proporciona una lista de controles de seguridad que los desarrolladores y arquitectos de software deben implementar para mitigar riesgos:​

1. **Verificar la seguridad de forma temprana y frecuente**: Integrar prácticas de seguridad desde las primeras etapas del desarrollo y realizar evaluaciones continuas.​
    
2. **Parametrizar consultas**: Utilizar consultas parametrizadas para prevenir ataques de inyección, especialmente en bases de datos.​
    
3. **Codificar datos**: Aplicar técnicas de codificación adecuadas para datos que se envían al navegador, evitando ataques como XSS.​
    
4. **Validar todas las entradas**: Implementar validaciones estrictas en todas las entradas de usuario para garantizar que sean seguras y esperadas.​
    
5. **Implementar controles de identidad y autenticación**: Asegurar que los mecanismos de autenticación sean robustos y que la gestión de identidades sea segura.​
    
6. **Implementar controles de acceso**: Definir y aplicar políticas claras sobre quién puede acceder a qué recursos y en qué condiciones.​
    
7. **Proteger los datos**: Garantizar que los datos sensibles estén protegidos tanto en tránsito como en reposo mediante técnicas de cifrado adecuadas.​
    
8. **Implementar registros y detección de intrusiones**: Establecer sistemas de registro y monitoreo para detectar y responder a actividades sospechosas.​
    
9. **Aprovechar frameworks y bibliotecas de seguridad**: Utilizar herramientas y bibliotecas de seguridad reconocidas para reducir errores y mejorar la eficiencia.​
    
10. **Manejo adecuado de errores y excepciones**: Gestionar errores de forma que no se revele información sensible y se mantenga la estabilidad de la aplicación.​
    
