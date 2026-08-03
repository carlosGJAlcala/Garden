---
title: "Html Linting"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

# HTML Linting

> **Relacionado**: [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

 ¿Qué es el linting?

Linting es el proceso de analizar código fuente automáticamente para detectar errores, problemas de estilo, convenciones no cumplidas o constructos potencialmente peligrosos.

HTML linting aplica este concepto específicamente al lenguaje HTML, revisando que el código:

Sea correcto sintácticamente.

Cumpla estándares de buenas prácticas.

Esté bien estructurado y sea semántico.



 Es muy útil antes de desplegar un sitio web para asegurarse de que el HTML sea robusto y de calidad.


---

 ¿Para qué sirve en pentesting?

En contexto ofensivo:

El linting puede revelar errores que indiquen malas prácticas o configuraciones defectuosas:

Formularios mal construidos.

Falta de atributos secure en formularios o inputs.

Elementos que pueden provocar problemas de accesibilidad (que a veces también son vectores de ataque).

Fragmentos incompletos o comments que podrían revelar información sensible.



 En combinación con análisis manual puede ayudar a detectar:

End-points ocultos (<!-- TODO: admin panel here -->).

Trazas de comentarios inseguros (<!-- debug=true -->).

HTML incorrecto que provoque comportamientos inesperados en navegadores.



---

 Herramientas de HTML linting

 Herramientas más usadas:

htmllint (CLI):

npm install -g htmllint
htmllint index.html

W3C Validator (online):

Servicio oficial de validación de HTML según los estándares W3C:  https://validator.w3.org/


HTMLHint (online y CLI):

npm install -g htmlhint
htmlhint index.html


 HTMLHint permite personalizar reglas de linting con un archivo .htmlhintrc.


---

 Qué tipos de problemas detecta

Etiquetas HTML mal cerradas.

Elementos HTML anidados incorrectamente.

Duplicidad de atributos id.

Falta de atributos obligatorios (alt en imágenes, por ejemplo).

Deprecated tags (uso de etiquetas obsoletas como <font>).

Espacios innecesarios y problemas de formato.



---

 Ventajas de usar HTML linting

 Desde perspectiva del desarrollo:

Código más limpio, semántico y fácil de mantener.

Mejor accesibilidad y compatibilidad entre navegadores.

Reducción de errores que pueden generar problemas de seguridad.


 Desde perspectiva del pentester:

Ayuda a identificar indicadores de configuraciones débiles.

Facilita el descubrimiento de comentarios ocultos o metadatos expuestos.



---

 Limitaciones

️ El linting no detecta vulnerabilidades de seguridad directamente (como XSS o CSRF), pero puede indicar malas prácticas que aumentan el riesgo.

Por ejemplo:

Formularios sin autocomplete="off" → posible exposición de datos sensibles.

Falta de type="password" en campos que deberían ocultar información.



---

 Resumen rápido para recordar:

>  HTML Linting = proceso de revisar el HTML en busca de errores de sintaxis, estructura o estilo, útil para detectar malas prácticas antes del despliegue y como apoyo en reconocimiento durante un pentest.




---