---
title: "Procesos e hilos"
---

# Procesos e hilos

*Departamento de Automática*

## Contenido

- Programas
  - El concepto de programa
  - Ejemplo de programa en UNIX
  - Formato ejecutable
- Procesos
  - El concepto de proceso
  - El bloque de control de proceso (PCB)
  - Estados de un proceso en Linux
  - Mapa de memoria de un proceso
- Servicios POSIX para la gestión de procesos
  - Creación de procesos
  - Ejecución de programas
  - Terminación de procesos
  - Espera a la terminación de un proceso
- Hilos
  - Objetivos y conceptos
  - Implementación y programación con hilos
  - Hilos frente a procesos
  - Ejemplo de programación
- Sincronización de procesos e hilos
  - El problema
  - Sincronización mediante semáforos

## Programas

### Concepto y características de un programa

Un programa es un conjunto de instrucciones y datos que normalmente se guarda en un
fichero regular.

Características de un programa:

- Se almacena en un dispositivo no volátil
- Para ejecutarse, tiene que cargarse en memoria
- Es una entidad estática

### Ejemplo de programa en UNIX

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int printit = 1;
char *nomprog;

int main(int argc, char *argv[]) {
    int i;
    int *ptr;
    nomprog = argv[0];
    printf("No. of args = %d\n", argc);
    printf("Program name.: %s\n", nomprog);
    for (i = 0; i < argc; i++) {
        ptr = malloc(strlen(argv[i]) + 1);
        strcpy(ptr, argv[i]);
        if (printit) {
            printf("%s\n", ptr);
        }
        free(ptr);
    }
    return 0;
}
```

*(el programa está anotado con un mapa de memoria "Memory Map" que
señala qué parte del código corresponde a cada región: la declaración
`int printit = 1;` a "Código (text)" — sic, aparece mezclada con la
etiqueta en inglés "(text)" doblada por el resaltado del PDF —, `char
*nomprog;` a "Datos inicializados (data)", las variables locales `i` /
`ptr` a "Datos no inicializados (bss)", la memoria reservada con
`malloc` a "Dynamic memory (heap)", y las variables automáticas de la
pila a "Pila / Stack (stack)". La posición exacta de cada llamada no
se pudo recuperar de la extracción OCR.)*

### Formato ejecutable

Fichero ejecutable:

| Nombre | Offset | Tamaño |
| --- | --- | --- |
| Código (text) | 1000 | 3000 |
| Datos inicializados | 4000 | 1000 |
| Datos no inicializados | - | 100 |
| Tabla de símbolos | 7000 | 1000 |

*(diagrama del fichero ejecutable: la cabecera "Header" ("redaeH"
invertido en la extracción) contiene el número mágico "Magic number" y
el contador de programa inicial "Initial program counter", seguida de
la tabla de secciones "Section table" ("snoitceS" invertido); las
secciones —Code, Initialized data, Symbol table— comienzan en los
offsets 0, 1000, 4000 y 7000 respectivamente)*

Existen muchos formatos distintos de fichero ejecutable: ELF, EXE, COM, etc.

## Procesos

### El concepto de proceso

Un proceso es un programa en ejecución.

Características de un proceso:

- Es una entidad dinámica
- Los procesos tienen sus propios datos, código, pila, heap, etc.
- El SO les asigna recursos: CPU, memoria, ficheros, etc.
- El SO controla su ejecución
- El SO lleva la contabilidad de todos los procesos en ejecución

Muchos procesos pueden ejecutar el mismo programa. Un proceso puede crear otro proceso.

#### Procesos en UNIX

- Cada proceso tiene un identificador de proceso único (PID)
- Todos los procesos forman una jerarquía cuya raíz es el proceso
  init
  - init es el primer proceso que arranca en UNIX
  - Su PID es 1
  - El objetivo principal de init es arrancar los distintos procesos, por
    ejemplo: login
  - En muchas distribuciones de Linux, init está siendo sustituido por systemd
- El PPID (Parent Process IDentifier) es el PID del proceso
  padre

### El bloque de control de proceso (PCB)

**Concepto**: es una gran estructura de datos con información sobre cada proceso.

La información del PCB es:

- El estado actual del proceso
- El identificador de proceso único (PID)
- La prioridad del proceso
- El mapa de memoria del proceso
- Los recursos asignados al proceso
- El área de salvaguarda de los registros

En Linux, el PCB se llama `task_struct`.

### Diagrama de estados de un proceso en Linux

*(diagrama de estados del proceso en Linux: Ready —(Dispatch)→ Run
—(Preempt)→ Ready; Run —(Sleep)→ Sleep —(Wake up)→ Ready; Run
—(End)→ Zombie (EXIT_ZOMBIE); los estados del kernel de Linux
asociados son TASK_RUNNING, TASK_INTERRUPTIBLE, TASK_UNINTERRUPTIBLE /
TASK_KILLABLE (ambos para Sleep), TASK_STOPPED (Parado) y
TASK_TRACED)*

### Mapa de memoria de un proceso

#### El espacio de direcciones virtual de un proceso

*(diagrama de traducción de direcciones: los espacios de direcciones
virtuales de "application A" y "application B" (con páginas A-G) se
traducen, cada uno mediante su propia tabla de traducción ("Translation
table") y la MMU, al mismo espacio de memoria física ("Physical
Memory"); la disposición exacta de las páginas no se pudo recuperar de
la extracción OCR)*

#### El fichero ejecutable frente al mapa de memoria de un proceso

| Fichero ejecutable | Mapa de memoria |
| --- | --- |
| Cabecera ("redaeH" invertido): número mágico, contador de programa inicial | — |
| Tabla de secciones ("snoitceS" invertido) | — |
| Código | Código (text) |
| Datos inicializados | Datos inicializados (data) |
| La tabla de símbolos | Datos no inicializados (bss) |
| — | Memoria dinámica (heap) |
| — | Proyección del fichero X |
| — | Memoria compartida |
| — | Código de la biblioteca dinámica Z |
| — | Datos de la biblioteca dinámica Z |
| — | Pila del hilo 1 / Pila |

*(la correspondencia fila a fila entre el fichero ejecutable —offsets
0, 1000, 4000, 7000— y el mapa de memoria resultante no se pudo
recuperar con precisión de la extracción OCR; se listan ambas columnas
por separado)*

Propiedades de las regiones: soporte (fichero/anónima), compartida, protección y tamaño.
*(«Posibles regiones presentes en tiempo de ejecución» — texto invertido en la
extracción como "ni / tneserp / snoiger / elbissoP / emit-nur")*

#### Mapa de memoria de un proceso en UNIX

*(diagrama de contextos: el "User context" incluye Code (text),
Initialized data, Uninitialized data (BSS) y HEAP (dynamic memory);
el "Kernel Context" incluye datos del kernel sobre el proceso y la
pila en modo kernel ("Kernel mode stack"). La pregunta que ilustra el
diagrama es "What's the relationship between context and CPU execution
mode?": en modo supervisor ("Supervisor mode") se distinguen las
transiciones 2 (User context) y 4 (Interrupts); en modo usuario
("User mode") las transiciones 1 (Normal execution) y 3 (System
calls). La disposición exacta del diagrama no se pudo recuperar de la
extracción OCR.)*

#### Mapa de memoria de un proceso en Linux en arquitecturas de 32 bits

*(diagrama de espacio de direcciones de 32 bits: de 0x00000000 a
0xC0000000 el espacio de Usuario (3 GB), que empieza en 0x08048000 con
Code (text), Initialized data (data), Uninitialized data (bss),
crece hacia arriba con la memoria dinámica (heap, con desplazamiento
aleatorio a partir de start_brk) hasta 0xBFFFFFFF, y hacia abajo con la
pila (Stack, con un "Stack max size" y desplazamiento aleatorio a
partir de start_stack) y la memoria compartida; de 0xC0000000 a
0xFFFFFFFF el espacio de Kernel (1 GB). La disposición exacta no se
pudo recuperar de la extracción OCR.)*

#### Mapa de memoria de un proceso en Windows en arquitecturas de 32 bits

*(diagrama de espacio de direcciones de 32 bits: de 0x00000000 a
0x80000000 el espacio de Usuario (2 GB) — Code .EXE, Thread stacks,
Heap, Code .DLL, hasta 0x7FFFFFFF—; de 0x80000000 a 0xFFFFFFFF el
espacio de Kernel (2 GB) — Executive, kernel, HAL, drivers, kernel
threads stack, Win32K.sys, Page map tables, Filesystem cache—. La
disposición exacta no se pudo recuperar de la extracción OCR.)*

## Servicios POSIX para la gestión de procesos

Objetivo de los servicios POSIX para la gestión de procesos:

- Creación de procesos (fork)
- Asignación de un programa al proceso
- Terminación de procesos
- Identificación de procesos
- Gestión del entorno del proceso

### Creación de procesos

#### Visión general

*(diagrama de `fork()`: el proceso A (PA), con su mapa de memoria
virtual —text, data-PA, bss-PA, heap-PA, stack-PA, shared libs, tabla
de traducción y PCB—, se duplica en un proceso hijo B (PB) con su
propia copia —data-PB, bss-PB, heap-PB, stack-PB, tabla de traducción
y PCB—, compartiendo el mismo `text` y las mismas bibliotecas
compartidas ("shared libs"); ambos PCB quedan enlazados en la lista de
PCBs del sistema. La disposición exacta del diagrama no se pudo
recuperar de la extracción OCR.)*

#### Creación de procesos (servicio POSIX)

**Prototipo**

```c
pid_t fork()
```

**Descripción**

Crea una copia del proceso que realiza la llamada (padre) en un proceso nuevo (hijo).

**Devuelve**

Si la función tiene éxito:

- Al padre: el pid del proceso hijo
- Al proceso hijo: 0

En caso contrario: -1, y el código de error en la variable global errno.

#### Creación de procesos (ejemplo)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    pid_t id;
    id = fork();
    if (id == -1) {
        perror("Error when calling fork");
        exit(1);
    }
    if (id == 0) {
        while (1) {
            printf("Hi! I'm the child\n");
        }
    } else {
        while (1) {
            printf("Hi! I'm your father\n");
        }
    }
    return 0;
}
```

