---
title: "Programación concurrente de memoria común"
---

# Programación concurrente de memoria común

Concurrencia de memoria común

## 1.1 INTRODUCCIÓN

La programación concurrente se denomina de memoria única cuando tenemos una única memoria central donde residen todos los datos utilizados por el ordenador ytodos los procesos en ejecución, así como el sistema operativo y los recursos utilizados por éste. Una memoria no implica una UCP ( Procesador, Unidad Central de Proceso o
CPU). Podemos tener varias y será recomendable para conseguir la ejecución concurrente. La Figura 7.1 representa nos posibles tipos de ordenador sobre los que ser realizaría la programación concurrente de memoria única ( en adelante sólo programación para memoria
única o PMU). Figura 7.1: Esquemas de ordenadores para programación concurrente de memoria única
Este modelo de programación está fuertemente influido por la arquitectura de los ordenadores ya que la comunicación y sincronización se van a realizar mediante el usode variables situadas en esta memoria común que se compartirán entre varios procesos. Estas variables compartidas estarán en la base de todos los mecanismos de PMU,
permitiendo su existencia y creando los problemas a los que deberá dar solución la PMU. Para ilustrar claramente la idea de las variables compartidas, tenemos los dos diagramas de la Figura 7.2. Estos diagramas representan la memoria única, en la que vamosa situar dos procesos. Para estos dos procesos se muestra la estructura interna de la
 memoria asignada, habitualmente dotada por los sistemas operativos, que varía en cada caso pero en línea de mínimos coincide con lo representado. En el diagrama ( a), tenemos solamente los procesos con su contenido formado por:
el código, las variables globales y la memora dinámica en la cual se irá tomando la cantidad requerida para el crecimiento de la pila del proceso y el montículo. En el diagrama ( b), tenemos también un pequeño espacio de la memoria reservado para como variable compartida y podemos observar que dicha variable, no forma parte de ninguno de los dos procesos ya que la memoria en la que se aloja está reservada en otra zona distinta. Sin embargo, ambos procesos cuentan con dicha variable como zona de memoria utilizable.
*(diagrama con dos esquemas de memoria (a) y (b): en ambos, la memoria total disponible para Pr1 y para Pr2 se divide en código, variables globales y memoria dinámica (pila y montículo); en el esquema (b) se añade además una zona de memoria reservada para una variable compartida, situada fuera del espacio de ambos procesos; parte del texto de las etiquetas apareció invertido letra a letra en la extracción OCR y la disposición exacta de los bloques no se pudo recuperar)*

Figura 7.2: Memoria de los procesos usando una variable compartida
Gracias a estas variables compartidas, podemos comunicar dos procesos,
sincronizarlos o comunicarlos sincronizadamente. La comunicación pura, implica el intercambio de información mediante una omás variables de forma que los procesos depositan o toman información en las variables sin control ninguno. Estos valores son valores de información relevante para las aplicaciones concretas sin significado para la gestión de los procesos concurrentes. En el caso de la sincronización, también se utilizan variables, pero los valores depositados tienen un significado muy específico e importante para la gestión de los procesos concurrentes que se realiza en base a dichos valores.
Por último, la comunicación sincronizada, combina ambos conceptos, teniendo un intercambio de información relevante para la aplicación controlado por un intercambio de información que permite la gestión de la concurrencia y del intercambio de información de aplicación de forma correcta. Para ilustrar los tres conceptos vamos a plantear sistemas en los que se necesitan outilizan los tres enfoques en el uso de las variables compartidas. Para la comunicación pura, vamos a suponer la existencia de un sistema de medición de la temperatura exterior y su representación en un panel informativo para su lectura directa por personas. Cada una de las dos partes del sistema, será implementada mediante un proceso, y estos procesos se comunicarán mediante una variable compartida en la que el proceso de medición de la temperatura dejará un valor cada cierto tiempo y el proceso de escritura en el panel lo tomará para escribirlo. La velocidad de refresco requerida para el sistema no es muy elevada en la parte de visualización ya que los seres humanos no somos capaces de distinguir imágenes que cambian a mayor velocidad que
1/25 de segundo. Además, si en algún momento falla la sincronización y uno de los dos procesos se adelanta al otro, se tomará una temperatura y se mostrará dos veces o se escribirá una nueva temperatura antes de que la última sea leída y ésta se perderá. Pero estono es un problema porque la temperatura necesita minutos para variar y no décimas de segundo ( lo que detectaría el ojo humano) ni milésimas de segundo ( lo que tardarían nuestro procesos en tomar una nueva temperatura correcta). Por todo esto, el sistema de la Figura 7.3 implementa una comunicación pura.
20 ºC
Figura 7.3: Sistema con comunicación pura
Este tipo de sistemas se dan habitualmente en la realidad cuando aparecen este tipode situaciones en las que el valor de un dato concreto es muy escaso. En cambio, sistemas en los que se realice una sincronización pura son un poco más difíciles de encontrar, ya queesta características es más usada a bajo nivel.
Un sistema ejemplo de sincronización pura podría ser el formado por varios procesos en los que tenemos uno especial encargado de inicializar una impresora y otros que deben imprimir por esta impresora una vez que esté lista. El proceso de inicialización puede durar unos 10 segundos y cada proceso de impresión deberá recibir un documento,
prepararlo e imprimirlo, pudiendo tardar las tareas previas a la impresión de 2 a 15
segundos. Se ve claramente que merece la pena que todos los procesos se inicien a la vez,
para que se ejecute la mayor cantidad de trabajo en paralelo, pero las impresiones no podrán empezar hasta que el proceso especial inicialice la impresora. En este punto hará
falta una sincronización entre el proceso y los demás, sin ningún otro intercambio que el destinado a asegurar el correcto orden de las operaciones. La Figura 7.4 representa este sistema. Inic. Rec. Rec. Rec. Rec. Prep. Prep. Prep. Prep. Imp. Imp. Imp. Imp. Figura 7.4: Sistema con sincronización pura
El tercer tipo, comunicación sincronizada, es el más utilizado de todos, ya que los datos manejados suelen ser muy importantes y no es admisible su pérdida o duplicación. Existen mucho ejemplos de sistemas de este tipo, pero vamos a utilizar uno muy interesante que consiste en un conjunto de cabinas de votación y un sistema central de recuento. Cada cabina estará modelada en su funcionamiento por un proceso y el sistema central por otro. La comunicación del valor de cada uno de los votos se realizará mediante una variable compartida por cada una de las cabinas más variables adicionales de control para cada variable compartida que nos informe de que un voto nuevo está disponible o deque el voto ya ha sido contabilizado por el sistema central. El diagrama de la Figura 7.5
representa este sistema.
*(diagrama con varias cabinas de votación, cada una con su variable de control "v. control", enviando sus valores a un único "Proceso de recuento" central; la disposición exacta de las flechas no se pudo recuperar de la extracción OCR)*

Figura 7.5: Sistema con comunicación sincronizada
Tanto estas como otras situaciones o sistemas, deberán ser representadas utilizando las herramientas que hemos presentado en el capítulo anterior, PseudoPascal y diagramas de precedencia. Empezaremos con un primer ejemplo de programa que corresponde al esquema dela comunicación pura. Se trata de un programa que toma una variable compartida X y lesuma 1, 2 y 3 en tres procesos distintos. La representación de este programa según la técnica de los diagramas de precedencia es:
*(diagrama de precedencia: el nodo inicial "x=0" se ramifica en tres nodos paralelos "x=x+1", "x=x+2" y "x=x+3" que confluyen en un nodo final "W(x)")*

Figura 7.6: Primer programa concurrente
Y el código equivalente en PseudoPascal:
program conc_001;
var
x: integer; { variable compartida }
procedure pr1; { instrucciones de un proceso }
begin x:=x+1;
end;
procedure pr2; { instrucciones de otro proceso }
begin x:=x+2;
end;
procedure pr3; { instrucciones de otro proceso }
begin x:=x+3;
end;
begin { programa principal }
x:=0; { inicialización de la variable compartida }
cobegin pr1;
pr2;
pr3;
coend writeln ( x);
end. Este primer programa cuyo objetivo es realizar tres sumas debería producir unvalor final en la variable X de 6. Pero, ¿es éste el resultado? El problema que existe es que las operaciones de tipo “X:=X+1” no son indivisibles. En realidad el procesador realiza como mínimo tres operaciones como las siguientes:
- Cargar en un registro de la CPU el valor de X desde la memoria.
- Sumar 1 al valor del registro.
- Devolver el resultado obtenido en el registro a la memoria designada por X. Debido a esta descomposición del contenido en varias operaciones, surgen los problemas que serán mayores cuanto mayor sea una sección crítica, debido a que tendrá
mayor número de instrucciones y mayor duración. Veamos una serie de cronogramas de la posible ejecución de este programa y su efecto sobre la variable X según los procesos tengan mejor o peor fortuna en su ejecución sobre el sistema operativo:
*(dos cronogramas del valor de x frente al tiempo durante la ejecución de Pr1, Pr2 y Pr3: uno que alcanza correctamente el valor final 6 (secuencia 0, 1, 3, 6) y otro en el que un solapamiento hace que el resultado final quede en 3; la disposición exacta de los ejes y las líneas no se pudo recuperar de la extracción OCR)*

Figura 7.7: Cronogramas del primer programa concurrente
En la Figura 7.7 tenemos el cronograma que conseguiría el resultado deseado y otroen el que obtendremos un 3 en lugar de un 6. Esto es debido a que se solapan los uso de la variable compartida dando lugar a resultados intermedios que no son tenidos en cuenta para la solución final.

*(tres cronogramas adicionales del valor de x frente al tiempo para Pr1, Pr2 y Pr3, cada uno con un solapamiento distinto; la disposición exacta de los ejes y las líneas no se pudo recuperar de la extracción OCR)*

Figura 7.8: Más cronogramas del primer programa concurrente
El los cronogramas de la Figura 7.8, todos los valores obtenidos son incorrectos debido a los solapamientos y la pérdida de valores intermedios. Este ejemplo nos plantea el principal problema derivado del uso de variables compartidas, que afecta a toda tarea realizada en los programas concurrentes y es preciso solucionar.
El indeterminismo ( no tener un comportamiento siempre fijo) es inherente a la programación concurrente, tenemos que crear programas que aseguren un funcionamiento correcto en toda situación.
Como paso previo a la solución vamos a presentar la definición del concepto de sección crítica que nos servirá para referirnos a las secciones de código donde se pueden producir solapamientos y pérdida de valores intermedios. Decimos que una sección crítica es: “Un fragmento de código donde la corrección del programa puede verse comprometida por el uso de variables compartidas, si su ejecución se solapa en el tiempo con otros fragmentos que usen las mismas variables”. Repasando el programa anterior, vemos que el contenido de cada uno de los tres procesos que lo formaban eran tres secciones críticas y si se solapaban en el tiempo entre ellas, siempre se obtenía un resultado incorrecto. Por tanto, la solución al problema es evitar el solapamiento. Esto se conoce como exclusión mutua entre secciones críticas y nuestro objetivo será asegurar sin posibilidad de error que esta exclusión se produce siempre. Si conseguimos esto sobre el programa planteado, el resultado será equivalente atener un único proceso. El cronograma de la Figura 7.9 lo muestra.

*(dos cronogramas comparando Pr1, Pr2 y Pr3 ejecutados con exclusión mutua frente a un programa secuencial equivalente, ambos alcanzando la secuencia de valores 1, 2, 3; la disposición exacta de los ejes y las líneas no se pudo recuperar de la extracción OCR)*

Figura 7.9: Cronogramas de programa concurrente y secuencial
Entonces ¿cuál es la ventaja de utilizar programación concurrente? ¿es realmente recomendable su uso? La respuesta a estas preguntas es que sí es recomendable porque se obtiene un ahorro en el tiempo de ejecución de los programas. Esto es debido a que los procesos que crearemos no contendrá únicamente código peligroso, secciones críticas. La mayoría del código de un proceso no será S. C. y su ejecución en paralelo con otro código será
permitida y recomendable ya que nos llevará a la disminución en el tiempo total de ejecución.
Para ilustrar estas ideas volveremos ahora crear un cronograma pero, en esta ocasión, con procesos más cercanos a la realizar, con menor proporción de S. S. C. C. en su código. La Figura 7.10 contiene estos dos cronogramas.

*(dos cronogramas de Pr1 y Pr2 marcando sus secciones críticas (SC) en el eje de tiempo: "Cronograma sin colisión, paralelismo total", donde las SC de ambos procesos no se solapan, y "Cronograma con colisión, peligro de error, se debe disminuir el paralelismo", donde las SC se solapan en un "espacio de colisión"; la disposición exacta de los ejes y las líneas no se pudo recuperar de la extracción OCR)*

