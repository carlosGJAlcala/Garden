---
title: "Qué es un sistema operativo"
---

# Introducción

*Departamento de Automática*

## Índice

- Introducción a esta asignatura
  - Una máquina nueva
  - ¿Cómo se usa esta máquina?
  - El sistema operativo
- Los sistemas operativos en la Ingeniería de Computadores / Informática
  - Visión general
  - Arquitectura de computadores: conceptos básicos
- Evolución histórica
  - Máquina desnuda
  - Monitor residente
  - Sistemas de procesamiento por lotes
  - Multiprogramación
  - Sistemas de tiempo compartido
  - Sistemas de tiempo real

## Introducción a esta asignatura

### Una máquina nueva

- Procesador - Memoria

Entrada/Salida

- Monitor - Tarjeta de vídeo

Hub

Entrada/Salida

- Teclado: Puerto USB: Puerto SATA: Disco duro

Controller Hub

Sonido

Puerto USB

Tarjeta

Ethernet

- Ratón - 10/100/1000

MAC

### ¿Cómo podemos usar esta máquina?

#### ¿En qué consiste esta máquina nueva?

#### ¿Qué problemas tiene esta máquina?

- Cada elemento es distinto y muy complicado
- ¿Tengo que aprender a usarlos todos?
- ¿Y si el fabricante cambia de modelo? ¿Tengo que volver a aprender
  a usarlo?
- ¿Pueden compartir la máquina distintos usuarios?
- Pero los recursos son limitados. ¿Cómo podemos compartirlos?
- ¿Y si más de uno quiere el mismo recurso a la vez?
- ¿Cómo podemos proporcionar privacidad a cada usuario?
- ¿Pueden los demás usuarios compartir mis datos?
- ¿Podrán usar esta máquina los usuarios sin conocimientos técnicos?

#### ¿Qué quiere el usuario?

#### Uso de abstracciones

### El sistema operativo

#### Algunas definiciones

- S. Sánchez: un sistema operativo es un conjunto de programas que,
  mediante abstracciones, ponen el hardware del computador a disposición
  del usuario de forma segura
- H. Deitel: un sistema operativo es un programa que hace de interfaz
  entre el usuario y el hardware del computador, ofreciendo un
  entorno cómodo para la ejecución de programas
- H. Katzan: un sistema operativo es un conjunto de programas y datos que
  ayudan a crear otros programas y a controlar su ejecución
- Madnik y Donovan: un sistema operativo es un conjunto de programas que
  gestionan los recursos del sistema, optimizan su uso y resuelven
  conflictos

## Los sistemas operativos en la Ingeniería de Computadores / Informática

### Arquitectura de computadores: conceptos básicos

#### Visión general

- CPU: MEM: E/S

BUSES

Arquitectura de Computadores

Compiladores Sistemas Operativos

CLang/LLVM

#### Definición y bloques básicos

**Arquitectura**: comprende los atributos de un sistema que son visibles para el
programador y que controlan la ejecución de un programa.

- CPU: MEM: E/S

**Bloques básicos**

BUSES

- Memoria
- CPU
- Buses
- Entrada / Salida

#### Memoria (1/3)

Características

- Permite almacenar datos y código en el computador.
- Es una gran tabla con celdas numeradas que contienen datos.
- El número de celdas determina el tamaño de la memoria.
- El tamaño de la celda puede variar de un diseño
  a otro.
- Los programas deben cargarse en memoria para poder ejecutarse.

#### Memoria (2/3)

Una memoria de 65536 celdas de 8 bits cada una.

*(diagrama de memoria — la extracción del PDF entremezcló las columnas de direcciones/datos de la tabla y las etiquetas "Address bus" / "Data bus" / "16 lines / 16 bits" / "8 lines / 8 bits" / "Write / Read" que la rodean; el contenido literal que sobrevivió es:)*

```
0 1 2: 3 4 5 6: 7 8 9 A: B C D E F
0x000: 01 1A 03: 1E 33 DF 25: 24 7C 3D 3A: 2D 12 00 12 19
0x001: 1C 1D D1: E3 23 3D A3: 23 83 4A 3B: F1 00 08 1F 20
0x002: 21 2D F1: F2 27 4C BB: F1 21 3F 4C: 11 00 1A 1A 21
0x003: 23 3F73 E2: FE AA 2F CC: 2A A0 FD C1: 03 03 10 13 57
…………………………….……………………
0xFFC: 1E DE 34: E2 23 DF 25: 74 71 2D 0A: 21 81 30 10 1B
0xFFD 1D DD 12 E7 33 30 B4 77 03 40 0B C1 80 38 00 2B
0xFFE: 23 BD E1: F0 47 42 CC: F1 22 20 0C: D1 00 88 02 11
0xFFF: 2A 33 E2: E1 5A 00 00: 01 02 03 04: 05 06 07 08 09
```

