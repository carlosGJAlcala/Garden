---
title: "Principios básicos de la seguridad de la información"
---

# Máster Universitario en Ciberseguridad ( M179)
## Fundamentos de la Gestión de la Seguridad de la Información
**2024 – 2025**
## Tema 1: Principios Básicos de la Seguridad de la Información
## # Contenidos
1. Aclaraciones Previas: Datos, Información y Conocimiento
2. Definición e Implicaciones de la Seguridad de la Información
3. Dimensiones de la Seguridad de la Información
4. Clasificación Y Preservación de la Información
5. Seguridad Lógica: Control de Accesos
6. Diferentes aspectos de la S.I. ( Económicos, Físicos, Sociales y Humanos, Legales)
7. Auditorias de Seguridad. Análisis y Gestión del Riesgo. Controles de Seguridad.
---
## 1. ACLARACIONES PREVIAS: DATOS, INFORMACIÓN Y CONOCIMIENTO
Vamos, primeramente, a introducir y aclarar algunos conceptos. En concreto, la diferencia entre Dato, Información y Conocimiento.
## # Datos
Los datos son la mínima unidad semántica. Se corresponden con elementos primarios de información que por sí solos son irrelevantes como apoyo a la toma de decisiones.
Se pueden ver como un conjunto discreto de valores, que no dicen nada sobre el porqué de las cosas y no son orientativos para la acción ( un número telefónico o un nombre de una persona, sin un propósito, una utilidad o un contexto no sirven como base para apoyar la toma de una decisión).
Los datos pueden provenir de fuentes externas o internas a la organización, pudiendo ser de carácter objetivo o subjetivo, o de tipo cualitativo o cuantitativo, etc.
## # Información
La información se puede definir como un conjunto de datos procesados y que tienen un significado ( relevancia, propósito y contexto), y que por lo tanto son de utilidad para quién debe tomar decisiones, al disminuir su incertidumbre.
Los datos se pueden transforman en información añadiéndoles valor:
- Contextualizando: se sabe en qué contexto y para qué propósito se generaron.
- Categorizando: se conocen las unidades de medida que ayudan a interpretarlos.
- Calculando: los datos pueden haber sido procesados matemática o estadísticamente.
- Corrigiendo: se han eliminado errores e inconsistencias de los datos.
- Condensando: los datos se han podido resumir de forma más concisa ( agregación).
**Información = Datos + Contexto ( añadir valor) + Utilidad ( disminuir la incertidumbre)**
## # Conocimiento
El conocimiento es una mezcla de experiencia, valores, información y saber-hacer que sirve como marco para la incorporación de nuevas experiencias e información, y es útil para la acción.
Se origina y aplica en la mente de los conocedores.
No sólo se encuentra dentro de documentos o bases de datos, sino que también está en rutinas organizativas, procesos, prácticas, y normas.
Se deriva de la información, como esta de los datos. Para que la información se convierta en conocimiento es necesario:
- Comparar con otros elementos.
- Predecir consecuencias.
- Buscar conexiones.
- Conversar con otros portadores de conocimiento.
**Conceptos sacados de:** "Working Knowledge How Organizations Manage What They Know" Davenport, T. H., & Prusak, L. ( 1999). Harvard Business School Press.
## # El Valor de la Información en la Era de Internet
En la Era de Internet en la que nos encontramos, el principal bien a proteger, el que representa un mayor valor para los negocios, es la información. No en vano, se dice, que vivimos en la Sociedad de la Información.
Naturalmente, como ha sucedido a lo largo de toda la historia, el ser humano tiende a proteger siempre aquello que más valor tiene para él y que más aprecia.
Por otro lado, hay que partir de antemano de la idea de que no podremos proteger todo de manera absoluta, es decir, que no se puede alcanzar la seguridad absoluta. Deberemos perseguir el objetivo de reducir los "riesgos" a unos niveles aceptable y razonablemente pequeños.
Este concepto, el riesgo, depende de la probabilidad de que un incidente de seguridad ocurra y del impacto que tendrá en nuestra organización en el caso de que así sea.
Otra idea a transmitir aquí es que la seguridad debe ser entendida en un sentido amplio. No solamente es un conjunto de controles de seguridad en los programas, bases de datos y comunicaciones, sino que también incluye la seguridad física ( de las oficinas, salas de ordenadores y equipos), la organización ( cómo preparar una estructura de perfiles para responder adecuadamente a los incidentes diarios y a la estrategia a largo plazo) y la legalidad ( analizar y reducir el impacto de incumplir una legislación).
---
## 2. DEFINICIÓN E IMPLICACIONES DE LA SEGURIDAD DE LA INFORMACIÓN
Veamos otra definición más de Información:
**Información:** todo conocimiento que pueda ser comunicado, presentado o almacenado en cualquier forma.
## # La Información como Activo Estratégico
Es un activo estratégico:
- Aporta valor a la organización ( en casos extremos, es la razón de ser de la misma).
- Requiere la aplicación de medidas de protección y supervisión sobre los elementos que hacen uso de ella.
Su Ciclo de Vida lo podemos ver de la siguiente manera: Creación : Almacenamiento : Uso : Archivo : Destrucción.
## # Definiciones de Seguridad de la Información
### # ISO 27001 – Normas ISO/IEC
Organización Internacional para la Estandarización ( ISO) y la Comisión Electrotécnica Internacional ( IEC).
"Preservación de la confidencialidad, la integridad y la disponibilidad de la información, pudiendo, además, abarcar otras propiedades como la autenticidad, responsabilidad, fiabilidad o el no repudio"
### # MAGERIT V.3
Metodología de Análisis y Gestión de Riesgos de los Sistemas de Información: Ministerio de Hacienda y Administraciones Públicas, 2012
«Seguridad es la capacidad de las redes o de los sistemas de información para resistir, con un determinado nivel de confianza, los accidentes o acciones ilícitas o malintencionadas que comprometan la disponibilidad, autenticidad, integridad y confidencialidad de los datos almacenados o transmitidos y de los servicios que dichas redes y sistemas ofrecen o hacen accesibles.»
Lo toman de: "Reglamento ( CE) n 460/2004 del Parlamento Europeo y del Consejo, de 10 de marzo de 2004, por el que se crea la Agencia Europea de Seguridad de las Redes y de la Información"
### # RFC 2828 - Internet Security Glossary
Internet Architecture Board ( IAB), comité del Internet Engineering Task Force ( IETF)
Seguridad de la Información: «Medidas tomadas para proteger un sistema. El estado de un sistema que resulta del establecimiento y mantenimiento de estas medidas. El estado de un sistema cuando no hay accesos desautorizados, o cambios, destrucciones o pérdidas no autorizadas».
## # Síntesis de Seguridad de la Información
Resumiendo, podemos sintetizar que, de lo que estamos tratando es de mantener "la confidencialidad, integridad y disponibilidad ( qué protegemos) de los activos de información más valiosos ( de qué activos) mediante controles implementados en políticas, estándares y procedimientos ( de qué manera).
De todo lo anterior podemos deducir que aspectos conforman la seguridad de la información:
- Diferentes dimensiones de la Seguridad de la Información
- Clasificación de la Información.
- Aspectos Económicos de la S.I.
- Aspectos Físicos de la S.I.
- Aspectos Sociales y Humanos de la S.I.
- Aspectos Legales de la S.I.
---
## 3. DIMENSIONES DE LA SEGURIDAD DE LA INFORMACIÓN
Podemos entender la Seguridad de la Información como el conjunto de actividades encaminadas a garantizar la confidencialidad, integridad y disponibilidad, que serían los tres pilares básicos o dimensiones, de los recursos más valiosos de un sistema de información.
Sus atributos «inversos», de carácter negativo o no deseable, son la revelación, la alteración y la destrucción.
## # Confidencialidad
Es la garantía de que la información sólo es accedida por las personas o los procesos autorizados.
## # Integridad
Es la garantía de que la información sólo puede ser modificada por las personas o los proceso autorizados, de manera exacta y completa, no pudiendo perderse o deteriorarse.
## # Disponibilidad
Es la garantía de que la información es accesible en el momento y en las condiciones preestablecidas cuando se necesita.
## # Otras Dimensiones de la Seguridad
Es frecuente también encontrar referencias a otras dimensiones de la seguridad, contempladas incluso en la legislación vigente:
### # Autenticidad y no Repudio
Es la garantía de la identidad de los usuarios o procesos que tratan la información, y de la autoría de una determinada acción.
### # Trazabilidad
Es la garantía de poder reproducir un histórico o secuencia de acciones sobre un determinado proceso y determinar quién ha sido el autor de cada acción.
## # Relevancia de Cada Dimensión
Todas las dimensiones de seguridad son relevantes y deben ser tenidas en cuenta por igual, aunque dependiendo del tipo de información que se esté tratando, tendrá mayor relevancia una u otra.
- Si el objetivo es proteger la información de nóminas de una compañía, la confidencialidad e integridad serán las dimensiones más relevantes.
- Si el objetivo es proteger una página de comercio en línea, posiblemente sean más importantes la integridad y la disponibilidad.
- Si el objetivo es proteger una página a través de la cual los ciudadanos realizan trámites electrónicos con la Administración, disponibilidad, integridad y trazabilidad pasarán por delante.
- Si el objetivo es proteger un sistema de comunicación a los ciudadanos para emergencias de carácter nacional, la disponibilidad será primordial.
## # Confidencialidad y Privacidad
Una de las caras de la Confidencialidad es la Privacidad. La privacidad de la información personal es un derecho protegido por regulaciones internacionales y nacionales. Es quizá el aspecto que se menciona con más frecuencia en cuanto a la confidencialidad.
Es importante notar que confidencialidad y privacidad, aunque están muy relacionadas, no son sinónimos, ya que la privacidad se refiere únicamente a datos de carácter personal que pueden o no ser públicos, mientras que la confidencialidad se refiere a información, personal o no, que la compañía, por el motivo que fuere, quiere proteger de ser difundida abiertamente ( el código fuente de una aplicación informática desarrollada en una empresa para su venta, la lista de los mejores proveedores en un área, etc…).
## # Integridad: Principios Básicos
La integridad de la información se gestiona de acuerdo a los siguientes principios básicos:
### # Necesidad de Conocer ( Criterio Need-to-Know)
Determinación positiva por la que se confirma que un posible destinatario requiere el acceso a una determinada información para desempeñar servicios, tareas o cometidos oficiales.
### # Principio del Mínimo Privilegio
Todo usuario debe tener asignados los mínimos privilegios necesarios de manera que pueda seguir realizando su función.
### # Separación de Obligaciones ( Duties) y Rotación de Obligaciones
Para realizar una determinada tarea, no debe haber nunca un solo usuario responsable de realizarla. De esta manera, al menos habrá dos personas implicadas y será más difícil que se utilice una manipulación de datos para beneficio personal.
El problema con la rotación es que, en empresas con pocos empleados en un determinado tipo de puesto, puede ser difícil el intercambiar sus tareas.
## # Disponibilidad
En el contexto de la seguridad de la información, habitualmente se habla de la disponibilidad en dos situaciones típicas:
- Ataques de denegación de servicio ( Denial of Service, DoS).
- Pérdidas de datos o capacidades de procesamiento de datos debidas a catástrofes naturales ( terremotos, inundaciones, etc.) o a acciones humanas ( bombas, sabotajes, etc.).
## # Autenticidad y Trazabilidad
Los conceptos de Autenticación, Autorización y Trazabilidad o Rendición de Cuentas ( Accountability) ( La Triple A, en inglés) están muy imbricados ( Control de Accesos) y se verán más adelante en este capítulo y en profundidad en otras asignaturas.
---
## 4. CLASIFICACIÓN Y PRESERVACIÓN DE LA INFORMACIÓN
Es claro que no todos los datos ni toda la información tienen el mismo valor para una organización, por eso definiremos unos niveles de protección de acuerdo a una clasificación previa de nuestro activos de información. Esto nos permitirá dedicar más esfuerzos en proteger los recursos y activos más valiosos.
La práctica más extendida es hacer una clasificación por niveles que estarán basados más en prevenir la confidencialidad de la información que en preservar la integridad o la disponibilidad.
## # Definición de Clasificación
Por Clasificación se entiende el acto formal por el cual la Autoridad de Clasificación asigna a una información un grado de clasificación, en atención al riesgo que supone su revelación no autorizada para la seguridad y defensa del Estado o sus intereses, y con la finalidad de protegerla. ( CCN-STIC-822 Procedimientos de Seguridad en el ENS. Anexo II)
En ámbitos públicos y estatales se suele manejar una escala de 4 o 5 niveles, dependiendo de los países.
## # Niveles de Clasificación en Ámbitos Públicos
Un ejemplo de clasificación puede ser:
### # Secreto ( Top Secret)
Esta información podría provocar un "daño excepcionalmente grave" a la seguridad nacional si estuviera públicamente disponible.
### # Reservado ( Secret)
Su difusión eventualmente causaría "serios daños" o daños importantes a la seguridad nacional.
### # Confidencial ( Confidential)
La información que de ser difundida puede causar daño a la seguridad nacional.
### # Difusión Limitada ( Restricted)
Este material podría producir "efectos indeseados" si estuviera públicamente disponible. Este nivel no existe en los modelos de 4 niveles.
### # Sin Clasificar ( Unclassified)
Información no clasificada como sensible o clasificada. Por definición, la difusión de esta información no afecta a la confidencialidad.
## # Niveles de Clasificación en Ámbitos Empresariales
En el ámbito empresarial, esta clasificación se suele simplificar a 3 niveles.
- Confidencial: La información más sensible.
- Uso interno: Información que se puede difundir internamente pero no externamente.
- Uso público: Puede difundirse públicamente.
## # Acciones Según Nivel de Clasificación
Las acciones que pueden realizarse con la información dependen del nivel de seguridad asignado y de los roles de cada persona en la organización.
### # Propietario ( Owner)
El propietario debe ser un directivo o gestor encargado de la protección de los recursos de información. Establece las políticas de clasificación y delega las tareas rutinarias al responsable.
### # Custodios o Responsables ( Custodian)
Normalmente es personal técnico, en quien el propietario delega la custodia efectiva de la información. Esto incluye la gestión de las copias de seguridad y cualquier otra tarea técnica necesaria.
### # Elaborador ( Developer)
Son los "productores" de la información.
### # Usuario ( User)
Son los «consumidores» de la información para su trabajo diario.
Además de la Autoridad de Clasificación de la que hablamos anteriormente.
## # Ciclo de Vida de la Información
El valor de la información no suele ser una cosa estática. Puede dejar de reflejar una realidad actual para pasar a ser información histórica con una disminución de su valor. Por eso un dato que hoy es secreto, porque su divulgación ocasionaría un grave perjuicio, mañana no tiene por qué ocasionarlo.
En otras palabras, la información tiene un ciclo de vida que puede conllevar una disminución de su sensibilidad a ser divulgada. Esto debe traducirse en una reclasificación a la baja en el nivel de seguridad, realizada por la autoridad que clasificó en su día esa información.
Estas fases conllevan, implícitamente, además de las tareas de recalificación de las que hablábamos antes, tareas de conservación y, sobre todo, preservación.
## # Preservación de la Información
En este caso, el objetivo a cubrir es la integridad y la autenticidad de la información; es decir, que no sea manipulada o borrada sin control. En realidad se busca algo más: que sea auténtica ( o en otros términos, que existan garantías de que se ajusta a la realidad).
En general, la autenticidad se consigue por medio de dos medidas:
- La generación de un resumen ( o hash) de documentos.
- La firma por una autoridad "reconocida" de esos documentos.
El resumen es la aplicación de un algoritmo de cifrado sobre un fichero que da la capacidad de obtener un fichero secundario de longitud fija, llamado "hash". Se trata de un proceso matemático "en un solo sentido"; es decir, que dado un fichero, es posible generar un "hash", pero no al contrario.
La verificación de la firma se hace volviendo a aplicar el algoritmo de cifrado con otra clave, lo que genera un hash. Se puede comprobar que un fichero no ha sido modificado cuando el hash generado coincide con el él traía originalmente el fichero.
La autenticidad se consigue cuando la clave de firma ( que es privada) ha sido generada por una autoridad que certifica que su poseedor, y sólo él, posee la clave necesaria para firmar y además que le ha asociado otra clave a la primera ( esta vez pública).
## # Preservación de Información Estructurada
A la hora de preservar información estructurada, registros de información con campos asociados formando tablas, la conservación y preservación puede hacerse en estos casos mediante varios mecanismos de seguridad:
- Control de acceso:** que trataremos más adelante en esta asignatura. Baste decir ahora que un control de acceso minimiza el riesgo de manipulación no autorizada porque sólo pueden acceder a la información ciertos usuarios o aplicaciones.
- Copias de seguridad:** que aseguran que si la información original es degradada no lo será la copia. Las copias se refuerzan con las siguientes características:
 1. Si se graban en dispositivos de solo lectura.
 2. Si están físicamente alejadas de los datos originales. De esta manera, una amenaza física ( fuego, inundación, atentado terrorista, etc.) no tiene por qué afectar a la copia de seguridad.
 3. Si son completas, no parciales ni incrementales.
 4. Si se guardan varias de la misma información. Así es más difícil que se destruyan los datos originales y a la vez todas y cada una de sus réplicas.
