---
title: "Programación concurrente en Java"
---

# 4. Concurrencia de memoria común en Java

## 4.1 INTRODUCCIÓN

### 4.1.1 Historia de la concurrencia

Los sistemas operativos han evolucionado hasta permitir la ejecución de más de un programa de forma simultánea, en procesos individuales, aislados a los que el sistema operativo les asigna los recursos ( memoria, descriptores de archivo, etc.). Los procesos pueden comunicarse con los demás procesos si fuera necesario a través de los mecanismos de comunicación que proporciona el sistema operativo: sockets,
manejadores de señales, memoria compartida, semáforos y archivos.
Los motivos que llevaron a desarrollar sistemas operativos que permitiera la ejecución simultánea de varios programas son:
- Uso de recursos:
 Cuando un programa está a la espera de un recurso de E/S está
- desperdiciando tiempo de CPU. Justicia:
procesos y usuarios.
 El sistema operativo asigna el mismo tiempo de uso de CPU a todos los
- Conveniencia:
 Es más fácil escribir varios programas que cumplan una única tarea y coordinarlos antes que tener un solo programa que se encargue de todas las tareas.
Las mismas preocupaciones que motivaron el desarrollo de los procesos ha motivado el desarrollo de los hilos. Los hilos comparten recursos como la memoria y los descriptores de archivos, pero cada hilo tiene su propio contador de programa, su propia pila y sus variables locales. Además permiten el paralelismo en sistemas multiprocesador, múltiples hilos del mismo programa pueden ser ejecutados simultáneamente en múltiples CPUs.
A los hilos también se les conoce como “procesos ligeros”, y los sistemas operativos modernos tratan con hilos como unidad básica de programación. En la ausencia de coordinación explícita, los hilos se ejecutan de forma simultánea y asíncrona respecto alos demás, sin embargo, es necesario coordinar el acceso a los datos compartidos yaque, un hilo puede querer modificar una variable mientras está siendo utilizada por otro obteniendo resultados inesperados.

### 4.1.2 Beneficios de los hilos

Cuando se usan correctamente los hilos pueden reducir costes de desarrollo y mantenimiento además de mejorar el rendimiento de la aplicación.
1.2.1. Aprovechamiento de múltiples procesadores.
 Los sistemas multiprocesador son cada vez más comunes, ya que cada vez es más difícil aumentar la velocidad del procesador y más fácil añadir más procesadores. Cada procesador puede ejecutar como máximo un programa a la vez, en cambio, un programa compuesto por múltiples hilos puede ser ejecutado en varios procesadores simultáneamente, pudiendo así aumentar el rendimiento de la aplicación. También se puede lograr un mejor rendimiento de la aplicación usando hilos sobre sistemas con un solo procesador. Mientras un hilo se queda esperando por una operación síncrona ( E/S) otro hilo puede ejecutarse permitiendo que la aplicación siga ejecutándose durante el bloqueo E/S.
 1.2.2. Simplicidad de modelado. Es más fácil escribir programas que ejecuten un solo tipo de tarea secuencialmente, más sencillo de probar y de mantener que múltiples tipos de tareas a la vez. Asignando acada hilo un tipo de tarea se puede simplificar el código. Un flujo de trabajo complejo yasíncrono puede descomponerse en varios flujos simples y síncronos cada uno de los cuales ejecutados en hilos distintos, interactuando unos con otros en puntos concretos. Un ejemplo de esto es el RMI ( Remote Method Invocation), que puede gestionar múltiples peticiones de forma simultánea.
1.2.3. Manejo simplificado de eventos asíncronos. Los servidores deben ser capaces de aceptar múltiples conexiones de los clientes y concada uno debe establecer un canal de comunicación, cuando se espera recibir datos deun cliente, todo el servidor se bloquea, para evitar esto se forzó a usar operaciones de
E/S no bloqueantes, lo que aumentaba el número de errores de la aplicación además sermás complejo que la comunicación síncrona. Otra solución para solventar este problema son los hilos, si para cada conexión se crea un hilo, cuando se espera la recepción dedatos sólo quedaría bloqueado el hilo en cuestión, y no todo el servidor.
1.2.4. Interfaces de usuario más sensibles. Utilizando interfaces gráficas de usuario con un solo hilo se presentaban problemas como la aparente “congelación” de la interfaz o que los controles de la interfaz podían quedar inservibles durante un cierto tiempo ya que al ser un solo hilo, hasta que no terminaba la tarea que estuviera ejecutando, no devolvía el control a la interfaz. Las interfaces modernas como AWT y Swing no tienen este problema ya que,
reemplazan el bucle de eventos con un gestor de eventos, quedando así la interfaz siempre activa y funcional. La interfaz es la que se encargaría de gestionar los hilos, nosería un único bucle encargado de hacer todas las tareas como en el caso de un solo hilo.

### 4.1.3 Riesgos de los hilos

1.3.1. Peligros de seguridad
Los hilos pertenecientes a una misma tarea comparten direcciones de memoria y se ejecutan concurrentemente, esto es una gran ventaja porque hace que la compartición sea mucho más sencilla de lo que sería con otros mecanismos de comunicación, pero tiene un inconveniente, y es que el acceso simultáneo a las variables por parte de los
hilos puede provocar valores inesperados, es decir, el resultado del programa dependería del orden de acceso a la variable, lo que se conoce como condiciones de carrera. Para evitar esto, Java proporciona mecanismos de sincronización que permite a los hilos acceder a las variables de uno en uno, evitando las condiciones de carrera. Para esto,
los hilos no han de modificar la variable directamente, sino que han de hacer uso de un método “synchronized” que modifique el valor de la variable, y este método será quien llevará la sincronización de los hilos.
1.3.2. Bloqueo mutuo. El bloqueo mutuo se produce cuando un hilo A está esperando por los recursos que posee un hilo B y éste no los libera, por tanto el hilo A se quedará en un bucle de espera infinito y nunca progresará en su ejecución.
1.3.3. Peligros de rendimiento. Los hilos tienen un coste de rendimiento adicional debido a los mecanismos de sincronización necesarios, a que la gestión de programas con varios hilos por parte del procesador es más costosa que de los programas con un solo hilo, y estos factores rendimiento.
añaden
adicional
coste
un
de

### 4.1.4 Los hilos están por todas partes

Incluso cuando un programa no crea explícitamente hilos, los frameworks pueden crearlos en tu nombre, y esos hilos también deben ser “seguros”. Todas las aplicaciones de Java usan hilos: el hilo que ejecuta el método main, los hilos correspondientes a
AWT y Swing, etc. Algunas facilidades para hacer seguros los hilos ( desde el propio código no desde la aplicación principal) son los siguientes:
- Timer:
- RMI:
- Es un mecanismo de gestión de tareas a ejecutar.
 Estos frameworks están diseñados para
Servlets y JavaServer Pages ( JSPs):
manejar el despliegue de aplicaciones web y manejar las peticiones remotas de clientes HTTP.
 Permite ejecutar métodos que se están ejecutando remotamente.
Swing y AWT:
 Gestionan acciones asíncronas, es decir, es capaz de controlar las acciones llevadas a cabo por el usuario mientras la aplicación está haciendo algo.

## 4.2 SEGURIDAD EN HILOS (THREAD-SAFETY)

Los hilos y los bloqueos en la programación concurrente no distan mucho de lo que sonlas vigas y remaches para un ingeniero de obras públicas. Esto viene a decir, que en la construcción de un puente, para que éste no se caiga, se requiere un correcto uso de unagran cantidad de vigas y remaches. Esto mismo ocurre en la programación concurrente con los hilos y bloqueos, ya que se requiere un correcto uso de ellos para manejar el acceso a un estado, y en concreto, para compartir dichos estados variables. Hablamos de hilos-seguros como si fuera código, pero lo que realmente intentamos hacer es proteger los datos de un acceso concurrente no controlado. Es una propiedad decómo se utiliza el objeto en un programa, no de lo qué hace. Si más de un hilo accede a un estado variable, y cualquiera de ellos puede modificarlo,
se deben coordinar sus accesos usando sincronización.

### 4.2.1 Definiciones

Qué es un thread safety
- Thread-safe describe parte de código o rutina que puede ser llamada desde múltiples hilos programados sin querer tener ningún tipo de interacción entre ellos.
- Debe satisfacer la necesidad de que múltiples threads accedan a los mismos datos compartidos, y la necesidad de que una pieza compartida de datos sea accedida por solo un thread en un momento dado.

### 4.2.2 Atomicidad

Si queremos crear un contador en nuestro código para calcular el número de peticiones recibidas, si lo implementamos de la siguiente manera:
public void contador (){
count++;
}
será una única operación pero no atómica, es decir, no se ejecutará como una simple eindivisible operación ya que realmente se divide en una secuencia de 3 operaciones atómicas: leer el valor, sumarle 1 y escribir el nuevo valor. De esta forma, se puede darel caso de que varios procesos accedan al mismo tiempo al recurso compartido,
cambiando su estado y obteniendo de esta forma un valor no esperado de la misma. Estoes lo que conocemos como condiciones de carrera.

### 4.2.3 Bloqueo

En java hay un mecanismo para forzar la atomicidad: el bloque síncrono. El bloquesíncrono consta de dos partes: una referencia a un objeto que servirá como bloqueo y un bloque de código que deberá de proteger el bloqueo. Los bloqueos en Java como mutex o exclusión mutua permiten que al menos un hilo acceda al bloqueo, es decir, cuando un hilo A intente acceder a un bloqueo utilizado por
un hilo B, A deberá de esperar o bloquearse hasta que B lo suelte. Si B nunca lo suelta, A estará siempre en un estado de espera. Desde el momento en el que un único hilo pueda ejecutar una parte de código protegida por un bloqueo, el bloque sincronizado es protegido por el mismo bloqueo la ejecución atómica respecto a cualquier otro, es decir, que se ejecuta como una unidad indivisible. Ningún hilo ejecutando un bloque sincronizado puede observar a otro hilo que esté
dentro del bloque sincronizado protegido por el mismo bloqueo.

