---
title: "Programación concurrente distribuida"
---

# Programación concurrente distribuida

Programación concurrente distribuida

## 1.1 INTRODUCCIÓN

Ahora llega el momento de analizar el tipo de programación resultante de aplicar las ideas de concurrencia sin contar con la herramienta de una memoria común que facilite las tareas de comunicación entre los procesos concurrentes.

El nuevo escenario de trabajo, nos plantea que los procesos van a poder comunicarse y sincronizarse, siendo válidos todos los conceptos generales de la programación concurrente. Sin embargo, toda comunicación y sincronización deberá hacerse mediante el intercambio de información a través de unas líneas de comunicación física entre los procesadores que ejecutan los procesos concurrentes.

Esta necesidad de comunicación explícita mediante dispositivos, que serán mucho más lentos que la ejecución de los procesos y el resto de tareas internas a cada ordenador, nos lleva a intentar minimizar esta comunicación en aras de conseguir el mayor rendimiento posible. Por este motivo los sistemas de este tipo serán muy desacoplados, intercambiando la menor cantidad de información posible.

Las líneas de comunicación física son muy importantes pero su estudio escapa de los objetivos de este texto siendo materia de libros sobre redes de ordenadores y comunicaciones. A pesar de esto, necesitaremos razonar sobre ellas con un cierto nivel de abstracción y lo haremos mediante el concepto de canal, una línea de comunicación ideal, fiable al 100% y con una serie de características que analizaremos en un apartado específico posterior dada su importancia. La siguiente Figura representa el cambio conceptual planteado por este tipo de programación:

*(diagrama comparativo de los tres tipos de programación, con un bloque para cada uno; la extracción OCR sólo conservó las etiquetas sueltas que se reproducen a continuación y la disposición exacta no se pudo recuperar)*

Programa secuencial
1 Ordenador
1 Proceso
3 secciones
10 tareas
Programa concurrente para memoria única
1 Ordenador
3 Procesos
3 secciones
10 tareas
memoria única
Programa concurrente distribuido
3 Ordenadores
3 Procesos
3 secciones
10 tareas
canal canal
canal

Figura 8.1: Diferencias conceptuales entre los tres tipos de programación

Veremos ahora las nuevas características que presentan estos sistemas, todas condicionadas por las necesidades impuestas por la comunicación a través de canales.

### 1.1.1 Características

En sistemas de este tipo tendremos siempre varios ordenadores completos y separados físicamente, cada uno con su procesador, memoria y resto de componentes. A pesar de esta separación, tendremos la necesidad de interacción entre los ordenadores, para que los procesos puedan cooperar y exista el concepto de programa concurrente distribuido. Y esto nos llevará a la existencia de conexiones físicas entre los ordenadores que posibiliten su interacción.

Las conexiones van a influir en las posibilidades de programación disponibles. Podrán ser de varios tipos como:

- Conexión directa entre dos ordenadores mediante un cable serie o infrarrojos. Estas conexiones son lentas, poco fiables y sólo permiten crear sistemas específicos que se basen en la existencia de la conexión. Este tipo sólo es útil cuando se trabaja con algún componente que no es capaz de una conexión de mayor nivel y no es de interés para nosotros.
- Conexión directa con cable de tipo red, ya sea con cable o inalámbricas, pero entre dos equipos concretos. Estas conexiones son más eficientes y seguras, permitiendo una programación más genérica que podría escalarse fácilmente a conexiones de red. Sin embargo, el sistema seguirá estando limitado a trabajar con dos ordenadores y las ventajas de la programación distribuida no se alcanzan realmente. Esta situación no se da casi nunca.
- Conexión directa múltiple con cable de tipo red, pero sin alcanzar el nivel de red. En esta situación tendremos una serie de conexiones que al no estar apoyadas por un nivel de red que nos ofrezca protocolos de alto nivel, sería necesario conocer la topología de conexiones para poder desarrollar aplicaciones. Esta situación está limitada a necesidades concretas sin interés para nosotros.
- Conexión de red hacia una red completa, ya sea interna ( intranet) o con salida a Internet. En esta situación, además de las conexiones existen componentes hardware y protocolos software que no aíslan del componente físico de la red. Este es el escenario donde la programación concurrente distribuida adquiere sentido y se obtienen todas las ventajas que puede proporcionar. Para ello no será necesario la existencia de conexión a Internet. Una aplicación distribuida en la red interna de una organización puede suponer una mejora sustancial para el trabajo en la misma.

Como se puede apreciar, las características de la red influyen de manera determinante en las posibilidades de nuestro sistema. Esto se concreta en dos conceptos que van a ser muy importantes para calificar los sistemas, la escalabilidad y la apertura del sistema.

Un sistema escalable es aquel que permitirá que se añadan más equipos conectados, será capaz de utilizarlos y aumentará su rendimiento global. Como vemos, esta posibilidad va a depender de la red y sólo va a ser factible si la red es completa con protocolos de red que abstraigan la topología y el funcionamiento de bajo nivel.

En cuanto a los sistemas abiertos o no, se trata en este caso de que los componentes del sistema cumplan especificaciones públicas que todo fabricante pueda desarrollar. Se trata de que nuestro sistema no dependa de características establecidas unilateralmente por un fabricante o marca. Este concepto se aplica a todos los niveles, desde el hardware de los ordenadores o la red hasta el sistema operativo o el lenguaje. Debido a esto, existen muchos niveles de dependencia del fabricante siendo más importante la independencia del hardware.

Todo esto nos lleva a destacar unas características derivadas que se extraen directamente pero es importante tener claras que son:

- Existirá siempre concurrencia real, ya que siempre habrá hardware duplicado disponible para la ejecución de instrucciones de forma concurrente a disposición del programa.
- Debido al comportamiento de la conexión como una red, será necesario el concepto de nombrado que permitirá localizar a los ordenadores participantes sin conocer detalles sobre la red subyacente. Este concepto estará soportado por el software y los protocolos que conforman la red.

A partir de estas características se pueden justificar los motivos que habitualmente se aducen para utilizar la programación distribuida que son los siguientes:

- Se desea que los recursos de varios ordenadores sean compartidos en tiempo real y sin la utilización de dispositivos de almacenamiento externo ni medios manuales. Esta posibilidad es muy útil cuando la compartición es una necesidad y mediante estos sistemas se puede automatizar la misma. En otras situaciones estos sistemas ofrecen la posibilidad de informatización que no es posible sin la compartición de recursos.
- Se dispone de un recurso único y necesidad de utilizarlo por parte de varias personas. Estas situaciones suelen partir de un estado en el que las personas se tienen que desplazar al recurso y distribuir su uso de forma manual. Esto evoluciona a la existencia de un equipo que controla el uso del recurso y al que los operadores acceden de forma remota utilizando el programa distribuido.
- Se necesita aumentar la seguridad en el uso de ciertos recursos, y se pretende conseguirlo aislándolos físicamente de los operadores que acceden a los recursos mediante el software distribuido y disponiendo sólo de las operaciones que se le ofrezcan según el nivel de confianza que la organización le concede.
- Se precisa un aumento de la potencia de cálculo en el sistema, para conseguirlo, se crea una red de equipos entre los que se distribuye el trabajo para que el software tenga a su disposición más procesadores y memoria. Esta posibilidad dependerá siempre de que el algoritmo implementado tenga un nivel de paralelismo que permita este aumento.

