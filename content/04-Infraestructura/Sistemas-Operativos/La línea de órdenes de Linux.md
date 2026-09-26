---
title: "La línea de órdenes de Linux"
---

# La línea de órdenes de Linux

*Departamento de Automática*

## Resumen

- El intérprete de órdenes
  - Cómo obtener ayuda
- El sistema de ficheros
  - Navegar por el sistema de ficheros
  - Manipular ficheros y directorios
  - Permisos de acceso
- Trabajar con órdenes
  - Control de trabajos
- Entrada/salida
  - Redirecciones
  - Tuberías
- Ejercicios propuestos

## El intérprete de órdenes

### Visión general

- Es un programa que permite al usuario lanzar órdenes para que
  las ejecute el sistema operativo
- Ejemplos de órdenes:
  - date: muestra o establece la fecha y la hora del sistema
  - cal: muestra un calendario
  - df: muestra el espacio ocupado en el sistema de ficheros
  - exit: termina el intérprete de órdenes
- Guarda un historial de las órdenes ejecutadas
- Permite autocompletar órdenes (TAB)

Usaremos bash como intérprete de órdenes.
Con la orden df, el usuario puede añadir la opción -h para mostrar los valores en un
formato «legible para humanos».

El historial de órdenes ofrece al usuario algunas funcionalidades interesantes:

- La orden history muestra la lista completa de órdenes en tuplas
  (número de evento, orden)
- Pulsando la flecha arriba podemos recorrer las últimas órdenes anteriores
- Pulsando Ctrl+R podemos buscar dentro del historial de órdenes
- Escribiendo el carácter «!» delante de uno o más caracteres, por ejemplo !cal, podemos
  repetir la última orden lanzada que empezaba por esos caracteres.

Pulsando la tecla TAB podemos completar las órdenes.

### Cómo obtener ayuda

- La herramienta man proporciona ayuda sobre los distintos elementos del sistema:

```bash
man df
man man
```

- Las páginas de man (manual) se dividen en distintas secciones:
  - 1 : Órdenes generales
  - 2 : Llamadas al sistema
  - 3 : Funciones de la biblioteca de C

El usuario puede buscar dentro de las páginas de man introduciendo el carácter / seguido de la
cadena que quiere buscar.

Se puede buscar una orden a partir de su descripción:

```bash
man -k text_to_lookup
```

Puede ocurrir que una misma entrada de man esté presente en más de una sección,
por ejemplo read, write… En ese caso es necesario indicar la sección concreta en la que
buscar:

```bash
man 3 write
```

## El sistema de ficheros

### El árbol de directorios

*(diagrama del árbol de directorios de Unix/Linux: `/` como raíz, con
`boot`, `etc`, `bin`, `usr` (que contiene a su vez `bin` y `local`),
`home`, `root`, `dev`, `proc` y `mnt` como directorios de primer nivel)*

- La orden pwd muestra el directorio de trabajo actual
- La orden ls muestra el contenido del directorio de trabajo
  actual

En Unix/Linux, los ficheros se organizan en lo que llamamos directorios. Un directorio no es
más que un fichero especial que contiene información que permite localizar otros ficheros.
A su vez, los directorios pueden contener otros directorios, que se denominan subdirectorios.

La jerarquía de directorios de Unix estandariza una serie de directorios con sus funciones
asociadas:

- /boot: contiene el núcleo de Linux y los ficheros de arranque del sistema
- /etc: contiene los ficheros de configuración del sistema
- /bin y /usr/bin: contienen la mayoría de los programas del sistema. El directorio /bin
  guarda los programas esenciales, mientras que /usr/bin contiene las aplicaciones de usuario.
- /usr/local: se usa para instalar programas que se van a utilizar localmente en la máquina. En
  principio, estos programas no forman parte de la distribución de Linux, sino que se instalan
  a criterio del usuario.