### 4.2.4 Protección de estados con bloqueos

También podemos utilizar los bloqueos para garantizar el acceso exclusivo a estados compartidos. Las acciones sobre estados compartidos, como incrementar un contador oel inicio perezoso, necesitan ser atómicas para evitar las condiciones de carrera. En este caso no podemos utilizar los bloques sincronizados ya que necesitamos saber qué
variable está siendo accedida en todo momento. La solución es crear un bloqueo paraque proteja dicho estado compartido. No todos los datos deben de ser protegidos por un bloqueo, sólo es necesario aquellos estados variables que puedan ser accedidos por varios hilos. Cuando una variable está protegida por un bloqueo hay que asegurarse deque dicha variable en ese momento solo puede ser accedida por un único hilo. En elcaso de que se necesite sincronizar el acceso de varias variables al mismo tiempo, todas las variables implicadas deberán de ser protegidas por el mismo bloqueo.

### 4.2.5 Vida y rendimiento

Si la sincronización soluciona las condiciones de carrera, ¿por qué no hacemos que todos los métodos sean sincronizados? Esto se debe a que puede afectar a la vida y al rendimiento de nuestro programa. Por ejemplo si tenemos un servicio sincronizado alque pueden acceder varios usuarios, en cada momento sólo un usuario puede acceder al servicio por lo que puede desesperar al resto de usuarios por el elevado tiempo de espera.

### 4.2.6 Resumen

Hay unas pocas maneras de conseguir thread-safety:

1. Código reentrante: Básicamente, escribir código de tal manera que pueda ser interrumpido durante una tarea, ser ejecutado ( reentrado) de nuevo para realizar otra tarea, y después continuar con su tarea original. Esto normalmente incluye guardar la información de estado en variables locales, en lugar de usar variables static o variables globales.
2. Exclusión mutua: El acceso a los datos compartidos es serializado usando mecanismos que aseguran que sólo un thread está accediendo alos datos compartidos al mismo tiempo. Se requiere gran cautela si una pieza de código accede a múltiples piezas compartidas de datos - los problemas incluyen condición de carrera, deadlocks, livelocks, oinanición de recursos.
3. Almacenamiento thread-local: Las variables están localizadas de manera que cada thread tiene su propia copia privada. Las variables retienen sus
valores a través de la subrutina y otros límites de código, y el código alcual acceden podría no ser reentrante, pero dado que son locales a cada hilo, son thread-safe.
4. Operación atómica: Los datos compartidos son accedidos usando atomicidad la cual no puede ser interrumpida por otros threads. Dado quelas operaciones son atómicas, los datos compartidos están siempre guardados en un estado válido, sin importar el orden en que los threads acceden. Atomicidad forma la base de muchos mecanismos de bloqueo de thread.
 4.3 OBJETOS COMPARTIDOS
En este capítulo se examinaran las técnicas para compartir y publicar datos de modo que puedan ser accesibles por varios hilos de una forma segura. Es un error común pensar que la sincronización entre bloques y métodos se basa en resolver las secciones críticas,
ya que se olvida otro aspecto muy delicado: La visibilidad de memoria.

### 4.3.1 Visibilidad

En un hilo simple, si guardamos un valor en una variable y luego lo leemos, podemos esperar leer el valor anteriormente guardado. Pero cuando la lectura y la escritura ocurren en diferentes hilos, no habrá garantía de que la lectura de la variable devuelva un valor escrito por otro hilo. Por ello es necesario usar sincronización, A continuación se muestra un ejemplo da mala sincronización:

```

public class NoVisibility {
private static boolean ready;
private static int number;
private static class ReaderThread extends Thread {
public void run () {
while (!ready)
Thread.yield ();
System.out.println ( number);
}
}
public static void main ( String[] args) {
new ReaderThread ().start ();
number = 42;
ready = true;
}
}

```

Vemos dos hilos, el hilo principal y el hilo lector, que acceden a las variables compartidas “Ready” y “number”. El hilo principal inicia el hilo lector y a continuación guarda el valor 42 en la variable “number” true para “ready”. El hilo lector se ejecuta hasta que "ready" es verdadero, y entonces, imprime el número. Aunque parezca obvio que imprimirá 42, de hecho es posible que se imprima cero, o nunca terminan en todo.
3.1.1. Datos Obsoletos
En el ejemplo NoVisibility, cuando el hilo lector examina la variable “ready”, el valor podría estar obsoleto. A menos que la sincronización se utilice cada vez que se accede auna variable, siempre existirá la posibilidad de que el valor de esa variable esté
obsoleto
3.1.2. Operaciones de 64 bits no atómicas
Las variables de 64 bits “double” y “long” no son declaradas volátiles. Java permite quelas operaciones de lectura y escritura sobre estos 64 bits se hagan como dos operaciones separadas de 32 bits. Si la lectura y escritura ocurre en diferentes hilos, podría leerse una variable no-volátil y obtener los primeros 32 bits de un valor y los segundos 32 bitsde otro.
3.1.3. Visibilidad y bloqueo
Cuando un hilo A ejecuta un bloque sincronizado, y un hilo B usa ese bloque sincronizado guardado por el mismo bloqueo, los valores que eran visibles en A antesde liberar el bloqueo serán de esta forma visibles en B al realizar de nuevo el bloqueo. Por ello la lectura y escritura de variables compartidas en hilos deben sincronizarse bajoun bloqueo común sobre ellas.
3.1.4. Variables volátiles
Además de la sincronización, Java provee de otra alternativa ( más débil): las variables volátiles: Cuando una variable es declarada volátil, no son guardadas en registros, deeste modo siempre retorna el valor de más reciente de cada hilo. Aunque convenientes para usar como flags o variables interrupción o de estado como “despierto” o “dormido”
y otras similares, no es suficientemente fuerte para el incremento de operaciones atómicas como ( count++).

### 4.3.2 Publicación y Escape

Al declarar un objeto como público en Java, permitimos que sus métodos y variables sean visibles por otros objetos. Diremos que un objeto se ha escapado cuando un objeto que no debería haber sido publicado lo fue. Una buena práctica de programación es no permitir que este objeto escape durante su construcción.

### 4.3.3 Hilos que no comparten variables (Confinamiento de hilos)

Si los datos son accesibles solo por un hilo, no es necesaria ninguna sincronización. Esta técnica es una de las formas más simples de conseguir seguridad en los hilos y esusada extensivamente por Swing y JDBC.
3.3.1. Hilos que no comparten variables Ad-Hoc
Cuando la responsabilidad de mantener el aislamiento de las variables dentro de cada hilo recaiga enteramente sobre la implementación denotaremos estos hilos Ad-hoc.
3.3.2. Reclusion de pila
El confinamiento de pila es un caso especial de hilos que no comparten variables dondeel objeto puede ser solo alcanzado a través variables locales.
3.3.3. Hilo Local
Una definición formal para el mantenimiento de hilos que no comparten variables eshilo local. El hilo local provee métodos de acceso que mantienen una copia separada del valor en cada hilo que lo usa. Los hilos locales son ampliamente usados en aplicaciones
Framework.

### 4.3.4 Inmutabilidad

Hay otra finalidad en la necesidad de usar sincronización y es la de usar objetos inmutables. Uno objeto inmutable será aquel cuyo estado no puede ser cambiado tras se construcción. Esto hace que los hilos sean siempre seguros, ya que sus invariantes son establecidas por el constructor y después no pueden ser cambiadas.
3.4.1. Final Class
La clase “Final” son una versión mas limitada del mecanismo “const” usado por C#,
soportando la construcción de objetos inmutables. Estas clases no pueden ser modificadas y además tienen una semántica especial bajo el modelo de memoria Java.

### 4.3.5 Publicación Segura

3.5.1. Publicación Impropia: Cuando los buenos objetos van mal. No podemos confiar en la integridad de objetos construidos parcialmente. Un hilo podría ver el objeto un estado inconsistente y más tarde ver que de repente ha cambiado incluso aunque no haya sido modificado desde que se publicó.
3.5.2. Objetos Inmutables e inicialización segura. Debido a que la inmutabilidad de objetos es tan importante, el modelo de memoria de
Java ofrece una garantía especial de inicialización segura para los objetos inmutables compartidos. Esto es que aunque la referencia de un objeto se convierta en visible para otros hilos, no necesariamente significa que el estado de ese objeto sea visible para elhilo que va hacer uso de él.
3.5.3. Expresiones de publicación seguras. Los objetos que no son inmutables, deben ser publicados de forma segura, que usualmente implica sincronización tanto del hilo que lo publica como del hilo que accede a él. Para una publicación segura, tanto la referencia al objeto como el estado de este, deben ser visibles a otros hilos al mismo tiempo. Un objeto correctamente construido puede ser publicado de forma segura mediante:
Inicializando la referencia de un objeto desde un inicializador estático.
5.

## 6. Almacenando una referencia a él en una clase volátil o Referencia

Atómica.
7. Almacenando una referencia a él en una clase final de un objeto
correctamente construido ó
8. Almacenando una referencia a él en una clase que es apropiadamente
guardado por un bloqueo.
3.5.4. Objetos Inmutables Efectivos
La publicación segura es suficiente para los hilos para objetos seguramente accesibles,
que no van a ser modificados después de su publicación, sin ninguna sincronización adicional. Los objetos que técnicamente no son inmutables, pero sus estados no serán modificados después de ser publicados, serán considerados inmutables.
3.5.5. Objetos Mutables. La sincronización debe ser usada no solo para publicar un objeto mutables, sino también para cata vez que el objeto es accedido para asegurar la visibilidad de la consecuente modificación
3.5.6. Compartir Objetos de forma segura. Siempre que se adquiera la referencia de un objeto, se debería saber que está permitido hacer con él, si es necesario adquirir un bloqueo antes de usarlo, si está permitido modificar su estado, o si se trata de un objeto tan solo de lectura. De este modo cuando se publique un objeto siempre debemos documentar como ese objeto puede ser accedido
 4.4 COMPOSICIÓN DE OBJETOS.