Estas características y motivos para el uso de sistemas distribuidos, son las ventajas que se consideran que puede aportar un sistema de este tipo frente a los que no poseen la característica de la distribución. Resumiéndolas, podemos decir que las ventajas que este tipo de sistemas presentan son:

- Hardware más económico
- Mayor potencia de cálculo global
- Uso de la distribución de cálculo y datos
- Mayor fiabilidad global del sistema ante caídas y otros percances
- Posibilidad de escalabilidad del sistema
- Compartición recursos entre varios equipos

Aunque estas ventajas también se enfrentan con una serie de desventajas que son:

- Existe poco software distribuido que apoye los desarrollos ( esta afirmación es cada vez menos cierta si aún sigue siéndolo)
- La necesidad de una red con una buena fiabilidad y rapidez. Este elemento está presente en la actualidad en todos los sistemas por lo que ha dejado de ser un problema su existencia aunque sigue planteando un trabajo adicional su mantenimiento que puede ser laborioso en redes grandes.
- La seguridad que puede ser menor que en el caso de un ordenador único, aislado y bien protegido. Una conexión de red es una puerta abierta a los ataques si bien existen formas eficaces de evitar los problemas.

Dada la importancia que la red subyacente tiene, vamos a establecer una forma en la que usaremos dicha red desde nuestros programas, ya que aunque lo haremos desde un punto de vista abstracto, debemos hacer coincidir sus características con las de nuestra abstracción

### 1.1.2 Canales y tipos de programación

La caracterización que vamos a hacer de las conexiones de red se va a denominar canal y consiste en asumir que existe una conexión totalmente fiable y un sistema de nombrado que nos va a permitir crear un “tubo” que comunica dos procesos existentes en dos máquinas distintas y utilizarlo para enviar información entre los procesos.

La siguiente figura ilustra la idea de canal que vamos a manejar:

*(diagrama del canal abstracto que comunica directamente dos procesos frente a la comunicación real subyacente; sólo se conservan las etiquetas sueltas y la disposición exacta no se pudo recuperar de la extracción OCR)*

Pr1 Pr1
Canal

Figura 8.2: Canal abstracto y comunicación real

En esta Figura tenemos el canal abstracto que comunica los procesos directamente, desde nuestro punto de vista, aunque realmente existe toda la pila de protocolos de red y una conexión física que hacen el trabajo.

Los canales serán bidireccionales. Una vez establecido entre dos procesos, un canal entre dos procesos, cualquiera de los dos podrá enviar o recibir por el mismo.

Estos canales van a ser de dos tipos, con y sin capacidad de almacenamiento, que van a servir para modelar los dos tipos de comunicación a través de redes y los dos tipos de programación derivados de las mismas, la comunicación síncrona y asíncrona.

Además, cada canal tendrá asociado un tipo de datos, único válido para los elementos que se envíen por dicho canal. Esta característica permitirá simplificar la programación ya que el uso de canales sin tipo obliga a añadir mecanismos para detectar el tipo de lo que se ha recibido y realizar transformaciones de datos. El tipo de datos que aceptará cada canal no está limitado, pudiendo ser un tipo compuesto como registros o vectores aunque estos últimos no se recomiendan, siendo mejor el envío consecutivo de una serie de datos.

Estos dos tipos de comunicación han existido desde el comienzo de las redes de comunicaciones y se basan en dos modelos distintos de trabajo. El modelo síncrono establece la necesidad de que los dos extremos de la comunicación estén dispuestos para que la comunicación se produzca, mientras que el modelo asíncrono permitirá que uno de los extremos envíe datos aunque el otro no esté a la espera de los mismos y que el segundo pueda recibirlos más tarde sin problemas. También se denominan comunicación orientada a la conexión y orientada a datagramas. Los datagramas son las unidades de comunicación que se envían sin saber cuando se va a producir la recepción.

Los canales serán por tanto de tipo conexión o de tipo datagrama. En el caso de los canales para datagramas, dichos datagramas podrán quedar almacenados en la red, o en el propio sistema receptor pero en las capas inferiores del sistema, a la espera de ser solicitados.

Ya que los canales son nuestra caracterización de las conexiones subyacentes, debemos considerar que siempre existen, aunque presentemos mecanismos de mayor nivel que los lleguen a ocultar.

De los tipos de comunicación y de canales, se derivan los dos tipos fundamentales de programación distribuida, la programación síncrona y asíncrona. Sobre estos dos tipos, se establecerán algunos tipos adicionales que representen simplificaciones que aumentan el nivel de abstracción y facilitan la programación de sistemas.

## 1.2 TIPOS DE PROGRAMACIÓN DISTRIBUIDA

Los tipos básicos, síncrona y asíncrona, se basan en el envío explícito de mensajes, aunque también existen modelos de un nivel de abstracción superior que ocultan los propios canales. Veamos estos tipos de programación y las modificaciones a la sintaxis PseudoPascal necesarias.

### 1.2.1 Paso de mensajes

El paso de mensajes consiste en la creación de los programas necesarios en cada uno de los ordenadores, el establecimiento de canales de comunicación entre ellos y el envío de datos cuando sea necesario.

Estos programas se crean independientemente, se compilan y su única relación se establece en el momento de la ejecución, cuando se crean los canales y se envían los datos con las consiguientes validaciones de tipos de datos.

Por tanto, necesitaremos añadir al lenguaje las construcciones para:

- Definir el canal. En esta construcción será necesario incluir el identificador para el canal, el nombre del destino del canal ( el nombre del programa), el tipo de canal ( Síncrono o asíncrono) y el tipo de datos a enviar. La definición de un canal implica que en el momento de la ejecución del programa, el canal se crea sin problemas contra el programa que se encuentra o encontrará en el ordenador destino. Este canal existirá durante toda la ejecución del programa.
- Enviar datos, esta operación sólo debe recibir el identificador del canal de envío y una expresión cuyo tipo sea coherente con el tipo del canal a usar. La operación informará del resultado correcto o no de la acción mediante un valor lógico.
- Recibir datos. Esta operación necesita el identificador del canal y una variable sobre la que descargar los datos recibidos. La variable debe ser del mismo tipo que el canal a usar. La operación informará del resultado correcto o no de la acción mediante un valor lógico.

