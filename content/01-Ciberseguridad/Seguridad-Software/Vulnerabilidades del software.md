---
title: "Vulnerabilidades del software"
---

# Vulnerabilidades del software
Fundamentos de la Seguridad en el Software y en los Componentes — Máster Universitario en Ciberseguridad. Susel Fernández Melián.
## Objetivos
- Comprender conceptos básicos relacionados con las vulnerabilidades.
- Conocer las principales vulnerabilidades del software.
- Conocer herramientas para la detección y el análisis de vulnerabilidades.
- Familiarizarse con las principales bases de datos y clasificaciones de vulnerabilidades.
## Contenidos
- Introducción al estudio de las vulnerabilidades del software
- Conceptos básicos
- Tipos de vulnerabilidades
- Ciclo de vida de una vulnerabilidad
- Factores que definen una vulnerabilidad
- Taxonomía de vulnerabilidades del software
- Herramientas para la detección y el análisis de vulnerabilidades
- Bases de datos y clasificación de vulnerabilidades
## Conceptos básicos
- Activo**: recurso necesario para desempeñar las actividades de la empresa y cuya no disponibilidad o deterioro supone un agravio o coste.
- Amenaza**: posibilidad de que un efecto adverso cause daño a nuestros activos.
- Vulnerabilidad**: debilidad en un sistema o proceso que hace posible que una amenaza tenga efecto.
- Riesgo**: relación entre la probabilidad de que se materialice una amenaza y la severidad de los daños.
- Control**: mecanismo para mitigar el riesgo que ocasiona una vulnerabilidad.
- Auditoría**: proceso de analizar el sistema para descubrir vulnerabilidades que los atacantes puedan explotar.
## Amenazas a la seguridad del software
Explotan vulnerabilidades en las aplicaciones o los servicios. ¿Qué ocurre si a un programa se le introduce un dato inesperado? El programa se comporta de forma inesperada; lo más probable es que deje de funcionar ( denegación de servicio), aunque también puede dar acceso a funcionalidades no previstas o permitir la ejecución de código.
## Tipos de vulnerabilidades software
- Fallos de diseño**: por ejemplo, Telnet.
- Fallos de implementación**: buffer overflow, cadenas de formato, condiciones de carrera, inyección SQL.
- Fallos de configuración**: por defecto se instalan servicios que no se usan y que pueden presentar debilidades.
## Ciclo de vida de una vulnerabilidad
1. **Descubrimiento**: detección de un fallo en el software.
2. **Explotación**: los atacantes desarrollan el exploit adecuado para atacar.
3. **Verificación de la vulnerabilidad**: al recibir la notificación, los desarrolladores comprueban la veracidad del error.
4. **Solución**: los desarrolladores del producto buscan solución en entornos controlados y toman medidas para mitigar las posibles pérdidas.
5. **Difusión**: se divulga el incidente a través de los medios de comunicación.
6. **Actualización**: se instalan los parches necesarios ( los sistemas no actualizados vuelven a ser víctimas).
7. **Búsqueda**: los técnicos buscan vulnerabilidades similares y el ciclo vuelve a comenzar.
## Factores que definen una vulnerabilidad
- Producto**: ¿a qué software/versiones afecta?
- Componente**: ¿en qué parte del software está el fallo?
- Descripción técnica**: causas y consecuencias — ¿cuál es el fallo concreto? ¿Qué proceso desencadena?
- Impacto o alcance**: ¿cómo de grave es? ¿Hasta dónde puede llegar un atacante?
- Vector de ataque**: técnica del atacante para aprovechar la vulnerabilidad.
## Taxonomía de vulnerabilidades del software de Fortify ( 7 reinos perniciosos + 1)
Errores de desarrollo: 1. Validación de la entrada y representación; 2. Abuso en APIs; 3. Características de seguridad; 4. Tiempo y estado; 5. Manejo de errores; 6. Calidad del código; 7. Encapsulación. Y, aparte, errores de configuración y entorno.
*Fuente: Fortify Software Security Research Group, https://vulncat.fortify.com/data/Fortify_TaxonomyofSoftwareSecurityErrors.pdf*
## 1. Vulnerabilidades relacionadas con validación de entrada y representación
- Overflow** ( buffer overflow, integer overflow...): desbordamiento de memoria.
- Format Strings**: mal uso de las funciones de tratamiento de cadenas con parámetros de formato.
- Injection**: inyección de comandos maliciosos, inyección SQL.
## # Organización de la memoria en un proceso
- Code**: instrucciones del programa a ser interpretadas y ejecutadas.
- Data**: variables globales, estáticas.
- Heap**: variables dinámicas.
- Stack**: argumentos de funciones, variables locales y puntero de instrucciones ( dirección de retorno).
## # Buffer Overflow
Consiste en sobrescribir datos en memoria: ocurre cuando se copia en un buffer un valor que ocupa más espacio del que se ha reservado. Puede afectar a los segmentos Data ( variables globales y estáticas), Heap ( variables dinámicas) y Stack ( argumentos de funciones, variables locales, puntero de instrucciones).
**Stack-based Overflow.** Imaginemos el siguiente código en C:
```c
void funcion ( char * cadena){
 char buffer[512];
 strcpy ( buffer, cadena);
}
```
En la pila se almacenan los parámetros de la función (`*cadena`), la dirección de retorno (`ret`) y el espacio para la variable `buffer`. El problema es que `strcpy` no comprueba si `cadena` cabe en `buffer`. Si `cadena` es mayor que `buffer`, se produce un overflow que sobrescribe `ret`: en el mejor caso provoca una denegación de servicio, y en el peor el programa salta a la nueva dirección de retorno, permitiendo la ejecución arbitraria de código.
## # Integer Overflow
Ocurre cuando en un programa se intenta asignar a un entero un valor que está fuera del rango de los valores representables. El rango depende de la arquitectura y el tamaño de palabra: con 8 bits el valor máximo representable es 2⁸ − 1 = 255; con 16 bits, 2¹⁶ − 1 = 65.535; con 32 bits ( x86), 2³² − 1 = 4.294.967.295; con 64 bits, 2⁶⁴ − 1 = 18.446.744.073.709.551.615.
Con 16 bits hay 2¹⁶ valores posibles ( 65.536): un `unsigned int` ( entero sin signo) va del 0 al 65.535, y un `int` ( entero con signo) va de −32.768 a 32.767.
El problema típico es que una operación como `uia + uib` puede desbordar el espacio reservado para el resultado. La solución es una precondición: verificar si puede haber desbordamiento antes de hacer la operación.
Otro caso es la conversión automática de tipos, por ejemplo al recibir un `int` cuando se espera un `unsigned int`: si se recibe un entero positivo no hay problema, pero si se recibe un número negativo se realiza una conversión automática mediante complemento a 2, que convierte el número negativo en un número positivo enorme y provoca un desbordamiento.
**Medidas de protección frente a overflow:**
- Utilizar buenas prácticas de programación: verificar los tamaños de las variables que se copian en memoria ( usando funciones que comprueben la longitud de lo copiado) y verificar la compatibilidad entre los tipos de datos y las funciones de conversión del lenguaje específico.
- Auditar y probar los programas.
- Desactivar los servicios innecesarios.
- Tener el software actualizado.
- No permitir la ejecución de la pila ( a nivel de sistema operativo).
## # Format String
Ocurre en funciones que permiten caracteres de formato de cadenas, cuando estos no se introducen adecuadamente. Funciones típicas: `printf` ( imprime en la salida estándar), `sprintf` ( imprime en una cadena), `snprintf` ( imprime en una cadena verificando la longitud) y `fprintf` ( imprime en un fichero).
Caracteres de formato: `%d` ( entero por valor), `%x` ( hexadecimal por valor), `%s` ( string por referencia, `char *`), `%n` ( almacena el número de caracteres procesados, `int *`).
En una llamada como `printf ("Título: %s %d", cadena, entero)`, la función procesa la cadena de formato carácter a carácter y, al encontrar `%`, determina el tipo de parámetro y lo extrae de la pila. El problema aparece con código como:
```c
void funcion ( char * cadena) {
 printf ( cadena);
}
```
Aquí la llamada a `printf` es vulnerable porque se toma como cadena de formato la cadena introducida por el usuario: insertando `%` adecuadamente, el usuario puede controlar la función. Esto permite, entre otros:
- Denegación de servicio: `cadena = "%s%s%s%s%s%s%s%s%s%s%s%s%s%s"`.
- Volcado de pila: `cadena = "%08x.%08x.%08x.%08x.%08x.%08x."`.
- Lectura de la memoria: `cadena = "%08x|%s"`.
- Ejecución de código sobrescribiendo la dirección de retorno en la pila: `cadena = "<direcciónret><shellcode>"`.
Para evitarlo, basta con utilizar correctamente las funciones que admiten cadenas de formato: `printf ("%s", cadena)`.
## # Inyección SQL
Consiste en ejecutar comandos SQL a través de la construcción de instrucciones SQL dinámicas en la entrada: se inserta código SQL intruso dentro del código SQL programado, con el fin de que se ejecute la porción de código incrustada sobre la base de datos. Se debe a la incorrecta comprobación o filtrado de las variables utilizadas en un programa que contiene o genera código SQL. Ocurre cuando los datos ingresan en un programa desde una fuente que no es de confianza y esos datos construyen dinámicamente una consulta SQL.
Ejemplo de código vulnerable:
```
query := "SELECT * FROM users WHERE id=" + UserID + ";"
```
Si el usuario escribe un UserID válido ( por ejemplo, 1), se genera `SELECT * FROM users WHERE id=1;`. Pero si escribe `1;DROP TABLE users`, se genera:
```sql
SELECT * FROM users WHERE id = 1;
DROP TABLE users;
```
Los ataques por inyección SQL permiten a los atacantes acceder a datos prohibidos, alterar datos existentes, causar problemas de repudio ( anular transacciones o cambiar balances), destruir los datos o volverlos inasequibles, e incluso convertirse en administradores del servidor de base de datos.
Efectos relacionados: **confidencialidad** ( las bases de datos SQL suelen almacenar información sensible, y su pérdida es un problema frecuente); **autenticación** ( consultas SQL pobres para chequear usuarios o contraseñas pueden permitir conectarse sin conocer la contraseña); **autorización** ( si la información de autorización está en una base de datos SQL, puede cambiarse mediante inyección); **integridad** ( así como se puede leer información sensible, también se puede modificar o borrar).
**Medidas de protección:**
- Limpiar de caracteres especiales las peticiones ( en PHP, la función `mysqlrealescapestring ()` evita que este tipo de caracteres interfieran en la consulta).
- Parametrización de las consultas ( sustituir valores literales por parámetros).
- Verificar siempre que los datos recibidos sean del tipo correcto ( si es un email, comprobar el formato; si es un teléfono, comprobar longitud y formato).
- Asignar mínimos privilegios al usuario que conectará con la base de datos.
- La mayoría de los entornos de programación tienen sus propias medidas de protección contra la inyección SQL.
## 2. Vulnerabilidades de abuso en APIs
Una API puede verse como un contrato entre una entidad que invoca y una entidad invocada. Las vulnerabilidades de abuso se producen cuando no se siguen las reglas establecidas en este "contrato": incluyen debilidades que implican que el software utilice una API de una manera contraria a su uso previsto. Ejemplo: las jaulas de seguridad `chroot ()` no cambian el directorio actual; si el directorio actual se encuentra fuera de la jaula, el atacante podría eludirla utilizando `chdir ()`. Se viola el contrato sobre cómo cambiar de directorio raíz de manera segura.
- Mal uso de la autenticación**: por ejemplo, usar funciones inseguras para obtener datos de autenticación (`getlogin ()` es fácil de falsificar).
- Inspección del heap**: usar `realloc ()` para cambiar el tamaño de buffers que almacenan datos confidenciales no es recomendable.
- Mal manejo de cadenas**: el mal uso de funciones que manipulan cadenas de caracteres puede dar lugar a overflow y format strings.
- Falta de control de los valores de retorno**: ignorar el valor de retorno de un método puede hacer que el programa pase por alto estados y situaciones inesperadas.
## 3. Vulnerabilidades en características de seguridad
Vulnerabilidades relacionadas con la mala utilización de características de seguridad: control de acceso, autenticación, autorización ( administración de privilegios), confidencialidad, criptografía, privacidad.
- Aleatoriedad insegura**: uso de PRNGs inseguros, vulnerables a ataques criptográficos.
- Violación del mínimo privilegio**: el nivel de privilegio elevado requerido para operaciones como `chroot ()` debe eliminarse inmediatamente después de realizarla.
- Violación de privacidad**: el mal manejo de información privada puede comprometer la privacidad del usuario, y además es ilegal.
- Falta de control de acceso**: ausencia de verificaciones de control de acceso de manera consistente.
- Mal manejo de contraseñas**: almacenarlas en texto plano, guardarlas en ficheros de configuración, dejar la contraseña vacía en el fichero de configuración, incrustarlas en el código ( hard-coded passwords), o usar criptografía débil.
## 4. Vulnerabilidades relacionadas con el tiempo y el estado
**Race Conditions**: aprovechan ventanas temporales en las que un proceso es vulnerable, generalmente en entornos con múltiples hilos o procesos concurrentes que pueden interactuar. Provocan acceso a un recurso compartido en un orden diferente al esperado.
Ejemplo: en los servlets de Java, que son multi-hilo, el programador puede asumir que en el momento en que se imprime la variable `count` esta tiene el mismo valor que en la línea previa. Si dos usuarios acceden al mismo tiempo, puede que no se imprima el valor correcto de `count`. Una mejora parcial es `p.println (++count + " hits so far!")`, aunque no evita del todo la condición de carrera. La solución habitual es usar la palabra clave `synchronized`, que evita que varios hilos ejecuten código sobre el mismo objeto, aunque tiene un serio impacto en la eficiencia; por eso conviene mantener el bloque sincronizado lo más pequeño posible, aplicándolo solo al código crítico.
**Time of Check-Time of Use ( TOC-TOU)**: múltiples procesos en una misma máquina pueden tener condiciones de carrera entre ellos cuando operan con datos que pueden compartirse ( por ejemplo, archivos). Generalmente hay una comprobación en alguna propiedad del archivo que precede a su uso:
```c
void main ( int argc, char **argv) {
 int fd;
 if ( access ( argv[1], R_OK) == 0){
 fd = open ( argv[1], O_RDONLY);
 // Procesamos el fichero
 }
 else exit ( 1);
}
```
`access ()` verifica si hay permiso para leer el fichero, pero el problema es el tiempo que tarda `open ()` en abrirlo: en ese intervalo, un atacante puede modificar el significado de esa ruta y acceder a un fichero prohibido.
**Medidas de prevención:**
- Evitar colocar ficheros temporales o de configuración en directorios compartidos con acceso de escritura (`/tmp`).
- Minimizar el acceso a ficheros y directorios.
- Identificar ficheros por descriptor y no por nombre.
- Usar herramientas del sistema operativo para prevenir borrado o enlace a ficheros por usuarios no autorizados.
## 5. Vulnerabilidades relacionadas con la manipulación de errores
Ocurren cuando el sistema revela mensajes de error demasiado detallados ( por ejemplo, códigos generados a partir de seguimientos de pila, volcados de bases de datos, memoria insuficiente, excepciones de puntero nulo, errores de tiempo de espera de la red, etc.), que pueden ofrecer pistas sobre cómo funciona un software y cómo explotarlo, o cuando no se gestionan adecuadamente los errores.
- Bloque catch vacío**: ignorar las excepciones y otras condiciones de error puede permitir que un atacante induzca un comportamiento inesperado sin ser notado.
- Bloque catch demasiado amplio**: dificulta el manejo de errores y es más probable que el bloque contenga vulnerabilidades de seguridad.
- Valor de retorno no verificado**: ignorar el valor de retorno de un método puede hacer que el programa pase por alto estados y condiciones inesperados.
Consecuencias posibles: bloqueos del sistema, desbordamientos de buffer, ataques de DoS, exposición de datos e información confidenciales ( incluidas contraseñas).
**Medidas de prevención:**
- Todos los errores deben ser manejados por el programador, sin confiar en que el sistema operativo, el servidor, la base de datos u otros paquetes subyacentes proporcionen el manejo de errores.
- Se debe capturar información relevante y detallada en un registro seguro para futuros análisis.
- Se debe presentar a los usuarios un mensaje de error genérico que no contenga información demasiado detallada ni confidencial.
## 6. Vulnerabilidades relacionadas con la calidad del código
La mala calidad del código conduce a un comportamiento impredecible: desde la perspectiva del usuario se manifiesta como mala usabilidad, y para un atacante brinda la oportunidad de estresar el sistema de maneras inesperadas.
- No liberar memoria**: cuando la memoria se asigna pero nunca se libera, provoca el agotamiento de los recursos.
- Doble free**: llamar a `free ()` dos veces en la misma dirección de memoria puede provocar una vulnerabilidad de overflow.
- Uso después de free**: hacer referencia a la memoria después de liberarla puede generar un bloqueo.
- Implementaciones inconsistentes**: inconsistencias entre funciones y versiones del sistema operativo causan problemas de portabilidad.
- Funciones obsoletas**: su uso puede indicar código descuidado y vulnerable.
- Variables sin inicializar**: provocan un funcionamiento inadecuado de las funciones y bloqueos.
## 7. Vulnerabilidades relacionadas con la encapsulación
La encapsulación se dirige a trazar fuertes límites entre las cosas y establecer barreras entre ellas. Los límites más importantes hoy en día vienen entre clases con varios métodos; la confianza y los modelos de confianza requieren una atención cuidadosa y meticulosa a esos límites ( lo público y lo privado).
- Comparar clases por nombre**: puede llevar a un programa a tratar dos clases como iguales cuando realmente difieren.
- Fugas de datos entre usuarios**: los datos pueden pasar de una sesión a otra a través de variables y objetos de un grupo compartido ( por ejemplo, servlets).
- Datos públicos asignados a un campo privado de tipo array**: asignar datos públicos a una matriz privada equivale a dar acceso público a la matriz.
- Infracción de límites de confianza**: la combinación de datos confiables y no confiables en la misma estructura de datos alienta a los programadores a confiar erróneamente en datos no validados.
## Vulnerabilidades relacionadas con los entornos de programación
Conjunto de vulnerabilidades que incluye todo lo que está fuera de nuestro código, pero sigue siendo crítico para la seguridad del software que creamos. Los diferentes entornos de programación también presentan vulnerabilidades propias, generalmente por configuración incorrecta:
- Creación de binario de depuración**: los mensajes de depuración ayudan a los atacantes a aprender sobre el sistema y planear una forma de ataque.
- Ausencia de gestión de errores personalizada**: una aplicación debe habilitar páginas de error personalizadas para evitar que los atacantes extraigan información de las respuestas integradas del framework.
- Hard-coded passwords**: no se deben incrustar contraseñas en el propio software.
- Transporte inseguro**: la configuración de la aplicación debe garantizar que se use TLS para todas las comunicaciones con acceso controlado.
- Longitud de ID de sesión insuficiente**: los identificadores de sesión deben tener al menos 128 bits de longitud para evitar ataques de fuerza bruta.
- Permisos de acceso débiles**: el permiso para invocar ciertos métodos no debe otorgarse al usuario medio.
## Resumen: medidas de prevención
- Validar los parámetros de entrada: longitud, formato.
- Usar funciones de copia que permitan controlar el número de bytes a copiar.
- Proporcionar siempre el formato de las cadenas cuando se usen funciones que lo permitan.
- Mantener el sistema operativo actualizado.
- Configurar segmentos stack/heap no ejecutables a nivel de sistema operativo.
- Instalar herramientas para prevenir stack overflow: Stack Guard, Stack Shield...
- Minimizar el acceso a ficheros y directorios; acceder a los ficheros por descriptor y no por nombre.
- Evitar colocar ficheros temporales o de configuración en directorios con acceso de escritura (`/tmp`).
- Usar herramientas del sistema operativo para prevenir borrado o enlace por usuarios no autorizados.
- Hacer un uso seguro de las APIs y verificar los valores de retorno de las funciones ( manejo de excepciones).
- Hacer un uso correcto de la encapsulación.
- Utilizar configuraciones seguras en los diferentes entornos de programación.
## Herramientas para escanear código
- RATS**: analizador de código estático para C/C++, Perl, Python, PHP ( https://security.web.cern.ch/security/recommendations/en/codetools/rats.shtml).
- Flawfinder**: herramienta opensource para escanear código C y C++, escrita en Python ( http://www.dwheeler.com/flawfinder/).
- SonarQube**: herramienta opensource para escanear código, con interfaz de usuario amigable y amplia gama de reglas personalizables ( https://www.sonarsource.com/products/sonarqube/).
- EsLint**: herramienta de análisis estático de código específica para JavaScript ( https://eslint.org/).
## Herramientas para análisis de vulnerabilidades en sistemas
- Microsoft Baseline Security Analyzer ( MBSA)**: desarrollado por Microsoft para analizar la seguridad de pequeñas redes formadas por equipos con Windows. Analiza el sistema operativo en busca de posibles fallos y vulnerabilidades, y controla la seguridad de otros servicios como el firewall, servidor SQL, IIS y las aplicaciones de Office.
- OpenVAS de Greenbone Networks**: herramienta potente para análisis de vulnerabilidades, gratuita para todos los usuarios y con la mayoría de módulos abiertos. Cuenta con más de 50.000 escáneres diferentes que se actualizan periódicamente.
- SolarWinds Network Configuration Manager**: uno de los escáneres de vulnerabilidades más completos para auditar la seguridad de redes; herramienta de pago ( y no precisamente barata).
- Retina Network Community**: versión limitada y gratuita del Network Security Scanner de AboveTrust, con análisis exhaustivos de vulnerabilidades, parches faltantes y problemas de configuración.
- OpenSCAP**: herramienta de procesado automático de configuración de seguridad. SCAP intenta cubrir las necesidades de automatización de la configuración, verificación y parcheo de vulnerabilidades de seguridad, controles técnicos relacionados con cumplimiento y mediciones de seguridad.
## Efectividad del análisis automático
A menudo es posible encontrar problemas dentro de los primeros minutos de análisis, que de otro modo no se hubieran encontrado tan rápidamente. Aunque los escáneres de seguridad analizan una buena cantidad de información, todavía requieren un nivel significativo de conocimiento experto para la toma de decisiones. Incluso para los expertos, el análisis lleva mucho tiempo: en general, este tipo de escaneo solo elimina entre 1/4 y 1/3 del tiempo que lleva realizar un análisis completo, porque aún se requiere intervención del usuario.
## Bases de datos de vulnerabilidades
- Common Vulnerabilities and Exposures ( CVE)** ( http://cve.mitre.org): cada entrada incluye identificador, breve descripción de la vulnerabilidad, referencias y fecha de creación.
- Common Weakness Enumeration ( CWE)**: estándar internacional y de libre uso cuyos principales objetivos son proporcionar un lenguaje común para describir los defectos y debilidades de seguridad de software en arquitectura, diseño y codificación; proporcionar un estándar de comparación de herramientas de auditoría de seguridad de software; y proporcionar una línea base para la identificación de vulnerabilidades, su mitigación y los esfuerzos de prevención. Incluye, entre otros, tipos como buffer overflow, formato de cadenas, problemas de validación y estructura, e inyección de código. Referencia: http://cwe.mitre.org/data/definitions/259.html.
- Common Vulnerability Scoring System ( CVSS)** ( https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator): calcula la severidad de una vulnerabilidad de manera estricta a través de fórmulas matemáticas. Proporciona un estándar para comunicar las características y el impacto de una vulnerabilidad identificada con su código CVE, permite ver las características subyacentes usadas para generar su puntuación y ayuda a priorizar las actividades de remediación o parcheo. Se compone de un vector base, un vector temporal y un vector ambiental ( cada uno con puntuación de 0 a 10) que combinados dan la puntuación CVSS total, calculada a partir de métricas de explotabilidad e impacto.
- National Vulnerability Database ( NVD)**: base de datos del gobierno estadounidense que permite la automatización de la gestión de vulnerabilidades y la medición del nivel de seguridad. Incluye listas de comprobación de configuraciones de seguridad de productos, defectos de seguridad del software relacionados, malas configuraciones, y los nombres de producto y métricas de impacto.
## Informes de vulnerabilidades
**Common Vulnerability Reporting Framework ( CVRF)**: formato XML que permite compartir información crítica sobre vulnerabilidades en un sistema abierto y legible por cualquier equipo. Fue el primer estándar para informar de vulnerabilidades de los sistemas TIC, y deriva originalmente del proyecto Incident Object Description Exchange Format ( IODEF). Su propósito es reemplazar los múltiples formatos previamente en uso no estándar de presentación de informes, acelerando el intercambio de información y el proceso.
## Clasificaciones de vulnerabilidades
**CWE / MITRE Top 25**: herramienta destinada a ayudar a los programadores y auditores de seguridad del software a prevenir las vulnerabilidades que afectan a la industria de las TIC. Es una colaboración entre el Instituto SANS, MITRE y muchos de los mejores expertos en software de EE. UU. y Europa. Contiene los mayores errores de programación que pueden causar vulnerabilidades en el software, e incluye todo tipo de vulnerabilidades en aplicaciones web y no web, condiciones que dan lugar a vulnerabilidades graves y métodos de prevención, mitigación y principios de programación seguros.
Para cada entrada de la tabla se incluye: clasificación de la debilidad según CVSS, identificador CWE, información adicional útil para priorizar acciones de mitigación, una breve discusión informal sobre la naturaleza de la debilidad y sus consecuencias, los pasos que los desarrolladores pueden tomar para mitigarla o eliminarla, otras entradas CWE relacionadas, entradas sobre ataques que pueden llevarse a cabo con éxito contra la debilidad, y enlaces con más detalles ( ejemplos de código fuente, métodos de detección, etc.).
CWE / MITRE Top 25 ( 2023) — http://cwe.mitre.org/top25/:
1. CWE-787 — Out-of-bounds Write
2. CWE-79 — Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')
3. CWE-89 — Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')
4. CWE-416 — Use After Free
5. CWE-78 — Improper Neutralization of Special Elements used in an OS Command ('OS Command Injection')
6. CWE-20 — Improper Input Validation
7. CWE-125 — Out-of-bounds Read
8. CWE-22 — Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
9. CWE-352 — Cross-Site Request Forgery ( CSRF)
10. CWE-434 — Unrestricted Upload of File with Dangerous Type
11. CWE-862 — Missing Authorization
12. CWE-476 — NULL Pointer Dereference
13. CWE-287 — Improper Authentication
14. CWE-190 — Integer Overflow or Wraparound
15. CWE-502 — Deserialization of Untrusted Data
16. CWE-77 — Improper Neutralization of Special Elements used in a Command ('Command Injection')
17. CWE-119 — Improper Restriction of Operations within the Bounds of a Memory Buffer
18. CWE-798 — Use of Hard-coded Credentials
19. CWE-918 — Server-Side Request Forgery ( SSRF)
20. CWE-306 — Missing Authentication for Critical Function
21. CWE-362 — Concurrent Execution using Shared Resource with Improper Synchronization ('Race Condition')
22. CWE-269 — Improper Privilege Management
23. CWE-94 — Improper Control of Generation of Code ('Code Injection')
24. CWE-863 — Incorrect Authorization
25. CWE-276 — Incorrect Default Permissions
**OWASP Top 10**: su objetivo es crear conciencia sobre la seguridad en aplicaciones mediante la identificación de algunos de los riesgos más críticos que enfrentan las organizaciones. Periódicamente presenta una lista concisa y enfocada sobre los diez riesgos más críticos sobre seguridad en aplicaciones web, ordenada por criticidad y predominio.