Figura 7.10: Cronogramas con y sin solapamiento de S. S. C. C. Como se aprecia, el problema de la corrección, realmente no produce programas aleatorios, crea programas que sólo funcionan mal en pocas ocasiones cuando se dan ciertas circunstancias. Los programas que sólo tienen un comportamiento erróneo en pocas ocasiones son peligrosos porque pueden superar las fases de pruebas, y se llega confiar en ellos. Cuando se produce el fallo causa más problemas. Por tanto, la concurrencia nos interesa a pesar del problema del solapamiento de regiones críticas. Tan sólo, deberemos asegurar la exclusión mutua en el tiempo de la ejecución de las distintas secciones críticas. Para conseguirlo ha habido históricamente dos fases principales. La primera en la que se aportaban soluciones algorítmicas que era preciso implementar cada vez y la segunda en que se dejaba en manos del compilador conseguir la exclusión. Veremos las dos a continuación.

## 1.2 EVOLUCIÓN HISTÓRICA

El comienzo de estas técnicas se produce cuando aparece el primer hardware capazde ejecutar programas en varios procesadores y usa sola memoria. En esta situación se crean los primeros programas y como resultado aparecen todos los conceptos que hemos presentado, solapamiento, sección crítica, exclusión mutua. Con estos problemas y las herramientas disponibles, la única solución era desarrollar algún algoritmo que consiguiese la exclusión mutua sin contar con el hardware. Es el primer hito, las soluciones algorítmicas. Se desarrollan varios algoritmos que permiten asegurar la exclusión mutua. Las primeras versiones añaden nuevos problemas que se van solucionando paulatinamente hasta llegar a algoritmos suficientemente completos para no plantear problemas añadidos y obtener el objetivo de exclusión mutua. Sin embargo, pronto se comprueba que mediante algoritmos es imposible conseguir exclusión mutua sin tener un bucle permanente de comprobación de ciertos indicadores. Esta situación que se denomina “espera activa” es un inconveniente muy importante ya que sobrecarga los sistemas con la ejecución de instrucciones sin ninguna utilidad. En el siguiente subapartado, veremos en detalle el problema de la espera activa. Además, las soluciones algorítmicas presentan una complejidad elevada a incluir para proteger cualquier acceso a una sección crítica dando lugar a programas mucho más complejos. Por tanto, es necesario encontrar soluciones basadas en el hardware, se requieren modificaciones en los procesadores y arquitecturas que permitan eliminar alguno de los dos problemas que encontramos. El primer esfuerzo, de bajo nivel, consiste en añadir a los procesadores alguna instrucción indivisible que realice como una sola instrucción dos delos pasos que se requieren para completar los algoritmos. Son las instrucciones exchange,
decremento-incremento y text-and-set. Estas instrucciones se traducen en un mecanismo que se usa en los programas de alto nivel, denominado cerrojo que permite simplificar las tareas necesarias para proteger el acceso a una sección crítica a una línea de código sencillo, reduciendo las posibilidades de error y mejorando la legibilidad del código. El mecanismo de los cerrojos implicaba un acceso casi directo a instrucciones del procesador y seguía implicando espera activa, por tanto, se debe seguir mejorando. Esto dalugar al primer mecanismo capaz de solucionar todos los problemas, el semáforo. El semáforo es un mecanismo de programación de alto nivel basado en modificaciones en elhardware que no son accesibles al programador, están ocultos por la implementación quehace el sistema operativo. Este mecanismo no tiene espera activa y su uso en la protección de secciones críticas es tan sencillo como usar un procedimiento de librería. Además, los semáforos permiten comunicar, sincronizar y comunicar sincronizadamente sin solapamiento y sin espera activa. Gracias a los semáforos, se han solucionado todos los problemas inicialmente planteados. Esto nos permite crear programas de mayor tamaño y fiabilidad, dando lugar aun uso extendido de este tipo de programación y llevando el mecanismo al límite de sus posibilidades. Al usar semáforos en programas de gran tamaño se descubre que siendo una
 herramienta muy flexible y sencilla, tenía el problema de que se podía utilizar incorrectamente dando lugar a programas con problemas de bloqueo infinito y otros. Como posible mejora de los semáforos se plantea el mecanismo región crítica que consiste en añadir un bloque para incluir código en su interior que implica la ejecución en exclusión mutua. De esta forma, es el propio compilador es que puede verificar si se crearon correctamente las secciones críticas. Esta propuesta supone un avance en el nivel conceptual de los mecanismos aunque al crearse específicamente para solucionar el problema de la comunicación sincronizada, queda mal cubierto el caso de sincronización precisando de la inclusión de dos modificaciones, las regiones críticas condicionales ylas regiones críticas condicionales con eventos. Gracias a la inclusión de las regiones críticas, se consigue realizar programas mayores con menor complejidad y menos posibilidad de error. Esta situación junto con la aparición de la programación orientada a objetos, produce la aparición de un nuevo mecanismo acorde con el enfoque de objetos. Este mecanismo son los monitores que consisten en crear un componente semejante a un objeto en el que tenemos como elemento central los datos compartidos ycomo métodos accesibles desde fuera tenemos las secciones críticas que antes estaban mezcladas con los procesos del programa. Por tanto, se reúnen las secciones críticas junto alos datos compartidos que manejan y se simplifica su uso a una llamada a un método que se incluyen en el punto donde haya que usar el dato compartido. A pesar de las mejoras aportadas por los monitores, sucede igual que en las regiones críticas, habiendo dejado pendiente la sincronización pura y necesitando de la inclusión de modificaciones para evitar la espera activa. Se añaden varias opciones como las compuertas que son semejantes a semáforos. El siguiente gráfico resumen la evolución temporal de los mecanismos y el motivo de lo pasos que se fueron produciendo:
Evolución de los mecanismos de protección de secciones críticas

*(línea temporal con los mecanismos "Problemas iniciales", "Algoritmos", "Cerrojos", "Semáforos", "RC", "Monitores" sobre un eje de tiempo "t", con anotaciones adicionales sobre soluciones software/hardware, eliminación de la espera activa, mayor nivel de abstracción y orientación a objetos; el texto de estas anotaciones apareció con las letras entremezcladas en la extracción OCR y no se pudo reconstruir con la fidelidad exigida — el contenido ya está descrito en el párrafo anterior)*

Figura 7.11: Historia de los mecanismos para proteger secciones críticas

### 1.2.1 Espera activa

Este concepto es bastante sencillo, pero conviene analizar un poco más sus repercusiones sobre el funcionamiento de un sistema para darle la importancia real que tiene. Vamos a pensar en un sistema PMU con tres procesos en el que uno de ellos está
en situación de espera activa. Esto significa que dicho proceso sólo ejecuta un bucle sencillo consultando una variable lo que implica que no va a requerir ningún acceso de E/Sa recursos. El proceso estará siempre ejecutando o preparado para ejecutar sin utilizar otros estados posibles mientras esté en estado de espera activa. En esta situación, el proceso siempre está listo para entrar en la CPU o dentro, en cambio los demás realizarán solicitudes E/S cada cierto tiempo y siempre que vuelvan al estado preparado, tendrán que esperar a que el proceso en espera activa termine en la CPU, siendo un proceso que siempre completa todo su tiempo asignado porque no hace otra cosa que un bucle. Además de esta repercusión sobre el resto de los procesos, la CPU pasará a estar ocupada al 100% ya que siempre está este proceso listo para seguir ejecutando su bucle. La
Figura 7.12 muestra este efecto sobre la CPU de un proceso con espera activa. Figura 7.12: CPU con situación de espera activa
Tras una situación de espera activa que se resuelve el sistema recuperará la normalidad rápidamente como vemos en la Figura 7.13. Figura 7.13: Estado de la CPU tras superar la espera activa
Por último, pensemos en un sistema con 10 procesos en espera activa. La concurrencia real se pierde y todos los procesos esperan siempre para usar la CPU.

## 1.3 DESCRIPCIÓN DE LAS SOLUCIONES

Vamos a repasar una a una las soluciones propuestas para solucionar el problema del solapamiento en el uso de las variables compartidas. Recordamos que la enumeración realizada no es exhaustiva, existen unos pocos mecanismos adicionales pero no los hemos considerado de interés para la exposición.

### 1.3.1 Algoritmos

Esta primera solución se caracteriza por ser la primera propuesta disponible generada tras crearse los primeros equipos con capacidad de concurrencia y producirse la detección del problema del indeterminismo por solapamiento en el tiempo de los accesos avariables compartidas. Estos algoritmos intentarán aportar soluciones sin contar con unhardware que las apoye, lo que determinará que no puedan alcanzar el nivel de perfección deseado aunque sentarán las bases necesarias para poder crear mecanismos absolutamente seguros y eficientes. La base de los algoritmos y la posteriores soluciones consiste siempre en conseguir que los procesos se excluyan mutuamente cuando desean utilizar los recursos compartidos. Para conseguirlo, se incluye un código extra que rodea cada sección crítica de los procesos con una fase previa de bloqueo del recurso que nos asegure su exclusividad y unafase posterior de desbloqueo para que el resto de los procesos puedan usarlo. Esquemáticamente podemos representar estas fases como se aprecia en el diagrama de la Figura 7.14.

*(diagrama de tres bloques en secuencia: "Bloqueo", "Sección crítica" y "Desbloqueo")*