- Grabación de las actualizaciones sobre los datos:** Lo ideal es grabar los registros justo antes y después de su actualización. Esto permitiría reconstruir exactamente el estado final de una base de datos desde una copia de seguridad y la aplicación sucesiva de sus movimientos hasta el punto de recuperación.
- Firma de los datos:** ( originales, copias de seguridad o movimientos sobre la información). Es un proceso costoso en términos de CPU, pero que puede valer la pena si los riesgos de pérdida de integridad son lo suficientemente altos. Podría darse el caso de que se tuvieran que firmar los logs de acceso a determinados ficheros restringidos para asegurar que ni siquiera un administrador pudiera alterar los registros.
## # Documentos Electrónicos y Expedientes
El mundo electrónico se parece en muchos aspectos a la información almacenada en soporte papel. Uno de ellos es que, al igual que existen documentos ( hojas con información firmada y sellada) y expedientes ( conjunto de documentos) en papel, también existen Documentos y Expedientes Electrónicos con sus correspondientes Metadatos.
### # Documentos Electrónicos
Un documento electrónico es, pues, un conjunto de datos no estructurados cuya integridad y autenticidad están protegidas con alguno de los siguientes mecanismos:
- Adición de una firma electrónica:** que es función de una clave privada vigente ( no revocada) que sólo es poseída por una autoridad. Cuando esa autoridad es una organización la firma puede equivaler a un sello electrónico y el certificado que se aplica es un certificado de sello.
- Verificación manual de un documento:** La firma electrónica anterior tiene el inconveniente de que no puede verificarse de manera manual porque es un conjunto muy largo de bits que no pueden traducirse a caracteres imprimibles y, por tanto visualizables. En estos casos hay dos mecanismos de verificación:
 1. La generación de un identificador único para cada documento de la organización, de forma que la verificación se hace accediendo a un servicio que es capaz de generar exactamente el mismo documento ( está almacenado). La verificación se hace a simple vista comparando ambos documentos.
 2. Generando un código corto e imprimible a partir de los datos variables de un documento. La verificación se hace mediante un servicio de verificación que presenta como formulario de entrada esos campos variables y generando ese código. Si coinciden ambos, el documento no ha sido manipulado.