### 4.4.1 Diseño de clases de hilos seguras

El encapsulado permite determinar si una clase de hilos es segura sin tener que examinar todo el programa. El proceso de diseño de clases de hilos seguras debería incluir estos 3 elementos:
Identificar las variables que forman el estado del objeto. Identificar las invariantes que restringen el estado de esas variables.
- Establecer una política de gestión de acceso concurrente al estado del objeto. La política de sincronización define como un objeto coordina el acceso a su estado sin violar sus invariantes o post-condiciones. Especifica qué variables están protegidas por quién. Ejemplo de contador de hilo:

```

 public final class Counter {
@GuardedBy ("this") private long value = 0;
public synchronized long getValue () {
return value;
}
public synchronized long increment () {
if ( value == Long. MAX_VALUE)
throw new IllegalStateException ("counter overflow");
return ++value;
}
}

```

4.1.1. Requisitos de sincronización. Para que una clase de hilos sea segura debemos asegurar que cualquier operación que modifique el valor de las variables asegure que se seguirán cumpliendo las post-
condiciones.
4.1.2. Operaciones dependientes de los estados. En un programa con un solo hilo si la precondición no se cumple solo hay opción aerror. Cuando se tienen varios hilos se puede esperar hasta que la precondición se cumpla antes de realizar la operación ( wait y notify). Para crear operaciones que esperen que se cumpla una precondición antes de avanzar, suele ser más fácil utilizar las librerías existentes, como por ejemplo los semáforos o las colas de bloqueo.

### 4.4.2 Encapsulado

Encapsular datos dentro de un objeto restringe el acceso a los datos a través de los métodos del objeto, haciendo más fácil asegurar que los datos siempre se accederán aellos de forma segura. Ejemplo de encapsulado de datos:

```

public class PersonSet {
@GuardedBy ("this")
private final Set<Person> mySet = new HashSet<Person>();
public synchronized void addPerson ( Person p) {
mySet.add ( p);
}
public synchronized boolean containsPerson ( Person p) {
return mySet.contains ( p);
}
}

```

El encapsulado hace que sea más fácil construir clases de hilos seguras porque una clase que encapsula su estado permite comprobar si es segura sin tener que examinar todo el programa.
4.2.1. El monitor de Java. Un monitor es un objeto que implementa el acceso en exclusión mutua a sus métodos,
es decir, permite e acceso a sus variables únicamente a través de los métodos ( los métodos ofrecidos deben estar sincronizados).

### 4.4.3 Delegar/confiar la seguridad de los hilos.

 A veces es posible delegar la seguridad del hilo a los elementos subyacentes. En caso deque las variables de estado responsables de asegurar la sincronización no sean independientes ( y seguras), puede haber inconsistencia de datos. Si una variable de estado es segura, no participa en ninguna invariante que restrinja suvalor, y no tiene prohibida la transición de estado por ninguna de sus operaciones,
entonces puede ser publicada de forma segura.

### 4.4.4 Añadir funcionalidad a las clases de hilos seguras existentes

Rehusar las clases existentes suele ser menos costoso y menos arriesgado que crear clases nuevas, ya que las clases existentes ya están probadas. No siempre es posible añadir operaciones modificando la clase original, ya que no siempre se tiene acceso al código. En el caso de tener acceso a la clase es necesario comprender la implementación y la política de sincronización para que las
modificaciones que se hagan sean coherentes con el modelo original. Ejemplo de extensión de Vector:

```

public class BetterVector<E> extends Vector<E> {
public synchronized boolean putIfAbsent ( E x) {
boolean absent = !contains ( x);
if ( absent)
add ( x);
return absent;
}
}

```

4.4.1. Bloqueo por parte del cliente. Otra forma de extender la funcionalidad de la clase sin extender la clase es añadiendo el código en una clase “helper”. Éste bloqueo implica guardar el código de cliente que utiliza un objeto X con el bloqueo que X utiliza para tener a salvo su propio estado.

```

public class ListHelper<E> {
public List<E> list =
Collections.synchronizedList ( new ArrayList<E>());
public boolean putIfAbsent ( E x) {
synchronized ( list) {
boolean absent = !list.contains ( x);
if ( absent)
list.add ( x);
return absent;
}
}
}

```

4.4.2. Composición. La composición significa utilizar objetos dentro de otros objetos. Por ejemplo, un appletes un objeto que contiene en su interior otros objetos como botones, etiquetas, etc. Esuna alternativa menos frágil para añadir operaciones atómicas a las clases existentes.

```

public class ImprovedList<T> implements List<T> {
private final List<T> list;
public ImprovedList ( List<T> list) { this.list = list; }
public synchronized boolean putIfAbsent ( T x) {
boolean contains = list.contains ( x);
if ( contains)
list.add ( x);
return !contains;
}
public synchronized void clear () { list.clear (); }
}

```

### 4.4.5 Documentar políticas de sincronización

Documentar una clase segura de hilos ofrece garantía a sus clientes, documentar una política de sincronización ofrece facilidades a los encargados de mantener o mejorar el código. La documentación es una de las herramientas más poderosas y menos usadas para gestionar la seguridad de los hilos.
 4.5 BLOQUES DE CONSTRUCCIÓN ( BUILDING BLOCKS)
En el anterior capítulo hemos visto varias técnicas para construir clases thread-safe,
incluyendo la delegación de la seguridad de los hilos en clases thread-safe existentes. Las librerías de la plataforma incluyen una gran cantidad de conjuntos de buildingblocks concurrentes, como las colecciones de thread-safe y una variedad de sincronizadores que pueden coordinar el flujo de control de hilos cooperantes. En este capítulo vamos a ver los building blocks más útiles para usarlos en aplicaciones concurrentes.

### 4.5.1 Colecciones sincronizadas

Estas clases logran la seguridad de los hilos encapsulando sus estados y sincronizando cada método público así que sólo un único hilo puede acceder al estado de la colección en un momento dado.
5.1.1. Problemas con las colecciones sincronizadas
Las colecciones sincronizadas son thread-safe, pero en ocasiones se puede necesitar un bloqueo adicional para proteger acciones. Por ejemplo, en el problema del productor-
consumidor podemos tener el siguiente código:

```

public static Object getLast ( Vector list) {
int lastIndex = list.size () - 1;
return list.get ( lastIndex);
}
public static void deleteLast ( Vector list) {
int lastIndex = list.size () - 1;
list.remove ( lastIndex);
}

```

A simple vista parece que no haya ningún problema si varios hilos acceden simultáneamente a los métodos, pero como veremos a continuación, el programa puede que se comporte de forma inesperada. Por ejemplo, un hilo A decide eliminar un elemento de un vector, y a su vez, un hilo B desea obtener el último valor del mismo vector, se puede dar el caso que ambos hilos accedan a la vez al último valor del vector,
el hilo A lo elimine y el hilo B intente recuperarlo, por lo que se produciría una excepción ya que el hilo B no puede recuperar el dato del vector ya que ha sido eliminado. Para solucionar este problema hay que crear una nueva política de sincronización que permita bloquear al productor-consumidor. Esto es posible creando nuevas operaciones que sean atómicas y para ello sincronizamos la parte de código que deba ser compartida.

```

public static Object getLast ( Vector list) {
synchronized ( list) {
int lastIndex = list.size () - 1;
return list.get ( lastIndex);
}
}
public static void deleteLast ( Vector list) {
synchronized ( list) {
int lastIndex = list.size () - 1;
list.remove ( lastIndex);
}
}

```

De esta manera hacemos que getLast y deleteLast sean atómicas, asegurándonos que el tamaño del vector no variará entre la llamada de size y get.

### 4.5.2 Colecciones concurrentes

Java mejora las colecciones sincronizadas ofreciendo varias clases de colecciones concurrentes. Las colecciones sincronizadas lograban la seguridad de los hilos serializando todos los accesos al estado. El coste de esta solución es una pobre concurrencia ya que cuando hay múltiples hilos para la parte que hay que sincronizar, el rendimiento decae sensiblemente. Por ello, las colecciones concurrentes están diseñadas para accesos concurrentes de múltiples hilos. Reemplazando las colecciones sincronizadas por colecciones concurrentes puede ofrecer unas mejoras de escalabilidad con pequeños riesgos. La primera colección que vamos a ver es Queue. Un Queue tiene la finalidad de almacenar un conjunto de elementos temporalmente mientras esperan a ser procesados. Las operaciones sobre Queue no se bloquearán, puesto que si queremos acceder a un elemento que no existe, nos devolverá un null en vez de una excepción. Otra colección concurrente es ConcurrentHashMap que ofrece las mismas utilidades que HashMap pero con una estrategia distinta de bloqueo que ofrece una mejor concurrencia y escabilidad. Otra colección es CopyOnWriteArrayList que es equivalente a una lista sincronizada pero ofrece mejoras de concurrencia y elimina la necesidad de bloquear o copiar la colección durante la iteración.

### 4.5.3 Blocking Queues

La colección BlockingQueue provee un sistema de bloqueo para los métodos put y take. Si la cola está llena, el método put se bloqueará hasta que haya espacio disponible; si lacola está vacía, el método take se bloqueará hasta que haya un elemento disponible. BlockingQueue es un buen sistema para el problema del productor consumidor, ya que simplifica el desarrollo eliminando dependencias de código entre las clases de productory consumidor, y simplifica la carga de trabajo de gestión de actividades que puede producir o consumir datos a distintas velocidades.

### 4.5.4 Métodos de bloqueo e interrupción