Figura 7.14: Sección crítica protegida
Los algoritmos creados proponen distintas formas de realizar los bloqueos basándose en variables compartidas adicionales y distintos protocolos de actualización que intentan garantizar la exclusión mutua. Para ilustrar el funcionamiento de cada algoritmo, vamos a plantear un programa enel que tenemos el problema de la indeterminación motivado por el uso de la variable x,
sobre el que aplicaremos cada uno de los algoritmos comprobando sus efectos. El uso de la variable x se producirá en dos procesos distintos incrementándola y decrementándola respectivamente. El resultado en la variable x dependerá del orden de ejecución de los procesos. Se ha añadido a cada proceso una serie de instrucciones fuera de la sección crítica para representar un programa más realista son las instrucciones writeln (‘nada’);.
{------------------------------------------------------------}
{-- versión inicial, con indeterminismo }
{------------------------------------------------------------}
program algoritmos_Version_0;
var x:Integer; { variable compartida }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
{----------------------}
x:=x+1; { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
{----------------------}
x:=x-1; { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
cobegin
Pr1; Pr2;
coend;
end. El resultado del programa puede ser 1, 2, o 3, y no hay forma de determinar cual será el valor obtenido. Por este motivo necesitamos acceso a x en exclusión mutua. Vamosa aplicarle las diversas propuestas algorítmicas para analizar el efecto conseguido.
La primera solución consiste en usar una marca o indicador sobre un recurso para indicar que está libre u ocupado. Se trata de otra variable compartida de cualquier tipo pero generalmente de tipo lógico cuyos valores se decide que significan ocupado o libre. El código resultante de modificar el programa es:
{------------------------------------------------------------}
{-- versión primera, con un indicador para el recurso }
{------------------------------------------------------------}
program algoritmos_Version_1;
var x:Integer; { variable compartida }
ind:boolean; { indicador para proteger el recurso }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
while ind do ; { esperando a que el recurso esté libre }
ind:=true; { ocupamos el recurso }
{----------------------}
x:=x+1; { SC }
{----------------------}
ind:=false; { liberamos el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
while ind do ; { esperando a que el recurso esté libre }
ind:=true; { ocupamos el recurso }
{----------------------}
x:=x-1; { SC }
{----------------------}
ind:=false; { liberamos el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
ind:=false; { recurso libre }
cobegin
Pr1; Pr2;
coend;
end. Esta primera posibilidad parece solucionar el problema pero no lo consigue deltodo. Si se da la circunstancia de que lo dos procesos realicen la comprobación simultáneamente, los dos encontrarán el recurso libre, los dos lo marcarán como ocupado ylos dos entrarán en la sección crítica y seguiremos teniendo el mismo problema.
Lo que se ha conseguido en este caso es reducir la probabilidad de que exista indeterminación a unas pocas situaciones, sin embargo, ha introducido otro problema queserá inherente a toda solución algorítmica, la espera activa. Otra posible solución que se plantea para mejorar los resultados de la primera es lade utilizar varios indicadores, uno en cada proceso mediante el cual cada proceso pueda indicar su intención de usar el recurso y los demás puedan consultarlo para decidir cómo actuar, esperando o indicando su intención. El código resultante de aplicar esta algoritmo es:
{------------------------------------------------------------}
{-- versión segunda, con un indicador para cada proceso }
{------------------------------------------------------------}
program algoritmos_Version_2;
var x:Integer; { variable compartida }
ind_pr1:boolean; { indicador para el proceso 1 }
ind_pr2:boolean; { indicador para el proceso 2 }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr1:=true; { quiero usar el recurso }
while ind_pr2 do ; { esperando a que el recurso esté libre }
{----------------------}
x:=x+1; { SC }
{----------------------}
ind_pr1:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr2:=true; { quiero usar el recurso }
while ind_pr1 do ; { esperando a que el recurso esté libre }
{----------------------}
x:=x-1; { SC }
{----------------------}
ind_pr2:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
ind_pr1:=false; { proceso 1 no usa el recurso }
ind_pr2:=false; { proceso 2 no usa el recurso }
cobegin
Pr1; Pr2;
coend;
end. Se puede ver que seguimos teniendo espera activa, y que si los dos procesos activan su indicador para indicar su interés en usar la variable y luego comprueban el delotro procesos, los dos se lo encuentran a verdadero y se quedan esperando indefinidamente. Esta situación se llama interbloqueo ( deadlock) porque es un bloqueo que cada uno provoca sobre el otro. Un sistema en esta situación no se recupera si los procesos no son eliminados manualmente. Para mejorar esta situación de interbloqueo se propuso que si un proceso encontraba que el otro proceso tenía activado su indicador, los desactivara temporalmente para que uno de los dos consiguiera seguir adelante. Con esta modificación el código quedaría:
{------------------------------------------------------------}
{-- versión tercera, con un indicador para cada proceso }
{-- y liberación en la espera }
{------------------------------------------------------------}
program algoritmos_Version_3;
var x:Integer; { variable compartida }
ind_pr1:boolean; { indicador para el proceso 1 }
ind_pr2:boolean; { indicador para el proceso 2 }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr1:=true; { quiero usar el recurso }
while ind_pr2 do { esperando a que el recurso esté libre }
begin ind_pr1:=false; { doy paso un momento al otro proceso }
ind_pr1:=true;
end;
{----------------------}
x:=x+1; { SC }
{----------------------}
ind_pr1:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr2:=true; { quiero usar el recurso }
while ind_pr1 do { esperando a que el recurso esté libre }
begin ind_pr2:=false; { doy paso un momento al otro proceso }
ind_pr2:=true;
end;
{----------------------}
x:=x-1; { SC }
{----------------------}
ind_pr2:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
ind_pr1:=false; { proceso 1 no usa el recurso }
ind_pr2:=false; { proceso 2 no usa el recurso }
cobegin
Pr1; Pr2;
coend;
end. En este caso hay espera activa, interbloqueo sí hay sincronización total entre procesos y otro problema denominado cierre ( o lockout o inanición o starvation) que consiste en que uno de los procesos puede quedarse siempre esperando si el otro termina muy rápido su SC y vuelve a querer entrar antes de que el otro proceso reaccione. El proceso nunca llega a continuar y por eso se dice que muere de inanición. Como solución a estos problemas, tenemos el denominado “algoritmo de
Dekker” ( 1968) que es similar pero añade una variable turno que sirve para dirimir las situaciones en que los procesos pidan el acceso simultáneamente. El código quedaría de la siguiente forma:
{------------------------------------------------------------}
{-- versión cuarta, con un indicador para cada proceso }
{-- e indicador de turno }
{-- Algoritmo de Dekker }
{------------------------------------------------------------}
program algoritmos_Version_4;
var x:Integer; { variable compartida }
ind_pr1:boolean; { indicador para el proceso 1 }
ind_pr2:boolean; { indicador para el proceso 2 }
turno:Integer; { indicador del turno de proceso }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr1:=true; { quiero usar el recurso }
while ind_pr2 do { esperando a que el recurso esté libre }
begin if turno=2 then { si no es mi turno }
begin ind_pr1:=false; { doy paso un momento al otro proceso }
while turno=2 do ; { espero mi turno }
ind_pr1:=true; { me toca }
end;
end;
{----------------------}
x:=x+1; { SC }
{----------------------}
turno :=2; { paso el turno al otro proceso }
ind_pr1:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr2:=true; { quiero usar el recurso }
while ind_pr1 do { esperando a que el recurso esté libre }
begin if turno=1 then { si no es mi turno }
begin ind_pr2:=false; { doy paso un momento al otro proceso }
while turno=1 do ; { espero mi turno }
ind_pr2:=true; { me toca }
end;
end;
{----------------------}
x:=x-1; { SC }
{----------------------}
turno :=1; { paso el turno al otro proceso }
ind_pr2:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
ind_pr1:=false; { proceso 1 no usa el recurso }
ind_pr2:=false; { proceso 2 no usa el recurso }
turno :=1; { proceso con prioridad }
cobegin
Pr1; Pr2;
coend;
end. En esta ocasión, se solucionan todos los problemas previos salvo el de la espera activa que no es posible solucionar sin ayuda del hardware. Este algoritmo es una solución suficiente dentro de las posibilidades de un algoritmo para conseguir la exclusión mutua, sin embargo es algo compleja la implementación y puede llevar a errores su utilización. Esto nos lleva a la última versión que vamos a ver, denominada “algoritmo de Peterson” ( 1981) que realiza las mismas tareasy tiene las mismas características pero el turno se utiliza en la fase de bloqueo, fuera de la sección crítica y simplifica bastante el código. El resultado es:
{------------------------------------------------------------}
{-- versión quinta, con un indicador para cada proceso }
{-- e indicador de turno }
{-- Algoritmo de Peterson }
{------------------------------------------------------------}
program algoritmos_Version_5;
var x:Integer; { variable compartida }
ind_pr1:boolean; { indicador para el proceso 1 }
ind_pr2:boolean; { indicador para el proceso 2 }
turno:Integer; { indicador del turno de proceso }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr1:=true; { quiero usar el recurso }
turno :=2; { paso el turno al otro proceso }
while ind_pr2 and turno=2 do { esperando a recurso libre }
{----------------------}
x:=x+1; { SC }
{----------------------}
ind_pr1:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
ind_pr2:=true; { quiero usar el recurso }
turno :=1; { paso el turno al otro proceso }
while ind_pr1 and turno=1 do { esperando a recurso libre }
{----------------------}
x:=x-1; { SC }
{----------------------}
ind_pr2:=false; { ya he terminado con el recurso }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
ind_pr1:=false; { proceso 1 no usa el recurso }
ind_pr2:=false; { proceso 2 no usa el recurso }
cobegin
Pr1; Pr2;
coend;
end. Esta solución sólo tiene el problema de la espera activa, que por sí solo es suficiente para plantearse la necesidad de tener algo mejor. Además de estos algoritmos, tenemos también: el algoritmo incorrecto de Hyman,
el algoritmo de Eisenberg-McGuire y el algoritmo de Lamport. No vamos a desarrollarlos porque no es necesario para comprender las necesidades que deben cubrir los mecanismosy porque ha quedado demostrado que necesitamos mecanismos sin espera activa.

### 1.3.2 Cerrojos

Los cerrojos son la primera aportación del hardware para conseguir unas fases de bloqueo y desbloqueo simplificadas. Consisten en la inclusión de una instrucción en el procesador que sea indivisible y realice como en un paso un par de operaciones necesarias para la verificación de la fase de bloqueo. La más significativa de estas operaciones por ser la más compleja es la operación denominada: test-and-set. Esta instrucción realiza de forma indivisible las siguientes acciones:
if indicador = false then indicador:=true;
Como vemos, son las acciones realizadas en los algoritmos cada vez que un proceso quiere bloquear un recurso. Primero se comprueba el indicador y si está libre se cierra para indicar que el proceso va a usar el recurso. Con esta instrucción disponible en los procesadores, se ofrecía a los lenguajes la posibilidad de usarla desde el código de alto nivel mediante una función de librería que devolvía verdadero si el indicador estaba libre y se había podido ocupar y falso si ya estaba ocupado. El ejemplo que veníamos desarrollando quedaría:
{------------------------------------------------------------}
{-- versión con cerrojos }
{------------------------------------------------------------}
program mecanismos_Version_cerrojos;
var x:Integer; { variable compartida }
ind:boolean; { indicador para proteger datos }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
while not test-and-set ( ind) do ; { bucle de espera }
{----------------------}
x:=x+1; { SC }
{----------------------}
ind:=false; { libero indicador }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
while not test-and-set ( ind) do ; { bucle de espera }
{----------------------}
x:=x-1; { SC }
{----------------------}
ind:=false; { libero indicador }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
init ( s,1,1); { inicializo semáforo, abierto, binario}
cobegin
Pr1; Pr2;
coend;
end. Sin embargo, esta solución aún tiene el problema de la espera activa. Para eliminar este problema es necesario una mayor sofisticación en el sistema operativo que no debe limitarse a permitir utilizar las instrucciones indivisibles del hardware sino que debe comprometerse con la implementación de la concurrencia añadiendo estados a los procesos que sirvan para conseguir espera no activa. Una vez conseguido esto tendremos mecanismos verdaderamente eficaces como los semáforos.

### 1.3.3 Semáforos

Esta es la primera solución completamente efectiva para obtener exclusión mutua sin ningún tipo de problema añadido. Se basa en las mismas ideas de los algoritmos, con un indicador que ahora se denomina semáforo pero que se implica en la gestión de procesos del sistema operativo y aporta como resultado tres procedimientos que permiten una gestión simple y flexible de los bloqueos. Es semáforo indicará si un cierto recurso al que se asocia está disponible o no,
estando abierto o cerrado. En el caso de sincronización indicará si la situación a la que sedebe esperar se ha producido o no. El funcionamiento de un semáforo se basa en la existencia de un nuevo estado paralos procesos, similar al estado bloqueado pero que implica un bloqueo voluntario. El motivo de que sea voluntario es que sería posible usar el recurso pero no correcto por tanto el bloqueo no es automático, el proceso debe darse cuenta de que no debe usar el recurso y solicitar el paso a bloqueo voluntario. La salida de este estado se produce cuando otro proceso reactiva al proceso bloqueado voluntario que pasa al estado listo para ejecutarse. El siguiente diagrama de estados incluye este nuevo estado:

*(diagrama de estados de proceso con los estados EJECUCIÓN, ESPERA, BLOQUEADO y el nuevo BLOQUEO VOLUNTARIO, y transiciones etiquetadas "Inicio ejecución", "Fin ejecución", "~CPU" y "~Recurso"; la disposición exacta de las flechas no se pudo recuperar de la extracción OCR)*

Figura 7.15: Diagrama actualizado de estados de procesos
El cambio a este nuevo estado, se produce de forma automática para el programador cuando se utilizan los procedimientos de gestión del semáforo. Por tanto, la forma de trabajo con un semáforo será doble:
- En el caso de que se requiera comunicación sincronizada el proceso que desea utilizar un recurso protegido comprobará el semáforo asociado antes de utilizarlo y si el semáforo está cerrado pasará a estado de bloqueo voluntario. Siel semáforo está abierto, el proceso lo cerrará y pasará a utilizar el recurso. Cuando el proceso termina de usar el recurso lo libera abriendo el semáforo, loque permite a otros procesos utilizarlo, bien a procesos en estado de bloqueo voluntario que serán despertados, bien a nuevos procesos que soliciten el usodel recurso.

*(diagrama con los procesos Pr1, Pr2 y Pr3 accediendo a un recurso protegido por un semáforo; la disposición exacta no se pudo recuperar de la extracción OCR)*

Figura 7.16: acceso a recurso protegido por semáforo
- Si se trata de sincronización pura, se utilizará un semáforo inicialmente cerrado que será abierto por el proceso que condiciona la ejecución de otro. El segundo proceso comprobará el semáforo en el momento preciso, continuando su ejecución si está abierto o pasando a estado bloqueado voluntario si está
cerrado, siendo reanudado cuando el otro proceso lo indique.

*(diagrama con los procesos Pr1 y Pr2 sincronizados mediante un semáforo; la disposición exacta no se pudo recuperar de la extracción OCR)*

Figura 7.17: Sincronización pura con semáforo
Para conseguir esto, el indicador de tipo semáforo, tiene una estructura interna compleja formada por dos elementos, un contador que indica el estado del semáforo y una lista de posibles procesos en estado de bloqueo voluntario por haber comprobado el semáforo y haberlo encontrado cerrado. Una posible representación de un semáforo en varios estados podría ser:

| | Estado 1 | Estado 2 | Estado 3 |
|---|---|---|---|
| CONTADOR | 1 | 0 | 0 |
| LISTA DE PROCESOS | — | — | PR1, PR3 |

Figura 7.18: Estructura de un semáforo
En esta representación tendríamos primero un semáforo abierto, sin procesos en estado de bloqueo, segundo un semáforo cerrado sin procesos esperando, y tercero, un semáforo cerrado con dos procesos en bloqueo a la espera de que sean activados por otro proceso que libere el semáforo.
Para implementar este comportamiento, vamos a incluir en nuestro lenguaje el tipo
“semaphore” que se corresponderá con una implementación de esta estructura de datos y conel comportamiento que hemos descrito. Utilizaremos palabras en inglés para crear todos los mecanismos. De esta forma,
siempre podremos distinguir lo que es palabra reservada de los identificadores que definamos en nuestros programas que siempre se crearán en español. Los semáforos definidos con este tipo, podrán ser de los dos tipos existentes,
binarios o señales y generales o con contador. La diferencia entre estos dos tipos es elrango de valores que puede tener el contador, 0 y 1 en los binarios y 0, 1, …, N en los generales. La diferenciación entre unos y otros se realiza en la inicialización. Más adelante veremos las diferencias de comportamiento entre los dos tipos. Para la utilización del semáforo, vamos a tener tres procedimientos que sirven para inicializar, comprobar-ocupar y liberar. Son los siguientes:
- init ( S, valor inicial, valor máximo): Establecer el valor inicial del contador de un semáforo y el valor máximo. El valor máximo establecerá el tipo de semáforo ( 1 binario, >1 con contador). Esta operación se debe realizar en un momento anterior a la fase de concurrencia donde va a utilizarse el semáforo. En los lenguajes de programación se obliga a utilizarlo en el programa principal como es nuestro caso ya que sólo se podrá usar en el programa principal y fuerade bloque “cobegin-coend”.
- wait ( S): Operación indivisible de consulta del estado del semáforo y cierre del mismo si está abierto. La forma de operar de este procedimiento es:
- Si el contador del semáforo es mayor que 0, se decrementa en uno.
- Si el contador es 0, entonces:
1º) Se añade el descriptor de proceso al final de la lista de procesos bloqueados del semáforo para que pueda ser despertado cuando el semáforo sea liberado.
2º) El proceso queda en estado “bloqueo voluntario”.
3º) El Sistema Operativo asigna el procesador a otro proceso.
- signal ( S): Operación indivisible que libera el semáforo, su modo de operación es el siguiente:
- Si el semáforo es binario y el contador es 1, no se realiza ninguna acción.
- Si el contador es mayor que 0 y el semáforo es general y el contador es = N
( máximo del contador), no se realiza ninguna acción.
- Si el contador es mayor que 0 y el semáforo es general y el contador es < N,
se incrementa en uno el contador.
- Si el contador es 0 ( tanto para binarios como generales), se hará:
1º) Si no hay procesos bloqueados en la lista asociada al semáforo, se incrementa en uno el contador.
2º) Si hay procesos bloqueados, se desbloquea el primero de la lista,
eliminando su descriptor de la misma. Como se puede observar, la operación de liberación del semáforo sólo desbloquearía un proceso, el primero que tuvo que esperar por el semáforo y quedó
bloqueado y con su descriptor en la lista del semáforo. Los valores de inicialización de un semáforo serán siempre [1..n] para el valor máximo ( nunca 0) y entre [0..máx] para el valor inicial. Un semáforo binario tiene dos estados, 1 abierto y 1 cerrado. Un semáforo general tiene 1 estado cerrado y n-1 estados de abierto. Veamos ahora el mismo ejemplo que hemos utilizado con los método algorítmicos resuelto mediante el uso de semáforos, en lo que sería un caso de comunicación sincronizada. En el código resultante tendremos la comprobación del semáforo en la fasede bloqueo previa a la sección crítica y la liberación del semáforo una vez terminada la sección crítica. En cuanto a la inicialización tendremos unos valores inicial y máximo iguales a uno que significan que el recurso no puede admitir más de un proceso trabajando simultáneamente y que inicialmente este recurso está libre. Esto es lógico porque la variable al inicio del programa no está siendo utilizada por nadie. Los semáforos para proteger recursos suelen inicializarse a valor >0 ya que al comienzo están libres. El código resultante es el siguiente:
{------------------------------------------------------------}
{-- versión sexta, con semáforos }
{------------------------------------------------------------}
program mecanismos_Version_6;
var x:Integer; { variable compartida }
s:Semaphore; { semáforo para proteger datos }
Procedure Pr1;
begin
writeln ('nada');
writeln ('nada');
writeln ('nada');
wait ( s); { compruebo semáforo }
{----------------------}
x:=x+1; { SC }
{----------------------}
signal ( s); { libero semáforo }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
wait ( s); { compruebo semáforo }
{----------------------}
x:=x-1; { SC }
{----------------------}
signal ( s); { libero semáforo }
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
init ( s,1,1); { inicializo semáforo, abierto, binario}
cobegin
Pr1; Pr2;
coend;
end. Tal y como se pretendía con la este mecanismo, no sólo tenemos todas las buenas características de los algoritmos más la ausencia de espera activa, además el bloqueo ydesbloqueo ha quedado totalmente simplificado. Este mecanismo también sirve para casos generales de sincronización. Por ejemplo,
el representado por el diagrama de precedencia no simétrico que sirve para ilustrar las limitaciones de la construcción “cobegin-coend”. En este caso el semáforo se utilizará enlos puntos origen y destino del arco no simétrico del diagrama. En nuestro caso en C y en D.

