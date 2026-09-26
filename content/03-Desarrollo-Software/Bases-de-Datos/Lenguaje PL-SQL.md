---
title: "Lenguaje PL-SQL"
---

# Lenguaje PL/SQL
# INTRODUCCIÓN 
Hasta ahora hemos trabajado con la BD de manera más o menos *interactiva*. Esto supone que todos los usuarios tendrían que conocer SQL. Desde luego, esta forma de proceder no resulta operativa en un entorno real de producción.
Para superar estas limitaciones, Oracle incorpora un gestor en el servidor de la BD denominado **PL/SQL**. Esto es un lenguaje en toda regla dado que incorpora manejo de variables, estructura modular ( procedimientos y funciones), estructuras de control ( bifurcaciones, bucles, ...), control de excepciones, etc.
<u>Estos programas escritos en PL/SQL tienen la ventaja de que se pueden almacenar en la base de datos como cualquier otro objeto. De esta manera su disponibilidad y acceso es inmediata</u>.
El uso del lenguaje PL/SQL es también necesario para crear **disparadores de bases de datos** que permitan implementar reglas complejas de negocio y auditoria en la BD.
Todo ello hace de PL/SQL un lenguaje prácticamente imprescindible para trabajar en un entorno Oracle, tanto para administradores de la base de datos como desarrolladores de aplicaciones.
## INTRODUCCIÓN FORMATO PL/SQL
Tal y como hemos mencionado previamente, Sql**plus es una herramienta que sirve para ejecutar órdenes SQL y programas y procedimientos escritos en el lenguaje de programación PL/SQL, que no es otra cosa que una extensión del lenguaje SQL. En definiciones de la propia empresa:
> “SQL**PLUS: Es un lenguaje basado en SQL e interactivo utilizado para la manipulación de datos y la definición de accesos correctos a una base de datos ORACLE. A menudo es usada como una herramienta de informes para usuario final.”
>
> “PL/SQL: es una extensión, en lenguaje procedural creada por Oracle, del lenguaje SQL. Combina la facilidad y flexibilidad del SQL con la funcionalidad procedural de un lenguaje de programación estructurado ( if … then, while o for … loop, etc …).”
PL/SQL es un lenguaje que tiene como unidad de trabajo los **bloques**, que no son más que conjuntos de declaraciones, sentencias y excepciones ( o controles). Permite utilizar dentro de estos bloques estructuras condicionales, bucles, etc. Por este motivo podremos hacer tareas y procesos que no podríamos hacer solo con SQL.
Y un programa hecho en una versión funciona casi perfectamente en otras ( seguramente con pequeños cambios) y también funciona con distintos sistemas operativos.
## Bloques
PL/SQL trabaja con bloques cuyo formato es:
*[ DECLARE*
*declaraciones de variables ]*
***BEGIN***
*Órdenes;*
*[ EXCEPTION*
*Tratamiento de excepciones ( controles o errores) ]*
***END ;***
***/***
Solamente son obligatorias las líneas
BEGIN
órdenes;
END;
es decir, el programa más simple sería
BEGIN
NULL;
END;
Estos bloques, además, *se pueden anidar en las secciones BEGIN y EXCEPTION*. Sin embargo, <u>no se permite la anidación en la sección DECLARE</u>. El siguiente programa también es valido:
BEGIN
> BEGIN
>
> NULL;
>
> END;
END;
/
<u>La utilización de bloques supone una notable mejora de rendimiento ya que se envían los bloques completos al servidor para que sean procesados en lugar de cada sentencia SQL. Así se ahorran muchas operaciones de E/S.</u>
El símbolo **“/”** hace que se guarde el bloque en el buffer y lo envía al servidor para su ejecución.
## Comentarios
En PL/SQL podemos ya introducir comentarios como en todos los programas, y lo hacemos de dos formas:
- Para poner un comentario en una línea se utilizan los guiones “--”.
- Para utilizar más de una línea de comentario ponemos los signos “/*” para el inicio y “*/” para el final.
Podemos pues “complicar “ nuestro programa.
- Ejemplo (`Scripts\PLsql_1.sql`):
```sql
BEGIN -- mi primer programa
/* Mi primer programa tiene
muchos comentarios */
NULL;
END; -- final de mi primer programa
/
```
## Mensajes por pantalla
PL/SQL es un lenguaje diseñado para trabajar con la base de datos y manejar grandes volúmenes de datos de manera eficaz. No ha sido diseñado para interacturar con el usuario por lo que no dispone de órdenes para la captura de datos introducidos por el usuario, ni tampoco para visualizarlos por pantalla. Para estos propósitos se utilizan otros lenguajes y o herramientas, desde donde PL/SQL puede ser invocado. Sin embargo, con el objeto de **“depurar”** los programas PL/SQL, Oracle incorpora el paquete **DMBS_OUTPUT** y un procedimiento, dentro de éste, denominado **PUT_LINE** para visualizar mensajes por pantalla.
Estos son los comentarios dentro de un programa, y para que nos vaya mostrando por pantalla mensajes de comprobación, como un “debug”, utilizamos la orden:
***DBMS_OUTPUT.PUT_LINE** (‘mensaje’ o variable || ... ||‘mensaje’ o variable);*
Para activar esta opción:
Utilizar el comando de sql**plus **SET SERVEROUTPUT ON** y después ( opcionalmente y dependiendo del entrono utilizado) en el programa usar la sentencia **DBMS_OUTPUT.ENABLE.**
*Por defecto la salida por pantalla está desactivada.*
```sql
<u>Ejemplo</u>: Mensajes por pantalla `( Scripts\PLsql_2.sql`).
SQL\> SET SERVEROUTPUT ON
BEGIN -- mi primer programa
/ Mi primer programa tiene muchos comentarios /
/* Si no se ve nada por pantalla utilizar
DBMS_OUTPUT.ENABLE;
**/*
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE ('Mi primer mensaje.');
END; -- final de mi primer programa
/
<u>NOTA</u>: Si hay problemas con los caracteres debido al conjunto de caracteres de la BD. Intentar modificarlo con:
ALTER DATABASE mi_base NATIONAL CHARACTER SET WE8ISO8859P1.
Para averiguar los valores actuales se puede utilizar: SELECT parameter, value FROM nls_database_parameters.
```
## Introducción de datos
Para pasar datos a un programa PL/SQL se pueden realizar alguna de las siguientes opciones:
- Introducir los datos en una tabla y, después leerlos desde el programa.
- Pasar los datos como parámetros en la llamada a través de procedimientos o funciones.
- Utilizar variables de sustitución SQL**Plus. <u>Esta opción solamente puede utilizarse con bloques anónimos</u>, ya que SQL**Plus realizará la sustitución antes de enviar el bloque al servidor.
```sql
<u>Ejemplo</u>: (`Scripts\PLsql_3.sql)`
SQL\> SET SERVEROUTPUT ON
DECLARE
v_nombre_dep departamentos.nombre%TYPE;
BEGIN -- comienza el programa
*/**
Este programa hace uso de variables de sustitución SQL**Plus
**/*
DBMS_OUTPUT.ENABLE;
SELECT nombre
INTO v_nombre_dep
FROM departamentos
WHERE cod_depto = &vn_cod_dep;
DBMS_OUTPUT.PUT_LINE ('El departamento es : ' || v_nombre_dep);
END;
/
![]( 2cuatri/SistemasEmpotrados/TrabajoGrupal/_media/Plantilla-Trabajo-GrupoMIo/media/image1.png)
```
# VARIABLES, CONSULTAS Y EXCEPCIONES
## VARIABLES 
Las variables PL/SQL sirven, al igual que en cualquier otro lenguaje de programación, para almacenar información cuyo valor puede cambiar a lo largo de la ejecución del programa.
## Declaración en inicialización de variables
Las variables que utilizan los bloques de PL/SQL se declaran en la sección DECLARE. El formato que se utiliza es:
***nombre_variable tipo_de_variable** [NOT NULL] [:= valor_inicial];*
y hay que crearlas antes de utilizarlas ( excepto en las estructuras FOR que veremos más adelante). Los tipos más usuales son:
- Number o Number ( ) o Number ( , ) para datos numéricos.
- Char () y Varchar2 ( ) para caracteres.
- Date para fechas ( se mueven en un rango, en v.7 era 1 Ene, -4712 hasta 31 Dic. 4712).
- Boolean que pueden ser TRUE, FALSE o NULL.
## Atributos %TYPE y %ROWTYPE
Estos atributos sirven para declarar variables del mismo tipo que otros objetos ya previamente definidos.
- %TYPE**: asignamos el mismo tipo, que otra variable o, que una columna de una tabla.
- %ROWTYPE**: mismo tipo que un registro.
y cuyo formato es respectivamente:
*variable \<tabla.columna o variable\>**%TYPE**;*
*variable \<tabla o variable\>**%ROWTYPE**;*
<u>Ejemplo</u>:
*Nombre_comprador clientes.nombre**%TYPE**;*
Declara la variable *nombre_comprador* del mismo tipo que la columna *nombre* de la tabla *Clientes*.
## Ámbito y visibilidad de las variables
El ámbito de una variable queda enmarcado dentro del bloque en el que se declara, incluyendo sus bloques hijos.
Una variable será **local** para el bloque en el que ha sido declarada y **global** para los bloques hijos de aquel. <u>Las variables declaradas en los bloques hijo no son accesibles desde el bloque padre.</u>
```sql
DECLARE -- Bloque padre
v1 NUMBER;
BEGIN
v1 := 23;
DECLARE -- Bloque hijo
v2 NUMBER;
BEGIN
v2 := 21;
v1 := 25;
…
END;
v2 := 30; -- ERROR, v2 está fuera de ámbito
v1 := 19;
END;
/
```
En el caso de que un identificador local coincida con uno global, se referenciará el local. Esto es, el identificador local dentro de su ámbito oculta la visibilidad del global. No obstante, se pueden utilizar y cualificadores para deshacer la ambigüedad.
## SELECT ... INTO 
PL/SQL permite ejecutar cualquier consulta pero su resultado no se muestra automáticamente en el terminal del usuario, sino que queda en un área de memoria denominada **cursor** a la que se accede utilizando *variables*.
Por ejemplo, para obtener el número total de empleados:
```
SELECT COUNT (**) FROM Empleados;
dará error en PL/SQL.
Lo correcto es:
**SELECT** COUNT (**) **INTO** v_total_emple FROM Empleados;
que ejecuta la consulta y deposita el resultado en la variable *v_total_emple* que debe haber sido declarada previamente. A este tipo de cursores se les denomina **cursores implícitos**, puesto que necesitan ser declarados.
Para asignar un valor a las variables podemos hacerlo de tres formas:
- En el DECLARE ( siempre debe hacerse).
- En sentencias dentro de la parte ejecutable del bloque, con sentencias como
variable := \<expresión\>;
- Y por último la sentencia SELECT..INTO.. ( que hemos visto anteriormente) y cuyo formato es:
> ***SELECT** columna1, columna2, ... , columna n*
>
> ***INTO** variable1, variable2, ... , variable n*
>
> ***FROM** tabla*
>
> *[WHERE condiciones]*
>
> *[ORDER BY expresiones]*
>
> *[GROUP BY expresiones]*
>
> *[HAVING condiciones];*
<u>Ejemplo</u>: Hacer un programa que saque por pantalla el nombre del departamento al que pertenece un determinado empleado. Este ejemplo `( Scripts\PLsql_4.sql`) llegado el momento, se puede transformar fácilmente en una función.
```sql
DECLARE
v_nombre_dep departamentos.nombre%TYPE;
BEGIN -- comienza el programa
*/**
Este programa saca por pantalla el nombre del departamento
al que pertenece un determinado empleado
**/*
DBMS_OUTPUT.ENABLE;
SELECT nombre
INTO v_nombre_dep
FROM departamentos
WHERE cod_depto = ( SELECT depto
FROM empleados
WHERE nombre = 'ANA'
AND apell1 = 'GOMEZ');
DBMS_OUTPUT.PUT_LINE ('El departamento es : ' || v_nombre_dep);
END;
/
```
## EXCEPCIONES
```
Cuando PL/SQL detecta una excepción, pasa automáticamente el control del programa a la sección **EXCEPTION**. Allí buscará un **manejador** ( cláusula WHEN) para la excepción producida o uno genérico ( WHEN OTHER). Al finalizar este tratamiento, sale del bloque actual y devuelve el control al programa o herramienta que realizó la llamada.
El formato que se utiliza es:
***EXCEPTION***
*WHEN \<tipo de error1\> THEN*
*sentencia11;*
*...*
*WHEN \<tipo de error2\> THEN*
*sentencia21;*
.
<u>El tipo de error puede ser tipificado o definido por el usuario</u>. Entre los tipificados los más comunes son:
- NO_DATA_FOUND** la select no recupera datos;
- TOO_MANY_ROWS**: la select recupera demasiados datos;
- DUP_VAL_ON_INDEX**: cuando intenta insertar un registro duplicado violando la unicidad de un índice.
- INVALID_NUMBER**: cuando en un tipo de dato numérico intentamos meter caracteres.
- OTHERS**: cuando ocurre algún error no tratado.
```sql
<u>Ejemplo</u>: igual que el ejemplo 4 pero añadiendo excepciones `( Scripts\PLsql_5.sql`)
SET SERVEROUTPUT ON
DECLARE
v_nombre_dep departamentos.nombre%TYPE;
BEGIN -- comienza el programa
DBMS_OUTPUT.ENABLE;
*/**
Este programa saca por pantalla el nombre del departamento
al que pertenece un determinado empleado y emplea excepciones
**/*
SELECT nombre
INTO v_nombre_dep
FROM departamentos
WHERE cod_depto = ( SELECT depto
FROM empleados
WHERE nombre = 'EVA'
AND apell1 = 'GARCIA');
DBMS_OUTPUT.PUT_LINE ('El departamento es : ' || v_nombre_dep);
EXCEPTION
WHEN NO_DATA_FOUND THEN
DBMS_OUTPUT.PUT_LINE ('No está en ningún departamento.');
WHEN TOO_MANY_ROWS THEN
DBMS_OUTPUT.PUT_LINE ('Mas de un departamento tiene empleados con estos datos.');
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE ('Ocurrió otro tipo de error: '||SQLERRM);
END;
/
```
Para las excepciones definidas por el usuario el proceso es el siguiente:
- En el DECLARE se le da un nombre a la excepción y el tipo excepción de la siguiente manera:
DECLARE
**\<etiqueta\> exception**;
- En el programa dentro de un bloque se le hace saltar con un **RAISE**:
> BEGIN
>
> **RAISE \<etiqueta\>;**
- Dentro del mismo bloque se le trata en las excepciones:
> EXCEPTION
>
> WHEN \<etiqueta\> THEN
>
> ... ;
>
> END;
<u>Ejemplo</u>: Excepciones personalizadas `( Scripts\PLsql_6.sql`). Vamos a añadir una excepción personalizada al ejemplo anterior y la hacemos saltar. La excepción preguntará si la empresa quiere privacidad y si el valor introducido es ‘S’ dará un aviso en lugar de mostrar el resultado.
```sql
SET SERVEROUTPUT ON
DECLARE
v_nombre_dep departamentos.nombre%TYPE;
v_privacidad CHAR ( 1) := '&Privacidad';
e_privacidad EXCEPTION;
BEGIN -- comienza el programa
DBMS_OUTPUT.ENABLE;
*/**
Este programa saca por pantalla el nombre del departamento
al que pertenece un determinado señor
**/*
SELECT .nombre
INTO v_nombre_dep
FROM departamentosa
WHERE cod_depto = ( SELECT depto
FROM empleados
WHERE nombre = 'ANA'
AND apell1 = 'GOMEZ');
IF ( v_privacidad = 'S') THEN
RAISE e_privacidad;
ELSE
DBMS_OUTPUT.PUT_LINE ('El departamento es : ' || v_nombre_dep);
END IF;
EXCEPTION
WHEN e_privacidad THEN
DBMS_OUTPUT.PUT_LINE ('Política de PRIVACIDAD de la Empresa.');
WHEN NO_DATA_FOUND THEN
DBMS_OUTPUT.PUT_LINE ('No está en ningún departamento.');
WHEN TOO_MANY_ROWS THEN
DBMS_OUTPUT.PUT_LINE ('Mas de un departamento tiene empleados con estos datos.');
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE ('Ocurrió otro tipo de error: ' || SQLERRM);
END;
/
```
# ESTRUCTURAS DE CONTROL
Cuando definíamos PL/SQL decíamos que era “una extensión procedural del lenguaje SQL” y que tenía “la funcionalidad procedural de un lenguaje de programación estructurado”. En este capítulo empezamos a encontrarnos estructuras comunes de los lenguajes de programación estructurada ( Pascal, Fortran, C y otros). Dichas estructuras son, principalmente, las condicionales ( IF…THEN) y las repetitivas ( LOOP…END LOOP, WHILE-LOOP…END LOOP y FOR-LOOP…END LOOP).
## ESTRUCTURAS CONDICIONALES
En las **estructuras condicionales** tenemos la forma **IF…THEN**, que permite elegir entre ejecutar unas órdenes, otras o nada dependiendo de una o varias condiciones. Su formato es:
> ***IF** condición1 **THEN***
>
> *órdenes1;*
>
> *[ **ELSIF** condición2 **THEN***
>
> *órdenes2; ]*
>
> ***…***
>
> *[ **ELSE***
>
> *órdenes ; ]*
>
> ***END IF** ;*
Si la ‘condición1’ es verdadera se ejecutan las ‘ordenes1’, si la ‘condición2’ es la verdadera y no se cumplía la ‘condición1’ se ejecutan las ‘órdenes2’. Para que esté bien programado las condiciones 1 y 2 deben ser excluyentes. En el caso de que no se cumpla ninguna de las condiciones se ejecutan las órdenes de la cláusula ELSE. Y si no hay cláusula ELSE simplemente no ejecuta nada y pasa a la orden siguiente.
Entre las órdenes que se ejecutan cuando se cumple una condición puede haber a su vez otra estructura condicional, es decir, <u>se pueden anidar IF´s</u>.
<u>Ejemplo</u>: Forma IF … THEN. Como ejemplo puede valernos el ejemplo anterior con una pequeña modificación `( Scripts\PLsql_7.sql`).
```sql
IF ( UPPER ( v_privacidad) = 'S') THEN
RAISE e_privacidad;
ELSIF ( UPPER ( v_privacidad) = 'N' ) THEN
DBMS_OUTPUT.PUT_LINE ('El departamento es: ' || v_nombre_dep);
ELSE
DBMS_OUTPUT.PUT_LINE ('Valores válidos para privacidad: S o N.');
END IF;
```
En las **estructuras condicionales** también tenemos la estructura **CASE**, que es equivalente a la alternativa múltiple ELSIF.
> ***CASE** expresión*
>
> ***WHEN** condición1 **THEN***
>
> *Órdenes1;*
>
> ***WHEN** condición2 **THEN***
>
> *Órdenes2;*
>
> ***…***
>
> *[ **ELSE***
>
> *órdenes ; ]*
>
> ***END CASE** ;*
<u>Ejemplo</u>: Forma CASE `( Scripts\PLsql_8.sql).`
```sql
CASE UPPER ( v_privacidad)
WHEN 'S' THEN
RAISE e_privacidad;
WHEN 'N' THEN
DBMS_OUTPUT.PUT_LINE ('El departamento es: ' || v_nombre_dep);
ELSE
DBMS_OUTPUT.PUT_LINE ('Valores válidos para privacidad: S o N.');
END CASE;
```
## ESTRUCTURAS REPETITIVAS
En las **estructuras repetitivas** tenemos la forma:
> ***LOOP***
>
> *Órdenes;*
>
> ***END LOOP;***
que es simplemente un bucle infinito. Evidentemente o salimos de él de alguna forma o hemos cometido un error de programación ( si no estamos preparando algún virus o similar). Para salir, una de las órdenes que ha de contener el bucle va a ser **EXIT** y lo normal será que esté dentro de una estructura condicional, como en el siguiente ejemplo.
Una abreviatura existente para la condicional con orden EXIT es
> ***EXIT WHEN** ( n_vueltas = n_orden_termino);*
por ejemplo para el ejemplo anterior, se sustituiría
> *IF ( n_vueltas = n_orden_termino ) THEN*
>
> **EXIT;**
>
> *END IF;*
por EXIT WHEN ( n_vueltas = n_orden_termino);
Una segunda estructura repetitiva, derivada de la anterior es la que tiene por formato
***WHILE** condición **LOOP***
*Órdenes;*
***END LOOP;***
que se diferencia de la anterior en que la condición para salir del bucle infinito se saca fuera de la estructura de órdenes con lo cual no se tiene porqué entrar tan siquiera en el bucle. Esta sintaxis es mucho más habitual que la anterior.
Y por último, el bucle FOR-LOOP .. END LOOP cuyo formato es:
> ***FOR** variable **IN** [REVERSE] mínimo..máximo **LOOP***
>
> *Órdenes;*
>
> ***END LOOP*;**
Este bucle tampoco necesita una sentencia EXIT y en cuanto a la variable decir que no necesita ser declarada. Esto es muy interesante y como veremos más adelante es muy utilizada en los cursores pues evitará abrir, llamar y cerrar un cursor..
La opción ***REVERSE*** hace que los pasos de la variable se produzcan de forma inversa, es decir del máximo al mínimo.
<u>Ejemplo</u>. For. Calcular el factorial de n `( Scripts\PLsql_9.sql).`
```sql
DECLARE
n_fact NUMBER := 1;
n NUMBER := 5;
BEGIN
FOR i IN 1..n LOOP
n_fact := n_fact**i;
END LOOP;
DBMS_OUTPUT.PUT_LINE ('Factorial: ' || n_fact);
END;
```
# DATOS COMPUESTOS Y CURSORES
Un tipo compuesto se compone de partes que pueden ser manipuladas individualmente. Nos podemos encontrar dos tipos: *registros* (***RECORD***) y *colecciones* (***TABLE*** y ***VARRAY***).
## REGISTROS. RECORD
Un **RECORD** o registro es un grupo de elementos de datos relacionados. Se relacionan por algún criterio lógico. Es el caso, por ejemplo, del nombre y apellidos de una persona que muchas veces son entendidos como un todo. Se declaran en la forma:
> ***TYPE** nombre **IS RECORD** ( nombre_campo[,declaracion_campo]...);*
Donde la declaración del campo está compuesta por :
> *nombre_campo tipo_campo [[NOT NULL] {:= | DEFAULT} expresión]*
<u>Ejemplo</u>: Definir un tipo registro que almacene el nombre y apellidos de un empleado.
> ***TYPE** nombre_persona **IS RECORD** (*
>
> *chr_nombre empleados.nombre%TYPE,*
>
> *chr_apellido1 empleados.apell1%TYPE,*
>
> *chr_apellido2 empleados.apell2%TYPE*
>
> *);*
Los tipos registro podemos inicializarlos en la definición inicial como se hacía para los campos de una tabla. E incluso, también añadir una restricción de tipo NOT NULL, por ejemplo:
<u>Ejemplo:</u> Inicializar en la definición.
```sql
DECLARE
TYPE nombre_persona IS RECORD (
nombre CHR ( 25) NOT NULL := ‘Desconocido’,
apellido1 CHR ( 25) NOT NULL := ‘Desconocido’,
apellido2 CHR ( 25) := ‘X’ );
BEGIN
...
END;
```
Igualmente pueden inicializarse en el cuerpo del programa con una sentencia de asignación y haciendo referencia a ellos con el nombre del registro, un punto y la componente, por ejemplo:
<u>Ejemplo:</u> Inicializar entre BEGIN y END..
```sql
DECLARE
TYPE nombre_persona IS RECORD (
nombre empleados.nombre%TYPE,
apellido1 empleados.apell1%TYPE,
apellido2 empleados.apell2%TYPE);
BEGIN
nombre_persona.nombre := ‘MARTIN LUTHER’;
nombre_persona.apellido1 := ‘KING’;
nombre_persona.apellido2 := NULL;
...
END;
```
## COLECCIONES. TABLE y VARRAY
Los tipos definidos para ***colecciones***, **TABLE** y **VARRAY** permiten declarar tablas por índice, tablas jerarquizadas y matrices de tamaño variable. <u>Una **colección** es un grupo ordenado de elementos del mismo tipo</u>. Cada elemento tiene un subíndice único que determina su posición en la colección.
Y para referenciar un cierto elemento se usa su sintaxis estándar. Por ejemplo, la siguiente llamada referencia al 5º elemento de una tabla jerarquizada y devuelta por una función ( concepto éste que veremos posteriormente):
> *DECLARE*
>
> *fecha_referencia DATE := TO_DATE (’01/09/2006’,’DD/MM/RRRR’);*
>
> ***TYPE** t_empleados **IS TABLE OF** empleados;*
>
> *v_empleado empleado;*
>
> *FUNCTION incorporados_desde ( fecha_alta DATE)*
*RETURN t_empleados IS*
```sql
BEGIN
...
END;
BEGIN
v_empleado := incorporados_desde ( fecha_referencia)( 5);
...
END;
```
PL/SQL ofrece estos tipos de colecciones:
- Tablas por índice** ( index-by tables): permiten buscar elementos usando números arbitrarios y cadenas de caracteres, para los valores referenciados.
- Tablas jerarquizadas** ( Nested tables): mantienen un número arbitrario de elementos. Utilizan números secuenciales como subíndices. Se puede definir tipos equivalentes SQL, permitiendo que las tablas jerarquizadas sean almacenadas en tablas de la base de datos utilizando SQL. En éstas, a diferencia de las anteriores, es muy importante el orden de los registros en la tabla.
- Matrices de tamaño variable** ( Varrays): mantienen un número fijo de elementos ( aunque se puede cambiar el número de elementos en ejecución). Utilizan números secuenciales como subíndices. Se pueden definir tipos equivalentes SQL, permitiendo que los varrays sean almacenados en tablas de la base de datos. Pueden ser almacenadas y ser recuperadas con el SQL, pero con menos flexibilidad que las tablas jerarquizadas.
## Tablas por índice o indexadas
Las tablas indexadas se basan en sistemas de pares clave-valor, donde la primera es única y se utiliza para localizar el valor correspondiente en la tabla. La clave puede ser un número entero o una secuencia. Es importante elegir una clave que sea única, bien usando la clave primaria de una tabla del SQL, o concatenando secuencias juntas para formar un valor único.
La sintaxis utilizada es:
> *TYPE \<nombre_tipo\> IS TABLE OF \<elemento_tipo\> [NOT NULL]*
***INDEX BY** \<tipo_llave\>;*
siendo:
***INDEX BY** [BINARY_INTEGER | PLS_INTEGER | VARCHAR2 ( \<limite_tamaño\>)];*
donde *nombre_tipo* es el tipo específico que se usará después para declarar colecciones. Y *elemento_tipo* es cualquier tipo definido. *Tipo_llave* puede ser numérico, como BINARY_INTEGER o PLS_INTEGER. También puede ser VARCHAR2 o uno de sus subtipos VARCHAR, STRING, o LONG. Se debe especificar la longitud en estos últimos, excepto para LONG que es equivalente a declarar VARCHAR2 ( 32760). Los tipos RAW, LONG RAW, ROWID, CHAR, y CHARACTER no son permitidos como llaves. Tampoco se pueden utilizar cláusulas de inicialización.
<u>Para acceder a los elementos se pone el nombre de la variable y, entre paréntesis, el número del elemento: nombre_variable ( indice).</u>
Se van a ver dos ejemplos: un primer ejemplo sencillo sin utilizar tablas de la base de datos, y un segundo ejemplo más complejo con tablas en BD.
<u>Ejemplo</u>. Index-by tables `( Scripts\PLsql_10.sql).` Definir un tipo tabla indexada de valores numéricos por clave carácter. Definir alguna tabla indexada y rellenarla. Reemplazar alguno de sus valores y mostrar en pantalla tanto índices como valores.
```sql
DECLARE
TYPE t_poblacion IS TABLE OF NUMBER INDEX BY VARCHAR2 ( 64);
paises_poblacion t_poblacion;
continentes_poblacion t_poblacion;
n_cuantos NUMBER ( 12);
s_cual VARCHAR2 ( 64);
BEGIN
DBMS_OUTPUT.ENABLE;
paises_poblacion ('Portugal') := 10000000;
paises_poblacion ('Irlanda') := 15000000;
n_cuantos := paises_poblacion ('Irlanda');
DBMS_OUTPUT.PUT_LINE ( 'Irlanda: '|| n_cuantos );
continentes_poblacion ('Europa') := 300000000;
continentes_poblacion ('Asia') := 3000000003;
continentes_poblacion ('Oceania') := 75000000; -- Nueva entrada
continentes_poblacion ('Oceania') := 75000001; -- Reemplaza entrada
s_cual := continentes_poblacion.FIRST;
DBMS_OUTPUT.PUT_LINE ( 'Primero: ' || s_cual );
s_cual := continentes_poblacion.LAST;
DBMS_OUTPUT.PUT_LINE ( 'Ultimo: ' || s_cual );
n_cuantos := continentes_poblacion ( continentes_poblacion.LAST);
DBMS_OUTPUT.PUT_LINE ( 'Cuantos en el ultimo: '|| n_cuantos );
END;
/
```
La salida que produce por pantalla es:
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image2.png)
<u>Ejemplo:</u> Index-by tables, en BD `( Scripts\PLsql_11.sql)`. Guardar en una tabla indexada el empleado con *cod_empl=’0001’* y mostrar su nombre. Como ejercicio queda controlar en el ejemplo que no falle el programa si no existe ese código de empleado y que informe de ello.
```sql
SET SERVEROUTPUT ON
DECLARE
TYPE t_empleados IS TABLE OF empleados%ROWTYPE
INDEX BY BINARY_INTEGER;
v_empleados t_empleados;
s_cod_empleado empleados.cod_empl%TYPE;
BEGIN
DBMS_OUTPUT.ENABLE;
SELECT **
INTO v_empleados ( 1)
FROM empleados
WHERE cod_empl = '0001';
DBMS_OUTPUT.PUT_LINE (v_empleados ( 1).nombre || ‘ ‘ ||
v_empleados ( 1).f_alta );
END;
/
```
Las tablas indexadas ayudan a representar conjuntos de datos de tamaño arbitrario, con operaciones de búsqueda rápidas para un elemento individual sin saber su posición y sin tener que colocar los elementos de la matriz. Es como una versión simple de una tabla del SQL donde se puede recuperar los valores basados en la clave primaria.
Para el almacenamiento temporal sencillo de los datos de las operaciones de búsqueda, las tablas indexadas permiten evitar el uso de espacio en disco requerido para las tablas del SQL.
Ya que están pensadas para almacenamiento temporal no se pueden utilizar con declaraciones SQL tales como INSERT y SELECT INTO (¡Cuidado!, en el ejemplo se usa pero no como origen de datos que es a lo que se refiere esta afirmación).
Se pueden hacer persistentes durante una sesión de la base de datos declarando el tipo en un paquete y asignando los valores en un cuerpo del paquete. Es realmente aconsejable para listas de valores pequeñas tales como letras del NIF con su correspondiente módulo.
## Tablas jerárquicas
Las tablas jerárquicas usan la sintaxis:
> ***TYPE** \<nombre_tipo\> **IS TABLE OF** \<elemento_tipo\> [NOT NULL];*
donde *nombre_tipo* es el tipo específico que se usará después para declarar colecciones. Y *elemento_tipo* es cualquier tipo de dato PL/SQL excepto REF CURSOR.
También pueden definirse como objetos de la BD utilizando la sintaxis:
> ***CREATE [OR REPLACE] TYPE** \<nombre_tipo\>*
>
> ***AS TABLE OF** \<elemento_tipo\> [NOT NULL];*
Las tablas jerárquicas declaradas globalmente en SQL tienen restricciones adicionales. No pueden usarse los tipos:
> BINARY_INTEGER, PLS_INTEGER
>
> BOOLEAN
>
> LONG, LONG RAW
>
> NATURAL, NATURALN
>
> POSITIVE, POSITIVEN
>
> REF CURSOR
>
> SIGNTYPE
>
> STRING
Como las tablas jerárquicas no tienen un tamaño máximo, podemos rellenarlas con cuantos registros sean necesarios. Para ello se utiliza el método EXTEND, según el siguiente formato:
Nombre_variable.**EXTEND;**
En relación con la base de datos, las tablas jerarquizadas se pueden considerar tablas de una columna. Oracle almacena las filas de una tabla jerarquizada sin un orden particular. Pero cuando se recupera la tabla jerarquizada en una variable de PL/SQL, <u>las filas vienen identificadas por subíndices consecutivos que empiezan en 1</u>. Esto ordena el acceso a las filas individuales.
Las tablas jerarquizadas PL/SQL son como vectores unidimensionales. Se pueden modelar los matrices multidimensionales creando tablas jerarquizadas cuyos elementos son también tablas jerarquizadas.
<u>Ejemplo</u>. Nested tables `( Scripts\PLsql_12.sql)` Podemos ver un ejemplo sencillo donde rellenaremos una tabla jerárquica y modificaremos alguno de sus elementos y finalmente mostraremos sus valores.
```sql
DECLARE
TYPE t_empleados IS TABLE OF VARCHAR2 ( 15);
v_empleados t_empleados := t_empleados ('ANA','MANUEL', 'ISABEL');
BEGIN
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE (' Tabla original');
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 1));
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 2));
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 3));
FOR i IN v_empleados.FIRST .. v_empleados.LAST
LOOP
IF v_empleados ( i) = 'DANIEL' THEN
v_empleados ( i) := 'CARLOS';
END IF;
END LOOP;
DBMS_OUTPUT.PUT_LINE (' Tabla modificada');
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 1));
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 2));
DBMS_OUTPUT.PUT_LINE ( v_empleados ( 3));
v_empleados.EXTEND;
v_empleados ( 4) := 'JOSE';
DBMS_OUTPUT.PUT_LINE (' Tabla extendida');
FOR i IN v_empleados.FIRST .. v_empleados.LAST
LOOP
DBMS_OUTPUT.PUT_LINE ( v_empleados ( i));
END LOOP;
END;
/
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image3.png)
```
## Matrices de tamaño variable
Las matrices de tamaño variable usan la sintaxis:
> ***TYPE** \<nombre_tipo\> **IS** {VARRAY | VARYING ARRAY} ( \<limite_tamaño\>)*
>
> ***OF** \<elemento_tipo\> [NOT NULL];*
El significado de *\<nombre_tipo\>* y *\<elemento_tipo\>* es el mismo que en las tablas indexadas*. \<limite_tamaño\>* es un entero positivo que representa el máximo número de elementos del array.
Con los **VARRAY** se puede asignar a un identificador sencillo una colección entera y deja manipular la colección en su totalidad y referirse a elementos individuales fácilmente. Para referirse a un elemento, se utiliza la sintaxis estándar de los subíndices. Por ejemplo, el ***\<variable_varray\>( 3)*** referencia el tercer elemento. Un VARRAY tiene un tamaño máximo, que se debe especificar en su definición. <u>Su índice tiene un límite inferior de 1 y un límite superior extensible según lo vayamos decidiendo, pero que nunca podrá superar el tamaño máximo</u>. El número de elementos, por tanto, varía desde 0, cuando está vacío, hasta donde nosotros decidamos. Veamos un ejemplo de matrices con VARRAY.
<u>Ejemplo</u>. VARRAY `( Scripts\PLsql_13.sql).` Es un ejemplo de cómo trabajar con una matriz, de cómo rellenarla y de cómo recuperar sus datos, así como de las excepciones que se pueden producir.
```sql
SET SERVEROUTPUT ON
DECLARE
*/**
Un ejemplo de cómo jugar con "pseudo matrices"
**/*
v_celda INTEGER;
TYPE t_fila IS VARRAY ( 4) OF v_celda%TYPE;
TYPE t_matriz IS VARRAY ( 4) OF t_fila;
v_matriz t_matriz;
n_valor v_celda%TYPE;
BEGIN
DBMS_OUTPUT.ENABLE;
-- Rellenamos una matriz
v_matriz := t_matriz ( t_fila ( 1,2,3), t_fila ( 4,5,6),
t_fila ( 7,8,9));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 3)( 1));
-- Añadimos una fila a la matriz
v_matriz.EXTEND;
-- v_matriz ( 5) := t_fila ( 10,11,12);
-- no vale, salta un ORA-06532: Subscript outside of limit
v_matriz ( 4) := t_fila ( 10,11,12);
-- Reemplazar una existente
v_matriz ( 4) := t_fila ( 66,66,66);
-- Reemplazar un elemento
v_matriz ( 1)( 1) := 0;
-- Y cuidado, también podemos añadirle un pico ...
v_matriz ( 4).extend;
v_matriz ( 4)( 4):= 99;
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 3)( 1));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 3)( 2));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 3)( 3));
-- DBMS_OUTPUT.PUT_LINE ( v_matriz ( 3)( 4));
-- no vale, salta un ORA-06533: Subscript beyond count
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 4)( 1));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 4)( 2));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 4)( 3));
DBMS_OUTPUT.PUT_LINE ( v_matriz ( 4)( 4));
END;
/
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image4.png)
```
## Diferencias entre tablas jerarquizadas y VARRAY
Las diferencias más importantes entre tablas jerarquizadas y VARRAY son:
Los VARRAY tienen un ***tamaño limitado*** y no así las “NESTED TABLES”. El tamaño de estas últimas se puede incrementar dinámicamente.
Los VARRAY son ***densos***, tienen *subíndices consecutivos*, No se pueden borrar en ellos elementos individuales. Inicialmente las tablas jerarquizadas también lo son pero podemos borrarles elementos utilizando el procedimiento DELETE ( no se ve en este tema). Esto permite dejar huecos en el índice pero la función NEXT nos permite recorrer cualquier serie de subíndices.
## Atributos de colecciones PL/SQL
Facilitan el acceso y manipulación de los elementos de una colección. Su formato es el siguiente:
> ***variabledetabla.atributo[lista de parámetros];***
- FIRST**: devuelve el valor de la clave o índice del primer elemento de la tabla.
- LAST**: devuelve el valor de la clave o índice del último elemento de la tabla.
- PRIOR**: devuelve el valor de la clave o índice del elemento anterior al elemento *n*.
> variabletabla.PRIOR ( n);
- NEXT**: devuelve el valor de la clave o índice del elemento siguiente al elemento *n*.
> <u>PRIOR del primer elemento devuelve NULL, así como NEXT del último elemento.</u>
- COUNT**: devuelve el número de filas que tiene una tabla.
- EXISTS**: devuelve TRUE si existe el elemento *n* y FALSE en caso contrario.
> variabletabla.EXISTS ( n);
- DELETE**: se utiliza para borrar elementos de una tabla.
 - Variable.DELETE: borra todos los elementos de la tabla.
 - Variable.DELETE ( n): borra el elemento indicado por *n* si es que existe.
 - Variable.DELETE ( n1, n2): borra las filas comprendidas entre n1 y n2, siendo n1\>=n2.