Los canales que vamos a utilizar se consideran de capacidad ilimitada. Por tanto, si queremos realizar un programa que controle que los datos sean recibidos en el destino, deberemos incluir la programación al efecto.

La sintaxis que vamos a utilizar para cada operación es:

```pascal
{ definición de tipos para canales }
type
reg= record
nombre:string;
edad :integer;
end;
{ definición de canales }
var
{ canal síncrono de tipo entero con destino “programa_01” }
canal1: channel sinc to ( programa_01) of integer ;
{ canal síncrono de tipo registro con destino “programa_02” }
canal2: channel sinc to ( programa_02) of reg;
{ canal asíncrono de tipo entero con destino “programa_02” }
canal3: channel asinc to ( programa_02) of integer ;
{ variables para recibir datos por el canal }
temp1:integer;
temp2:reg;
{ variables para comprobar si la comunicación fue correcta }
envio_correcto:boolean;
recepcion_correcta:boolean;
begin
cobegin
envio_correcto = send ( canal1,2*54);
envio_correcto = send ( canal3,2*54);
recepcion_correcta = receive ( canal1,temp1);
recepcion_correcta = receive ( canal2,reg);
recepcion_correcta = receive ( canal3,temp1);
coend;
end.
```

En la sintaxis que hemos utilizado, se introducen una serie de palabras clave que son: channel, sinc, asinc, to y of, que sirven para delimitar el tipo que estamos definiendo y separar los distintos componentes de su definición.

También hemos introducido dos operaciones que son send y receive que sirven para enviar y recibir respectivamente, independientemente del tipo de canal que estemos utilizando. Ambas operaciones son funciones cuyo resultado es boolean dando como resultado un valor falso si la operación no fue correcta por error de tipos o error de red.

El comportamiento de las operaciones será distinto dependiendo del canal y del estado de ocupación del mismo. Este comportamiento es:

- Send en canales asíncronos, siempre enviará el dato y continuará la ejecución con la siguiente instrucción.
- Send en canales síncronos, sólo enviará el dato y continuará la ejecución con la siguiente instrucción cuando el receptor esté esperando para recibir. En otro caso, se producirá un bloqueo voluntario ( sin espera activa) hasta que el destino ejecute receive. En este momento se producirá el envío y se pasará a la siguiente instrucción.
- Receive en canales asíncronos, recibirá el dato y continuará la ejecución con la siguiente instrucción si había algún dato pendiente en el canal. En caso contrario, quedará a la espera de que se produzca un envío.
- Receive en canales síncronos, sólo recibirá el dato y continuará la ejecución con la siguiente instrucción si el envío se intentó anteriormente y quedó bloqueado a la espera. En caso contrario se bloqueará sin espera activa hasta que el envío se produzca.

Es el momento de aplicar estas nuevas posibilidades sobre un programa y para ello empezaremos por el ejemplo sencillo que hemos desarrollado en la programación de memoria única. Se trata de la utilización de la variable X por dos procesos que suman y restan una unidad a su valor. En el caso de programación distribuida, la forma de conseguir comunicación es el envío explicito, por tanto, ahora habrá que decidir cuando el valor terminará de usarse en un programa para enviárselo al otro. Para dar al programa más riqueza, devolveremos el valor modificado al primer programa para que sea este el que imprima el resultado. El canal será síncrono en esta primera versión.

```pascal
{------------------------------------------------------------}
{-- primera versión distribuida }
{------------------------------------------------------------}
program dist_v1_equipo_A;
var x:Integer; { variable a intercambiar }
c: channel sinc to ( dist_v1_equipo_B) of integer;
begin
x:=0;
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
x:=x+1; { antes SC }
send ( c,x); { envío el valor }
receive ( c,x); { recibo los cambios }
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
write ('El valor de X es:');
writeln ( x);
end.
program dist_v1_equipo_B;
var x:Integer; { variable a intercambiar }
c: channel sinc to ( dist_v1_equipo_A) of integer;
begin
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
receive ( c,x); { recibo los cambios }
x:=x-1; { SC }
send ( c,x); { envío el valor }
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
end.
```

Los cambios realizados en el programa para adaptarlo a las características de la programación distribuida, implican que incluso el diagrama de precedencia cambie. Este cambio se deriva de la desaparición del concepto de sección crítica, sustituida por la comunicación explícita. También tiene gran importancia en los cambios producidos el hecho de que ahora la comunicación no se centra en variables y su contenido cambiante. Ahora lo importante es un conjunto de datos que pueden pasar por diferentes variables, en diferentes máquinas siendo habitual que las variables sigan conteniendo los mismos valores aún cuando el dato que contenían se haya enviado a otro ordenador y se considere que es allí donde está ahora.

Los nombres de los canales en cada equipo pueden variar. Se sabrá que es el canal correcto por el ordenador de destino y el tipo del canal. Además, no crearemos más de un canal hacia otro proceso que sea del mismo tipo.

El cambio en los diagramas de precedencia que se pueden observar en el siguiente diagrama, vemos como el nivel de concurrencia aumenta debido a que estos procesos son más desacoplados.

En el diagrama para PMU tenemos las líneas de precedencia de sincronización y la dependencia que implica el tener dos secciones críticas que hay que proteger.

En cambio, para programación distribuida tenemos que desaparecen las líneas de sincronización pero aparecen otras líneas que representan el intercambio explícito que sustituya al uso de variables compartidas.