*(el diagrama de precedencia asimétrico referido en el texto no se pudo recuperar de la extracción OCR; sólo sobrevivió el pie de figura)*

Figura 7.19: Diagrama asimétrico con sincronización pura
En estos nodos implicados en la asimetría, liberaremos y comprobaremos el semáforo en los puntos origen y destino de la flecha respectivamente. Se tendrá en cuenta que las flechas saldrán después de ejecutado el nodo ( C) y llegarán antes de ejecutar el nodo
( D). La implementación con semáforos sería así:
{------------------------------------------------------------}
{-- semáforos para sincronización pura }
{------------------------------------------------------------}
program semaforos_sincronizacion_pura;
var s:Semaphore; { semáforo para proteger datos }
Procedure Pr1;
begin
B;
wait ( s); { compruebo semáforo = recibo señal }
D;
end;
Procedure Pr2;
begin
C;
signal ( s); { libero semáforo = envío señal }
E;
end;
begin init ( s,0,1); { inicializo semáforo, cerrado, binario}
A;
cobegin
Pr1; Pr2;
coend;
F;
end.
Los valores con que inicializamos el semáforo son 1 de máximo ( semáforo binario)
y 0 de valor inicial del contador que significa que empieza cerrado. Los semáforos utilizados para sincronización suelen empezar con valor inicial 0 yaque el evento que indican aún no puede haberse producido antes de empezar la ejecución concurrente. Los semáforos que hemos utilizado hasta ahora son binarios, ya que son los más utilizados, pero los semáforos generales también pueden ser de utilidad en ciertos casos.

#### 1.3.3.1 SEMÁFOROS GENERALES

Estos semáforos se caracterizan por tener n-1 estados en los que el semáforo está
abierto. Tienen utilidad tanto en situaciones de sincronización pura como de comunicación sincronizada pero en ambos casos, sólo cuando se dan ciertas condiciones especiales queson:
- Para el caso de comunicación sincronizada, el recurso que se protege con el semáforo debe ser capaz de admitir el uso simultáneo por varios procesos. Uncaso real de este tipo de recursos son las impresoras matriciales que disponen de varios carros de impresión y admiten la impresión simultánea sin mezcla ni problemas de hasta tres trabajos. En este caso, el semáforo tendrá valor máximo 3, para cada uno de los procesos que admite imprimiendo. Si tres procesos están el uso de la impresora, al haber realizado tres wait, el contador estará en 0. A medida que los procesos terminen y hagan signal el contador volverá a subir hasta 3 o nuevos procesos podrán hacer uso del recurso. Otro caso para el que son de utilidad estos semáforos en comunicación sincronizada es cuando se dispone de varios recursos iguales que forman una cierta unidad. Entonces se agrupan como un todo y se coloca un sólo semáforos general. Esto permite tener una gestión centralizada y una única cola lo que produce una optimización en los tiempos medios de espera acceso a los recursos.
- En el caso de sincronización pura, los semáforos generales, tienen la utilidad de permitir reunir o “resumir” conjuntos de n arcos en un sólo semáforo. Para permitir esto, vamos a contemplar tres situaciones que son cuando tenemos Nlíneas paralelas en el mismo sentido y sin ninguna otra línea que se entrecruce con ellas, cuando N líneas lleguen al mismo nodo o cuando N líneas partan del mismo nodo. En todos estos casos, utilizaremos un semáforo con contador yvalor máximo N que empezará cerrado y deberá tener tantos signal como wait.

*(tres diagramas, uno por cada situación descrita (N líneas paralelas, N líneas convergiendo en un nodo, N líneas partiendo de un nodo), mostrando el contador del semáforo general descendiendo de N=3 a 0 según se van produciendo las llamadas wait ( w) y signal ( s); la disposición exacta de las líneas y contadores no se pudo recuperar de la extracción OCR)*

Figura 7.20: Semáforos generales para sincronización
Como se puede apreciar en el diagrama, en el caso de un nodo que recibe o emite varias líneas, tendrá que realizar varias llamadas wait o signal. La diferencia o ventaja es que serán sobre el mismo semáforo ya que el orden no será relevante y se deberán recibir oemitir todas las señales para poder continuar con la ejecución correcta.

#### 1.3.3.2 PROBLEMAS CON LOS SEMÁFOROS

A pesar de la utilidad del mecanismo y sus buenas características, pasado un tiempo desde su creación, se detectaron una serie de problemas que se producían frecuentemente que son los siguientes:
- Se invertía la secuencia de llamadas al usar un semáforo para proteger un recurso:
signal ( s);
{ S. C. }
wait ( s);
Esto provocaba que se usase el recurso sin haber conseguido exclusión mutuay que una vez terminado el uso, en lugar de liberar el semáforo se bloquease, lo cual degradaba el sistema.
- Se confundía el nombre del semáforo a utilizar:
wait ( s_2);
{ S. C. }
signal ( s_1);
Esto provocaba que no se libere el semáforo lo que da lugar a un cierre del recurso para el resto de la ejecución del programa.
- Se confundía la operación a realizar tanto en comunicación sincronizada como en sincronización
wait ( s);
{ S. C. }
wait ( s);
Esto provocaba que no se libere el semáforo lo que da lugar a un cierre del recurso para el resto de la ejecución del programa, además de que el proceso que provoca el cierre se queda bloqueado en ese punto. En el caso se sincronización o no se recibía el envío y se producía bloqueo o se enviaba dos veces o no se esperaba. Estas pocas situaciones sirven para ilustrar el problema de fondo existente en los semáforos. Es un mecanismo eficaz y eficiente pero con un nivel de abstracción demasiado bajo para el desarrollo de aplicaciones comerciales. Por este motivo, su uso se limita al diseño de sistemas operativos y plataformas y se crean otros mecanismos de más fácil uso y mantenimiento en los que estos errores no son posibles, a cambio de perder una cierta flexibilidad.

### 1.3.4 Regiones críticas