- /home: contiene los directorios personales de los usuarios. Cada usuario registrado tiene
  su propio directorio dentro de /home
- /root: es el directorio personal del usuario root (superusuario)
- /dev: directorio cuyos ficheros representan los dispositivos instalados en el sistema. En los
  sistemas Unix/Linux, los ficheros se usan como abstracciones de los dispositivos. Así, cuando
  leemos o escribimos en uno de estos ficheros, en realidad estamos leyendo y escribiendo datos
  del dispositivo correspondiente.
- /proc: es un directorio virtual cuyos ficheros permiten obtener información sobre el
  sistema, el funcionamiento del sistema operativo y los procesos que se están
  ejecutando en ese momento.
- /mnt: en algunos sistemas, como Ubuntu, también se usa otro directorio llamado /media.
  Normalmente este directorio se utiliza como «punto de montaje» para sistemas de ficheros
  distintos del principal. Por ejemplo, al insertar una memoria USB, el sistema
  «monta» los ficheros de la memoria colgando de este directorio.

Otros directorios:

- /var: contiene ficheros que se modifican durante la ejecución del sistema, como los ficheros
  de registro (logs).
- /tmp: directorio que usan los programas para guardar ficheros temporales. Se borra con
  cada reinicio del sistema.

El directorio de conexión (~), también llamado directorio personal (home), es el directorio en el que
empieza un usuario al iniciar sesión en Unix/Linux. Cada usuario tiene su propio directorio de conexión.
Normalmente el directorio de conexión se encuentra en /home/user, donde user es el nombre del
usuario.

### Navegar por el sistema de ficheros

#### Cambiar el directorio de trabajo actual

- La orden cd permite cambiar el directorio de trabajo actual
- Se pueden usar rutas absolutas y relativas para referirse al
  directorio de destino

Ejemplo de ruta absoluta:

```bash
cd /usr/local/bin
```

- Toma como origen el directorio raíz /
- No depende del directorio de trabajo actual

Ejemplo de ruta relativa:

*(diagrama del árbol relativo: `/` → `usr` → `local` (origen) y `usr` →
`share` (destino), navegando con `..`; el comando exacto de este
ejemplo no se pudo reconstruir con fiabilidad de la extracción — el
fragmento que sobrevivió es `$ cd bin`)*

- Toma como origen el directorio de trabajo actual
- El directorio especial .. se usa para moverse por el árbol de ficheros

Cada directorio tiene dos subdirectorios especiales:

- El directorio punto (.), que es una referencia al directorio de trabajo actual.
- El directorio punto punto (..), que es una referencia al directorio padre del
  directorio de trabajo actual.

#### Listar ficheros con ls

- La orden ls ofrece distintas opciones de visualización:
  - -a: muestra los ficheros ocultos
  - -l: muestra una vista detallada de los ficheros
- Ejemplo de vista detallada:

```bash
drwxr-xr-x 2 root root 4096 ago 12 08:42 subversion
drwxrwxr-x 6 parraman parraman 4096 mar 29 2017 local
-rw-rw-r-- 1 parraman parraman 462 nov 30 12:52 instr.txt
```

| Campo | Significado |
| --- | --- |
| `drwxr-xr-x` | Permisos del fichero |
| `2` | Número de enlaces |
| `root` | Propietario |
| `root` | Grupo |
| `4096` | Tamaño |
| `ago 12 08:42` | Última modificación |
| `subversion` | Nombre del fichero |

El primer carácter del bloque «Permisos del fichero» indica el tipo de fichero:

- d: directorio
- -: fichero regular
- c: dispositivo de caracteres (por ejemplo, el teclado)
- b: dispositivo de bloques (por ejemplo, el disco duro)

Los permisos de los ficheros en general se tratan más adelante, en otra diapositiva.

### Manipular ficheros y directorios

#### Inspeccionar ficheros

- La orden file muestra el tipo de un fichero
  - Determina el tipo del fichero a partir de su «número mágico»