Los hilos se pueden bloquear o pausar por distintas razones: esperando por una entrada/salida, esperando para adquirir un bloqueo, esperando para despertarse de unsleep, o esperando por la devolución de un resultado de otro hilo. Cuando un hilo se boquea, se suele suspender y situar en unos de los estados de bloque de hilos
( BLOCKED, WAITING o TIMED_WAITING). La diferencia entre una operación de bloqueo y una operación ordinaria que requiere cierto tiempo para finalizar, es que unhilo bloqueado debe esperar por un evento ajeno a él. Cuando ocurre dicho evento, elhilo se le devuelve el estado de RUNNABLE y puede pasar de nuevo por el planificador. Los hilos poseen el método interrupt para interrumpir un hilo y para consultar si un hiloha sido interrumpido. Cada hilo tiene una propiedad booleana para representar su estado de interrupción. La interrupción es un mecanismo cooperativo. Un hilo no puede forzar a otro a parar su ejecución pero si puede mandarle una interrupción para que pare en un punto de parada si éste lo desea.

### 4.5.5 Sincronizadores

Los blocking queues son únicos entre las colecciones de clases: no solo realizan sus acciones como contenedores de objetos, sino que también coordinan el control de flujode los hilos productor y consumidor hasta que la cola entra en el estado deseado. Un sincronizador es cualquier objeto que coordina el control de flujo de los hilos basado en su estado. Por lo tanto los blocking queues son sincronizadores, pero no son los
únicos sincronizadores. También existen los semáforos, las barreras y los cerrojos. Todos los sincronizadores comparten ciertas propiedades estructurales: ellos encapsulan el estado que determina si los hilos de entrada al sincronizador pueden entrar o deben esperar, proveyendo métodos para manipular ese estado y métodos para esperar eficientemente para que entren en el estado deseado.
5.5.1. Cerrojos
Un cerrojo es un sincronizador que duerme el progreso de los hilos hasta que alcanza un estado final. Un cerrojo actúa como una puerta: hasta que el cerrojo no alcance el estado final, la puerta permanecerá cerrada y ningún hilo podrá pasar, y si alcanza dicho estado final, la puerta se abrirá permitiendo pasar a todos los hilos. Una vez que el cerrojo ha alcanzado su estado final, éste no podrá cambiar su estado por lo que permanecerá
abierto siempre. CountDownLatch es una implementación flexible del cerrojo que simplemente inicializa un contador a un valor igual al número de hilos que se van a ejecutar de forma concurrente; cada hilo deberá invocar el método countDown () de CountDownLatch al terminar su ejecución. El hilo principal, una vez que manda ejecutar todos los hilos,
espera a que estos terminen; para lograrlo, se invoca el método await (). Cuando el contador llega a cero, el hilo principal sale del await () y continúa su ejecución de forma normal.
5.5.2 Semáforos
Los semáforos se utilizan para controlar el número de actividades que pueden acceder aun cierto recurso o realizar una acción dada al mismo tiempo. Un semáforo gestiona un
conjunto de permisos virtuales; el número inicial de permisos se le pasa al constructor del Semaphore. Las actividades pueden adquirir permisos y liberarlos cuando hayan terminado. Si no hay permisos, se bloqueará hasta que uno de ellos termine ( o hasta quehaya una interrupción o se agote el tiempo de la operación). Un tipo de semáforo es el semáforo binario, el cual tiene un contador inicial de uno. Un semáforo binario puede ser usado como un mutex sin bloqueos semánticos reentrantes;
quien tiene el único permiso, posee el mutex.
5.5.3 Barreras
Hemos visto como los cerrojos facilitan el comienzo de un grupo de actividades oesperan a que se complete un grupo de ellas. Los cerrojos son objetos de un solo uso;
una vez que el cerrojo entra en el estado final, ya no se puede reiniciar. Las barreras son similares a los cerrojos en cuanto se refiere a bloquear grupos de hilos hasta que ocurre un evento, con la salvedad de que todos los hilos deben llegar juntos alpunto de la berrera a la vez para continuar. Los cerrojos esperan eventos mientras quelas berreras esperan por el resto de hilos.

## 4.6 EJECUCIÓN DE TAREAS

La mayoría de las aplicaciones concurrentes son organizadas alrededor de la ejecución de tareas: abstractas, unidades discretas de trabajo. Dividir el trabajo de la aplicación en tareas simplifica la organización de programas, facilita la recuperación de errores proveyendo límites de transacción naturales y promueve la concurrencia proveyendo una estructura natural de trabajo en paralelo

### 4.6.1 Ejecutando tareas en hilos

El primer paso en ordenar un programa sobre la ejecución de tareas es identificado los límites sensibles de las tareas. Idealmente las tareas son actividades independientes:
trabajo que no depende del estado, resultado o efectos colaterales de otras tareas. La independencia facilita la concurrencia, ya que como tareas independientes pueden ser ejecutadas en paralelo si hay adecuados procesos de recursos.
6.1.1. Ejecutando hilos secuencialmente. Es el modo más simple de ejecutar hilos. Simple y teóricamente correcto, pero cuya producción y rendimiento sería pobre ya que solo atiende una petición a la vez. El hilo principal alterna entre conexiones aceptadas y procesar las peticiones asociadas,
mientras el servidor está atendiendo una petición, las nuevas conexiones deben esperar hasta que acabe la actual petición y pedir ser aceptadas de nuevo.
6.1.2. Creación explicita de hilos para tareas. Un mejor enfoque es crear un nuevo hilo para servir cada petición. Aunque similar al modelo anterior, esta vez el hilo principal alterna entre las conexiones entrantes yaceptadas y despachando solicitudes. La diferencia es que para cada conexión el bucle principal crea un nuevo hilo para procesar la solicitud en lugar de ser procesada en elhilo principal.
6.1.3. Desventajas
Sin embargo cuando un gran número de hilos son creados el enfoque de hilo por tarea tiene algunos inconvenientes prácticos como son la sobrecarga del ciclo de vida de unhilo, el consumo de recursos y la inestabilidad. Y es que aunque hasta cierto punto la creación de más hilos puede mejorar el rendimiento, más allá de ese punto la creación de más hilos tan solo ralentiza nuestro programa, de este modo el problema de este enfoque es que nada establece un límite en el número de hilos que deben ser creados excepto la tasa que usuarios remotos pueden lanzar como peticiones de http.

### 4.6.2 El Framework executor

Las tareas son unidades lógicas de trabajo y los hilos, mecanismos por lo que las tareas pueden ser ejecutadas asíncronamente. Tras ver las limitaciones de los enfoques anteriores veremos ahora la implementación del Framework ejecutor cuya interfaz forma la base para un flexible y poderoso Framework para la ejecución de tareas asíncronas que soportan la amplia variedad de políticas de ejecución. Además provee
soporte para el ciclo de vida de los hilos y medios para la recopilación de estadísticas,
manejo de aplicaciones y monitoreo. De este modo las abstracciones primarias de cada ejecución de una tarea en las librerías de clases Java no es “Thread” sino “Executor” como vemos a continuación:

```

public interface Executor {
void execute ( Runnable command);
}

```

6.2.1. Políticas de ejecución. Las políticas de ejecución son una herramienta de manejo de recursos y la política
óptima depende de los recursos de computación disponibles y los requerimientos de calidad de servicio. Limitando el número de las tareas concurrentes, podemos asegurar que la aplicación no falla debido al agotamiento de recursos ó no sufre problemas de rendimiento en la conexión por escasez de recursos.
6.2.2. Threads pools
Una piscina de hilos, como su nombre sugiere, gestiona una homogénea concentración de hilos. Una piscina de hilos está limitada a una cola de tareas esperando a ser ejecutadas. Ejecutar las tareas en piscinas de hilos tiene una serie de ventajas sobre el enfoque de hilo por tarea. Reutilizando un hilo existente en lugar de crear uno nuevo,
amortiza la creación de subprocesos y los costos de desmontaje sobre las solicitudes múltiples. Además, debido a que el hilo ya existe en el momento de la solicitud, la latencia asociada con la creación de hilos no retrasa la ejecución, mejorando además el tiempo de respuesta.
 La librería de clases provee una flexible implementación de piscina de hilos, donde podemos crear una piscina de hilos mediante uno de los siguientes métodos estáticos en
Executors: newFixedThreadPool y newCachedThreadPool.
6.2.3. Ciclo de vida Executor
Tras ver cómo crear un Executor veremos cómo destruirlo. El ciclo de vida de un servicio ejecutor tiene tres estados: ejecutando ( running), cerrado ( shutting down) yterminado ( terminated). El servicio Ejecutor es inicializado en el estado ejecutando, el siguiente estado cerrado no permite que nuevas tareas sean aceptadas, pero se permiten que las que ya lo han sido se completen, incluyendo aquellas que todavía no han empezado a ejecutarse, una vez todas han sido ejecutadas pasa al estoado terminado.
6.3.4 Tareas periódicas y retrasadas. Si necesitamos construir nuestra propia programación de servicios, podríamos usar
“DelayQueue” una implementación de la cola de bloques que provee la funcionalidad organizativa de “ScheduledThreadPoolExecutor”. Una “DelayQueue” gestiona una colección de objetos retrasados. Un retraso tiene un tiempo de retraso asociado con él,
“DelayedQueue” nos permite tomar un elemento solo si su retraso ha expirado. Lo objetos son retornados de “DelayedQueue” ordenados por el tiempo asociado con su retraso.

### 4.6.3 Encontrando paralelismo explotable