*(la siguiente parte de la diapositiva — un diagrama de una instrucción `MOV BR8, [0x0023]` accediendo a memoria a través del bus de direcciones, con el efecto de "doblado de caracteres" típico de resaltados en negrita del PDF original — no se pudo reconstruir con fiabilidad; se deja el texto extraído tal cual)*

```
Ad00dxxr00e00s23s31 bus
CPU
MMOOVVBBRR88,, 00xx00002233
Memoria
IINNCCBBRR88 R8 (8 bits)
00000xxxxx0FFFF02233 - WriWRteer /ai tRdeead
MMOOVVBB 00xx00003311,, RR88
Bus00 dxxeFF d23atos
```

#### Memoria (3/3)

Una memoria de 65536 celdas de 8 bits cada una.

Bus de direcciones

```
0 1 2: 3 4 5: 6 7: 8 9 A: B C D E F: Data bus
…………………………….……………………
16 lines / 16 bits
0x002: 21 2D F1: F2 27 4C: BB F1: 21 3F 4C: 11 00 1A 1A 21
…………………………….…………………… - 16 lines / 16 bits
```

Escritura / Lectura

- 0x0023
- CPU - Memoria

Lectura

`MOV R16, [0x0024]`

- 0x274C
- Big-endian - Little-endian
- Memoria - Memoria
- 0x0024 0x0025: R16 (16 bits): 0x0024: 0x0025: R16 (16 bits)
- 27 4C: 0x274C: 27: 4C: 0x4C27
- MSB LSB: LSB: MSB

#### Unidad Central de Proceso (CPU) — Descripción general

- CPU = procesador = microprocesador
- Dos bloques principales:
  - ALU (Unidad Aritmético-Lógica): realiza operaciones aritméticas
    (suma, resta, etc.) y lógicas bit a bit (AND, OR, etc.)
  - Unidad de Control: decodifica las instrucciones y secuencia
    las acciones necesarias para ejecutarlas.
- La CPU controla todos los demás componentes del sistema y
  ejecuta las instrucciones del programa.

#### Unidad Central de Proceso (CPU) — Modelo de programación

El modelo de programación incluye todos los recursos que la CPU
ofrece al programador para controlar el sistema

- Elementos de almacenamiento: registros generales, contador de programa, registros
  de estado, punteros de pila, mapas de memoria y de E/S, etc.
- Juegos de instrucciones y modos de direccionamiento.

#### Unidad Central de Proceso (CPU) — Registros

Los registros son los elementos de almacenamiento más pequeños y básicos (también
los más rápidos y caros)

- Registros de propósito general
- Registros de datos
- Registros de direcciones
- Puntero de pila o SP (Stack Pointer): registro que apunta a la cima de una
  estructura de pila (operaciones push y pop)
- Registros de estado y de control

#### Unidad Central de Proceso (CPU) — El puntero de pila

Memoria de 65536 bytes.

*(diagrama de la pila mostrando el efecto de `PUSH`/`POP` sobre el Stack Pointer, con el mismo "doblado de caracteres" que en la sección de Memoria; el contenido extraído es:)*

```
CPU
- SP (16 bits) - R8 (8 bits)
0x3FFA 00
00000xxxxx33333FFFFFFFFFFFEEDD: 000xxxB11E22: 0x3FFB 02
SP
0x3FFC 08
SP
0x3FFD 00
SP
0x3FFE 011222
0x3FFF B0BE8E
0x4000 34
PPUUSSHHBBRR88 - 0x4001 A5
PPUUSSHHBB 00xx1122
PPOOPPBBRR88 - ….
```

#### Unidad Central de Proceso (CPU) — Registros de control

Los registros de control determinan el comportamiento de la CPU:

- Puntero de instrucción o contador de programa (IP o PC): mantiene
  la posición en memoria de la siguiente instrucción.
- Palabra de estado del programa (PSW, Program Status Word): señala mediante indicadores (flags) distintos eventos
  relacionados con la ejecución de instrucciones (acarreo, desbordamiento, cero)

#### El modelo de programación — Juego de instrucciones