- Una fecha y hora generada por sello de tiempo:** que genera un resumen o hash del documento con una clave privada propia y la fecha y hora obtenida de una fuente fiable de tiempo.
### # Expedientes Electrónicos
Los expedientes son conjuntos de documentos electrónicos a los que se añade un índice electrónico.
Un índice electrónico es un documento electrónico más que contiene una lista de documentos ( junto con algunos metadatos, como la fecha de incorporación al expediente). Este índice está firmado electrónicamente y garantiza la integridad del expediente de la siguiente manera:
- La firma de cada documento electrónico garantiza la integridad de ese documento.
- El índice electrónico garantiza que el expediente está formado por el número determinado de documentos que lo forman el expediente.
Cuando un expediente se actualiza, el índice no debe modificarse, sino que se añade una nueva versión del índice ( con los documentos actualizados) al expediente.
### # Metadatos
Los metadatos son campos que proporcionan información adicional sobre el contenido de los documentos y sobre los que es posible realizar búsquedas indexadas.
Algunos están asociados al expediente y otros a los documentos electrónicos.
Son ejemplos de metadatos:
- La fecha y hora de creación.
- El autor.
- La versión.
- El formato en el que está presentado.
- El procedimiento o expediente administrativo al que está asociado.
### # Custodia de Documentos
La custodia consiste el refirmado periódico de la firma electrónica de un documento garantizando su validez de la firma efectuada y, por tanto, de la integridad y autenticidad de los documentos firmados.
Las funcionalidades que ofrece un custodio documental sobre las firmas electrónicas de documentos son de:
- Almacenamiento de firmas.
- Recuperación de firmas.
- Resellado o regeneración de firmas.
- Inserción, modificación y recuperación de metadatos asociados a firmas.
- Borrado a nivel físico y lógico de firmas.
### # Política de Custodia
La política de custodia recoge el conjunto de acciones que se deben realizar sobre el firmado de documentos y se basa en tres parámetros principales:
- La retención, que indica el tiempo que se va a custodiar un documento.
- El resellado, que indica los periodos máximos en los que los documentos deben resellarse.
- El acceso, que especifica quién puede acceder a qué documentos. El acceso al servicio de custodia no da derecho al acceso universal a los documentos custodiados.
### # Arquitectura de Custodia
La custodia debe entenderse como una extensión de un servicio de almacenamiento de expedientes.
Un archivo documental guarda la información de expedientes ( documentos, índices y metadatos) y el custodio es un repositorio aparte que almacena las firmas de documentos y les aplica la política de custodia.
El custodio no almacena los documentos, sólo los datos de firma y tiempo ( sellado).
## # Tipos de Firma de Documentos
### # Firma XaDES
XAdES sigla en inglés de XML Advanced Electronic Signature ( Firma electrónica avanzada XML) es un conjunto de extensiones a las recomendaciones XML-DSig haciéndolas adecuadas para la firma electrónica avanzada.
Define varios perfiles según el nivel de protección ofrecido. Cada perfil incluye y extiende al previo:
- XAdES-BES, forma básica que simplemente cumple los requisitos legales de la directiva europea para firma electrónica avanzada.
- XAdES-EPES, forma básica a la que se la ha añadido información sobre la política de firma.
- XAdES-T ( timestamp), añade un campo de sellado de tiempo para proteger contra el repudio.
- XAdES-C ( complete), añade referencias a datos de verificación ( certificados y listas de revocación) a los documentos firmados para permitir verificación y validación offline en el futuro ( pero no almacena los datos en sí mismos).
- XAdES-X ( extended), añade sellos de tiempo para evitar que pueda verse comprometida en el futuro una cadena de certificados.
- XAdES-X-L ( extended long-term), añade los propios certificados y las respuestas OCSP o CRL, pero no las listas de revocación, para permitir la verificación en el futuro incluso si las fuentes originales ( de consulta de certificados o de las listas de revocación) no estuvieran ya disponibles.
- XAdES-A ( archivado), añade la posibilidad de timestamping periódico ( por ejemplo cada año) de documentos archivados para prevenir que puedan ser comprometidos debido a la debilidad de la firma durante un periodo largo de almacenamiento.
### # Firma PadES
El estándar PAdES perfila el soporte para firmas digitales del formato PDF 1.7 ( ISO 32000-1) con la finalidad de poder incluir firmas electrónicas avanzadas en los documentos PDF.
Además, amplía dicho soporte ya que define estructuras de datos adicionales que sirven para mantener la validez de las firmas durante períodos largos de tiempo. Está previsto que las extensiones de ISO 32000-1 que define PAdES sean recogidas por ISO 32000-2.
Concretamente define los siguientes perfiles:
- PAdES-CMS: Define una firma CMS/PKCS#7 basada en ISO 32000-1. Este es el perfil soportado por la mayor parte de la soluciones de software que generan firmas en PDF.
- PAdES-BES y PAdES-EPES: Definen una firma CAdES-BES y otra CAdES-EPES que tienen como restricciones específicas la necesidad de que la clave /ByteRange del diccionario de firma abarque la totalidad del documento.
- PAdES-LTV: Este perfil constituye una extensión de ISO 32000-1, ya que define dos estructuras que permiten prorrogar la validez de las firmas por tiempo indefinido.
- PAdES-XML: Engloba un conjunto de perfiles que describen cómo utilizar las firmas XAdES en los documentos PDF.
## # Infraestructura de Clave Pública ( PKI)
Una infraestructura de clave pública o PKI ( Public Key Infraestructure) consiste en un conjunto de programas, formatos de datos, procedimientos, políticas de seguridad y mecanismos de clave pública que trabajan de forma coordinada para permitir a un amplio rango de usuarios dispersos comunicarse de una forma segura y predecible.
La infraestructura proporciona autenticación, confidencialidad, no repudio e integridad de los mensajes intercambiados.
Aunque la infraestructura de clave pública usa algoritmos de clave pública, es un concepto más amplio que el del propio algoritmo. Una infraestructura contiene elementos que identifican los usuarios, crean y distribuyen certificados, los mantienen y los revocan. Mantienen claves de cifrado y permiten a todas las tecnologías comunicar y trabajar juntas para el propósito de tener una comunicación cifrada y con autenticación.
### # Certificado Digital
Es una credencial que relaciona los datos que identifican a su titular de manera única con una clave pública. La estructura de los certificados sigue el estándar X.509, que define los diferentes campos que lo componen.
El certificado incluye el número de serie, el número de versión, la información de identificación del titular, el algoritmo de información, las fechas de tiempo de vida, y la firma de la autoridad de certificación.
Los certificados pueden residir en un directorio, que puede almacenarse en el disco duro de un ordenador, un pen drive o en un CD, o bien en tarjeta, más seguros, pues estos dispositivos garantizan que los certificados no se pueden copiar fuera de ellos.
### # Componentes de una PKI
**Autoridad de Certificación**
La autoridad de certificación ( CA o "Certification Authority") es una organización de confianza que está encargada de crear y firmar el certificado del usuario.
La CA permite que dos personas que tienen que intercambiarse información puedan confiar la una en la otra a través de sus certificados, pues han sido concedidos con las debidas garantías en los dos casos.
**Autoridad de Registro**
La autoridad de registro ( RA o "Registration Authority") establece y comprueba la identidad de la persona a quien se concede el certificado y pasa la petición a la Autoridad de Certificación.
Inicia la petición del certificado en favor de su titular y realiza las tareas de gestión del ciclo de vida del certificado actuando como intermediario entre el titular y la Autoridad de Certificación.
**Autoridad de Validación**
La autoridad de validación ( VA o "Validation Authority") es una parte de confianza que se encarga de verificar la validez de un certificado presentado por un titular. Para ello accede a la lista de revocación de certificados, que es un repositorio donde se almacenan los certificados que han dejado de ser válidos ( por denuncia, caducidad u otros motivos).
La autoridad de validación suele usar un protocolo llamado OCSP ("Online Certificate Status Protocol") para comprobar la validez del certificado en lugar de leer directamente una CRL.
**Lista de Revocación de Certificados**
La lista de revocación de certificados ( CRL o "Certificate Revocation List") es el repositorio que almacena los certificados que por diversas causas han dejado de ser válidos.
Cuando un certificado se revoca no se borra del directorio de certificados, sino que se da de alta en esta lista. De esta manera existe un histórico del momento en que un certificado dejó de ser válido.
Esta lista está mantenida y actualizada periódicamente por la CA.
**Directorio de Certificados**
Es el lugar donde se almacena la identificación de los certificados que una CA concede, junto con los datos que identifican a su titular.
**Autoridad de Sellado de Tiempo ( TSA)**
Finalmente también es un componente necesario ya que sirve para generar sellos de tiempo o firmas electrónicas AdES-T o superiores.
### # Principales Procesos con los Certificados
**Emisión de Certificados**
Este proceso tiene como objetivo que el titular obtenga un certificado. Para ello, la RA actúa ante la CA en su nombre.
Los pasos son los siguientes:
1. El titular hace una petición a la RA.
2. La RA le solicita cierta información de identificación.
3. Una vez la RA recibe esa información, la reenvía a la CA.
4. La CA crea el certificado. Hay un paso de creación de un par de claves pública y privada que son complementarias una de la otra. Esta creación debe hacerse en el equipo del titular o bien en la CA.
5. La CA firma el certificado recién creado. De esa forma enlaza la identidad individual de su titular con la clave pública, y además se responsabiliza de la identidad de la persona.
6. La clave privada queda en poder del titular. Si su propósito es la firma de documentos o la identificación, el proceso anterior debe hacerse con garantías de que sólo el titular puede poseerla.
**Revocación de Certificados**
La revocación de los certificados es su desactivación cuando el titular o la CA detectan una situación de riesgo ( por robo o sospecha de que alguien sin legitimación está haciendo uso de él) o bien cuando cumple su periodo de caducidad y no se renueva.
El proceso consiste básicamente en que:
1. El titular presenta una petición de revocación ante la RA y ésta la tramita a la CA.
2. La CA añade el identificador de certificado a la CRL sin borrarlo del repositorio de certificados.
3. La CA lo notifica a la RA.
**Propósito de los Certificados**
Los certificados pueden tener diferentes usos. Esta cualidad se llama "propósito" y debe quedar especificada por la CA.
Son propósitos habituales:
- La firma digital de los documentos. El titular puede firmar con su clave privada los documentos que genera o que avala con su aprobación.
- La identificación de su titular, que puede ser una persona física, un servidor o un organismo.
- El cifrado de documentos. Usando algoritmos de cifrado asimétricos.
Aunque técnicamente sea posible usar un certificado para un propósito para el que inicialmente fue creado, no se debe usar fuera de su intención inicial, pues las medidas de protección están pensadas para los propósitos para los que fueron creados y la CA avala el certificado creado con los propósitos iniciales determinados.
---
## 5. SEGURIDAD LÓGICA: CONTROL DE ACCESOS
( Por desarrollar en tema posterior)
---
## 6. DIFERENTES ASPECTOS DE LA S.I.
( Económicos, Físicos, Sociales y Humanos, Legales)
( Por desarrollar en tema posterior)
---
## 7. AUDITORIAS DE SEGURIDAD. ANÁLISIS Y GESTIÓN DEL RIESGO. CONTROLES DE SEGURIDAD
( Por desarrollar en tema posterior)