El Framework ejecutor hace fácil especificar una política de ejecución, pero para usarun ejecutor, tenemos que ser capaces de describir nuestra tarea como Ejecutable.
6.3.1. Ejemplo: Procesador de página secuencial. El enfoque más sencillo es procesar los HTML secuencialmente. Según se encuentra eltexto marcado, se procesa en un buffer de imagen, según se encuentren es….. Es facil de implementar y requiere tocar cada elemento del documento tan solo una vez, pero podría enojar al usuario que podría tener que esperar un largo periodo de tiempo antesde que todo el texto sea procesado. Un enfoque menos molesto para el usuario, aunque aun secuencial, consistiría en procesar primero los elementos de texto, dejando los contenedores rectangulares paralas imágenes, y después de de completar una primera pasada inicial sobre el documento,
volver en una segunda pasada a descargar las imágenes y cargarlas en los contenedores asociados.
6.3.2. Callable and Future
El framework usa “Runnable” como su representación de tarea básica. Runnable es una abstracción limitada, la ejecución no puede retornar un valor o lanzar excepciones,
aunque puede tener efectos laterales tales como escribir en un archivo o alojar un resultado en una estructura de datos compartida.
“Runnable” y “Callable”describen tareas computacionales abstractas. Las tareas son normalmente finitas, tienen un claro punto de partida y finalmente acaban. El ciclo devida de una tarea ejecutada por un “Executor”tiene cuatro fases, creado, presentado,
comenzado, y completado. Ya que las tareas pueden llevar un largo tiempo para ser ejecutadas, nosotros tambien queremos ser capaces de cancelar tareas. En el “Executor
Framework” las tareas que han sido presentadas pero no comenzadas pueden ser siempre ser canceladas, y las tareas que han empezado pueden algunas veces ser canceladas si responden a la interrupción. Cancelar una tarea que no ha sido todavía completada no tiene efecto.
“Future” representa el ciclo de vida de una tarea y provee métodos para testear si latarea ha sido completada o cancelada, recobra su resultado y cancela la tarea. Acontinuación se muestra un ejemplo de ambas.

```

public interface Callable<V> {
V call () throws Exception;
}

```

```

public interface Future<V> {
boolean cancel ( boolean mayInterruptIfRunning);
boolean isCancelled ();
boolean isDone ();
V get () throws InterruptedException, ExecutionException, CancellationException;
V get ( long timeout, TimeUnit unit)
throws InterruptedException, ExecutionException, CancellationException, TimeoutException;
}

```

6.3.5. CompletionService
Si tenemos un grupo de operaciones que enviar a un “Executor” y queremos recobrar su resultado según vallan estando disponibles.
“Completion Service”, combina la funcionalidad de un “Executor” y un
“BlockingQueue”. “ExecutorCompletionService” implementa “CompletionService”,
delegando la computación en un “Executor”.
 La implementación de
“ExecutorCompletionService” es bastante sencilla. El constructor crea una cola de bloqueos “BloquingQueue”, para mantener los resultados completos. Las tareas futuras tienen un método echo que es llamado cuando se completa la computación. Cuando una tarea es prensetada, es envuelta en una “QueueingFuture” una subclase de “FutureTask”
que sobrescribe “done” para poner el resultado en la cola “BlockingQueue” como podemos obsevar en el siguiente ejemplo:

```

private class QueueingFuture<V> extends FutureTask<V> {
QueueingFuture ( Callable<V> c) { super ( c); }
QueueingFuture ( Runnable t, V r) { super ( t, r); }
protected void done () {
completionQueue.add ( this);
}
}

```

Los métodos “take” y “poll” delegan en la cola “BlockingQueue”, bloqueando si los resultados no están aun disponibles.
 4.7 CANCELACIÓN Y FINALIZACIÓN. No siempre se puede esperara a que un hilo termine su ejecución y es necesario terminarlo antes de tiempo. Java no tiene mecanismos cooperativos para forzar el cierre de los hilos, pero ofrece mecanismos que permiten que los hilos que pregunten a otros sideben parar, pudiendo así parar de forma segura y sin dejar las estructuras de datos de inconsistentes.

### 4.7.1 Cancelación de Tareas

Una actividad es cancelable si un código externo puede llevarla al estado de finalización antes de su finalización normal. Pueden darse casos en los que no finalice. Ejemplo de cancelación de tareas:

```

public class ejemploCancelacion implements Runnable {
private volatile boolean cancelled;
public void run () {
while (!cancelled ) {…}
}
public void cancel () { cancelled = true; }
}

```

7.1.1. Interrupción:
La interrupción es un mecanismo de un hilo para avisar a otro de que debe terminar loque está haciendo y hacer otra cosa. Las interrupciones son frágiles y difíciles de mantener. No siempre paran al hilo, avisan de que ha llegado un mensaje de interrupción. Son la manera más acertada de implementar una cancelación.

```

public class ejemploCancelacion implements Runnable {
public void run () {
try{
while (! Thread.currentThread ().isInterrupted () ) {…}
}catch (…)
}
public void cancel () { interrupt (); }
}

```

7.1.2. Políticas de interrupción. Determinan cómo debe comportarse un hilo ante una interrupción. Cada hilo tiene su propia política de interrupción, por tanto no se debe interrumpir a no ser que se conozca su política, por esto, es recomendable que un hilo sea interrumpido únicamente por su propietario.
7.1.3. Respuesta a las Interrupciones. Cuando se llama a un método interrumpible como por ejemplo Thread.sleep, hay dos estrategias para manejar InterruptedException:
1
2
Propagar la excepción. Restaurar el estado de la interrupción.
7.1.4. Bloqueos no interrumpibles. No todos los métodos bloqueantes o mecanismos de bloqueo son sensibles a las interrupciones. A veces se puede “convencer” a las tareas ininterrumpibles mediante medios similares a las interrupciones, pero necesitamos saber porqué está bloqueado.
Socket E/S síncrono ( java.io).
- E/S síncrona ( java.io).
- E/S asíncrona con Selector
- Adquisición de bloqueo.

### 4.7.2 Detención de servicios basados en hilos

Si una aplicación va a finalizar, debe finalizar la ejecución de todos sus serviciosy sus hilos deben terminar. Como no hay forma preferente de terminar un hilo,
debe persuadirse para terminar por sí mismo.
El servicio debe ofrecer métodos para finalizar su ejecución ( del servicio y de los hilos que posea) de forma segura.
7.2.1. Apagado ExecuteService. Execuros service ofrece 2 maneras apagar:
- Apagado elegante ( shutdown), que es más lento pero más seguro, ya que
ExecutorService no finaliza hasta que todas sus tareas han finalizado.
- Apagado brusco ( shutdownNow), es más rápido pero más peligroso que
shutdown, porque puede ser interrumpido en medio de una ejecución.
- 7.2.2. Poisson Pills. Es una forma de finalizar un servicio productor-consumidor. Con una cola FIFO, se aseguran de que el consumidor termine su trabajo antes de cerrarse, los productores nodeben realizar ningún trabajo tras poner la píldora en la cola. Este método sólo funciona cuando se conoce el número de productores y consumidores. Ejemplo de productor-
consumidor:

```

public class productor extends Thread {
public void run () {
(…)
try {
queue.put ( POISON);
break;
} catch ( InterruptedException e1) { }
(…)
}
}

```

```

public class consumidor extends Thread {
public void run () {
try {
(…)
File file = queue.take ();
if ( file == POISON)
break;
else
indexFile ( file);
} catch ( InterruptedException consumed) { }
}
}

```

### 4.7.3 Terminaciones anómalas de los hilos

El marco donde se ejecuta el hilo debe controlar las excepciones producidas porsus hilos y controlarlas, creando nuevos hilos que reemplacen al que ha terminado inesperadamente, finalizando la tarea de forma segura o no modificando nada si la cantidad de hilos restantes pueden cumplir con la tarea asignada.
7.3.1. Uncaught exception handlers. UncaughExceptionHandler permite detectar cuando un hilo muere debido a una excepción no capturada. La acción más común de estos manejadores es mostrar mensaje por pantalla, pero también pueden intentar reiniciar el hilo, finalizar la aplicación, etc. En aplicaciones de larga duración, es recomendable usar “uncaught exception handler”
para todos los hilos para que al menos muestre la excepción.
- 7.4.- JVM shutdown. La máquina virtual de Java puede finalizar en modo normal o abrupto:
- El programa finaliza de forma normal ( cuando el último hilo termina).
- Terminando el proceso de la JVM a través del sistema operativo. Shutdown hooks:
Runtime.addShutdownHook.
- Daemon threads: Son hilos que no finalizan hasta que su JVM finaliza, pero la
JVM no los tiene en cuenta a la hora de finalizar, sino que son ellos los que tienen
JVM.
cuenta
- Finalizers:Se usa para liberar los recursos que el sistema no puede liberar. Se pueden ejecutar en cualquier hilo. Son difíciles de escribir y de gestionar.
Son hilos no
registrados con
iniciados
en
la
 4.8 UTILIZANDO LOS GRUPOS DE SUBPROCESOS
Este capítulo trata las opciones avanzadas para configurar y modificar grupos de hilos ydescribir los riesgos de usar el framework de ejecución de tareas.

### 4.8.1 Unión entre tareas y políticas de ejecución