- Una instrucción máquina es una secuencia de bits que representa una
  operación a realizar y la ubicación de los datos necesarios para
  llevarla a cabo
- A las instrucciones máquina (también llamadas códigos máquina) se les asigna un
  mnemónico para que sean más fáciles de recordar
- Las instrucciones pueden necesitar un número variable de operandos
- No todo el mundo puede ejecutar todas las instrucciones. Hay
  instrucciones privilegiadas
- El juego de instrucciones define qué operaciones pueden hacerse con
  la CPU (¿puede tu pequeña CPU sumar dos enteros pequeños, y números en coma flotante,
  y vectores, y matrices?)

#### El modelo de programación — Tipos de instrucciones

- Aritméticas - Lógicas bit a bit
- ADD: SUB: MUL: AND: OR: NOT
- suma: resta: multiplicación: Y lógico: O lógico: negación
- Transferencia de datos - Control de flujo
- MOV: PUSH: POP: CALL: RET
- mover: salto a subrutina: retorno de subrutina

JMP JNE

- Salto incondicional - Salto si no igual

#### Modelo de programación — Modos de direccionamiento

Cómo encuentra la CPU los operandos que necesita al ejecutar una instrucción.

Modos distintos:

- Implícito: el operando puede deducirse del código de operación
- Explícito:
  - Inmediato: el operando está en memoria, a continuación del
    código de operación.
  - Directo: a continuación del código de operación está la dirección del
    operando en memoria.
  - Otros: indexado, registro, etc.

#### Unidad Central de Proceso — El ciclo de ejecución de instrucciones

Ciclo de ejecución:

- Búsqueda del código de operación
- Decodificación de la instrucción
- Búsqueda de operandos (si es necesario)
- Ejecución de la instrucción
- Escritura de los resultados

#### Buses — Descripción general

- Interconectan entre sí los distintos componentes del
  sistema
- Al principio eran simples componentes pasivos (cables), pero
  hoy en día se han vuelto realmente complejos (chipset)
- Un bus se caracteriza por:
  - Sus conectores y elementos físicos.
  - Su topología (estrella, paralelo, serie, malla, . . . )
  - Sus señales y protocolos.

*(diagrama de un bus conectando tres elementos, con las señales Data bus / Address bus / Address Valid / Control bus / Read; el layout exacto no se pudo recuperar de la extracción OCR)*

```
Element 1 Element 2
0x0023
Data bus
Address Valid
Address bus
Read
Control bus
0xF2
Element 3
```

#### Entrada / Salida — Objetivos y descripción general

Objetivo: comunicarse con el mundo exterior para…

- Obtener los programas que se van a ejecutar (y almacenarlos en memoria)
- Obtener los datos que necesitan los programas durante su ejecución
- Obtener datos y órdenes del usuario y de otras máquinas

Características:

- Los dispositivos son distintos entre sí.
- Todos ellos deben comunicarse con la CPU (a través de los buses).
- Solución: definir una arquitectura común para comunicarse con los
  dispositivos (controlador)

#### Entrada / Salida — Arquitectura de los dispositivos: el controlador

- Son elementos hardware
- Se conectan a los buses del computador y ofrecen distintos
  registros:
  - Registro de datos
  - Registro de control
  - Registro de estado
- Puede haber otros registros según el dispositivo (por ejemplo,
  el framebuffer)

#### Entrada / Salida — Técnicas

- Los dispositivos pueden necesitar atención inmediata (por ejemplo, un sensor de colisión)
- Dos enfoques:
  - Hacer que la CPU pregunte al dispositivo si necesita atención:
    - ¿Con qué frecuencia habría que "preguntar"?
    - Carga de trabajo adicional para la CPU. Uso innecesario del bus.
    - Mecanismo sencillo, sin hardware adicional.
  - Hacer que el dispositivo interrumpa a la CPU cuando sea necesario
    - Hace falta hardware adicional
    - Hace falta una CPU que pueda ser interrumpida

#### Entrada / Salida — Mecanismo de interrupción

1. La CPU está ejecutando un código
2. Un dispositivo necesita intervención y envía una interrupción a la CPU
3. La CPU deja de ejecutar ese código y salta a ejecutar otro
   distinto, llamado rutina de servicio de interrupción (ISR, Interrupt Service Routine)
4. La ISR es un código muy especializado que atiende al dispositivo
5. La CPU reanuda la ejecución del programa en el mismo punto en que
   fue interrumpida

## Evolución histórica

### El modelo de máquina desnuda

Objetivo: ejecutar programas almacenados en memoria.

