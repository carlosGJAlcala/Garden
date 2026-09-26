# Diseño conceptual. Modelo E/R
[1.1 Introducción 2](#introducción)
[1.2 Elementos estáticos 2](#elementos-estáticos)
[1.2.1 Entidades 2](#entidades)
[1.2.2 Dominios y Valores 3](#dominios-y-valores)
[1.2.3 Atributos 4](#atributos)
[1.2.4 Interrelaciones 5](#interrelaciones)
[1.3 Control de redundancias 8](#control-de-redundancias)
[1.4 Dimensión temporal 9](#dimensión-temporal)
[1.5 Notaciones 10](#notaciones)
[1.6 Ejercicio Resuelto 11](#ejercicio-resuelto)
[1.7 Ejercicios propuestos. 15](#ejercicios-propuestos)
[1.7.1 Cursos de formación 15](#cursos-de-formación)
[1.7.2 Campeonato de Ajedrez 15](#campeonato-de-ajedrez)
[1.7.3 Energía eléctrica 16](#energía-eléctrica)
[1.7.4 Conflictos bélicos 17](#conflictos-bélicos)
[1.7.5 Gestión de nóminas 18](#gestión-de-nóminas)
## Introducción
El modelo entidad-relación es el modelo conceptual más utilizado para el diseño conceptual de bases de datos. Fue introducido por Peter Chen en 1976. El modelo Entidad-Relación está formado por un conjunto de conceptos que permiten describir la realidad mediante un conjunto de representaciones gráficas y lingüísticas.
Originalmente, el modelo entidad-relación sólo incluía tres clases de objetos: entidades, interrelaciones y atributos. Más tarde, se añadieron al modelo básico un conjunto de constructores que ayudaron a recoger una mayor semántica del universo de discurso ( los atributos compuestos, cardinalidades máximas y mínimas, las jerarquías de generalización, dependencia en existencia y en identificación, etc.) y este nuevo modelo es lo que se ha denominado modelo E/R extendido.
El Modelo E/R ha tenido una gran difusión en la comunidad informática dedicada a las BD, prueba de ello es que ha sido el modelo más extendido en las herramientas CASE de ayuda al diseño de BD.
## Elementos estáticos
En el Modelo E/R, tal como fue propuesto por Chen, se distinguen los siguientes elementos para la componente estática: Entidad, Interrelación, Dominio y Atributo.
## # Entidades
Las entidades son los objetos principales sobre los que debe recogerse información y generalmente denotan personas, lugares, cosas o eventos de interés. Las entidades aparecerán reflejadas en el enunciado habitualmente como nombres. A cada una de las posibles ocurrencias ( cada persona, lugar, cosa o evento concreto) de la entidad se denomina **ejemplar**.
Las entidades se representan gráficamente mediante rectángulos y su nombre aparece en el interior. Un nombre de entidad sólo puede aparecer una vez en el esquema conceptual.
Existen dos categorías de entidades:
- Regulares** o **fuertes**, que son aquellas que existen por sí mismas y que la existencia de un ejemplar en la entidad no depende de la existencia de otros ejemplares en otra entidad. La representación gráfica dentro del diagrama es mediante un rectángulo.
- Débiles**, que son aquellas entidades en las que se hace necesaria la existencia de ejemplares de otras entidades distintas para que puedan existir ejemplares en esta entidad. La representación gráfica dentro del diagrama es mediante dos rectángulos, uno dentro de otro.
Un ejemplo de entidad débil sería EJEMPLAR, ya que la existencia de un ejemplar depende de la existencia del LIBRO, y por tanto, la desaparición de un determinado libro de la base de datos hace que desaparezcan todos los ejemplares de dicho libro. Su representación como entidades sería la siguiente:
LIBRO
EJEMPLAR
Uno de los problemas que existirán en el diseño E/R es la decisión de si un determinado objeto o concepto se modela como un tipo de entidad o no. Por ejemplo, el color es habitualmente una propiedad de una entidad ( como es el caso del color de un coche), pero en una fábrica de pinturas probablemente sería apropiado modelar el color como una entidad con sus propias propiedades.
Por esta razón, algunos autores han intentado precisar el concepto de entidad. Así, TARDIEU ( 1979) propone tres reglas generales que debe cumplir una entidad:
- tiene que tener existencia propia
- cada ejemplar de un tipo de entidad debe poder distinguirse de las demás
- todos los ejemplares de un tipo de entidad deben tener las mismas propiedades
Como se puede observar por la propia definición, las entidades débiles nunca cumplirán la primera regla.
## # Dominios y Valores
Las distintas propiedades o características de un tipo de entidad o de interrelación toman **valores** para cada ejemplar de éstas.
Un **dominio** se define como un conjunto de valores homogéneos con un nombre que lo identifica. Una cierta característica o propiedad de un objeto toma valores que pertenecen a un determinado dominio.
Un dominio lleva siempre asociado un predicado que permite comprobar si un determinado valor pertenece al dominio:
D = { vi : p ( vi) }
donde D es el dominio, vi es un valor y p es el predicado asociado a dicho dominio.
Un dominio puede definirse por **intensión**, especificando el tipo de datos ( por ejemplo, carácter 30 para el Nombre); o por **extensión**, enumerando los valores que pertenecen al dominio ( por ejemplo, los días de la semana).
## # Atributos
Los atributos se utilizan para detallar las entidades asignándoles propiedades descriptivas tales como nombre, color y peso. Los atributos son cada una de las propiedades o características que tiene un tipo de entidad o un tipo de interrelación.
Los atributos toman valores de uno o varios dominios ( si es compuesto). El atributo le da una determinada interpretación al dominio ( o dominios) en el contexto de un tipo de entidad o de un tipo de interrelación. A diferencia de los dominios que existen por sí mismos, la existencia de un atributo está ligada a la del correspondiente tipo ( de entidad o de interrelación).
Existen dos tipos de atributos: *identificadores* y *descriptores*. Los primeros se utilizan para distinguir de manera única cada una de las ocurrencias de una entidad ( distinguiéndose entre *identificadores principales* e *identificadores alternativos*), mientras que los descriptores de utilizan para describir una ocurrencia de entidad. No sólo es posible especificar atributos en las entidades sino también en las interrelaciones ( en este caso sólo tiene sentido hablar de atributos descriptotes y no de identificadores).
- <u>Identificadores</u>**
Entre todos los atributos de un tipo de entidad han de existir uno o varios conjuntos de atributos ( simples y/o compuestos) que identifiquen unívocamente cada una de los ejemplares de ese tipo de entidad.
Cada uno de estos conjuntos de atributos se denomina **Identificador Candidato** ( IC). Todo IC debe cumplir la condición de ser unívoco y mínimo: cuando un IC es compuesto, el número de los atributos que lo componen debe ser mínimo, en el sentido de que la eliminación de cualquiera de ellos le haría perder su carácter de identificador.
Entre los IC se elige uno como **Identificador Principal** ( IP) y el resto serán **Identificadores** **Alternativos** ( IA).
- Atributos Multivaluados vs Univaluados**
Los atributos **Multivaluados** son aquellos que pueden tomar más de un valor a la vez ( una persona puede tener más de un teléfono). Los atributos **Univaluados**: toman un solo valor.
- Atributos Opcionales vs Obligatorios:**
Opcionales: Por otro lado, puede obligarse a un atributo de un tipo de entidad a que tome, como mínimo, un valor del ( o de los) dominio ( s) subyacente ( s) para cada ejemplar de entidad, es decir, el valor de ese atributo es obligatorio ( no puede ser nulo) para todo ejemplar de la entidad.
## # Interrelaciones
Se entiende por interrelación una asociación, vinculación o correspondencia entre entidades. Distinguiremos entre el tipo de interrelación o estructura genérica que describe un conjunto de interrelaciones, y cada interrelación, es decir, cada uno de los **ejemplares** concretos.
Matemáticamente, el conjunto de interrelaciones de un tipo de interrelación I se define como: { \<e<sub>1</sub>, e<sub>2</sub>, ..., e<sub>n</sub> \> } donde *e*<sub>i</sub> es un ejemplar del tipo de entidad *Ei* y *n* el **grado** del tipo de interrelación, es decir, el número de tipos de entidades participantes ( que están asociados en el tipo de interrelación).
Un ejemplo de interrelación sería: IMPARTE es un tipo de interrelación que vincula los tipos de entidad PROFESOR y CURSO; un ejemplar del tipo de interrelación IMPARTE es la vinculación entre el profesor “Gutiérrez” y el curso “Sistemas Gestores de Bases de Datos”.
### # Elementos de un tipo de interrelación
En una interrelación podemos encontrar lo siguientes elementos:
- Nombre**: identificador único en el esquema.
![]( 1cuatri/Electronica/Lab/Practica4/_media/Practica_P4_Sistemas_adquisición_datos/media/image1.jpeg)
**Figura 1.1.** Tipos de correspondencia
- Tipo de correspondencia**: número máximo de ejemplares de una entidad asociados a una combinación de ejemplares de las otras entidades en la interrelación que puede ser 1 ó N.
- Grado**: número entidades participantes en la interrelación. Normalmente las interrelaciones son binarias, es decir, en la relación participan dos entidades. Aunque lo más habitual es que en la interrelación participen dos entidades distintas, puede ocurrir que una entidad se relacione consigo misma, este tipo de relaciones las denominamos *reflexivas*. Una interrelación en la que participan tres entidades se denominará ternaria.
> ![]( 2cuatri/Seguridad en sistemas distribuidos/OSINT/Kike/_media/KiKeQuintano/media/image2.jpeg)
>
> **Figura 1.2.** Diferentes casos de tipos de interrelaciones
Un constructor que amplía la semántica recogida en una interrelación es la **restricción de cardinalidad**. Se definen las cardinalidades mínimas y máximas de las entidades que participan en una interrelación como el número máximo y mínimo de ejemplares de una entidad que puede relacionarse con un único ejemplar de la otra, u otras entidades que participan en la interrelación.
Los tipos de interrelación se clasifican también en **regulares** y **débiles**, según estén asociando dos tipos de entidad regulares, o un tipo de entidad débil con un tipo de entidad ( regular o débil), respectivamente. Dentro del tipo de interrelación débil, se distinguen dos tipos especiales:
- Dependencia en existencia**: los ejemplares de un tipo de entidad ( débil) no pueden existir si desaparece el ejemplar del tipo de entidad regular del cual depende.
- Dependencia en identificación**: además de cumplirse la condición anterior, los ejemplares del tipo de entidad débil se identifican mediante atributos propios más el identificador principal del tipo de entidad regular del cual depende. Una dependencia en identificación es siempre una dependencia en existencia.
![]( 2cuatri/AIC/Laboratorio/L0.0Guia de Inicia RVfpgaRISC-V/_media/SesionL0.0_RVfpga_GuiadeInicio_AICC_PREGUNTAS_v1/media/image3.jpeg)
**Figura 1.3.** Representación de dependencia en existencia e identificación
### # 
### # Generalizaciones
La **Generalización** se considera como un caso especial de interrelación entre uno o varios tipos de entidad ( subtipos) y un tipo más general ( supertipo), cuyas características son comunes a todos los subtipos.
La interrelación que se establece entre los subtipos y el supertipo es de la forma *es un*. Es decir, un ejemplar de un subtipo ES_UN ejemplar ( también) del supertipo.
Las cardinalidades mínimas y máximas siempre son ( 1,1) en el supertipo, y ( 0,1) en los subtipos.
El mecanismo de abstracción contrario se llama **especificación**.
![]( 2cuatri/AIC/Laboratorio/L0.0Guia de Inicia RVfpgaRISC-V/_media/SesionL0.0_RVfpga_GuiadeInicio_AICC_PREGUNTAS_v1/media/image4.jpeg)
**Figura 1.4.** Representación de generalizaciones
Una característica muy importante de esta clase de interrelaciones es la herencia:
- Toda propiedad ( atributo, identificadores, o participación en tipos de interrelación) del supertipo pasa a ser un atributo de los subtipos.
- Las propiedades comunes a todos los subtipos se asignan al supertipo, mientras que las propiedades específicas se asocian al subtipo al cual pertenecen.
La división en subtipos ( especialización) puede venir determinada por una condición predefinida ( por ejemplo, en función de los valores de un atributo llamado discriminante).
La Generalización/Especialización tiene dos restricciones semánticas asociadas:
- Totalidad**: todo ejemplar del supertipo tiene que pertenecer obligatoriamente a alguno de los subtipos. El caso contrario se llama **Parcialidad**, es decir, cuando existe algún ejemplar en el supertipo que no pertenece a ninguno de los subtipos.
- Solapamiento**: un mismo ejemplar del supertipo puede pertenecer a más de un subtipo. El caso contrario se llama **Exclusividad**.
## Control de redundancias
Los esquemas E/R, y en general en los de cualquier modelo de datos es necesario evitar las redundancias para no tener problemas de inconsistencias de la representación.
Un elemento de un esquema es redundante si puede ser eliminado sin pérdida de semántica.
Existen dos formas principales de redundancia:
- En los atributos ( atributos derivados o calculados): aunque son redundantes, no dan lugar a inconsistencias siempre que en el esquema se indique su condición de **derivados** y la fórmula mediante la que han de ser calculados.
- En las interrelaciones ( también llamadas interrelaciones derivadas): una interrelación es redundante si su eliminación no implica pérdida de semántica porque existe la posibilidad de realizar la misma asociación de ejemplares por medio de otras interrelaciones.
Para ello es condición necesaria pero no suficiente que forme parte de un ciclo. Hay que estudiar detenidamente los ciclos en el diagrama E/R. La existencia de un ciclo no implica la existencia de interrelaciones redundantes. Para que una interrelación pueda ser eliminada por redundante se tiene que cumplir:
1. que exista un ciclo
2. que las interrelaciones que componen el ciclo sean equivalentes semánticamente
3. que después de eliminar la interrelación se puedan seguir asociando los ejemplares de las dos entidades que estaban interrelacionadas
4. que la interrelación no tenga atributos o que éstos puedan ser transferidos a otro elemento del esquema a fin de no perder su semántica.
> ![]( 1cuatri/Electronica/Lab/Practica1/_media/práctica1/media/image5.jpeg)
**Figura 1.5** Ciclo con tipo de interrelación redundante
> ![]( 4anyo/TFG/_media/TFG_SUCIO/media/image6.jpeg)
**Figura 1.6** Ciclo de interrelaciones sin redundancia
## Dimensión temporal
Es necesario establecer un método semántico y gráfico que recoja de algún modo, en el esquema conceptual, el transcurso del tiempo y su influencia en la forma en que cambian los datos.
Existen varias aproximaciones, la más simple la constituyen los atributos de **tipo fecha** asociados a algunas entidades o interrelaciones. Para sucesos instantáneos, es decir, sin duración, bastará con un sólo atributo de este tipo. Para poder almacenar hechos que transcurren en un intervalo de tiempo determinado necesitaremos una *fecha_inicio* y una *fecha_fin*. En las bases de datos históricas, en las que una interrelación entre dos ejemplares concretos se pueda repetir en el tiempo, el atributo fecha será multivaluado.
Cuando es necesario representar la evolución de un tipo de entidad a lo largo del tiempo se utiliza un **atributo de estado**, que indicará en qué estado concreto se encuentra la entidad. En muchos casos lleva asociado otro atributo, que es la fecha en la que se ha producido el cambio de estado o el intervalo de tiempo en que ha permanecido en dicho estado.
![]( 4anyo/SegundoCuatri/PyC/Lab_pyc_alvaro/Lab/Practica 2/_media/Memoria PL2/media/image7.jpeg)
**Figura 1.7** Base de datos con solo el estado actual de la información
![]( 1cuatri/Electronica/Lab/Practica1/_media/práctica1/media/image8.jpeg)
**Figura 1.8** Base de datos con información histórica y posibilidad de varios préstamos del mismo ejemplar al mismo usuario
## Notaciones
A continuación se muestra las convenciones que se van a seguir, en los problemas a resolver, para la representación gráfica de los distintos constructores del diagrama E/R.
<table>
<colgroup>
<col style="width: 43%" />
<col style="width: 56%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Representación</strong></td>
<td><blockquote>
<strong>Tipo de Atributo</strong>
</blockquote></td>
</tr>
<tr class="even">
<td>![]( 1cuatri/Electronica/Lab/Practica1/_media/práctica1/media/image9.jpeg)
![]( 2cuatri/Seguridad en sistemas distribuidos/OSINT/Kike/_media/KiKeQuintano/media/image10.jpeg)</td>
<td><blockquote>
Identificador principal
Identificador Alternativo
Atributo obligatorio
Atributo opcional
Atributo multivaluado
Atributo compuesto
</blockquote></td>
</tr>
<tr class="odd">
<td>Interrelación</td>
<td><blockquote>
Interrelación
</blockquote></td>
</tr>
<tr class="even">
<td>![]( 4anyo/SegundoCuatri/PyC/Lab_pyc_alvaro/Lab/Practica 2/_media/Memoria PL2/media/image11.jpeg)</td>
<td>Jerarquía solapada y parcial</td>
</tr>
<tr class="odd">
<td>![]( 4anyo/SegundoCuatri/PyC/Lab_pyc_alvaro/Lab/Practica 2/_media/Memoria PL2/media/image12.jpeg)</td>
<td><blockquote>
Jerarquía solapada y total
</blockquote></td>
</tr>
<tr class="even">
<td>![]( 1cuatri/Electronica/Lab/Practica2/_media/PL2_JordyIvánSanMartínPonce_CarlosGarridoJunco/media/image13.jpeg)</td>
<td><blockquote>
Jerarquía exclusiva y parcial
</blockquote></td>
</tr>
<tr class="odd">
<td>![]( 4anyo/TFG/_media/TFG_Plantilla/media/image14.jpeg)</td>
<td>Jerarquía exclusiva y total</td>
</tr>
</tbody>
</table>
## Ejercicio Resuelto
Supongamos el siguiente universo de discurso sobre municipios, viviendas y personas. Cada persona puede habitar una vivienda y estar empadronado en un único municipio, pero puede ser propietaria de varias viviendas. Nos interesa también conocer las personas que dependen del cabeza de familia ( C.F.). Se indicarán los supuestos semánticos que se consideren oportunos para justificar todas las decisiones de diseño.
**Discusión del enunciado**
**1<sup>er</sup> Paso**: Elaborar la lista de conceptos candidatos a ser entidades e interrelaciones e indicar también los conceptos que no se sabe cómo catalogar. La lista obtenida es:
> <u>Entidades Interrelaciones</u>
>
> MUNICIPIO **Habita** entre PERSONA y VIVIENDA
>
> VIVIENDA **Empadrona** entre PERSONA y MUNICIPIO
>
> PERSONA **Propiedad** entre PERSONA y VIVIENDA
**2º Paso:** Construir una matriz de entidades y entidades para representar todas las interrelaciones junto con su tipo de correspondencia. Para ello iremos analizando los supuestos semánticas explícitamente representados en el enunciado, así como los que están implícitos o son de sentido común.
1) Supuestos no dados en el enunciado.
- Una vivienda puede ser habitada por muchas personas.
- Una vivienda puede ser propiedad de muchas personas.
- Una persona sólo puede tener un cabeza de familia y un cabeza de familia puede serlo de varias personas.
- Un municipio puede tener muchas viviendas y una vivienda pertenece a un solo municipio.
<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 19%" />
<col style="width: 31%" />
<col style="width: 27%" />
</colgroup>
<tbody>
<tr class="odd">
<td></td>
<td>PERSONA</td>
<td>MUNICIPIO</td>
<td>VIVIENDA</td>
</tr>
<tr class="even">
<td>PERSONA</td>
<td>C.F. ( 1:N)</td>
<td>Empadronado ( 1:N)</td>
<td>Habita ( 1:N)
Propiedad ( N:M)</td>
</tr>
<tr class="odd">
<td>MUNICIPIO</td>
<td>X</td>
<td>--</td>
<td>Está _n ( N:1)</td>
</tr>
<tr class="even">
<td>VIVIENDA</td>
<td>X</td>
<td>X</td>
<td>--</td>
</tr>
</tbody>
</table>
**3<sup>er</sup> Paso:** Obtener una versión preliminar del esquema entidad relación. A continuación se muestra una primera versión del esquema E/R correspondiente a los supuestos del enunciado.
VIVIENDA
MUNICIPIO
está_en
N:1
PERSONA
habita
propiedad
C.F.
1:N
1:N
N:M
empadronado
N:1
**4º Paso:** Análisis de cardinalidades mínimas.
- Una persona tiene obligatoriamente como mínimo una persona que es cabeza de familia y una persona que es cabeza de familia puede no tener ninguna persona a su cargo.
- Una persona habita por lo menos en una vivienda y una vivienda puede que no esté habitada.
- Una vivienda tiene por lo menos una persona que sea propietaria y una persona puede que no sea propietaria de ninguna vivienda.
- Una persona esta empadronada por lo menos en un municipio y en un municipio tiene que haber por lo menos una persona empadronada.
- Una vivienda esta en un único municipio y en un municipio por lo menos hay una vivienda.
VIVIENDA
MUNICIPIO
está_en
N:1
( 1,1)
( 1,n)
PERSONA
habita
propiedad
( 0,n)
( 1,1)
( 0,n)
( 0,n)
C.F.
( 0,n)
( 1,1)
1:N
1:N
N:M
empadronado
N:1
( 1,1)
( 1,n)
**5º Paso**: Análisis de redundancias. Como existen dos ciclos en el esquema E/R hay que estudiar si existe alguna interrelación redundante, es decir, si hay alguna interrelación cuya semántica se puede obtener a partir de otras interrelaciones.
El primer ciclo lo forman las interrelaciones **Propiedad**, **Esta_en** y **Empadronada**. La primera condición para saber si tenemos un ciclo en el que haya alguna interrelación susceptible de ser redundante es que las tres interrelaciones estén semánticamente relacionadas. En este caso la interrelación Propiedad no es semánticamente equivalente a Esta_en y Empadronada, puesto que el poseer o no una vivienda no influye en si la persona reside en el municipio en el que se encuentra la vivienda.
El segundo ciclo lo constituyen las interrelaciones **Habita**, **Esta_en** y **Empadronado**. En este caso las tres relaciones están semánticamente relacionadas ( suponemos que las personas habitan en los municipios en los que están empadronadas).
Interrelación **Habita**: Si intentamos eliminar la interrelación Habita debe ser posible obtener su semántica a partir de las otras dos relaciones del ciclo. Así, si queremos obtener las personas que habitan en una determinada vivienda, a partir de la relación Esta_en se obtiene el municipio en el que se encuentra la vivienda y con la interrelación Empadrona se obtienen las personas que habitan en un municipio, pero no sabemos las personas que habitan en la vivienda sino las que habitan en todas las viviendas del municipio. Por ello, la interrelación Habita no se puede eliminar.
Interrelación **Esta_en**: Si intentamos eliminar la interrelación Esta_en debe ser posible obtener su semántica a partir de las otras dos relaciones del ciclo. Para conocer las viviendas que se encuentran en un determinado municipio, a partir de Empadrona obtenemos todas las personas empadronadas en ese municipio y mediante la interrelación Habita obtenemos las viviendas en las que habitan esas personas ( pues una persona debe habitar obligatoriamente una vivienda); de esta forma, sabemos las viviendas de ese municipio. En el otro sentido de la interrelación Esta_En, para conocer en qué municipio está una determinada vivienda, a partir de Habita obtenemos las personas que habitan en ella; sin embargo puede ocurrir que en una determinada vivienda no habite nadie ( cardinalidad mínima 0), por lo que no podemos alcanzar la interrelación empadrona entre persona y municipio. Así, la interrelación Está_en no es redundante.
Interrelación **Empadrona**: Si intentamos eliminar la interrelación Empadrona debe ser posible obtener su semántica a partir de las otras dos relaciones del ciclo. Para conocer el municipio en que está empadronada una persona, mediante Habita obtenemos la vivienda en la que habita esa persona y con la interrelación Está_en obtenemos el municipio en que se encuentra la vivienda; por ello conocemos el municipio en el que está empadronada la persona. En el otro sentido de la interrelación Empadrona, debe ser posible conocer las personas empadronadas en un determinado municipio; mediante la interrelación Está_en conocemos las viviendas de ese municipio y a partir de Habita sabemos todas las personas que viven en esas viviendas, conociendo así todas las personas empadronadas en el municipio. Consecuentemente, la interrelación Empadrona se puede eliminar del esquema E/R sin perder semántica.
VIVIENDA
MUNICIPIO
está_en
N:1
( 1,1)
( 1,n)
PERSONA
habita
propiedad
( 0,n)
( 1,1)
( 0,n)
( 0,n)
C.F.
( 0,n)
( 1,1)
1:N
1:N
N:M
## Ejercicios propuestos
## # Cursos de formación
El departamento de formación de una empresa desea construir una base de datos para planificar y gestionar la formación de sus empleados.
La empresa organiza cursos internos de formación de los que se desea conocer el código del curso, el nombre, una descripción, el número de horas de duración y el coste del curso.
Un curso puede tener como prerrequisito haber realizado otro ( s) cursos previamente, y, a su vez la realización de un curso puede ser prerrequisito de otros. Un curso que es un prerrequisito de otro puede serlo de forma obligatoria o sólo recomendable.
Un mismo curso tiene diferentes ediciones, es decir, se imparte en diferentes lugares, fechas y con diferentes horarios ( intensivo, de mañana y de tarde). En una misma fecha de inicio sólo puede impartirse una edición de un curso.
Los cursos se imparten por personal de la propia empresa.
De los empleados se desea almacenar un código de empleado, nombre y apellidos, dirección, teléfono, NIF ( número de identificación fiscal), fecha de nacimiento, nacionalidad, sexo, firma y salario, así como si está o no capacitado para impartir cursos.
Un mismo empleado puede ser docente en una edición de un curso y alumno en otra edición, pero nunca puede ser ambas cosas a la vez ( en una misma edición de curso o lo imparte o lo recibe).
## # Campeonato de Ajedrez
El club de ajedrez de Villatortas de Arriba, ha sido encargado por la Federación Internacional de Ajedrez de la organización de los próximos campeonatos mundiales que se celebrarán en la mencionada localidad. Por este motivo, desea llevar a una base de datos toda la gestión relativa a participantes, alojamientos y partidas teniendo en cuenta que:
En el campeonato participan jugadores y árbitros; de ambos se requiere conocer el número de asociado, nombre, dirección, teléfono de contacto y campeonatos en los que han participado ( como jugador o como árbitro). De los jugadores de precisa además el nivel de juego en una escala de 1 a 10.
Ningún árbitro puede participar como jugador.
Los países envían al campeonato un conjunto de jugadores y árbitros, aunque no todos los países envían participantes. Todo jugador y árbitro es enviado por un único país. Un país puede ser representado por otro país.
Cada país se identifica por un número correlativo según su orden alfabético e interesa conocer además su nombre, el número de clubes de ajedrez existentes en el mismo.
Cada partida se identifica por un número correlativo ( Cod_P), la juegan dos jugadores y la arbitra un árbitro. Interesa registrar las partidas que juega cada jugador y el color ( blancas o negras) con las que juega. Ha de tener en cuenta que un árbitro no puede arbitrar a jugadores enviados por el mismo país que le ha enviado a él.
Todo participante participa en al menos una partida.
Tanto jugadores como árbitros se alojan en uno de los hoteles en los que se desarrollan las partidas, se desea conocer en qué hotel y en qué fechas se ha alojado cada uno de los participantes. Los participantes pueden no permanecer en Villatortas durante todo el campeonato, sino acudir cuando tiene que jugar alguna partida alojándose en el mismo o distinto hotel. De cada hotel, se desea conocer el nombre, la dirección y el número de teléfono.
El campeonato se desarrolla a lo largo de una serie de jornadas ( año, mes, día) y cada partida tiene lugar en una de las jornadas aunque no tengan lugar partidas todas las jornadas.
Cada partida se celebra en una de las salas de las que pueden disponer los hoteles, se desea conocer el número de entradas vendidas en la sala para cada partida. De cada sala, se desea conocer la capacidad y medios de que dispone ( radio, televisión, video ...) para facilitar la retransmisión de los encuentros. Una sala puede disponer de varios medios distintos.
De cada partida se pretende registrar todos los movimientos que la componen, la identificación de movimiento se establece en base a un número de orden dentro de cada partida: Para cada movimiento se guardan la jugada ( 5 posiciones) y un breve comentario realizado por un experto.
## # 
## # Energía eléctrica
Se pretende llevar a cabo un control sobre la energía eléctrica que se produce y consume en un determinado país. Se parte de las siguientes hipótesis.
Existen productores básicos de electricidad que se identifican por un nombre, de los cuales nos interesa su producción media, producción máxima y fecha de entrada en funcionamiento. Estos productos básicos lo son de una de las siguientes categorías: Hidroeléctrica, Solar, Nuclear o Térmica. De una central hidroeléctrica o presa nos interesa saber su ocupación, capacidad máxima y número de turbinas. De una central solar nos interesa saber la superficie total de paneles solares, la media anual de horas de sol y tipo ( fotovoltaica o termodinámica). De una central nuclear, nos interesa saber el número de reactores que posee, el volumen de plutonio consumido y el de residuos nucleares que produce. De una central térmica, nos interesa saber el número de hornos que posee, el volumen de carbón consumido y el volumen de emisión de gases.
Por motivos de seguridad nacional interesa controlar el plutonio de que se provee una central nuclear, este control se refiere a la cantidad de plutonio que compra a cada uno de sus posibles suministradores, ( nombre y país), y que porta un determinado transportista ( nombre y matrícula), ha de tenerse en cuenta que el mismo suministrador puede vender plutonio a distintas centrales nucleares y que cada porte, ( un único porte por compra), puede realizarlo un transportista diferente.
Cada día, los productores entregan la energía producida a una o varias estaciones primarias, las cuales pueden recibir diariamente una cantidad distinta de energía de cada uno de los productores. Los productores entregan siempre el total de su producción. Las estaciones primarias se identifican por su nombre y tienen un número de trasformadores de baja a alta tensión y son cabecera de una o varias redes de distribución.
Una red de distribución se identificará por su número de red y sólo pede tener una estación primaria como cabecera. La propiedad de una red puede ser compartida por varias compañías eléctricas, a cada compañía eléctrica se le identifica por su nombre.
La energía sobrante en una de las redes puede enviarse a otra red. Se registrará el volumen total de energía intercambiada entre dos redes.
Una red está compuesta por una serie de líneas, cada línea se identifica por un número secuencial dentro del número de la red y tiene una determinada longitud. La menor de las líneas posibles abastecerá al menos a dos subestaciones.
Una subestación es abastecida sólo por una línea y distribuye a una o varias zonas de servicio, a tales efectos, las provincias ( código y nombre), se encuentran divididas en tales zonas de servicio, aunque no se puede hablar de zonas de servicio que pertenezcan a más de una provincia. Cada zona de servicio puede ser atendida por más de una subestación.
En cada zona de servicio se desea registrar el consumo medio y el número de consumidores finales de cada una de las siguientes categorías: particulares, empresas e instituciones.
## # Conflictos bélicos
Una organización internacional pretende realizar un seguimiento de los conflictos bélicos que se producen en todo el mundo. Para ello creará una base de datos que responderá al siguiente análisis:
Se entiende por conflicto cualquier lucha armada que afecte a uno o varios países y en el cual se produzcan muertos y/o heridos. Todo conflicto se identificará por un nombre que habitualmente hará referencia a la zona o causa que provoca el conflicto, aunque dado que este nombre puede cambiar con el paso del tiempo, dentro de la BD cada conflicto se identificará por un código numérico sin significado alguno. Para cada conflicto se desea recoger los países a que afecta, así como el número de muertos y heridos contabilizados hasta el momento.
Los conflictos pueden ser de distintos tipos según la causa que lo ha originado, clasificándose, a lo sumo, en cuatro grupos: territoriales, religiosos, económicos o raciales., en cada uno de estos grupos se recogerán diversos datos. En los conflictos territoriales se recogerán las regiones afectadas, en los religiosos las religiones afectadas, en los económicos las materias primas disputadas y en los raciales las etnias enfrentadas.
En los conflictos intervienen diversos grupos armados ( al menos dos) y diversas organizaciones mediadoras ( podrá no haber ninguna). Los mismos grupos armados y organizaciones mediadoras pueden intervenir en diferentes conflictos. Tanto los grupos armados como las organizaciones mediadoras podrán entrar y salir del conflicto, en ambos casos se recogerá tanto la fecha de incorporación como la fecha de salida. Temporalmente, tanto un grupo armado como una organización mediadora podrían no intervenir en conflicto alguno.
De cada grupo armado se recoge el código que se le asigna y un nombre. Cada grupo armado dispone al menos de una división y es liderado por al menos un líder político. Las divisiones de que dispone un grupo armado se numeran consecutivamente y se registrará el número de barcos, tanques, aviones y hombres de que dispone, asimismo se recoge el número de bajas que ha tenido. Para los grupos armados se recoge el número de bajas como suma de las bajas producidas en todas sus divisiones.
Los traficantes de armas suministran diferentes tipos de arma a los grupos armados. De cada tipo de armas se recoge un nombre y un identificador de su capacidad destructiva. De cada traficante se recoge un nombre, los diferentes tipos de armas que puede suministrar y cantidad de armas de cada uno de los tipos de armas que podría suministrar. Se mantiene número total de armas de cada uno de los diferentes tipos de armas suministrados por cada traficante a cada grupo armado.
Los líderes políticos se identifican por su nombre y el código de grupo armado que lideran. Además se recoge una descripción textual de los apoyos que éste posee.
Cada división la pueden dirigir conjuntamente un máximo de tres jefes militares, aunque cada jefe militar no dirige más de una división. A cada jefe militar se le identifica por un código, además se recoge el rango que éste posee, y dado que un jefe militar no actúa por iniciativa propia sino que siempre obedece a las órdenes de un único líder político de entre aquellos que lideran al grupo armado al que el jefe pertenece, se registrará el líder político al que obedece.
De las organizaciones medidoras se recogerá su código, su nombre, su tipo ( gubernamental, no gubernamental o internacional), la organización de que depende ( una como máximo), el número de personas que mantiene desplegadas en cada conflicto y el tipo de ayuda que presta en cada conflicto que será de uno y sólo uno de los tres tipos siguientes, médica, diplomática o presencial.
Con diversos fines, los líderes políticos dialogan con las organizaciones; se desea recoger explícitamente esta información. Así para cada líder se recogerán aquellas organizaciones con que dialoga y viceversa.
## # Gestión de nóminas
Una empresa decide informatizar su nómina. Del resultado del análisis realizado, se obtienen las siguientes informaciones:
A cada empleado se le entregan múltiples justificantes de nómina a lo largo de su vida laboral en la empresa y al menos uno mensualmente.
A cada empleado se le asigna un número de matrícula en el momento de su incorporación a la empresa, y éste es el número usado a efectos internos de identificación. Además se registra el NIF del empleado, nombre, número de hijos, porcentaje de retención para Hacienda, datos de cuenta corriente en la que se le ingresa el dinero ( banco, sucursal y número de cuenta) y departamentos en los que trabaja. Un empleado puede trabajar en varios departamentos y cada uno de ellos trabajar con una función distinta.
De un departamento se mantiene el nombre y cada una de sus posibles sedes.
Son datos propios de un justificante de nómina el ingreso total percibido por el empleado y el descuento total aplicado. La distinción entre dos justificantes de nómina se hará, además de mediante el número de matrícula del empleado, mediante el ejercicio fiscal y número de mes al que pertenece y un número de orden en el caso de varios justificantes de nómina recibidos el mismo mes.
Cada justificante de nómina consta de varias líneas ( al menos una de ingresos) y cada línea se identifica por un número de línea del correspondiente justificante. Una línea puede corresponder a un ingreso o a un descuento. En ambos casos, se recoge la cantidad que corresponde a la línea ( en positivo si se trata de un ingreso o en negativo si se trata de un descuento); en el caso de los descuentos, se recoge la base sobre la cual se aplica y el porcentaje que se aplica para el cálculo de estos
Toda línea de ingreso de un justificante de nómina responde a un único concepto retributito. En un mismo justificante, puede haber varias líneas que respondan al mismo concepto retributito. De los conceptos retributitos se mantiene un código y una descripción.
De cara a la contabilidad de la empresa, cada línea de un justificante de nómina se imputa al menos a un elemento de coste. Al mismo elemento de coste pueden imputársele varias líneas. Para cada elemento de coste, se recoge un código, una descripción y un saldo.
Entre los elementos de coste se establece una jerarquía, en el sentido de que un elemento de coste puede contener otros elementos de coste, pero un elemento de coste sólo puede estar contenido en, a lo sumo, otro elemento de coste.
En determinadas fechas, que se deben recoger, cada elemento de coste se liquida con cargo a varios apuntes contables ( código y cantidad) y a una o varias transferencias bancarias, de las que se recogen los datos de cuenta corriente ( banco, sucursal y número de cuenta) y la cantidad. Por cada apunte contable y transferencia bancaria se puede liquidar varios elementos de coste.