- El sistema proporciona distintas órdenes para inspeccionar el contenido
  de los ficheros de «texto»:
  - cat: muestra el contenido completo de un fichero
  - more: muestra el contenido de un fichero paginado
  - less: versión mejorada de more que permite recorrer el
    contenido de un fichero hacia delante y hacia atrás, y línea a línea

El número mágico de un fichero son unos bytes concretos que se guardan dentro del fichero en
posiciones fijas (normalmente al principio) y que sirven para determinar su tipo.

Ejemplos de números mágicos:

- JPEG: los ficheros empiezan por los bytes [0xFF, 0xD8] y terminan con los bytes [0xFF, 0xD9].
- PDF: los ficheros empiezan por la cadena de caracteres "%PDF" (en hexadecimal: [0x25,
  0x50, 0x44, 0x46])
- ZIP: los ficheros empiezan por los caracteres "PK" (en hexadecimal: [0x50, 0x4B])

Para comprobar el número mágico se puede usar la orden hexdump:

```bash
hexdump -C archivo | less
```

Ejemplos de ficheros interesantes para visualizar: /proc/cpuinfo, /proc/meminfo,
/etc/passwd

#### Enlaces simbólicos y enlaces duros

- Un enlace simbólico o blando es un fichero que contiene una referencia a
  otro fichero: `/home/user/link` → `/etc/prog.conf`
- Un enlace duro es una entrada de directorio asociada a un fichero
  - Un mismo fichero puede tener más de una entrada en el árbol de directorios:
    `/home/user/name1` y `/etc/name2` → el mismo fichero

Tanto los enlaces simbólicos como los duros se crean con la orden ln.

Para crear un enlace simbólico:

```bash
ln -s link_name destination
```

Para crear un enlace duro:

```bash
ln link_name destination
```

Tras crear un enlace simbólico, se puede ver el «contenido» del enlace (es decir, a dónde
apunta) haciendo un listado detallado del fichero (con ls -l). Si se borra el fichero de destino,
el enlace queda «roto».

Tras crear un enlace duro, el listado detallado mostrará que ha aumentado el número de enlaces
del fichero. Con la orden ls -li se puede comprobar que el número de i-nodo
es el mismo para ambos enlaces duros. Si se borra uno de los dos ficheros, el otro se mantiene.
El fichero no se borra del todo hasta que se eliminan todos sus enlaces.

#### Comodines y variables

- El intérprete de órdenes define comodines que permiten
  definir patrones de coincidencia. Estos caracteres se analizan y
  se sustituyen antes de ejecutar los programas:
  - * (asterisco): coincide con una secuencia de cero o más caracteres
  - ? : coincide con un único carácter
- Se pueden definir variables cuyos valores también se sustituyen en la
  orden final:
  - Variables del shell: variables de la instancia actual del shell
  - Variables de entorno: variables que heredan los programas
    lanzados desde el intérprete de órdenes

Para definir una variable del shell:

```bash
NAME=value
```

Para definir una variable de entorno:

```bash
export NAME=value
```

Las variables pueden incluirse como parte de la orden poniendo el carácter '$' delante
del nombre de la variable, por ejemplo:

```bash
echo $PATH
```

Antes de llamar a la orden echo, el shell sustituye PATH por el valor de la
variable.

Las variables de entorno se pueden mostrar con la orden env.

Además de las variables, el shell puede sustituir el resultado de la ejecución de una
orden:

```bash
DIRECTORIO=$(pwd)
echo $DIRECTORIO
```

#### Órdenes generales

- Hay distintas órdenes que permiten realizar
  operaciones generales sobre los ficheros:
  - cp: copia el contenido de un fichero en otro fichero
  - mkdir: crea un directorio nuevo
  - rm: borra un fichero
  - rmdir: borra un directorio vacío
  - mv: mueve (o renombra) un fichero