La primera respuesta a los problemas detectados sobre los semáforos son las regiones críticas. Se trata de una idea muy sencilla consistente en añadir un nuevo tipo de bloque para incluir código. Este bloque va a servir para poner en su interior una sección crítica, etiquetarla con el recurso o variable sobre el que debe tener exclusión mutua y dejar que el compilador traduzca la construcción en el manejo de semáforos u otros mecanismos utilizados por el sistema operativo. No debemos confundir sección crítica ( segmento de código cualquiera que usa una variable compartida) con región crítica ( mecanismo para asegurar la exclusión mutua en la ejecución de una sección crítica sobre una variable compartida). Gracias a este mecanismo, se consigue que los programadores no cometan algunos de los errores comunes con semáforos, pero para asegurar que esto es así, es necesario obligar a que todo acceso a variable compartida se realice con la sintaxis de una región. La sintaxis a utilizar en la definición de las variables a compartir es la siguiente:
{ definición de variables compartidas }
var v_comp: shared integer; { toda variable llevará la palabra shared }
En cuanto a la sintaxis de creación de regiones críticas, sólo tendremos que poner:
region v_comp do { sección crítica que usa la variable v_comp };
Veamos la aplicación de este mecanismo sobre el ejemplo que venimos desarrollando para todas las soluciones:
{------------------------------------------------------------}
{-- versión séptima, con regiones críticas }
{------------------------------------------------------------}
program mecanismos_Version_7;
var x: shared integer; { variable compartida }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
region x do { abro una región }
{----------------------}
x:=x+1; { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
region x do { abro una región }
{----------------------}
x:=x+1; { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin x:=0;
cobegin
Pr1; Pr2;
coend;
end. La sencillez de esta versión es máxima comparada con todas las demás aunque alguna de las otras características del mecanismo no son tan favorables como veremos. Empezamos indicando que uso de este bloque está limitado a segmentos de código que tenga ejecución concurrente con otros.
La sección crítica contenida en una región crítica será una instrucción o un bloque rodeado de “begin-end”. El resto del trabajo necesario para asegurar la exclusión mutua en el uso de la variable que se usa para etiquetar la región será realizado por el compilador, pero si necesitamos crear una sección crítica que utiliza varias variables compartidas tendremos que anidar los bloques. Este anidamiento se realizará siguiendo las normas de la programación estructurada sin ninguna limitación adicional. Por ejemplo:
region v_comp do { región crítica principal }
begin v_comp:=5;
region v_comp_2 do { región crítica anidada }
v_comp_2:=v_comp+3; { puedo usar las dos variables }
v_comp:=0;
end;
Sin embargo, esto nos puede llevar a situaciones incorrectas por errores del programador como puede ser:
region v_comp do { región crítica principal }
region v_comp do { región crítica anidada sobre la mismav_comp }
v_comp:=3;
En este caso, hemos intentado anidar dos regiones sobre la misma variable, es unerror que puede ocurrir de forma menos visible si una región usa un procedimiento auxiliar que vuelve a abrir una nueva región. En este caso, el proceso se auto-bloquea ya que teniendo una región sobre una variable, la tenemos bloqueada, cualquier otro intento de creación de región sobre la misma variable, produce un bloque voluntario y paso a espera. Pero el bloqueo lo hace el proceso que tiene una región abierta y esto puede producir quela variable quede permanentemente bloqueada. También se puede dar una situación de bloqueo que será mutuo entre dos procesos si se codifica el acceso a dos recursos distintos en orden diferente como en este ejemplo proceso pr1 proceso pr2
region v_comp do region v_comp2 doregion v_comp2 do region v_comp do
Con esta codificación, se puede producir el caso en que los dos procesos lleguen simultáneamente al bloqueo del primer recurso y lo consigan, estando el segundo bloqueado en ambos casos. Este tipo de bloqueos se llama interbloqueo y se tratará más adelante en una sección especial. Además de estas situaciones, también tenemos el problema con las regiones derivado de que el mecanismo se creó para mejorar la comunicación sincronizada pero sin pensar en la sincronización pura. Como todo acceso debe realizarse con RC, el uso de semáforos no está permitido ( no tiene sentido aunque algunos lenguajes si lo permitan, escomo darte cubiertos y dejarte comer con las manos). Por todo esto, en las situaciones de sincronización, lo único que podemos hacer es utilizar una variable compartida y crear unbucle de comprobación con la espera activa que esto implica. Por ejemplo:
..
var x:shared boolean;
procedure Pr1;
begin
A;
region x do x:=true;
B;
end;
procedure Pr2;
var x_local:boolean;
begin
C;
repeat region x do x_local:=x;
until x_local;
D;
end;
{ principal }
begin
x:=false; { el indicador empieza cerrado }
cobegin
Pr1; Pr2;
coend;
end. Como podemos ver en el código, utilizamos una variable con valor inicial falso, quees puesta a verdadero por el proceso originario de la sincronización y es comprobada por el proceso destino en un bucle de espera activa. Es interesante destacar que el bucle de comprobación entra y sale continuamente de la R. C. Si esto no se hace así, el otro proceso no podría entrar nunca en R. C. para actualizar el valor del indicador. Es claro que no se puede admitir un mecanismo que no aporta una solución sin espera activa para la sincronización entre procesos, por este motivo se propuso una modificación a las regiones críticas.

### 1.3.5 RC Condicionales

Esta modificación implica la inclusión de una condición que se evalúa antes de entrar en una RC. En la condición se puede y debe incluir la variable compartida que seestá protegiendo de forma que la condición para ejecutar el contenido de la región esté
relacionado con una condición compartida, ya que la condición se puede modificar desde otros procesos modificando la variable compartida utilizada. La traducción a código PseudoPascal de esta idea es la siguiente:
region v_comp when v_comp>1 do { región crítica condicional}
v_comp:=3;
Y el funcionamiento:
- Si la variable compartida está en uso, no se podrán iniciar las tareas de la región quedando en estado bloqueado voluntario.
- Una vez que se puede acceder a la región y con la variable bloqueada se pasa aevaluar la condición.
- Si la expresión lógica usada como condición da verdadero se ejecuta la sección crítica asociada.
- Si la expresión lógica produce un valor falso, el proceso pasa a bloqueo voluntario y su descriptor se coloca en una cola especial diferente de la cola principal de acceso a la región.
- Los procesos en la cola especial de condición no cumplida sólo saldrán de ella cuando algún proceso consiga entrar en la región, su condición se cumpla yejecute su sección crítica. Cuando esto ocurre, la variable puede haber cambiado de valor y las condiciones que antes eran falsas pasar a verdaderas. Por este motivo, todos los procesos de la cola de condición pasan a la cola normal de acceso a la región para intentar entrar otra vez y volver a comprobar su condición. Este comportamiento permite evitar el bucle que comprobaba la condición continuamente con espera activa por una condición con bloqueo voluntario. Además, las condiciones son muy flexibles y permiten realizar expresiones complejas implicando varias variables compartidas si se anidan regiones críticas. El código del ejemplo anterior quedaría:
..
var x:shared boolean;
procedure Pr1;
begin
A;
region x when true do x:=true; { actualizo la variable}
B;
end;
procedure Pr2;
var x_local:boolean;
begin
C;
region x when x do ; { cuando la condición se cumple, no hacer nada
}
D;
end;
{ principal }
begin
x:=false; { el indicador empieza cerrado }
cobegin
Pr1; Pr2;
coend;
end. El código ha quedado simplificado y mucho más robusto, pero el mecanismo aún tiene algunas deficiencias, debido a que se ha planteado un mecanismo más flexible de lo necesario. En la mayoría de las ocasiones, la sincronización es tan sencilla como la que hemos visto en el ejemplo pero las condiciones hacen que sea preciso tener en cuenta detalles superfluos. Además, tenemos un problema de espera activa reducida, cuando un proceso cuya condición va a tardar mucho en cumplirse. Este proceso puede cambiar de cola muchas veces, comprobar su condición, entrar y salir de la región, para seguir esperando. Por último, las condiciones añaden otro problema consistente en que ahora tenemos más posibilidades de que se produzca un bloqueo indefinido como el siguiente:
proceso pr1 proceso pr2
region v_comp when ( a<0) do region v_comp when ( a>0) do
proceso pr1 proceso pr2
region v_comp when ( a>0) do region v when ( a>0) do
En este caso, la situación es similar, pero al ser la misma condición, lo que ocurre esque en lugar de dejar un caso pequeño sin contemplar se han dejado todos los números menores de 1, probablemente por un error de codificación.

### 1.3.6 RCC con Eventos

Esta segunda modificación de las regiones críticas, desarrolla la idea anterior,
integrando en la región un equivalente a los semáforos binarios para los casos de sincronización pura sencilla, teniendo las condiciones para situaciones más complejas o la región sencilla para la comunicación sincronizada. Esa modificación afecta, en primer lugar a la forma en que se etiquetan las variable como compartidas. Ahora, también será preciso definir los eventos en la definición de la variable. Esto tiene una implicación importante de uso, sólo se podrán usar los eventos enuna región sobre la variable donde se han definido. La sintaxis es:
{ definición de variables compartidas }
var v_comp: shared integer events e, ev1, mievento, mi_ev_4;
En la definición de los eventos se han utilizado identificadores elegidos por el programados que pasan a estar definidos. En cuanto a la sintaxis de creación de regiones críticas, no cambiará, pero ahora dispondremos de dos operaciones nuevas que sólo podrán utilizarse dentro de la región,
await y cause. Estas dos operaciones producirán y esperarán la llegada de eventos. La sintaxis a utilizar sería:
region v_comp when true do { región crítica que produce un evento }
cause ( mi_ev_4);
region v_comp when true do { región crítica que espera un evento }
await ( mi_ev_4);
El significado de await y cause es el mismo que en los semáforos binarios, la equivalencia es total, hasta el punto de que cada evento tiene su propia cola se espera específica para el evento. Además los eventos tienen memoria, un evento producido está ahí hasta que alguien lo consume y son binarios, si se producen dos cause seguidos, sólo se almacenará la recepción del evento como una unidad.
Para evitar confusión con el mecanismo semáforo, se han elegido palabras distintas para el envío y recepción de eventos. Las palabras se toman del inglés para seguir con la idea de separación entre palabras clave e identificadores en los programas. Rescribimos el código del ejemplo anterior quedaría:
..
var x:shared boolean events ev1;
procedure Pr1;
begin
A;
region x when true do cause ( ev1); { genero evento }
B;
end;
procedure Pr2;
var x_local:boolean;
begin
C;
region x when true do await ( ev1); { espero evento }
D;
end;
{ principal }
begin
x:=false; { el indicador empieza cerrado }
cobegin
Pr1; Pr2;
coend;
end. Con los eventos, el mecanismo RC queda completo, sin presentar ningún problemay con una sintaxis sencilla y bastante limpia, sin embargo, es un mecanismo poco implementado y que se puede considerar olvidado en los lenguajes actuales.

### 1.3.7 Monitores

Este es el último mecanismo que vamos a utilizar, es el más perfeccionado ypropone una estructura y comportamiento similar a de la programación orientada a objetos. Por este motivo, es el elegido en los lenguajes modernos que también son orientados a objetos como Java. Este modo de programar proporciona un mayor nivel de
 abstracción y es más cercano al pensamiento humano, permitiendo realizar mejores diseño se implementaciones. La propuesta consiste en evitar los problemas causados por tener que proteger las secciones críticas dispersas por el código reuniéndolas en el monitor al estilo O. O. donde se unen datos y métodos que manejan dichos datos. Por tanto, el resultado es una cápsula que contiene los datos compartidos, los métodos que los usan ( las secciones críticas modeladas como procedimientos) y una sección de inicialización que garantiza que el monitor parte de un estado coherente en sus datos compartidos.

*(diagrama de un monitor conteniendo las secciones críticas (SC) que antes estaban dispersas, junto a la variable ("var. comp.") y la sección de inicialización ("Inic."); la disposición exacta no se pudo recuperar de la extracción OCR)*

Figura 7.21: Incluir todas las SC en un monitor
El compilador generará el código necesario que asegure que no se ejecutan simultáneamente dos procedimientos incluidos dentro del mismo monitor y que esta exclusión mutua se realiza sin espera activa. El recurso compartido ( variable) incluido en un monitor no puede ser utilizado salvo por los procedimientos incluidos dentro del mismo monitor. Esto nos asegura que nose puede hacer mal uso del recurso. En PseudoPascal esto se va a traducir en una definición de tipo de datos donde se establece como es el monitor, según la siguiente sintaxis:

```
type nombre_tipo = monitor [(<parámetros de inicialización>)];
var
[procedure <nombre>[(<lista parámetros>)];
begin
{ procedimiento local }
end;]
procedure entry <nombre>[(<lista parámetros>)];
begin
{ procedimiento publico del monitor }
end;
begin { bloque de inicialización obligatorio }
}
end;
```

Donde tendremos las tres partes diferenciadas que hemos comentado, la definición de datos internos, delimitada por la palabra var, la definición de procedimientos que pueden ser internos u ofrecidos al exterior ( entry) y la sección de inicialización. Siempre tendremos algún procedimiento ofrecido al exterior, sin ellos el monitor no tendría sentido, pero podemos no tener procedimientos locales si no es necesario. Por último está la sección de inicialización cuyo end cierra el monitor y que asegura que el monitor parte de un estado
( estado del recurso protegido) coherente y que puede ser usado directamente. Los monitores sólo contienes procedimientos, no funciones. Si se desea devolver un valor en un monitor se utilizará un parámetro por referencia y se llamará al procedimiento con una variable para recibir la salida. En la sección de inicialización podremos usar los parámetros que hemos definido en la cabecera del monitor que servirá para poder crear varios monitores de este mismo tipo perocon distintos valores de partida. Los parámetros son opcionales y sólo sirven para ser usados en la sección de inicialización. Una vez que hemos definido el tipo monitor que vamos a utilizar, habrá de definir variables ( equivalente a instanciar objetos) de este tipo monitor. Estas variables serán compartidas para que todo proceso pueda utilizar el monitor.
var mon_1, moni_dos: nombre_tipo;
Aunque en este paso no se completaría la instanciación desde el punto de vista
O. O. ya que no se ha inicializado el monitor. Esto no ocurre hasta que no se hace uso de la instrucción ( no es un procedimiento) init que sirve para la inicialización explícita del monitor. La orden init se debe utilizar antes del bloque concurrente que utilice el monitor. Un ejemplo de uso podría ser:
begin
init mon_1; { inicializo monitor sin parámetros }
init moni_dos ( 1,2,’hola’); { inicializo monitor con parámetros }
end. Un monitor inicializado ya está listo para ser utilizado desde los procesos concurrentes. Para hacerlo se utilizará la notación punto, igual que en registros y objetos,
indicando la variable monitor a utilizar y el método seguido de los parámetros que sea preciso. Por ejemplo:
mon_1.proc_sin_parametros; { uso un procedimiento sin parámetros }
moni_dos.proc2 ( 1,2,’hola’); { uso un procedimiento con parámetros }
{------------------------------------------------------------}
{-- versión octava, con monitores }
{------------------------------------------------------------}
program mecanismos_Version_8;
type monx = monitor
var x: shared Integer; { variable compartida }
procedure mas;
begin x:=x+1;
end;
procedure menos;
begin x:=x-1;
end;
begin x:=0;
end;
var mx:monx; { instancio el monitor }
Procedure Pr1;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
{----------------------}
mx.menos (); { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
Procedure Pr2;
begin writeln ('nada');
writeln ('nada');
writeln ('nada');
{----------------------}
mx.mas (); { SC }
{----------------------}
writeln ('nada');
writeln ('nada');
writeln ('nada');
end;
begin init mx;
cobegin
Pr1; Pr2;
coend;
end. El resultado es un código muy limpio en los procesos concurrentes y con mayor nivel de abstracción ya que eligiendo bien los nombres de monitores y procedimientos, el código queda autocomentado. Por contra, la definición del monitor puede resultar algo engorrosa. La línea de ejecución de cada uno de los procesos es la que se representa en el siguiente diagrama:

*(diagrama de secuencia con Pr1 y Pr2 accediendo, en distintos momentos, a la sección crítica (SC) del monitor que encapsula la variable compartida ("v. comp.") en memoria; la disposición exacta no se pudo recuperar de la extracción OCR)*

Figura 7.22: Secuencia de ejecución de procesos que usan un monitor
En definitiva, tenemos un mecanismo de mayor nivel de abstracción que nos fuerzaa organizar el código y las ideas antes de programar y resultará el más productivo de cuantos hemos visto para crear programas de alto nivel. Sin embargo, nos sucede lo mismo que con las regiones críticas básicas, la sincronización pura no está contemplada y la única forma de conseguirla es desarrollando un algoritmo basado en un bucle de comprobación con espera activa. Veamos como debería escribirse este código:
..
type mo = monitor
var x:boolean;
procedure activa;
begin x:=true;
end;
procedure comprueba ( var a:boolean);
begin a:=x;
end;
begin x:=false; { inicializamos a cerrado }
end;
var mm:mo;
procedure Pr1;
begin
A;
mm.activa; { genero evento }
B;
end;
procedure Pr2;
var x_local:boolean;
begin
C;
repeat mm.comprueba ( x_local); { espero evento }
until x_local;
D;
end;
{ principal }
begin
init mm; { inicializa monitor que cierra el indicador }
cobegin
Pr1; Pr2;
coend;
end. Al igual que con las regiones críticas, el bucle debe implementarse fuera del monitor para evitar que éste quede bloqueado y el proceso que actualiza el valor de x pueda utilizarlo también.

### 1.3.8 Monitores con eventos

Esta es la solución del problema con los monitores que se plantea en los casos de sincronización pura. Se trata de añadir unos componentes iguales a los semáforos binarios como parte de los monitores. Es la misma solución adoptada en las RCCE pero adaptada ala sintaxis y condiciones de los monitores. Los eventos para los monitores serán binarios, con memoria y definidos en el interior del monitor de forma que sólo puedan ser usados en los procedimientos del interior del monitor. Dadas las similitudes, utilizaremos los mismos nombres que en el caso de las regiones criticas para simplificar y evitar confusiones. Para presentar la sintaxis retomamos el ejemplo de sincronización pura:
..
type mo = monitor
var eve:event;
procedure activa;
begin cause ( eve);
end;
procedure comprueba;
begin await ( eve);
end;
begin end;
var mm:mo;
procedure Pr1;
begin
A;
mm.activa; { genero evento }
B;
end;
procedure Pr2;
var x_local:boolean;
begin
C;
mm.comprueba; { espero evento }
D;
end;
{ principal }
begin
init mm; { inicializa monitor que cierra el indicador }
cobegin
Pr1; Pr2;
coend;
end.
La única cuestión pendiente es el comportamiento del monitor en el caso de que los procedimientos “entry” contengan otras instrucciones además de las relacionadas con la sincronización. En este caso, el proceso que ejecuta cause, no se verá afectado y seguirá consu ejecución hasta terminar su procedimiento, en cambio el que ejecuta await, si el evento seha producido ya, también continuará sin efecto, pero si el evento aún no se produjo pasará
a bloqueado voluntario y a la cola de este evento. Cuando el evento se produce pasará aesperar por el turno de entrada al monitor y cuando le corresponda, continuará la ejecución por la siguiente instrucción al await. Por último, reseñar que los eventos, abren la puerta a las situaciones de bloqueo indefinido con monitores ya que el programador puede confundir el orden de las llamadas o confundir el evento que debe utilizar. Estas situaciones, no controlables ni detectables por el compilador acaban siempre en situaciones de bloqueo indefinido del proceso mal codificado y en una degeneración general del sistema porque el resto de procesos acabarán esperando una señal que no llega nunca.

## 1.4 EL PROBLEMA DEL INTERBLOQUEO

Este problema afecta a varios mecanismos de los expuestos, en mayor medida cuanto menor es su nivel de abstracción, hasta llegar al punto de que en los monitores esmuy reducido. El problema se puede resumir en que se trata de una espera cruzada entre dos procesos. Cada uno espera a que el otro termine y libere un cierto recurso que necesita yestá bloqueado por el otro. Esta situación se puede alcanzar si el orden en que los procesos bloquean varios recursos es distinto. Si los bloqueos se hacen siempre en el mismo orden esta situación nose da. El problema es que cuando se definen los recursos no llevan un número asociado,
serán impresoras, discos o conexiones de Internet. Esto hace que cuando se programa el módulo encargado de la gestión de Internet, siempre se bloquee primero el recurso considerado importante como puede ser la conexión y luego otro secundario como eldisco. Lo mismo se hace en la gestión de impresoras con la impresora como principal y la conexión a Internet como secundario. Por último el módulo de gestión de disco, bloquea en primer lugar el disco y luego la impresora para imprimir un informe necesario. Esta situación lleva al interbloqueo si el bloqueo del primer recurso se produce de forma simultánea. El siguiente cronograma muestra esta situación:

*(cronograma de Pr1 y Pr2: cada uno consigue el bloqueo de un recurso (Rec1 y Rec2 respectivamente) y luego intenta bloquear el recurso que tiene el otro, quedando ambos bloqueados indefinidamente; la disposición exacta de los ejes no se pudo recuperar de la extracción OCR)*

Figura 7.23: Cronograma con interbloqueo
Esta situación se puede dar tanto en comunicación sincronizada como en sincronización pura aunque en la sincronización, es más difícil que se plantee una situación en la que el bloqueo se produzca salvo por error de codificación en algunos mecanismos. Analizando las distintas situaciones, llegamos a la conclusión de que los interbloqueos sólo serán posibles si se dar cuatro condiciones:
- Necesidad de exclusión mutua.
- Boqueo mientras se espera al resto de los recursos necesarios.
- No expropiación de recursos a un proceso bloqueado en espera de recursos.
- Espera circular donde cada proceso retiene un recurso y espera a otra retenido. Para evitar la existencia de estos bloqueos existen dos grandes enfoques, el de prevención ( prohibición) de los interbloqueos y el de reducción de los mismos. El enfoque de prevención consiste en evitar que se cumpla una de las cuatro condiciones necesarias para la existencia de interbloqueos. De entre las cuatro, la de exclusión mutua no se puede evitar ya que es necesaria, pero las demás sí. Por tanto,
tendremos un sistema que no admite la espera a un recurso reteniendo otros, o que permita que a un proceso en espera se le quiten los recursos que ya tuviera o que asegure la inexistencia de espera circular, dando un orden a cada recurso y asegurando que se pidenen orden. La prevención de interbloqueos en cualquier modalidad puede producir un bajo usoo rendimiento de los recursos. Por este motivo se plantea la reducción, consistente en evitar la mayoría de los bloqueos mediante diversos algoritmos y comprobar periódicamente si se ha producido un bloqueo, para deshacerlo. Esta forma de trabajar obtiene mejores rendimientos en general aunque los casos que sufren los bloqueos que hayque deshacer se vean penalizados.

### 1.4.1 Detección y eliminación de interbloqueos

Para la detección de los interbloqueos es necesario mantener permanentemente actualizada la información sobre las peticiones de recursos pendientes y sobre los recursos que están actualmente bloqueados. Con esta información se crea el grafo de asignación de recursos que resume esta información y permite la aplicación de algoritmos para determinar si existen o no ciclos. El grafo está compuesto por dos tipos de elementos, los procesos ( círculos) y los recursos ( cuadrados) y una serie de arcos dirigidos. Los arcos siempre irán desde un proceso a un recurso o al revés, nunca entre recursos o entre procesos. Un arco que va deun proceso a un recurso indica que ese proceso tiene solicitado un bloqueo sobre ese recurso pero aún no se le ha concedido. Si el arco va de un recurso a un proceso el proceso mantiene un bloqueo sobre dicho recurso. Un ejemplo de grafo de asignación es:

*(grafo con los nodos Pr1, Pr2, Pr3, Rec1 y Rec2; las flechas exactas no se pudieron recuperar de la extracción OCR, pero se describen a continuación en el texto)*

Figura 7.24: Grafo de asignación de recursos
En el grafo, “Pr1” quiere un bloqueo sobre el recurso “Rec1” que está bloqueado por “Pr3” que quiere también un bloqueo sobre “Rec2” que está bloqueado por “Pr2”. El algoritmo que permite detectar de forma automática los interbloqueos es muy sencillo. Consiste en realizar de forma repetida los dos pasos siguientes:
- Buscar todos los procesos que sólo tengan bloqueos realizados y ninguna petición de nuevos y eliminarlos del grafo, así como los arcos de sus bloqueos.
- Buscar todos los recursos que sólo tengan arcos de petición y eliminarlos del grafo, así como los arcos de sus peticiones. Si al repetir estos dos pasos sucesivamente llegamos a un grafo vacío, el sistema notenía interbloqueos.
Si al repetir los pasos, llegamos a una situación en la que en ninguno de los dos pasos eliminamos elementos y el grafo no es vacío, tenemos una situación de interbloqueo. El siguiente grafo presenta una situación de interbloqueo:

*(grafo con los nodos Pr1, Pr2, Pr3, Pr4, Rec1, Rec2 y Rec3; las flechas exactas no se pudieron recuperar de la extracción OCR, pero se describen a continuación en el texto)*

Figura 7.25: Grafo con interbloqueo
De forma intuitiva nos podemos dar cuenta de que si encontramos un camino que podamos seguir saltando en las direcciones de las flechas y es circular, el grafo tiene un interbloqueo. En nuestro caso, Pr3 tiene Rec1 y quiere Rec2 que lo tiene Pr4 que quiere
Rec3 que lo tiene Pr2 que quiere Rec1 y ya hemos cerrado un ciclo. Si en el sistema tuviésemos bloques de recursos que funcionan como una unidad,
podemos optar por una representación gráfica algo distinta en la que los bloques se representan como un recurso que tiene en su interior elementos. La Figura 7.26 presenta un grafo de este tipo. Los bloqueos existentes se marcan directamente sobre los subelementos mientras que los bloqueos solicitados sobre el grupo. La reducción a realizares similar ya que se van eliminando los procesos que tienen los bloqueos que necesitan ylos recursos con un número de elementos libres suficientes para el número de arcos que reciben del mismo proceso ( si recibe varios del mismo puede haber problemas, si no, no yaque atendería las peticiones secuencialmente). Una vez determinada una situación de interbloqueo, es preciso deshacerla. Para conseguir esto existen varios enfoques, consistentes en reiniciar procesos bloqueados loque permite que sus recursos queden libres o expropiar recursos de algunos procesos bloqueados. Ambas técnicas presentan sus problemas, porque el trabajo de ciertos procesos no se podrá reiniciar al ser cambios consolidados y ciertos recursos no podrán ser expropiados como las impresoras porque las impresiones se podrían mezclar.
*(grafo con los nodos Pr1, Pr2, Pr3 y Pr4 y un recurso central con dos elementos; las flechas exactas no se pudieron recuperar de la extracción OCR)*

Figura 7.26: Grafo con recursos de múltiples elementos
Este grafo tiene las mismas líneas y procesos que el anterior, pero hay un recurso más. El bloque central tiene dos recursos, luego El proceso Pr3 podrá obtener el recurso que necesita y terminará dejando libre el primer recurso que podrá ser usado por Pr1 y Pr2
que también se eliminan liberando el tercer recurso que permite terminar a Pr4.

## 1.5 CONCLUSIONES

Revisando los mecanismos hemos visto que su utilización que permite un uso seguro de la concurrencia de memoria única, es sencilla y eficaz. Por otro lado sabemos que la PMU está muy extendida y ha demostrado su utilidad,
mejorando el rendimiento de los sistemas, ofreciendo al usuario interfaces más agradables yflexibles con un mayor tiempo de disponibilidad y mayor comodidad. Por último, en las situaciones que así lo requieren se dispone de mayor potencia de cálculo a un precio muy asequible por la compartición de recursos. Finalmente, sólo queda reseñar que en las situación actual, de los mecanismos de
PMU se utilizan tan sólo los monitores y semáforos. Unos en lenguajes de alto nivel y otrosen lenguajes de bajo nivel o programación de sistemas operativos.

## 1.6 EJEMPLOS Y EJERCICIOS

En este apartado incluiremos todos los ejemplos posibles que ilustren en funcionamiento de los distintos mecanismos, así como ejercicios de repaso. En la sección de ejemplos, vamos a incluir un método para desarrollar los programas concurrentes equivalentes a un diagrama de precedencia.

### 1.6.1 Ejemplos

1) Ejemplo de seguimiento de la evolución de un semáforo utilizado por cuatro procesos para proteger el acceso a un recurso.

*(diagrama con los procesos Pr1, Pr2, Pr3 y Pr4 accediendo a un recurso protegido por semáforo; la disposición exacta no se pudo recuperar de la extracción OCR)*

Empezamos con el semáforo a uno y el recurso libre, es el estado ( a), luego el proceso Pr2 solicita el recurso usando el semáforo que queda cerrado, es el estado ( b). Después, los procesos Pr1 y Pr3 solicitan usar el recurso comprobando el semáforo que está en uso, quedando bloqueados ( c).

| | Estado (a) | Estado (b) | Estado (c) |
|---|---|---|---|
| CONTADOR | 1 | 0 | 0 |
| LISTA DE PROCESOS | — | — | PR1, PR3 |

Desde este estado, tenemos que Pr2 termina y libera el semáforo, cuyo contador no cambia pero que deja pasar a Pr1 ( d). Cuando éste termina ocurre igual y pasa Pr3 ( e) y cuando Pr3 termina el semáforo queda abierto porque nadie está usando el recurso y nadie lo ha solicitado ( f).

| | Estado (d) | Estado (e) | Estado (f) |
|---|---|---|---|
| CONTADOR | 0 | 0 | 1 |
| LISTA DE PROCESOS | PR3 | — | — |
2) Método de transformación de diagramas de precedencia en programas
PseudoPascal. El método que presentamos consta de una serie de fases muy sencillas que nos aseguran la traducción de los diagramas a programas y se utilizará en los ejemplos y ejercicios posteriores. Los pasos a realizar son:
- Se reordena, gira o invierte el diagrama para que se ajuste más convenientemente a la visón del programador.
- Se eliminan las redundancias del diagrama que se consideren oportunas. En algunos casos no se eliminarán todas las posibles para mejorar los resultados del siguiente paso. Y en otras este paso no existirá porque se dará un diagrama ya particionado en procesos.
- Se decidirá una partición de los nodos en procesos,
estableciendo grupos que tengan una secuencialidad interna claray si tuvieran concurrencia interna, que esta esté relacionada con alguno de los nodos con un arco ( no incluir nodos sueltos). La partición en procesos es importante porque toda línea que forme parte de la secuencialidad interna del proceso no podrá
ser eliminada aunque sea redundante pero su implementación no requerirá trabajo especial.
- Se etiquetarán los nodos con los recursos compartidos que se utilizan en dichos nodos, se entenderá que todo el nodo es una sección crítica sobre ese recurso. De no serlo, se descompondrá
el nodo en una secuencia de nodos de forma que finalmente quede un nodo como sección crítica total sobre el recurso.
- Se repetirá la fase de eliminación de redundancias teniendo en cuenta que no se eliminará la secuencialidad interna de los procesos.
- Se etiquetará cada uno de los arcos que crucen entre procesos para su implementación con los mecanismos existentes.
- Se tomarán las decisiones dependientes del mecanismo a utilizar,
sobre todo con los semáforos que pueden ser generales ypermitir reducir el número de ellos.
- Se creará el programa en PseudoPascal. En la fase de creación del programa, realizaremos las siguientes tareas:
- Escribiremos el esqueleto del programa, formado por la cabecera, el programa principal, con la sección de ejecución concurrente y espacio para variables compartidas,
procedimientos para cada proceso y fase de inicialización del mecanismo a utilizar.
- Definiremos las variables compartidas establecidas en el enunciado o determinadas por el análisis del problema. Estableceremos tipos de datos y seguiremos las normas que el mecanismo a utilizar en la implementación nos requiera.
- Definiremos los mecanismos de sincronización y comunicación sincronizada necesarios.
- Inicializaremos los mecanismos en el cuerpo del programa principal.
- Implementaremos los procedimientos, empezando por escribirlos nodos de proceso como si fuesen llamadas a procedimientos del nombre indicado, cuya implementación no es de interés y se considera realizada ( salvo que se indique lo contrario).
- Implementaremos los procedimientos, rodeando los nodos de proceso que sean sección crítica con las fases de bloqueo ydesbloqueo según dicte el mecanismo utilizado.
- Implementaremos los procedimientos, añadiendo las llamadas que permitan la recepción y envío de los arcos de sincronización incluidos en el diagrama y etiquetados anteriormente. Para la fase de implementación es interesante considerar que cada nodo está
precedido de un bloque de código anterior y otro posterior y que en el anterior es donde se incluye todo lo relacionado con la recepción de arcosde sincronización y en el posterior todo lo relacionado con la emisión dearcos. El siguiente diagrama muestra esta idea sobre un nodo implementándolo con semáforos.

*(esquema de un nodo genérico: antes del nodo, esperas de sincronización (wait(s1), wait(s5)) y de exclusión mutua sobre la variable V1 (wait(S_V1)); el nodo en sí; después del nodo, liberación de la exclusión mutua (signal(S_V1)) y señales de sincronización (signal(s3), signal(s7)); la disposición exacta no se pudo recuperar de la extracción OCR)*

Vamos a aplicar el método sobre el ejemplo primero que nos planteó la necesidad de los mecanismos de sincronización. Utilizaremos semáforos para su realización en PseudoPascal y consideraremos que los nodos B y C son secciones críticas sobre la variable V1 y los nodos D y E sobre la variable V2:

*(diagrama de precedencia con los nodos A, B, C, D, E y F; la disposición exacta de las flechas no se pudo recuperar de la extracción OCR)*

Etiquetamos el diagrama con toda la información y establecemos una partición en procesos conveniente, especialmente porque aunque no ahorramos líneas de precedencia entre procesos, dos de ellas se pueden representar con el mismo semáforo ( general) por ser paralelas y entre los mismos procesos.

*(mismo diagrama etiquetado con la partición en dos procesos, Pr1 (nodos B y D) y Pr2 (nodos A, C, E y F), las variables compartidas V1 y V2, y los semáforos de sincronización s1 y s2 sobre los arcos entre procesos; la disposición exacta no se pudo recuperar de la extracción OCR)*

El código resultante es:
program ejemplo_2;
var V1:T1; { variable compartida }
V2:T2; { variable compartida }
s1,s2,s_V1,s_V2:Semaphore; { semáforos }
Procedure Pr1;
begin
{----------------nodo B-----------}
wait ( s1); { sincronización antes de B }
wait ( s_V1); { exclusión mutua en acceso a V1 }
B; { SC sobre V1 }
signal ( s_V1); { libero recurso V1 }
signal ( s2); { sincronización después de B }
{----------------nodo D-----------}
{ nada antes de D }
wait ( s_V2); { exclusión mutua en acceso a V2 }
D; { SC sobre V2 }
signal ( s_V2); { libero recurso V2 }
signal ( s2); { sincronización después de D }
end;
Procedure Pr2;
begin
{----------------nodo A-----------}
{ nada antes de A }
A;
signal ( s1); { sincronización después de A }
{----------------nodo C-----------}
{ nada antes de C }
wait ( s_V1); { exclusión mutua en acceso a V1 }
C; { SC sobre V1 }
signal ( s_V1); { libero recurso V1 }
{ nada después de C }
{----------------nodo E-----------}
wait ( s2); { sincronización antes de E }
wait ( s_V2); { exclusión mutua en acceso a V2 }
E; { SC sobre V2 }
signal ( s_V2); { libero recurso V2 }
{ nada después de E }
{----------------nodo F-----------}
wait ( s2); { sincronización antes de F }
F;
{ nada después de F }
end;
begin init ( s1,0,1); { inicializo semáforo, cerrado, binario}
init ( s2,0,2); { inicializo semáforo, cerrado, general ( n=2)}
init ( s_V1,1,1); { inicializo semáforo, abierto, binario}
init ( s_V2,1,1); { inicializo semáforo, abierto, binario}
cobegin
Pr1; Pr2;
coend;
end. Por último, observamos cómo se ha creado una estructura en el código similar al diagrama de precedencia. La extracción OCR presentaba el código de Pr1 y Pr2 a dos columnas lado a lado, reconstruidas aquí una a continuación de la otra (el nodo F, presente sólo en el original arriba como "F;", apareció con una "E" en esta segunda copia, corregido aquí por comparación con la versión anterior):

```
Procedure Pr2;
begin
    {----------------nodo A-----------}
    { nada antes de A }
    A;
    signal ( s1); { sincronización después de A }
    {----------------nodo C-----------}
    { nada antes de C }
    wait ( s_V1); { exclusión mutua en acceso a V1 }
    C; { SC sobre V1 }
    signal ( s_V1); { libero recurso V1 }
    { nada después de C }
    {----------------nodo E-----------}
    wait ( s2); { sincronización antes de E }
    wait ( s_V2); { exclusión mutua en acceso a V2 }
    E; { SC sobre V2 }
    signal ( s_V2); { libero recurso V2 }
    { nada después de E }
end;

Procedure Pr1;
begin
    {----------------nodo B-----------}
    wait ( s1); { sincronización antes de B }
    wait ( s_V1); { exclusión mutua en acceso a V1 }
    B; { SC sobre V1 }
    signal ( s_V1); { libero recurso V1 }
    signal ( s2); { sincronización después de B }
    {----------------nodo D-----------}
    { nada antes de D }
    wait ( s_V2); { exclusión mutua en acceso a V2 }
    D; { SC sobre V2 }
    signal ( s_V2); { libero recurso V2 }
    signal ( s2); { sincronización después de D }
    {----------------nodo F-----------}
    wait ( s2); { sincronización antes de F }
    F;
    { nada después de F }
end;

```

3) Vamos a realiza ahora una modificación en la partición de procesos que no resulta muy útil en general pero es interesante conocer. Supongamos la siguiente partición:

*(mismo diagrama de precedencia con los nodos A, B, C, D, E y F, particionado ahora de forma distinta en dos procesos; la disposición exacta no se pudo recuperar de la extracción OCR)*

En este caso, uno de los procesos mantiene en su interior, concurrencia. Estose implementará incluyendo en su código un bloque cobegin-coend, aunque en realidad se debería realizar de forma recursiva todos los pasos para este proceso como si fuese un nuevo diagrama completo. El código resultante es:
program ejemplo_3;
var s1,s2:Semaphore; { semáforos }
Procedure Pr1;
begin
{----------------nodo B-----------}
wait ( s1);
B;
signal ( s2);
end;
Procedure Pr2;
begin
{----------------nodo A-----------}
A;
signal ( s1);
{----------------nodo C-----------}
C;
{=========== Inicio bloque concurrente interno }
cobegin begin {----------------nodo D-----------}
wait ( s2);
D;
end;
begin {----------------nodo E-----------}
E;
end;
coend;
{=========== Fin bloque concurrente interno }
{----------------nodo F-----------}
F;
end;
begin init ( s1,0,1); { inicializo semáforo, cerrado, binario}
init ( s2,0,1); { inicializo semáforo, cerrado, binario}
cobegin
Pr1; Pr2;
coend;
end. Para implementar los nodos D y E hace falta “begin-end” en torno a D porque sino,
el wait no sería recibido por D, se ejecutaría en paralelo con D y E, pudiendo terminar, antes, después o a la vez que ellos.
4) Escribir el programa de PMU que sea equivalente al siguiente diagrama de precedencia, utilizando semáforos, RCC con eventos y monitores con eventos.

