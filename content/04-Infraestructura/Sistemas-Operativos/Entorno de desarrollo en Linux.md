---
title: "Entorno de desarrollo en Linux"
---

# El entorno de desarrollo de Linux

*Departamento de Automática*

## Contenidos

- El editor Vim
  - Opciones de configuración
  - Referencia rápida
  - Ayuda integrada
- Ciclo de creación de programas
  - Generación del ejecutable
  - Depuración
- La herramienta make
  - Ejemplo de makefile

## El editor Vim

### Descripción general

- El editor Vim (Vi iMproved) es un editor de ficheros libre y de código abierto
  para la consola de Linux
- Lo desarrolló Bram Moolenaar
  - Está escrito en C y en vimscript
  - La primera versión es de noviembre de 1991
  - Se puede ampliar mediante plugins

Proyecto en Github: https://github.com/vim/vim

Uso de editores y entornos de desarrollo. Encuesta basada en 46.613 respuestas
publicada por Stackoverflow. El desarrollador medio usa entre dos y
tres entornos distintos.

Vim es el editor más utilizado en entornos de línea de comandos.

### Primeros pasos

#### Modos

El editor Vim tiene cuatro modos de trabajo:

| Modo | Descripción |
| --- | --- |
| Modo normal | Moverse, copiar (yank), pegar, borrar, etc. |
| Modo inserción | Edición de texto |
| Modo línea de comandos | Guardar, buscar, salir |
| Modo visual | Selección de texto (resaltado) |

Siempre arranca en modo normal: `$ vim filename`

El editor Vim define cuatro entornos de trabajo:

- El modo normal es el modo general de la aplicación. En este modo podemos usar
  órdenes para movernos por el documento; copiar, pegar o borrar texto; o cambiar
  al resto de modos.
- El modo inserción permite añadir texto al documento.
- El modo línea de comandos es un modo especial que acepta órdenes en lenguaje
  vimscript.
- El modo visual permite seleccionar (resaltar) una parte del texto del documento
  y aplicar después una orden específicamente sobre la selección.

#### Edición de ficheros

1. Pasar a modo inserción: `i`
2. Escribir el texto
3. Volver a modo normal: `esc`
4. Pasar a modo línea de comandos: `:`
5. Guardar los cambios en disco: `w` `Enter`
6. Pasar a modo línea de comandos: `:`
7. Salir del editor: `q` `Enter`

Pulsar ':' desde el modo normal es una de las formas de pasar al modo línea de comandos.
Otras son '/' y '?', para buscar cadenas dentro del documento.

### Opciones de configuración

Opciones de configuración:

- La configuración de Vim se hace mediante el modo línea de comandos (vimscript)
- El fichero `~/.vim/vimrc` contiene las órdenes que se
  ejecutarán cada vez que se inicie vim
- Ejemplos de configuración (dentro del fichero vimrc no hace falta poner ':'):

```vim
syntax on                                      " activates syntax highlighting
set tabstop=4                                  " tabulation of 4 spaces
set shiftwidth=4                               " indentation of 4 spaces
set expandtab                                  " use of spaces instead of the TAB character
autocmd FileType make setlocal noexpandtab     " for Make files, use the TAB character instead of spaces
```

Edita el fichero `~/.vim/vimrc` para modificar las opciones de configuración. Una vez modificado y
guardado, hay que salir de Vim y volver a entrar para que se apliquen los cambios.

Las órdenes "set" pueden agruparse en una sola línea:

```vim
set tabstop=4 shiftwidth=4 expandtab
```

La orden `autocmd` sirve para configurar que se ejecute una
orden cuando se produzca un determinado evento. Por ejemplo, en este caso, si el fichero es de
tipo "make" (FileType make), se ejecuta la orden setlocal noexpandtab.

Cuestiones como el tamaño del tabulador forman parte de lo que se denomina
estilo de programación. Otros elementos del estilo de programación pueden ser, por ejemplo, el
tamaño máximo de una línea de código (80 o 120 caracteres) o la forma de nombrar
las variables (snake-case o camel-case). Normalmente, cada organización o empresa fija su
propio estilo de programación para homogeneizar el software que produce. Un ejemplo de
documento de estilo es el del kernel de Linux.

### Referencia rápida

*(las siguientes tablas de referencia rápida se extrajeron del PDF como
un único bloque de texto a dos columnas, con las columnas intercaladas
línea a línea; se han separado con alta confianza en las dos columnas
originales)*

**Movimiento del cursor**

