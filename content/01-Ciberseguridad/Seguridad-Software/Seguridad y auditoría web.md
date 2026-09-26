---
title: "Seguridad y auditoría web"
---

# Seguridad Web
Fundamentos de la Seguridad en el Software y en los Componentes — Máster Universitario en Ciberseguridad. Susel Fernández Melián.
## Objetivos
- Recordar los fundamentos básicos de las aplicaciones web.
- Conocer las vulnerabilidades y los ataques más típicos en las aplicaciones web.
- Conocer medidas de protección contra los ataques a las aplicaciones web.
- Conocer metodologías y herramientas de auditoría de seguridad web.
## Aplicación web
Programa que se codifica en un lenguaje interpretable por los navegadores web, que los usuarios pueden utilizar accediendo a un servidor web a través de internet o de una intranet ( cliente web ↔ servidor web mediante HTTP ↔ servidor de base de datos).
Características:
- Navegador web como cliente ligero.
- Independencia del sistema operativo.
- Facilidad para actualización y mantenimiento sin distribuir e instalar software a miles de usuarios potenciales.
- Interacción activa entre el usuario y la información: el usuario accede a los datos de modo interactivo, gracias a que la página responde a cada una de sus acciones ( llenar y enviar formularios, etc.).
## Elementos básicos, tecnologías y protocolos web
- URI** ( Uniform Resource Identifier): identificador para todos los documentos o recursos web.
- HTML** ( Hypertext Markup Language): lenguaje simple para "marcar" documentos de texto con etiquetas que identifican la estructura semántica y la presentación visual.
- HTTP** ( Hypertext Transport Protocol): protocolo simple de aplicación para intercambiar información entre el servidor web y el cliente.
**Contenido estático**: datos presentados al usuario en función de cómo hayan sido definidos por el creador de la aplicación. Se usan lenguajes interpretados ( scripts) para añadir funcionalidades, especialmente para ofrecer una experiencia interactiva: HTML, XML, JavaScript...
**Contenido dinámico**: el servidor web crea contenido sobre la marcha, en función de las acciones de los usuarios que acceden a la aplicación: PHP, Java ( Servlets y JSP), Perl, Ruby, Python, Node.js, ASP/ASP.NET...
## # Aplicaciones web: inconvenientes
- Habitualmente ofrecen menos funcionalidades que las aplicaciones de escritorio.
- La disponibilidad depende del proveedor de la conexión a internet o del enlace entre el servidor de la aplicación y el cliente.
- Están más expuestas a ataques.
## Vulnerabilidades web más críticas
OWASP ( Open Web Application Security Project) publica el Top Ten de vulnerabilidades ( https://owasp.org/Top10/, última actualización 2021) y el Top Ten Controls ( https://www.owasp.org/index.php/OWASP_Proactive_Controls).
## # Las 10 vulnerabilidades más críticas ( OWASP Top 10 - 2021)
- A01 Broken Access Control
- A02 Cryptographic Failures
- A03 Injection
- A04 Insecure Design
- A05 Security Misconfiguration
- A06 Vulnerable and Outdated Components
- A07 Identification and Authentication Failures
- A08 Software and Data Integrity Failures
- A09 Security Logging and Monitoring Failures
- A10 Server-Side Request Forgery ( SSRF)
**A01 — Broken Access Control.** Fundamentalmente, mal manejo de los servicios de autorización: las restricciones sobre los permisos de los usuarios autenticados no se aplican correctamente ( por ejemplo, se deja activado un acceso para pruebas y se olvida desactivarlo después). Los atacantes pueden acceder de forma no autorizada a funcionalidades y/o datos, cuentas de otros usuarios, archivos sensibles, modificar datos, cambiar derechos de acceso y permisos, etc.
**A02 — Cryptographic Failures.** Muchas aplicaciones web y APIs no protegen adecuadamente datos sensibles ( información financiera, de salud, etc.). El error más común es no cifrar datos sensibles, aunque también puede deberse al uso de algoritmos criptográficos débiles, claves débiles, etc. Los datos sensibles requieren métodos de protección adicionales, como el cifrado en almacenamiento y en tránsito.
**A03 — Injection.** Ocurre cuando se permite enviar datos no confiables a un intérprete del sistema como parte de un comando o consulta. Incluye la inyección SQL ( insertar código SQL intruso para operar sobre una base de datos) y el Cross-Site Scripting ( XSS, insertar código para su ejecución en sitios web).
**A04 — Insecure Design.** Riesgos relacionados con defectos de diseño y arquitectura ( se separan de los defectos de implementación): cuando no se diseñan los controles de seguridad necesarios, o estos son inefectivos, o no se sigue una metodología SDL durante el desarrollo. Ejemplo: un sistema de recuperación de credenciales que use preguntas de control como prueba de identidad no es un método seguro, porque más de una persona puede conocer las respuestas.
**A05 — Security Misconfiguration.** Los errores de configuración pueden poner en riesgo la seguridad del sistema, y pueden suceder en varios niveles: sistema operativo, servidor web, servidor de bases de datos, servidor de ficheros, framework, aplicación. Incluye funcionalidades y/o servicios innecesarios habilitados ( por ejemplo, puertos abiertos), contraseñas por defecto, entidades externas XML ( XXE), etc.
**A06 — Vulnerable and Outdated Components.** Ocurre cuando los desarrolladores no se preocupan de actualizar los componentes o librerías con los que desarrollan la aplicación. Estos componentes se ejecutan con los mismos privilegios que la aplicación y, como todo código, pueden tener vulnerabilidades conocidas que el atacante puede explotar.
**A07 — Identification and Authentication Failures.** Los desarrolladores hacen su propio diseño de autenticación y gestión de sesión en sus aplicaciones, y pueden incurrir en malas prácticas ( por ejemplo, permitir contraseñas débiles o almacenarlas en texto plano). Los atacantes pueden comprometer usuarios/contraseñas, comprometer tokens de sesión o explotar fallas de implementación para suplantar la identidad de otros usuarios, temporal o permanentemente.
**A08 — Software and Data Integrity Failures.** Vulnerabilidades relacionadas con código o infraestructura que no protege contra violaciones de integridad, cuando una aplicación depende de complementos, bibliotecas o módulos de fuentes, repositorios y redes de entrega de contenido no confiables. Incluye la deserialización insegura, que ocurre cuando una aplicación recibe objetos serializados dañinos y usa referencias directas a objetos del sistema que pueden ser manipulados por el atacante.
**A09 — Security Logging and Monitoring Failures.** El registro y monitorización insuficientes, junto a la falta de respuesta ante incidentes, permiten a los atacantes mantener el ataque en el tiempo, pivotear a otros sistemas y manipular, extraer o destruir datos. La explotación de un registro y monitorización insuficientes es la base de casi todos los incidentes importantes: los atacantes confían en la falta de monitorización y respuesta oportuna para lograr sus objetivos sin ser detectados.
**A10 — Server-Side Request Forgery ( SSRF).** Falsificación de solicitudes del lado del servidor: ocurre cuando una aplicación web obtiene un recurso remoto sin validar la URL proporcionada por el usuario. El atacante podría editar la consulta para que la llamada se haga a una dirección diferente de la permitida, forzando al servidor a enviar una solicitud maliciosa a un destino inesperado. Puede tratarse de ataques contra el propio servidor ( proporcionando "localhost" o 127.0.0.1 para acceder a recursos inesperados) o contra otros servidores ( forzando al servidor de aplicaciones a solicitar recursos a sistemas a los que los usuarios no pueden acceder directamente).
Comparación OWASP Top 10 2017-2021: https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project
## Profundizando en algunas vulnerabilidades: autenticación, autorización, inyección
## # Autenticación
Métodos más comunes de ataque a la autenticación basada en usuario/contraseña: enumeración de nombres de usuario, adivinar contraseñas, robar contraseñas, robar cookies, acceder a las credenciales mediante ataques de inyección, explotar debilidades en el sistema de gestión de identidad ( registro de usuarios, recuperación de contraseñas, etc.).
**Enumeración de usuarios.** Objetivo: conseguir los nombres de usuario válidos en el sistema. Métodos: usar la información obtenida en el reconocimiento de la aplicación para inferir posibles nombres; observar mensajes de error en el login ( un mensaje como "Nombre de usuario no válido" o "Contraseña no válida" es menos seguro que uno genérico como "Nombre de usuario o contraseña no válidos"); aprovechar procesos mal diseñados en el servicio de recuperación de contraseñas ( SSPR, Self-Service Password Reset) que responden si el nombre de usuario no es válido; aprovechar que se permita usar el propio nombre como identificador en el registro, mostrando variantes fácilmente adivinables si ya existe; o realizar un ataque de temporización, analizando si el tiempo de respuesta difiere entre un nombre erróneo y una contraseña errónea cuando el sistema no da detalles explícitos.
Contramedidas: no dar detalles en los mensajes de error; política de bloqueo de cuentas ( registrar el número de intentos fallidos en un intervalo y bloquear la cuenta al superar un límite); uso de CAPTCHA ( Completely Automated Public Turing test to tell Computers and Humans Apart) para evitar el uso de robots, distinguiendo entre una máquina y un humano mediante operaciones fáciles para el humano pero difíciles para la máquina.
**Adivinar contraseña.** De forma manual: muy pesado, el atacante puede usar su intuición apoyándose en datos conocidos de la víctima ( deportista favorito, fecha de nacimiento, mascota, familia, lugar de nacimiento, etc.). De forma automática: se puede usar un diccionario de contraseñas típicas y variaciones ("contraseña", "contraseña2023"...), adaptando el ataque a las políticas de contraseñas conocidas ( por ejemplo, si se sabe que debe tener al menos un número, no probar contraseñas sin número). Técnicas automáticas: *depth first* ( probar todas las contraseñas para un usuario antes de pasar al siguiente, con más riesgo de activar el bloqueo de cuenta) o *breadth first* ( probar la misma contraseña sobre un grupo de usuarios, menos sensible a los bloqueos). Herramientas: Hydra ( prueba combinaciones nombre/contraseña desde un fichero diccionario contra un método como http-get), WebCracker ( similar a Hydra para Windows), Brutus ( HTTP Basic, formularios HTTP, POP3, SMTP, etc.), John the Ripper ( originalmente para Unix, disponible en quince plataformas) y Hashcat ( Linux, macOS y Windows).
Defensa: política de contraseñas fuertes; política de bloqueo ( teniendo en cuenta que aumenta la probabilidad de DoS); revisar los logs de acceso en busca de anomalías; CAPTCHA condicional, que vigila la IP de acceso y lo añade si esta cambia en cierta ventana de tiempo, previniendo ataques distribuidos; y OTP, añadiendo a la autenticación un PIN enviado por SMS o email como segundo factor.
**Robar contraseña.** Ataques de escucha y repetición: posibles si la aplicación expone credenciales en la comunicación ( como ocurre en la autenticación básica, donde las contraseñas se envían en texto plano), permitiendo capturarlas y reutilizarlas. Defensa: configurar HTTPS adecuadamente para cifrar y autenticar el mensaje mediante una sesión TLS, y usar autenticación de acceso basada en Digest para confirmar la identidad del usuario antes de servir información sensible, aplicando una función hash a la contraseña en lugar de enviarla en claro. Con Digest, la contraseña no se envía en claro sino su valor hash, por lo que el atacante debe recurrir a fuerza bruta —computacionalmente costosa— para averiguarla; usar hashes "con sal" complica aún más un ataque de diccionario.
**Cookies como mecanismo genérico de acceso a recursos.** El servidor configura qué recursos necesitan autenticación; si el cliente solicita uno de esos recursos, se le redirige al formulario de autenticación, y si las credenciales coinciden con las almacenadas, se le redirige al recurso adjuntando un ID de sesión en una cookie. Las peticiones siguientes se envían con esa cookie para no reautenticar. El objetivo del atacante es robar la cookie y usarla de forma maliciosa.
Para prevenir ataques a cookies: usar un buen generador de cookies, cifrarlas para mayor seguridad, ofrecer un botón de sign-out que las borre al salir, no guardar información sensible en claro ( y si se hace, cifrarla) y enviarlas solo por HTTPS.
**Robo de credenciales por ataques de inyección.** Si las credenciales se guardan en una base de datos SQL, se puede usar inyección SQL para obtener información de credenciales de forma no autorizada. Si se guardan en ficheros XML, se puede usar inyección XPath ( lenguaje de consultas para navegar por un documento XML) cuando la aplicación no valida adecuadamente la consulta del usuario. Prevención: validación de entradas, evitando que el usuario introduzca caracteres interpretables, y parametrización de las consultas.
**Gestión de identidad.** Comprende el registro, la recuperación de contraseña y el cambio de contraseña. Estas aplicaciones son complejas y no siempre están bien diseñadas, por lo que son susceptibles de ataques dirigidos a conseguir acceso. En aplicaciones abiertas, crear una cuenta basta para acceder al sistema, por lo que se propone el uso de CAPTCHA para evitar la creación indiscriminada de cuentas por robots. En la recuperación de contraseña, las preguntas personales ( por ejemplo, "¿nombre de tu primer profesor?") suelen ser fácilmente adivinables, y el envío de un enlace de recuperación por correo puede ser vulnerable si el atacante consigue falsificar el enlace con su propia dirección de correo, cambiando así la contraseña de la víctima.
Resumen de defensas frente a ataques a la autenticación: políticas de contraseñas fuertes, bloqueo y CAPTCHA contra el adivinado de contraseñas; HTTPS y autenticación Digest contra el robo por escucha; cifrado de la información de las cookies contra su robo; validación de datos y parametrización de consultas contra el robo de credenciales por inyección; y buenas políticas de gestión de identidad contra los ataques al sistema de gestión de identidad.
## # Autorización
Una vez autenticado, el usuario necesita acceder a servicios, operaciones o recursos, y la aplicación debe comprobar si tiene permiso para ello. Habitualmente se implementa dando al usuario autenticado un token de acceso o ID de sesión que lo identifica en la aplicación. La aplicación decide los derechos de acceso en función del token, consultando su ACL ( Access Control List): si el token está en la lista, se comprueban los recursos a los que tiene acceso; si el recurso solicitado está asociado, se da acceso, y si no lo está o el token no figura en la lista, se rechaza.
Con los tokens/ACL se evita la reautenticación continua, lo cual es cómodo para el usuario, pero los tokens pueden ser robados o adivinados y usados para obtener accesos no autorizados. Las vulnerabilidades típicas son errores en la configuración de ACL y errores de software.
**Gestión de los tokens.** El token ( ID de sesión) lo genera el servidor de forma aleatoria ( no adivinable) y temporal ( dura lo que la sesión). El servidor lo envía al cliente ( por ejemplo, mediante `set-cookie`) y el cliente lo almacena y lo envía en sus peticiones ( GET, POST...).
**Ataques a los sistemas de autorización:** fingerprinting ( reconocimiento para obtener información sobre el sistema de autorización), ataques a los tokens y violación de ACL.
**Fingerprinting.** El *crawling* consiste en programas que inspeccionan los sitios web de forma metódica y automatizada ( a menudo indexándolos); algunos rastreadores facilitan la exploración de ACLs y la identificación de tokens de acceso ocultos. El análisis de la estructura del token intenta decodificarlo ( puede ir codificado, por ejemplo en Base64, o cifrado, lo que es más complicado). El análisis diferencial hace crawling con dos cuentas de usuario distintas y compara las estructuras de datos para localizar los identificadores que cambian, algunos de los cuales pueden ser los tokens.
**Ataques a tokens.** Tres métodos: predicción, captura y repetición, y fijación de sesión.
- Predicción**: predecir y generar el token para saltarse la autenticación. Como el token se genera aleatoriamente, "adivinarlo" es difícil; se recurre a análisis estadístico sobre una colección de tokens capturados ( para conocer su grado de determinismo) o a ataques de fuerza bruta o diccionario.
- Captura y repetición**: capturar el token y repetirlo al servidor para acceder. Formas de conseguirlo: robo ( entrando en el proxy del ISP, escuchando con Wireshark), ingeniería social ( engañando a la víctima, por ejemplo con un enlace malicioso por email) o man-in-the-middle ( interceptando el tráfico entre víctima y servidor).
- Fijación de sesión**: el atacante selecciona un ID de sesión y fuerza a la víctima a usarlo, por ejemplo engañándola para que acceda a un enlace que ya contiene ese ID (`http://www.web-objetivo.com/?PHPSESSID=XXXXX`); si el servidor comprueba que ese ID no existe, lo crea y se lo asigna al usuario. Puede darse cuando la aplicación entrega un ID de sesión al acceder y este no cambia al autenticarse.
**Violación de ACLs.** Una vez conocidos los datos de autorización necesarios, las prácticas comunes para violar los permisos de acceso son el directory traversal ( path traversal) y el acceso a recursos ocultos.
- Directory Traversal**: consiste en acceder a un recurso no autorizado moviéndose por el sistema de directorios del servidor, aprovechando aplicaciones que construyen la ruta de acceso a un fichero a partir de datos ingresados por el usuario. Usa los caracteres `../` para retroceder en subdirectorios y acceder al fichero deseado, por ejemplo `PATH=../../../../../etc/shadow`. Es un ataque famoso contra una vulnerabilidad de IIS ( 2001). Para evitarlo se puede "escapar" el carácter `/` en el HTML, pero existe otra forma de saltarse el chequeo usando codificación Unicode del carácter `/` (`%c0%af`).
- Recursos ocultos**: en algunos casos se ocultan directorios sensibles en vez de protegerlos mediante ACL; un estudio cuidadoso de la aplicación puede revelar información oculta ( por ejemplo, si existe `/user/menu`, podría existir también `/admin/menu`).
**Defensas.** Buenas prácticas para evitar ataques a los tokens: usar TLS, usar el parámetro `Secure` en la cabecera `Set-Cookie` ( solo HTTPS), no incluir datos personales sensibles en el token, regenerar el token si cambian los privilegios o hay un nuevo inicio de sesión, invalidar el token tras un tiempo de inactividad y no permitir varias sesiones concurrentes del mismo usuario.
Logs de seguridad: dan información precisa sobre ataques y pueden alertar de anomalías que sean potenciales ataques. Conviene registrar cambios en parámetros del perfil de usuario ( teléfono, email...) y de contraseña, avisar por correo de eventos como el cambio de contraseña o la eliminación/adición de usuarios, y no añadir información sensible en los logs.
## # Inyección
Los ataques de inyección son de los más comunes entre los dirigidos a las aplicaciones web. La clave para prevenirlos es la validación de datos, una labor compleja.
Ataques clasificados por objetivo: control del servidor mediante buffer overflow ( introduciendo valores de variables muy largos que desbordan la memoria); almacenamiento de datos ( SQL...); usuarios de la aplicación ( XSS, phishing...); host del servidor web ( ejecutar comandos del sistema operativo); y contenido de la aplicación ( provocar mensajes de error reveladores, saltarse restricciones de acceso a ficheros, acceder a datos prohibidos).
¿Dónde realizar la inyección? En los parámetros enviados por GET o POST ( procedentes de formularios o de la propia aplicación, con valores interesantes como nombre, contraseña, teléfono, número de tarjeta); mediante crawling se pueden catalogar ficheros, parámetros y campos de formulario; también en las cookies ( por ejemplo, el token de sesión).
**Buffer overflow por inyección.** Ejemplo con `curl` ( verifica conectividad a una URL y muestra el contenido de una página). Petición legítima: `curl https://website/login.php?user=Juan`. Ataque: `curl https://website/login.php?user='perl -e print="a" x 500'`. Defensa: detectar la vulnerabilidad mediante test a la aplicación.
**Path traversal (`../`).** Se da en aplicaciones que no verifican la localización y contenido de los recursos solicitados; si el fichero no existe, el mensaje de error puede revelar el path completo. Ejemplo: una petición legítima `GET /servlet/webacc?User.html=nombredeficheroalazar` cuyo mensaje de error informa sobre el camino completo base del sitio ( por ejemplo, 7 saltos desde la raíz), permite construir un ataque como `GET /servlet/webacc?User.html=../../../../../../../boot.ini%00` para acceder a `boot.ini` en el directorio raíz. Defensa: eliminar todos los "." de los parámetros enviados con GET y POST, eliminar también el código equivalente en Unicode, usar expresiones regulares para eliminar el camino que acompaña al nombre del fichero, forzar lecturas desde un directorio específico, mantener la información sensible fuera de los directorios web, e iniciar el servidor web con un usuario de privilegios mínimos ( acceso solo al directorio de la app web).
**Inyección HTML: Cross-Site Scripting ( XSS).** Consiste en insertar código para su ejecución en el cliente web, mediante scripts incrustados. Es código malicioso que se ejecuta en el navegador, por ejemplo para robar información ( cookies), a menudo apoyándose en ingeniería social. Ejemplos típicos de inyección:
```html
<script>document.write ( document.cookie)</script>
<script>alert ('Hi, you have been hacked')</script>
<script src=http://www.malhost.bad/malscript.js></script>
```
También pueden inyectarse scripts más elaborados, como uno que simula una expiración de sesión y solicita la contraseña al usuario para enviarla a un servidor del atacante.
Tipos de XSS: **almacenado** ( el código malicioso se guarda permanentemente en el servidor, y el cliente se infecta al descargar el objeto que lo contiene) y **reflejado** ( el código llega al cliente reflejado desde el servidor vulnerable, en el cual el cliente confía, procedente de un tercer nodo malicioso; la víctima debe ser engañada para acceder a un enlace falso que inicia el proceso de reflexión). En el XSS reflejado, la víctima pica en un enlace y envía la petición al servidor vulnerable del banco, que incluye los datos de la petición en la respuesta ( por ejemplo, un mensaje de "no encontrado" que incrusta el script); la víctima confía en que el código proviene del banco, y el atacante obtiene acceso a su cuenta.
Contramedidas: en URLs y entradas de formularios, convertir `<` y `>` en su código HTML equivalente (`&lt` y `&gt`), de forma que el navegador no interprete `&ltscript&gt` como una etiqueta de script; si la aplicación permite etiquetas de formato de texto ( negrita, cursiva...), usar expresiones regulares para validar que solo se aceptan las etiquetas permitidas.
**Evitar ataques de inyección en general:** parametrización; validación de datos ( límites de valores, caracteres permitidos, listas blancas de valores); rechazar caracteres especiales sin sentido para la naturaleza del dato ( por ejemplo, en un email tiene sentido `@` pero no `(`); tipado apropiado, asignando tipos específicos en lugar de strings cuando sea posible; y control de acceso, limitando el acceso solo a los recursos necesarios.
## Auditoría web
## # Evaluación de la seguridad de las aplicaciones web ( testing web)
- Black box**: no hay conocimientos previos ( necesaria una fase de reconocimiento); evaluación totalmente externa a la red objetivo.
- Grey box**: se actúa como usuario del sistema, con cierta información conocida ( diseño, arquitectura, documentación); evaluación más específica.
- White box**: se dispone de todos los datos sobre actividad, arquitectura, sistemas y procesos, con relación directa con los desarrolladores; evaluación basada en conocimiento no accesible a los hackers.
## # Tipos de herramientas de testing web
- Crawler/spider**: descarga de forma sistemática páginas y las indexa ( bot).
- Fuzzer**: busca errores software introduciendo datos inesperados en las entradas de las aplicaciones.
- Proxy**: intercepta las comunicaciones entre cliente y servidor.
- Scanner**: busca vulnerabilidades.
## # Herramientas de testing en la red
- Escaneo de puertos: Nmap.
- Escaneo de vulnerabilidades: OpenSCAP, OpenVas, Nikto, Nessus.
- Explotación de vulnerabilidades: Metasploit.
- Otras más específicas: inyección SQL ( sqlmap), crackeo de contraseñas ( John the Ripper), ingeniería social ( SET).
**Kali Linux**: distribución basada en Debian GNU/Linux, diseñada principalmente para la auditoría y seguridad informática en general. Trae preinstalados más de 600 programas ( Nmap, Wireshark, John the Ripper, etc.) y puede usarse desde un Live-CD, live-USB o instalarse como sistema operativo principal.
Clasificación de algunas herramientas de testing web disponibles en Kali:
- Herramienta
 - Scanner
 - Fuzzer
 - Proxy
 - Crawler
| --- | --- | --- | --- | --- |
- Burpsuite
 - x
 - x
 - x
 - x
- Owasp-ZAP
 - x
 - x
 - x
 - x
- WebScarab
 -
 - x
 - x
 - x
- Vega
 -
 -
 - x
 - x
- Nikto
 - x
 -
 -
 -
- WebSploit, Paros
 -
 -
 - x
 -
## # Metodologías
Hay muchas: PTEST ( http://www.pentest-standard.org/index.php/Main_Page), SANS ( http://www.sans.org/reading-room/whitepapers/auditing/conducting-penetration-test-organization-67), OSSTMM ( http://www.pen-tests.com/open-source-security-testing-methodology-manual-osstmm.html) y OWASP ( https://owasp.org/www-project-web-security-testing-guide/).
**OWASP Testing Guide**: metodología específica de testing web, basada en la experiencia de un gran grupo de expertos en seguridad web, y muy completa.
## # Procedimiento integrado
La verificación de la seguridad debe estar presente en todas las fases del ciclo de vida de la aplicación ( define, diseña, desarrolla, despliega, mantiene), dentro del SDLC ( Secure/Software Development Life Cycle).
## # Ciclo de vida del producto web ( OWASP)
Fases a considerar en el ciclo del desarrollo seguro ( SDL) del producto web: antes del inicio, definición y diseño, desarrollo software, despliegue, operación y mantenimiento.
**Actividades antes del inicio:**
1. Verificar que la seguridad se contempla en el ciclo de vida del desarrollo del software.
2. Aplicar las políticas y estándares de seguridad apropiados.
3. Desarrollar las métricas y criterios de medida.
**Actividades en fase de definición y diseño:**
1. Revisar requisitos de seguridad de la aplicación, buscando ausencias o defectos en la especificación de procesos críticos: gestión de usuarios, autenticación, autorización, confidencialidad de datos, contabilidad, gestión de la sesión, seguridad de transporte, privacidad.
2. Revisar diseño y arquitectura.
3. Crear y revisar un modelo UML sobre la aplicación.
**Actividades durante el desarrollo:**
1. Revisión de código a alto nivel, para entender la estructura y lógica del código ( capas de la aplicación, diagramas de flujo...), conjuntamente con desarrolladores y posiblemente arquitectos del sistema.
2. Revisión del código para buscar errores de seguridad, validando una serie de aspectos ( checklist): requisitos de negocio, guías ( por ejemplo, OWASP Top 10), requisitos dependientes del lenguaje o framework, y requisitos de normativa industrial o legal.
**Actividades durante la fase de despliegue:**
1. Verificar la infraestructura, el procedimiento de despliegue y la configuración de la aplicación.
2. Aplicar un test de penetración completo, analizando todos los posibles tipos de ataques a la aplicación.
**Actividades de operación y mantenimiento:**
1. Revisión de los procedimientos de gestión y mantenimiento de la aplicación e infraestructura.
2. Revisión periódica/auditoría ( mensual, cuatrimestral) de la aplicación y la infraestructura, para conocer el nivel de seguridad actual y verificar que los nuevos riesgos son tratados.
3. Chequear los cambios introducidos en la aplicación: actualizaciones, nuevas funcionalidades.
## # Metodología de auditoría
1. Evaluar vulnerabilidades: ¿con herramientas automáticas o de forma manual? ¿Cómo se sabe qué posibles ataques verificar?
2. Calcular riesgos e impacto de los posibles ataques: ¿cómo se define un riesgo? ¿Cómo se define el impacto?
3. Realizar el informe: ¿a quién va dirigido? ¿Con qué lenguaje? ¿Qué estructura tiene?
**1. Evaluar vulnerabilidades.** Puede hacerse de forma automática ( por ejemplo con ZAP u OpenVas, más completa y efectiva) o manual ( el resultado depende de la experiencia y habilidad del auditor; la guía OWASP tiene una clasificación completa de ataques). Para cada prueba, la guía presenta un breve resumen, descripción, ejemplos de pruebas de caja negra/gris, referencias y herramientas usadas en la comprobación. Categorías de pruebas:
- Recopilación de información**: spiders, robots, crawlers; descubrimiento/reconocimiento; identificación de puntos de entrada en la aplicación; fingerprint de aplicaciones web ( por ejemplo, WhatWeb); análisis de errores de código.
- Gestión de la configuración**: SSL/TLS, bases de datos, configuración de la infraestructura y de la aplicación, gestor de extensión de ficheros, ficheros antiguos de backup o no referenciados, interfaces de administración de aplicación e infraestructura, métodos HTTP y XST.
- Autenticación**: transporte de credenciales sobre canales cifrados, enumeración de usuarios, cuentas por defecto o adivinables ( diccionario), ataques de fuerza bruta contra la contraseña, procedimientos de recordatorio y recuperación de contraseña, cierre de sesión y gestión de caché, CAPTCHA, autenticación multifactor, condición de carrera.
- Gestión de la sesión**: esquema de gestión de sesión, atributos de cookies, fijación de sesión, variables de sesión expuestas, CSRF ( Cross-Site Request Forgery).
- Autorización**: path traversal ( directory traversal), salto del esquema de autorización, escalada de privilegios.
- Lógica de negocio**: conocer la lógica del negocio en la aplicación ( artículos, precios, cesta de compra, pagos, relación entre ellos, procedimientos); pueden existir errores y formas de atacarlos en los procedimientos sobre estos datos; son ataques complicados de detectar y con fuerte impacto potencial.
- Validación de datos**: XSS reflejado, XSS almacenado, XSS basado en DOM, cross-site basado en flashing, inyección SQL, inyección LDAP, inyección ORM, inyección XML, inyección SSI, inyección XPath, pruebas IMAP/SMTP, inyección de código, comandos del sistema operativo, buffer overflow, HTTP splitting/smuggling.
- DoS**: SQL wildcard, búsqueda de cuentas de cliente, buffer overflow, localización de objetos especificada por el usuario, entradas de usuario como contador en bucle, escritura en disco de datos proporcionados por el usuario, fallos en la liberación de recursos, guardar demasiados datos en la sesión.
- Servicios web**: captura de información de WS, WSDL, estructura XML, XML a nivel de contenido, parámetros HTTP GET/pruebas de REST, SOAP, repetición.
**2. Calcular riesgos e impacto.** Las amenazas se pueden materializar en ataques; si hay vulnerabilidad, los ataques son más probables. El análisis de riesgos estima la importancia de las amenazas para el negocio en función de la probabilidad de materializarse y el impacto en el negocio; la criticidad de una vulnerabilidad depende de cada aplicación concreta y modelo de negocio ( modelo de riesgo personalizado). Riesgo = probabilidad × impacto. Pasos del análisis: identificar el riesgo; estimar la probabilidad; estimar el impacto en el negocio; determinar la severidad del riesgo; decidir en qué riesgos aplicar medidas de reducción; ajustar el modelo de nivel de riesgo.
**3. Realizar el informe.** Debe usar un lenguaje fácil de entender y adaptado a su destinatario ( personal de gestión o personal técnico). Tipos de informe: resumen ejecutivo, visión general de gestión técnica, resultados de evaluación, herramientas usadas.
- Resumen ejecutivo**: resume los resultados de las pruebas, dirigido a personal no técnico ( directivo); da una idea del nivel de riesgo general; debe usar lenguaje sencillo, sin demasiados tecnicismos, apoyado en gráficos y diagramas.
- Visión general de gestión técnica**: dirigido a administradores de la infraestructura, con más detalle técnico: alcance de las pruebas, objetivos y advertencias, calificación de riesgos usada, resumen técnico de los resultados.
- Resultados de la evaluación**: vulnerabilidades encontradas en lenguaje técnico, con estructura de número de referencia, producto afectado, descripción técnica del problema, forma de resolverlo, nivel de riesgo y valor de impacto; incluye los resultados detallados de cada test ( por ejemplo, de recopilación de información o de gestión de configuración).
- Herramientas usadas**: herramientas empleadas en las pruebas, scripts o códigos usados en cada caso, y opcionalmente la metodología utilizada.