*(dos diagramas de precedencia enfrentados, el de programación de memoria única y el de programación concurrente distribuida; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

X=0
X=0
Nada Nada Nada
Nada
SC SC SC
SC
Nada Nada Nada
Nada
writeln ( x)
writeln ( x)
Programación de memoria única Programación concurrente distribuida

Figura 8.3: Diagramas de precedencia PMU y distribuido

Es importante destacar que lo que ha ocurrido sigue las normas que hemos establecido. En primer lugar tenemos que añadir las líneas que nos permitan realizar la comunicación cuando lo deseemos, y en segundo lugar tendremos que eliminar algunas líneas de sincronización ya que las tareas iniciales o finales quedarán sólo en uno de los procesos y la relación de precedencia con los demás procesos ya no tendrá sentido.

En muchas ocasiones ocurrirá que el diagrama debe ser modificado para ajustarse a las necesidades de comunicación explícita como en este caso. También ocurrirá que desaparezcan líneas ya que las dependencias entre algunas tareas carecen ya de sentido.

Por último, incluimos dos cronogramas que muestran el comportamiento del programa en dos situaciones distintas. Este es el comportamiento que tendremos dependiendo de que proceso llegue antes a las llamadas de comunicación. Se puede apreciar que hay pocas diferencias entre ambos, esto es debido a que se han realizado dos llamadas seguidas en sentidos contrarios, por este motivo, siempre alguno de los procesos tendrá que esperar:

*(dos cronogramas de Pr1 y Pr2 sobre el eje de tiempo t; parte de las etiquetas aparece escrita al revés en la extracción OCR ("dnes" por "send", ".cer" por "rec.") y la disposición exacta de los ejes y las líneas no se pudo recuperar)*

Pr1 X=0
X
Pr2
.cer
SC Nada Writeln ( x);
X
Nada SC Nada
t
Pr1 X=0 Nada SC Nada writeln ( x);
X X
Pr2 Nada SC Nada
t
dnes
dnes
.cer
.cer
dnes
dnes
.cer

Figura 8.4: Cronogramas del programa distribuido síncrono

En esta primera implementación hemos utilizado canales síncronos ( sin capacidad de almacenamiento, o sin memoria). Si queremos sustituirlos por canales asíncronos, sólo habrá que cambiar la definición del canal por una de estas dos:

```pascal
c: channel asinc to ( dist_v1_equipo_B) of integer;
c: channel asinc to ( dist_v1_equipo_A) of integer;
```

Según el proceso que estemos modificando. El resto del código será válido, y el comportamiento cambiará aunque estos cambios no tendrán efecto sobre el cronograma que quedará así:

*(dos cronogramas de Pr1 y Pr2 sobre el eje de tiempo t para la versión asíncrona; parte de las etiquetas aparece escrita al revés en la extracción OCR ("dnes" por "send", ".cer" por "rec.") y la disposición exacta de los ejes y las líneas no se pudo recuperar)*

Pr1 X=0
X
Pr2
.cer
SC Nada writeln ( x);
X
Nada SC Nada
t
Pr1 X=0 Nada SC Nada writeln ( x);
X
X
Pr2 Nada SC Nada
t
dnes
dnes
.cer
.cer
.cer
dnes
dnes
X

Figura 8.5: Cronogramas del programa distribuido asíncrono

El comportamiento del programa ha variado ya que vemos en ambos cronogramas que el send de Pr1 se ejecuta sin esperar, pero el receive siguiente se queda bloqueado, por tanto el comportamiento final resulta ser igual en cuanto a rendimiento y secuencia de ejecución de cada proceso.

Esto no será igual en todos los casos, y en general, la programación asíncrona producirá mejores resultados de rendimiento en los programas ya que el nivel de acoplamiento es menor.

La programación asíncrona obtendrá mayores cotas de concurrencia en la mayoría de los casos.

Veamos ahora un ejemplo de comunicación entre dos procesos en el que la información viaja siempre en la misma dirección. Se trata del problema denominado “productor-consumidor” ya que es equivalente a que uno de los procesos genere información o la extraiga de alguna fuente y el otro la reciba y la utilice. Vamos a implementar una versión de este problema que produce 10 valores en un proceso ( pidiéndoselos al usuario) y se los envía al otro que los imprime.

```pascal
{------------------------------------------------------------}
{-- productor-consumidor de 10 datos, versión distribuida }
{------------------------------------------------------------}
program productor_dist;
var x: integer; { variable a intercambiar }
c: channel sinc to ( consumidor_dist) of integer;
i: integer; { contador }
begin
for i:=1 to 10 do
begin
write ('introduzca un dato: ');
readln ( x);
send ( c,x); { envío el valor }
end;
end.
program consumidor_dist;
var x: integer; { variable a intercambiar }
c: channel sinc to ( productor_dist) of integer;
i: integer; { contador }
begin
for i:=1 to 10 do
begin
receive ( c,x); { recibo el valor }
write ('El dato es: ');
writeln ( x);
end;
end.
```

El diagrama que representa este comportamiento es el siguiente:

*(diagrama de precedencia del productor-consumidor de 10 datos, con diez nodos de lectura y diez de escritura; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x) Writeln ( x)
readln ( x) readln ( x) readln ( x) readln ( x) readln ( x) readln ( x) readln ( x) readln ( x) readln ( x) readln ( x)

Figura 8.6: Diagrama de precedencia prod-cons de 10

En este diagrama vemos que ningún arco va desde las operaciones de escritura las de lectura. Por tanto, se podría conseguir un alto grado de concurrencia si el ritmo de los dos procesos fuese similar. Como el primer proceso implica la acción del usuario, siempre irá más lento, pero sería beneficioso que el usuario no tuviese que esperar a que el segundo programa consumiera los datos. Esto se conseguiría si el canal fuese asíncrono.

Los cronogramas para el canal síncrono y el asíncrono quedarían así:

*(dos cronogramas de Pr1 y Pr2 sobre el eje de tiempo t, uno para el canal síncrono y otro para el asíncrono; parte de las etiquetas aparece escrita al revés en la extracción OCR ("dnes" por "send", ".cer" por "rec.") y la disposición exacta no se pudo recuperar)*

- dnes dnes: dnes dnes: dnes
- Pr1 readln ( x): readln ( x) readln ( x): readln ( x): readln ( x)
- X X: X: X
- Pr2: writeln ( x) writeln ( x): writeln ( x): writeln ( x)
- .cer .cer: .cer .cer: .cer
t
Síncrono
- dnes dnes: dnes dnes: dnes
- Pr1 readln ( x): readln ( x) readln ( x): readln ( x) readln ( x)
- X X: X: X
- Pr2: writeln ( x) writeln ( x): writeln ( x): writeln ( x)
- .cer .cer: .cer: .cer .cer
t
Asíncrono

Figura 8.7: Cronogramas para prod-cons de 10

Se puede apreciar que en el caso asíncrono se reducen las esperas en el caso de que el productor sea más rápido o el consumidor se vea retrasado por algo ya que el productor puede continuar y los valores quedan almacenados en el canal.

Esta forma de crear programas, en la que hay que realizar cada envío de cada datos explícitamente es muy laboriosa y poco eficaz, obligando a prestar atención a unos detalles que no tienen interés para el programador. Por este motivo se plantean nuevas posibilidades.

### 1.2.2 RPC

Esta es la mejora que se plantea sobre el paso de mensajes. Se trata de utilizar canales síncronos para implementar la comunicación a un nivel de abstracción superior en el que no se manejan los canales directamente ni para definirlos ni para realizar envíos o recepciones.

La forma de comunicar ahora los procesos será llamando a procedimientos definidos en otros procesos. El nombre RPC significa, en inglés, Remote Procedure Call ( llamada a procedimientos remotos). Los parámetros de la llamada serán los datos enviados en una u otra dirección según sea el tipo del parámetro. La propia llamada implicará sincronización debido a que los canales utilizados serán síncronos.

El comportamiento del proceso que llama será el siguiente:

- Ejecuta la llamada RPC escrita por el programador.
- Se produce la creación de los canales de forma automática.
- Se envía la información al receptor.
- Se produce un bloqueo voluntario hasta que la información llegue al receptor, que puede no estar aún disponible, éste la procese y responda.
- Se recibe la respuesta y se carga en los parámetros de salida si los hubiera.
- Se pasa a la siguiente instrucción a la llamada RPC.

Y el comportamiento del proceso que se ofrece para ser llamado será el siguiente:

- Ejecuta la oferta RPC escrita por el programador.
- Se produce la creación de los canales de forma automática.
- Se espera a recibir la información del llamador, si no estuviera disponible, se bloqueará el proceso.
- Una vez recibida la llamada, se carga en los parámetros y se ejecuta el código escrito por el programador.
- Se envía la respuesta como resultado de la ejecución.
- Se pasa a la siguiente instrucción a la oferta RPC.

El cronograma que representa este comportamiento, teniendo en cuenta dos llamadas y que en cada caso sea uno de los procesos el que llega antes sería:

*(cronograma de Pr1 y Pr2 sobre el eje de tiempo t para dos llamadas RPC; parte de las etiquetas aparece escrita al revés en la extracción OCR ("amall" por "llama", "erbicer" por "recibe", "evleuved" por "devuelve") y la disposición exacta no se pudo recuperar)*

Pr1
Pr2
t
amall
evleuved
Ejecuta
erbicer
amall
erbicer
evleuved
Espera Espera
Ejecuta
Espera

Figura 8.8: Cronogramas para RPC

En el cronograma podemos ver que el proceso que llama siempre espera el tiempo de ejecución del procedimiento que invoca. Además de esta espera, uno de los dos procesos esperará al otro debido al carácter síncrono de los canales que utilizamos.

La sintaxis que vamos a utilizar en PseudoPascal para implementar las llamadas RPC es la siguiente:

```pascal
{ en el programa que ofrece RPC, de nombre acepta_RPC }
program acepta_RPC;
begin { cuerpo del programa }
accept proc1; { aquí se incluirán parámetros cuando sean
necesarios }
begin
end;
accept proc2 ( a:IN integer); { los parámetros IN son de entrada }
begin
end;
accept proc3 ( b:OUT integer); { los parámetros OUT son de salida }
begin
end;
accept proc4 ( a:OUT integer; b,c:IN integer); {se pueden combinar
tipos}
begin
end;
end.
{ en el programa que llama de nombre llama_PRC }
program llama_RPC;
var c:integer; { para recibir el resultado de las llamadas }
begin
acepta_RPC.proc1 (); { llamada sin parámetros }
acepta_RPC.proc2 ( 23*5); { llamada con una entrada }
acepta_RPC.proc3 ( x); { llamada con una salida }
acepta_RPC.proc4 ( x,45,3); { llamada con una entrada y dos salidas }
end.
```

En las llamadas hemos utilizado el nombre del proceso que contiene los procedimientos que queremos ejecutar y la notación “.”, la misma que en registros y objetos.

En las ofertas de procedimientos, hemos utilizado la palabra reservada accept y las palabras IN y OUT para establecer la dirección del envío de datos que representan los parámetros.

No existen parámetros que sirvan simultáneamente para enviar en las dos direcciones. Sólo pueden ser IN o OUT.

Rescribimos el programa que creamos con canales para utilizar RPC en él:

```pascal
{------------------------------------------------------------}
{-- primera versión distribuida }
{------------------------------------------------------------}
program dist_v2_equipo_A;
var x:Integer; { variable a intercambiar }
begin
x:=0;
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
x:=x+1; { antes SC }
dist_v2_equipo_B.decrementa ( x,x); { envío y recibo el valor }
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
write ('El valor de X es:');
writeln ( x);
end.
program dist_v2_equipo_B;
begin
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
accept decrementa ( a:IN integer; b:OUT integer); { recibo los
cambios }
begin
b:=a-1;
end;
writeln ('nada'); { aquí hay concurrencia }
writeln ('nada');
writeln ('nada');
end.
```

El código ha quedado mucho más sencillo, a pesar de que se trataba de un ejemplo básico con código muy simple. Hemos eliminado las definiciones de los canales y los envíos explícitos y también la definición de la variable x en el proceso B.

Esto mismo se puede aplicar al caso del “productor-consumidor”:

```pascal
{------------------------------------------------------------}
{-- productor-consumidor de 10 datos, versión RPC }
{------------------------------------------------------------}
program productor_dist;
var x: integer; { variable a intercambiar }
i: integer; { contador }
begin
for i:=1 to 10 do
begin
write ('introduzca un dato: ');
readln ( x);
consumidor_dist.consume ( x); { envío el valor }
end;
end.
program consumidor_dist;
var i: integer; { contador }
begin
for i:=1 to 10 do
begin
accept consume ( a:IN integer); { recibo el valor }
begin
write ('El dato es: ');
writeln ( a);
end;
end;
end.
```

En este caso se vuelve a conseguir simplicidad en el código aunque el rendimiento será inferior ya que a no existe casi concurrencia, tan sólo un proceso secuencial distribuido en dos equipos.

Este último ejemplo y otros que se verán en la sección de ejemplos nos enfrenta a la pérdida de rendimiento en el caso de los canales síncronos. Ya que este mecanismo, tiene el problema de que el proceso llamado se queda a la espera desde que ofrece un servicio hasta que éste es solicitado. Es necesario mejorar esta situación para obtener un mayor rendimiento de los equipos implicados en los sistemas distribuidos. Un planteamiento en esta línea es un tipo especial de RPC denominado cliente-servidor.

### 1.2.3 Cliente - servidor

El modelo o paradigma cliente-servidor ( en adelante CS) se basa en ideas similares a las que tenemos en RPC, la existencia de una oferta para ejecutar un cierto código, y un proceso que demanda la ejecución de dicho código. Sin embargo, el modelo extiende esta idea independizándose de la implementación concreta que se realice y estableciendo las características de modo genérico, útil para muchos lenguajes y tipos de aplicaciones.

La clave de este tipo de programación reside en que no todos los procesos participantes van a ser iguales ( no en código que casi nunca lo serán) en comportamiento. En un sistema CS sólo los procesos de tipo cliente iniciarán la comunicación hacia los procesos servidores que les ofrecen sus servicios.

Esta primera aproximación nos da las tres palabras clave en los sistemas CS:

- Servidor, un proceso distinguido cuya misión es ofrecer algo a otros procesos.
- Clientes, procesos principales del sistema que guían la ejecución del mismo y solicitan de los servidores la realización de tareas cuando es necesario.
- Servicios, tareas que ofrece realizar un servidor cuando le sea solicitado por un cliente mediante una llamada.

Por lo que hemos descrito hasta este momento, no existen demasiadas diferencias con RPC, pero en realidad sí las hay, fundamentalmente en el comportamiento del servidor.

Un servidor, contendrá en su interior un bucle infinito denominado de servicio. Un servidor ofrecerá un servicio o más, disponibles permanentemente para cualquier cliente, en lugar de estar ofrecidos en un momento puntual. El número y tipo de los servicios variará con el tiempo si el servidor evoluciona o cambia de estado. Estos cambios serán producidos por la invocación de servicios.

Un proceso servidor no realiza otras tareas distintas a las de ofrecer servicios o ejecutarlos. Las únicas tareas adicionales que forman parte de un servidor son las de inicialización de los recursos que el servidor posea y que se realizan antes del comienzo del bucle de servicio.

El siguiente diagrama representa esta idea de bucle de servicio:

*(diagrama del bucle de servicio de un servidor: un bloque de inicialización seguido de un bucle que ofrece los servicios; sólo se conservan las etiquetas y la disposición exacta no se pudo recuperar de la extracción OCR)*

Inicialización
svc1
svc2
svc3

Figura 8.9: Esquema de funcionamiento de un servidor

El motivo para que un proceso sea distinto de los demás y se establezca como servidor son varios, algunos objetivos ( el proceso no puede ser otra cosa que un servidor por causas externas) y otros subjetivos ( la elección como servidor no es obligada pero se toma así). Los motivos más habituales son:

- La existencia de un recurso especial y único al que sólo puede estar conectado un ordenador y que debe ser usado por otros. En el ordenador conectado se implementará un proceso servidor que ofrezca acceso al recurso mediante la ejecución de servicios.
- La posibilidad de reducir el número de ciertos recursos a uno creando una configuración como la anterior para reducir gastos. Es el caso de las impresoras.
- La necesidad de una potencia de cálculo elevada en momentos puntuales que es más recomendable concentrar en un sólo equipo y que los demás le soliciten la ejecución del trabajo pesado cuando sea preciso. De esta forma se consigue a un precio menor, tener un equipo más potente que si fuese necesario tener varios.
- La necesidad de un nivel de seguridad elevado. Los sistemas distribuidos son más sensibles a los problemas de seguridad, si se concentra en un equipo ciertos recursos, se puede realizar una inversión en seguridad más efectiva y barata.

Una vez establecido que un proceso va a ser servidor, se debe organizar para cumplir el esquema de funcionamiento que hemos descrito.

La forma de trabajar propuesta por CS se crea sobre las mismas conexiones y tecnologías de red que hemos estado manejando hasta ahora, por tanto, deberíamos poder implementar un servidor utilizando las misma instrucciones de PseudoPascal que hemos definido hasta ahora. Sin embargo, esto no es posible porque la necesidad de ofrecer más de un servicio y que cualquiera sea atendido sin esperar a los demás no se puede cumplir con las instrucciones actuales. Para conseguirlo es necesario introducir un concepto nuevo denominado espera selectiva y nueva sintaxis en el lenguaje que extienda la sintaxis RPC para permitir un nuevo comportamiento.

La construcción sintáctica que vamos a manejar es la siguiente:

```pascal
select { comienzo de la estructura de espera selectiva }
when a<b then
accept svc1;
begin
end;
or { separación entre los servicios ofrecidos }
when a<b then
accept svc2;
begin
end;
or { separación entre los servicios ofrecidos }
when a>=b then
accept svc3;
begin
end;
end;
```

Cuyo significado es que se ofrecen los tres servicios delimitados por las palabras select, or y end. Si alguno de los tres servicios es solicitado, se ejecutará de forma concurrente con el propio servidor en un procesos nuevo de tipo PMU quedando el servidor disponible y terminando la ejecución de la propia instrucción select. Pero los servicios que se ofrecerán no serán siempre los tres. Los servicios sólo se ofrecen si la expresión asociada al servicio, mediante la cláusula when, es verdadera.

La expresión y la cláusula when permiten que el conjunto de servicios ofrecidos por un servidor varíe. Si se desea que un servicio esté ofrecido siempre bastará con ponerle una condición siempre cierta como true.

Por tanto, la instrucción se combina con un bucle que puede ser infinito o no, y que sirve para que se ofrezcan los servicios permanentemente.

Un programa servidor responderá a la siguiente estructura:

```pascal
programa servidor;
var
final: boolean; { variable de control del servidor }
begin
final:=false; { si un servicio no cambia esta valor el bucle no
acaba }
repeat
select { comienzo de la estructura de espera
selectiva }
when a<b then
accept svc1;
begin
end;
or { separación entre los servicios ofrecidos }
when a<b then
accept svc2;
begin
end;
or { separación entre los servicios ofrecidos }
when a>=b then
accept svc3;
begin
end;
end;
until final; { si la variable final cambia a true el servidor
para }
end.
```

Y los clientes serán igual que los procesos de llamada RPC anteriores ya que la diferencia la tenemos ahora en el comportamiento del servidor que ahora siempre disponible ( desde que se pone en marcha) y los clientes nunca tienen que esperar.

El rendimiento de CS será mejor que el de RPC porque los clientes ya no tienen que esperar al servidor y el tiempo de espera del servidor no se considera relevante para el tiempo total del sistema.

La espera que realiza un servidor que no tiene peticiones se considera que no es activa y que el componente de gestión de red se encarga de despertar al proceso servidor cuando alguna petición se recibe por los canales que tiene asignados ( de forma transparente).

#### 1.2.3.1 CLIENTE - SERVIDOR, ABSTRACCIÓN Y CAPAS

La organización de las aplicaciones según la propuesta CS ayuda a la organización de los programas aportando un nivel de abstracción mayor, no sólo por utilizar las ideas de RPC, ya que una vez creado un servidor, de las tareas que se le encargan nos podemos olvidar y limitarnos a usarla. La separación ( desacoplamiento) entre los clientes y los servidores es casi máximo ya que lo único que necesita saber un cliente de un servicio es el nombre, los parámetros y en que servidor reside.

Esta mejora en la abstracción es útil en la creación de grandes aplicaciones, pero con el tiempo, se han planteado situaciones en las que las tareas de los clientes o de los servidores se han complicado y como respuesta a tal problema se ha propuesto la descomposición de cada uno de ellos en nuevos subsistemas CS dando lugar a las capas. El siguiente diagrama muestra esta evolución hacia las n-capas:

*(diagrama de la evolución de la estructura cliente-servidor hacia n-capas, con una fila para 2 capas, otra para 3 capas y otra para 4 capas; sólo se conservan las etiquetas y la disposición exacta no se pudo recuperar de la extracción OCR)*

Cliente Servidor
2 capas
Cliente Servidor
3 capas
Cliente Servidor
4 capas

Figura 8.10: Capas Cliente-servidor

En el diagrama tenemos la estructura original con un cliente y un servidor, luego tenemos la estructura en tres capas que implica la descomposición de las tareas del servidor en tareas de dos niveles, quedando el servidor que ofrece servicios al cliente como un cliente del servidor final de la cadena.

Este proceso de descomposición se puede aplicar también en el cliente y repetirse las veces que sea necesario creando encadenamientos CS de las capas que sean necesarias.

## 1.3 EJEMPLOS Y EJERCICIOS

En este apartado intentaremos ilustrar la forma de programar en la creación de programas distribuidos mediante ejemplos y proponer ejercicios para que el lector pueda probar a desarrollar sus propios programas.

### 1.3.1 Ejemplos

1) El primer ejemplo que vamos a utilizar nos va a servir para ilustrar los cambios que suelen ser necesarios en los diagramas de precedencia generales para implementarlos como programas distribuidos. Plantearemos un diagrama sencillo, el ejemplo de sumar y restar uno a una cantidad. El diagrama que representa este programa es:

*(diagrama de precedencia del ejemplo de sumar y restar uno; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

x =0
- x=x+1 - x=x-1
W ( x)

Sobre este diagrama, tenemos que añadir una línea para enviar el dato de un nodo a otro una vez que se ha modificado. Lo añadimos desde la suma a la resta y luego eliminamos las redundancias resultantes y obtenemos:

*(el mismo diagrama de precedencia tras añadir la línea de envío del dato y eliminar las redundancias; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

x =0
- x=x+1 - x=x-1
W ( x)

Que es un diagrama secuencial. A pesar de esto, puede seguir siendo útil la programación distribuida si alguna de las tareas trabaja con un recurso sensible a la seguridad. Por tanto realizamos dos posibles particiones en procesos que pueden ser:

*(las dos posibles particiones en procesos del diagrama anterior, mostradas una junto a otra; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos y de las particiones no se pudo recuperar de la extracción OCR)*

- x =0 - x =0
- x=x+1: x=x-1: x=x+1: x=x-1
- W ( x) - W ( x)

Estas particiones nos mostrarán finalmente el número de envíos, y canales que necesitaremos.

2) Si aplicamos la misma idea sobre un diagrama un poco más complicado y aplicamos los mismos pasos, vemos que volvemos a tener un diagrama secuencial:

*(diagrama de precedencia con tres sumas, antes y después de eliminar redundancias; sólo se conservan las etiquetas de los nodos y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

x =0 x =0
x=x+1 x=x+2 x=x+3 x=x+1 x=x+2 x=x+3
Eliminar Redundancias
W ( x) W ( x)

3) Vamos a intentar esta misma idea sobre un diagrama un poco más complicado como puede ser:

*(diagrama de precedencia más complejo, con los nodos A, B, C, D, E, F, G, H e I y los valores V1 y V2 que viajan entre ellos; sólo se conservan las etiquetas y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

A
B
V1
D
V2 V2
F C
V1
E
H
V2
V1
I
V2
G

En este diagrama tenemos el problema de que los valores V1 y V2 deben viajar entre los nodos donde se utilizan y que no pueden usarse en paralelo porque este daría lugar a dos valores distintos.

Para V1 tenemos que el uso que se hace en B es anterior por las líneas de precedencia a lo dos usos que se hacen en E y H. En cambio, estos dos últimos se hacen en paralelo y esto hay que evitarlo. Añadiremos un arco entre los nodos E-H. La dirección del arco puede ser cualquiera de las dos pero si empieza en E, esto implicaría que el dato V1 tendría que ser enviado dos veces, primero desde B a D para que lo tenga E y luego de E a H. Si el arco empieza en H, el valor no tendrá que viajar más veces porque desde B a H está en el mismo proceso.

Para V2, el problema está en los usos en F y C ya que el uso en I y G se realizan en secuencia y no hay conflicto. Para F y C hay que añadir un arco que partirá de F para minimizar los envíos.

El diagrama quedará:

*(el mismo diagrama tras añadir los arcos E-H y F-C, con los arcos de envío etiquetados con el valor que transportan; sólo se conservan las etiquetas y la disposición exacta de los arcos no se pudo recuperar de la extracción OCR)*

A
B
V1
D
V2 V2
F V2 C
V1
E
V1
H
V2
V1
I
V2
V2
G

Pero ahora hay que eliminar las redundancias, las que ya teníamos y las que han aparecido nuevas. Hemos etiquetado los arcos que envían valores para evitar su eliminación ya que ésta haría inviable la implementación.

El resultado es:

*(el diagrama resultante tras eliminar las redundancias, con los nodos repartidos entre los procesos Pr1, Pr2 y Pr3; sólo se conservan las etiquetas y la disposición exacta de los arcos y de las particiones no se pudo recuperar de la extracción OCR)*

Pr2
A
Pr1
B
V1
Pr3
D
V2 V2
F V2 C
V1
E
V1
H
V2
V1
I
V2
V2
G

Y ahora lo implementamos. Lo haremos con canales sin capacidad de almacenamiento ya que para envíos únicos como los de este programa, no hay diferencia de rendimiento entre un caso y otro.

La idea de establecer el código de antes y después de cada nodo y la secuencia de los mismos seguirá siendo válida en programación con canales, facilitando la creación de los programas a partir de diagramas de precedencia.

El número de canales y dirección dependerá de la información a enviar. Sólo crearemos un canal si es necesario. Analizaremos los procesos por pares:

Pr1-Pr2: Será necesario un canal para el envío de V1 y los envíos de sincronización. El tipo del canal será el de V1 ( por ejemplo T1).

Pr2-Pr3: Sólo hay un arco que sirve para enviar V2, habrá un canal de tipo T2.

Pr1-Pr3: sólo hay un arco que envía V2 luego un canal de tipo T2.

```pascal
{------------------------------------------------------------}
{-- ejemplo 2, diagrama complejo }
{------------------------------------------------------------}
program Pr1;
var V1: T1;
V2: T2;
temp: T1; { variable para recibir la sincronizacion }
c_1_2 : channel sinc to ( Pr2) of T1;
c_1_3 : channel sinc to ( Pr3) of T2;
begin
{ -- nodo D -- }
receive ( c_1_2, temp); { recepción de sincronización }
D;
send ( c_1_2, temp); { envío de sincronización }
{ -- nodo E -- }
receive ( c_1_2, V1); { recepción de dato V1 }
E; { uso de V1 }
{ -- nodo G -- }
receive ( c_1_3, V2); { recepción de dato V2 }
G; { uso de V2 }
end.
program Pr2;
var V1: T1;
V2: T2;
temp: T1; { variable para recibir la sincronizacion }
c_2_1 : channel sinc to ( Pr1) of T1;
c_2_3 : channel sinc to ( Pr3) of T2;
begin
{ -- nodo A -- }
A;
{ -- nodo B -- }
B; { uso de V1 }
send ( c_2_1, temp); { envío de sincronización }
{ -- nodo F -- }
F; { uso de V2 }
send ( c_2_3, V2); { envío de dato V2 }
{ -- nodo H -- }
receive ( c_2_1, temp); { recepción de sincronización }
H; { uso de V1 }
send ( c_2_1, V1); { envío de dato V1 }
end.
program Pr3;
var V2: T2;
c_3_2 : channel sinc to ( Pr2) of T2;
c_3_1 : channel sinc to ( Pr1) of T2;
begin
{ -- nodo C -- }
receive ( c_3_2, v2); { recepción de dato V2 }
C; { uso de V2 }
{ -- nodo I -- }
I; { uso de V2 }
send ( c_3_1, v2); { envío de dato V2 }
end.
```

Utilizaremos la nomenclatura “c_1_2” para indicar que se está definiendo un canal desde el proceso 1 al 2 ( son bidireccionales). Se podrán admitir pequeñas variaciones con “can_1_5” o “can_prod_cons” o “can_cli1_ser3”, siempre que quede claro el origen, el destino y el hecho de ser un canal.

4) Otro ejemplo interesante es la creación de una versión CS del problema de productor-consumidor. Para realizarlo, tenemos dos posibilidades, que el productor sea cliente o que el consumidor sea cliente. En CS es el cliente el que lleva el control global de la aplicación por tanto, la elección dependerá de qué parte se considere más importante, si la producción o la consumición.

En el caso de que el productor sea cliente:

```pascal
{------------------------------------------------------------}
{-- productor, cliente }
{------------------------------------------------------------}
program productor_cliente;
var V1: T1;
final: boolean; { para indicar el final del productor }
begin
final:=false;
repeat
{ producir V1 }
V1:=1;
{ llamar al servidor enviándole V1 y esperando que lo consuma }
consumidor_servidor.consumir ( V1);
until final;
end.
program consumidor_servidor;
var final: boolean; { para indicar el final del consumidor }
begin
final:=false;
repeat { no usamos select porque sólo hay un servicio ofrecido }
accept consumir ( v1:IN T1); { recibir }
begin
{ consumir el dato V1}
end ;
until final;
end.
```

En el caso de que el consumidor sea cliente:

```pascal
{------------------------------------------------------------}
{-- consumidor, cliente }
{------------------------------------------------------------}
program productor_servidor;
var final: boolean; { para indicar el final del productor }
begin
final:=false;
repeat { no usamos select porque sólo hay un servicio ofrecido }
accept producir ( v1:OUT T1); { enviar }
begin
{ producir V1 }
V1:=1;
end ;
until final;
end.
program consumidor_cliente;
var V1: T1;
final: boolean; { para indicar el final del consumidor }
begin
final:=false;
repeat { no usamos select porque sólo hay un servicio ofrecido }
productor_servidor.producir ( V1); { llamamos para recibir dato }
{ consumir el dato V1}
until final;
end.
```

5) Un ejemplo de mayor envergadura sería el que responde al siguiente enunciado: “Vamos a considerar una base de datos programada como servidor. Esta base de datos sólo admitirá un cliente de forma simultánea y ofrecerá cuatro servicios: con, dat, des, parar. El servicio parar hará que el servidor pare, con realizará la conexión, des la desconexión y dat una petición de datos con una entrada tipo cadena con la información consultada y una salida de cadena con el resultado”