| Tecla | Acción |
| --- | --- |
| `k` | arriba |
| `j` | abajo |
| `h` | izquierda |
| `l` | derecha |
| `Ctrl+b` | página anterior |
| `Ctrl+f` | página siguiente |
| `w` | principio de la palabra siguiente |
| `b` | principio de la palabra anterior |
| `gg` | principio del documento |
| `G` | final del documento |
| `$` | final de la línea |
| `0` | primer carácter de la línea actual |
| `_` | primer carácter no blanco de la línea actual |

**Entrada en modo inserción**

| Tecla | Acción |
| --- | --- |
| `i` | en el cursor |
| `a` | antes del cursor |
| `gI` | primer carácter de la línea |
| `I` | primer carácter no blanco de la línea |
| `A` | final de la línea |
| `o` | en una línea nueva debajo de la actual |
| `O` | en una línea nueva encima de la actual |

**Reemplazar + insertar**

| Tecla | Acción |
| --- | --- |
| `s` | cambiar el carácter bajo el cursor |
| `cc` | cambiar la línea actual |
| `C` | cambiar hasta el final de la línea |
| `cm` | cambiar con el movimiento m |

**Borrar / cortar**

| Tecla | Acción |
| --- | --- |
| `x` | borrar el carácter bajo el cursor |
| `dd` | borrar la línea actual |
| `D` | borrar hasta el final de la línea |
| `dm` | borrar con el movimiento m |

**Copiar y pegar**

| Tecla | Acción |
| --- | --- |
| `yy` | copiar la línea actual |
| `ym` | copiar con el movimiento m |
| `p` | pegar después del cursor |
| `P` | pegar antes del cursor |

**Deshacer / rehacer**

| Tecla | Acción |
| --- | --- |
| `u` | deshacer la última acción |
| `Ctrl+R` | rehacer lo último deshecho |
| `.` | repetir la última acción |

**Modo visual**

| Tecla | Acción |
| --- | --- |
| `v` | iniciar selección en modo carácter |
| `V` | iniciar selección en modo línea |
| `Ctrl+v` | iniciar selección en modo bloque |

**Guardar y salir**

| Comando | Acción |
| --- | --- |
| `:w` | guardar el fichero actual |
| `:w f` | guardar el fichero actual como f |
| `:q` | salir del editor |
| `:wq` | guardar el fichero actual y salir del editor |
| `:q!` | salir del editor sin guardar los cambios |

**Búsqueda**

| Comando | Acción |
| --- | --- |
| `/s` | buscar la cadena s hacia delante |
| `?s` | buscar la cadena s hacia atrás |
| `n` | ir a la siguiente ocurrencia |
| `N` | ir a la ocurrencia anterior |

**Miscelánea**

| Comando | Acción |
| --- | --- |
| `:r f` | copiar el contenido del fichero f bajo el cursor |
| `:r! c` | copiar la salida de la orden c bajo el cursor |

**Ventanas**

| Comando | Acción |
| --- | --- |
| `:split` | dividir la ventana actual |
| `:new f` | abrir el fichero f en una nueva ventana horizontal |
| `:vnew f` | abrir el fichero f en una nueva ventana vertical |
| `Ctrl+w k` | ir a la ventana de arriba |
| `Ctrl+w j` | ir a la ventana de abajo |
| `Ctrl+w h` | ir a la ventana de la izquierda |
| `Ctrl+w l` | ir a la ventana de la derecha |

### Ayuda integrada

- Vim tiene ayuda integrada
- Para acceder a la documentación dentro del editor: `:help y` / `:h movement`
- La ayuda aparece en una pantalla de solo lectura
- Se pueden seguir los enlaces con las secuencias:
  - `Ctrl+]` ir al enlace bajo el cursor
  - `Ctrl+t` volver atrás
- Hay un tutorial complementario llamado Vimtutorial (vimtutor)

## Ciclo de creación de programas

### Pasos del desarrollo