Mientras el framework Executor ofrece una flexibilidad sustancial en la especificación y modificación de las políticas de ejecución, no todas las tareas son compatibles con todas las políticas de ejecución. Los tipos de tareas que requieren una política de ejecución específica incluyen:
- Tareas dependientes. Cuando tenemos tareas que dependen de otras en un grupode hilos, implícitamente se crean restricciones en la política de ejecución que deben ser cuidadosamente gestionadas para evitar problemas de rendimiento.
- Tareas que aprovechan el confinamiento de hilos. Los executores de un único hilo tratan mejor la recurrencia que lo que lo hacen los grupos de hilos arbitrarios. Ellos garantizan que las tareas no se ejecuten concurrentemente, locual permite la seguridad de los hilos en el código de la tarea.
- Tareas sensibles al tiempo de respuesta. Las aplicaciones GUI son sensibles al tiempo de respuesta: a los usuarios les molesta los retrasos entre pulsar un botóny su correspondiente reacción visual.
- Tareas que utilizan ThreadLocal. ThreadLocal permite a cada hilo tener su propia versión privada de una variable. Sin embargo los executores son libres de reutilizar los hilos como ellos crean conveniente. Los ThreadLocal no se deben utilizar en grupos de hilos para comunicar valores entre tareas.
- Los grupos de hilos trabajan mejor cuando las tareas son homogéneas e independientes. Combinar tareas de larga y corta duración produce
“obstrucción” del grupo a no ser que sea muy grande; la presentación de tareas que dependan de otras tareas provocan abrazos mortales ( deadlock) excepto enlos grupos ilimitados.
8.1.1. Deadlock por inanición de los hilos. Si la tarea depende de la ejecución de otras tareas en un grupo de subprocesos, puede darse un deadlock. En un executor de un único hilo, una tarea que espere el resultado deotra tarea en el mismo executor siempre se producirá deadlock ya que la segunda tarease pondrá en cola a la espera de que la primera tarea finalice, pero la primera no finalizará porque está esperando el resultado de la segunda tarea. Lo mismo puede ocurrir en un gran grupo de hilos si todos los hilos están ejecutando tareas que están bloqueadas esperando por otras tareas que están en la cola de trabajo. Esto se denomina deadlock por inanición de los hilos.
8.1.2 Tareas de larga duración. Los grupos de hilos pueden tener problemas de rendimiento si las tareas pueden bloquearse por un extenso periodo de tiempo, incluso si no hay posibilidad de deadlock. Un grupo de hilos pueden colapsarse con tareas de larga duración, incrementando el tiempo de servicio incluso para tareas cortas. Si el grupo de hilos es demasiado pequeño en comparación con el número de tareas a ejecutar, con frecuencia todo el grupo dehilos se ejecutará con una larga duración y el rendimiento se verá afectado.
Una técnica que puede mitigar este problema es usar recursos que miden el tiempo. Enla mayoría de las librerías de la plataforma hay métodos de bloqueo con versiones tanto con tiempo como sin tiempo. Si se termina el tiempo de espera, se marcará la tarea como fallida y se abortará o se encolará de nuevo para su posterior ejecución. Esto garantiza que cada tarea progrese satisfactoriamente o falle, dando oportunidad al restode tareas que se pueden completar más rápidamente.

### 4.8.2 Dimensionando los grupos de subprocesos

El tamaño ideal de un grupo de subprocesos depende del tipo de tarea que se va apresentar y las características del sistema implementado. El tamaño del grupo de hilos raramente se debería de pasar a mano, ya que el tamaño debería de ser cogido por un mecanismo de configuración consultando Runtime.availableProcessors. Dimensionar el tamaño del grupo de subprocesos no es una ciencia exacta, pero afortunadamente solo se deben evitar los extremos “demasiado grande” y “demasiado pequeño”. Si un grupo de subprocesos es demasiado grande, entonces los hilos competirán por los escasos recursos de memoria y CPU, provocando un mayor uso de la memoria y posiblemente saturación de los recursos. Si es demasiado pequeño, se desaprovecha rendimiento ya que procesadores estarán sin usar a pesar de tener trabajo disponible.
¿Entonces cual es la configuración idónea? Para tareas de cálculo intensivo, un sistema con N procesadores normalmente logra su estado óptimo de utilización con un grupo de subprocesos N+1 hilos. Para tareas que incluyan operaciones de I/O u otras operaciones que requieran bloqueos, se necesita un grupo mayor, ya que no todos los hilos serán planificables en todo momento. Entonces el tamaño idóneo del grupo se estimará del ratio del tiempo de espera respecto al tiempo de procesamiento de las tareas.
Ncpu = number of CPUs
Ucpu = utilización de la CPU, 0 ≤ Ucpu ≤ 1
W / C = ratio del tiempo de espera respecto al tiempo de procesamiento
Nthreads = Ncpu * Ucpu * ( 1 + W / C)
También se puede determiner el número de CPUs utilizando el Runtime:
int N_CPUS = Runtime.getRuntime ().availableProcessors ();
Naturalmente los ciclos de CPU no es el único recurso que se deba manejar utilizando grupos de subprocesos. Otros recursos que pueden contribuir al tamaño son la memoria,
los identificadores de archivos, los identificadores de sockets, y conexiones a la base dedatos. Para calcular el tamaño se suma cuantos recursos requiere cada tarea y se divide por la cantidad total disponible.

### 4.8.3 Configurando el ThreadPoolExecutor

ThreadPoolExecutor es, como su nombre lo indica, un pool de hilos, y en vez de estar creando un hilo para cada nueva tarea ( y con ello generar problemas de memoria cuando son muchos), se crean de antemano cierto número de hilos que serán ejecutados almismo tiempo, y cuando alguno termina su ejecución se asigna a otro proceso que esperaba su turno. Es algo así como un dispatcher.
Un ThreadPoolExecutor tiene un número determinado de hilos que se ejecutarán almismo tiempo, un número máximo de hilos, un timer para poder eliminar un hilo que ha estado parado por un determinado tiempo y una cola de espera para los hilos que tengan que esperar su turno.

```

class ThreadPoolExecutor implements ExecutorService (
int corePoolSize,
int maximumPoolSize,
long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue, ThreadFactory threadFactory, RejectedExecutionHandler handler
)

```

La cola de espera puede ser fija, dinámica o de transferencia, y de esto depende el comportamiento que tendrá el Executor:
- Fija: si se están ejecutando tantos hilos como el número determinado, la tarea sepone en la cola de espera: Si la cola está llena y llega un nuevo hilo a ella, revisa el número máximo de hilos. Si el número de hilos no ha rebasado el máximo, la ejecuta en uno nuevo. En caso contrario, la tarea es rechazada.
- Dinámica: si se están ejecutando tantos hilos como el número determinado, latarea siempre se pone en la cola de espera, por lo que en este caso el número máximo de hilos no importa porque nunca se revisa. Sin embargo, al momento de crear el ThreadPoolExecutor el número máximo de hilos tiene que ser mayoro igual al número determinado de hilos que se ejecutarán al mismo tiempo, o delo contrario el programa lanza una excepción.
- De transferencia: Crea un hilo para cada tarea sin siquiera intentar ponerlo en la
cola. La tarea es rechazada si no se puede ejecutar inmediatamente.
La cola de espera puede ser cualquier clase que implemente la interface BlockingQueue.
Hay que tener mucho cuidado con el número de hilos que se crean, independientemente de si son ejecutados en el acto o se ponen en la cola de espera: una gran cantidad dehilos lleva a problemas de memoria y errores raros aunque los métodos estén perfectamente sincronizados. Si de antemano se sabe el número máximo de tareas que serán ejecutadas, lo recomendable es usar una cola de espera fija.
RejectedExecutionHandler define la política con la que se descartan las tareas cuya ejecución es rechazada, bien por el proceso de shutdown o porque la cola de tareas es acotada y se está saturando. Hay varias implementaciones:
- AbortPolicy. Es la opción por defecto y lanza una excepción de rechazo de la
ejecución.
- CallerRunsPolicy. El caller es quien se encarga de tratar el desbordamiento.
- DiscardPolicy. Descarta las nuevas tareas si no se pueden encolar para su
ejecución.
- DiscardOldestPolicy. Descarta la próxima tarea que se va a ejecutar. En el casode que sea una cola de prioridades, la tarea que se descartará será la más prioritaria, por lo que esta opción no es buena en este caso.
La mayoría de los parámetros que se le pasan al constructor ThreadPoolExecutor se pueden modificar después de llamar a dicho constructor mediante setters. También existe la opción unconfigurableExecutorService que se le pasa al executor para que el servicio no se pueda modificar.

### 4.8.4 Ampliación de ThreadPoolExecutor

Se pueden realizar una serie de ampliaciones a las características de
ThreadPoolExecutor las cuales se deben de llamar desde el hilo que ejecuta la tarea ysirven para añadir temporizares, monitorizaciones o estadísticas:
- afterExecute se llama si la tarea finaliza de forma normal desde run o por saltar una excepción. Si la tarea finaliza con un error, afterExecute no se llama.
beforeExecute se llama y si se produce un RuntimeException la tarea no se ejecutará y por lo tanto no se llamará a afterExecute
Se debe llamar a terminated cuando el grupo completo de hilos termine el proceso,
después de que todas las tareas hayan terminado y todos los hilos estén cerrados. Se utiliza para liberar todos los recursos utilizados por executor durante todo su ciclo devida, mostrar alguna notificación o terminar las estadísticas.

## 4.9 APLICACIONES GUI ( GRAPHICAL USER INTERFACE)

Casi todos los kit de herramientas GUI, incluyendo Swing y SWT, son implementados como subsistemas individuales donde toda la actividad GUI esta en un solo hilo.

### 4.9.1 ¿Por qué son las GUI tratadas en un solo hilo?

Los frameworks GUI tratados en un solo hilo no son exclusivos de Java; QT, NextStep, MacOS Cocoa, X Windows, y muchos otros tambien los tratan de esta manera. Ha habido muchos otros intentos de escribir frameworks de GUI en multiples tratados en múltiples hilos pero debido a los constantes problemas con las condiciones de carrera e interbloqueos ( deadlocks) han acabado en el modelo de colas de eventos de hilos simples, donde un hilo dedicado busca eventos de una cola y los atiende con un controlador de eventos de aplicaciones definidas.
9.1.1. Procesamiento de eventos secuencial
Las aplicaciones GUI están orientadas a procesar eventos como el click del ratón, pulsar una tecla o expiraciones de tiempo. Los eventos son una clase de tarea. Debido a que solo hay un solo hilo para procesar tareas GUI, ellos son procesados secuencialmente, una tarea debe acabar antes de que la siguiente empiece. Esto hace que escribir el código sea fácil, ya que no debemos preocuparnos por las interferencias con otros hilos. La desventaja del procesamiento secuencial de tareas es que si una tarea toma mucho tiempo para ejecutarse, las otras deben esperar a que esta acabe. Si esas otras tareas son responsables de responder a las entradas del usuario proveyendo respuestas visuales, la aplicación parecerá haberse quedado colgada, ya que el usuario ni siquiera será capaz de cancelar la tarea, debido a que la acción del botón cancelar no será llamada hasta que laotra tarea acabe. Todos los componentes Swing ( tales como Jbutton y Jtable) y objetos de modelo dedatos ( como Tablemode y TreeMode) son confinados al hilo del evento, de tal forma que cualquier codigo que acceda al objeto debe ejecutarse en el hilo del evento. Los objetos GUI son consistentemente mantenidos no por sincronización, sino por confinamiento de hilos. La regla de los hilos simples Swing : Modelos y Componentes Swing, deberían ser creados, modificados y consultado tan solo por el hilo propio hilo que atiende su evento.

