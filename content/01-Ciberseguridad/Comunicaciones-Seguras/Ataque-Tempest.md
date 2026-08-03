---
title: "Ataque Tempest"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

![](https://www.securityartwork.es/wp-content/uploads/2010/03/tempest.jpg)Hace algunos días mientras un amigo y compañero de trabajo revisaba el estándar ISO27002, se dio cuenta y comentó un detalle que cuanto menos nos pareció a todos curioso. El apartado “i” del control 9.2.1 sobre Emplazamiento y protección de equipos, dice:

“Se deberían proteger los equipos que procesen la información sensible para minimizar el riesgo de fugas de información debidas a una emanación”

Como habréis pensado el comentario vino a raíz de esa última palabra: “emanación”, la cual nos hizo pensar en si realmente la habían utilizado de forma correcta bajo el contexto en el que estábamos hablando. Dándole vueltas alguien recordó que había leído algo sobre la posibilidad de la captación de datos mediante el análisis de señales por emanación electromagnética, un fenómeno que desde luego parece más bien sacado de una serie de ciencia ficción, pero que no está para nada desencaminado de la realidad. Hoy vamos a hablar de los ataques TEMPEST.

Existen varias conjeturas alrededor de dicho término (TEMPEST); se dice que su nombre en clave procede de una operación militar que comenzó por la década de los años 50 en EEUU, en plena Guerra Fría, y que tenía como objetivo el estudio y utilización de las emisiones electromagnéticas no intencionadas de equipos electrónicos para la obtención de información, así como el desarrollo de normativas para su protección ante la posibilidad del uso indiscriminado de este tipo de ataques. Aunque el gobierno de EEUU ha indicado que este término no es un acrónimo y que no tiene un significado en particular, se le han buscado diferentes significados, uno de los más conocidos es *Transient ElectroMagnetic Pulse Emanation Standard*. Otro término, quizá más correcto para hablar de esta amenaza, es la de *Emission Security* (EMSEC).

Cualquier dispositivo electrónico emite continuamente radiaciones, a través del aire o de conductores, como son los propios cables mediante los cuales están conectados. La corriente que circula por un conductor genera un campo electromagnético alrededor de éste, que es capaz de inducir esta misma señal a otros conductores que estén situados cerca en ese mismo campo. De esta forma, y con los equipos apropiados, se puede captar y reproducir de forma remota las transmisiones que se están produciendo, como por ejemplo las imágenes que se están mostrando en un monitor o un proyector, los documentos que se envían a una impresora o las pulsaciones en un teclado, y que atenta directamente contra la confidencialidad de la información. [Aquí tienen un pequeño ejemplo](http://www.youtube.com/watch?v=B05wPomCjEY).

De ciencia ficción, ¿verdad? Desde luego se trata de una amenaza que en el marco de un análisis de riesgos muchas organizaciones considerarían como despreciable por su baja probabilidad, pero como todo, es una cuestión de tiempo y recursos. Otras empresas y organismos, como las dedicadas a defensa o investigación sí lo tienen muy en cuenta; y por poner un ejemplo, sin irnos muy lejos mirando en el BOE podemos encontrar:

**BOE-B-2008-85006**

Anuncio del Órgano de Contratación del Instituto Nacional de Técnica Aeroespacial «Esteban Terradas» por la que se hace pública la adjudicación del expediente 2007/2705 titulado «**Instrumentación de medidas tempest**».

**BOE-B-2007-184004**

Resolución del Órgano de Contratación de la Dirección de Abastecimiento y Transportes de la Armada por la que se anuncia la adjudicación del expediente 393/07. **Adquisición veinte (20) kits tempest 2007**.

**BOE-B-2006-312004**

Resolución del Órgano de Contratación de la Dirección de Abastecimiento y Transportes de la Armada por la que se anuncia la adjudicación del expediente 1360/06. **Suministro de equipamiento tempest para la red Sacomar**.

Como habéis observado existen equipos con certificación Tempest, es decir, equipos especialmente diseñados para que su emisión electromagnética sea baja, pero que son extremadamente caros. Por poner un ejemplo, en [esta página](http://www.advprograms.com/products.htm) podéis ver algunos de estos productos, que existen y que como tal tienen demanda. Como podéis observar hay de todo, desde portátiles y equipos de sobremesa, teléfonos VoIP, impresoras o hasta sistemas de videoconferencia.

La autoridad de certificación Tempest en España recae bajo el [CCN (Centro Criptológico Nacional)](https://www.ccn.cni.es/index.php?option=com_content&view=article&id=21&Itemid=25), que cae en el ámbito del Ministerio de Defensa y como tal es el responsable del desarrollo de la normativa para la protección de los equipos/sistemas y las instalaciones donde se procesa información clasificada. Estas normas están basadas, o se desarrollan, siendo compatibles con la normativa que marca la OTAN.

No obstante existen otras medidas de prevención ante ataques Tempest. A continuación explicamos brevemente algunas de ellas:

+   **Jaulas de Faraday y Laberintos de Radiofrecuencia**: Se trata de proteger, no solo a unos equipos concretos, sino a una sala o edificio completo, creando zonas electromagnéticamente aisladas haciendo imposible captar las emisiones que se producen en su interior.
+   **Técnicas de zoning**: La más barata y utilizada, basada en situar los dispositivos más sensibles en las zonas más seguras. Por ejemplo, para lanzar un ataque Tempest el atacante debe situarse junto a su equipo lo más cerca posible de la fuente emisora de la señal que desea capturar (20~30 metros), a más distancia la señal se atenúa hasta perderse, por lo tanto intentaremos situar los equipos a proteger en zonas donde nos aseguremos que ninguna persona sin autorización pueda acercarse a ellos y captarlos.
+   **Ruido electromagnético**: Mientras más señales existan, más difícil le será al atacante filtrar aquello que está buscando. Existen aparatos diseñados exclusivamente para crear ruido electromagnético, otra posibilidad es la de situar otros dispositivos emisores cerca del equipo a proteger, y aunque no imposibilita la recepción de la señal sí dificulta la obtención de la información enormemente.

Finalmente y para concluir, quería hacer una pequeña reflexión: ¿hasta qué punto podemos llegar a asegurar la protección y confidencialidad de nuestros datos? ¿estamos a salvo de estos ataques o es una amenaza real para empresas y gobiernos? Cierto es que el coste de este tipo de ataques, tanto por precio como por su complejidad, es muy elevada y al alcance de la mano de muy pocos. Aunque la pequeña y mediana empresa como comentaba anteriormente, en un análisis de riesgos ni siquiera llegaría a contemplarla, no deja de estar expuesta y ser vulnerable. Otro asunto más acentuado es el de las grandes multinacionales y gobiernos, donde el valor del conocimiento de la información en algunos casos no tiene precio, y existiendo la tecnología y teniendo recursos ¿creen que no lo van a intentar? No hay que dejar de lado el hecho de que las empresas que venden dispositivos con certificación Tempest existen y tienen unas altas ganancias, por lo que, aunque parezca un caso extremo de espionaje o ciencia ficción, la amenaza existe.

Si quieren más información, les recomiendo [esta página](http://www.eskimo.com/~joelm/tempest.html). Por lo demás, si están en Valencia, que pasen unas buenas fiestas, y si no es así, manténganse a la escucha.