Para borrar un directorio que no está vacío se puede usar la orden rm con la opción -r
(borrado recursivo).

### Permisos de acceso

- Los permisos de los ficheros se dividen en tres clases:
  - Permisos de lectura
  - Permisos de escritura
  - Permisos de ejecución
- Cada fichero tiene tres conjuntos de permisos:
  - Permisos asignados al propietario del fichero
  - Permisos asignados al grupo propietario del fichero
  - Permisos para los demás usuarios
- Los permisos se pueden cambiar con la orden chmod

Los ficheros tienen un usuario propietario y un grupo propietario (un usuario al que pertenece el fichero y un grupo al que
también pertenece).

Los permisos del fichero se muestran en el listado detallado (ls -l)

La orden chmod permite cambiar los permisos de un fichero. Los permisos pueden
expresarse como un número de tres cifras en octal. Cada una de las cifras representa los
permisos de un conjunto (propietario, grupo y demás usuarios). Cada uno de los tres dígitos de la
representación binaria de cada una de esas cifras octales fija una de las clases de
permisos (lectura, escritura y ejecución, en este orden).

## Trabajar con órdenes

### ¿Qué es una orden?

- Hay distintos tipos de órdenes:
  - Ficheros ejecutables
  - Órdenes internas definidas por el intérprete
  - Guiones (scripts) de órdenes
  - Alias de órdenes
- La orden which muestra la ruta de los ficheros
  ejecutables

Ejemplo de orden interna: cd

Primer contacto paso a paso con vim: editar un fichero con dos órdenes (por ejemplo, un echo y un
ls), darle permisos de ejecución con chmod y ejecutarlo.

### Gestión de trabajos

- Las órdenes pueden ejecutarse en primer plano o en
  segundo plano
  - Para ejecutar una orden directamente en segundo plano, la línea de órdenes
    que la lanza tiene que terminar con el carácter &
- La orden jobs muestra todas las órdenes (trabajos) lanzadas en
  segundo plano
- Cuando una orden se está ejecutando en primer plano, se puede
  detener pulsando Ctrl+Z
- La orden fg reanuda en primer plano un trabajo detenido
- La orden bg reanuda en segundo plano un trabajo detenido

Pruebe a ejecutar una orden en primer plano y otra en
segundo plano:

```bash
sleep 10
sleep 10 &
```

Ejemplo con xload: http://linuxcommand.org/lc3_lts0100.php. Se pueden lanzar trabajos,
detenerlos con Ctrl + Z y pasarlos a primer o segundo plano con fg o bg.

### Monitorización de procesos

- Hay órdenes que proporcionan información sobre los
  procesos del sistema:
  - ps: lista los procesos vivos y muestra información sobre
    ellos
  - top: muestra de forma interactiva información sobre los procesos
    vivos
  - El sistema proporciona un mecanismo de comunicación asíncrona
    entre procesos conocido como señales
  - kill: permite enviar una señal a un proceso

Todos los procesos vivos tienen un identificador único llamado identificador de proceso o PID.

La orden kill se usa de la siguiente manera:

```bash
kill -N PID
```

Donde N es el número de la señal. Algunos ejemplos de señales:

- 2 : SIGINT: interrupción. Se envía al pulsar Ctrl+C.
- 9 : SIGKILL: muerte segura. No puede ignorarse. Se usa para matar procesos que no
  responden y que no terminan de otra forma.
- 15 : SIGTERM: fin del proceso. Similar a la 9, pero esta sí puede ignorarse.

## Entrada/salida

### Visión general

*(diagrama: un Process con tres ficheros especiales asignados —
(0) Standard input, (1) Standard output y (2) Standard error output)*

- A todos los procesos se les asignan tres ficheros especiales:
  - 0 : entrada estándar (por defecto, el teclado del terminal)
  - 1 : salida estándar (por defecto, la pantalla del terminal)
  - 2 : salida estándar de errores (por defecto, la pantalla del terminal)
