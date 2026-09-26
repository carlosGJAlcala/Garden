# **Lenguaje de Definición de Datos.**

**Lenguaje de Definición de Datos.**
**Introducción a la Administración de Bases de Datos.**
[1.1 INTRODUCCIÓN 3](#introducción)
[1.2 CREACIÓN DE UNA BASE DE DATOS 3](#creación-de-una-base-de-datos)
[1.2.1 Crear una tabla 3](#crear-una-tabla)
[1.2.2 Restricciones sobre una tabla 5](#restricciones-sobre-una-tabla)
[1.3 CREAR TABLAS CON DATOS RECUPERADOS DE UNA CONSULTA 11](#crear-tablas-con-datos-recuperados-de-una-consulta)
[1.4 CREACIÓN Y USO DE VISTAS. CREATE VIEW 12](#creación-y-uso-de-vistas.-create-view)
[1.4.1 Crear una vista. CREATE VIEW 12](#crear-una-vista.-create-view)
[1.4.2 Consultar las vistas existentes. USER_VIEWS 13](#consultar-las-vistas-existentes.-user_views)
[1.4.3 Borrar una vista. DROP VIEW 13](#borrar-una-vista.-drop-view)
[1.4.4 Operaciones sobre vistas 13](#operaciones-sobre-vistas)
[1.4.5 Vistas definidas sobre más de una tabla 14](#vistas-definidas-sobre-más-de-una-tabla)
[1.4.6 Manejo de expresiones y de funciones en vistas 14](#manejo-de-expresiones-y-de-funciones-en-vistas)
[1.5 SECUENCIAS 15](#secuencias)
[1.5.1 Crear secuencias 15](#crear-secuencias)
[1.5.2 Borrar secuencias 17](#borrar-secuencias)
[1.6 SINÓNIMOS 17](#sinónimos)
[1.6.1 Crear sinónimos 17](#crear-sinónimos)
[1.6.2 Borrar sinónimos 18](#borrar-sinónimos)
[1.7 VISTAS DEL DICCIONARIO DE DATOS 18](#vistas-del-diccionario-de-datos)
[1.8 TRIGGERS 19](#triggers)
[1.8.1 Creación de triggers 19](#creación-de-triggers)
[1.8.2 Sintaxis de creación de triggers 20](#sintaxis-de-creación-de-triggers)
[1.8.3 Referencias NEW y OLD 21](#referencias-new-y-old)
[1.8.4 IF INSERTING, IF UPDATING e IF DELETING 23](#if-inserting-if-updating-e-if-deleting)
[1.8.5 Triggers del tipo INSTEAD OF 23](#triggers-del-tipo-instead-of)
[1.8.6 Triggers del sistema 24](#triggers-del-sistema)
[1.8.7 Eliminar triggers 26](#eliminar-triggers)
[1.8.8 Recompilar triggers 26](#recompilar-triggers)
[1.8.9 Desactivar triggers 27](#desactivar-triggers)
[1.8.10 Activar triggers 27](#activar-triggers)
[1.8.11 Desactivar o activar todos los triggers de una tabla 27](#desactivar-o-activar-todos-los-triggers-de-una-tabla)
[1.9 INTRODUCCIÓN A LA ADMINISTRACIÓN DE BASES DE DATOS 28](#introducción-a-la-administración-de-bases-de-datos)
[1.9.1 Gestión de usuarios 28](#gestión-de-usuarios)
[1.9.2 Privilegios de usuarios 30](#privilegios-de-usuarios)
[1.10 IMPORTANDO Y EXPORTANDO ESQUEMAS 35](#importando-y-exportando-esquemas)
## INTRODUCCIÓN 
Una vez analizado un problema y diseñada la solución informática que lo resuelve a través de los modelos conceptual, lógico y físico, llega el momento de construir una solución. Empieza ahora la **fase de implementación**. A partir de ahora se realiza:
- Programación de las funciones del sistema
- Creación y poblado de la Base de Datos
- Programación de accesos a la Base de Datos
Al final de las etapas de diseño ( y fundamentalmente con la ayuda de alguna herramienta CASE) se obtuvo la estructura de las tablas que conformarán nuestra Base de Datos. Esta estructura deberá ser *incorporada* al sistema, para posteriormente *poblarla* con información y realizar las *consultas* y *actualizaciones* necesarias y propias de la labor empresarial.
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
> *( Cod_Empl CHAR ( 5) NOT NULL,*
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
> *);*
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
> *...);*
>
> *CREATE TABLE empleados (*
>
> *Cod_Empl CHAR ( 5) ,*
>
> *...*
>
> ***CONSTRAINT** CLAVE_P PRIMARY KEY ( Cod_Empl)*
>
> *…);*
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
….. *);*
- <u>Formato de restricción de tabla:</u>**
*CREATE TABLE nom_tabla (*
*col1 TIPO_DE_DATO*
*Col2 TIPO_DE_DATO*
…..
*[CONSTRAINT nombre_restr]*
***FOREIGN KEY** ( col [,[col])*
***REFERENCES** nombretabla [( col)]*
***[ON DELETE CASCADE]|[ON DELETE SET NULL]**);*
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
**<u>Acciones de creación y borrado</u>**
- En el ejemplo, se debe crear primero la tabla CLIENTES y después la tabla VENTAS, ya que VENTAS referencia a CLIENTES. Si lo hacemos al revés, Oracle dará un error.
- Si queremos borrar las tablas, comenzamos borrando la tabla VENTAS y después, la tabla CLIENTE. Si lo hacemos al revés, Oracle dará un mensaje de error.
- Si queremos eliminar algún cliente en la tabla CLIENTES y que las filas correspondientes en la tabla VENTAS con ese *id_cliente* sean eliminadas automáticamente por Oracle, se añadirá la cláusula **ON DELETE CASCADE** en la opción **REFERENCES**:
*FOREIGN KEY ( id_cliente) REFERENCES clientes ( id_cliente)*
***ON DELETE CASCADE***
Se puede dar un nombre a la restricción con la cláusula CONSTRAINT[^2]:
> *CONTRAINT FK_VENTAS FOREIGN KEY ( id_cliente) REFERENCES clientes ( id_cliente) ON DELETE CASCADE*
Se pueden agregar restricciones de clave foránea a una tabla con el uso de la sentencia **ALTER TABLE**.
***ALTER TABLE** nombre_tabla*
*ADD [CONSTRAINT símbolo]*
***FOREIGN KEY**(...) **REFERENCES** otra_tabla (...) [**ON DELETE CASCADE**]*
**<u>Acciones de modificación</u>**
Si queremos modificar el código de algún cliente en la tabla CLIENTES y que las filas correspondientes en la tabla VENTAS con ese *id_cliente* sean modificadas automáticamente por Oracle, se creará un **disparador** que se activará justo después de realizar la modificación. El hecho de utilizar un disparador o trigger es porque Oracle no soporta ON UPDATE CASCADE.
> ***CREATE OR REPLACE TRIGGER** Ventas_UpdateCascade 
> **AFTER UPDATE OF** id_cli 
> **ON** clientes 
> **FOR EACH ROW** 
> **BEGIN***
>
> ***UPDATE ventas SET** id_cli=**:NEW**.id_cli 
> **WHERE** id_cli=**:OLD**.id_cli;*
>
> ***END;***
El disparador se ejecuta como cualquier otro procedimiento de PL/SQL. Se puede modificar el disparador con la opción **compile,** tal como se muestra en la figura.
> *SQL\> sta Compras_Update;*
Si se producen errores en la compilación, pueden mostrarse con el comando SHOW ERRORS
> *SQL\> SHOW ERRORS;*
![]( 2cuatri/SistemasEmpotrados/TrabajoGrupal/_media/Plantilla-Trabajo-GrupoMIo/media/image1.png)
### # La restricción de obligatoriedad NOT NULL
Esta restricción asociada a una columna significa que no puede tener valores nulos, es decir que ha de tener obligatoriamente un valor. En caso contrario, causa una excepción.
*CREATE TABLE persona*
*(*
> *NIF VARCHAR2 ( 10) **NOT NULL**,*
>
> *...*
>
> *EDAD NUMBER ( 2) **CONSTRAINT** Edad_nonula **NOT NULL***
*);*
### # Valores por defecto. DEFAULT
En el momento de crear una tabla podemos asignar valores por defecto a las columnas, es decir, un valor por omisión cuando el valor de la columna no se especifica al insertar una tupla.
En la especificación **DEFAULT** es posible incluir varias expresiones: constantes, funciones SQL y variables UID y SYSDATE.
*CREATE TABLE altaempleado*
*(*
> *NIF VARCHAR2 ( 10) NOT NULL,*
>
> *NOMBRE VARCHAR ( 30) NOT NULL,*
>
> *DIRECCION VARCHAR2 ( 40) **DEFAULT** ‘ ‘,*
>
> *EDAD NUMBER ( 2),*
>
> *FECHA DATE **DEFAULT** SYSDATE*
*);*
Si insertamos una fila en la tabla dando valores a todas las columnas salvo a DIRECCION y FECHA:
*INSERT INTO altaempleado ( DNI, NOMBRE, EDAD) VALUES (´1234´, ´PEPA´, 21);*
Al visualizar el contenido de la tabla, en la columna FECHA se almacenará la fecha del sistema ya que no se dio valor a la columna FECHA *( SELECT ** FROM altaempleados;)*
### # La restricción UNIQUE
<u>Evita valores repetidos en una o más columnas</u>. La diferencia con la restricción PRIMARY KEY es que ésta es única por tabla. En cambio, puede haber varias restricciones **UNIQUE** definidas en una misma tabla. Al igual que en PRIMARY KEY, cuando se define una restricción UNIQUE se crea un índice automáticamente.
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
La restricción **CHECK** nos permite definir los dominios de los campos. La siguiente restricción va a impedir que la columna *sexo* admita un valor distinto a F ( Femenino) o M ( masculino).
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
> *CONSTRAINT pk_mascotas PRIMARY KEY ( nombre)*
>
> *);*
Alternativamente podría haberse creado el CHECK a nivel de tabla:
> *CONSTRAINT check_mascotas CHECK ( sexo=’M’ OR sexo=’F’);*
Algunos ejemplos de uso de CHECK:
> CHECK ( CURSO IN ( 1, 2 ,3))
>
> CHECK ( EDAD BETWEEN 5 AND 20)
>
> CHECK ( NOMBRE=UPPER ( NOMBRE))
>
> CHECK ( A IS NOT NULL) equivale a la restricción NOT NULL.
## CREAR TABLAS CON DATOS RECUPERADOS DE UNA CONSULTA
La sentencia **CREATE TABLE** permite crear una tabla a partir de la consulta de otra tabla ya existente. La nueva tabla tendrá los datos obtenidos en la consulta.
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
> ***CREATE VIEW** **comerciales***
>
> ***AS SELECT** **Cod_Empl, Nombre***
>
> ***FROM** **empleados***
>
> ***WHERE** **Cod_Depto=‘007’;***
También podríamos haber creado la vista dando nombre a las columnas, por ejemplo, CNOM, CCOD.
> ***CREATE VIEW** **comerciales ( CCOD, CNOM)***
>
> ***AS SELECT** **Cod_Empl, Nombre***
>
> ***FROM** **empleados***
>
> ***WHERE** **Cod_Depto=‘007’;***
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
***SELECT** ( col1, col2, …|**)*
***FROM** nombrevista*
***WHERE** condicion;*
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
*SELECT A.Cod_Depto, A.Nombre, B.Nombre, A.F_Ingr*
*FROM empleados A, departamentos B*
*WHERE A.Cod_Depto = B.Cod_Depto;*
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
- CYCLE**: la secuencia continúa tras alcanzar su valor máximo o mínimo siguiendo por el otro extremo ( según sea ascendente o descendente). Su valor por defecto es NOCYCLE, que hace que la secuencia no generará más valores.
Una vez creada la secuencia, accedemos a ella mediante las pseudocolumnas:
- CURRVAL**: devuelve el valor actual de la secuencia
- NEXTVAL**: devuelve el siguiente valor e incrementa la secuencia.
Para acceder a estos valores tenemos que poner el nombre de la secuencia, un punto y, a continuación, la pseudocolumna. Veámoslo con un ejemplo:
Creamos la vista:
*CREATE TABLE animales*
*( codigo NUMBER ( 2) PRIMARY KEY,*
*nombre VARCHAR2 ( 15) );*
Creamos la secuencia *códigos* comenzando por 1, con incremento de 1 en 1 y con valor máximo 99.
***CREATE SEQUENCE** CODIGOS*
*START WITH 1*
*INCREMENT BY 1*
*MAXVALUE 99;*
Insertamos varias filas en la tabla animales obteniendo el código del animal de la secuencia *CODIGOS*:
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘león’);*
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘ciervo’);*
*INSERT INTO animales VALUES ( CODIGOS.NEXTVAL, ‘tigre’);*
El resultado de esta inserciones serán tres filas, la primera con código 1 y nombre *león*, la segunda con código 2 y nombre *ciervo* y la tercera con código 3 y nombre *tigre*.
Para saber el valor actual de la secuencia utilizaremos:
***SELECT CODIGOS.CURRVAL** FROM DUAL;*
## # Borrar secuencias
Para eliminar una secuencia se usa la orden **DROP SEQUENCE**:
***DROP SEQUENCE** CODIGOS;*
## SINÓNIMOS
Para acceder a las tablas de otro usuario es preciso anteponer a dichas tablas el nombre del usuario propietario de las mismas.
Si el usuario MIM1 quisiera consultar la tabla JOBS del usuario HR, introduciría:
***SELECT ** FROM HR.JOBS**;*
Obteniendo el resultado esperado siempre y cuando a MIM1 se le hubiera concedido el permiso de consulta a la tabla JOBS.
Mediante el uso de **SINÓNIMOS** se pueden utilizar dos o más nombres diferentes ( alias) para referirse al mismo objeto. Son especialmente útiles para acceder a vistas del usuario administrador por parte de los usuarios convencionales, dado que crean *transparencia de localización*.
## # Crear sinónimos
<u>Para crear un sinónimo en el esquema propio es necesario tener el privilegio</u> **CREATE SYNONYM**.
La sentencia de creación de secuencias tiene la siguiente sintaxis:
***CREATE [PUBLIC] SYNONYM** nomsinónimo **FOR** [usuario.]nombretabla;*
Donde PUBLIC permite que el sinónimo esté disponible para todos los usuarios.
SQL\> CREATE SYNONYM EMPLEOS FOR HR.JOBS;
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image2.png)
## # Borrar sinónimos
Para eliminar una sinónimo se usa la orden **DROP [PUBLIC] SYNONYM [usuario.]sinónimo**:
***DROP SYNONYM** EMPLEOS;*
## VISTAS DEL DICCIONARIO DE DATOS
- Información de tablas y otros objetos: USER_TABLES, USER_OBJECTS, USER_CATALOG
- Información de restricciones: USER_CONSTRAINTS, ALL_CONSTRAINTS, DBA_CONSTRAINTS, USER_CONS_COLUMNS, ALL_CONS_COLUMS, DBA_CONS_COLUMNS
- Información sobre vistas: USER_VIEWS, ALL_VIEWS
- Información sobre sinónimos: USER_SYNONYMS, ALL_SYNONYMS
## TRIGGERS 
Se llama **trigger** ( o **disparador)** al código que se ejecuta automáticamente cuando es procesada una determinada operación DML ( insert, delete, update, etc.) sobre una tabla o vista y también cuando ocurre algún evento del sistema ( arranque/parada de la base de datos, entrada/salida de un usuario, etc.). El código que se ejecuta es independiente de la aplicación que realizó dicha operación.
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
## # Creación de triggers
**<u>Elementos de los triggers</u>**
Puesto que un trigger es un código que se dispara, al crearle se deben indicar los siguientes elementos:
- El evento que da lugar a la ejecución del trigger (**INSERT**, **UPDATE** o **DELETE**) .
- Cuando se lanza el evento en relación a dicho evento (**BEFORE** ( antes), **AFTER** ( después) o **INSTEAD OF** ( en lugar de)) .
- Las veces que el trigger se ejecuta ( tipo de trigger: de instrucción o de fila).
- El cuerpo del trigger, es decir el código que ejecuta dicho trigger .
**<u>Cuándo ejecutar el trigger</u>**
En el apartado anterior se han indicado los posibles tiempos para que el trigger se ejecute. Éstos pueden ser:
- BEFORE**. El código del trigger se ejecuta antes de ejecutar la instrucción DML que causó el lanzamiento del trigger.
- AFTER**. El código del trigger se ejecuta después de haber ejecutado la instrucción DML que causó el lanzamiento del trigger.
- INSTEAD OF**. El trigger sustituye a la operación DML Se utiliza para vistas que no se pueden modificar.
**<u>Tipos de trigger</u>**
Hay dos tipos de trigger:
- De instrucción**. <u>El cuerpo del trigger se ejecuta una sola vez por cada evento que lance el trigge</u>r. *Esta es la opción por defecto*. El código se ejecuta aunque la instrucción DML no genere resultados.
- De fila**. <u>El código se ejecuta una vez por cada fila afectada por el evento</u>. Por ejemplo si hay una cláusula UPDATE que desencadena un trigger y dicho UPDATE actualiza 10 filas; si el trigger es de fila se ejecuta una vez por cada fila, si es de instrucción se ejecuta sólo una vez ( por instrucción).
## # Sintaxis de creación de triggers
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
- ------------: --------------------------------------------------------------------: --------------------------------------------------------------------------------------------------
- *FOR EACH STATEMENT***: ***FOR EACH ROW***
- BEFORE**: **Se ejecuta la regla una vez antes de la ejecución del evento**: **Se ejecuta la regla una vez antes de la actualización de cada tupla afectada por el evento**
- AFTER**: **Se ejecuta la regla una vez después de la ejecución del evento**: **Se ejecuta la regla una vez después de la actualización de cada tupla afectada por el evento**
<u>Ejemplo:</u>
***CREATE OR REPLACE TRIGGER** **tr_insdatos_enviaenergia***
Error: valor entre –20000
y -20999
***BEFORE INSERT ON enviaenergia***
***BEGIN***
***IF ( TO_CHAR ( SYSDATE, ‘HH24’) NOT IN (‘10’, ‘11’) THEN***
***RAISE_APPLICATION_ERROR (-20001,***
*‘Sólo se puede enviar energía entre las 10 y las 11:59’);*
***END IF;***
***END;***
***/***
Este trigger impide que se puedan añadir registros a la tabla ENVIAENERGIA entre las 10 y las 12 horas.
## # Referencias NEW y OLD
Cuando se ejecutan instrucciones UPDATE, hay que tener en cuenta que se modifican valores antiguos (**OLD**) para cambiarles por valores nuevos (**NEW**). Las palabras NEW y OLD permiten acceder a los valores nuevos y antiguos respectivamente.
El apartado REFERENCING de la creación de triggers, permite asignar nombres a las palabras NEW y OLD ( en la práctica no se suele utilizar esta posibilidad). Así *new.nombre* haría referencia al nuevo nombre que se asigna a una determinada tabla y *old.nombre* al viejo.
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
Como queremos que la tabla se actualice automáticamente, creamos el siguiente trigger. Lo escribimos en un archivo de texto con extensión *.sql* para poder ser ejecutado desde el entorno SQL:
> ***CREATE OR REPLACE TRIGGER** **tr_crear_audit_productor***
>
> ***BEFORE UPDATE OF** **prodMax** **ON** **productor ***
>
> ***FOR EACH ROW***
>
> ***BEGIN***
>
> ***IF (:new.prodmax \<\> :old.prodmax) THEN***
>
> ***INSERT INTO** **productor_audit***
>
> ***VALUES (:old.nombre, :old.prodmax, :new.prodmax, sysdate);***
***END IF;***
> ***END;***
>
> */*
Lo ejecutamos y realizamos un cambio en la tabla PRODUCTOR
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image3.png)
Con este trigger cada vez que se modifique una fila de la tabla PRODUCTOR que afecte a la producción máxima, se añadirá una nueva fila en la tabla PRODUCTOR_AUDIT.
## # IF INSERTING, IF UPDATING e IF DELETING
Son palabras que se utilizan para determinar la instrucción que se estaba realizando cuando se lanzó el trigger. Esto se utiliza en triggers que se lanzan para varias operaciones ( utilizando INSERT OR UPDATE por ejemplo). En ese caso se pueden utilizar sentencias IF seguidas de INSERTING, UPDATING o DELETING; estas palabras devolverán TRUE si se estaba realizando dicha operación.
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
> ***ELSE - -estará actualizando, UPDATING***
>
> ***. . .***
>
> ***ENDIF***
***END;***
## # Triggers del tipo INSTEAD OF
Hay un tipo de trigger especial que se llama INSTEAD OF y que sólo se utiliza con las vistas. Una vista es una consulta SELECT almacenada. En general sólo sirven para mostrar datos, pero podrían ser interesantes para actualizar. Por ejemplo, si partimos de las siguientes tablas y vista correspondiente:
> PIEZAS (<u>tipo</u>, <u>modelo</u>, precio_venta)
>
> EXISTENCIAS (<u>tipo</u>, <u>modelo</u>, n\_<u>almacen</u>, cantidad)
>
> EXISTENCIASCOMPLETA ( tipo, modelo, precio, almacen, cantidad);
>
> ***CREATE VIEW** **existenciasCompleta ( tipo, modelo, precio, almacen, cantidad)***
***AS***
***SELECT p.tipo, p.modelo, p.precio_venta,***
***e.n_almacen, e.cantidad***
***FROM PIEZAS p, EXISTENCIAS e***
***WHERE p.tipo = e.tipo AND p.modelo = e.modelo***
***ORDER BY p.tipo, p.modelo, e.n_almacen;***
Esta instrucción daría lugar a error
*INSERT INTO existenciasCompleta VALUES (‘X01’, ‘007’, 53.75, 4, 21);*
Indicando que esa operación no es válida en esa vista ( al utilizar dos tablas). Esta situación la puede arreglar un trigger que inserte primero en la tabla de piezas ( sólo si no se encuentra ya insertada esa pieza) y luego inserte en existencias.
Eso lo realiza el trigger de tipo INSTEAD OF, que sustituirá el INSERT original por el indicado por el trigger:
> ***CREATE OR REPLACE TRIGGER tr_insert_piezasexistencias***
***INSTEAD OF INSERT***
***ON existenciasCompleta***
***BEGIN***
***INSERT INTO PIEZAS ( tipo, modelo, precio_venta)***
***VALUES (:new.tipo, :new.modelo, :new.precio);***
***INSERT INTO EXISTENCIAS ( tipo, modelo, n_almacen, cantidad)***
***VALUES (:new.tipo, :new.modelo, :new.almacen, :new.cantidad);***
> ***END;***
>
> ***/***
Este trigger permite añadir a esa vista añadiendo los campos necesarios en las tablas relacionadas en la vista. Se podría modificar el trigger para permitir actualizar, eliminar o borrar datos directamente desde la vista y así desde cualquier acceso a la base de datos se utilizaría esa vista como si fuera una tabla más.
## # Triggers del sistema
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
- ------------: -----------------: -----------------------------------------------------------
- EVENTO**: **MOMENTO**: **SE DISPARAN:**
- STARTUP: AFTER: Después de iniciar la instancia de la Base de Datos
- SHUTDOWN: BEFORE: Antes de parar la instancia de la Base de Datos
- LOGON: AFTER: Después de conectarse a la Base de Datos
- LOGOFF: BEFORE: Antes de que un usuario se desconecte de la Base de Datos
- CREATE: BEFORE \: AFTER: Antes o después de crear un objeto en el esquema
- DROP: BEFORE \: AFTER: Antes o después de eliminar un objeto en el esquema
- ALTER: BEFORE \: AFTER: Antes o después de modificar un objeto en el esquema
- GRANT: BEFORE \: AFTER: Antes o después de conceder un permiso
- REVOKE: BEFORE \: AFTER: Antes o después de revocar un permiso
**<u>Ejemplo:</u>**
Vamos a auditar los accesos a la base de datos, así como todos los eventos generados por instrucciones DDL. Para ello, primeramente creamos una tabla denominada CTRL_ACCESOS en un usuario con privilegios de administrador.
> CREATE TABLE ctrl_accesos (
>
> usuario VARCHAR2 ( 20),
>
> instante TIMESTAMP,
>
> evento VARCHAR2 ( 20)
>
> );
Posteriormente creamos el disparador:
> ***CREATE OR REPLACE TRIGGER*** ***tr_Control_Accesos***
>
> ***AFTER DDL OR LOGON ON DATABASE***
>
> ***BEGIN***
>
> ***INSERT INTO*** ***ctrl_accesos ( usuario, instante, evento)***
>
> ***VALUES*** ***( USER, SYSTIMESTAMP, ORA_SYSEVENT || '**' || ORA_DICT_OBJ_NAME);***
>
> ***END;***
>
> ***/***
Realizamos diversos accesos con diferentes usuarios y generamos diversas instrucciones DDL.
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image4.png)
## # Eliminar triggers
***DROP TRIGGER** nombretrigger;*
## # Recompilar triggers
***ALTER TRIGGER** nombretrigger **COMPILE**;*
## # Desactivar triggers
***ALTER TRIGGER** nombretrigger **DISABLE**;*
## # Activar triggers
***ALTER TRIGGER** nombretrigger **ENABLE**;*
## # Desactivar o activar todos los triggers de una tabla 
Eso permite en una sola instrucción operar con todos los triggers relacionados con una determinada tabla ( es decir actúa sobre los triggers que tienen dicha tabla en el apartado ON del trigger).
***ALTER TABLE** nombretabla { **DISABLE** | **ENABLE} ALL TRIGGERS**;*
## INTRODUCCIÓN A LA ADMINISTRACIÓN DE BASES DE DATOS
Conforme van creciendo las aplicaciones de los sistemas de información de la empresa, se van necesitando más y más datos, por lo que al mismo tiempo crecen las aplicaciones y objetos de bases de datos. Así pues, la administración de éstas se vuelve cada vez más y más complicada. Ello nos lleva a crear la **función de administración de la base de datos**. El responsable de dicha función es el **administrador de la base de datos ( DBA).**
Si bien no existe un estándar de funciones del DBA, se acostumbra a definirla según el <u>ciclo de vida de la base de datos</u>: planificación, toma de requerimientos y diseño conceptual, diseño lógico, diseño físico y creación, pruebas y mantenimiento de la base datos.
Estas funciones se concretan en una serie de procedimientos de trabajo del DBA:
- Recolección de requisitos del usuario*
- Diseño y modelado de la Base de Datos*: diagramas E/R, normalización, herramientas CASE, metodología orientada a objetos, etc.
- Selección del software de Base de Datos*: elegir el Sistema Gestor de Bases de Datos más adecuado a la empresa.
- Seguridad e integridad de la Base de Datos*: establecimiento de técnicas para aumentar la seguridad e integridad de los datos, tales como definir usuarios, grupos de usuarios, roles, contraseñas, privilegios de acceso, creación de vistas, control y seguimiento de accesos, etc.
- Respaldo y recuperación de la Base de Datos*: recuperación de la información en caso de pérdida física o pérdida de integridad de los datos. Utilización de utilidades de carga, descarga, importación y exportación de datos.
- Control de concurrencia de múltiples usuarios a un mismo recurso*.
- Manejo de herramientas de administración de la Base de Datos*: control de objetos y diccionario de datos.
## # Gestión de usuarios
Un **usuario** es un nombre definido en la base de datos con posibilidad de conectarse a ella y acceder a determinados recursos de la misma según ciertas restricciones definidas por el usuario administrador.
Asociado a cada usuario de la base de datos se encuentra el objeto **esquema** que tiene el mismo nombre que el usuario. <u>El esquema es una colección de objetos ( tablas, secuencias, procedimientos, funciones, disparadores, índices, etc.) a los que tiene derecho dicho usuario</u>. Para acceder a los objetos de otro esquema se necesita el correspondiente permiso.
En el caso concreto de la instalación de la Base de Datos Oracle, se crearon dos usuarios con privilegios de administrador: **SYS** y **SYSTEM.**
El usuario SYS es el propietario de las tablas del diccionario de datos, donde se almacena información sobre el resto de estructuras de la base de datos. Ningún otro usuario puede modificar estas tablas.
El usuario SYSTEM se utiliza para realizar tareas de administrador, tales como crear otros usuarios.
**<u>Creación de usuarios</u>**
La orden para crear usuarios es la siguiente:
***CREATE** **USER** nombre_usuario **IDENTIFIED BY** clave*
*[DEFAULT TABLESPACE nombre_espacio_tabla ]*
*[TEMPORARY TABLESPACE nombre_espacio_tabla ]*
*[QUOTA {entero {K | M } | UNLIMITED } ON nombre_espacio_tabla ]*
*[ PROFILE nombre_perfil ];*
donde:
- DEFAULT TABLESPACE asigna al usuario un tablespace para almacenar los objetos que cree. Si no se especifica, el tablespace por defecto será USERS.
- TEMPORARY TABLESPACE asigna al usuario un tablespace para almacenar trabajos temporales. Si no se especifica, el tablespace por defecto será TEMP.
- QUOTA asigna un determinado espacio en megabytes o kilobytes en el tablespace asignado.
- PROFILE asigna un perfil al usuario. Si no se especifica ninguno, Oracle asigna uno ppor defecto.
*<u>Ejemplos:</u>*
Prompt Se crea el usuario *usu01* con clave de acceso *mim1*
***CREATE USER** **usu01** **IDENTIFIED BY mim1;***
Prompt Se crea el usuario *usu02* con clave de acceso *mim2* y se le asocia un tablespace por
Prompt defecto denominado maste*r* y otro temporal denominado *aula3*. Puede almacenar hasta
Prompt 2Mb en *master* y 750Kb en a*ula3*
***CREATE USER** **usu02** **IDENTIFIED BY mim2 DEFAULT TABLESPACE master ***
***TEMPORARY TABLESPACE aula3 QUOTA 2M ON master QUOTA 750K ON aula3;***
Para ver información sobre los usuarios se utilizan las vistas del sistema:
- USER_USERS**: información del usuario conectado.
- ALL_USERS**: información de todos los usuarios creados en la base de datos.
**<u>Modificación de usuarios</u>**
La orden para modificar usuarios es la siguiente:
***ALTER** **USER** nombre_usuario **IDENTIFIED BY** clave*
*[DEFAULT TABLESPACE nombre_espacio_tabla ]*
*[TEMPORARY TABLESPACE nombre_espacio_tabla ]*
*[QUOTA {entero {K | M } | UNLIMITED } ON nombre_espacio_tabla ]*
*[ PROFILE nombre_perfil ];*
**<u>Borrado de usuarios</u>**
***DROP USER** nombre_usuario [CASCADE];*
La opción CASCADE elimina todos los objetos del usuario antes de borrar el usuario.
## # Privilegios de usuarios
Ningún usuario puede realizar una operación si previamente no se le ha concedido el **privilegio** de hacerlo. Un **rol** o función es un conjunto de privilegios. A un rol se le pueden asignar privilegios y a un usuario roles y privilegios. Existen tres roles creados por defecto por el sistema:
| | |
- ----------: -----------------------------------------------------------------
- ROL**: **PRIVILEGIOS**
- CONNECT: ALTER SESSION, CREATE SESSION, CREATE TABLE, CREATE SEQUENCE, …
- RESOURCE: CREATE PROCEDURE, CREATE TABLE, CREATE TRIGGER, CREATE TYPE, …
- DBA: Posee todos los privilegios del sistema.
Se pueden conceder privilegios sobre los objetos ( DELETE, UPDATE, INSERT, etc.) o sobre el sistema ( CREATE SESION, CREATE TABLE, CREATE USER, GRANT, etc.).
**<u>Concesión de privilegios</u>**
La sintaxis general para crear un privilegio de sistema es:
***GRANT** { lista de privilegios }*
***TO** { lista usuarios o roles | PUBLIC }*
*[ WITH ADMIN OPTION ] ;*
donde:
- WITH ADMIN OPTION permite que el receptor del privilegio o rol pueda conceder esos mismos privilegios a otros usuarios o roles.
La sintaxis general para crear un privilegio de objeto es:
***GRANT** { lista de privilegios | ALL PRIVILEGES }*
***ON** {[usuario.]objeto*
***TO** { lista usuarios o roles | PUBLIC }*
*[ WITH GRANT OPTION ] ;*
**<u>Retirada de privilegios</u>**
La sintaxis general para crear un privilegio de sistema es:
***REVOKE** { lista de privilegios sistema | rol }*
***FROM** { lista usuarios o roles | PUBLIC } ;*
La sintaxis general para crear un privilegio de objeto es:
***REVOKE** { lista de privilegios objeto | ALL PRIVILEGES }*
***ON** {[usuario.]objeto }*
***FROM** { lista usuarios o roles | PUBLIC } ;*
*<u>Ejemplos:</u>*
***GRANT CREATE SESSION TO usu01;***
***GRANT CONNECT TO usu02;***
***GRANT CREATE USER TO usu03 WITH ADMIN OPTION;***
***GRANT SELECT ON compania TO PUBLIC;*** -- concede permiso de consulta sobre la tabla compania a todos los usuarios de la BD
***REVOKE CREATE USER TO usu03;***
***REVOKE SELECT ON compania TO PUBLIC;***
Después de crear un usuario, hay que concederle a éste, como mínimo, el privilegio *CREATE SESSION* para poder acceder a la base de datos.
En el ejemplo siguiente se crea el usuario *usu05*. Un intento de conexión con este usuario resulta fallido. Después de concederle el rol CONNECT ( GRANT CONNECT TO usu05) que contiene, entre otros, el privilegio CREATE SESSION ya sí que puede conectarse a la base de datos.
Se pueden consultar los privilegios que tiene el usuario conectado accediendo a la vista **SESSION_PRIVS**.
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image5.png)
Podemos comprobar en la figura anterior que después de conceder el rol CONNECT al usuario usu05, éste tiene únicamente el privilegio CREATE SESSION.
Si ahora le concedemos el rol RESOURCE, veremos que le dotamos con muchos más privilegios.
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image6.png)
>
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image7.png)
>
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image8.png)
Se pueden consultar los privilegios cedidos y recibidos por un usuario, así como los roles concedidos a través de las vistas **USER_TAB_PRIVS_MADE, USER_TAB_PRIVS_RECD** y **SESSION_ROLES.**
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image9.png)
>
> ![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image11.png)
## IMPORTANDO Y EXPORTANDO ESQUEMAS
En Oracle se puede *exportar* e *importar* un esquema completo de la Base de Datos a través de la utilidad **Data Pump Export**. <u>El esquema es volcado en un formato interno de Oracle a un archivo de disco del Sistema Operativo</u>.
Puesto que el archivo volcado es escrito por el Sistema Gestor de Bases de Datos, es necesario crear previamente un *directorio virtual* en el SGBD que apunta físicamente al directorio real del Sistema Operativo.
**<u>Ejemplo:</u>** Vamos a exportar por completo un esquema de base de datos denominado *endesa.* Posteriormente importaremos el volcado a un usuario inexistente de otra base de datos denominado, por ejemplo, *volcendesa.*
Primeramente creamos el directorio virtual en la BD y proporcionamos permiso de escritura y lectura al usuario propietario del esquema, esto es, *endesa*. Esto se hace desde el usuario SYSTEM. Evidentemente, el directorio físico debe existir, en nuestro caso C:\MIM\Electricidad
SQL\> CREATE OR REPLACE DIRECTORY dmpdir AS ‘C:\MIM\Electricidad’;
SQL\> GRANT READ, WRITE ON DIRECTORY dmpdir TO endesa;
Seguidamente, desde el prompt del sistema operativo, introducimos el siguiente comando:
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image12.png)
C:\expdp SYSTEM/password SCHEMAS=endesa DIRECTORY=dmpdir DUMPFILE=schema.dmp
El volcado del esquema queda almacenado dentro del directorio *C:\MIM\Electricidad* en el archivo SCHEMA.DMP.
Para importar en otra base de datos el volcado anterior se introduce el siguiente comando:
C:\\impdp SYSTEM/password SCHEMAS=endesa DIRECTORY=dmpdir DUMPFILE=schema.dmp REMAP_SCHEMA=endesa:volcendesa LOGFILE=impschema.log
![]( 2cuatri/Sistemas en tiempo Real/_media/Resumen STR/media/image13.png)
El comando anterior ha creado el usuario *volcendesa*. Pero este usuario no tiene el permiso de acceso a la base de datos, por lo que hay que dárselo.
SQL\> GRANT CONNECT TO volcendesa;
Si por ejemplo no se quisiera importar el esquema con restricciones de bases de datos, índices, etc., se introduciría el siguiente comando:
C:\\impdp SYSTEM/password SCHEMAS=endesa DIRECTORY=dmpdir DUMPFILE=schema.dmp REMAP_SCHEMA=endesa:volcendesa EXCLUDE=constraint, ref_constraint, index LOGFILE=impschema.log
[^1]: *El nombre de una tabla puede tener de 1 a 30 caracteres de longitud. No puede ser una palabra reservada de Oracle. Su primer carácter debe ser alfabético, el resto pueden ser letras, números y el carácter \_*
[^2]: Dando un nombre a una restricción es más fácil identificar los errores que da Oracle cuando se viola dicha restricción ya que aparece el nombre de la restricción como parte del mensaje de error.