El servidor necesitará una variable de estado que controle los servicios que se ofrecen en cada momento ya que una vez conectado un cliente, no debe poder conectarse otro. Para esto, lo mejor es que no esté disponible el servicio de conexión.

Los estados se resumen en el siguiente diagrama:

*(diagrama de estados del servidor de base de datos, con los estados Desconectado, Conectado y Parado y las transiciones etiquetadas con los servicios; sólo se conservan las etiquetas y la disposición exacta de las transiciones no se pudo recuperar de la extracción OCR)*

con dat
Desconectado Conectado
salir
des
Parado
salir

La implementación del servidor y un cliente sería:

```pascal
{ Base de Datos para un usuario }
{ 4 servicios: con, dat, des, parar }
program servidor;
type
estados=( conectado,desconectado);
var
estado: estados;
parar : boolean;
begin
estado:=desconectado;
parar :=false;
while not parar do
select
when estado=desconectado then
accept con;
begin
estado:=conectado;
end;
or when estado=conectado then
accept dat ( pet:IN string; res:OUT string);
begin
res:=pet;
end;
or when estado=conectado then
accept des;
begin
estado:=desconectado;
end;
or when true then
accept parar; { sin guarda, siempre disponible }
begin
parar:=true;
end;
end; { select }
end. { servidor }
{----------------------------------------------------------------------}
{----------------------------------------------------------------------}
program cliente;
var
datos: string;
begin
servidor.con;
servidor.dat ('hola',datos);
servidor.dat ( datos,datos);
servidor.des;
servidor.parar;
end.
```