- Se programa directamente sobre el hardware
- No existe ningún software parecido a un sistema operativo
- Problemas:
  - Los programadores necesitaban un conocimiento profundo del hardware
  - Pequeños cambios en el hardware provocaban grandes cambios en el
    software
  - La funcionalidad común no puede reutilizarse

### Monitor residente simple

Objetivo: reutilizar código y funcionalidad común entre diseños.

- El software común se trasladó a un monitor residente
  (siempre en memoria)
  - Este monitor es el origen del sistema operativo.
  - Incluye principalmente servicios de E/S.
  - El monitor gestiona la E/S (es un driver)
- El programador ya no tiene que programar el hardware a bajo nivel. Ahora
  puede centrarse en cosas más importantes
- Es posible cambiar el hardware sin afectar al software:
  solo hay que actualizar el monitor.
- Problema: se pierde demasiado tiempo cargando el siguiente programa del
  lote que se va a ejecutar

### Procesamiento de programas por lotes (sistemas batch)

Objetivo: reducir el tiempo de espera al cargar programas.

- La E/S deja de gestionarla la CPU principal. En su lugar, se introduce
  una CPU independiente (y más barata)
- La CPU principal (y cara) no se ocupa de cargar programas;
  solo se dedica a ejecutarlos

**Ciclo de operación**:

- El operador introduce las tarjetas perforadas en un computador de bajo coste.
- Se genera una cinta de instrucciones que luego se carga en el computador
  principal.
- El computador principal ejecuta el código de la cinta
- La ejecución genera una cinta de salida
- El operador introduce la cinta en un tercer computador que lee la
  cinta e imprime los resultados
- Problema: fuerte intervención de un operador humano

### Multiprogramación

**Propósito y requisitos hardware**

Objetivo: solapar la E/S con la ejecución en la CPU, un primer paso hacia los sistemas
interactivos.

- Un gran salto en complejidad: tener más de un programa cargado en
  memoria al mismo tiempo
- Mientras se carga un programa nuevo, se ejecuta otro programa ya
  cargado en memoria
- Esto trae nuevas necesidades hardware:
  - Mecanismo de interrupciones
  - Acceso directo a memoria (DMA)

**Requisitos del sistema operativo**

- Aquí es donde surgen casi todos los problemas clásicos de los sistemas
  operativos:
  - Gestión de memoria
  - Planificación de la CPU
  - Planificación de la E/S
  - Seguridad y protección de los procesos. Control de la
    concurrencia
- Problemas:
  - Un programa en ejecución puede monopolizar la CPU
  - No es adecuado para sistemas interactivos

### Sistemas de tiempo compartido

Objetivo: garantizar un uso equitativo de la CPU.

- Protección frente a la monopolización de la CPU: interrupciones.
- El tiempo de ejecución de un proceso se divide en intervalos llamados quantum.
- Si un proceso intenta ejecutarse durante más tiempo que el quantum, el sistema
  operativo asigna la CPU a otro proceso, de modo que los demás procesos tienen
  la oportunidad de ejecutarse por turno rotatorio (round robin).
- Estos sistemas operativos de tiempo compartido son muy habituales hoy en día
  en los computadores de consumo.

### Sistemas de tiempo real

**Conceptos y características**

Objetivo: garantizar que los procesos se ejecutan dentro de una restricción
de tiempo dada.

- Cumplir las restricciones de tiempo real (RT) no es una cuestión de potencia
  del computador ni de velocidad de procesamiento
- Tiempo real no es sinónimo de rápido, sino de "a tiempo"
- Este comportamiento temporal es habitual en los sistemas empotrados.
- Hay dos tipos de aplicaciones de tiempo real
  - Aplicaciones de tiempo real estricto (Hard Real-Time).
  - Aplicaciones de tiempo real no estricto (Soft Real-Time).

## Bibliografía

- Sebastián Sánchez. Operating Systems. Second Edition.
  Universidad de Alcalá - Servicio de Publicaciones, 2005
- A. S. Tanenbaum. Modern Operating Systems. 3rd Edition.
  Prentice Hall, 2009
- William Stallings. Computer organization and architecture.
  10th Edition. Pearson, 2015

---

© Pablo Parra, Óscar García. Departamento de Automática. Universidad de Alcalá.
Este documento se distribuye bajo los términos de la licencia Creative Commons Reconocimiento-CompartirIgual 4.0 (internacional)
(Attribution ShareAlike 4.0): https://creativecommons.org/licenses/by-sa/4.0/