- EXTEND**: reserva espacio para nuevo elementos ( VARRAYS y TABLAS ANIDADAS), siempre y cuando no exceda el límite indicado en la declaración.
 - Variable.EXTEND: reserva espacio para un nuevo elemento.
 - Variable.EXTEND ( n): reserva espacio para *n* elementos.
- TRIM**: elimina los últimos elementos de una tabla ( VARRAYS y TABLAS ANIDADAS).
 - Variable.TRIM: elimina el elemento con índice más alto.
 - Variable.TRIM ( n): elimina los *n* elementos con índice más alto.
- LIMIT**: devuelve elvalor más alto permitido en un VARRAY.
## CURSORES
Hasta ahora hemos trabajado con *cursores implícitos*, <u>pero éstos solamente deben devolver una fila ( y sólo una), ya que de lo contrario, se producirá un error</u>. Como una consulta suele devolver varias filas, se suelen utilizar **cursores explícitos**. Por tanto, un cursor explícito ( de ahora en adelante, simplemente, cursor) es un tipo de variable que se utiliza para trabajar con varias filas de registros como si fuera un conjunto de tipos %ROWTYPE. Se puede asimilar a una vista.
Los cursores se declaran en la sección de declaración en la forma:
> ***CURSOR** \<nombre del cursor\> **IS** \<consulta correspondiente\>*
>
> *[\<variable\> \<nombre del cursor\>%ROWTYPE;]*
donde la segunda parte se omite si se va a utilizar el cursor en un bucle FOR.
- Ejemplo. Definición cursor.
> ***CURSOR departamentos_cursor IS SELECT ** FROM departamentos;***
>
> ***v_departamentos_cursor departamentos_cursor%ROWTYPE;***
Para ser utilizados los cursores se abren y se cierran con las sentencias
***OPEN** \<nombre del cursor\>;*
***CLOSE** \<nombre del cursor\>;*
Esto de nuevo se omite si se utiliza en un bucle FOR.
- Ejemplo. OPEN y CLOSE.
> ***OPEN** departamentos_cursor;*
>
> ***CLOSE** departamentos_cursor;*
Y ¿cómo trabajar con los datos de un cursor? Pues para ello lo que se hace es recoger los datos en una variable que ha tenido que ser declarada anteriormente si no se está utilizando la sentencia FOR.
La sentencia para introducir los datos en el cursor es:
> ***FETCH** \<nombre cursor\> **INTO** \<nombre variable\>;*
- Ejemplo. FETCH
> ***FETCH** departamentos_cursor **INTO** v_departamentos_cursor;*
Si estamos utilizando un FOR no es necesario declarar la variable ni realizar asignación.
- Ejemplo. FOR sin declaración.
> ***FOR** v_departamentos_cursor **IN** departamentos_cursor **LOOP***
>
> *… ( sin FETCH)*
>
> ***END LOOP;***
¿Cómo trabajamos con cada una de las columnas de la consulta que da origen al cursor? Pues una vez designada o declarada la variable cada una de las columnas se referencia como:
> \<nombre de la variable\>.\<nombre de la columna\>
es decir, si por ejemplo la tabla departamentos estaba compuesta de COD_DEPTO, NOMBRE, NUM_EMPL e IMP_PRESUP en nuestro ejemplo anterior estas columnas se referenciarán como:
> *v_departamentos_cursor.cod_depto*
>
> *v_departamentos_cursor.nombre*
>
> *v_departamentos_cursor.num_empl*
>
> *v_departamentos_cursor.imp_presup*
- Ejemplo. FOR para cursores.
> Hacer un programa que lea los departamentos de la tabla departamentos y muestre por pantalla sus nombres separados por una coma ( utilizar un bucle FOR).
Este ejemplo lo hemos realizado con un FOR porque aún no hemos hablado de los atributos de los cursores. Estos atributos son variables asociadas al cursor que devuelven distintos valores, según el estado de este, su tamaño, etc …. Son los siguientes:
- \<cursor\>%NOTFOUND: devuelve TRUE cuando la llamada FETCH no recupera ningún valor.
- \<cursor\>%FOUND: lo contrario del anterior, devuelve TRUE mientras encuentre valores. Antes de un FETCH esta a NULL.
- \<cursor\>%ROWCOUNT: devuelve el número de registros ( o filas) que ha recuperado hasta el momento el cursor
- \<cursor\>%ISOPEN: devuelve TRUE si el cursor está abierto.
<u>Ejemplo</u>: `( Scripts\PLsql_14.sql).`
```sql
SET SERVEROUTPUT ON
DECLARE
CURSOR empleados_cursor IS
SELECT nombre, apell1
FROM empleados;
v_empleados_cursor empleados_cursor%ROWTYPE;
v_nombre VARCHAR2 ( 20);
v_apellido1 VARCHAR2 ( 20);
BEGIN
DBMS_OUTPUT.ENABLE;
OPEN empleados_cursor;
LOOP
FETCH empleados_cursor INTO v_nombre, v_apellido1;
EXIT WHEN empleados_cursor%NOTFOUND;
DBMS_OUTPUT.PUT_LINE ( empleados_cursor%ROWCOUNT || ' ' ||v_nombre || '**' || v_apellido1);
END LOOP;
CLOSE empleados_cursor;
EXCEPTION
WHEN OTHERS THEN
IF ( empleados_cursor%ISOPEN) THEN
CLOSE empleados_cursor;
END IF;
DBMS_OUTPUT.PUT_LINE ('Ocurrió error no controlado: '||SQLERRM);
END;
/
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image5.png)
```
Existe otra alternativa para procesar la consulta y es utilizar una estructura repetitiva FOR o WHILE.
```sql
FOR v_empleados_cursor IN empleados_cursor LOOP
DBMS_OUTPUT.PUT_LINE ( empleados_cursor%ROWCOUNT || ' ' ||v_nombre || '**' || v_apellido1);
END LOOP;
```
<u>Ejemplo</u>. Atributos y WHILE `( Scripts\PLsql_15.sql).`
```sql
SET SERVEROUTPUT ON
DECLARE
CURSOR departamentos_cursor IS
SELECT nombre
FROM departamentos;
v_departamentos_cursor departamentos_cursor%ROWTYPE;
s_cadena VARCHAR2 ( 250);
BEGIN
DBMS_OUTPUT.ENABLE;
OPEN departamentos_cursor;
FETCH departamentos_cursor INTO v_departamentos_cursor;
WHILE ( departamentos_cursor%FOUND ) LOOP
IF ( s_cadena IS NULL ) THEN
s_cadena := v_departamentos_cursor.nombre;
ELSE
s_cadena := s_cadena||', '||v_departamentos_cursor.nombre;
END IF;
FETCH departamentos_cursor INTO v_departamentos_cursor;
END LOOP;
DBMS_OUTPUT.PUT_LINE ( s_cadena);
CLOSE departamentos_cursor;
EXCEPTION
WHEN OTHERS THEN
IF ( departamentos_cursor%ISOPEN) THEN
CLOSE departamentos_cursor;
END IF;
DBMS_OUTPUT.PUT_LINE ('Ocurrió error no controlado: '||SQLERRM);
END;
/
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image6.png)
```
# CREACIÓN DE PROCEDIMIENTOS Y FUNCIONES
## PROCEDIMIENTOS
Un procedimiento es un subprograma ( un trozo llamado por otros programas) que realiza una acción específica. Se escriben procedimientos usando la sintaxis:
```sql
[CREATE [OR REPLACE]]
PROCEDURE nombre_procedimiento[( parámetro[, parámetro]...)]
[AUTHID {DEFINER | CURRENT_USER}] {IS | AS}
[PRAGMA AUTONOMOUS_TRANSACTION;]
[Declaraciones locales]
BEGIN
Sentencias ejecutables
[EXCEPTION
Tratamiento de excepciones]
END [nombre_procedimiento];
```
Donde la sintaxis de “parámetro” es:
> nombre_parametro [IN | OUT [NOCOPY] | IN OUT [NOCOPY]] tipo_dato
>
> [{:= | DEFAULT} expresión]
La cláusula **CREATE** permite crear procedimientos independientes, que son almacenados en una base de datos ORACLE. Se puede ejecutar la sentencia CREATE PROCEDURE desde SQL**Plus o desde un programa usando el SQL dinámico nativo ( Esto último sería objeto de cursos de SQL avanzado).
La cláusula **AUTHID** determina si un procedimiento almacenado se ejecuta con privilegios del propietario ( por defecto) o del usuario actual y si las referencias a los objetos del esquema son resueltas en el esquema del propietario o del usuario actual. Se puedes eliminar el comportamiento por defecto especificando CURRENT_USER.
**PRAGMA AUTONOMOUS_TRANSACTION** manda al compilador de PL/SQL que lo marque como procedimiento autónomo ( independiente). Las transacciones autónomas dejan suspender la transacción principal, hacer otras operaciones, un COMMIT o un ROLL BACK de esas operaciones y, finalmente, retomar la transacción principal.
No se puede constreñir el tipo de dato de un parámetro. Por ejemplo la siguiente declaración es ilegal porque hay una restricción de tamaño:
-- Ilegal.
> PROCEDURE prc_calcular_letra_nif ( num_dni NUMBER ( 15)) IS ...
Pero se puede dar un rodeo para conseguirlo:
> DECLARE
>
> -- ¡Atención! Sencillo pero no se ha contado.
>
> SUBTYPE Num15 IS NUMBER ( 15);
>
> PROCEDURE prc_calcular_letra_nif ( num_dni Num15) IS ...
Y cuidado los parámetros de salida no deben llevar cláusula DEFAULT:
PLS-00230: OUT and IN OUT formal parameters may not have default expressions
Un procedimiento tiene dos partes: la **especificación** y el **cuerpo**.
La especificación del procedimiento comienza con la palabra clave PROCEDURE y termina con el nombre del procedimiento o una lista del parámetros. La declaración de parámetros es opcional. Los procedimientos que no toman ningún parámetro se escriben sin paréntesis.
El cuerpo del procedimiento comienza con la palabra clave IS ( o AS) y termina con la palabra clave END seguido por el nombre del procedimiento ( esto último opcional). El cuerpo del procedimiento tiene tres partes: una parte declarativa ( que puede ir vacía), una parte ejecutable, y una parte opcional de tratamiento de excepciones.
La parte declarativa contiene las declaraciones locales, que se ponen entre las palabras claves IS y BEGIN. No se usa DECLARE. La parte ejecutable contiene sentencias, que se ponen entre las palabras claves BEGIN y EXCEPTION ( o END). Por lo menos debe haber una sentencia en la parte ejecutable de un procedimiento. Por ejemplo, NULL. El tratamiento de excepciones se coloca entre EXCEPCIÓN y END.
<u>Ejemplo</u>: Aumentar salario `( Scripts\PLsql_16.sql).` Crear un procedimiento que dado el código de un empleado le aumente su sueldo en una cantidad dada.
```sql
SET SERVEROUTPUT ON
DECLARE
b_bien BOLEAN := FALSE;
s_empleado empleados.cod_empl%TYPE := ´0001´ ;
n_importe empleados.imp_salario%TYPE := 1200;
PROCEDURE prc_aumentar_salario (
p_cod_empl IN empleados.cod_empl%TYPE,
p_imp_aumento IN empleados.imp_salario%TYPE,
p_bien OUT BOOLEAN ) IS
s_parametro VARCHAR2 ( 30);
n_imp_salario empleados.imp_salario%TYPE;
e_parametros_nulos EXCEPTION;
e_salario_nulo EXCEPTION;
BEGIN
IF ( p_cod_empl IS NULL ) THEN
s_parametro := 'P_COD_EMPLEADO';
RAISE e_parametros_nulos;
ELSIF ( p_imp_aumento IS NULL ) THEN
s_parametro := 'P_IMP_AUMENTO';
RAISE e_parametros_nulos;
END IF;
SELECT imp_salario
INTO n_imp_salario
FROM empleados
WHERE cod_empl = p_cod_empl;
IF ( n_imp_salario IS NULL ) THEN
RAISE e_salario_nulo;
ELSE
UPDATE empleados
SET imp_salario = imp_salario + p_imp_aumento
WHERE cod_empl = p_cod_empl;
END IF;
p_bien := TRUE;
EXCEPTION
WHEN e_parametros_nulos THEN
DBMS_OUTPUT.PUT_LINE ('El valor del parámetro '||s_parametro||' entra a nulo.');
WHEN e_salario_nulo THEN
DBMS_OUTPUT.PUT_LINE ('El salario recuperado es nulo para el empleado '||p_cod_empl||'.');
WHEN NO_DATA_FOUND THEN
DBMS_OUTPUT.PUT_LINE ('No encontrado empleado con código '||p_cod_empl||'.');
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE ('Fatal error: '||SQLERRM);
END prc_aumentar_salario;
BEGIN
DBMS_OUTPUT.ENABLE;
prc_aumentar_salario ( s_empleado, n_importe, b_bien);
IF ( b_bien ) THEN
COMMIT;
DBMS_OUTPUT.PUT_LINE ('Salario del empleado '||s_empleado||' aumentado en '||n_importe);
ELSE
ROLLBACK;
DBMS_OUTPUT.PUT_LINE ('Salario del empleado '||s_empleado||' NO aumentado en '||n_importe);
END IF;
END;
/
```
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image7.png)
## FUNCIONES
Una **función** es un subprograma que devuelve un valor. Las funciones y los procedimientos se estructuran de forma similar, salvo que las funciones tienen una cláusula **RETURN**. Se escriben usando la sintaxis:
```sql
[CREATE [OR REPLACE ] ]
FUNCTION nombre_función [ ( parámetro [ , parámetro ]... ) ]
RETURN Tipo_dato
[ AUTHID { DEFINER | CURRENT_USER } ]
[ PARALLEL_ENABLE
[ { [CLUSTER parámetro BY ( nombre_columna [, nombre_columna ]... ) ] |
[ORDER parámetro BY ( nombre_columna [ , nombre_columna ]... ) ] } ]
[ ( PARTITION parámetro BY
{ [ {RANGE | HASH } ( nombre_columna [, nombre_columna]...)] | ANY }
) ]
]
[DETERMINISTIC] [ PIPELINED [ USING tipo_implementacion ] ]
[ AGGREGATE [UPDATE VALUE] [WITH EXTERNAL CONTEXT]
USING tipo_implementacion ] {IS | AS}
[ PRAGMA AUTONOMOUS_TRANSACTION; ]
[ Declaraciones locales ]
BEGIN
Sentencias ejecutables
[EXCEPTION
Tratamiento de excepciones]
END [ nombre_función ];
```
La cláusula **CREATE** permite crear funciones independientes, que son almacenados en una base de datos ORACLE. Se puede ejecutar la sentencia CREATE PROCEDURE desde SQL**Plus o desde un programa usando el SQL dinámico nativo ( Esto último sería objeto de cursos de SQL avanzado).
La cláusula **AUTHID** determina si una función almacenada se ejecuta con privilegios del propietario ( por defecto) o del usuario actual y si las referencias a los objetos del esquema son resueltas en el esquema del propietario o del usuario actual. Se puedes eliminar el comportamiento por defecto especificando CURRENT_USER.
La opción de **PARALLEL_ENABLE** indica que una función almacenada se puede utilizar “safely” (¿con seguridad?) en las sesiones auxiliares de las “evaluaciones paralelas de DML”(¿?). El estado de una sesión principal ( la conexión) nunca se comparte con sesiones auxiliares. Cada sesión auxiliar tiene su propio estado, que se inicializa cuando la sesión comienza. El resultado de la función no debe depender del estado de las variables ( estáticas) de la sesión. Si no, los resultados podrían variar a través de las sesiones.
**DETERMINISTIC** ayuda al optimizador para evitar llamadas a función redundantes. Si una función almacenada fue llamada previamente con los mismos argumentos, el optimizador puede elegir usar el resultado anterior. El resultado de la función no debe depender del estado de las variables de la sesión o de los objetos del esquema. Si no, los resultados podrían variar a través de llamadas. Solamente las funciones con DETERMINISTIC se pueden llamar desde un función indexada ( function-based index) o una vista materializada que tenga activado reescribir las consultas.
**PRAGMA AUTONOMOUS_TRANSACTION** manda al compilador de PL/SQL que marque a la función como función autónoma ( independiente). Las transacciones autónomas dejan suspender la transacción principal, hacer otras operaciones, un COMMIT o un ROLL BACK de esas operaciones y, finalmente, retomar la transacción principal.
No se puede constreñir el tipo de dato de un parámetro ( con NOT NULL por ejemplo, o con tamaños) o del valor retornado por la función. Sin embargo, de la misma forma que se vio en los procedimientos se puede obligar a ello indirectamente. Para ver como, se hace referencia a este mismo caso en procedimientos. Mirarlo allí.
Como un procedimiento, una función tiene dos partes sintácticas: la **especificación** y el **cuerpo.** La especificación de la función comienza con la palabra clave **FUNCTION** y termina con la cláusula **RETURN**, que especifica el tipo de dato del valor retornado. La declaración de parámetros es opcional. Las funciones que no toman ningún parámetro se escriben sin paréntesis.
El cuerpo de la función tiene tres partes: una parte **declarativa** ( que puede ir vacía), una parte **ejecutable**, y una *parte opcional* de tratamiento de **excepciones**.
La parte declarativa contiene las declaraciones locales, que se ponen entre las palabras claves IS y BEGIN. <u>No se usa DECLARE</u>.
La parte ejecutable contiene sentencias, que se ponen entre las palabras claves BEGIN y EXCEPTION ( o END). Por lo menos debe haber una sentencia en la parte ejecutable de un procedimiento. Por ejemplo, NULL.
El tratamiento de excepciones se coloca entre EXCEPCIÓN y END.
<u>Ejemplo</u>: Validar letra NIF `( Scripts\PLsql_17.sql).`Crear una función que determine a partir de un DNI y una letra si esta última corresponde a la letra de su NIF. Si es así debe devolver TRUE y si no FALSE.
```sql
SET SERVEROUTPUT ON
DECLARE
n_dni empleados.dni%TYPE := '&DNI';
s_letra_nif empleados.letra_nif%TYPE := '&LETRA';
FUNCTION fnc_validar_nif ( p_dni IN empleados.dni%TYPE,
p_letra_nif IN empleados.letra_nif%TYPE )
RETURN BOOLEAN IS
s_parametro VARCHAR2 ( 15);
TYPE t_fila_letras_nif IS VARRAY ( 23) OF VARCHAR ( 1);
v_letras_nif t_fila_letras_nif;
n_modulo INTEGER;
e_parametros_nulos EXCEPTION;
b_bien BOOLEAN := FALSE;
BEGIN
IF ( p_dni IS NULL) THEN
s_parametro := 'P_DNI';
RAISE e_parametros_nulos;
ELSIF ( p_letra_nif IS NULL) THEN
s_parametro := 'P_LETRA_NIF';
RAISE e_parametros_nulos;
END IF;
v_letras_nif := t_fila_letras_nif ('R','W','A','G','M',
'Y','F','P','D','X',
'B','N','J','Z','S',
'Q','V','H','L','C',
'K','E','T');
n_modulo := MOD ( p_dni, 23);
DBMS_OUTPUT.PUT_LINE ('Valor del módulo : '|| n_modulo);
DBMS_OUTPUT.PUT_LINE ('Valor Letra recuperada : '||v_letras_nif ( n_modulo));
IF ( v_letras_nif ( n_modulo) = UPPER ( p_letra_nif) ) THEN
b_bien := TRUE;
END IF;
RETURN b_bien;
EXCEPTION
WHEN e_parametros_nulos THEN
DBMS_OUTPUT.PUT_LINE ('El valor del parámetro '|| s_parametro||' entra a nulo.');
RETURN FALSE;
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE ('Fatal error: '|| SQLERRM);
RETURN FALSE;
END fnc_validar_nif;
BEGIN
DBMS_OUTPUT.ENABLE;
IF ( fnc_validar_nif( n_dni, s_letra_nif ) ) THEN
DBMS_OUTPUT.PUT_LINE ('NIF correcto.');
ELSE
DBMS_OUTPUT.PUT_LINE ('¡Cuidado! El NIF '|| n_dni||'-'||s_letra_nif||' es incorrecto.');
END IF;
END;
/
```
## Sentencia RETURN
La sentencia **RETURN** termina inmediatamente la ejecución de un subprograma y devuelve control a quien lo llamó. La ejecución continúa con la sentencia que sigue a la llamada al subprograma. (*No confundir la sentencia RETURN con la cláusula RETURN de la especificación de la función, que especifica el tipo de dato que retorna la función*.)
Un subprograma puede contener varias sentencias RETURN. No es necesario que la última sentencia del subprograma sea un RETURN. Ejecutando cualquier sentencia RETURN termina el subprograma inmediatamente. <u>Sin embargo, tener puntos múltiples de salida no es una buena práctica ( dificulta el seguimiento de un programa) y se aconseja evitarlo</u>.
En procedimientos, una sentencia RETURN no puede devolver un valor, y por lo tanto, no puede contener una expresión *(“PLS-00372: In a procedure, RETURN statement cannot contain an expresión”*), pero sí se utiliza para devolver el control antes de la finalización normal del procedimiento.
Sin embargo, en funciones, una sentencia RETURN debe contener una expresión, que se evalúa cuando se ejecuta la sentencia RETURN. El valor que resulta se asigna al identificador de la función, que actúa como una variable del tipo especificado en la cláusula RETURN.
Un ejemplo muy sencillo puede ser el siguiente `( Scripts\PLsql_18.sql).`:
```sql
DECLARE
FUNCTION fnc_identidad ( p_numero INTEGER) RETURN INTEGER IS
BEGIN
RETURN p_numero;
END fnc_identidad;
BEGIN
DBMS_OUTPUT.ENABLE;
IF ( fnc_identidad ( 1) = 1) THEN
DBMS_OUTPUT.PUT_LINE ('Bien');
END IF;
END;
/
```
Veamos que funciona:
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image8.png)
## Almacenamiento en diccionario
Hasta ahora nos hemos limitado a generar código de procedimientos y funciones y ejecutarlos inmediatamente en el mismo script. Esto solamente tiene utilidad para mostrar y probar cómo funcionan los subprogramas. Lo que se necesita es podérseles invocar desde otros programas o aplicaciones. Con la orden **CREATE**, Oracle automáticamente compila el código fuente, genera el código objeto y los guarda en el diccionario de datos. De este modo, quedan disponibles para su utilización. Se puede acceder a estos objetos a través de la vista **USER_OBJECTS**.
<u>Ejemplo</u>: Creación de un procedimiento. `( Scripts\PLsql_19.sql).`
```sql
CREATE OR REPLACE PROCEDURE proc_a_tanto_porciento ( p_numero NUMBER)
AS
BEGIN
DBMS_OUTPUT.PUT_LINE ('En porcentaje: ' || p_numero/100);
END proc_a_tanto_porciento;
/
Una vez creado y almacenado el procedimiento en la Base de Datos, puede ser invocado y ejecutado por otro programa. Por ejemplo, Oracle proporciona el procedimiento EXECUTE para ejecutar procedimientos desde SQL**Plus
```
***SQL\>EXECUTE proc_a_tanto_porciento ( 16);***
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image9.png)
<u>Ejemplo</u>: Creación de una función. `( Scripts\PLsql_20.sql).`
> ***CREATE OR REPLACE FUNCTION** **fnc_a_tanto_porciento** ( p_numero NUMBER)*
***RETURN** NUMBER **IS***
***BEGIN***
> ***RETURN** p_numero/100;*
***END** **fnc_a_tanto_porciento;***
***/***
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image10.png)
## Compilación y borrado de subprogramas
Para volver a compilar un subprograma almacenado en la base de datos se emplea la orden **ALTER** con la opción ***COMPILE***.
> ***ALTER** {PROCEDURE | FUNCTION} nombre subprograma **COMPILE**;*
Para borrar un subprograma almacenado se usa la orden **DROP**.
> ***DROP** {PROCEDURE | FUNCTION} nombresubprograma;*
## PAQUETES
Un **paquete** es un objeto del esquema que agrupa tipos lógicamente relacionados, variables, constantes y subprogramas de PL/SQL. Los paquetes tienen generalmente dos partes, una **especificación** y un **cuerpo**, aunque el cuerpo es a veces innecesario.
La **especificación** es el interfaz para las aplicaciones. <u>Declara los tipos, las variables, las constantes, las excepciones, los cursores, y los subprogramas dejándolos disponibles para el uso. El **cuerpo** define completamente los cursores y los subprogramas, y por tanto implementa la especificación.</u>
Se puede pensar en la especificación como una interfaz operacional y en el cuerpo como una “caja negra.” Esto es algo muy común en la Programación Modular y perfectamente asumido por la Programación Orientada a Objetos. Por ejemplo, en lenguaje C tenemos, por un lado, los archivos cabecera *.h* donde se define los prototipos de las funciones y, por otro lado, los archivos *.c* donde está implementado el código de cada una de las funciones anteriores.
Una gran ventaja de este tipo de programación es que se pueden eliminar errores, añadir código, o sustituir el cuerpo del paquete sin cambiar el interfaz ( especificación del paquete).
Para crear un paquete se usa la sentencia **CREATE PACKAGE**, que se puede ejecutar desde SQL**Plus. Su sintaxis es:
```sql
CREATE [OR REPLACE] PACKAGE package_name
[AUTHID {CURRENT_USER | DEFINER}]
{IS | AS}
[PRAGMA SERIALLY_REUSABLE;]
[collection_type_definition ...]
[record_type_definition ...]
[subtype_definition ...]
[collection_declaration ...]
[constant_declaration ...]
[exception_declaration ...]
[object_declaration ...]
[record_declaration ...]
[variable_declaration ...]
[cursor_spec ...]
[function_spec ...]
[procedure_spec ...]
[call_spec ...]
[PRAGMA RESTRICT_REFERENCES ( assertions) ...]
END [package_name];
[CREATE [OR REPLACE] PACKAGE BODY package_name {IS | AS}
[PRAGMA SERIALLY_REUSABLE;]
[collection_type_definition ...]
[record_type_definition ...]
[subtype_definition ...]
[collection_declaration ...]
[constant_declaration ...]
[exception_declaration ...]
[object_declaration ...]
[record_declaration ...]
[variable_declaration ...]
[cursor_body ...]
[function_spec ...]
[procedure_spec ...]
[call_spec ...]
[BEGIN
sequence_of_statements]
END [package_name];]
```
La especificación posee las declaraciones públicas, que son visibles a la aplicación. Se deben declarar los subprogramas en el final de la especificación después de el resto de los componentes del paquete.
El cuerpo se compone del código de las funciones y procedimientos y de las declaraciones privadas, que se ocultan a la aplicación. Después de la parte declarativa del cuerpo del paquete se puede poner una parte opcional, que lleva a cabo generalmente las declaraciones que inicializan variables del paquete.
La cláusula de AUTHID, se utiliza como en procedimientos y funciones.
En **call spec** se nos permite publicar un método de Java o una función externa de C en el diccionario de los datos de ORACLE. Para aprender cómo escribirlas ver *Oracle9i Java Stored Procedures Developer’s Guide*. Para aprender a escribir especificaciones de llamadas C, ver *Oracle9i Application Developer’s Guide - Fundamentals*.
<u>Ejemplo</u>: Paquete en BD en el que se recogen los ejemplos anteriores. Se crean dos ficheros por separado, uno para el cuerpo y otro para la cabecera, donde se recoge la solución.
```sql
CREATE OR REPLACE PACKAGE pkg_empleados
IS
TYPE t_fila_letras_nif IS VARRAY ( 23) OF VARCHAR ( 1);
v_letras_nif t_fila_letras_nif;
PROCEDURE prc_aumentar_salario
( p_cod_empl IN empleados.cod_empl%TYPE,
p_imp_aumento IN empleados.imp_salario%TYPE,
p_bien OUT BOOLEAN );
FUNCTION fnc_validar_nif
( p_dni IN empleados.dni%TYPE,
p_letra_nif IN empleados.letra_nif%TYPE )
RETURN BOOLEAN;
END pkg_empleados;
/
CREATE OR REPLACE PACKAGE BODY pkg_empleados
IS
PROCEDURE prc_aumentar_salario
( p_cod_empl IN empleados.cod_empl%TYPE,
p_imp_aumento IN empleados.imp_salario%TYPE,
p_bien OUT BOOLEAN ) IS
s_parametro VARCHAR2 ( 30);
n_imp_salario empleados.imp_salario%TYPE;
e_parametros_nulos EXCEPTION;
e_salario_nulo EXCEPTION;
BEGIN
IF ( p_cod_empl IS NULL ) THEN
s_parametro := 'P_COD_EMPLEADO';
RAISE e_parametros_nulos;
ELSIF ( p_imp_aumento IS NULL ) THEN
s_parametro := 'P_IMP_AUMENTO';
RAISE e_parametros_nulos;
END IF;
SELECT imp_salario
INTO n_imp_salario
FROM empleados
WHERE cod_empl = p_cod_empl;
IF ( n_imp_salario IS NULL ) THEN
RAISE e_salario_nulo;
ELSE
UPDATE empleados
SET imp_salario = imp_salario + p_imp_aumento
WHERE cod_empl = p_cod_empl;
END IF;
p_bien := TRUE;
EXCEPTION
WHEN e_parametros_nulos THEN
DBMS_OUTPUT.PUT_LINE ('El valor del parámetro '||s_parametro||' entra a nulo.');
WHEN e_salario_nulo THEN
DBMS_OUTPUT.PUT_LINE ('El salario recuperado es nulo para el empleado '||p_cod_empl||'.');
WHEN NO_DATA_FOUND THEN
DBMS_OUTPUT.PUT_LINE ('No encontrado empleado con código '||p_cod_empl||'.');
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE ('Fatal error: '||SQLERRM);
END prc_aumentar_salario;
FUNCTION fnc_validar_nif
( p_dni IN empleados.dni%TYPE,
p_chr_letra_nif IN empleados.letra_nif%TYPE )
RETURN BOOLEAN IS
s_parámetro VARCHAR2 ( 15);
n_modulo INTEGER;
e_parametros_nulos EXCEPTION;
b_bien BOOLEAN := FALSE;
BEGIN
IF ( p_dni IS NULL) THEN
s_parametro := 'P_NUM_DNI';
RAISE e_parametros_nulos;
ELSIF ( p_letra_nif IS NULL) THEN
s_parametro := 'P_CHR_LETRA_NIF';
RAISE e_parametros_nulos;
END IF;
n_modulo := MOD ( p_dni,23);
DBMS_OUTPUT.PUT_LINE ('Valor del módulo : '||n_modulo);
DBMS_OUTPUT.PUT_LINE ('Valor Letra recuperada : '||v_letras_nif ( n_modulo));
IF ( v_letras_nif ( n_modulo) = UPPER ( p_letra_nif) ) THEN
b_bien := TRUE;
END IF;
RETURN b_bien;
EXCEPTION
WHEN e_parametros_nulos THEN
RETURN FALSE;
DBMS_OUTPUT.PUT_LINE ('El valor del parámetro '||s_parametro||' entra a nulo.');
WHEN OTHERS THEN
RETURN FALSE;
DBMS_OUTPUT.PUT_LINE ('Fatal error: '||SQLERRM);
END fnc_validar_nif;
BEGIN
v_letras_nif := t_fila_letras_nif ('R','W','A','G','M',
'Y','F','P','D','X',
'B','N','J','Z','S',
'Q','V','H','L','C',
'K','E','T');
END pkg_empleados;
/
```
Solamente los declaraciones en la especificación del paquete son visibles y accesibles a las aplicaciones. Los detalles implementados en el cuerpo del paquete están ocultos e inaccesibles. Así pues, puedes cambiar el cuerpo sin tener que volver a compilar los paquetes que lo llamen.
# DISPARADORES DE TABLAS
## INTRODUCCIÓN
Se llama **trigger** ( o **disparador)** al código PL/SQL que se ejecuta *<u>automáticamente</u>* cuando es procesada una determinada operación DML ( insert, delete, update, etc.) sobre una tabla o vista y también cuando ocurre algún evento del sistema ( arranque/parada de la base de datos, entrada/salida de un usuario, etc.). El código que se ejecuta es independiente de la aplicación que realizó dicha operación.
Los triggers suelen utilizarse para:
- Crear instrucciones complejas de seguridad e integridad.
- Generar de forma automática valores derivados o calculados.
- Auditar o realizar un seguimiento de actualizaciones.
- Prevenir o incluso impedir transacciones erróneas.
- Gestionar réplicas remotas de una tabla.
El código que se lanza con el trigger es PL/SQL. Sin embargo, no resulta del todo conveniente realizar excesivos triggers dado que complica el uso de la base de datos. En general, hay tres tipos de disparadores:
- Disparadores de tablas**: se producen cuando se ocurre cualquier operación DML sobre una tabla.
- Disparadores de sustitución**: se producen cuando se ocurre cualquier operación DML sobre una vista.
- Disparadores del sistema**: se producen cuando ocurre cualquier suceso del sistema o una instrucción DDL sobre un objeto.
## CREACIÓN DE TRIGGERS
## Elementos de los triggers
Puesto que un trigger es un código que se dispara, al crearle se deben indicar los siguientes elementos:
- El evento que da lugar a la ejecución del trigger (**INSERT**, **UPDATE** o **DELETE**) .
- Cuando se lanza el evento en relación a dicho evento (**BEFORE** ( antes), **AFTER** ( después) o **INSTEAD OF** ( en lugar de)) .
- Las veces que el trigger se ejecuta ( tipo de trigger: de instrucción o de fila).
- El cuerpo del trigger, es decir el código que ejecuta dicho trigger .
## Cuándo ejecutar el trigger
En el apartado anterior se han indicado los posibles tiempos para que el trigger se ejecute. Éstos pueden ser:
- BEFORE**. El código del trigger se ejecuta antes de ejecutar la instrucción DML que causó el lanzamiento del trigger.
- AFTER**. El código del trigger se ejecuta después de haber ejecutado la instrucción DML que causó el lanzamiento del trigger.
- INSTEAD OF**. El trigger sustituye a la operación DML Se utiliza para vistas que no se pueden modificar.
## Tipos de trigger
Hay dos tipos de trigger:
- De instrucción**. <u>El cuerpo del trigger se ejecuta una sola vez por cada evento que lance el trigge</u>r. *Esta es la opción por defecto*. El código se ejecuta aunque la instrucción DML no genere resultados.
- De fila**. <u>El código se ejecuta una vez por cada fila afectada por el evento</u>. Por ejemplo si hay una cláusula UPDATE que desencadena un trigger y dicho UPDATE actualiza 10 filas; si el trigger es de fila se ejecuta una vez por cada fila, si es de instrucción se ejecuta sólo una vez ( por instrucción).
## Sintaxis de creación de triggers
***CREATE** [OR REPLACE] **TRIGGER** nombre_trigger*
*{ BEFORE | AFTER }*
*{ DELETE | INSERT | UPDATE [ OF \<columna [, columna]\>] }*
***ON** nombre_tabla*
*[ FOR EACH {STATEMENT | ROW } ]*
*[WHEN ( condicion)] ]*
*\< cuerpo del trigger ( bloque PL/SQL) \> ;*
La cláusula de tiempo es una de estas palabras: **BEFORE** o **AFTER**.
Los eventos se realizan con la instrucción DML (**DELETE, INSERT, UPDATE OF**) que desencadena el trigger. El apartado OF en el UPDATE hace que el trigger se ejecute sólo cuando se modifique la ( s) columna ( s) indicada ( s).
El nivel de disparo puede ser a nivel de orden (**FOR EACH STATEMENT**) o a nivel de fila (**FOR EACH ROW**). *Se asume por defecto a nivel de orden* y el trigger se activará una sola vez por orden, independientemente del número de filas involucradas en dicha orden. A nivel de fila, el trigger se ejecutará una vez por cada fila afectada por la orden.
| | | |
|------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| | ***FOR EACH STATEMENT*** | ***FOR EACH ROW*** |
| **BEFORE** | **Se ejecuta la regla una vez antes de la ejecución del evento** | **Se ejecuta la regla una vez antes de la actualización de cada tupla afectada por el evento** |
| **AFTER** | **Se ejecuta la regla una vez después de la ejecución del evento** | **Se ejecuta la regla una vez después de la actualización de cada tupla afectada por el evento** |
<u>Ejemplo</u>: `( Scripts\ControlHorarioEnvioEnergia.sql)`
> RED (<u>Id_Red</u>, Estacion)
>
> ENVIAENERGIA (<u>Id_RedE</u>, <u>Id_RedR</u>, <u>Fecha</u>, Volumen)
***CREATE OR REPLACE TRIGGER** **tr_insdatos_enviaenergia***
Error: valor entre –20000
y -20999
***BEFORE INSERT ON enviaenergia***
***BEGIN***
***IF ( TO_CHAR ( SYSDATE, ‘HH24’) NOT IN (‘10’, ‘11’) ) THEN***
***RAISE_APPLICATION_ERROR (-20001,***
*‘Sólo se puede enviar energía entre las 10 y las 11:59’);*
***END IF;***
***END;***
***/***
Este trigger impide que se puedan añadir registros a la tabla ENVIAENERGIA entre las 10 y las 12 horas.
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image11.png)
## Referencias NEW y OLD
Cuando se ejecutan instrucciones UPDATE, hay que tener en cuenta que se modifican valores antiguos (**OLD**) para cambiarles por valores nuevos (**NEW**). Las palabras NEW y OLD permiten acceder a los valores nuevos y antiguos respectivamente.
El apartado **REFERENCING** de la creación de triggers, permite asignar nombres a las palabras NEW y OLD ( en la práctica no se suele utilizar esta posibilidad). Así, *new.nombre* haría referencia al nuevo nombre que se asigna a una determinada tabla y *old.nombre* al viejo.
En el apartado de instrucciones del trigger ( BEGIN) hay que adelantar el símbolo “:” a las palabra NEW y OLD ( serían *:new.nombre* y *:old.nombre*)
Imaginemos que deseamos hacer una auditoria sobre una tabla PRODUCTOR. Queremos almacenar en otra tabla PRODUCTOR_AUDIT los cambios de producción máxima para cada productor. Para ello creamos la tabla:
> create table productor_audit (
>
> nombre varchar2 ( 10),
>
> prodmax_ant integer,
>
> prodmax_act integer,
>
> fecha_audit date );
Como queremos que la tabla se actualice automáticamente, creamos el siguiente trigger. `( Scripts\AuditoriaProductor.sql)`
```sql
CREATE OR REPLACE TRIGGER tr_crear_audit_productor
BEFORE UPDATE OF prodMax ON productor
FOR EACH ROW
BEGIN
IF (:new.prodmax \<\> :old.prodmax) THEN
INSERT INTO productor_audit
VALUES (:old.nombre, :old.prodmax, :new.prodmax, sysdate);
```
***END IF;***
> ***END;***
>
> */*
Lo ejecutamos y después realizamos un cambio en la tabla PRODUCTOR
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image12.png)
Con este trigger cada vez que se modifique una fila de la tabla PRODUCTOR que afecte a la producción máxima, se añadirá una nueva fila en la tabla PRODUCTOR_AUDIT.
Los triggers se utilizan muy habitualmente en la modificaciones de tablas en cascada ( UPDATE ON CASCADE) ya que Oracle no admite este tipo de modificación de forma automática como sí que lo hace con el borrado en cascada ( DELETE ON CASCADE).
<u>Ejemplo</u>: Vamos a realizar una modificación en cascada de la tabla REDCOMPANIA cuando se modifica el código de una compañía `( Scripts\UdpateCascadeRedComp.sql)`
```sql
REDCOMPANIA (<u>Id_Red</u>, <u>Id_Comp</u>)
COMPANIA (<u>Cod_Comp</u>, Nombre)
CREATE OR REPLACE TRIGGER tr_redcom_upd_cascade
AFTER UPDATE OF Cod_Comp ON COMPANIA
FOR EACH ROW
BEGIN
IF (:old.Cod_Comp != :new.Cod_Comp ) THEN
BEGIN
UPDATE REDCOMPANIA
SET Cod_Comp = :new.Cod_Comp
WHERE REDCOMPANIA.Cod_Comp = :old.Cod_Comp ;
END;
END IF;
END;
/
```
## Predicados condicionales
Un mismo trigger puede ser disparado por múltiples operaciones o eventos de disparo. Para indicarlo se utilizará el operador OR. Para facilitar el control, Oracle permite la utilización de predicados condicionales que devolverán un valor verdadero o falso para cada una de las posibles operaciones: INSERT, DELETE o UPDATE.
Dichos predicados son, respectivamente, **IF INSERTING, IF DELETING** e **IF UPDATING**.
***CREATE** [OR REPLACE] **TRIGGER** nombre_trigger*
***BEFORE INSERT OR DELETE OR UPDATE OF** columna **ON** nombre_tabla*
***FOR EACH ROW***
***BEGIN***
***IF DELETING THEN***
***. . .***
> ***ELSIF DELETING THEN***
>
> ***. . .***
>
> ***ELSE - - estará actualizando, UPDATING***
>
> ***. . .***
>
> ***ENDIF***
***END;***
## TRIGGERS DEL TIPO INSTEAD OF
Hay un tipo de trigger especial que se llama **INSTEAD OF** y que sólo se utiliza con las vistas. Una vista es una consulta SELECT almacenada. En general sólo sirven para mostrar datos, pero podrían ser interesantes para actualizar. Por ejemplo, si partimos de las siguientes tablas y vista correspondiente:
> PIEZAS (<u>tipo</u>, <u>modelo</u>, precio_venta)
>
> EXISTENCIAS (<u>tipo</u>, <u>modelo</u>, n\_<u>almacen</u>, cantidad)
>
> EXISTENCIASCOMPLETA ( tipo, modelo, precio, almacen, cantidad);
>
> ***CREATE VIEW** **existenciasCompleta ( tipo, modelo, precio, almacen, cantidad)***
***AS***
***SELECT p.tipo, p.modelo, p.precio_venta, e.n_almacen, e.cantidad***
***FROM PIEZAS p, EXISTENCIAS e***
***WHERE p.tipo = e.tipo AND p.modelo = e.modelo***
***ORDER BY p.tipo, p.modelo, e.n_almacen;***
La siguiente instrucción daría lugar a error
*INSERT INTO existenciasCompleta VALUES (‘X01’, ‘007’, 53.75, 4, 21);*
indicando que esa operación no es válida en esa vista ( al utilizar dos tablas). Esta situación la puede arreglar un trigger insertando primero en la tabla de piezas ( sólo si no se encuentra ya insertada esa pieza) y luego insertando en existencias.
Eso lo realiza el trigger de tipo INSTEAD OF, que sustituirá el INSERT original por el indicado por el trigger:
> ***CREATE OR REPLACE TRIGGER tr_insert_piezasexistencias***
***INSTEAD OF INSERT***
***ON existenciasCompleta***
***BEGIN***
***INSERT INTO PIEZAS ( tipo, modelo, precio_venta)***
***VALUES (:new.tipo, :new.modelo, :new.precio);***
***INSERT INTO EXISTENCIAS ( tipo, modelo, n_almacen, cantidad)***
***VALUES (:new.tipo, :new.modelo, :new.almacen, :new.cantidad);***
***END;***
***/***
Este trigger permite añadir a esa vista añadiendo los campos necesarios en las tablas relacionadas en la vista. Se podría modificar el trigger para permitir actualizar, eliminar o borrar datos directamente desde la vista y así desde cualquier acceso a la base de datos se utilizaría esa vista como si fuera una tabla más.
## TRIGGERS DEL SISTEMA
Se disparan cuando se produce un suceso del sistema o se activa una instrucción DDL y su sintaxis general es la siguiente:
***CREATE** [OR REPLACE] **TRIGGER** nomtrigger*
*{ BEFORE | AFTER }*
*{ \<lista eventos definición\> | \<lista eventos del sistema\> }*
***ON** { DATABASE | SCHEMA } [WHEN ( condicion)] ]*
*\< cuerpo del trigger ( bloque PL/SQL) \> ;*
donde:
- \<lista eventos definición\> puede incluir uno o más eventos DDL separados por OR
- \<lista eventos del sistema\> puede incluir uno o más eventos del sistema separados por OR.
- El especificador ON DATABASE | SCHEMA indica el nivel de disparo del trigger:
 - ON DATABASE se disparará siempre que ocurra el evento de disparo
 - ON SCHEMA ocurrirá si el esquema ocurre dentro del esquema determinado por el trigger, que por defecto es aquel al que pertenece el trigger.