1. Edición
2. *(paso no identificado en la extracción — el índice enumera "1: 2:
   3" pero solo se conservan las etiquetas "Edition" y "Debugging")*
3. Depuración

*(diagrama: cadena de herramientas GNU — GDB, Make)*

### Generación del ejecutable

*(diagrama del proceso de generación de un ejecutable a partir de dos
módulos fuente: Module 1 y Module 2 pasan por el Compilador/Ensamblador
("relbmessa" y "relipmoC" invertidos en la extracción = "assembler" y
"Compiler") para producir Object file 1 y Object file 2; estos, junto
con ficheros objeto externos y bibliotecas, pasan por el Linker
("rekniL" invertido) para producir el Executable file, todo almacenado
en Secondary storage)*

Un programa ejecutable puede desarrollarse en distintos ficheros fuente, llamados módulos.
Cada módulo tiene que compilarse por separado para obtener su fichero objeto correspondiente.
Estos ficheros contienen las instrucciones binarias resultantes de traducir el código fuente
de los módulos. Para obtener el ejecutable final puede ser necesario combinar el código
de los ficheros objeto recién obtenidos con otros fragmentos de código que se han
compilado previamente. Estos fragmentos de código compilado pueden almacenarse por separado o
agrupados en bibliotecas (una biblioteca es un conjunto de ficheros objeto). Un ejemplo de estos
códigos precompilados es la biblioteca estándar de C, que contiene, por ejemplo, el
código de las funciones printf () o scanf (), entre muchas otras.

#### Herramientas de GCC

*(diagrama de la cadena `gcc`: Preprocessing (cpp) → Compilation (comp) →
Object code generation (as) → Linker (ld); ficheros intermedios
`program.c` → `program.i` → `program.s` → `program.o` → `a.out`)*

- gcc puede conservar los ficheros intermedios a voluntad (-E, -S, -c)
- Otras opciones de gcc: -o, -Wall, -g

En la etapa de preprocesado se sustituyen, entre otras cosas, directivas como las MACROS (#define) o la inclusión de
ficheros (#include).

Por defecto, la orden gcc intenta ejecutar toda la cadena de generación a partir de un
fichero fuente en C, es decir, preprocesado, compilación, generación de código objeto y enlazado con
las bibliotecas estándar. Sin embargo, permite mediante opciones detener el proceso en cualquier
punto:

- -E: detiene el proceso tras el preprocesado.
- -S: se detiene tras la compilación.
- -c: se detiene tras generar un fichero objeto.

La opción -c es muy útil al generar programas implementados en varios
módulos. Como tenemos que compilar cada módulo por separado, necesitamos detener gcc
justo después de generar el código objeto para obtener los ficheros objeto resultantes de la compilación.

#### Programa de ejemplo

```c
// main.c
#include <stdio.h>
#include "add.h"

int add(int sumando1, int sumando2);

int main() {
    int a = 5, b = 10, c;
    c = add(a, b);
    printf("The result of the addition: %d\n", c);
    return 0;
}
```

```c
// add.c
#include "add.h"

int add(int a, int b) {
    return a + b;
}
```

Generación del fichero ejecutable:

```bash
gcc -g -Wall -c main.c -o main.o
gcc -g -Wall -c add.c -o add.o
gcc -g -Wall main.o add.o -o program
```

Para obtener los productos intermedios se pueden usar las opciones de gcc de la diapositiva
anterior:

- Detenerse tras el preprocesado: `$ gcc -E main.c -o main.i`
- Detenerse tras compilar y antes de ensamblar: `$ gcc -S main.c -o main.S`

Para mostrar el contenido de los ficheros objeto (o de los ejecutables) se puede usar el programa
objdump, que forma parte de las herramientas de GCC:

```bash
objdump -D main.o | less
```

Con la orden anterior podemos desensamblar el contenido del fichero objeto binario. Se
puede observar que las direcciones de las funciones (por ejemplo, la dirección de la
función sum ()) aún no están resueltas, es decir, quedan preparadas para fijarse al hacer
la combinación con el resto de módulos en la fase de enlazado.

Si desensamblamos el ejecutable final, podemos ver que las direcciones ya están
convenientemente resueltas:

```bash
objdump -D program | less
```

### Depuración

- Con el depurador podemos:
  - Ejecutar un programa paso a paso
  - Poner puntos de ruptura (breakpoints)
  - Inspeccionar el valor de las variables
- GDB puede invocarse desde la línea de comandos: `$ gdb program`
- Las órdenes de depuración se introducen a través de la consola de GDB

#### Referencia rápida

*(misma disposición a dos columnas que la tabla de Vim, separada con
alta confianza)*

**Ejecución**

| Comando | Acción |
| --- | --- |
| `run` | iniciar la ejecución del programa |
| `set args <argumentos>` | establecer los argumentos |
| `quit` | salir del depurador |

**Puntos de ruptura**

| Comando | Acción |
| --- | --- |
| `break <position>` | poner un punto de ruptura |
| `delete <# breakpoint>` | eliminar el punto de ruptura número # |
| `clear` | ir a la siguiente instancia |

**Ejecución paso a paso**

| Comando | Acción |
| --- | --- |
| `step` | ejecutar la siguiente instrucción entrando en las funciones |
| `next` | ejecutar la siguiente instrucción sin entrar en las funciones |
| `finish` | continuar hasta el final de la función actual |
| `continue` | continuar la ejecución del programa |

**Variables y memoria**

| Comando | Acción |
| --- | --- |
| `print/format <item>` | mostrar un valor con formato |
| `x/nfu <address>` | volcar valores de memoria con formato |

`<item>`: expresión (por ejemplo, el nombre de una variable), dirección de memoria, `$register` (p. ej. `$ax`)

**Formato (format)**

| Formato | Significado |
| --- | --- |
| `a` | un puntero |
| `d` | decimal con signo |
| `u` | decimal sin signo |
| `f` | coma flotante |
| `x` | hexadecimal |

**Unidades**

| Unidad | Significado |
| --- | --- |
| `b` | byte |
| `h` | media palabra (dos bytes) |
| `w` | palabra (cuatro bytes) |
| `g` | palabra gigante (ocho bytes) |

## La herramienta make

### Descripción general

- La herramienta Make automatiza el proceso de generación de programas cuando
  se usan muchos módulos
- Un fichero le indica a Make cómo obtener todos los subproductos intermedios
  y cómo enlazarlos para generar un fichero ejecutable.
  - Por defecto, el nombre de este fichero es makefile o Makefile
  - Está escrito en un lenguaje específico
- La herramienta puede invocarse desde la línea de comandos:

```bash
make
make -f makefile_file
```

Al lanzarse, la herramienta busca el fichero de reglas. Si la llamamos sin argumentos,
intentará localizar un fichero llamado makefile o Makefile. Si el fichero tiene otro
nombre, hay que indicarlo expresamente con la opción -f.

### El lenguaje de Make

- La unidad fundamental de un makefile es la regla
- Cada regla consta de
  - objetivo (target): el subproducto que se quiere generar
  - dependencias: la lista de ficheros necesarios para construir el objetivo
  - órdenes: las órdenes que hay que ejecutar sobre las dependencias para construir
    el objetivo

```makefile
target: dependency1 dependency2 …    # Space-separated list of dependencies
<TAB> command1
<TAB> command2
<TAB> …
                                       # Blank line
```

- Un makefile puede contener una o varias reglas
- Por defecto, la herramienta intenta completar la primera regla del fichero
  - Si queremos completar otra, podemos poner el nombre del objetivo
    después de la orden make en la línea de comandos
- Si una dependencia no existe:
  - Busca en el fichero una regla para generar la dependencia
  - Si no encuentra ninguna regla, muestra un mensaje de error
- Si el objetivo ya existe:
  - Compara su fecha de modificación con la fecha de modificación de las
    dependencias.
  - Si alguna dependencia es más reciente que el objetivo, el objetivo se reconstruye

### Ejemplo de makefile

```makefile
.PHONY: clean
CC=gcc
CFLAGS=-g -Wall

program: main.o add.o
	$(CC) $(CFLAGS) main.o add.o -o program

main.o: main.c add.h
	$(CC) $(CFLAGS) -c main.c -o main.o

add.o: add.c add.h
	$(CC) $(CFLAGS) -c add.c -o add.o

clean:
	rm -rf *.o program
```

- Para generar el fichero ejecutable: `$ make`
- Para eliminar los productos intermedios y el propio ejecutable: `$ make clean`

El lenguaje de los Makefile permite definir variables cuyo valor puede
sustituirse en el resto del fichero. En el ejemplo se definen dos variables,
CC y CFLAGS, que sustituyen, respectivamente, el nombre del compilador y las opciones
de compilación.

El fichero de ejemplo define un objetivo llamado clean. Este objetivo es muy habitual y se
suele usar para limpiar el proyecto de ficheros intermedios y del ejecutable final del
programa, dejando solo los ficheros fuente. El objetivo clean se define como un objetivo
PHONY. Así le indicamos a Make que el objetivo no corresponde a un
fichero concreto del proyecto y que, si por casualidad existe un fichero llamado "clean", se
ignore. De este modo, el objetivo clean siempre se ejecuta cuando se solicita desde
la línea de comandos.

## Bibliografía

- Drew Neil. Practical Vim. The Pragmatic Programmers, 2 Ed., 2015.
- Debugging with GDB. Disponible en:
  https://sourceware.org/gdb/onlinedocs/gdb/
- GNU Make Reference Manual. Disponible en:
  https://www.gnu.org/software/make/manual/make.html

---

© Pablo Parra, Óscar García. Departamento de Automática. Universidad de Alcalá.
Este documento se distribuye bajo los términos de la licencia Creative Commons Reconocimiento-CompartirIgual 4.0 (internacional)
(Attribution ShareAlike 4.0): https://creativecommons.org/licenses/by-sa/4.0/