- Los procesos se comunican con el exterior leyendo y escribiendo
  en esos ficheros

Cuando un proceso necesita leer datos, normalmente lo hace a través de la entrada estándar,
es decir, leyendo del fichero con descriptor 0, que por defecto se refiere al
teclado. Del mismo modo, cuando un proceso necesita mostrar información, normalmente
lo hará escribiendo en el fichero con descriptor 1, que corresponde a la salida
estándar. Si la información que se va a mostrar corresponde a algún error de ejecución, el
proceso puede usar la salida estándar de errores, es decir, el fichero con descriptor 2.

### Redirecciones

- Los ficheros por defecto de la entrada y las salidas estándar se pueden
  modificar en la propia orden mediante redirecciones:

Redirección de la entrada estándar (<):

```bash
bc < operaciones
```

Redirección de la salida estándar (>, >>):

```bash
echo $PATH > path
```

Redirección de la salida estándar de errores (2>, 2>>):

```bash
ls /foo 2> /dev/null
```

### Tuberías

#### Descripción general

- Las tuberías (pipes) son un mecanismo de comunicación entre procesos
- Permiten conectar la salida estándar de un proceso con la
  entrada estándar de otro, por ejemplo:

```bash
ls | wc -w
```

- Pueden conectar dos o más procesos (pipeline):

```bash
command_1 | command_2 | command_3 | ...
```

#### Filtros

- Un filtro es un programa que lee de su entrada estándar y escribe
  en su salida estándar
- Normalmente los filtros pueden aceptar uno o más ficheros como parámetros
  (sin necesidad de redirigir la entrada)
- En el sistema hay numerosos filtros:
  - sort: ordena las líneas de la entrada
  - cut: extrae uno o más campos de las líneas de la entrada
  - grep: busca patrones de texto en las líneas de la entrada
  - tail: muestra las últimas N líneas de la entrada
  - head: muestra las primeras N líneas de la entrada

La orden cut permite extraer determinados caracteres de las líneas de un fichero. Por
ejemplo:

```bash
cut -c 1-9 filename
```

Extrae los nueve primeros caracteres de cada línea del fichero de entrada y los escribe en la
salida estándar.

También permite extraer campos usando delimitadores, por ejemplo:

```bash
cut -f 3 -d ':' /etc/passwd
```

Extrae el tercer campo, delimitado por el carácter ':', de las líneas del fichero
/etc/passwd.

## Ejercicios propuestos

*(el título de esta diapositiva ya estaba en español, «Ejercicios propuestos»,
en el original, que por lo demás estaba en inglés)*

1. Mostrar la fecha actual con el formato 31-12-2019 (día,
   mes y año separados por un guion '-')
2. Copiar el fichero /etc/passwd en el directorio de trabajo actual:
   - Usando rutas absolutas
   - Usando rutas relativas
3. Guardar la ocupación actual del disco en un fichero con el siguiente
   nombre: diskreport-{month}-{day}-{hour}-{min}-{sec}
4. ¿Cuántas imágenes hay en la web https://www.uah.es?
   - Buscar información sobre la orden curl
   - Filtrar con grep las líneas que contienen la etiqueta img
   - Contar el número de líneas

Si la orden curl no estuviera instalada, se puede usar en su lugar la orden wget:

```bash
wget -qO - https://www.uah.es
```

## Bibliografía

- Sebastián Sánchez Prieto y Óscar García Población.
  Unix y Linux, guía práctica. Ra-Ma, 3.ª ed., 2004.
- The Linux Command Line. Disponible en:
  http://linuxcommand.org/lc3_learning_the_shell.php

---

© Pablo Parra, Óscar García. Departamento de Automática. Universidad de Alcalá.
Este documento se distribuye bajo los términos de la licencia Creative Commons Attribution ShareAlike 4.0 (internacional):
https://creativecommons.org/licenses/by-sa/4.0/