Algunos eventos de sistema y su momento de disparo son:
| | | |
|------------|-----------------|-----------------------------------------------------------|
| **EVENTO** | **MOMENTO** | **SE DISPARAN:** |
| STARTUP | AFTER | Después de iniciar la instancia de la Base de Datos |
| SHUTDOWN | BEFORE | Antes de parar la instancia de la Base de Datos |
| LOGON | AFTER | Después de conectarse a la Base de Datos |
| LOGOFF | BEFORE | Antes de que un usuario se desconecte de la Base de Datos |
| CREATE | BEFORE | AFTER | Antes o después de crear un objeto en el esquema |
| DROP | BEFORE | AFTER | Antes o después de eliminar un objeto en el esquema |
| ALTER | BEFORE | AFTER | Antes o después de modificar un objeto en el esquema |
| GRANT | BEFORE | AFTER | Antes o después de conceder un permiso |
| REVOKE | BEFORE | AFTER | Antes o después de revocar un permiso |
<u>Ejemplo</u>: Vamos a auditar los accesos a la base de datos, así como todos los eventos generados por instrucciones DDL. Para ello, primeramente creamos una tabla denominada CTRL_ACCESOS en un usuario con privilegios de administrador.
> CREATE TABLE ctrl_accesos (
>
> usuario VARCHAR2 ( 20),
>
> instante TIMESTAMP,
>
> evento VARCHAR2 ( 20)
>
> );
Posteriormente creamos el disparador: `( Scripts\ControlAccesos.sql)`
```sql
CREATE OR REPLACE TRIGGER tr_Control_Accesos
AFTER DDL OR LOGON ON DATABASE
BEGIN
INSERT INTO ctrl_accesos ( usuario, instante, evento)
VALUES ( USER, SYSTIMESTAMP, ORA_SYSEVENT || '**' || ORA_DICT_OBJ_NAME);
END;
/
```
Realizamos diversos accesos con diferentes usuarios y generamos diversas instrucciones DDL.
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image13.png)
## ELIMINACIÓN DE TRIGGERS
***DROP TRIGGER** nombretrigger;*
## RECOMPILACIÓN DE TRIGGERS
***ALTER TRIGGER** nombretrigger **COMPILE**;*
## ACTIVACIÓN/DESACTIVACIÓN DE TRIGGERS
***ALTER TRIGGER** nombretrigger **DISABLE**;*
## Activar triggers
***ALTER TRIGGER** nombretrigger **ENABLE**;*
## Desactivar o activar todos los triggers de una tabla
Eso permite en una sola instrucción operar con todos los triggers relacionados con una determinada tabla ( es decir actúa sobre los triggers que tienen dicha tabla en el apartado ON del trigger).
***ALTER TABLE** nombretabla { **DISABLE** | **ENABLE} ALL TRIGGERS**;*
## Vistas con información de los triggers
Al igual que otros objetos de la BD como tablas, vistas o usuarios, se puede consultar información sobre los triggers en las visas **DBA_TRIGGERS** y **USER_TRIGGERS.**