### 1.3.2 Ejercicios

1) Implementar una base de datos como la del ejemplo pero con capacidad para 30 usuarios y los mismos servicios. Ahora habrá que llevar la cuenta de usuarios conectados y tendremos un nuevo estado. El diagrama de estados quedará

*(diagrama de estados propuesto para el ejercicio, con los estados Desconectado, Conectado, Máx. conex. y Parado; sólo se conservan las etiquetas y la disposición exacta de las transiciones no se pudo recuperar de la extracción OCR)*

con dat dat
con
des
con
Desconectado Conectado Máx. conex.
des
des
salir
salir
Parado
salir

2) Implementar en PseudoPascal con canales las dos particiones sobre el diagrama hexagonal asimétrico. Se asume que no hay datos que compartir.

*(diagrama hexagonal asimétrico, repetido dos veces para mostrar las dos particiones, con los nodos A, B, C, D, E y F; sólo se conservan las etiquetas y la disposición exacta de los arcos y de las particiones no se pudo recuperar de la extracción OCR)*

A A
B C B C
D E D E
F F

3) Crear un programa CS en el que tenemos un servidor que ofrece dos servicios, uno sirve para comprobar que una cadena no contiene dígitos numéricos y otro para convertir a mayúsculas las letras de una cadena que no tenga dígitos numéricos, dando una salida vacía en caso contrario. Crearemos un cliente que le pide cadenas al usuario y si una cadena sólo contiene letras la vuelve a escribir en mayúsculas, pero si la cadena contiene números, termina la ejecución con un mensaje. Para implementar las tareas del cliente se utilizarán los servicios incluidos en el servidor. El servidor incluirá otro servicio para que se pueda parar su ejecución una vez que no se le van a pedir más servicios.

4) Crear un programa similar al anterior pero utilizando sólo canales, aprovechando el orden que siempre siguen las operaciones. El programa que sustituye al servidor debe acabar cuando no vayamos a tener más llamadas.