### 4.9.2 Tareas de ejecución corta

En una aplicación GUI, los eventos se originan en el hilo de evento, y llegan a los hilos que proveen aplicaciones, que probablemente llevaran a cabo alguna operación que afecte a la presentación de objetos. Para las sencillas tareas de corta ejecución, la completa acción puede permanecer en el hilo del evento, sin embargo, para tareas delarga ejecución algunos de los procesos deberían ser descargados desde otro hilo. En el caso simple, la confinación de los objetos presentados al hilo de eventos es natural. En el ejemplo vemos como se crea un botón cuyo color cambia aleatoriamente cuando es presionado.
Este ejemplo trivial caracteriza la mayoría de interacciones de entre las aplicaciones
GUI y los kit de herramientas GUI. Siempre que las tareas sean de ejecución corta, yaccedan únicamente a objetos GUI, ( u otros hilos que no compartan variables, u objetos de aplicación de hilo seguro), podemos ignorar totalmente las preocupaciones por otros hilos, y hacer todo desde el hilo del evento de una forma correcta. Una versión algo más complicada del mismo escenario, involucra el uso de un modelo formal de datos tal como “TableModel” o “treeModel”. Swindivide la mayoria de componentes visuales en dos objetos, un modelo ( model) y una vista ( view). De este modo, Los datos a ser mostrados residen en el modelo ( model) y las reglas que especifican como es mostrado residen en la vista ( view). Los objetos modelo pueden disparar eventos indicando que el modelo de datos ha cambiado y las vistas recogen esos eventos y entonces consultan al modelo para los nuevos datos y actualiza la visualización.

### 4.9.3 Tareas de ejecución Larga

Si todas las tareas fueran de ejecución corta, ( y la aplicación no significara nada en laparte no GUI), entonces la aplicación entera podría ejecutarse en el hilos de eventos yno tendríamos que preocuparnos por el resto de hilos. Sin embargo las aplicaciones GUIsofisticada podrían ejecutar tareas que podrían tardar más de lo que el usuario esta dispuesto a esperar, tales como, corrección de escritura, compilación de fondo ybúsqueda de nuevos recursos. Estas tareas deben ejecutarse en otro hilo de modo que
GUI sigue respondiendo mientras ellas se ejecutan. Swing hace fácil tener una tare ejecutable en el hilo de eventos, pero hasta Java 6 no provee ningún mecanismo para ayudar a las tareas GUI a ejecutar código en otras tareas. Pero no necesitamos Swing para ayudarnos aquí. Nosotros podemos crear nuestros propio “Executor” para procesar tareas de larga duración.. Empezamos con una tarea simple que no soporta cancelación o indicación de progreso,
y que no actualiza la GUI tras la focalización, y añade las características de una en una. A continuación vemos un ejemplo de la acción de un hilo que escucha, ligado a un componente visual, que somete una tarea de larga ejecución a un “Executor”. Este ejemplo muestra una tarea de larga duración,

```

ExecutorService backgroundExec = Executors.newCachedThreadPool ();
button.addActionListener ( new ActionListener () {
public void actionPerformed ( ActionEvent e) {
backgroundExec.execute ( new Runnable () {
public void run () { doBigComputation (); }
});
}
}
);

```

El siguiente ejemplo ilustra el modo obvio de hacer esto, que está empezando acomplicarse, ahora tenemos hasta tres niveles de clases interiores.

```

button.addActionListener ( new ActionListener () {
 public void actionPerformed ( ActionEvent e) {
button.setEnabled ( false);
label.setText ("busy");
backgroundExec.execute ( new Runnable () {
public void run () {
try {
doBigComputation ();
} finally {
GuiExecutor.instance ().execute ( new Runnable () {
public void run () {
button.setEnabled ( true);
label.setText ("idle");
}
});
}
}
});
 }
});

```

 La tarea disparada cuando el botón es presionado está compuesta de tres subtareas secuenciales, cuya ejecución alterna entre el hilo de eventos y el hilo de segundo plano. La primera tarea actualiza la interfaz de usuario para mostrar que una operación de larga ejecución ha empezado e inicia la segunda subtarea en un hilo en segundo plano. Cuando la primera es completada, la segunda encola la tercera subtarea para ejecutar denuevo en el hilo de eventos, que actualiza la interfaz de usuario para reflejar que la operación se ha completado.

### 4.9.4 Modelo de datos compartido

La representación de objetos Swing, incluyendo modelos de datos tales como
“TableModel” o “treeModel”, son confinados ( no comparten variables con otros hilos)
con el hilo de eventos. En programas GUI sencillos, todos los estados mutables son mantenidos en los objetos y el único hilo mas aparte del hilo de eventos es el hilo principal. En estos programas la regla es sencilla: no acceder al modelo de datos o los componentes desde el hilo principal.
9.4.1 Modelos de datos de hilo seguro
Los modelos de datos de hilo seguro deben ademas generar eventos cuando el modelo hasido actualizado, de modo que las vistas ( viewa) puedan ser actualizadas cuando los datos cambien.

### 4.9.5 Otras formas de subsistemas de hilo simple

El confinamiento de hilos no se limita a las GUIs, puede ser usado siempre algo se implemente como un subsistema de hilo simple.
 4.10 EVITANDO PROBLEMAS DE BLOQUEO INDEFINIDO ( LIVENESS)
Usamos bloqueos para asegurar la seguridad de nuestros hilos. Pero un uso indiscriminado de bloqueos puede causar interbloqueos permanentes ( deadlocks),
entendiendo como interbloqueo cuando un elemento bloquea a otro, y éste bloquea alque le bloqueó, produciéndose un interbloqueo permanente y un ( cuelgue) de la aplicación. Usamos grupos de subprocesos ( piscina de hilos) y semáforos para gestionar el consumo de los recursos limitados, y a veces provocamos interbloqueos
( deadlocks). Las aplicaciones Java no pueden recuperarse de estos interbloqueos, porello es importante que al programar se eviten las condiciones que puedan provocarlos.

### 4.10.1 Interbloqueos

El interbloqueo suele ser ilustrado por el clásico problema de la cena de los filósofos,
este es un problema clásico de las ciencias de la computación propuesto por Edsger
Dijkstra para representar el problema de la sincronización de procesos en un sistema operativo. Cabe aclarar que la interpretación está basada en pensadores chinos, quienes comían con dos palillos, donde es más lógico que se necesite el del comensal que se siente al lado para poder comer.
Cinco filósofos se sientan alrededor de una mesa y pasan su vida cenando y pensando. Cada filósofo tiene un plato de fideos y un tenedor a la izquierda de su plato. Para comer los fideos son necesarios dos tenedores y cada filósofo sólo puede tomar los que están a su izquierda y derecha. Si cualquier filósofo coge un tenedor y el otro está
ocupado, se quedará esperando, con el tenedor en la mano, hasta que pueda coger el otro tenedor, para luego empezar a comer.
Si dos filósofos adyacentes intentan tomar el mismo tenedor a una vez, se produce una condición de carrera: ambos compiten por tomar el mismo tenedor, y uno de ellos sequeda sin comer.
Si todos los filósofos cogen el tenedor que está a su derecha al mismo tiempo, entonces todos se quedarán esperando eternamente, porque alguien debe liberar el tenedor que les falta. Nadie lo hará porque todos se encuentran en la misma situación ( esperando que alguno deje sus tenedores). Entonces los filósofos se morirán de hambre. Este bloqueo mutuo es al que llamamos interbloqueo o deadlock.
Los sistemas de bases de datos son diseñados para detectar y recuperarse de los interbloqueos. Cuando el servidor de la base de datos detecta que algún grupo de transacciones esta interbloqueado, escoge una víctima y aborta la transacción. Esto libera los bloqueos que mantenía la víctima y las demás transacciones pueden proseguir. Pero la maquina virtual de Java ( JVM) no es tan útil resolviendo interbloqueos. Cuando una serie de hilos en java se interbloquean entre ellos, es el fin del juego para ellos.
Ejemplo : LeftRightDeadLock
// Warning: deadlock-prone!

```

public class LeftRightDeadlock {
private final Object left = new Object ();
private final Object right = new Object ();
public void leftRight () {
synchronized ( left) {
synchronized ( right) {
doSomething ();
}
}
}
public void rightLeft () {
synchronized ( right) {
synchronized ( left) {
doSomethingElse ();
}
}
}
}

```

