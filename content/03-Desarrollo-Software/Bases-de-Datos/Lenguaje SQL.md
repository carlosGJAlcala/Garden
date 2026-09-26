---
title: "Lenguaje SQL"
---

# Lenguaje SQL
[1.1 INTRODUCCIÓN 3](#introducción)
[1.1.1 Tipos de sentencias SQL 3](#tipos-de-sentencias-sql)
[1.2 TIPOS DE DATOS 3](#tipos-de-datos)
[1.3 CREACIÓN DE UNA BASE DE DATOS 5](#creación-de-una-base-de-datos)
[1.3.1 Crear una tabla 6](#crear-una-tabla)
[1.3.2 Restricciones sobre una tabla 7](#restricciones-sobre-una-tabla)
[1.3.3 Modificar una tabla 13](#modificar-una-tabla)
[1.3.4 Modificar restricciones. ALTER TABLE 15](#modificar-restricciones.-alter-table)
[1.3.5 Eliminar una tabla. DROP TABLE 16](#eliminar-una-tabla.-drop-table)
[1.3.6 Insertar datos en una tabla. INSERT 16](#insertar-datos-en-una-tabla.-insert)
[1.3.7 Borrar datos de una tabla. DELETE y TRUNCATE 17](#borrar-datos-de-una-tabla.-delete-y-truncate)
[1.3.8 Actualización de tablas. UPDATE 17](#actualización-de-tablas.-update)
[1.3.9 Transacciones. ROLLBACK, COMMIT, AUTOCOMMIT 18](#transacciones.-rollback-commit-autocommit)
[1.4 CONSULTA DE DATOS 19](#consulta-de-datos)
[1.4.1 Cláusula SELECT 19](#cláusula-select)
[1.4.2 Cláusula WHERE 20](#cláusula-where)
[1.4.3 Cláusula ORDER BY 21](#cláusula-order-by)
[1.4.4 Alias de columnas 22](#alias-de-columnas)
[1.4.5 Uso de operadores aritméticos: +, -, **, / 22](#uso-de-operadores-aritméticos--)
[1.4.6 Coincidencia de patrones. LIKE y NOT LIKE 22](#coincidencia-de-patrones.-like-y-not-like)
[1.4.7 NULL y NOT NULL 23](#null-y-not-null)
[1.4.8 Cláusula BETWEEN…AND 23](#cláusula-betweenand)
[1.4.9 Cláusula IN 24](#cláusula-in)
[1.4.10 Conteo de filas. COUNT 24](#conteo-de-filas.-count)
[1.4.11 Cláusula para la agrupación de elementos: GROUP BY y HAVING TO 25](#cláusula-para-la-agrupación-de-elementos-group-by-y-having-to)
[1.4.12 Combinación de tablas 26](#combinación-de-tablas)
[1.4.13 Consultas anidadas: subconsultas 28](#consultas-anidadas-subconsultas)
[1.4.14 Union, Intersect y Minus 29](#union-intersect-y-minus)
[1.5 CREAR TABLAS CON DATOS RECUPERADOS DE UNA CONSULTA 32](#crear-tablas-con-datos-recuperados-de-una-consulta)
[1.6 CREACIÓN Y USO DE VISTAS. CREATE VIEW 32](#creación-y-uso-de-vistas.-create-view)
[1.6.1 Crear una vista. CREATE VIEW 32](#crear-una-vista.-create-view)
[1.6.2 Consultar las vistas existentes. USER_VIEWS 33](#consultar-las-vistas-existentes.-user_views)
[1.6.3 Borrar una vista. DROP VIEW 33](#borrar-una-vista.-drop-view)
[1.6.4 Operaciones sobre vistas 33](#operaciones-sobre-vistas)
[1.6.5 Vistas definidas sobre más de una tabla 34](#vistas-definidas-sobre-más-de-una-tabla)
[1.6.6 Manejo de expresiones y de funciones en vistas 35](#manejo-de-expresiones-y-de-funciones-en-vistas)
[1.7 SECUENCIAS 36](#secuencias)
[1.7.1 Crear secuencias 36](#crear-secuencias)
[1.7.2 Borrar secuencias 38](#borrar-secuencias)
[1.8 FUNCIONES 38](#funciones)
[1.8.1 Funciones aritméticas 38](#funciones-aritméticas)
[1.8.2 Funciones de cadenas de caracteres 40](#funciones-de-cadenas-de-caracteres)
[1.8.3 Funciones de manejo de fechas 43](#funciones-de-manejo-de-fechas)
[1.8.4 Funciones de conversión 43](#funciones-de-conversión)
[1.9 OTRAS FUNCIONES 46](#otras-funciones)
## INTRODUCCIÓN 
Una vez analizado un problema y diseñada la solución informática que lo resuelve a través de los modelos conceptual, lógico y físico, llega el momento de construir una solución. Empieza ahora la **fase de implementación**. A partir de ahora se realiza:
- Programación de las funciones del sistema
- Creación y poblado de la Base de Datos
- Programación de accesos a la Base de Datos
Al final de las de las etapas de diseño ( y fundamentalmente con la ayuda de alguna herramienta CASE) se obtuvo la estructura de las tablas que conformarán nuestra Base de Datos. Esta estructura deberá ser *incorporada* al sistema, para posteriormente *poblarla* con información y realizar las *consultas* y *actualizaciones* necesarias y propias de la labor empresarial.
## # Tipos de sentencias SQL
**<u>DDL</u>** (*Lenguaje de Descripción de Datos*) sirven para crear y mantener la estructura de la BD.
Con ellas podremos:
- Crear** un objeto de BD: tablas, vistas, procedimientos, ... ( orden **CREATE**)
- Eliminar** un objeto de BD ( orden **DROP**)
- Modificar** un objeto de BD ( orden **ALTER**)
- Conceder privilegios** sobre un objeto de BD ( orden **GRANT**)
- Retirar privilegios** sobre un objeto de BD ( orden **REVOKE**)
**<u>DML</u>** *( Lenguaje de Manipulación de Datos*) sirven para manipular los datos contenidos en la BD. Con ellas podremos
- Insertar** filas de datos a una tabla ( orden **INSERT**)
- Modificar** filas de datos en una tabla ( orden **UPDATE**)
- Eliminar** filas de datos en una tabla ( orden **DELETE**)
- Recuperar** filas de datos de una tabla o vista ( orden **SELECT**)
## TIPOS DE DATOS 
**CHAR ( n)**
Permite almacenar *cadenas de caracteres* de ***longitud fija*** ( entre 1 y 255 caracteres.).
Si se introduce una cadena de menor longitud que la definida, *se rellena con blancos a la derecha hasta que quede completa*. Si la cadena es de mayor longitud que la fijada, Oracle devolverá un error.
**VARCHAR2 ( n)**
Almacena *cadenas de caracteres* de ***longitud variable***. Longitud máxima es de 2000 caracteres.
Si se introduce una cadena de menor longitud que la definida, se almacenará con esa longitud *<u>NO</u> rellenando con caracteres a la derecha*. Si la cadena es de mayor longitud que la fijada, Oracle devolverá un error.
**NUMBER ( Precision, Escala)**
Almacena datos *numéricos enteros y decimales, con o sin signo*.
***Precisión***: representa el número total de dígitos que va a tener el dato; el rango va de 1 a 38.
***Escala***: representa el nº de dígitos a la derecha del punto decimal; si es negativa indica ceros a la izquierda del decimal.
**NUMBER ( Precisión)**
Este formato especifica *números enteros*.
**NUMBER**
Representa un *decimal con precisión 38*. Almacena el dato tal y como se introduzca, sea entero o decimal. Ejemplos de datos correspondientes a tipos NUMBER son:
> <u>Dato Actual Formato Almacenamiento</u>
>
> 7456123.89 NUMBER 7456123.89
>
> 7456123.89 NUMBER ( 9) 7456124
>
> 7456123.89 NUMBER ( 9,2) 7456123.89
>
> 7456123.89 NUMBER ( 9,1) 7456123.9
>
> 7456123.8 NUMBER ( 6) ERROR
>
> 7456123.8 NUMBER ( 15,1) 7456123.8
>
> 7456123.89 NUMBER ( 7,-2) 7456100
>
> 7456123.89 NUMBER (-7,2) ERROR
**LONG**
Almacena cadenas de *caracteres de longitud variable de hasta 2 gigabytes de información*. Se usa para almacenar textos muy grandes. Sólo se puede definir una columna LONG por tabla. Presenta las siguientes restricciones:
- No pueden aparecer en restricciones de integridad ( constraints).
- No sirve para indexar
- Una función almacenada no puede devolver un valor LONG
- No puede ser argumento de funciones
- No se puede usar en cláusulas WHERE, GROUP BY, ORDER BY, CONNECT BY, DISTINCT ni con operaciones de UNION, INTERSECT o MINUS.
**DATE**
Almacena información de *fechas y horas*. Por defecto, el formato es DD/MM/YY. Se puede cambiar este formato con la orden ALTER SESSION ( parámetro NLS_DATE_FORMAT).
**RAW y LONG RAW**
Sirve para almacenar *datos binarios*. RAW almacena cadenas de hasta 255 bytes y LONG RAW de hasta 2 gigabytes, se usa para almacenamiento de gráficos, sonidos, etc.
**ROWID**
*<u>Cada fila de una tabla tiene una dirección que la identifica de forma única</u>*. Podemos consultar dicha dirección preguntando por la columna ROWID. Utiliza una representación binaria de la localización física de la fila.
## CREACIÓN DE UNA BASE DE DATOS
Vamos a crear una BD con información de empleados y departamentos.
Primero crearemos una tabla que contenga un registro para cada uno de los empleados de la empresa con la siguiente información:
- Código de empleado
- Dni
- Nombre
- Edad
- Sexo
- Fecha de ingreso
- Código de Departamento
## # 
## # Crear una tabla
Para crear una tabla[^1] en SQL usaremos la sentencia ***CREATE TABLE*** cuya sintaxis general es:
> ***CREATE TABLE** NOMBRETABLA (*
>
> *COLUMNA1 TIPO DE DATO*
>
> *[CONSTRAINT NOMBRERESTRICCIÓN]*
>
> *[NOT NULL]*
>
> *[UNIQUE]*
>
> *[PRIMARY KEY]*
>
> *[DEFAULT VALOR]*
>
> *[REFERENCES NOMBRETABLA [ ( COLUMNA [,COLUMNA] ) ] [ON DELETE CASCADE] ]*
>
> *[CHECK CONDICIÓN] ,*
>
> *COLUMNA2 TIPO DE DATO*
>
> *[CONSTRAINT NOMBRERESTRICCIÓN]*
>
> *[NOT NULL]*
>
> *[UNIQUE]*
>
> *[PRIMARY KEY]*
>
> *[DEFAULT VALOR]*
>
> *[REFERENCES NOMBRETABLA [ ( COLUMNA [,COLUMNA] ) ] [ON DELETE CASCADE] ]*
>
> *[CHECK CONDICIÓN],*
>
> *................*
>
> *);*
Por ejemplo, para crear la tabla de empleados:
> *SQL\> **CREATE TABLE** empleados*
>
> *(*
>
> *Cod_Empl CHAR ( 5) NOT NULL,*
>
> *Dni CHAR ( 9) NOT NULL,*
>
> *Nombre VARCHAR ( 40) NOT NULL,*
>
> *Edad NUMBER ( 3),*
>
> *Sexo CHAR ( 1),*
>
> *Fec_Ingreso DATE NOT NULL,*
>
> *Cod_Depto CHAR ( 3),*
>
> *CONSTRAINT CLAVE_P PRIMARY KEY ( Cod_Empl)*
>
> *) TABLESPACE USERS;*
Podemos comprobar que la tabla ha sido creada mediante la siguiente consulta:
> SQL\> ***select** table_name **from** user_tables;*
Y que además ha sido creada con el formato que realmente queríamos:
> SQL\> ***desc** empleados*
## # Restricciones sobre una tabla
La orden CREATE TABLE permite definir distintos tipos de **restricciones** sobre una tabla, con ayuda de la cláusula ***CONSTRAINT** nombrerestricción restriccion*:
- Claves primarias ( PRIMARY KEY)
- Claves ajenas ( FOREIGN KEY)
- Obligatoriedad ( NOT NULL)
- Valores por defecto ( DEFAULT)
- Verificación de condiciones ( CHECK)
- Restricción UNIQUE.
Existen dos modos de especificar restricciones:
- RESTRICCIÓN DE COLUMNA:** como parte de la definición de columnas.
> Si se define una restricción sin darle un nombre, por defecto, Oracle le asigna un nombre del tipo SYS_C00n, donde **n** es un número asignado automáticamente por Oracle.
>
> *CREATE TABLE empleados (*
>
> *Cod_Empl CHAR ( 5) PRIMARY KEY ,*
>
> *...*
>
> *...*
- RESTRICCION DE TABLA:** al final, una vez especificadas todas las columnas.
> *CREATE TABLE empleados (*
>
> *Cod_Empl CHAR ( 5) ,*
>
> *...*
>
> *...*
>
> ***CONSTRAINT** CLAVE_P PRIMARY KEY ( nombre),*
>
> *...*
### # La restricción PRIMARY KEY
*<u>Una **clave primaria** es una columna o conjunto de columnas que el diseñador ha elegido para identificar de manera única una fila de una tabla</u>*.
Las claves proporcionan una manera rápida y eficiente de buscar datos en una tabla, además de que permiten preservar la integridad de los datos. <u>Cuando se crea una clave primaria, automáticamente se crea un índice que facilita el acceso a la tabla</u>.
La restricción PRIMARY KEY se usa para definir una **clave primaria** dentro de una tabla.
> *CREATE TABLE empleados (*
>
> *Cod_Empl CHAR ( 5) ,*
>
> *...)*
>
> *CREATE TABLE empleados (*
>
> *Cod_Empl CHAR ( 5) ,*
>
> *...*
>
> ***CONSTRAINT** CLAVE_P PRIMARY KEY ( Cod_Empl)*
>
> *…)*
### # La restricción FOREIGN KEY
En la mayoría de las ocasiones es necesario relacionar dos o más tablas. Es algo intrínseco a la vida real y que ya quedó reflejado en el esquema relacional ( grafo relacional) dentro del diseño lógico.
Para poder relacionar dos tablas, es necesario asignar un ***<u>campo en común</u>*** a las dos tablas. En nuestro ejemplo, el campo *Cod_Depto* existe tanto en la tabla *empleados* como en la tabla *departamentos*.
*<u>Una **clave foránea** o **ajena** es una columna en una tabla que se corresponde con la clave primaria de otra tabla</u>*. En nuestro ejemplo, la columna *Cod_Depto* en la tabla *empleados* es la clave foránea y se debe corresponder con la clave primaria de la tabla Departamentos.
Para trabajar con claves foráneas, la sentencia CREATE TABLE proporciona la cláusula
> ***FOREIGN KEY**( campo_fk)*
>
> ***REFERENCES** nombre_tabla ( nombre_campo)*
que se puede usar en dos formatos distintos:
- <u>Formato de restricción de columna:</u>**
*CREATE TABLE nom_tabla (*
*col1 TIPO_DE_DATO*
*[CONSTRAINT nombre_restr]*
***REFERENCES** nombretabla [( col)]*
*[**ON DELETE CASCADE**]*
*col2 TIPO_DE_DATO*
….. *)*
- <u>Formato de restricción de tabla:</u>**
*CREATE TABLE nom_tabla (*
*col1 TIPO_DE_DATO*
*Col2 TIPO_DE_DATO*
…..
*[CONSTRAINT nombre_restr]*
***FOREIGN KEY** ( col [,[col])*
***REFERENCES** nombretabla [( col)]*
***[ON DELETE CASCADE]|[ON SET NULL]**)*
A continuación se muestra cómo definir dos tablas de ejemplo con una clave foránea. Las tablas se van a llamar: clientes y ventas
> *CREATE TABLE clientes (*
>
> *id_cliente NUMBER ( 5),*
>
> *nombre VARCHAR2 ( 40),*
>
> *PRIMARY KEY ( id_cliente));*
>
> *CREATE TABLE ventas (*
>
> *id_factura NUMBER ( 5),*
>
> *id_cliente NUMBER ( 5) NOT NULL,*
>
> *cantidad NUMBER ( 5),*
>
> *PRIMARY KEY ( id_factura),*
>
> ***FOREIGN KEY** ( id_cliente) **REFERENCES** clientes ( id_cliente));*
**<u>Acciones de creación y borrado.</u>**
- En el ejemplo, se debe crear primero la tabla CLIENTES y después la tabla VENTAS, ya que VENTAS referencia a CLIENTES. Si lo hacemos al revés, Oracle dará un error.
- Si queremos borrar las tablas, comenzamos borrando la tabla VENTAS y después, la tabla CLIENTE. Si lo hacemos al revés, Oracle dará un mensaje de error.
- Si queremos eliminar algún cliente en la tabla CLIENTES y que las filas correspondientes en la tabla VENTAS con ese id_cliente sean eliminadas automáticamente por Oracle, se añadirá la cláusula **ON DELETE CASCADE** en la opción **REFERENCES**:
*FOREIGN KEY ( id_cliente) REFERENCES clientes ( id_cliente)*
***ON DELETE CASCADE***
Se puede dar un nombre a la restricción con la cláusula CONSTRAINT[^2]:
> *CONTRAINT FK_VENT FOREIGN KEY ( id_cliente) REFERENCES clientes ( id_cliente) ON DELETE CASCADE*
Se pueden agregar restricciones de clave foránea a una tabla con el uso de la sentencia **ALTER TABLE**.
***ALTER TABLE** nombre_tabla*
*ADD [CONSTRAINT símbolo]*
***FOREIGN KEY**(...) **REFERENCES** otra_tabla (...) [**ON DELETE CASCADE**]*
### # La restricción de obligatoriedad NOT NULL
Esta restricción asociada a una columna significa que no puede tener valores nulos, es decir que ha de tener obligatoriamente un valor. En caso contrario, causa una excepción.
*CREATE TABLE persona*
*(*
*NIF VARCHAR2 ( 10) **NOT NULL**,*
*...*
*EDAD NUMBER ( 2) **CONSTRAINT** Edad_nonula **NOT NULL***
*);*
### # Valores por defecto. DEFAULT
En el momento de crear una tabla podemos asignar valores por defecto a las columnas, es decir, un valor por omisión cuando el valor de la columna no se especifica al insertar una tupla.
En la especificación **DEFAULT** es posible incluir varias expresiones: constantes, funciones SQL y variables UID y SYSDATE.
*CREATE TABLE altaempleado*
*(*
*NIF VARCHAR2 ( 10) NOT NULL,*
*NOMBRE VARCHAR ( 30) NOT NULL,*
*DIRECCION VARCHAR2 ( 40) **DEFAULT** ‘ ‘,*
*EDAD NUMBER ( 2),*
*FECHA DATE **DEFAULT** SYSDATE*
*);*
Si insertamos una fila en la tabla dando valores a todas las columnas salvo a DIRECCION y FECHA:
*INSERT INTO altaempleado ( DNI, NOMBRE, EDAD) VALUES (´1234´, ´PEPA´, 21);*
Al visualizar el contenido de la tabla, en la columna FECHA se almacenará la fecha del sistema ya que no se dio valor a la columna FECHA *( SELECT ** FROM altaempleados;)*
### # La restricción UNIQUE
<u>Evita valores repetidos en una o más columnas</u>. La diferencia con la restricción PRIMARY KEY es que ésta es única y en cambio puede haber varias restricciones **UNIQUE** definidas en una misma tabla. Al igual que en PRIMARY KEY, cuando se define una restricción UNIQUE se crea un índice automáticamente.
Restricción de columna sin nombre:
*CREATE TABLE alumnos (*
*dni VARCHAR2 ( 20) PRIMARY KEY,*
*nmat VARCHAR2 ( 20) **UNIQUE***
*…*
Restricción de tabla con nombre:
*CREATE TABLE columnas (*
*…..*
***CONSTRAINT** R_UNI **UNIQUE** ( nmat))*
### # La restricción CHECK
La restricción **CHECK** nos permite definir los dominios de los campos. La siguiente restricción va a impedir que el campo sexo admita un valor distinto a F ( Femenino) o M ( masculino).
> *CREATE TABLE mascotas*
>
> *(*
>
> *nombre VARCHAR ( 20) NOT NULL,*
>
> *propietario VARCHAR ( 20),*
>
> *especie VARCHAR ( 20),*
>
> *sexo CHAR ( 1) **CHECK ( sexo=‘M’ OR sexo=‘F’)**,*
>
> *nacimiento DATE,*
>
> *fallecimento DATE,*
>
> *CONSTRAINT CLAVE_P PRIMARY KEY ( nombre)*
>
> *);*
Algunos ejemplos de uso de CHECK:
> CHECK ( CURSO IN ( 1, 2 ,3))
>
> CHECK ( EDAD BETWEEN 5 AND 20)
>
> CHECK ( NOMBRE=UPPER ( NOMBRE))
>
> CHECK ( A IS NOT NULL) equivale a la restricción NOT NULL.
## # Modificar una tabla
Para modificar la estructura de una tabla utilizamos la sentencia **ALTER TABLE.** Su sintaxis es la siguiente:
```
ALTER TABLE nombretabla
{ [ ADD ( columna [,columna] …) ]
[ MODIFY ( columna [,columna] …) ]
[ ADD CONSTRAINT restriccion ]
[ DROP CONSTRAINT restriccion ] };
Si la elección de la longitud de los campos no es adecuada, la sentencia ALTER TABLE nos permitirá cambiarlos. Se puede aumentar la longitud de una columna en cualquier momento pero no es posible disminuir la longitud de una columna si no está vacía. Para modificar el tamaño del campo propietario:
> *ALTER TABLE empleados*
>
> ***MODIFY** Cod_Depto CHAR ( 5);*
Para <u>añadir una nueva columna</u> a la tabla *empleados*:
*ALTER TABLE empleados*
***ADD** Direccion VARCHAR2 ( 40);*
Para <u>eliminar una columna</u> de la tabla:
*ALTER TABLE empleados*
***DROP** COLUMN Sexo;*
Para <u>cambiar el nombre de una columna</u> de la tabla:
*ALTER TABLE empleados*
***RENAME** **COLUMN** Sexo **TO** Genero;*
Para c<u>ambiar el nombre</u> de la tabla:
*ALTER TABLE empleados*
***RENAME TO** colaboradores;*
## # Modificar restricciones. ALTER TABLE
```
Con **ALTER TABLE** también se pueden añadir, modificar y borrar restricciones en una tabla y/o índices. Para consultar las restricciones asociadas a la tabla empleados:
*SELECT table_name, constraint_name, constraint_type*
*FROM user_constraints*
*WHERE table_name = ´empleados´;*
El tipo de CONSTRAINT ( CONSTRAINT TYPE) puede ser:
- C: Restricciones de tipo CHECK
- P: Restricción PRIMARY KEY
- R: Restricción FOREIGN KEY ( References)
- U: Restricción UNIQUE
Para <u>borrar una restricción</u>, por ejemplo, la clave primaria:
*ALTER TABLE empleados **DROP CONSTRAINT** CLAVE_P;*
*CLAVE_P* es el nombre dado a la restricción de clave primaria cuando se creó la tabla.
<u>Añadir una restricción</u>, por ejemplo, añadir de nuevo la restricción de clave primaria
*ALTER TABLE empleados*
***ADD CONSTRAINT** CLAVE_P*
*PRIMARY KEY ( Cod_Empl);*
Comprobamos:
> *SELECT constraint_name, constraint_type*
>
> *FROM user_constraints;*
Un ejemplo para añadir una restricción check sería la siguiente:
*ALTER TABLE empleados*
***ADD** **CONSTRAINT** check_sexo*
***CHECK** ( sexo=‘H’ OR sexo=‘M’)*
<u>Esta restricción también se pueden especificar en la sentencia CREATE TABLE dando o no nombre a la restricción.</u>
## # Eliminar una tabla. DROP TABLE
La orden **DROP TABLE** la estructura de una tabla, es decir, la elimina del diccionario de datos. Además elimina todos los datos pudiera contener la tabla.
***DROP TABLE** [usuario].nombre_tabla*
Para eliminar una tabla a la que se haga referencia con una restricción FOREIGN KEY:
***DROP TABLE** nombre_tabla **CASCADE CONSTRAINTS**;*
Esta opción suprime todas las restricciones de integridad referencial que se refieran a claves de la tabla borrada.
## # Insertar datos en una tabla. INSERT
Con la sentencia **INSERT** se añaden filas de datos en una tabla.
***INSERT INTO** NombreTabla [ ( col [,col] …)] **VALUES** ( valor [,valor] …);*
Si los nombres de columnas no se especifican, se consideran, por defecto, todas las columnas de la tabla.
Los valores se deben corresponder con cada una de las columnas que aparecen; además, deben coincidir con el tipo de dato definido para cada columna.
Cualquier columna que no se encuentre en la lista de columnas y no tenga definido un valor por defecto recibirá el valor NULL, siempre y cuando no esté definida como NOT NULL, en cuyo caso INSERT fallará.
Un ejemplo para insertar datos en la tabla empleado podría ser:
*INSERT INTO empleados* VALUES ('S0001', '50237441L', 'Ana García', 23, 'M', '29/07/97', NULL);
*INSERT INTO empleados* VALUES ('S0002', '01837441M', 'Rafael Gómez', NULL, 'H', '01/03/04', ‘523’);
Los valores de cadenas y fechas deben estar encerrados entre comillas. Podemos insertar el valor NULL directamente para representar un valor que no conocemos.
## # Borrar datos de una tabla. DELETE y TRUNCATE
Se pueden eliminar registros de una tabla usamos la sentencia **DELETE**
***DELETE FROM** empleados*
***WHERE** nombre = ‘Ana’*;
Sin la cláusula WHERE, borrará todas las filas de la tabla:
***DELETE FROM** empleados;*
También disponemos de la orden **TRUNCATE**, que nos permite suprimir todas las filas de una tabla y liberar el espacio ocupado para otros usos sin que desaparezca la definición de la tabla de la BD.
Es una orden DDL que no genera información de retroceso ( ROLLBACK), es decir, una sentencia TRUNCATE no se puede anular. Por eso su ejecución es más rápida que DELETE.
***TRUNCATE TABLE** [usuario.]nombretabla*
## # 
## # Actualización de tablas. UPDATE
La sentencia **UPDATE** sirve para actualizar datos de las tablas de una BD.
***UPDATE** empleados*
***SET** Direccion=‘Gran Vía 241’, Sexo=‘M’ **WHERE** Nombre=‘Ana García’;*
Si se omite WHERE, se actualizan todas las filas de la tabla destino.
***UPDATE** empleados SET Sexo=‘M’;*
## # Transacciones. ROLLBACK, COMMIT, AUTOCOMMIT
Si por error o descuido borráramos datos de una tabla, esto no sería un problema ya que Oracle permite dar marcha atrás a un trabajo realizado usando la orden **ROLLBACK** siempre y cuando no hayamos validado los cambios en la BD mediante la orden **COMMIT**.
<u>Cuando hacemos transacciones sobre la BD ( insertamos, actualizamos y eliminamos datos en las tablas) los cambios no serán efectivos en la BD hasta que no hagamos un COMMIT</u>. Si durante el tiempo que hemos estado haciendo transacciones, no hemos hecho ningún *commit* y de pronto se va la luz, todo nuestro trabajo se habrá perdido y las tablas quedarán en la situación de partida.
Para <u>validar cambios</u> en la BD ejecutaremos:
SQL\> ***COMMIT***;
Validación terminada
SQLPLUS permite validar automáticamente nuestras transacciones sin tener que indicarlo de forma explícita. Para este propósito sirve el parámetro **AUTOCOMMIT**.
SQL\> *SHOW AUTOCOMMIT*;
autocommit OFF
```
AUTOCOMMIT = OFF es el valor por omisión ===\> las transacciones ( INSERT, UPDATE y DELETE) no son definitivas hasta que no hagamos COMMIT.
Si queremos que tengan un carácter definitivo sin necesidad de realizar COMMIT activamos el parámetro:
SQL\> ***SET AUTOCOMMIT ON**;*
SQL\> *SHOW AUTOCOMMIT*;
autocommit INMEDIATE
SQL\> *INSERT INTO empleados* VALUES ('S0003', '50183741R', 'Jose Pérez', 24, 'H', '20/11/02', ‘430’);
1 fila creada.
Validación terminada.
Para <u>deshacer cambios</u> en la BD de las transacciones no validadas usaremos la orden:
SQL\> ***ROLLBACK***;
<u>Con la orden deshacemos los cambios que hemos realizado en las tablas desde el último COMMIT.</u>
**<u>COMMIT implícito</u>**
Hay varias órdenes SQL que fuerzan la ejecución de un COMMIT sin necesidad de indicarlo.
- QUIT, EXIT
- CONNECT, DISCONNECT
- CREATE TABLE, CREATE VIEW, DROP TABLE, DROP VIEW
- GRANT, REVOKE
- ALTER
- AUDIT, NOAUDIT
**<u>ROLLBACK automático</u>**
Si después de haber realizado cambios en nuestras tablas, se produce un fallo del sistema ( ej. se va la luz) y no hemos validado el trabajo, Oracle hace un ROLLBACK automático sobre cualquier trabajo no validado. Tendremos que repetir el trabajo al poner de nuevo en marcha la BD.
## CONSULTA DE DATOS
```
## # Cláusula SELECT
<u>Se usa para recuperar información de una tabla</u>. Sintaxis genérica es:
***SELECT** LaInformaciónQueDeseamos*
***FROM** DeQueTabla*
***WHERE** CondiciónASatisfacer*
LaInformaciónQueDeseamos puede ser una lista de columnas, o un ** para indicar "todas las columnas".
Recuperar <u>todos los datos</u> de una tabla:
*SELECT ** FROM empleados;*
<u>Si el usuario que hace la consulta no es el propietario de la tabla, es necesario especificar el nombre de usuario delante de ella: *nombre_usuario.nombre_tabla.*</u>
Para <u>seleccionar sólo las columnas</u> que nos interesan de la tabla, indicaremos su nombre después de la cláusula SELECT:
*SELECT Nombre, Direccion*
*FROM empleados;*
Por ejemplo, para conocer a qué departamento pertenece un empleado, hacemos la consulta:
*SELECT Cod_Depto FROM empleados;*
La consulta anterior recupera el código de departamento de cada empleado. Sin embargo, en la salida cada departamento aparecerá tantas veces como empleados tenga, lo cual no es muy adecuado. Para evitar esto y recuperar sólo las filas que son distintas, agregamos la palabra clave **DISTINCT**:
*SELECT **DISTINCT** Cod_Depto*
*FROM empleados;*
## # Cláusula WHERE
Para obtener las filas que cumplen una determinada condición usamos la cláusula **WHERE**:
*SELECT ** FROM empleados*
> ***WHERE** nombre=‘Ana García’;*
El formato de la condición es:
*expresión operador expresión*
Las expresiones pueden ser: una constante, una expresión aritmética, un valor nulo o un nombre de columna.
Los operadores de comparación pueden ser:
> =, \>, \<, \>=, \<=, !=, \<\>, IN, NOT IN, BETWEEN, NOT BETWEEN, LIKE
Se pueden construir condiciones múltiples usando los operadores lógicos booleanos estándares AND, OR y NOT. Se pueden emplear paréntesis para forzar el orden de evaluación. Veamos a continuación unos ejemplos:
*SELECT ** FROM empleados*
*WHERE Sexo = ‘H’ AND Edad = 27;*
*SELECT ** FROM empleados*
*WHERE ( Sexo = ‘H’ AND Edad = ‘H’) OR ( Sexo = ‘M’ AND Edad = 25);*
Otros ejemplos:
> *WHERE NOTA = 5*
>
> *WHERE ( NOTA\>=10) AND ( CURSO=1)*
>
> *WHERE ( NOTA IS NULL) OR ( UPPER ( NOM_ALUM)=‘PEDRO’)*
## # Cláusula ORDER BY
Para ordenar los resultados de una consulta, usamos la cláusula **ORDER BY**, tal y como se muestra a continuación.
*SELECT Nombre, F_Ingr*
*FROM empleados*
***ORDER BY** F_Ingr;*
<u>Por defecto, la ordenación es ascendente ( de menor a mayor). Para que sea descendente, deberemos indicárselo:</u>
*SELECT Nombre, F_Ingr*
*FROM empleados*
*ORDER BY F_Ingr **DESC**;*
Podemos ordenar múltiples columnas:
> *SELECT Nombre, Direccion, Cod_Depto, F_Ingr FROM empleados*
>
> *ORDER BY Cod_Depto, F_Ingr DESC;*
## # Alias de columnas
Cuando realizamos una consulta, las cabeceras de la salida coinciden con el nombre que tiene la columna cuando ésta fue creada. Como este nombre no siempre es suficientemente descriptivo, xxiste la posibilidad de cambiarlo con la misma sentencia SQL de consulta creando un **ALIAS**. <u>El ALIAS se pone entre comillas dobles, a la derecha de la columna</u>.
> *SELECT nombre “Nombre empleado”,*
>
> *F_Ingr “Fecha de Ingreso”*
>
> *FROM empleados;*
## # Uso de operadores aritméticos: +, -, **, /
Sirven para formar expresiones con constantes, valores de columnas y funciones de valores de columnas. Por ejemplo:
*SELECT col1**col2, col1-col2*
*FROM tabla1*
*WHERE col1+col2=34;*
## # 
## # Coincidencia de patrones. LIKE y NOT LIKE
Oracle proporciona métodos de coincidencia de patrones basados en SQL estándar: operador **LIKE**. <u>En Oracle, los patrones SQL son sensibles al uso de mayúsculas y minúsculas</u>. La coincidencia de patrones basada en SQL nos permite usar:
- \_ ( guión bajo) para un solo carácter
- % para un arbitrario número de caracteres ( cadena de 0 o más caracteres)
<u>No se usan los operadores =, \< o \> cuando se usan los patrones SQL; en su lugar se usan los operadores LIKE y NOT LIKE</u>
Para encontrar los nombres que comienzan con *b*:
*SELECT ** FROM empleados*
*WHERE Nombre **LIKE** ‘b%’;*
Para encontrar nombres cuyo penúltimo carácter no sea una *a*:
*SELECT ** FROM empleados*
*WHERE Nombre **NOT LIKE** ‘%a\_’;*
## # NULL y NOT NULL
Una columna de una fila es NULL si está completamente vacía. Para comprobar si el valor de una columna es nulo, usamos **IS NULL.** Para saber si el valor de una columna no es nulo usamos **IS NOT NULL.**
Por ejemplo para consultar los nombres de empleados que no tienen departamento asociado:
*SELECT Nombre*
*FROM empleados*
*WHERE Cod_Depto **IS NULL**;*
## # Cláusula BETWEEN…AND
El operador **BETWEEN** comprueba si un valor está comprendido o no ( NOT) dentro de un rango de valores, desde un valor inicial a un valor final.
Para obtener la información de los empleados que han ingresado en la empresa entre los años 2001 y 2005
*SELECT ** FROM empleados*
*WHERE TO_CHAR ( F_Ingr, ‘yyyy’)*
***BETWEEN** ‘2001’ **AND** ‘2005’;*
Para obtener la información de los empleados que no han ingresado en la empresa entre los años 1999 y 2003:
*SELECT ** FROM empleados*
*WHERE TO_CHAR ( F_Ingr, ‘yyyy’) **NOT BETWEEN** ‘1999’ **AND** ‘2003’;*
## # Cláusula IN
Comprueba si un valor dado coincide con uno de una lista de valores especificada.
Para tener la información de todos los empleados cuyo departamento sea ‘001’, ‘004’ o ‘009’:
*SELECT ** FROM empleados*
*WHERE Cod_Depto **IN** (‘001’, ‘004’, ‘009’);*
Empleados que no sean de los departamentos ‘001’ ni ‘005’:
*SELECT ** FROM empleados*
*WHERE Cod_Depto **NOT IN** (‘001’, ‘005’ );*
## # Conteo de filas. COUNT
Para contar las filas de una tabla usaremos la palabra **COUNT**. A continuación se muestra un ejemplo que nos devolverá el número de filas que hay en la tabla empleados.
*SELECT **COUNT (**)** FROM empleados;*
El operador COUNT puede tener distintos usos:
- COUNT (**):** devuelve el número de filas de una tabla incluidos los valores NULL y duplicados.
- COUNT ( columna):** devuelve el número de valores no NULL de la columna especificada.
- COUNT ( DISTINT columna):** devuelve el número de valores únicos no NULL de la columna especificada.
La siguiente consulta devuelve el número de departamentos distintos que hay en la tabla empleados:
*SELECT **COUNT**( DISTINCT Cod_Depto)*
*FROM empleados;*
Para saber cuántos empleados tienen informado el dato *Edad* emplearemos cualquiera de las siguientes consultas:
*SELECT COUNT ( Edad)*
*FROM empleados;*
*SELECT COUNT (**)*
*FROM empleados*
*WHERE Edad IS NOT NULL;*
## # Cláusula para la agrupación de elementos: GROUP BY y HAVING TO
La cláusula **GROUP BY** posibilita agrupar uno o más conjuntos de filas por las columnas en la sentencia SELECT.
Por ejemplo, para saber cuántos empleados tiene cada uno de los departamentos, realizaremos la siguiente consulta.
*SELECT Cod_Depto, COUNT (**)*
*FROM empleados **GROUP BY** Cod_Depto;*
<u>Se usa la cláusula GROUP BY para agrupar todas las filas de cada departamento. Si no se utilizara, daría error</u>. Para saber cuántos empleados hay por departamento y género podemos realizar la siguiente consulta:
*SELECT Cod_Depto, Sexo, COUNT (**)*
*FROM empleados **GROUP BY** Cod_Depto, Sexo;*
Al igual que existe la condición de búsqueda WHERE para filas individuales, también hay una condición de búsqueda para grupos de filas: **HAVING**. Esta condición se evalúa sobre la tabla que devuelve el GROUP BY, así que no puede existir sin GROUP BY.
*SELECT Cod_Depto, COUNT (**)*
*FROM empleados*
***GROUP BY** Cod_Depto*
***HAVING** COUNT (**) \>= 2*
*ORDER BY COUNT (**) DESC;*
Esta consulta obtiene el número de empleados por departamento siempre que haya al menos 2 empleados en el departamento. Además se ordena la salida por el número de empleados por departamento en orden descendente.
<u>ORDER BY se ejecutará detrás de las cláusulas WHERE, GROUP BY y HAVING.</u>
- WHERE: Selecciona las filas
- GROUP BY: Agrupa estas filas
- HAVING: Filtra los grupos. Selecciona y elimina los grupos
- ORDER BY: Clasifica la salida. Ordena los grupos.
## # Combinación de tablas
En las consultas realizadas hasta ahora sólo se ha utilizado una tabla. Hay veces que una consulta necesita columnas de varias tablas:
*SELECT columnas de las tablas deseadas*
*FROM tabla1, tabla2, …*
*WHERE **tabla1.columna = tabla2.columna***
Es posible unir tantas tablas como se desee. Si hay columnas con el mismo nombre en distintas tablas, se deben identificar: *nombretabla.nombrecolumna* Si el nombre de una columna existe sólo en una tabla, no es necesario especificarla como nombretabla.nombrecolumna. Sin embargo, hacerlo mejora la **legilibilidad**.
<u>El criterio que se siga para combinar las tablas ha de especificarse en la cláusula WHERE. Si se omite esta cláusula, que especifica la condición de combinación, el resultado será un PRODUCTO CARTESIANO, que emparejará todas las filas de una tabla con cada fila de la otra.</u>
Por ejemplo, obtener el nombre de cada empleado y el nombre del código del departamento para el que trabaja:
*SELECT empleados.nombre, departamentos.nombre*
*FROM empleados, departamentos*
*WHERE **empleados.Cod_Depto = departamentos.Cod_Depto***
En el ejemplo vemos que la cláusula FROM lista dos tablas ya que la consulta necesita información que se encuentra en ambas tablas.
Cuando se combina ( junta) información de múltiples tablas, es necesario especificar los registros de una tabla que pueden coincidir con los registros en la otra tabla. En este caso, ambas tablas tienen una columna común “nombre“: se usa la cláusula WHERE para obtener las filas cuyo valor en dicha columna es el mismo en ambas tablas.
Dado que la columna “Cod_Depto" ocurre en ambas tablas, debemos de especificar a cuál de las columnas nos referimos. Por eso anteponemos el nombre de la tabla al nombre de la columna.
Existe una variedad de combinación de tablas que se llama **OUTER JOIN** que <u>permite seleccionar algunas filas de una tabla aunque éstas no tengan correspondencia con las filas de la otra tabla con la que se combina</u>.
*SELECT tabla1.col1, tabla1.col2, tabla2.col1, tabla2.col2*
*FROM tabla1, tabla2*
*WHERE tabla1.col1 = tabla2.col1**(+)**;*
Se seleccionan todas las filas de la *tabla1* aunque no tengan correspondencia con las filas de la *tabla2*. El resto de columnas de la *tabla2* se rellena con NULL
## # Consultas anidadas: subconsultas
A veces, para realizar alguna operación de consulta, necesitamos los datos devueltos por otra consulta.
La forma de resolverlo es utilizar una **subconsulta**, es decir, una sentencia SELECT que forma parte de una cláusula WHERE de una sentencia SELECT anterior.
> *SELECT .....*
>
> *FROM ....*
>
> *WHERE columna operador_comparativo ( SELECT ...*
>
> *FROM ...*
>
> *WHERE ...);*
La subconsulta se ejecutará primero y, posteriormente, el valor extraído es “introducido” en la consulta principal.
Por ejemplo, para obtener todos los datos del empleado más antiguo:
*SELECT ** FROM empleados*
*WHERE F_Ingr = (**SELECT MIN ( F_Ingr)***
***FROM empleados**);*
Podemos tener subconsultas que generan más de una fila o más de un valor: en estos casos no usamos el operador **=** sino que se usa el operador **IN** en la cláusula WHERE.
Por ejemplo, para obtener los datos de los departamentos que tienen algún empleado de 22 o de 25 años:
*SELECT ***
*FROM departamentos*
*WHERE Cod_Depto **IN***
*( **SELECT DISTINCT Cod_Depto***
***FROM empleados***
***WHERE Edad IN ( 22, 25));***
## # Union, Intersect y Minus
Comencemos con un ejemplo. Supongamos tres tablas:
- ALUM: contiene los nombres de los alumnos que hay actualmente en el centro
- NUEVOS: contiene los nombres de los futuros alumnos.
- ANTIGUOS: contiene los nombres de antiguos alumnos del centro.
Las tres tablas tienen la misma estructura:
- Nombre varchar2 ( 15)
- Edad number ( 2)
- Localidad varchar2 ( 15)
SQL \> *SELECT ** FROM ALUM;*
> JUAN 18 COSLADA
>
> PEDRO 19 COSLADA
>
> ANA 17 ALCALA
>
> LUISA 18 TORREJON
>
> MARIA 20 MADRID
>
> ERNESTO 1 MADRID
>
> RAQUEL 19 TOLEDO
SQL \> *SELECT ** FROM NUEVOS;*
> JUAN 18 COSLADA
>
> MAITE 15 ALCALA
>
> SOFIA 14 ALCALA
>
> ANA 17 ALCALA
>
> ERNESTO 21 MADRID
SQL \> *SELECT ** FROM ANTIGUOS;*
> MARIA 20 MADRID
>
> ERNESTO 21 MADRID
>
> ANDRES 26 LAS ROZAS
>
> IRENE 24 LAS ROZAS
**UNION** combina los resultados de dos consultas reduciendo a una fila única las filas duplicadas.
*SELECT nombre FROM ALUM*
***UNION***
*SELECT nombre FROM NUEVOS;*
Esta consulta visualizará los nombres de los alumnos actuales y de los futuros alumnos. Utilizando **UNION ALL** aparecerán las filas duplicadas en el resultado de la consulta.
**INTERSECT** devuelve las filas que son iguales en ambas consultas. Todas las filas duplicadas serán eliminadas antes de la generación del resultado final.
*SELECT nombre FROM ALUM*
***INTERSECT***
*SELECT nombre FROM ANTIGUOS;*
Esta consulta visualizará los nombres de los alumnos que están actualmente en el centro y que estuvieron en el centro hace ya un tiempo. La consulta anterior también se puede hacer usando el operador **IN**:
*SELECT nombre FROM ALUM*
*WHERE NOMBRE **IN** ( SELECT nombre FROM ANTIGUOS);*
**MINUS** devuelve aquellas filas que están en la primera select y no están en la segunda. Las filas duplicadas del primer conjunto se reducirán a una fila única antes de que empiece la comparación con el otro conjunto.
Para visualizar los nombres y la localidad de los alumnos que están actualmente en el centro y que nunca estuvieron anteriormente en él haríamos la siguiente consulta:
*SELECT nombre, localidad FROM ALUM*
***MINUS***
*SELECT nombre, localidad FROM ANTIGUOS;*
o también
*SELECT nombre, localidad FROM ALUM*
*WHERE nombre **NOT IN** ( SELECT nombre FROM ANTIGUOS);*
Veamos algunos ejemplos. Seleccionar los nombres de la tabla ALUM que estén en NUEVOS y no estén en ANTIGUOS.
*SELECT nombre FROM ALUM*
*WHERE nombre **IN***
*( SELECT nombre FROM NUEVOS*
***MINUS***
*SELECT NOMBRE FROM ANTIGUOS);*
o también:
*SELECT nombre FROM ALUM*
*WHERE nombre **IN***
*( SELECT nombre FROM NUEVOS)*
*AND nombre **NOT IN***
*( SELECT NOMBRE FROM ANTIGUOS);*
### # Reglas de utilización de operadores de conjuntos
Para la utilización de los operadores de conjuntos se deben seguir las siguientes reglas:
- Las columnas de las dos consultas se relacionan en orden, de izquierda a derecha.
- Los nombres de columna de la primera select no tienen por qué ser los mismos que los nombres de la segunda
- Las SELECT necesitan tener el mismo nº de columnas.
- Los tipos de datos deben coincidir, aunque la longitud no tiene que ser la misma.
- Los operadores de conjuntos se pueden encadenar:
*SELECT … INTERSECT SELECT … UNION SELECT …*
- Los conjuntos se evalúan de izquierda a derecha. Para forzar precedencia se pueden utilizar paréntesis:
*SELECT … UNION ( SELECT … MINUS SELECT …)*
*( SELECT … UNION SELECT …) MINUS SELECT ….*
## CREAR TABLAS CON DATOS RECUPERADOS DE UNA CONSULTA
La sentencia **CREATE TABLE** permite crear una tabla a partir de la consulta de otra tabla ya existente. La nueva tabla tendrá los datos obtenidos en la consulta. Crear tablas con datos recuperados de una consulta
*CREATE TABLE empledeptos*
***AS***
*SELECT empleados.Cod_Empl, empleados.Nombre, departamentos.Nombre*
*FROM empleados, departamentos*
*WHERE empleados.Cod_Depto = departamentos.Cod_Depto;*
La consulta puede contener una subconsulta, una combinación de tablas o cualquier consulta SELECT válida.
## CREACIÓN Y USO DE VISTAS. CREATE VIEW
Una **vista** es una tabla lógica que permite acceder a la información de una o de varias tablas. No contiene información por sí misma, su información está basada en la que contienen otras tablas ( tablas base).
<u>Permiten, a partir de una consulta simple, obtener datos de una consulta compleja. Tienen la misma estructura que una tabla: filas y columnas, y se tratan de igual forma que una tabla.</u>
## # Crear una vista. CREATE VIEW
***CREATE** [OR REPLACE] **VIEW** nombrevista*
*[( columna [, columna])*
***AS** consulta;*
Donde:
- AS consulta**: determina las columnas y las tablas que aparecerán en la vista.
- [OR REPLACE]** crea de nuevo la vista si ya existía.
Un ejemplo de creación de una vista sería la que contiene únicamente aquellos empleados que son comerciales.
> *CREATE VIEW comerciales*
>
> *AS SELECT Cod_Empl, Nombre*
>
> *FROM empleados*
>
> *WHERE Cod_Depto=‘007’;*
También podríamos haber creado la vista dando nombre a las columnas, por ejemplo, CNOM, CCOD.
> *CREATE VIEW comerciales ( CCOD, CNOM)*
>
> *AS SELECT Cod_Empl, Nombre*
>
> *FROM empleados*
>
> *WHERE Cod_Depto=‘007’;*
## # Consultar las vistas existentes. USER_VIEWS
Para consultar las vistas creadas se dispone de la vista **USER_VIEWS**. Podemos visualizar los nombres de vistas con sus textos de la manera:
*SELECT VIEW_NAME, TEXT*
*FROM **USER_VIEWS**;*
<u>Si borramos la tabla *empleados,* la vista creada (*comerciales*) seguiría existiendo pero quedaría inutilizada. Por eso, es preferible borrarla.</u>
## # Borrar una vista. DROP VIEW
Para borrar una vista utilizaremos la siguiente sentencia:
> ***DROP VIEW** nombre_vista;*
## # Operaciones sobre vistas
Las operaciones que se pueden realizar sobre vistas son las mismas que las que se llevan a cabo sobre las tablas: SELECT, INSERT, UPDATE y DELETE, aunque se han de tener en cuenta ciertas restricciones.
Las **consultas** siguen la misma sintaxis que sobre tablas:
*SELECT ( col1, col2, …|**)*
*FROM nombrevista*
*WHERE condicion;*
<u>Existen algunas restricciones a considerar en el borrado, actualización y la inserción de filas en una tabla a través de una vista.</u>
Para **borrar** una fila a través de una vista, ésta debe haber sido creada:
- Con filas de una sola tabla
- Sin utilizar GROUP BY ni DISTINCT
- Sin usar funciones de grupo o referencias a pseudocolumnas.
Para la **actualización** de filas a través de una vista: además de las restricciones anteriores, ninguna de las columnas que se va a actualizar se habrá definido como una expresión
En el caso de la **inserción** de filas a través de una vista: además de las restricciones anteriores, todas las columnas obligatorias de la tabla asociada deben estar presentes en la vista.
## # Vistas definidas sobre más de una tabla
Se pueden crear vistas definidas sobre el número de tablas que se deseen. Un ejemplo sería:
*CREATE VIEW empl_deptos*
*( CODEMPL, NOMBRE, NOMDEPTO, FINGRESO)*
*AS*
*SELECT Cod_Depto, empleados.Nombre, departamentos.Nombre, F_Ingr*
*FROM empleados, departamentos*
*WHERE empleados.Cod_Depto = departamentos.Cod_Depto;*
Si intentamos insertar una fila en la vista creada obtenemos error ya que la vista se creó a partir de dos tablas.
*INSERT INTO empl_deptos (‘007’, ’Marga Solano’, ‘RRHH’, ‘27/10/2006’);*
*ORA-01776: no se puede modificar más de una tabla base a través de una vista de unión*
Los borrados y modificaciones también producirán errores.
## # Manejo de expresiones y de funciones en vistas
Se pueden crear vistas usando funciones, expresiones en columnas y consultas avanzadas, pero únicamente se podrán consultar esas vistas. Por ejemplo:
*CREATE VIEW empl ( NOMBRE, DEPTO, FINGRESO)*
*AS*
*SELECT UPPER ( Nombre) ,Cod_Depto, ADD_DAYS ( F_Ingr, 1)*
*FROM empleados;*
Sólo podremos **actualizar** filas siempre y cuando la columna que se va a modificar no sea una columna expresada en forma de cálculo ( edad + 3) o creada mediante una función ( UPPER, ADD_DAYS)
*UPDATE empl SET NOMBRE=‘Luis’*
*WHERE NOMBRE=‘Juan’;*
*UPDATE empl SET FINGRESO=’25/09/06’*
*WHERE NOMBRE=‘Ana’; 🡪 Error ORA-01733: columna virtual no permitida aquí*
En la **inserción** tampoco es posible introducir filas si las columnas de la vista contienen cálculos o funciones.
*INSERT INTO empl VALUES (‘Irene’, ‘001’, ’25/09/06’);*
da el error: ORA-01733: columna virtual no permitida aquí
## SECUENCIAS
Una **SECUENCIA** es un objeto de Base de Datos que sirve para generar enteros únicos. <u>Son muy útiles para generar automáticamente valores para claves primarias</u>.
## # Crear secuencias
<u>Para crear una secuencia en el esquema propio es necesario tener el privilegio</u> **CREATE SEQUENCE**. Se crea una secuencia en cualquier otro esquema con el privilegio CREATE ANY SEQUENCE.
La sentencia de creación de secuencias tiene la siguiente sintaxis:
***CREATE SEQUENCE** nombresecuencia*
*[INCREMENT BY entero]*
*[START WITH entero]*
*[MAXVALUE entero | NOMAXVALUE]*
*[MINVALUE entero | NOMINVALUE]*
*[CYCLE | NOCYCLE];*
- INCREMENT BY entero**: especifica el intervalo de crecimiento de la secuencia. Si se omite, se asume el valor 1. Si es negativo, produce un decremento de la secuencia.
- START WITH entero**: el número con el que comienza la secuencia
- MAXVALUE entero**: el número más alto que generará la secuencia. Debe ser mayor que los valores de START WITH y MINVALUE. Puede sustituirse por NOMAXVALUE ( opción por defecto) que especifica el valor 1027 y -1 para secuencias ascendentes y descendentes respectivamente.
- MINVALUE entero**: el número más bajo que generará la secuencia. Debe ser menor o igual que el valor de START WITH y menor que MAXVALUE. Puede sustituirse por NOMINVALUE ( opción por defecto) que especifica el valor 1 y –1026 para secuencias ascendentes y descendentes respectivamente.
- CYCLE**: La secuencia continua tras alcanzar su valor máximo o mínimo siguiendo por el otro extremo ( según sea ascendente o descendente). Su valor por defecto es NOCYCLE, que hace que la secuencia no generará más valores.
Una vez creada la secuencia, accedemos a ella mediante las pseudocolumnas:
- CURRVAL**: devuelve el valor actual de la secuencia
- NEXTVAL**: devuelve el siguiente valor e incrementa la secuencia.
Para acceder a estos valores tenemos que poner el nombre de la secuencia, un punto y, a continuación, la pseudocolumna. Veámoslo con un ejemplo:
Creamos la vista:
*CREATE TABLE animales*
*( codigo NUMBER ( 2) NOT NULL PRIMARY KEY,*
*nombre VARCHAR2 ( 15) );*
Creamos la secuencia *códigos* comenzando por 1, con incremento de 1 en 1 y con valor máximo 99.
***CREATE SEQUENCE** CODIGOS*
*START WITH 1*
*INCREMENT BY 1*
*MAXVALUE 99;*
Insertamos varias filas en la tabla frutas obteniendo el código de la fruta de la secuencia *codigos*:
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘perro’);*
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘gato’);*
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘tigre’);*
El resultado de esta inserciones serán tres filas, la primera con código 1 y nombre *perro*, la segunda con código 2 y nombre *gato* y la tercera con código 3 y nombre *tigre*.
Para saber el valor actual de la secuencia utilizaremos:
*SELECT CODIGOS.CURRVAL FROM DUAL;*
## # Borrar secuencias
Para eliminar una secuencia se usa la orden **DROP SEQUENCE**:
***DROP SEQUENCE** CODIGOS;*
## FUNCIONES
Las funciones se usan dentro de expresiones y actúan con los valores de las columnas, variables o constantes. Se utilizan en cláusulas SELECT, WHERE, ORDER BY.
Existen cinco tipos de funciones:
- Aritméticas
- De cadenas de caracteres
- De manejo de fechas
- De conversión
- Otras funciones.
## # Funciones aritméticas
Las funciones aritméticas trabajan con datos de tipo numérico NUMBER.
Trabajan con tres clases de números: valores simples, grupos de valores y listas de valores.
Algunas funciones modifican los valores sobre los que actúan; otras dan información sobre los valores.
### # Funciones aritméticas: DE VALORES SIMPLES
Trabajan con un número, una variable o una columna de una tabla. Usaremos para probar estas funciones la tabla **DUAL**, que es una tabla pequeña de trabajo de Oracle creada para probar funciones o para hacer cálculos simples.
**ABS ( n):** devuelve el valor absoluto de n. Es siempre un nº positivo.
*SELECT ABS (-20) “ABSOLUTO” FROM DUAL;*
**CEIL ( n):** obtiene el valor entero inmediatamente superior o igual a n.
*SELECT CEIL ( 20.7) FROM DUAL; 🡪 21*
*SELECT CEIL ( 16) FROM DUAL; 🡪 16*
*SELECT CEIL (-20.2) FROM DUAL; 🡪 -20*
**FLOOR ( n)**: obtiene el valor entero inmediatamente inferior o igual a n.
*SELECT FLOOR ( 20.7) FROM DUAL; 🡪 20*
*SELECT FLOOR ( 16) FROM DUAL; 🡪 16*
*SELECT FLOOR (-20.2) FROM DUAL; 🡪 -21*
**MOD ( m,n):** devuelve el resto resultante de dividir m entre n. m y n pueden ser números reales.
*SELECT MOD ( 11,4), MOD ( 11,0), MOD (-10,3), MOD ( 10.4,4.5) FROM DUAL;*
**NVL ( col, expresión**): se usa para sustituir un valor nulo en la columna por otro valor. Es decir si al hacer una consulta el valor de un campo es NULL, este campo es sustituido por expresión indicada a continuación. La columna y la expresión deben ser del mismo tipo.
*INSERT INTO PARALEER VALUES ( 400, NULL);*
*SELECT cod_libro, NVL ( nombre_libro, ‘Desconocido’) FROM PARALEER;*
**POWER ( m, exponente):** calcula la potencia de un número
> *SELECT POWER ( 3,4) FROM DUAL;*
**ROUND ( numero [,m]):** redondea los números con la cantidad indicada de dígitos de precisión. Devuelve el valor de número redondeado a *m* decimales. Si *m* es negativo, el redondeo se lleva a cabo a la izquierda del punto decimal. Si se omite **m**, devuelve el valor de número con 0 decimales y redondeado.
> *SELECT ROUND ( 1.5631, 1) FROM DUAL;*
**SIGN ( valor):** indica el signo del valor, si valor es menor que 0 devuelve -1 y si valor es mayor que 0 devuelve 1. Si valor es igual a 0 devuelve 0
*SELECT SIGN (-10), SIGN ( 10) FROM DUAL;*
**SQRT ( n):** devuelve la raíz cuadrada de *n*. *n* no puede ser negativo.
*SELECT SQLR ( 25) FROM DUAL;*
**TRUNC ( número [,m]):** trunca los números para que tengan una cierta cantidad de dígitos de precisión. Devuelve el número truncado a *m* decimales; si *m* es negativo trunca por la izquierda del punto decimal. Si se omite *m* devuelve el número con cero decimales
*SELECT TRUNC ( 1.5634,1) FROM DUAL;*
### # Funciones aritméticas: DE GRUPOS DE VALORES
Estas funciones actúan sobre un grupo de filas para obtener un valor.
**AVG ( n):** Calcula el valor medio de “n” ignorando valore negativos.
**COUNT (**| expresion):** Cuenta el número de veces que la expresión evalúa algún dato con valor no nulo. La opción “**” cuenta todas las filas seleccionadas.
**MAX ( expresion**): Calcula el máximo valor de la expresión.
**MIN ( expresion):** Calcula el mínimo valor de la expresión.
**SUM ( expresion):** obtiene la suma de valores de la expresión.
<u>Los valores nulos son ignorados por las funciones de grupos de valores, y los cálculos se realizan sin contar con ellos.</u>
### # Funciones aritméticas: DE LISTAS
Actúan sobre un grupo de columnas dentro de una misma fila: comparan los valores de cada una de las columnas en el interior de una fila para obtener el mayor o el menor valor de la lista.
**GREATEST ( valor1, valor2, …):** obtiene el mayor valor de la lista
**LEAST ( valor1, valor2, …):** obtiene el menor valor de la lista
## # Funciones de cadenas de caracteres
Las funciones de cadenas de caracteres trabajan con datos de tipo CHAR o VARCHAR2. Es posible anidar funciones de cadena y pueden devolver valores carácter o valores numéricos. Entre ella tenemos:
**CHR ( n):** devuelve el carácter cuyo valor en binario ( ASCCI) es equivalente al número “n”.
*SELECT CHR ( 75), CHR ( 65) FROM DUAL;*
**CONCAT ( cad1, cad2):** equivalente al operador || devuelve la cadena cad1 concatenada con cad2.
*SELECT CONCAT (‘Nombre de empleado:’, Nombre)*
*FROM empleados;*
**LOWER ( cad):** devuelve la cadena *cad* con todas sus letras convertidas a minúsculas.
*SELECT LOWER (‘EJEMPLO’) “Minúscula”*
*FROM DUAL;*
**UPPER ( cad):** devuelve la cadena **cad** con todas sus letras convertidas a mayúsculas.
*SELECT UPPER ( Nombre) “Nombre”*
*FROM empleados;*
**INITCAP ( cad):** convierte la primera letra de cada palabra de “cad” a mayúsculas y el resto, a minúsculas.
*SELECT INITCAP (‘SISTEMAS GESTORES DE BASES DE DATOS’) FROM DUAL;*
**LPAD ( cad1, n [,cad2]):** añade caracteres a la izquierda de cad1 hasta que alcance la longitud *n.* Devuelve cad1 con longitud *n* ajustado a la derecha; cad2 es la cadena con la que se rellena por la izquierda ( si se suprime, se asume como carácter de relleno el blanco ‘ ‘).
*SELECT LPAD ( Nombre, 10, ‘.’)*
*FROM empleados;*
**RPAD ( cad1, n [,cad2]):** añade caracteres a la derecha de cad1 hasta que alcance la longitud n. Devuelve cad1 con longitud n ajustado a la izquierda; cad2 es la cadena con la que se rellena por la derecha ( si se suprime, se asume como carácter de relleno el blanco ‘ ‘).
*SELECT LPAD ( Nombre, 10, ‘**’)*
*FROM empleados;*
**LTRIM ( cad [,set]):** suprime el conjunto de caracteres indicado en set a la izquierda de la cadena cad. Devuelve cad con el grupo de caracteres “set” omitido por la izquierda de la cadena. Por defecto, si la cadena contiene blancos por la izquierda y se omite set, se devuelve la cadena sin blancos por la izquierda.
*SELECT LTRIM (‘abaAaBFUNC’, ‘ab’)*
*FROM DUAL;*
Suprime los caracteres ‘a’ y ‘b’ a la izquierda de la cadena hasta encontrar un carácter distinto de ‘a’ y ‘b’.
**RTRIM ( cad [,set]):** suprime el conjunto de caracteres indicado en set a la derecha de la cadena cad. Devuelve cad con el grupo de caracteres “set” omitido por la derecha de la cadena. Por defecto, si la cadena contiene blancos por la derecha y se omite set, se devuelve la cadena sin blancos por la izquierda.
```
SELECT LTRIM (‘hola ’) || LTRIM (‘adios ’)
FROM DUAL;
**REPLACE ( cad, cadena_búsqueda [,cadena_sustitución]):** devuelve cad con cada ocurrencia de “cadena_busqueda” sustituida por “cadena_sustitución”. Si no ponemos nada en cadena_sustitución se sustituye cadena_búsqueda por nada.
*SELECT REPLACE (‘BLANCO Y NEGRO’, ‘O’, ‘A’)*
*FROM DUAL;*
**SUBSTR ( cad, inicio [,n])**: devuelve la subcadena de cad, que abarca desde la posición indicada en “inicio” hasta tantos caracteres como indica “n”. Si se omite n, de vuelve la cadena desde inicio hasta el final. El valor n no puede ser inferior a 1; si es negativo, devuelve la cadena empezando por su final, yendo de derecha a izquierda.
*SELECT (‘ABCDEFG’, 3, 2) FROM DUAL; 🡪 CD*
*SELECT (‘ABCDEFG’, -3, 2) FROM DUAL; 🡪 EF*
*SELECT (‘ABCDEFG’, 4) FROM DUAL; 🡪 DEFG*
**TRANSLATE ( cad1, cad2, cad3)**: devuelve cad1 con los caracteres encontrados en cad2 y sustituidos por los caracteres de cad3. Cualquier carácter que no esté en la cadena cad2 permanece como estaba.
> *SELECT TRANSLATE (‘LOS PILARES DE LA TIERRA’, ‘AEIOU’, ‘aeiou’) FROM DUAL; ( sustituye la A por la a, la E por la e, ….)*
>
> *SELECT TRANSLATE (‘LOS PILARES DE LA TIERRA’, ‘AEIOU’, ‘a’) FROM DUAL; ( sustituye la A por la a, y la E, I, O, U por nada)*
**ASCII ( cad):** devuelve el valor ASCII del primer carácter de cad.
*SELECT ASCII (‘A’) FROM DUAL;*
**LENGTH ( cad):** devuelve el nº de caracteres de cad.
*SELECT Nombre, LENGTH ( Nombre) FROM empleados;*
## # Funciones de manejo de fechas
```
**SYSDATE**: devuelve la fecha del sistema
*SELECT SYSDATE FROM DUAL;*
**ADD_MONTHS ( fecha, n):** devuelve la fecha incrementada en “n” meses o decrementada en “n” meses si n es negativo.
*SELECT F_Ingr, ADD_MONTHS ( F_Ingr, 2)*
*FROM empleados;*
**LAST_DAY ( fecha)**: devuelve la fecha del último día del mes que contiene fecha.
*SELECT F_Ingr, LAST_DAY ( F_Ingr)*
*FROM empleados;*
**MONTHS_BETWEEN ( fecha1, fecha2)**: devuelve la diferencia en meses entre fecha1 y fecha2. Puede ser un número decimal. Para calcular nuestra edad haríamos:
*SELECT MONTHS_BETWEEN ( SYSDATE, ’21/11/70’) / 12*
*FROM DUAL;*
**NEXT_DAY ( fecha, cad):** devuelve la fecha del primer día de la semana indicado por “cad” después de la fecha indicada por “fecha”. El día de la semana ( cad) se indica por su nombre.
*SELECT NEXT_DAY ( SYSDATE, ‘MARTES’)*
> *FROM DUAL; //¿Qué fecha será el próximo Martes?*
## # Funciones de conversión
Son funciones que transforman un tipo de dato en otro.
**TO_CHAR**: transforma un tipo DATE o NUMBER en una cadena de caracteres.
**TO_DATE:** transforma un tipo NUMBER o CHAR en DATE.
**TO_NUMBER:** transforma una cadena de caracteres en NUMBER.
**TO_CHAR ( fecha, ‘formato’)**: convierte una fecha ( de tipo DATE) a tipo VARCHAR2 en el ‘formato’ especificado. El formato es una cadena de caracteres que puede incluir las máscaras de formato definidas a continuación y donde es posible incluir literales definidos por nosotros encerrados entre comillas dobles.
**<u>Máscaras de formato numéricas:</u>**
- cc o scc**: valor del siglo
- yyyy**: año
- yyy, yy, y**: últimos tres, dos o uno dígitos del año
- q**: número del trimestre
- ww**: número de semana del año
- w**: número semana del mes
- mm**: número del mes
- ddd**: número de día del año
- dd**: número de día del mes
- d**: número de día de la semana
- hh o hh12**: hora ( 1-12)
- hh24**: hora ( 1-24)
- mi**: minutos
- ss**: segundos
- ssss**: segundos transcurridos desde medianoche
- j**: Juliano
**<u>Máscaras de formato de caracteres:</u>**
- syear o year**: año en inglés ( nineteen-eighty-two)
- month**: nombre del mes ( enero, ..)
- mon**: abreviatura de tres letras del nombre del mes ( ENE)
- day**: nombre del día de la semana ( LUNES)
- dy**: abreviatura de tres letras del nombre del día ( LUN)
- a.m. o p.m**.: muestra a.m. o p.m. dependiendo del momento del día.
- b.c. o a.d**.: indicador para el año ( antes o después de Cristo)
A continuación veamos un ejemplo. Para obtener la fecha de ingreso de los empleados formateada tal que aparezca el nombre del mes con todas sus letras, el número de día del mes y el año con cuatro dígitos.
*SELECT TO_CHAR ( F_Ingr, ‘month dd yyyy’) “Fecha Ingreso”*
*FROM empleados;*
<u>Observación</u>: si dentro del formato ponemos:
month: produce por ejemplo enero, todo en minúsculas.
Month: produce, p.ej, Enero, la primera en mayúsculas
MONTH: produce ENERO, todo en mayúsculas.
Lo mismo ocurre con day y dy.
Por defecto el formato para la fecha viene definido en función del idioma: dd/mm/yy. Podemos cambiar el valor por omisión para la fecha con el parámetro **NLS_DATE_FORMAT** usando la orden **ALTER SESSION**. Por ejemplo:
***ALTER SESSION** SET NLS_DATE_FORMAT=‘DD/month/YYYY HH24:MI:SS’;*
*SELECT SYSDATE FROM DUAL;*
Podemos cambiar también el lenguaje utilizado para nombrar los meses y los días con el parámetro **NLS_DATE_LANGUAGE** usando la orden **ALTER SESSION**. Por ejemplo:
***ALTER SESSION** SET NLS_DATE_LANGUAGE=French;*
> *SELECT TO_CHAR ( SYSDATE, ‘ “Hoy es “ day “,” dd “ de “ month “ de “ yyyy’) “Fecha ”FROM DUAL;*
**TO_CHAR ( numero, ‘formato’)**: convierte un número de tipo NUMBER a tipo VARCHAR2 en el formato especificado.
**9**: devuelve el valor con el número especificado de dígitos. Si es + deja un espacio, con el signo – si es negativo. Si el valor tiene ceros a la izquierda los deja en blanco excepto si el valor es 0.
*SELECT **TO_CHAR ( 1, ‘999’)**, **TO_CHAR (-1, ‘999’)** FROM DUAL;*
**$**: devuelve el valor con el símbolo $ a la izquierda.
*SELECT **TO_CHAR ( 10, ‘$9999’)** FROM DUAL;*
**S**: devuelve el valor con el signo + si el valor es positivo o con el signo – si el valor es negativo.
*SELECT **TO_CHAR (-55, ‘999S’),** **TO_CHAR (-55,‘S999’)** FROM DUAL;*
**D**: devuelve el carácter decimal en la posición especificada
*SELECT **TO_CHAR ( 34.55, ’99D99’)** FROM DUAL;*
**L**: devuelve el símbolo de la moneda local en la posición indicada
*SELECT **TO_CHAR ( 123, ‘L999’)** FROM DUAL;*
**RN o rn**: devuelve el valor en números romanos en mayúsculas o minúsculas
*SELECT TO_CHAR ( 12, ‘RN’) FROM DUAL;*
Para cambiar el símbolo de la moneda:
*ALTER SESSION SET NLS_CURRENCY=‘euros’;*
**TO_NUMBER ( cadena [,formato]):** convierte la cadena a tipo NUMBER según el formato especificado. La cadena ha de contener números, el carácter decimal o el signo menos a la izquierda. No puede haber espacios entre los números, ni otros caracteres.
*SELECT **TO_NUMBER (‘-123456’),** **TO_NUMBER (‘123,99’, ‘999D99’)** FROM DUAL;*
**TO_DATE ( cad, ‘formato’):** convierte cad de tipo VARCHAR2 o VAR a un valor de tipo DATE. El formato de fecha elegido es “formato”.
*SELECT **TO_DATE (‘010103’)** FROM DUAL;*
*SELECT **TO_CHAR ( TO_DATE (‘01012001’, ‘ddmmyyyy’), ‘Month’)** “Mes” FROM DUAL;*
TO_DATE y TO_CHAR son similares, la deferencia es que TO_DATE convierte una cadena de caracteres en una fecha y TO_CHAR convierte una cadena en una fecha. Ambas pueden utilizar las máscaras de formato de fechas.
## OTRAS FUNCIONES
**USER**: función que devuelve el nombre del usuario actual
**UID**: devuelve el identificador del usuario actual. Al crear un usuario, Oracle le asigna un número que identifica a cada usuario y es único en la Base de datos.
*SELECT USER, UID FROM DUAL;*
En realidad, USER, UID y SYSDATE no son funciones sino pseudocolumnas: devuelven un valor al seleccionarlas pero no son columnas de una tabla.
[^1]: *El nombre de una tabla puede tener de 1 a 30 caracteres de longitud. No puede ser una palabra reservada de Oracle. Su primer carácter debe ser alfabético, el resto pueden ser letras, números y el carácter \_*
[^2]: Dando un nombre a una restricción es más fácil identificar los errores que da Oracle cuando se viola dicha restricción ya que aparece el nombre de la restricción como parte del mensaje de error.