### Ejecución de programas

#### Esquema

*(diagrama de `exec()`: el proceso A (PA), con su mapa de memoria
virtual —text, data, bss, heap, stack, shared libs, tabla de
traducción y PCB—, carga el código del fichero ejecutable
correspondiente desde el dispositivo de almacenamiento secundario
("Executable Secondary storage device"), sustituyendo su imagen de
memoria; la lista de PCBs se mantiene. La disposición exacta del
diagrama no se pudo recuperar de la extracción OCR.)*

#### Ejecución de programas (servicio POSIX)

**Prototipo**

```c
int execl(const char *path, const char *arg, ...)
int execlp(const char *file, const char *arg, ...)
int execv(const char *path, char const *argv[])
int execvp(const char *path, char const *argv[])
int execvpe(const char *path, char const *argv[], char const *evnp[])
```

**Descripción**: sustituye la imagen del proceso actual por otra cargada
desde un fichero ejecutable.

**Devuelve**

En caso de error: -1, y el código de error en la variable global errno.

#### Ejecución de programas (ejemplo)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    pid_t id;
    char *args[3];
    args[0] = "ps";
    args[1] = "-l";
    args[2] = NULL;
    if (execvp(args[0], args) == -1) {
        perror("Error when calling execvp");
        exit(1);
    }
    return 0;
}
```

### Terminación de procesos

**Prototipo**

```c
void exit(int status)
```

**Descripción**

Termina la ejecución de un proceso. El proceso indica cómo
ha terminado mediante el parámetro status.

- Cuando un proceso termina, sus hijos los adopta el proceso
  init/systemd.
- El valor de status se entrega al proceso padre

### Espera a la terminación de un proceso

**Prototipo**

```c
pid_t wait(int *status)
pid_t waitpid(pid_t pid, int *status, int options)
```

**Descripción**: hace que el proceso que llama espere a que termine un
proceso hijo, y obtiene su estado de terminación.

**Devuelve**: el PID del proceso que ha terminado.

¿Cómo se ejecuta una orden de bash?

#### Espera a la terminación de un proceso (ejemplo)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    pid_t id;
    int status;
    id = fork();
    if (id == -1) {
        perror("Error when calling fork");
        exit(1);
    }
    if (id == 0) {
        printf("I'm the child\n");
        sleep(5);
        printf("Child: awakes and ends\n");
        exit(0);
    } else {
        printf("I'm the father\n");
        wait(&status);
        printf("Father: The child ended up with status = %d\n", estado);
        exit(0);
    }
    return 0;
}
```