Algunas posibles soluciones
Por turno cíclico
Se empieza por un filósofo, que si quiere puede comer y después pasa su turno al de la derecha. Cada filósofo sólo puede comer en su turno. Problema: si el número de filósofos es muy alto, uno puede morir de hambre antes de su turno.
Varios turnos
Se establecen varios turnos. Para hacerlo más claro supongamos que cada filósofo que puede comer ( es su turno) tiene una ficha que después pasa a la derecha. Si por ejemplo
hay 7 comensales podemos poner 3 fichas en posiciones alternas ( entre dos de las fichas quedarían dos filósofos).
Se establecen turnos de tiempo fijo. Por ejemplo cada 5 minutos se pasan las fichas ( ylos turnos) a la derecha.
En base al tiempo que suelen tardar los filósofos en comer y en volver a tener hambre,
el tiempo de turno establecido puede hacer que sea peor solución que la anterior. Si el tiempo de turno se aproxima al tiempo medio que tarda un filósofo en comer esta variante da muy buenos resultados. Si además el tiempo medio de comer es similar al tiempo medio en volver a tener hambre la solución se aproxima al óptimo.
Colas de tenedores
Cuando un filósofo quiere comer se pone en la cola de los dos tenedores que necesita. Cuando un tenedor está libre lo toma. Cuando toma los dos tenedores, come y deja libre los tenedores.
Visto desde el otro lado, cada tenedor sólo puede tener dos filósofos en cola, siempre los mismos.
Esto crea el problema comentado de que si todos quieren comer a la vez y todos empiezan tomando el tenedor de su derecha se bloquea el sistema
( deadlock). Resolución de conflictos en colas de tenedores
Cada vez que un filósofo tiene un tenedor espera un tiempo aleatorio para conseguir el segundo tenedor. Si en ese tiempo no queda libre el segundo tenedor, suelta el que tieney vuelve a ponerse en cola para sus dos tenedores.
Si un filósofo A suelta un tenedor ( porque ha comido o porque ha esperado demasiado tiempo con el tenedor en la mano) pero todavía desea comer, vuelve a ponerse en cola para ese tenedor. Si el filósofo adyacente B está ya en esa cola de tenedor ( tiene hambre) lo toma y si no vuelve a cogerlo A.
Es importante que el tiempo de espera sea aleatorio o se mantendrá el bloqueo del sistema.
El portero del comedor
Se indica a los filósofos que abandonen la mesa cuando no tengan hambre y que no regresen a ella hasta que vuelvan a estar hambrientos ( cada filósofo siempre se sienta enla misma silla). La misión del portero es controlar el número de filósofos en la sala,
limitando su número a n-1, pues si hay n-1 comensales seguros que al menos uno puede comer con los dos tenedores.
 4.11 RENDIMIENTO Y ESCALABILIDAD
Una de las mayores razones para utilizar los hilos es para mejorar el rendimiento. La utilización de hilos puede mejorar el uso de los recursos dejando que las aplicaciones aprovechen mejor la capacidad de procesamiento disponible y mejorando el rendimiento permitiendo que las aplicaciones puedan procesar nuevas tareas inmediatamente mientras aún hay otras taras en ejecución. Este capítulo trata técnicas de análisis, monitorización, y mejoras del rendimiento para programas concurrentes.
 4.11.1 Pensando en el rendimiento
Mejorar el rendimiento significa realizar más trabajo con menos recursos. Mientras quela finalidad es mejorar el rendimiento en general, el uso de varios hilos presenta algún coste de rendimiento frente al enfoque de un único hilo. Esto incluye la coordinación entre hilos ( bloqueos, señales y sincronización de memoria), el aumento de cambio de contexto, la creación y liberación de hilos, y planificarlo todo. Si el diseño con hilos es eficiente entonces estos costes están más que compensados en el rendimiento y en la capacidad de respuesta, pero por otro lado si el diseño no es bueno, la aplicación concurrente tendrá peor rendimiento que la misma aplicación de forma secuencial. Para lograr un mejor rendimiento utilizando concurrencia vamos a intentar hacer dos cosas: utilizar los recursos que tenemos más eficientemente, y de permitir a nuestro programa que utilice recursos adicionales en caso de que estén disponibles.
11.1.1 Rendimiento frente a escalabilidad
El rendimiento de la aplicación puede ser medido de varios modos, tales como tiempo de servicio, latencia, rendimiento, eficiencia, escalabilidad, o capacidad. Algunos deestos miden lo rápido que son a partir de una unidad de trabajo y otros miden cuanto trabajo desempeñar con una cantidad de recursos proporcionados. La escalabilidad describe la habilidad de mejorar el rendimiento o capacidad cuando se añaden recursos adicionales, como CPUs, memoria, almacenamiento o ancho de bandade I/O.
11.1.2 Evaluar las ventajas y desventajas del rendimiento
Prácticamente en todas las decisiones en ingenierías hay un estudio de ventajas ydesventajas, por ejemplo, usando un acero más grueso en un puente puede aumentar su capacidad y seguridad, pero también aumentará su coste de construcción. En ingeniería del software no suele haber decisiones sobre ventajas y desventajas entre el dinero y la seguridad de la personas, pero normalmente hay menos información para crear un buen estudio de ventajas y desventajas. Por ejemplo, el método quicksort es muy eficiente para grandes conjuntos de datos, pero sin embargo el método burbuja es más eficiente en conjuntos pequeños de datos. Por eso si se quiere implementar una ordenación eficiente, habrá que saber la cantidad de datos que se van a tratar, y lo mismo no se tiene ese dato de antemano, por lo que la mayoría de optimizaciones son prematuras. Muchos programadores intuyen si una aplicación es mejor realizarla secuencialmente omediante concurrencia. Pero esto no es correcto, ya que para una correcta implementación de nuestra aplicación se deben de medir todas las mejoras y ver si realmente merece la pena respecto al coste.

### 4.11.2 La ley de Amdahl

La Ley de Amdahl establece que la mejora obtenida en el rendimiento de un sistema debido a la alteración de uno de sus componentes está limitada por la fracción de tiempo que se utiliza dicho componente.
En el caso de que el número de procesadores ( n) tienda a infinito, el máximo rendimiento tenderá a 1/Wl.
 4.11.3 Costes de los hilos
Los programas de un único hilo no necesitan planificación o sincronización, y no necesitan bloqueos para conserv1ar la consistencia de las estructuras de datos. Sin embargo, en sistemas multihilo éstos conllevan un coste en el rendimiento, por lo que habrá que estudiar los beneficios de la paralelización presentado por la concurrencia.
 4.12 RECOMENDACIONES
Utilizando el lenguaje Java, para crear concurrencia de memoria común, tenemos
los siguientes conceptos a tener en cuenta.
- La máquina virtual es un único proceso dentro del cuál tendremos una seriede hilos del propio sistema de ejecución más el hilo denominado main quees el hilo para ejecutar el programa de usuario más los hilos que se creen desde éste. ( Ver sesiones de laboratorio)
- Para la creación de hilos se precisa el uso de la clase Thread, bien heredando de ella, bien instanciando directamente y alimentando con un objeto
Runnable. ( Ver sesiones de laboratorio)
- Cada hilo en Java es un objeto cuyo contenido de ejecución simultánea está
en el interior del método run. Cuando este método termina, el hilo termina.
( Ver sesiones de laboratorio)
- La parte dinámica del programa concurrente, los hilos, se complementa conlos datos compartidos por estos hilos. El acceso a estos datos es la parte realmente importante de la concurrencia ya que son las base para la actividad global del programa.
- El acceso a los datos debe ser protegido. La mayoría de las clases que se programan en Java contiene código que no protege sus datos. Este código es vulnerable frente a los errores adicionales que plantea la concurrencia yque se dan no sólo cuando creamos hilos de forma consciente ya que muchos frameworks que podemos usar crean hilos ( servlets, Swing, etc.)
- Para crear clases con protección sobre sus datos, es necesario el uso de
bloqueos y otros mecanismos.
- Todo objeto Java puede se utilizado para crear un bloqueo, bien para usarlo
dentro de dicho objeto, bien para usarlo desde otros.
 4.12.1 Soluciones para compartir variables.
Como ya hemos visto, el uso de variables compartidas por varios hilos es fundamental para que los programas concurrentes cooperen y produzcan un resultado correcto. Por tanto, será fundamental identificar todas las secciones críticas en el código yprotegerlas frente a posibles inconsistencias o pérdidas de corrección de los programas. En definitiva, tenemos que evitar la situaciones en las que se depende de las “race condition” o
“data race”.
Por otro lado, las soluciones para el tratamiento de los datos en concurrencia,
además de asegurar la exclusión mutua de los accesos, necesita conseguir la visibilidad de la información.
Para esto, el lenguaje provee varios mecanismos cada uno de ellos con limitaciones y distintos niveles de seguridad. Los niveles de seguridad no implican que no exista seguridad en alguno de ellos. Tan sólo que son capaces de proporcionar seguridad en situaciones más o menos complicadas.
Hay 3 niveles:
9. Synchonized. Con este mecanismo se consigue el máximo nivel de seguridad. Se trata de bloqueos explícitos o intrínsecos, lock, que usando un objeto o clase como referencia de bloqueo, asegura la exclusión mutua de
un fragmento de código frente a cualquier otro que adquiera un bloqueo sobre el mismo objeto o clase.
10. Atomic. Librería disponible en java.util.concurrent.atomic que contiene diversas clases para datos cuyas operaciones están implementadas para ser atómicas. El uso de estas clases para definir el estado de un objeto, puede servir para asegurar su protección frente al uso por varios hilos, siempre queel estado del objeto no esté formado por varios elementos. En dichas situaciones esto no será suficiente.
11. Volatile. Esta características, aplicable a los atributos, previene al compilador de que serán usados de forma simultánea por varios hilos y por tanto se evita la reordenación del código y el almacenamiento en cache
( ambas acciones realizadas por el compilador para optimizar el código). Este mecanismo es el más débil ya que no asegura la exclusión mutua enmodo alguno, sólo la visibilidad de los datos.
 4.12.2 Recomendaciones para crear los programas.
La primera recomendación fundamental es utilizar el encapsulamiento siempre quesea posible. En realidad, es difícil encontrar una situación en la que sea necesario utilizar campos públicos. Evitarlo a toda costa es un primer paso para hacia la seguridad.
Utilizar campos constantes ( inmutables, marcados con final) siempre que sea
posible. Todo campo constante es seguro para su uso en concurrencia.
Bloquear siempre todo uso de variables modificables ( mutables) mediante bloques synchronized sobre el mismo objeto ( para cada variable o para el estado de cada objeto, usar distintos objetos como bloqueo si son independientes). Se bloquearán, las lecturas igual quelas escrituras.
Utilizar el modificador Volatile cuando el campo que se comparte no es necesario hacerlo de forma sincronizada. De esta forma se conseguirá que los datos leídos sean consistentes.
Utilizar objetos de las clases atomic cuando el estado a proteger del uso concurrente
esté formado por un único campo.
No diseñar los programas pensando en el rendimiento, hacerlo pensando en la
seguridad y luego optimizándo.
Considerar siempre la posibilidad de uso concurrente de nuestras clases y la
seguridad de su uso.