*(diagrama de precedencia con los nodos A, B, C, D y E; la disposición exacta no se pudo recuperar de la extracción OCR)*

Primero etiqueto y particiono:

*(mismo diagrama particionado en dos procesos, Pr1 (nodos A, B y D) y Pr2 (nodos C y E), con los semáforos de sincronización e1 y e2 sobre los arcos entre procesos; la disposición exacta no se pudo recuperar de la extracción OCR)*

Ahora codifico con semáforos:
program ejemplo_4_semaforos;
var e1,e2:Semaphore; { semáforos de sincronización }
Procedure Pr1;
begin
{----------------nodo A-----------}
A;
signal ( e1);
{----------------nodo B-----------}
B;
{----------------nodo D-----------}
wait ( e2);
D;
end;
Procedure Pr2;
begin
{----------------nodo C-----------}
wait ( e1);
C;
signal ( e2);
{----------------nodo E-----------}
E;
end;
begin init ( e1,0,1); { inicializo semáforo, cerrado, binario }
init ( e2,0,1); { inicializo semáforo, cerrado, binario }
cobegin
Pr1; Pr2;
coend;
end. Ahora codifico con regiones críticas con eventos:
program ejemplo_4_RCCE;
var
{ creo una variable que no uso para nada salvo añadir los eventos}
nada: shared boolean events e1,e2;
Procedure Pr1;
begin
{----------------nodo A-----------}
A;
region nada when true do cause ( e1);
{----------------nodo B-----------}
B;
{----------------nodo D-----------}
region nada when true do await ( e2);
D;
end;
Procedure Pr2;
begin
{----------------nodo C-----------}
region nada when true do await ( e1);
C;
region nada when true do cause ( e2);
{----------------nodo E-----------}
E;
end;
begin cobegin
Pr1; Pr2;
coend;
end. Ahora codifico con monitores con eventos:
program ejemplo_4_monitores_eventos;
type mm = monitor
var e:array [1..2] of events;
procedure espera ( a:integer);
begin await ( e[a]);
end;
procedure genera ( a:integer);
begin cause ( e[a]);
end;
begin end; {---- fin del monitor ----}
var nada:mm;
Procedure Pr1;
begin
{----------------nodo A-----------}
A;
nada.genera ( 1);
{----------------nodo B-----------}
B;
{----------------nodo D-----------}
nada.espera ( 2);
region nada when true do await ( e2);
D;
end;
Procedure Pr2;
begin
{----------------nodo C-----------}
nada.espera ( 1);
C;
nada.genera ( 2);
{----------------nodo E-----------}
E;
end;
begin cobegin
Pr1; Pr2;
coend;
end.
5) Además de estas situaciones abstractas, que nos sirven para mejorar el manejo de los mecanismos, existen muchos planteamientos de problemas que plantean una situación real. En estos problemas, nos encontramos con un enunciado en lenguaje natural que no indica el orden de tareas ni la descomposición de las mismas. Por ejemplo el siguiente: “tenemos una patio de juego lleno de niñosen el que no estaba previsto que hubiese tantos, por este motivo, sólo hay tres columpios de uso individual y un muñeco también de uso individual. En elpatio hay 10 niños en el momento actual. Cada niño juega en un columpio yluego juega con el muñeco, repitiendo este ciclo de forma indefinida yesperando cuando el juego que quiere usar está ocupado. Realizar un programa concurrente PMU que represente el comportamiento de este sistema”
Cuando tenemos este tipo de enunciados es interesante intentar crear el diagrama de precedencia, pero para ello es mejor detectar primero que elementos son activos
( procesos) y cuales pasivos ( recursos). En nuestro enunciado se ve claramente que los recursos son los tres columpios yque los procesos son los niños que desean jugar con los recursos. En un diagrama de procesos y recursos tendríamos:

*(diagrama con los recursos Muñeco y Columpios y los procesos Niño1, Niño2, ..., Niño10; la disposición exacta no se pudo recuperar de la extracción OCR)*

Por tanto, se trataría de crear un diagrama de precedencia que tuviese los nodos decada uno de los procesos y los arcos correspondientes. Para hacer esto, empezamos poruno de los procesos y vemos que sus nodos se corresponderían con un primer nodo previoa utilizar ningún recurso, luego un nodo que representa el uso del columpio, otro que representa el uso del muñeco, y luego una repetición de estos dos últimos nodos. Hay que tener en cuenta que los nodos de uso de elementos son secciones críticas sobre dichos elementos. El diagrama para un proceso sería:

*(diagrama de precedencia secuencial: "Antes" → "Uso columpio" → "Uso muñeco", repitiéndose los dos últimos nodos indefinidamente)*

Por tanto el diagrama general sería la misma idea repetida para los 10 procesos yaque no hay sincronización, sólo comunicación sincronizada por el uso de los recursos quese comparten. A la hora de implementar el programa, vamos a considerar que los tres columpios son un recurso con capacidad tres y vamos a utilizar semáforos, el programa quedaría:
program ejemplo_5_semaforos;
var columpio,muneco:Semaphore; { semáforos de recursos }
Procedure Nino1;
begin
Antes;
repeat wait ( columpio);
UsoColumpio;
signal ( columpio);
wait ( muneco);
UsoMuneco;
signal ( muneco);
until false;
end;
Procedure Nino2;
begin
Antes;
repeat wait ( columpio);
UsoColumpio;
signal ( columpio);
wait ( muneco);
UsoMuneco;
signal ( muneco);
until false;
end;
begin init ( columpio,3,3); { inicializo semáforo, libre, general N=3 }
init ( muneco,1,1); { inicializo semáforo, libre, binario }
cobegin
Nino1; Nino2; Nino3; Nino4; Nino5; Nino6; Nino7; Nino8; Nino9;
Nino10;
coend;
end.
6) En el ejemplo anterior, hemos trabajado con recursos y procesos ficticios y el programa ha quedado un poco desvirtuado. Vamos a cambiar ahora por una situación algo más realista y pondremos como recursos 3 impresoras y una conexión a Internet. Todo el análisis es igual, pero ahora la implementación toma más sentido:
program ejemplo_6_semaforos;
type
imp=record
DirIP:String;
Tipo:integer;
Libre:boolean;
end;
var conexion, impresoras:Semaphore; { semáforos de recursos }
imp:array [1..3] of imp;
Procedure InicImpresoras;
var i:integer;
begin for i:=1 to 3 do begin imp[i]. DipIP := ’127.0.0.1’;
imp[i]. Tipo := ’laser’;
imp[i]. Libre := true;
end;
end;
Function ImpLibre ():integer;
var i:integer;
begin for i:=1 to 3 do begin if imp[i].libre then ImpLibre:=i end;
end;
Procedure UsoImpresoras;
begin numImpre:=ImpLibre; { se que hay una libre pero no se cual }
imp[numImpre]:=false; { la pongo a ocupada }
{ uso la impresora }
imp[numImpre]:=false; { la libero }
end;
Procedure UsoConexion;
begin
{ uso la conexión }
end;
Procedure Proceso1;
begin
Antes;
repeat wait ( impresoras);
UsoImpresoras;
signal ( impresoras);
wait ( conexion);
UsoConexion;
signal ( conexion);
until false;
end;
Procedure Proceso2;
begin
Antes;
repeat wait ( impresoras);
UsoImpresoras;
signal ( impresoras);
wait ( conexion);
UsoConexion;
signal ( conexion);
until false;
end;
begin init ( impresoras,3,3); { inicializo semáforo, libre, general N=3 }
init ( conexion,1,1); { inicializo semáforo, libre, binario }
InicImpresoras; { inicializo el recurso }
cobegin
Proceso1; ... Proceso10;
coend;
end. En esta solución hemos implementado un aspecto que había quedado pendiente respecto a la gestión de este recurso triple que son las impresoras ya que no podemos suponer que las mismas impresoras gestionan el reparto del trabajo, hay que registrar lasque están ocupadas y libres. En un programa más real, también habría que inicializar las impresoras y la conexión a Internet, además de utilizar ambas realmente y establecer una gestión de errores para todas las posibles situaciones de desconexión con impresoras e
Internet. Sin embargo, hay una cuestión que ha quedado mal resuelta, ya que cuando accedemos al recurso que es un conjunto de impresoras, hemos admitido que varios procesos lo hagan a la vez y lo modificamos, pero esta modificación se hace realmente sobre una variable compartida que no puede ser manejada por tres procesos a la vez. Siesto quedase así podría ocurrir que varios procesos seleccionasen la misma impresora para trabajar. Hay que cambiar el programa así:
program ejemplo_6_semaforos;
type imp=record
DirIP:String;
Tipo:integer;
Libre:boolean;
end;
var conexion, impresoras, impres_dat:Semaphore; { semáforos de recursos
}
imp:array [1..3] of imp;
Procedure InicImpresoras;
var i:integer;
begin for i:=1 to 3 do begin imp[i]. DipIP := ’127.0.0.1’;
imp[i]. Tipo := ’laser’;
imp[i]. Libre := true;
end;
end;
Function ImpLibre ():integer;
var i:integer;
begin for i:=1 to 3 do begin if imp[i].libre then ImpLibre:=i end;
end;
Procedure UsoImpresoras;
begin wait ( impres_dat);
numImpre:=ImpLibre; { se que hay una libre pero no se cual }
imp[numImpre]:=false; { la pongo a ocupada }
signal ( impres_dat);
{ uso la impresora }
wait ( impres_dat);
imp[numImpre]:=false; { la libero }
signal ( impres_dat);
end;
Procedure UsoConexion;
begin
{ uso la conexión }
end;
Procedure Proceso1;
begin
Antes;
repeat wait ( impresoras);
UsoImpresoras;
signal ( impresoras);
wait ( conexion);
UsoConexion;
signal ( conexion);
until false;
end;
Procedure Proceso2;
begin
Antes;
repeat wait ( impresoras);
UsoImpresoras;
signal ( impresoras);
wait ( conexion);
UsoConexion;
signal ( conexion);
until false;
end;
begin init ( impresoras,3,3); { inicializo semáforo, libre, general N=3 }
init ( impres_dat,1,1); { inicializo semáforo, libre, binario }
init ( conexion,1,1); { inicializo semáforo, libre, binario }
InicImpresoras; { inicializo el recurso }
cobegin
Proceso1; ... Proceso10;
coend;
end. Ahora no habrá problemas, ya que cada proceso antes de usar una impresora comprueba que hay libres mediante el semáforo general, y luego vuelve a comprobar un semáforo para evitar colisión en la consulta y actualización de la estructura de datos que controla las impresoras.

### 1.6.2 Ejercicios

1) Implementar en PseudoPascal con semáforos las dos particiones sobreel diagrama hexagonal asimétrico. Se asume que no hay variables compartidas en uso.

*(dos particiones del diagrama de precedencia hexagonal con los nodos A, B, C, D, E y F; la disposición exacta no se pudo recuperar de la extracción OCR)*

2) Desarrollar el programa PseudoPascal equivalente a los siguientes diagramas de precedencia, utilizando semáforos, RC, RCC, RCCE, monitores y monitores con eventos. ( sin variables compartidas para datos)

*(varios diagramas de precedencia con los nodos A, B, C, D, E, F, G, H e I; la disposición exacta no se pudo recuperar de la extracción OCR)*

3) Realiza el programa PseudoPascal equivalente a los siguientes diagramas de precedencia, particiones distintas del mismo diagrama original. Considerando que se utiliza la variable compartida V1 en los nodos E, B, G e I; la variable compartida V2 en F, C e I y la variable compartida V3 en B, C y F.
4) Desarrollar el programa PseudoPascal equivalente al siguiente diagrama de precedencia, utilizando semáforos, RC, RCC, RCCE, monitores y monitores con eventos. Para hacerlo se considerarán las tres particiones en procesos quese proponen y se desarrollarán todas las versiones. ( sin uso de variables compartidas para datos)
*(diagrama de precedencia con los nodos A, B, C, D, E, F, G, H e I, y tres particiones distintas del mismo diagrama en procesos; la disposición exacta no se pudo recuperar de la extracción OCR)*

5) ¿Cual de las particiones propuestas es mejor? Razone su respuesta indicando los aspectos tenidos en cuenta para valorar cada partición.
6) Realiza el programa PseudoPascal equivalente a los siguientes diagramas de precedencia, particiones distintas del mismo diagrama original. Considerando que se utiliza la variable compartida V1 en los nodos E, B, G e I; la variable compartida V2 en F, C e I y la variable compartida V3 en B, C y F.
*(tres particiones distintas del mismo diagrama de precedencia con los nodos A, B, C, D, E, F, G, H e I; la disposición exacta no se pudo recuperar de la extracción OCR)*

7) Razone sobre la conveniencia de haber utilizado una de las tres particiones enel ejercicio anterior. ¿Hay particiones mejores según el mecanismo utilizado?.
8) Analice, particiones e implemente el siguiente diagrama de precedencia utilizando los mecanismos que considere más eficientes. Justifique su elección de mecanismo.

*(diagrama de precedencia con los nodos A, B, C, D, F, G y H; la disposición exacta no se pudo recuperar de la extracción OCR)*

9) Crear un monitor que implemente el funcionamiento y operaciones de un semáforo binario, incluyendo la inicialización.
10) En una organización bancaria, tenemos n procesos que realizan transferencias. Cada proceso recibe tres datos, cantidad a transferir, cuenta origen y cuenta destino. Si cada cuenta tiene asociado un semáforo binario para
su bloqueo y uso exclusivo, ¿podemos tener interbloqueo? ¿en que circunstancias? ¿cómo se puede prevenir ( prohibir) la posibilidad de interbloqueos.
11) Crear el grafo de precedencia y detectar si existen bloqueos para las siguientes situaciones ( los procesos se identifican por números y los recursos por letras):
a) [1 quiere a, b, c] [2 quiere c] [3 quiere a, b, c]
[4 quiere b] [2 tiene b] [4 tiene c]
b) [1 quiere a] [2 quiere b] [3 quiere c] [4 quiere e]
[1 tiene d] [2 tiene e] [3 tiene f] [4 tiene a,b,c]
c) [1 quiere a] [2 quiere b] [3 quiere a] [4 quiere a,d] [5 quiere c] [6 quiere d]
[2 tiene a] [3 tiene b] [6 tiene c]
12) Crear un grafo de precedencia en el que haya 5 recursos, 5 procesos y 7
líneas de solicitud de recurso y 4 líneas de bloqueo de recurso. ¿es posible obtener un grafo sin interbloqueo? ¿porqué?
13) Crear un programa con un comportamiento como el propuesto por el problema de los filósofos. En este problema tenemos n filósofos que tiene dos actividades que realizan una tras otra de forma repetida que son comer un pensar. Para pensar no necesitan recursos pero para comer sí. Los recursos disponibles son n platos en una mesa redonda y n palillos, colocados entre cada dos platos. Para comer, un filósofo coge siempre el palillo derecho y luegoel izquierdo. Resolver el problema asegurando que no hay interbloqueos. Utilizar un número concreto de filósofos. Implementar la solución usando todos los mecanismos posibles ( cada mecanismo en un programa distinto.
14) Crear una solución nueva para el problema de los filósofos suponiendo que n/2 toman primero el derecho y luego el izquierdo y n-( n/2) toman primero el izquierdo y luego el derecho.
15) ¿Qué ocurre con el problema de los filósofos si los filósofos eligen al azarel primer palillo que cogen?