## Hilos

### Objetivos y conceptos

**Objetivo**: compartir recursos entre procesos que cooperan.

**Concepto**

- Hilo = proceso ligero (LWP)
- Son las unidades fundamentales que utiliza el procesador.
- Cada hilo tiene su propia copia de los registros de la CPU y su propia pila
- Las tareas pasan a ser contenedores de hilos; por tanto, un hilo pertenece a una
  única tarea.
- El código, los datos y los recursos (ficheros, memoria compartida, etc.) pertenecen a la
  tarea

#### Características

- Cada hilo comparte el código, los datos y los recursos del SO con los demás
  hilos de su tarea.
- Una tarea sin hilos no tiene capacidad de ejecución
- Los hilos son muy convenientes para los sistemas multiprocesador (SMP)
- Un proceso convencional está formado por un único hilo de ejecución

*(diagrama: un proceso pesado "Heavy process" corresponde a una única
Task; los procesos ligeros "Lightweight processes" son los threads
dentro de esa misma Task)*

### Implementación y programación con hilos

- Todos los SO modernos admiten hilos (Windows,
  Linux, MacOS, etc.)
- Existen bibliotecas para programar con hilos, como
  POSIX Threads, Sun Threads, DCE Threads, etc.
- Al programar con hilos hay que tener especial cuidado
  para evitar las condiciones de carrera y otros
  problemas de sincronización

### Hilos frente a procesos

- Los hilos se crean y se destruyen más rápido que los procesos
- El tiempo de cambio entre hilos es mucho menor que el
  tiempo de cambio entre procesos (cambio de contexto)
- Todos los hilos de un mismo proceso comparten la memoria, por lo que
  hay menos sobrecarga de comunicación (y muchos más
  problemas de sincronización)

### Ejemplo de programación

```c
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>

void *threadfun(void *arg) {
    int thread_num = *((int *)arg);
    printf("I'm the child -> %d\n", thread_num);
    pthread_exit(0);
}

int main() {
    pthread_t thread1, thread2;
    int id1 = 1, id2 = 2;
    pthread_create(&thread1, NULL, threadfun, &id1);
    pthread_create(&thread2, NULL, threadfun, &id2);
    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);
    return 0;
}
```

## Sincronización de procesos e hilos

### El problema

Sincronización de hilos o procesos: los hilos o procesos necesitan con frecuencia
coordinarse, porque cooperan para alcanzar un objetivo o porque
compiten por un recurso.

Motivos por los que es necesario proporcionar sincronización:

- Algunos recursos deben usarse en exclusión mutua
- Un proceso debe esperar a la acción de otro proceso
- Varios procesos/hilos pueden leer-modificar-escribir la misma
  posición de memoria, lo que da lugar a las famosas condiciones de carrera

Un proceso no puede detener su propia ejecución ni la de
otro ⇒ se necesita la intervención del núcleo.

### Sincronización mediante semáforos

Los semáforos son objetos del núcleo compartidos por todos los procesos que intervienen en
la sincronización.

Operaciones sobre los semáforos:

- Operación P (semáforo):
  - Si el semáforo tiene un valor positivo, su valor se decrementa en una unidad
  - Si el semáforo vale cero, el hilo/proceso que llama se duerme en una lista
    de espera
- Operación V (semáforo):
  - Si no hay hilos/procesos dormidos, su valor se incrementa en una
    unidad.
  - Si hay hilos/procesos dormidos, se despierta al primero de la lista

#### Algunos problemas típicos de sincronización

Sección crítica (condición de carrera) frente a productor-consumidor básico:

| P1 | P2 | productor | consumidor |
| --- | --- | --- | --- |
| … | … | … | … |
| `P(S1);` | `P(S1);` | `data = create();` | `P(S1);` |
| `A++;` | `a++;` | `V(S1);` | `consume(data);` |
| `V(S1);` | `V(S1);` | … | … |
| … | … |  |  |

¿Importa el valor inicial de los semáforos?

## Bibliografía

- Sebastián Sánchez. Operating Systems. Second Edition.
  Universidad de Alcalá - Servicio de Publicaciones, 2005
- Francisco M. Márquez. UNIX. Advanced Programming. Ed.
  Ra-Ma, 2004
- A. S. Tanenbaum. Modern Operating Systems. 3rd Edition.
  Prentice Hall, 2009
- William Stallings. Computer organization and architecture.
  10th Edition. Pearson, 2015

---

© Pablo Parra, Óscar García. Departamento de Automática. Universidad de Alcalá.
Este documento se distribuye bajo los términos de la licencia Creative Commons Attribution ShareAlike 4.0 (internacional):
https://creativecommons.org/licenses/by-sa/4.0/
