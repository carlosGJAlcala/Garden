---
title: "Arquitectura de computadores - Fundamentos"
---

# AICC Capítulo 2: Arquitectura

*Bibliografía básica:*

- "Digital Design and Computer Architecture, RISC-V Edition, First Edition", Sarah Harris y David Harris, Morgan Kaufmann 2021. Capítulo 6.
- "Organización y Diseño Informático. Edición RISC-V", David A. Patterson, John Hennessy. Segunda edición, Morgan-Kaufman 2021. Capítulo 2.

## Capítulo 2: Temas

- Introducción
- Lenguaje ensamblador
- Programación
- Lenguaje de máquina
- Modos de direccionamiento
- Luces, cámara, acción: compilación, ensamblaje y carga
- Más..

## Introducción

- Saltando unos cuantos niveles de abstracción
- Arquitectura: vista del programador de la computadora
  - Definido por instrucciones y ubicaciones de operandos
- Microarquitectura: cómo implementar una arquitectura en hardware (cubierto en el Tema 3)

## Lenguaje ensamblador

- Instrucciones: comandos en un lenguaje de computadora
  - Lenguaje ensamblador: formato de instrucciones legible por humanos
  - Lenguaje de máquina: formato legible por computadora (1 y 0)
- Arquitectura RISC-V:
  - Desarrollado por Krste Asanovic, David Patterson y sus colegas en UC Berkeley en 2010.
  - Primera arquitectura informática de código abierto ampliamente aceptada

Una vez que haya aprendido una arquitectura, es más fácil aprender otras.

### Kriste Asanovic

- Profesor de Ciencias de la Computación en la Universidad de California, Berkeley
- Desarrolló RISC-V durante un verano
- Presidente del Patronato de la Fundación RISC-V
- Co-Fundador de SiFive, una empresa que comercializa y desarrolla herramientas de soporte para RISC-V

### David Patterson

- Profesor de Ciencias de la Computación en la Universidad de California, Berkeley desde 1976
- Coinventó la computadora con conjunto de instrucciones reducido (RISC) con John Hennessy en la década de 1980.
- Miembro fundador del equipo RISC-V.
- Recibió el Premio Turing (con John Hennessy) por ser pionero en un enfoque cuantitativo para el diseño y evaluación de arquitecturas informáticas.

### J. Hennessy

- Presidente de la Universidad de Stanford de 2000 a 2016.
- Profesor de Ingeniería Eléctrica y Ciencias de la Computación en Stanford desde 1977
- Coinventó la computadora con conjunto de instrucciones reducido (RISC) con David Patterson en la década de 1980.
- Recibió el Premio Turing (con David Patterson) por ser pionero en un enfoque cuantitativo para el diseño y evaluación de arquitecturas informáticas.

### Principios de diseño de arquitectura

Principios de diseño subyacentes, según lo articulado por Hennessy y Patterson:

1. La sencillez favorece la regularidad
2. Hacer el caso común rápido
3. Más pequeño es más rápido
4. Un buen diseño exige buenos compromisos

## Instrucciones

### Conjunto de instrucciones

- El repertorio de instrucciones de una computadora.
- Diferentes computadoras tienen diferentes conjuntos de instrucciones
  - Pero con muchos aspectos en común.
- Las primeras computadoras tenían conjuntos de instrucciones muy simples
  - Implementación simplificada
- Muchas computadoras modernas también tienen conjuntos de instrucciones simples

### Conjunto de instrucciones: principios de diseño

#### 1. La sencillez favorece la regularidad

- Formato de instrucción consistente
- Mismo número de operandos (dos fuentes y un destino)
- Más fácil de codificar y manejar en hardware

#### 2. Hacer el caso común rápido

- RISC-V incluye solo instrucciones simples y de uso común
- El hardware para decodificar y ejecutar instrucciones puede ser simple, pequeño y rápido
- Instrucciones más complejas (que son menos comunes) ejecutadas usando múltiples instrucciones simples
- RISC-V es una computadora con conjunto de instrucciones reducido (RISC), con una pequeña cantidad de instrucciones simples
- Otras arquitecturas, como la x86 de Intel, son computadoras con conjunto de instrucciones complejas (CISC)

#### 3. Más pequeño es más rápido

- RISC-V incluye solo una pequeña cantidad de registros

#### 4. Un buen diseño exige buenos compromisos

### Conjunto de instrucciones RISC-V

*Guía Práctica de RISC-V: El Atlas de una Arquitectura Abierta (riscbook.com)*

- Usado como ejemplo a lo largo del libro.
- Desarrollado en UC Berkeley como ISA abierta
- Ahora gestionado por la Fundación RISC-V (riscv.org)
- Típico de muchas ISA modernas
  - Consulte la tarjeta extraíble de datos de referencia de RISC-V
- Las ISA similares tienen una gran participación en el mercado central integrado
  - Aplicaciones en electrónica de consumo, equipos de red/almacenamiento, cámaras, impresoras,...

### Instrucciones: suma

**Código C:** `a = b + c;` → **código ensamblador RISC-V:** `add a, b, c`

- **add**: mnemotécnico, indica la operación a realizar.
- **b, c**: operandos fuente (sobre los que se realiza la operación).
- **a**: operando de destino (al que se le asigna el resultado, una vez realizado).

### Instrucciones: Resta

Similar a la suma: solo cambios mnemotécnicos.

**Código C:** `a = b - c;` → **código ensamblador RISC-V:** `sub a, b, c`

- **sub**: mnemotécnico
- **b, c**: operandos fuente
- **a**: operando de destino

### Principio de diseño 1: La sencillez favorece la regularidad

- Formato de instrucción consistente
- Mismo número de operandos (dos fuentes y un destino)
- Más fácil de codificar y manejar en hardware

### Instrucciones múltiples

El código más complejo es manejado por múltiples instrucciones RISC-V.

**Código C:**
```c
a = b + c - d;
```

**Código ensamblador RISC-V:**
```asm
add t, b, c   # t = b + c
sub a, t, d   # a = t - d
```

### Principio de diseño 2: Hacer el caso común rápido

- RISC-V incluye solo instrucciones simples y de uso común
- El hardware para decodificar y ejecutar instrucciones puede ser simple, pequeño y rápido
- Instrucciones más complejas (que son menos comunes) ejecutadas usando múltiples instrucciones simples
- RISC-V es una computadora con conjunto de instrucciones reducido (RISC), con una pequeña cantidad de instrucciones simples
- Otras arquitecturas, como la x86 de Intel, son computadoras con conjunto de instrucciones complejas (CISC)

## Operandos

### Ubicación del operando

- Ubicación del operando: ubicación física en la computadora
  - Registros
  - Memoria
  - Constantes (también llamadas inmediatas)

### Operandos: Registros

- RISC-V tiene 32 registros de 32 bits
- Los registros son más rápidos que la memoria.
- RISC-V llamado "arquitectura de 32 bits" porque opera con datos de 32 bits

### Principio de diseño 3: Más pequeño es más rápido

- RISC-V incluye solo una pequeña cantidad de registros

### Conjunto de registros RISC-V

| Número de registro | Nombre | Uso |
| --- | --- | --- |
| x0 | zero | Valor constante 0 |
| x1 | ra | Dirección del retorno |
| x2 | sp | Puntero de pila |
| x3 | gp | Puntero global |
| x4 | tp | Puntero de hilo |
| x5-7 | t0-2 | Temporales |
| x8 | s0/fp | Registro para salvado / Puntero de marco |
| x9 | s1 | registro salvados |
| x10-11 | a0-1 | Argumentos de función/valores devueltos |
| x12-17 | a2-7 | Argumentos de función |
| x18-27 | s2-11 | Registros slavados |
| x28-31 | t3-6 | Temporales |

### Registros x86 básicos

*Diagrama de la diapositiva: esquema comparativo de los registros básicos de la arquitectura x86 (EAX, EBX, ECX, EDX, ESI, EDI, EBP, ESP, etc.). El layout original no se pudo recuperar de la extracción OCR.*

### Operandos: Registros (continuación)

- Registros:
  - Puede usar cualquier nombre (es decir, ra, zero) o bien x0, x1, etc.
  - Se prefiere usar el nombre.
- Registros utilizados para fines específicos:
  - cero: siempre tiene el valor constante 0.
  - los registros guardados (s0-s11), utilizados para contener variables
  - los registros temporales (t0-t6), utilizados para contener valores intermedios durante un cómputo mayor
  - Discutir otros más tarde

### Instrucciones con Registros

- Revisar instrucción suma

**Código C:** `a = b + c;`

**Código ensamblador RISC-V:**
```asm
# s0 = a, s1 = b, s2 = c
add s0, s1, s2
```

### Instrucciones con constantes

- instrucción add inmediato: addi

| Código C | código ensamblador RISC-V |
| --- | --- |
| a = b + 6; | addi s0, s1, 6 |

### Ejemplo de registros con operandos

- Código C: `f = (g + h) - (i + j);`
  - f, …, j en x19, x20, …, x23
- Código RISC-V compilado:

```asm
add x5, x20, x21
add x6, x22, x23
sub x19, x5, x6
```

## Operandos de memoria

### Operandos: Memoria

- Demasiados datos para entrar en solo 32 registros
- Almacenar más datos en la memoria
- La memoria es grande, pero lenta
- Variables de uso común mantenidas en registros

### Memoria

- Primero, discutiremos la memoria direccionable por palabras
- Luego hablaremos de la memoria direccionable por bytes

RISC-V es direccionable por bytes.

### Memoria direccionable por palabra

Cada palabra de datos de 32 bits tiene una dirección única.

| Dirección de palabra | Datos | Número de palabra |
| --- | --- | --- |
| 00000004 | CD19A65B | Word 4 |
| 00000003 | 40F30788 | Word 3 |
| 00000002 | 01EE2842 | Word 2 |
| 00000001 | F2F1AC07 | Word 1 |
| 00000000 | ABCDEF78 | Word 0 |

*width = 4 bytes*

RISC-V usa memoria direccionable por bytes, de la que hablaremos a continuación.

### Lectura de memoria direccionable por palabras

*(Frase de la diapositiva parcialmente ilegible por mezcla de caracteres en la extracción OCR — por el contexto, se refiere a que la operación de leer de la memoria se llama "carga".)*

- Mnemotécnico: cargar palabra (lw)
- Formato:
```asm
lw t1, 5(s0)
lw destino, desplazamiento(base)
```
- Cálculo de dirección:
  - agregue la dirección base (s0) al desplazamiento (5)
  - dirección = (s0 + 5)
- Resultado:
  - t1 contiene el valor de los datos en la dirección (s0 + 5)

Cualquier registro puede ser utilizado como dirección base.

### Lectura de memoria direccionable por palabras: ejemplo

- Ejemplo: leer una palabra de datos en la dirección de memoria 1 en s3
  - dirección = (0 + 1) = 1
  - s3 = 0xF2F1AC07 después de la carga

Código de montaje:
```asm
lw s3, 1(cero)   # lee la palabra de memoria 1 en s3
```

| Dirección de palabra | Datos | Número de palabra |
| --- | --- | --- |
| 00000004 | CD19A65B | Word 4 |
| 00000003 | 40F30788 | Word 3 |
| 00000002 | 01EE2842 | Word 2 |
| 00000001 | F2F1AC07 | Word 1 |
| 00000000 | ABCDEF78 | Word 0 |

### Escritura de memoria direccionable por palabras

- La escritura en memoria se llama store.
- Mnemotécnico: almacenar palabra (sw)

### Escritura de memoria direccionable por palabras: ejemplo

- Ejemplo: Escribir (almacenar) el valor en t4 en la dirección de memoria 3
  - agregue la dirección base (cero) al desplazamiento (0x3)
  - dirección: (0 + 0x3) = 3
  - por ejemplo, si t4 tiene el valor 0xFEEDCABB, luego de que se complete esta instrucción, la palabra 3 en la memoria contendrá ese valor

Código en ensamblador:
```asm
sw t4, 0x3(cero)   # escribir el valor en t4 a la palabra de memoria
```

*El desplazamiento se puede escribir en decimal (predeterminado) o hexadecimal.*

| Dirección de palabra | Datos | Número de palabra |
| --- | --- | --- |
| 00000004 | CD19A65B | Word 4 |
| 00000003 | 4F0EFE3DC0A7B8B8 (ver nota) | Word 3 |
| 00000002 | 0011EEEE228844 22 (ver nota) | Word 2 |
| 00000001 | FF22FF11AACC0077 (ver nota) | Word 1 |
| 00000000 | AABBCCDDEEFF7788 (ver nota) | Word 0 |

*Nota: en esta diapositiva la extracción OCR duplica cada dígito hexadecimal (p. ej. "cc dd 11" en vez de "cd1"), un artefacto de renderizado de texto en negrita superpuesto. Los valores de arriba se han normalizado tomando un dígito de cada par repetido; dado el patrón irregular de esta tabla en concreto, tómense como referencia aproximada y no como transcripción bit a bit certera.*

### Memoria direccionable por bytes

- Cada byte de datos tiene una dirección única
- Cargar/almacenar palabras o bytes individuales: byte de carga (lb) y byte de almacenamiento (sb)
- palabra de 32 bits = 4 bytes, por lo que la dirección de la palabra se incrementa en 4

| Dirección de byte | Dirección de palabra | Datos | Número de palabra |
| --- | --- | --- | --- |
| 13-10 | 00000010 | CD19A65B | Word 4 |
| F-C | 0000000C | 40F30788 | Word 3 |
| B-8 | 00000008 | 01EE2842 | Word 2 |
| 7-4 | 00000004 | F2F1AC07 | Word 1 |
| 3-0 | 00000000 | ABCDEF78 | Word 0 |

*width = 4 bytes (MSB a la izquierda, LSB a la derecha en cada palabra)*

### Lectura de memoria direccionable por bytes

- La dirección de una palabra de memoria ahora debe multiplicarse por 4. Por ejemplo:
  - la dirección de la palabra de memoria 2 es 2 × 4 = 8
  - la dirección de la palabra de memoria 10 es 10 × 4 = 40 (0x28)
- RISC-V está direccionado por bytes, no por palabras

### Lectura de memoria direccionable por bytes: ejemplo

- Ejemplo: Cargue una palabra de datos en la dirección de memoria 8 en s3.
  - s3 mantiene el valor 0x01EE2842 después de la carga

Código ensamblador RISC-V:
```asm
lw s3, 8(cero)   # lee la palabra en la dirección 8 en s3
```

| Dirección de byte | Dirección de palabra | Datos | Número de palabra |
| --- | --- | --- | --- |
| 13-10 | 00000010 | CD19A65B | Word 4 |
| F-C | 0000000C | 40F30788 | Word 3 |
| B-8 | 00000008 | 01EE2842 | Word 2 |
| 7-4 | 00000004 | F2F1AC07 | Word 1 |
| 3-0 | 00000000 | ABCDEF78 | Word 0 |

### Escritura de memoria direccionable por bytes

- Ejemplo: almacenar el valor retenido en t7 en la dirección de memoria 0x10 (16)
  - si t7 tiene el valor 0xAABBCCDD, luego de que se complete el sw, la palabra 4 (en la dirección 0x10) en la memoria contendrá ese valor

Código ensamblador RISC-V:
```asm
sw t7, 0x10(cero)   # escribe t7 en la dirección 16
```

| Dirección de byte | Dirección de palabra | Datos (después de la escritura) | Número de palabra |
| --- | --- | --- | --- |
| 13-10 | 00000010 | AABBCCDD *(actualizado, antes CD19A65B)* | Word 4 |
| F-C | 0000000C | 40F30788 | Word 3 |
| B-8 | 00000008 | 01EE2842 | Word 2 |
| 7-4 | 00000004 | F2F1AC07 | Word 1 |
| 3-0 | 00000000 | ABCDEF78 | Word 0 |

*width = 4 bytes*

### Ejemplo de Operando de Memoria

- Código C: `A[12] = h + A[8];`
  - h en x21, dirección base de A en x22
- Código RISC-V compilado:
  - El índice 8 requiere una compensación de 64 (8 bytes por palabra doble)

```asm
ld x9, 64(x22)
add x9, x21, x9
sd x9, 96(x22)
```

### Registros vs Memoria

- Los registros son más rápidos de acceder que la memoria
- Operar en datos de memoria requiere cargas y almacenamientos
  - Más instrucciones para ejecutar
- El compilador debe usar registros para variables tanto como sea posible
  - Solo descargue en la memoria las variables que se usan con menos frecuencia
  - ¡La optimización del registro es importante!

## Generación de constantes

### Operandos inmediatos

- Datos constantes especificados en una instrucción

```asm
addi x22, x22, 4
```

- Hacer el caso común rápido
  - Las constantes pequeñas son comunes
  - El operando inmediato evita una instrucción de carga

### Generación de constantes de 12 bits

- Constantes con signo de 12 bits (inmediatas) con addi:

| Código C | código ensamblador RISC-V |
| --- | --- |
| // int es una palabra con signo de 32 bits | # s0 = a, s1 = b |
| int a = -372; | addi s0, zero, -372 |
| int b = a + 6; | addi s1, s0, 6 |

Cualquier inmediato que necesite más de 12 bits no puede usar este método.

### Generación de constantes de 32 bits

- Usar carga superior inmediata (lui) y addi
- lui: pone un inmediato en los 20 bits superiores del registro de destino y 0 en los 12 bits inferiores

| Código C | código ensamblador RISC-V |
| --- | --- |
| int a = 0xFEDC8765; | lui s0, 0xFEDC8 |
| | addi s0, s0, 0x765 |

Recuerda que addi hace extensión de signo sobre el valor inmediato de 12 bits.

### Generación de constantes de 32 bits (cont.)

- Si el bit 11 de la constante de 32 bits es 1, incremente los 20 bits superiores en 1 en lui

*Nota: -341 = 0xEAB*

Código C: `int a = 0xFEDC8EAB;`

Código ensamblador RISC-V:
```asm
lui s0, 0xFEDC9      # s0 = 0xFEDC9000
addi s0, s0, -341    # s0 = 0xFEDC9000 + 0xFFFFFEAB
```

## Instrucciones lógicas y de desplazamiento

### Programación

- Lenguajes de alto nivel:
  - por ejemplo, C, Java, Python
  - Escrito en un nivel más alto de abstracción.
- Construcciones de alto nivel: bucles, declaraciones condicionales, matrices, llamadas a funciones
- Primero, introduzca instrucciones que admitan lo siguiente:
  - Operaciones lógicas
  - Instrucciones de desplazamiento
  - Multiplicación y división
  - Saltos

### Ada Lovelace, 1815-1852

- Escribió el primer programa de computadora.
- Su programa calculó los números de Bernoulli en el motor analítico de Charles Babbage.
- Ella era la hija del poeta Lord Byron

### Instrucciones lógicas

Instrucciones para la manipulación bit a bit.

| Operación | C | Java | RISC-V |
| --- | --- | --- | --- |
| Shift left | << | << | slli |
| Shift right | >> | >>> | srli |
| Bit-a-bit AND | & | & | and, andi |
| Bit-a-bit OR | \| | \| | or, ori |
| Bit-a-bit XOR | ^ | ^ | xor, xori |
| Bit-a-bit NOT | ~ | ~ | (pseudoinstrucción, ver más adelante) |

Útil para extraer e insertar grupos de bits en una palabra.

### Instrucciones lógicas: uso

- and: útil para máscara de bits
  - Enmascarar todo menos el byte menos significativo de un valor: `0xF234012F Y 0x000000FF = 0x0000002F`
- or: útil para combinar campos de bits
  - Combine 0xF2340000 con 0x000012BC: `0xF2340000 O 0x000012BC = 0xF23412BC`
- xor: útil para invertir bits
  - A XOR -1 = NOT A (recuerda que -1 = 0xFFFFFFFF)

### Instrucciones Lógicas: Ejemplo 1

Source Registers:

| Registro | Valor |
| --- | --- |
| s1 | 0100 0110 1010 0001 1111 0001 1011 0111 |
| s2 | 1111 1111 1111 1111 0000 0000 0000 0000 |

Assembly Code Result:

| Código ensamblador | Resultado |
| --- | --- |
| and s3, s1, s2 | s3 = 0100 0110 1010 0001 0000 0000 0000 0000 |
| or s4, s1, s2 | s4 = 1111 1111 1111 1111 1111 0001 1011 0111 |
| xor s5, s1, s2 | s5 = 1011 1001 0101 1110 1111 0001 1011 0111 |

### Instrucciones Lógicas: Ejemplo 2

Source Values:

| Registro | Valor |
| --- | --- |
| t3 | 0011 1010 0111 0101 0000 1101 0110 1111 |
| imm sign-extended | 1111 1111 1111 1111 1111 1010 0011 0100 |

Assembly Code Result:

| Código ensamblador | Resultado |
| --- | --- |
| andi s5, t3, -1484 | s5 = 0011 1010 0111 0101 0000 1000 0010 0100 |
| ori s6, t3, -1484 | s6 = 1111 1111 1111 1111 1111 1111 0111 1111 |
| xori s7, t3, -1484 | s7 = 1100 0101 1000 1010 1111 0111 0101 1011 |

*-1484 = 0xA34 en representación de 12 bits complemento a 2.*

### Instrucciones de desplazamiento

La cantidad de desplazamiento está en (los 5 bits inferiores de) un registro.

- sll: desplazamiento lógico a la izquierda
  - Ejemplo: `sll t0, t1, t2   # t0 = t1 << t2`
- srl: desplazamiento lógico a la derecha
  - Ejemplo: `srl t0, t1, t2   # t0 = t1 >> t2`
- sra: desplazamiento aritmético a la derecha
  - Ejemplo: `sra t0, t1, t2   # t0 = t1 >>> t2`

### Instrucciones de desplazamiento inmediato

La cantidad de desplazamiento es inmediata, entre 0 y 31.

- slli: desplazamiento a la izquierda lógico inmediato
  - Ejemplo: `slli t0, t1, 23   # t0 = t1 << 23`
- srli: desplazamiento a la derecha lógico inmediato
  - Ejemplo: `srli t0, t1, 18   # t0 = t1 >> 18`
- srai: desplazamiento aritmético inmediato a la derecha
  - Ejemplo: `srai t0, t1, 5   # t0 = t1 >>> 5`

## Multiplicación y división

### Multiplicación

32 × 32 multiplicación: resultado de 64 bits.

- `mul s3, s1, s2` → s3 = 32 bits inferiores del resultado
- `mulh s4, s1, s2` → s4 = 32 bits superiores del resultado, trata los operandos como firmados (con signo)

Concatenación: {s4, s3} = s1 × s2

Ejemplo: s1 = 0x40000000 (= 2^30); s2 = 0x80000000 (= -2^31)

```
s1 × s2 = -2^61 = 0xE0000000_00000000
s4 = 0xE0000000; s3 = 0x00000000
```

### División

División de 32 bits: cociente y resto de 32 bits.

- `div s3, s1, s2   # s3 = s1/s2`
- `rem s4, s1, s2   # s4 = s1%s2`

Ejemplo: s1 = 0x00000011 (=17); s2 = 0x00000003 (=3)

```
s1 / s2 = 5
s1 % s2 = 2
s3 = 0x00000005; s4 = 0x00000002
```

## Ramificaciones y saltos

### Derivación

- Ejecutar instrucciones fuera de secuencia
- Tipos de saltos:
  - Condicional
    - salta si es igual (beq)
    - salta si no es igual (bne)
    - salta si es menor que (blt)
    - salta si es mayor o igual (bge)
  - Incondicional
    - saltar (j)
    - salto por registro (jr)
    - saltar y enlazar (jal) — hablaremos de esto cuando discutamos las llamadas a funciones.
    - salto por registro y enlace (jalr)

### Ramificación condicional

```asm
addi s0, cero, 4      # s0 = 0 + 4 = 4
addi s1, cero, 1      # s1 = 0 + 1 = 1
slli s1, s1, 2        # s1 = 1 << 2 = 4
beq s0, s1, destino   # rama que se toma
addi s1, s1, 1        # no ejecutado
sub s1, s1, s0        # no ejecutado
destino:              # etiqueta
add s1, s1, s0        # s1 = 4 + 4 = 8
```

Etiquetas indican la ubicación de la instrucción. No pueden ser palabras reservadas y deben ir seguidas de dos puntos (:).

### La rama no tomada (bne)

```asm
addi s0, cero, 4         # s0 = 0 + 4 = 4
addi s1, cero, 1         # s1 = 0 + 1 = 1
slli s1, s1, 2           # s1 = 1 << 2 = 4
bne s0, s1, objetivo     # bifurcación no tomada
addi s1, s1, 1           # s1 = 4 + 1 = 5
sub s1, s1, s0           # s1 = 5 – 4 = 1
objetivo:
add s1, s1, s0           # s1 = 1 + 4 = 5
```

### Ramificación incondicional (j)

```asm
j target             # jump to target
srai s1, s1, 2        # not executed
addi s1, s1, 1        # not executed
sub s1, s1, s0        # not executed
target:
add s1, s1, s0        # s1 = 1 + 4 = 5
```

## Condiciones: declaraciones y bucles

### Declaraciones condicionales y bucles

- Declaraciones condicionales
  - Declaraciones if
  - Declaraciones if/else
- Bucles
  - Bucles while
  - Bucles for

### Declaración if

| Código C | código ensamblador RISC-V |
| --- | --- |
| if (i == j) | bne s3, s4, L1 |
| f = g + h; | add s0, s1, s2 |
| | L1: |
| f = f – i; | sub s0, s0, s3 |

¿Ensamblador del caso opuesto (i != j) del código de alto nivel (i == j)?

### Declaración if/else

| Código C | código ensamblador RISC-V |
| --- | --- |
| if (i == j) | bne s3, s4, L1 |
| f = g + h; | add s0, s1, s2 |
| else | j done |
| | L1: |
| f = f – i; | sub s0, s0, s3 |
| | done: |

¿Ensamblador del caso opuesto (i != j) del código de alto nivel (i == j)?

### Compilar sentencia If/Else

- Código C:

```c
si (i==j) f = g+h;
si no f = g-h;
```

  - f, g, … en x19, x20, …
- Código RISC-V compilado:

```asm
bne x22, x23, Else
add x19, x20, x21
beq x0, x0, Exit    // incondicional
Else: sub x19, x20, x21
Exit: …
```

Ensamblador calcula direcciones.

### Bucles while

**Código C:**

```c
// determine la potencia de x tal que 2^x = 128
int pow = 1;
int x = 0;
while (pow != 128) {
  pow = pow * 2;
  x = x + 1;
}
```

**Código ensamblador RISC-V:**

```asm
# s0 = pow, s1 = x
addi s0, zero, 1
add s1, zero, zero
addi t0, zero, 128
while:
  beq s0, t0, done
  slli s0, s0, 1
  addi s1, s1, 1
  j while
done:
```

Prueba el caso opuesto (pow == 128) del código de alto nivel (pow != 128).

### Bucles for

`for (inicialización; condición; operación de bucle) declaración`

- inicialización: se ejecuta antes de que comience el ciclo
- condición: se prueba al principio de cada iteración
- operación de bucle: se ejecuta al final de cada iteración
- sentencia: se ejecuta cada vez que se cumple la condición

### Bucles for: ejemplo

**Código C:**

```c
// suma los numeros del 0 al 9
int sum = 0;
int i;
for (i=0; i!=10; i = i+1) {
  sum = sum + i;
}
```

**Código ensamblador RISC-V:**

```asm
# s0 = i, s1 = sum
addi s1, zero, 0
add s0, zero, zero
addi t0, zero, 10
for:
  beq s0, t0, done
  add s1, s1, s0
  addi s0, s0, 1
  j for
done:
```

### La comparación menor que

**Código C:**

```c
// suma las potencias de 2 de 1 a 100
int sum = 0;
int i;
for (i=1; i < 101; i = i*2) {
  sum = sum + i;
}
```

**Código ensamblador RISC-V:**

```asm
# s0 = i, s1 = suma
addi s1, zero, 0
addi s0, zero, 1
addi t0, zero, 101
loop:
  bge s0, t0, done
  add s1, s1, s0
  slli s0, s0, 1
  j loop
done:
```

### Menor que: Versión 2

**Código C:** (igual que el ejemplo anterior)

**Código ensamblador RISC-V:**

```asm
# s0 = i, s1 = sum
addi s1, zero, 0
addi s0, zero, 1
addi t0, zero, 101
loop:
  slt t2, s0, t0
  beq t2, zero, done
  add s1, s1, s0
  slli s0, s0, 1
  j loop
done:
```

slt: establece si es menor que la instrucción — `slt t2, s0, t0   # si s0 < t0, t2 = 1`

### Con y sin signo

- Comparación con signo: blt, bge
- Comparación sin signo: bltu, bgeu
- Ejemplo:
  - x22 = 1111 1111 1111 1111 1111 1111 1111 1111
  - x23 = 0000 0000 0000 0000 0000 0000 0000 0001
  - x22 < x23 // con signo: –1 < +1
  - x22 > x23 // sin signo: +4.294.967.295 > +1

### Compilación de sentencias de bucle

- Código C: `while (save[i] == k) i += 1;`
  - i en x22, k en x24, dirección de guardado en x25
- Código RISC-V compilado:

```asm
Loop: slli x10, x22, 3
add x10, x10, x25
ld x9, 0(x10)
bne x9, x24, Exit
addi x22, x22, 1
beq x0, x0, Loop
Exit: …
```

### Bloques básicos

- Un bloque básico es una secuencia de instrucciones con:
  - Sin ramas incrustadas (excepto al final)
  - Sin objetivos de rama (excepto al principio)
- Un compilador identifica bloques básicos para la optimización.
- Un procesador avanzado puede acelerar la ejecución de bloques básicos.

### Más operaciones condicionales

- `blt rs1, rs2, L1` – if (rs1 < rs2) bifurca a la instrucción etiquetada como L1
- `bge rs1, rs2, L1` – if (rs1 >= rs2) salta a la instrucción etiquetada como L1
- Ejemplo:
  - si (a > b) a += 1;
  - a en x22, b en x23

```asm
bge x23, x22, Salir   // rama si b >= a
addi x22, x22, 1
Salir:
```

## Matrices

### Matrices

- Acceda a grandes cantidades de datos similares
- Índice: acceder a cada elemento
- Tamaño: número de elementos

### Matrices: ejemplo en memoria

- matriz de 5 elementos
- Dirección básica = 0x123B4780 (dirección del primer elemento, array[0])
- Primer paso para acceder a una matriz: cargar la dirección base en un registro

| Address | Data |
| --- | --- |
| 123B4790 | array[4] |
| 123B478C | array[3] |
| 123B4788 | array[2] |
| 123B4784 | array[1] |
| 123B4780 | array[0] |

*Main Memory*

### Accediendo a matrices

**Código C:**

```c
int array[5];
array[0] = array[0] * 2;
array[1] = array[1] * 2;
```

| Address | Data |
| --- | --- |
| 123B4790 | array[4] |
| 123B478C | array[3] |
| 123B4788 | array[2] |
| 123B4784 | array[1] |
| 123B4780 | array[0] |

*Main Memory*

```asm
lui  s0, 0x123B4          # 0x123B4 in upper 20 bits of s0
addi s0, s0, 0x780        # s0 = 0x123B4780
lw   t1, 0(s0)            # t1 = array[0]
slli t1, t1, 1            # t1 = t1 * 2
sw   t1, 0(s0)             # array[0] = t1
lw   t1, 4(s0)            # t1 = array[1]
slli t1, t1, 1            # t1 = t1 * 2
sw   t1, 4(s0)             # array[1] = t1
```

### Acceder a matrices usando bucles for

**Código C:**

```c
int array[1000];
int i;
for (i=0; i < 1000; i = i + 1)
  array[i] = array[i] * 8;
```

### Acceder a arreglos usando bucles for: código

```asm
lui  s0, 0x23B8F      # s0 = 0x23B8F000
ori  s0, s0, 0x400     # s0 = 0x23B8F400
addi s1, zero, 0       # i = 0
addi t2, zero, 1000    # t2 = 1000
loop:
  bge  s1, t2, done     # if not then done
  slli t0, s1, 2        # t0 = i * 4 (byte offset)
  add  t0, t0, s0       # address of array[i]
  lw   t1, 0(t0)        # t1 = array[i]
  slli t1, t1, 3        # t1 = array[i] * 8
  sw   t1, 0(t0)         # array[i] = array[i] * 8
  addi s1, s1, 1         # i = i + 1
  j    loop               # repeat
done:
```

### Código ASCII

- ASCII: Código estándar estadounidense para el intercambio de información
- Cada carácter de texto tiene un valor de byte único
  - Por ejemplo, S = 0x53, a = 0x61, A = 0x41
  - Minúsculas y mayúsculas difieren en 0x20 (32)

### Reparto de caracteres: codificaciones ASCII

| # | Char | # | Char | # | Char | # | Char | # | Char | # | Char |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | space | 30 | 0 | 40 | @ | 50 | P | 60 | \` | 70 | p |
| 21 | ! | 31 | 1 | 41 | A | 51 | Q | 61 | a | 71 | q |
| 22 | " | 32 | 2 | 42 | B | 52 | R | 62 | b | 72 | r |
| 23 | # | 33 | 3 | 43 | C | 53 | S | 63 | c | 73 | s |
| 24 | $ | 34 | 4 | 44 | D | 54 | T | 64 | d | 74 | t |
| 25 | % | 35 | 5 | 45 | E | 55 | U | 65 | e | 75 | u |
| 26 | & | 36 | 6 | 46 | F | 56 | V | 66 | f | 76 | v |
| 27 | ' | 37 | 7 | 47 | G | 57 | W | 67 | g | 77 | w |
| 28 | ( | 38 | 8 | 48 | H | 58 | X | 68 | h | 78 | x |
| 29 | ) | 39 | 9 | 49 | I | 59 | Y | 69 | i | 79 | y |
| 2A | * | 3A | : | 4A | J | 5A | Z | 6A | j | 7A | z |
| 2B | + | 3B | ; | 4B | K | 5B | [ | 6B | k | 7B | { |
| 2C | , | 3C | < | 4C | L | 5C | \\ | 6C | l | 7C | \| |
| 2D | - | 3D | = | 4D | M | 5D | ] | 6D | m | 7D | } |
| 2E | . | 3E | > | 4E | N | 5E | ^ | 6E | n | 7E | ~ |
| 2F | / | 3F | ? | 4F | O | 5F | _ | 6F | o | | |

### Acceso a matrices de caracteres

**Código C:**

```c
char str[80] = "CAT";
int len = 0;
// calcula longitud de la cadena
while (str[len]) len++;
```

**Código ensamblador RISC-V:**

```asm
addi s1, zero, 0         # len = 0
while: add t0, s0, s1    # address of str[len]
  lw   t1, 0(t0)          # load str[len]
  beq  t1, zero, done     # are we at the end of the string?
  addi s1, s1, 1          # len++
  j    while                # repeat while loop
done:
```

## Llamadas de función

### Llamadas a función

- Llamador: función que llama (en este caso, main)
- Llamado: función llamada (en este caso, sum)

**Código C:**

```c
void main()
{
  int y;
  y = sum(42, 7);
}

int sum(int a, int b)
{
  return (a + b);
}
```

### Llamada a función simple

| Código C | código ensamblador RISC-V |
| --- | --- |
| int main() { | 0x00000300 main: jal simple   # call |
| simple(); | 0x00000304 add s0, s1, s2 |
| a = b + c; | ... |
| } | |
| void simple() { | 0x0000051c simple: jr ra   # return |
| return; | |
| } | |

- `void simple` significa que no devuelve un valor
- `jal simple`: ra = PC + 4 (0x00000304); salta a etiqueta simple (PC = 0x0000051c)
- `jr ra`: PC = (ra) (0x00000304)

### Convenciones de llamadas de función

- Llamante:
  - pasa argumentos al llamado
  - salta al llamado
- Llamado:
  - realiza la función
  - devuelve el resultado a llamador
  - vuelve al punto de llamada
  - no debe sobrescribir los registros o la memoria que usa el llamador

### Convenciones de llamada de función RISC-V

- Función de llamada: saltar y enlazar (jal función)
- Retorno de función: registro de salto (jr ra)
- Argumentos: a0 – a7
- Valor devuelto: a0

### Argumentos de entrada y valor devuelto: código C

```c
int main()
{
  int y;
  y = diffofsums(2, 3, 4, 5); // 4 arguments
}

int diffofsums(int f, int g, int h, int i)
{
  int result;
  result = (f + g) - (h + i);
  return result; // valor de retorno
}
```

### Argumentos de entrada y valor devuelto: ensamblador

```asm
main:
  ...
  addi a0, cero, 2   # argumento 0 = 2
  addi a1, cero, 3   # argumento 1 = 3
  addi a2, cero, 4   # argumento 2 = 4
  addi a3, cero, 5   # argumento 3 = 5
  jal diffofsums      # función de llamada
  add s7, a0, cero    # y = valor devuelto
  ...
diffofsums:
  add t0, a0, a1      # t0 = f + g
  add t1, a2, a3      # t1 = h + i
  sub s3, t0, t1      # resultado = (f + g) − (h + i)
  add a0, s3, cero    # coloca el valor de retorno en a0
  jr ra                # volver a la persona que llama
```

- diffofsums sobrescribió 3 registros: t0, t1, s3
- diffofsums puede usar la pila para almacenar registros temporalmente

## La pila

### La pila

- Memoria utilizada para guardar variables temporalmente
- Como una pila de platos, cola de último en entrar, primero en salir (LIFO)
- Expande: utiliza más memoria cuando se necesita más espacio
- Compacta: usa menos memoria cuando ya no se necesita el espacio

### La pila: crecimiento

- Crece hacia abajo (de direcciones de memoria más altas a más bajas)
- Puntero de pila: sp apunta a la parte superior de la pila

*Diagrama de la diapositiva: estado de la pila antes y después de reservar espacio para 2 palabras. Direcciones de ejemplo: 0xBEFFFAE8 (contiene 0xAB000001, apuntada por sp), 0xBEFFFAE4 (contiene 0x12345678), 0xBEFFFAE0 y 0xBEFFFADC (libres; sp pasa a apuntar a 0xBEFFFAE0 tras reservar espacio). El layout visual exacto no se pudo recuperar de la extracción OCR.*

### Cómo las funciones usan la pila

- Las funciones llamadas no deben tener efectos secundarios no deseados
- Pero diffofsums sobrescribe 3 registros: t0, t1, s3

```asm
diffofsums:
  add t0, a0, a1      # t0 = f + g
  add t1, a2, a3      # t1 = h + i
  sub s3, t0, t1      # resultado = (f + g) − (h + i)
  add a0, s3, zero    # pone valor de retorno en a0
  jr  ra                # vuelta al llamador
```

### Almacenamiento de valores de registro en la pila

```asm
diffofsums:
  addi sp, sp, -12    # hacer espacio en la pila
  sw   s3, 8(sp)       # guardar s3 en la pila
  sw   t0, 4(sp)       # guardar t0 en la pila
  sw   t1, 0(sp)       # guardar t1 en la pila
  add  t0, a0, a1      # t0 = f + g
  add  t1, a2, a3      # t1 = h + i
  sub  s3, t0, t1      # resultado = (f + g) − (h + i)
  add  a0, s3, cero    # coloque el valor de retorno en a0
  lw   s3, 8(sp)       # restaurar s3 desde la pila
  lw   t0, 4(sp)       # restaurar t0 desde la pila
  lw   t1, 0(sp)       # restaurar t1 desde la pila
  addi sp, sp, 12      # desasignar espacio de pila
  jr   ra                # volver al que llama
```

### La pila durante la llamada de diffofsums

*Diagrama de la diapositiva: estado de la pila en tres momentos (antes de la llamada, durante la llamada, después de la llamada), con direcciones 0xBEF0F0FC (sp, valor desconocido "?"), 0xBEF0F0F8 (s3 durante la llamada), 0xBEF0F0F4 (t0 durante la llamada) y 0xBEF0F0F0 (t1 durante la llamada; sp vuelve a apuntar aquí después de la llamada). El layout visual exacto, incluida una etiqueta rotada "stack frame", no se pudo recuperar de la extracción OCR.*

### Llamada a procedimiento

Pasos requeridos:

1. Coloque los parámetros en los registros x10 a x17
2. Transferir el control al procedimiento
3. Adquirir almacenamiento para el procedimiento
4. Realiza las operaciones del procedimiento
5. Coloque el resultado en el registro para el llamante
6. Regreso al lugar de la llamada (dirección en x1)

### Procedimiento Llamada: Instrucciones

- Llamada de procedimiento: salto y enlace — `jal x1, etiqueta_de_procedimiento`
  - Dirección de la siguiente instrucción puesta en x1
  - Salta a la dirección de destino
- Retorno de procedimiento: registro de salto y enlace — `jalr x0, 0(x1)`
  - Como jal, pero salta a 0 + dirección en x1
  - Use x0 como rd (x0 no se puede cambiar)
  - También se puede utilizar para saltos calculados, por ejemplo, para sentencias case/switch

### Registros preservados

| Nombre | Número de registro | Uso | Preservado / No conservado |
| --- | --- | --- | --- |
| cero | x0 | Valor constante 0 | — |
| ra | x1 | Dirección del vuelta | Guardado por llamante |
| sp | x2 | Puntero de pila | Guardado por llamado |
| gp | x3 | Puntero global | Guardado por llamado |
| tp | x4 | Puntero de hilo | Guardado por llamado |
| t0-2 | x5-7 | Temporales | Guardado por llamante |
| s0/fp | x8 | Registro guardado / Puntero de cuadro | Guardado por llamado |
| s1 | x9 | registro guardado | Guardado por llamado |
| a0-1 | x10-11 | Argumentos de función/valores devueltos | Guardado por llamante |
| a2-7 | x12-17 | Argumentos de función | Guardado por llamante |
| s2-11 | x18-27 | Registros guardados | Guardado por llamado |
| t3-6 | x28-31 | Temporales | Guardado por llamante |

*Nota: la pila se organiza con las direcciones por encima de sp reservadas al llamador y las de por debajo de sp disponibles para el llamado.*

### Uso de registros

- x5 – x7, x28 – x31: registros temporales
  - No conservado por el llamado
- x8 – x9, x18 – x27: registros guardados
  - Si se usan, el destinatario los guarda y los restaura

### Almacenamiento de registros guardados en la pila

```asm
diffofsums:
  addi sp, sp, -4      # hacer espacio en la pila
  sw   s3, 0(sp)        # guardar s3 en la pila
  add  t0, a0, a1       # t0 = f + g
  add  t1, a2, a3       # t1 = h + i
  sub  s3, t0, t1       # resultado = (f + g) − (h + i)
  add  a0, s3, cero     # coloque el valor devuelto en a0
  lw   s3, 0(sp)        # restaurar s3 de la pila
  addi sp, sp, 4        # desasignar espacio de pila
  jr   ra                 # volver a la rutina que llama
```

### Diffofsums optimizado

```asm
diffofsums:
  add t0, a0, a1     # t0 = f + g
  add t1, a2, a3     # t1 = h + i
  sub a0, t0, t1     # resultado = (f + g) − (h + i)
  jr  ra               # volver a la rutina que llama
```

### Llamadas a funciones no hoja

Función no hoja: una función que llama a otra función.

```asm
funcion1:
  addi sp, sp, -4     # hacer espacio en la pila
  sw   ra, 0(sp)       # guardar ra en la pila
  jal  func2
  lw   ra, 0(sp)       # restaurar ra desde la pila
  addi sp, sp, 4       # desasignar espacio de pila
  jr   ra                # volver a la persona que llama
```

Debe conservar ra antes de llamar a la función.

### Ejemplo de llamada de función no hoja

```asm
f1:
  addi sp, sp, -20   # hacer espacio en la pila para 5 palabras
  sw   a0, 16(sp)
  sw   a1, 12(sp)
  sw   ra, 8(sp)      # guardar ra en la pila
  sw   s4, 4(sp)
  sw   s5, 0(sp)
  jal  func2
  lw   ra, 8(sp)       # restaurar ra (y otros registros) de la pila
  addi sp, sp, 20      # desasignar espacio de pila
  jr   ra                # volver a la persona que llama

f2:
  addi sp, sp, -4    # hacer espacio en la pila para 1 palabra
  sw   s4, 0(sp)
  lw   s4, 0(sp)
  addi sp, sp, 4      # desasignar espacio de pila
  jr   ra               # volver a la persona que llama
```

### Pila durante las llamadas a funciones

*Diagrama de la diapositiva: evolución de la pila en tres estados (antes de las llamadas, después de llamar a f1, después de llamar a f2). Direcciones de ejemplo: 0xBEF7FF0C (sp inicial, valor "?"), 0xBEF7FF08 (marco de pila de f1: a0), 0xBEF7FF04 (a1), 0xBEF7FF00 (ra), 0xBEF7FEFC (s4), 0xBEF7FEF8 (marco de pila de f2: s5, sp tras llamar a f1), 0xBEF7FEF4 (s4, sp tras llamar a f2). El layout visual exacto, incluidas las etiquetas rotadas "f1's stack frame" y "f2's stack frame", no se pudo recuperar de la extracción OCR.*

### Resumen de llamada de función

- Llamador o Llamante:
  - Guarda los registros necesarios (ra, tal vez t0-t6/a0-a7)
  - Poner argumentos en a0-a7
  - Función de llamada: jal llamado
  - Buscar resultado en a0
  - Restaurar cualquier registro guardado
- Llamado:
  - Guardar registros que puedan ser perturbados (s0-s11)
  - realizar la función
  - Poner resultado en a0
  - Restaurar registros
  - Retorno: jr ra

## Funciones recursivas

### Ejemplo de función recursiva

- Función que se llama a sí misma
- Al convertir a código ensamblador:
  - En el primer paso, trate las llamadas recursivas como si estuvieran llamando a una función diferente e ignore los registros sobrescritos.
  - Luego guarde/restaure los registros en la pila según sea necesario.

### Ejemplo de función recursiva: factorial

- Función factorial:
  - factorial(n) = n! = n*(n-1)*(n-2)*(n-3)…*1
  - Ejemplo: factorial(6) = 6! = 6*5*4*3*2*1 = 720

### Ejemplo de función recursiva: código de alto nivel

```c
int factorial(int n) {
  if (n <= 1)
    return 1;
  else
    return (n*factorial(n−1));
}
```

Ejemplo: n = 3

- factorial(3): devuelve 3*factorial(2)
- factorial(2): devuelve 2*factorial(1)
- factorial(1): devuelve 1

De este modo:

- factorial(1): devuelve 1
- factorial(2): devuelve 2*1 = 2
- factorial(3): devuelve 3*2 = 6

### Ejemplo de función recursiva: paso 1 (ignorar pila)

| Código de alto nivel | Ensamblador RISC-V |
| --- | --- |
| int factorial(int n) { | factorial: |
| | addi t0, cero, 1   # temporal = 1 |
| if (n <= 1) | bgt a0, t0, else   # si n>1, ir a else |
| return 1; | addi a0, cero, 1   # sino, devuelve 1 |
| | jr ra                 # volver |
| else | else: |
| return (n*factorial(n−1)); | addi a0, a0, -1     # n = n − 1 |
| } | jal factorial          # llamada recursiva |

Paso 1: Tratar como si llamara a otra función. Ignorar pila.

```asm
mul a0, a0, a0   # a0 = n*factorial(n−1), valor devuelto: factorial(n-1)
jr  ra             # volver
```

Paso 2: Guarde los registros sobrescritos (necesarios después de la llamada a la función) en la pila antes de la llamada.

Problema: ¡n (a0) fue sobrescrito por una llamada de función! Debe guardarlo (y ra) en la pila antes de llamar a la función.

### Ejemplo de función recursiva: paso 2 (con pila)

| Código de alto nivel | Ensamblador RISC-V |
| --- | --- |
| int factorial(int n) { | factorial: |
| | addi sp, sp, -8    # guardar registros |
| | sw a0, 4(sp) |
| | sw ra, 0(sp) |
| | addi t0, cero, 1    # temporal = 1 |
| if (n <= 1) | bgt a0, t0, else    # si n>1, ir a else |
| return 1; | addi a0, cero, 1    # si no, devuelve 1 |
| | addi sp, sp, 8      # restaurar sp |
| | jr ra                  # volver |
| else | else: |
| return (n*factorial(n−1)); | addi a0, a0, -1      # n = n − 1 |
| } | jal factorial           # llamada recursiva |
| | lw t1, 4(sp)          # restaurar n en t1 |
| | lw ra, 0(sp)          # restaurar ra |
| | addi sp, sp, 8        # restaurar sp |
| | mul a0, t1, a0        # a0 = n*factorial(n−1) |
| | jr ra                    # volver |

Paso 1: Tratar como si llamara a otra función. Ignorar pila. Paso 2: Guarde los registros sobrescritos (necesarios después de la llamada a la función) en la pila antes de la llamada.

*Nota: n se restaura de la pila a t1 para que no sobrescriba el valor devuelto en a0.*

### Funciones recursivas: direcciones de código

```asm
0x8500 factorial:  addi sp, sp, -8       # guardar registros
0x8504             sw a0, 4(sp)
0x8508             sw ra, 0(esp)
0x850C             addi t0, cero, 1       # temporal = 1
0x8510             bgt a0, t0, else       # si n > 1, ir a else
0x8514             addi a0, cero, 1       # si no, devuelve 1
0x8518             addi sp, sp, 8         # restaurar sp
0x851C             jr ra                     # volver
0x8520 else:       addi a0, a0, -1         # n = n − 1
0x8524             jal factorial              # llamada recursiva
0x8528             lw t1, 4(sp)             # restaurar n en t1
0x852C             lw ra, 0(sp)             # restaurar ra
0x8530             addi sp, sp, 8           # restaurar sp
0x8534             mul a0, t1, a0           # a0 = n*factorial(n−1)
0x8538             jr ra                        # volver
```

PC+4 = 0x8528 cuando factorial se llama recursivamente.

### Apilar durante la función recursiva

*Diagrama de la diapositiva: evolución de la pila cuando se llama a factorial(3), en tres momentos (antes de las llamadas, después de las llamadas recursivas, retornando de las llamadas). Direcciones de ejemplo FF0, FEC, FE8, FE4, FE0, FDC, FD8 (relativas a sp), que guardan sucesivamente a0=n=3, ra=0x8528, a0=n=2, ra=0x8528, a0=n=1, y los valores de retorno a0=6, a0=3×2, a0=2×1, a0=1 según se completa cada nivel de recursión. El layout visual exacto, incluidas las etiquetas rotadas de "marco de pila", no se pudo recuperar de la extracción OCR.*

## Más sobre saltos y pseudoinstrucciones

### Saltos

- RISC-V tiene dos tipos de saltos incondicionales:
  - Saltar y enlazar (jal rd, imm[20:0])
    - rd = PC+4; PC = PC + inm
  - Salto y enlace con registro (jalr rd, rs, imm[11:0])
    - rd = PC+4; PC = [rs] + SignExt(imm)

### Pseudoinstrucciones

- Pseudoinstrucciones no son instrucciones RISC-V reales, pero a menudo son más convenientes para el programador.
- Assembler las convierte en instrucciones RISC-V reales.

### Pseudoinstrucciones de salto

RISC-V tiene cuatro pseudoinstrucciones de salto:

| Pseudoinstrucción | Instrucción RISC-V real |
| --- | --- |
| j imm | jal x0, imm |
| jal imm | jal ra, imm |
| jr rs | jalr x0, rs, 0 |
| ret | jr ra (es decir, jalr x0, ra, 0) |

### Etiquetas

- La etiqueta indica dónde saltar
- Representado en salto como desplazamiento inmediato
  - imm = # bytes después de la instrucción de salto
  - En el ejemplo, a continuación, imm = (51C-300) = 0x21C
  - `jal simple = jal ra, 0x21C`

Código ensamblador RISC-V:

```asm
0x00000300 principal: jal simple   # llamada
0x00000304             add s0, s1, s1
0x0000051c simple:     jr ra        # volver
```

### Saltos de longitud

- Lo inmediato tiene un tamaño limitado: 20 bits para jal, 12 bits para jalr
  - Limita hasta dónde puede saltar un programa
- Instrucciones especiales para ayudar a saltar más lejos:
  - auipc rd, imm: agregar inmediatamente superior al PC
    - rd = PC + {imm[31:12], 12'b0}
- Pseudoinstrucción `call`: se comporta como jal imm[31:0], pero permite el desplazamiento inmediato de 32 bits:

```asm
auipc ra, imm[31:12]
jalr  ra, ra, imm[11:0]
```

### Más pseudoinstrucciones de RISC-V

| Pseudoinstrucción | Instrucciones RISC-V |
| --- | --- |
| j label | jal zero, label |
| jr ra | jalr zero, ra, 0 |
| mv t5, s3 | addi t5, s3, 0 |
| not s7, t2 | xori s7, t2, -1 |
| nop | addi zero, zero, 0 |
| li s8, 0x56789DEF | lui s8, 0x5678A; addi s8, s8, 0xDEF |
| bgt s1, t3, L3 | blt t3, s1, L3 |
| bgez t2, L7 | bge t2, zero, L7 |
| call L1 | auipc ra, imm[31:12]; jalr ra, ra, imm[11:0] |
| ret | jalr zero, ra, 0 |

Consulte el Apéndice B para obtener más pseudoinstrucciones.

## Lenguaje máquina

### Lenguaje de máquina

- Representación binaria de instrucciones
- Las computadoras solo entienden 1 y 0
- Instrucciones de 32 bits
  - La simplicidad favorece la regularidad: datos e instrucciones de 32 bits
- 4 tipos de formatos de instrucciones:
  - R-Type
  - I-Type
  - S/B-Type
  - U/J-Type

### Tipo R

- Tipo registro
- 3 operandos de registro:
  - rs1, rs2: registros fuente
  - rd: registro de destino
- Otros campos:
  - op: el código de operación
  - funct7, funct3: la función (7 bits y 3 bits, respectivamente); junto con el código de operación, le dice a la computadora qué operación realizar

| 31:25 | 24:20 | 19:15 | 14:12 | 11:7 | 6:0 |
| --- | --- | --- | --- | --- | --- |
| funct7 | rs2 | rs1 | funct3 | rd | op |
| 7 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits |

### Ejemplos de tipo R

| Assembly | funct7 | rs2 | rs1 | funct3 | rd | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- | --- |
| add s2, s3, s4 (add x18, x19, x20) | 0 | 20 | 19 | 0 | 18 | 51 | 0x01498933 |
| sub t0, t1, t2 (sub x5, x6, x7) | 32 | 7 | 6 | 0 | 5 | 51 | 0x407302B3 |

### Más ejemplos de tipo R

| Assembly | funct7 | rs2 | rs1 | funct3 | rd | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- | --- |
| sll s7, t0, s1 (sll x23, x5, x9) | 0 | 9 | 5 | 1 | 23 | 51 | 0x00929BB3 |
| xor s8, s9, s10 (xor x24, x25, x26) | 0 | 26 | 25 | 4 | 24 | 51 | 0x01ACCC33 |
| srai t1, t2, 29 (srai x6, x7, 29) | 32 | 29 | 7 | 5 | 6 | 19 | 0x41D3D313 |

## Lenguaje máquina: más formatos

### Tipo I

- Tipo inmediato
- 3 operandos:
  - rs1: registra el operando fuente
  - rd: registra el operando de destino
  - imm: complemento a dos de 12 bits inmediato
- Otros campos:
  - op: el código de operación — la simplicidad favorece la regularidad: todas las instrucciones tienen código de operación
  - funct3: la función (código de función de 3 bits); junto con código de operación, le dice a la computadora qué operación realizar

| 31:20 | 19:15 | 14:12 | 11:7 | 6:0 |
| --- | --- | --- | --- | --- |
| imm[11:0] | rs1 | funct3 | rd | op |
| 12 bits | 5 bits | 3 bits | 5 bits | 7 bits |

### Ejemplos de tipo I

| Assembly | imm | rs1 | funct3 | rd | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- |
| addi s0, s1, 12 (addi x8, x9, 12) | 12 | 9 | 0 | 8 | 19 | 0x00C48413 |
| addi s2, t1, -14 (addi x18, x6, -14) | -14 | 6 | 0 | 18 | 19 | 0xFF230913 |
| lw t2, -6(s3) (lw x7, -6(x19)) | -6 | 19 | 2 | 7 | 3 | 0xFFA9A383 |
| lh s1, 27(zero) (lh x9, 27(x0)) | 27 | 0 | 1 | 9 | 3 | 0x01B01483 |
| lb s4, 0x1F(s4) (lb x20, 0x1F(x20)) | 0x1F | 20 | 0 | 20 | 3 | 0x01FA0A03 |

### Tipo S/B

- Store-Type
- Branch-Type
- Difieren solo en la codificación inmediata

| 31:25 | 24:20 | 19:15 | 14:12 | 11:7 | 6:0 | |
| --- | --- | --- | --- | --- | --- | --- |
| imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | op | S-Type |
| imm[12,10:5] | rs2 | rs1 | funct3 | imm[4:1,11] | op | B-Type |
| 7 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits | |

### Tipo S

- Store-Type
- 3 operandos:
  - rs1: registro base
  - rs2: valor que se almacenará en la memoria
  - imm: complemento a dos de 12 bits inmediato
- Otros campos:
  - op: el código de operación — la simplicidad favorece la regularidad: todas las instrucciones tienen código de operación
  - funct3: la función (código de función de 3 bits); junto con código de operación, le dice a la computadora qué operación realizar

| 31:25 | 24:20 | 19:15 | 14:12 | 11:7 | 6:0 |
| --- | --- | --- | --- | --- | --- |
| imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | op |
| 7 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits |

### Ejemplos de tipo S

| Assembly | imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- | --- |
| sw t2, -6(s3) (sw x7, -6(x19)) | 1111111 | 7 | 19 | 2 | 11010 | 35 | 0xFE79AD23 |
| sh s4, 23(t0) (sh x20, 23(x5)) | 0000000 | 20 | 5 | 1 | 10111 | 35 | 0x01429BA3 |
| sb t5, 0x2D(zero) (sb x30, 0x2D(x0)) | 0000001 | 30 | 0 | 0 | 01101 | 35 | 0x03E006A3 |

### Tipo B

- Branch-Type (formato similar al S-Type)
- 3 operandos:
  - rs1: registrar fuente 1
  - rs2: registrar fuente 2
  - imm[12:1]: complemento de dos de 12 bits inmediato — desplazamiento de dirección
- Otros campos:
  - op: el código de operación — la simplicidad favorece la regularidad: todas las instrucciones tienen código de operación
  - funct3: la función (código de función de 3 bits); con código de operación, le dice a la computadora qué operación realizar

| 31:25 | 24:20 | 19:15 | 14:12 | 11:7 | 6:0 |
| --- | --- | --- | --- | --- | --- |
| imm[12,10:5] | rs2 | rs1 | funct3 | imm[4:1,11] | op |
| 7 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits |

### Ejemplo de tipo B

El inmediato de 13 bits codifica dónde bifurcar (en relación con la instrucción de bifurcación). La codificación inmediata es "extraña" (bit-swizzled).

Ejemplo:

| Address | RISC-V Assembly |
| --- | --- |
| 0x70 | beq s0, t5, L1 |
| 0x74 | add s1, s2, s3 |
| 0x78 | sub s5, s6, s7 |
| 0x7C | lw t0, 0(s1) |
| 0x80 | L1: addi s1, s1, -15 |

L1 is 4 instructions (i.e., 16 bytes) past beq.

```
imm = 16
bit:   12 11 10 9 8 7 6 5 4 3 2 1 0
value:  0  0  0 0 0 0 0 0 1 0 0 0 0
```

| Assembly | imm[12,10:5] | rs2 | rs1 | funct3 | imm[4:1,11] | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- | --- |
| beq s0, t5, L1 (beq x8, x30, 16) | 0000000 | 30 | 8 | 0 | 10000 | 99 | 0x01E40863 |

### Tipo U/J

- Tipo inmediato superior
- Tipo de salto
- Difieren solo en la codificación inmediata

| 31:12 | 11:7 | 6:0 | |
| --- | --- | --- | --- |
| imm[31:12] | rd | op | U-Type |
| imm[20,10:1,11,19:12] | rd | op | J-Type |
| 20 bits | 5 bits | 7 bits | |

### Tipo U

- Tipo inmediato superior
- Usado para carga superior inmediata (lui)
- 2 operandos:
  - rd: registro de destino
  - imm[31:12]: 20 bits superiores de un inmediato de 32 bits
- Otros campos:
  - op: el código de operación, le dice a la computadora qué operación a realizar

| 31:12 | 11:7 | 6:0 |
| --- | --- | --- |
| imm[31:12] | rd | op |
| 20 bits | 5 bits | 7 bits |

### Ejemplo tipo U

| Assembly | imm[31:12] | rd | op | Machine Code |
| --- | --- | --- | --- | --- |
| lui s5, 0x8CDEF (lui x21, 0x8CDEF) | 0x8CDEF (10001100110111101111) | 21 | 55 | 0x8CDEFAB7 |

### Tipo J

- Tipo de salto
- Se utiliza para la instrucción de salto y enlace (jal)
- 2 operandos:
  - rd: registro de destino
  - imm[20,10:1,11,19:12]: 20 bits (20:1) de un inmediato de 21 bits
- Otros campos:
  - op: el código de operación, le dice a la computadora qué operación a realizar

| 31:12 | 11:7 | 6:0 |
| --- | --- | --- |
| imm[20,10:1,11,19:12] | rd | op |
| 20 bits | 5 bits | 7 bits |

*Nota: jalr es de tipo I, no de tipo J, para poder especificar rs.*

### Ejemplo tipo J

| Address | RISC-V Assembly |
| --- | --- |
| 0x0000540C | jal ra, func1 |
| 0x00005410 | add s1, s2, s3 |
| ... | ... |
| 0x000ABC04 | func1: add s4, s5, s8 |

0xABC04 – 0x540C = 0xA67F8. func1 es 0xA67F8 bytes past jal.

```
imm = 0xA67F8
bit:   20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0
value:  0  1  0  1  0  0  1  1  0  0  1 1 1 1 1 1 1 1 0 0 0
```

| Assembly | imm[20,10:1,11,19:12] | rd | op | Machine Code |
| --- | --- | --- | --- | --- |
| jal ra, func1 (jal x1, 0xA67F8) | 01111111100010100110 | 1 | 1101111 | 0x7F8A60EF |

### Revisión: formatos de instrucción

| Formato | 7 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits |
| --- | --- | --- | --- | --- | --- | --- |
| R-Type | funct7 | rs2 | rs1 | funct3 | rd | op |
| I-Type | imm[11:0] | | rs1 | funct3 | rd | op |
| S-Type | imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | op |
| B-Type | imm[12,10:5] | rs2 | rs1 | funct3 | imm[4:1,11] | op |
| U-Type | imm[31:12] | | | | rd | op |
| J-Type | imm[20,10:1,11,19:12] | | | | rd | op |

### Principio de diseño 4: Un buen diseño exige buenos compromisos

- Múltiples formatos de instrucción permiten flexibilidad
  - add, sub: usar 3 operandos de registro
  - lw, sw, addi: usa 2 operandos de registro y una constante
- Número de formatos de instrucción se mantienen pequeños
- Adherirse a los principios de diseño 1 y 3 (la simplicidad favorece la regularidad y lo más pequeño es más rápido).

## Codificaciones inmediatas

### Constantes / Inmediatos

- lw y sw usan constantes o inmediatos
- Inmediatamente disponible desde la instrucción
- Número de complemento a dos de 12 bits
- addi: añadir inmediato
- ¿Es necesario restar inmediato (subi)? No: basta con sumar un inmediato negativo.

| Código C | código ensamblador RISC-V |
| --- | --- |
| a = a + 4; | addi s0, s0, 4 |
| b = a – 12; | addi s1, s0, -12 |

### Constantes / Inmediatos: bits inmediatos

*Diagrama de la diapositiva: esquema de qué bits del inmediato (imm) ocupa cada formato de instrucción (I/S, B, U, J) dentro de los 32 bits de la instrucción — p. ej. I/S coloca imm[11:1] e imm[0] de forma contigua, B coloca imm[12], imm[11] e imm[11:1] en posiciones distintas, U coloca imm[31:21] e imm[20:12], y J coloca imm[20], imm[20:12] e imm[11:1]. El layout bit a bit exacto no se pudo recuperar de la extracción OCR; la asignación de bits para cada formato ya está descrita en las tablas de tipo S, B, U y J anteriores.*

### Codificaciones inmediatas: bits de instrucción

*Diagrama de la diapositiva: tabla que muestra, para cada formato de instrucción (R, I, S, B, U, J), qué posición de bit de la instrucción (31 a 0) contiene cada campo (opcode, rd, funct3, rs1, rs2, bits del inmediato). El layout exacto no se pudo recuperar de la extracción OCR; la asignación de campos ya está descrita en las tablas de formato anteriores (R-Type, I-Type, S/B-Type, U/J-Type).*

- Los bits inmediatos ocupan principalmente bits de instrucciones consistentes.
- Simplifica el hardware para construir el microprocesador
- El bit de signo de inmediato firmado está en el bit más significativo (msb) de la instrucción.
- Recuerde que rs2 de tipo R puede codificar la cantidad de desplazamiento inmediato.

### Resumen de codificación RISC-V

*Diagrama de la diapositiva: tabla resumen de la codificación de instrucciones RISC-V (formatos, opcodes y campos). El contenido ya se ha cubierto en detalle en las secciones anteriores de tipos R, I, S, B, U y J.*

### Codificación de instrucciones RISC-V vs MIPS

*CREATOR - Simulador de programación de ensamblaje didáctico y genérico (creatorsim.github.io)*

### Codificación básica de instrucciones x86

- Codificación de longitud variable
  - Los bytes de sufijo especifican el modo de direccionamiento
  - Operación de modificación de bytes de prefijo
- Longitud del operando, repetición, bloqueo, …

## Lectura de lenguaje de máquina y operandos de direccionamiento

### Campos y formatos de instrucciones

| Instrucción | op | funct3 | funct7 | Tipo |
| --- | --- | --- | --- | --- |
| add | 0110011 (51) | 000 (0) | 0000000 (0) | R-Type |
| sub | 0110011 (51) | 000 (0) | 0100000 (32) | R-Type |
| and | 0110011 (51) | 111 (7) | 0000000 (0) | R-Type |
| or | 0110011 (51) | 110 (6) | 0000000 (0) | R-Type |
| addi | 0010011 (19) | 000 (0) | - | I-Type |
| beq | 1100011 (99) | 000 (0) | - | B-Type |
| bne | 1100011 (99) | 001 (1) | - | B-Type |
| lw | 0000011 (3) | 010 (2) | - | I-Type |
| sw | 0100011 (35) | 010 (2) | - | S-Type |
| jal | 1101111 (111) | - | - | J-Type |
| jalr | 1100111 (103) | 000 (0) | - | I-Type |
| lui | 0110111 (55) | - | - | U-Type |

Consulte el Apéndice B para conocer otras codificaciones de instrucciones.

### Interpretación del código de la máquina

- Escribir en binario
- Empezar con op (& funct3): dice cómo analizar el resto
- Extraer campos
- op, funct3 y funct7 indican la operación

Ej: 0x41FE83B3 y 0xFDA48393

```
0x41FE83B3: 0100 0001 1111 1110 1000 0011 1011 0011
op = 51, funct3 = 0: add or sub (R-type)
funct7 = 0100000: sub

0xFDA48393: 1111 1101 1010 0100 1000 0011 1001 0011
op = 19, funct3 = 0: addi (I-type)
```

### Interpretación del código de la máquina: ejemplos

| | Machine Code | | Field Values | | | Assembly |
| --- | --- | --- | --- | --- | --- | --- |
| funct7 | rs2 | rs1 | funct3 | rd | op | |
| 0100 000 | 11111 | 11101 | 000 | 00111 | 011 0011 | sub t2, t4, t6 |

sub x7, x29, x31 (0x41FE83B3): funct7=32, rs2=31, rs1=29, funct3=0, rd=7, op=51

| | Machine Code | | Field Values | | Assembly |
| --- | --- | --- | --- | --- | --- |
| imm[11:0] | rs1 | funct3 | rd | op | |
| 1111 1101 1010 | 01001 | 000 | 00111 | 001 0011 | addi t2, s1, -38 |

addi x7, x9, -38 (0xFDA48393): imm=-38, rs1=9, funct3=0, rd=7, op=19

### Modos de direccionamiento

¿Cómo abordamos los operandos?

- Registro solo
- Inmediato
- Direccionamiento base
- Relativo a PC

### Modos de direccionamiento: registro solo e inmediato

**Registro solo**

- Operandos encontrados en registros
  - Ejemplo: `add s0, t2, t3`
  - Ejemplo: `sub t6, s1, zero`

**Inmediato**

- Inmediato con signo de 12 bits utilizado como operando
  - Ejemplo: `addi s4, t5, -73`
  - Ejemplo: `ori t3, t7, 0xFF`

### Modos de direccionamiento: direccionamiento básico

- Cargas y almacenamiento
- La dirección del operando es: dirección base + inmediato
  - Ejemplo: `lw s4, 72(cero)` → dirección = 0 + 72
  - Ejemplo: `sw t2, -25(t1)` → dirección = t1 - 25

### Modos de direccionamiento: relativo a PC

Direccionamiento relativo a PC: saltos (jal) y ramas (beq, bne, ...)

Ejemplo:

| Address | Instruction |
| --- | --- |
| 0x354 | L1: addi s1, s1, 1 |
| 0x358 | sub t0, t1, s7 |
| ... | ... |
| 0xEB0 | bne s8, s9, L1 |

La etiqueta L1 está (0xEB0-0x354) = 0xB5C (2908) bytes antes de bne.

```
imm = -2908
bit:   12 11 10 9 8 7 6 5 4 3 2 1 0
value:  1  0  1 0 0 1 0 1 0 0 1 0 0
```

| Assembly | imm[12,10:5] | rs2 | rs1 | funct3 | imm[4:1,11] | op | Machine Code |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bne s8, s9, L1 (bne x25, x26, L1) | 1100101 | 25 | 24 | 1 | 00100 | 99 | 0xCB8C9263 |

### Resumen de direccionamiento de RISC-V

*Diagrama de la diapositiva: tabla resumen de los modos de direccionamiento de RISC-V (registro, inmediato, base, relativo a PC). El contenido ya se ha cubierto en las diapositivas anteriores de esta sección.*

### Resumen básico de direccionamiento x86

- Dos operandos por instrucción

| Operando fuente/destino | Operando de segunda fuente |
| --- | --- |
| Registro | Registro |
| Registro | Inmediato |
| Registro | Memoria |
| Memoria | Registro |
| Memoria | Inmediato |

**Modos de direccionamiento de memoria x86**

- Dirección en el registro: `Dirección = R_base`
- `Dirección = R_base + desplazamiento`
- `Dirección = R_base + 2^escala × R_índice` (escala = 0, 1, 2 o 3)
- `Dirección = R_base + 2^escala × R_índice + desplazamiento`

## Compilación, ensamblaje y carga de programas

### El poder del programa almacenado

- Instrucciones de 32 bits y datos almacenados en la memoria
- Secuencia de instrucciones: única diferencia entre dos aplicaciones
- Para ejecutar un nuevo programa:
  - No se requiere recableado
  - Simplemente almacene el nuevo programa en la memoria
- Ejecución del programa:
  - El procesador obtiene (lee) las instrucciones de la memoria en secuencia
  - El procesador realiza la operación especificada

### El programa almacenado

| Assembly Code | Machine Code |
| --- | --- |
| add s2, s3, s4 | 0x01498933 |
| sub t0, t1, t2 | 0x407302B3 |
| addi s2, t1, -14 | 0xFF230913 |
| lw t2, -6(s3) | 0xFFA9A383 |

| Dirección | Instrucción |
| --- | --- |
| 0000083C | FFA9A383 |
| 00000838 | FF230913 |
| 00000834 | 407302B3 |
| 00000830 | 01498933 |

*Main Memory.* El contador de programa (PC) realiza un seguimiento de la instrucción actual.

### Alan Turing, 1912-1954

- Matemático e informático británico
- Fundador de la informática teórica
- Inventó la máquina de Turing: un modelo matemático de computación
- Diseñó el Motor de Cómputo Automático, una de las primeras computadoras con programa almacenado
- En 1952, fue procesado por actos homosexuales. Dos años después, murió por envenenamiento con cianuro.
- El Premio Turing fue nombrado en su honor, que es el más alto honor en computación.

### Cómo compilar y ejecutar un programa

*Diagrama de la diapositiva: cadena de herramientas de compilación — High Level Code → Compiler → Assembly Code → Assembler → Object File (+ Library Files → Object Files) → Linker → Executable → Loader → Memory.*

### Grace Hopper, 1906-1992

- Graduada de la Universidad de Yale con un Ph.D. en matemáticas
- Desarrolló el primer compilador
- Ayudó a desarrollar el lenguaje de programación COBOL
- Oficial naval altamente premiada
- Recibió la Medalla de la Victoria de la Segunda Guerra Mundial y la Medalla del Servicio de Defensa Nacional, entre otros

### ¿Qué se almacena en la memoria?

- Instrucciones (también llamadas texto)
- Datos
  - Global/estático: asignado antes de que comience el programa
  - Dinámico: asignado dentro del programa
- ¿Cómo es de grande la memoria?
  - Como máximo 2^32 = 4 gigabytes (4 GB)
  - De la dirección 0x00000000 a 0xFFFFFFFF

### Ejemplo de mapa de memoria RISC-V

| Dirección | Segmento |
| --- | --- |
| 0xFFFFFFFC | Operating System & I/O |
| 0x80000004 – 0x80000000 | Stack (sp) |
| | Dynamic Data (Heap) |
| 0x10001000 – 0x10000FFC | |
| 0x10000000 | Global Data (gp) |
| 0x00008000 | Text |
| 0x00000000 | Exception Handlers (pc) |

### Programa de ejemplo: Código C

```c
int f, g, y; // global variables

int func(int a, int b) {
  if (b < 0)
    return (a + b);
  else
    return (a + func(a, b-1));
}

void main() {
  f = 2;
  g = 3;
  y = func(f,g);
  return;
}
```

### Programa de ejemplo: ensamblador RISC-V (func)

```asm
Address   Machine Code  RISC-V Assembly Code
10144:    ff010113      func: addi sp,sp,-16
10148:    00112623            sw ra,12(sp)
1014c:    00812423            sw s0,8(sp)
10150:    00050413            mv s0,a0
10154:    00a58533            add a0,a1,a0
10158:    0005da63            bgez a1,1016c <func+0x28>
1015c:    00c12083            lw ra,12(sp)
10160:    00812403            lw s0,8(sp)
10164:    01010113            addi sp,sp,16
10168:    00008067            ret
1016c:    fff58593            addi a1,a1,-1
10170:    00040513            mv a0,s0
10174:    fd1ff0ef            jal ra,10144 <func>
10178:    00850533            add a0,a0,s0
1017c:    fe1ff06f            j 1015c <func+0x18>
```

*Mantenga la alineación de sp de 4 palabras (para compatibilidad con RV128I) aunque solo se necesita espacio para 2 palabras. Pseudoinstrucciones: mv es addi a0, s0, 0; ret (retorno) es jr ra.*

### Programa de ejemplo: ensamblador RISC-V (main)

```asm
Address   Machine Code  RISC-V Assembly Code
10180:    ff010113      main: addi sp,sp,-16
10184:    00112623            sw ra,12(sp)
10188:    00200713            li a4,2
1018c:    c4e1a823            sw a4,-944(gp)   # 11a30 <f>
10190:    00300713            li a4,3
10194:    c4e1aa23            sw a4,-940(gp)   # 11a34 <g>
10198:    00300593            li a1,3
1019c:    00200513            li a0,2
101a0:    fa5ff0ef            jal ra,10144 <func>
101a4:    c4a1ac23            sw a0,-936(gp)   # 11a38 <y>
101a8:    00c12083            lw ra,12(sp)
101ac:    01010113            addi sp,sp,16
101b0:    00008067            ret
```

*gp = 0x11DE0. Ponga 2 y 3 en f y g (y registros de argumentos) y llame a func. Luego ponga el resultado en y y regrese.*

### Programa de ejemplo: tabla de símbolos

```
Address   Size      Symbol   Name
00010074  l d .text 00000000 .text
000115e0  l d .data 00000000 .data
00010144  g F .text 0000003c func
00010180  g F .text 00000034 main
00011a30  g O .bss  00000004 f
00011a34  g O .bss  00000004 g
00011a38  g O .bss  00000004 y
```

- text segment: address 0x10074
- data segment: address 0x115e0
- func función: address 0x10144 (size 0x3c bytes)
- main función: address 0x10180 (size 0x34 bytes)
- f: address 0x11a30 (size 0x4 bytes)
- g: address 0x11a34 (size 0x4 bytes)
- y: address 0x11a38 (size 0x4 bytes)

### Programa de ejemplo en la memoria

*Diagrama de la diapositiva: contenido final de la memoria tras cargar el programa de ejemplo, mostrando el segmento de excepciones/texto (a partir de 0x00010074, incluyendo el código de func en 0x00010144 y de main en 0x00010180 con su código máquina), el segmento de datos globales (f, g, y en torno a 0x000115E0-0x00011A38, gp = 0x00011DE0) y la pila (sp = 0x7FFFFFF0), con pc = 0x00010180 al comenzar main. Los valores de código máquina y las direcciones ya están listados íntegramente en las tablas de las diapositivas "Programa de ejemplo: ensamblador RISC-V" anteriores; el layout visual exacto de esta diapositiva (una única columna de memoria con crecimiento de arriba hacia abajo) no se pudo recuperar de la extracción OCR debido al desorden del texto extraído.*

## Endianness

### Memoria Big-Endian y Little-Endian

- ¿Cómo numerar bytes dentro de una palabra?
- little-endian: los números de byte comienzan en el extremo pequeño (menos significativo)
- big-endian: los números de byte comienzan en el extremo grande (más significativo)
- La dirección de la palabra es la misma para big- o little-endian

*Diagrama de la diapositiva: comparación byte a byte de una palabra de 32 bits en Big-Endian frente a Little-Endian. Byte-Address 0-3 contiene los bytes de datos C,D,E,F (word address 0); en Big-Endian el byte 0 (MSB) está a la izquierda y el byte 3 (LSB) a la derecha; en Little-Endian el orden se invierte (byte 3 a la izquierda/MSB visual, byte 0 a la derecha/LSB visual). El mismo patrón se repite para las palabras en las direcciones 4, 8 y C. El layout visual exacto no se pudo recuperar de la extracción OCR, pero el contenido conceptual está descrito en el texto de esta diapositiva y la siguiente.*

### Memoria Big-Endian y Little-Endian: origen del nombre

- Los viajes de Gulliver de Jonathan Swift: los Little Endians rompieron sus huevos en el extremo pequeño del huevo y los Big Endians rompieron sus huevos en el extremo grande
- Realmente no importa qué tipo de direccionamiento se use, ¡excepto cuando los dos sistemas necesitan compartir datos!

### Ejemplo de Big-Endian y Little-Endian

- Supongamos que t0 inicialmente contiene 0x23456789
- Después de ejecutar el siguiente código en el sistema big-endian, ¿qué valor tiene s0? ¿Y en un sistema little-endian?

```asm
sw t0, 0(cero)
lb s0, 1(cero)
```

- Big endian: s0 = 0x00000045
- Little endian: s0 = 0x00000067

*Diagrama de la diapositiva: la palabra 0x23456789 almacenada en la dirección de palabra 0, con sus 4 bytes (23 45 67 89) distribuidos en las direcciones de byte 0-3. En Big-Endian el byte de dirección 0 es 23 (MSB) y el de dirección 3 es 89 (LSB); en Little-Endian el byte de dirección 0 es 89 (LSB) y el de dirección 3 es 23 (MSB). Esto explica por qué lb en la dirección 1 lee 0x45 en big-endian (segundo byte desde la izquierda) y 0x67 en little-endian (segundo byte desde la izquierda en ese orden).*

## Instrucciones con signo y sin signo

### Instrucciones con signo y sin signo

- Multiplicación y división
- Saltos
- Establecer menor que
- Cargas
- Detección de desbordamiento

### Multiplicación (con signo y sin signo)

- Signo: mulh
- Sin signo: mulhu, mulhsu
  - mulhu: trata ambos operandos como sin signo
  - mulhsu: trata el primer operando con signo, el segundo sin signo
  - Los 32 lsbs son idénticos, con o sin signo; use mul

Ejemplo: s1 = 0x80000000; s2 = 0xC0000000

| | mulh s4, s1, s2 | mulhu s4, s1, s2 | mulhsu s4, s1, s2 |
| --- | --- | --- | --- |
| | mul s3, s1, s2 | mul s3, s1, s2 | mul s3, s1, s2 |
| Interpretación | s1 = -2^31; s2 = -2^30 | s1 = 2^31; s2 = 3×2^30 | s1 = -2^31; s2 = 3×2^30 |
| Producto | s1 × s2 = 2^61 | s1 × s2 = 3×2^61 | s1 × s2 = -3×2^61 |
| Resultado | s4 = 0x20000000 | s4 = 0x60000000 | s4 = 0xA0000000 |
| | s3 = 0x00000000 | s3 = 0x00000000 | s3 = 0x00000000 |

### División y Resto

- Con signo: div, rem
- Sin signo: divu, remu

### Sucursales (ramas con signo y sin signo)

- Con signo: blt, bge
- Sin signo: bltu, bgeu

Ejemplos: s1 = 0x80000000; s2 = 0x40000000

- `blt s1, s2`: s1 = -2^31; s2 = 2^30 → tomado
- `bltu s1, s2`: s1 = 2^31; s2 = 2^30 → no tomado

### Establecer menor que

- Con signo: slt, slti
- Sin signo: sltu, sltiu

*Nota: RISC-V siempre extiende-signo lo inmediato, incluso para sltiu.*

Ejemplos: s1 = 0x80000000; s2 = 0x40000000

| Instrucción | Interpretación | Resultado |
| --- | --- | --- |
| slt t0, s1, s2 | s1 = -2^31; s2 = 2^30 | t0 = 1 |
| sltu t1, s1, s2 | s1 = 2^31; s2 = 2^30 | t1 = 0 |
| slti t2, s1, -1 | s1 = -2^31; imm = 0xFFFFFFFF = -1 | t2 = 1 |
| sltiu t3, s1, -1 | s1 = 2^31; imm = 0xFFFFFFFF = 2^32-1 | t3 = 1 |

### Cargas (con signo y sin signo)

- Con signo:
  - El signo se extiende para crear un valor de 32 bits para cargar en el registro
  - Cargar media palabra: lh
  - Cargar byte: lb
- Sin signo:
  - Extensión de cero para crear valor de 32 bits
  - Cargar media palabra sin firmar: lhu
  - Cargar byte sin firmar: lbu

### Detección de desbordamiento

- RISC-V no proporciona detección de desbordamiento en suma sin signo, porque se puede hacer con instrucciones existentes:

Ejemplo: detección de desbordamiento sin signo:

```asm
add t0, t1, t2
bltu t0, t1, desbordamiento
```

Ejemplo: detección de desbordamiento con signo:

```asm
add t0, t1, t2
slti t3, t2, 0             # t3=1 si t2 neg.
slt t4, t0, t1              # t4=1 si resultado < t1
bne t3, t4, desbordamiento  # desbordamiento si (t3 != t4)
```

## Instrucciones comprimidas

### Instrucciones comprimidas

- Instrucciones RISC-V de 16 bits
- Reemplace las instrucciones de punto flotante y entero común con versiones de 16 bits.
- La mayoría de los compiladores/procesadores RISC-V pueden usar una combinación de instrucciones de 32 y 16 bits (y usar instrucciones de 16 bits siempre que sea posible).
- Usa el prefijo: c.
- Ejemplos:
  - add → c.add
  - lw → c.lw
  - addi → c.addi

### Ejemplo de instrucciones comprimidas

**Código C:**

```c
int i;
int scores[200];

for (i=0; i<200; i=i+1)
  scores[i] = scores[i]+10;
```

**Código ensamblador RISC-V:**

```asm
# s0 = scores base address, s1 = i
c.li s1, 0             # i = 0
addi t2, zero, 200      # t2 = 200
for:
  bge  s1, t2, done      # i >= 200? done
  c.lw a3, 0(s0)         # a3 = scores[i]
  c.addi a3, 10          # a3 = scores[i]+10
  c.sw a3, 0(s0)         # scores[i] = a3
  c.addi s0, 4           # next element
  c.addi s1, 1           # i = i+1
  c.j  for                # repeat
done:
```

- 200 es demasiado grande para caber en un inmediato comprimido, por lo que no está comprimido: se usó addi en su lugar.
- `c.addi s0,4` es equivalente a `addi s0,s0,4`.
- c.bge no existe, por lo que se usa bge.

### Formatos de máquina comprimidos

- Algunas instrucciones comprimidas utilizan un código de registro de 3 bits (en lugar de 5 bits). Estos especifican los registros x8 a x15.
- Los inmediatos son de 6 a 11 bits.
- El código de operación es de 2 bits.

### Formatos de máquina comprimidos: campos

*Diagrama de la diapositiva: tabla de los formatos de instrucción comprimidos de 16 bits de RISC-V (CR-Type, CI-Type, CS-Type, CS'-Type, CB-Type, CB'-Type, CJ-Type, CSS-Type, CIW-Type, CL-Type), mostrando la posición de bits (15 a 0) de los campos funct3/funct4/funct6, rd/rs1, rs2, imm y op en cada formato. El layout bit a bit exacto no se pudo recuperar por completo de la extracción OCR.*

## Instrucciones de punto flotante

### Extensiones de punto flotante RISC-V

RISC-V ofrece tres extensiones de coma flotante:

- RVF: precisión simple (32 bits) — 8 bits de exponente, 23 bits de fracción
- RVD: doble precisión (64 bits) — 11 bits de exponente, 52 bits de fracción
- RVQ: precisión cuádruple (128 bits) — 15 bits de exponente, 112 bits de fracción

### Registros de punto flotante

- 32 registros de punto flotante
- El ancho es la precisión más alta; por ejemplo, si se implementa RVQ, los registros tienen un ancho de 128 bits
- Cuando se implementan múltiples extensiones de punto flotante, los valores de menor precisión ocupan los bits inferiores del registro

### Registros de coma flotante

| Nombre | Número de registro | Uso |
| --- | --- | --- |
| ft0-7 | f0-7 | Variables temporales |
| fs0-1 | f8-9 | Variables guardadas |
| fa0-1 | f10-11 | Argumentos de función/Valores devueltos |
| fa2-7 | f12-17 | Argumentos de función |
| fs2-11 | f18-27 | Variables guardadas |
| ft8-11 | f28-31 | Variables temporales |

### Instrucciones de punto flotante

- Agregue .s (simple), .d (doble), .q (cuádruple) para mayor precisión. Es decir, fadd.s, fadd.d y fadd.q.
- Operaciones aritméticas: fadd, fsub, fdiv, fsqrt, fmin, fmax, multiplicar y sumar (fmadd, fmsub, fnmadd, fnmsub)
- Otras instrucciones:
  - mover (fmv.xw, fmv.wx)
  - convertir (fcvt.ws, fcvt.sw, etc.)
  - comparación (feq, flt, fle)
  - Clasificar (fclass)
  - inyección de signo (fsgnj, fsgnjn, fsgnjx)

Consulte el Apéndice B para obtener instrucciones adicionales de coma flotante de RISC-V.

### Suma y multiplicación de punto flotante

- fmadd es la instrucción más crítica para los programas de procesamiento de señales.
- Requiere cuatro registros.

```asm
fmadd.f f1, f2, f3, f4   # f1 = f2 x f3 + f4
```

### Ejemplo de punto flotante

**Código C:**

```c
int i;
float scores[200];

for (i=0; i<200; i=i+1)
  scores[i] = scores[i]+10;
```

**Código ensamblador RISC-V:**

```asm
# s0 = scores base address, s1 = i
addi s1, zero, 0        # i = 0
addi t2, zero, 200       # t2 = 200
addi t0, zero, 10        # ft0 = 10.0
fcvt.s.w ft0, t0
for:
  bge  s1, t2, done       # i>=200? done
  slli t0, s1, 2          # t0 = i*4
  add  t0, t0, s0         # scores[i] address
  flw  ft1, 0(t0)         # ft1 = scores[i]
  fadd.s ft1, ft1, ft0     # ft1 = scores[i]+10
  fsw  ft1, 0(t0)         # scores[i] = ft1
  addi s1, s1, 1          # i = i+1
  j    for                  # repeat
done:
```

### Formatos de instrucciones de punto flotante

- Usar formatos de tipo R, I y S
- Introducir otro formato para instrucciones de suma y multiplicación que tienen 4 operandos de registro: tipo R4

| 31:27 | 26:25 | 24:20 | 19:15 | 14:12 | 11:7 | 6:0 |
| --- | --- | --- | --- | --- | --- | --- |
| rs3 | funct2 | rs2 | rs1 | funct3 | rd | op |
| 5 bits | 2 bits | 5 bits | 5 bits | 3 bits | 5 bits | 7 bits |

## Excepciones

### Excepciones

- Llamada de función no programada al controlador de excepciones
- Causado por:
  - Hardware, también llamado interrupción, por ejemplo, teclado
  - Software, también llamado trap, por ejemplo, instrucción indefinida
- Cuando ocurre una excepción, el procesador:
  - Registra la causa de la excepción.
  - Salta al controlador de excepciones
  - Vuelve al programa

### Causas de excepción

| Excepción | Causa |
| --- | --- |
| 0 | Dirección de instrucción desalineada |
| 1 | Fallo de acceso a la instrucción |
| 2 | Instrucción ilegal |
| 3 | Punto de ruptura |
| 4 | Dirección de lectura desalineada |
| 5 | Fallo de acceso de lectura |
| 6 | Dirección de escritura desalineada |
| 7 | Error de acceso de escritura |
| 8 | Llamada de entorno de U-Mode |
| 9 | Llamada de entorno desde S-Mode |
| 11 | Llamada de entorno desde M-Mode |

### Niveles de privilegio de RISC-V

- En RISC-V, las excepciones ocurren en varios niveles de privilegio.
- Los niveles de privilegio limitan el acceso a la memoria o ciertas instrucciones (privilegiadas).
- Los modos de privilegio de RISC-V son (de mayor a menor):
  - máquina (bare metal)
  - de sistema (sistema operativo)
  - de usuario (programa de usuario)
  - hipervisor (para admitir máquinas virtuales)
- Por ejemplo, un programa que se ejecuta en modo M (modo máquina) puede acceder a toda la memoria o instrucciones; tiene el nivel de privilegio más alto.

### Registros de excepción

- Cada nivel de privilegio tiene registros para manejar excepciones
- Estos registros se denominan registros de control y estado (CSR)
- Discutimos las excepciones del modo M (modo máquina), pero otros modos son similares
- Los registros en modo M utilizados para manejar excepciones son: mtvec, mcause, mepc, mscratch

(Del mismo modo, los registros de excepción del modo S son: stvec, scause, sepc, mscratch; y así sucesivamente para los demás modos).

### Registros de excepción: detalle

- Los CSR no forman parte del archivo de registro
- CSR en modo M utilizados para manejar excepciones:
  - mtvec: contiene la dirección del código del controlador de excepciones
  - mcause: registra causa de excepción
  - mepc (Excepción PC): registra la PC donde ocurrió la excepción
  - mscratch: espacio libre en la memoria para los controladores de excepciones

### Instrucciones relacionadas con excepciones

- Instrucciones privilegiadas (llamadas así porque acceden a los CSR):
  - csrr: lectura de registro CSR
  - csrw: Escritura de registro CSR
  - csrrw: lectura/escritura del registro CSR
  - mret: vuelve a la dirección contenida en mepc

Ejemplos:

```asm
csrr t1, mcausa     # t1 = mcausa
csrw mepc, t2        # mepc = t2
csrrw t0, mscratch, t1   # t0 = mscratch
```

### Resumen del controlador de excepciones

- Cuando un procesador detecta una excepción:
  - Salta a la dirección del controlador de excepciones en mtvec
  - El controlador de excepciones entonces:
    - guarda registros en una pila pequeña a la que apunta mscratch
    - Utiliza csrr (lectura de CSR) para buscar la causa de la excepción (en mcause)
    - Maneja la excepción
  - Cuando finaliza, opcionalmente incrementa mepc en 4 y restaura registros de la memoria
  - Y luego cancela el programa o regresa al código de usuario (usando mret, que regresa a la dirección contenida en mepc)

### Ejemplo de código de controlador de excepciones

Compruebe si hay dos tipos de excepciones:

- Instrucción ilegal (mcause = 2)
- Dirección de carga desalineada (mcause = 4)

### Ejemplo de código de controlador de excepciones: código

```asm
csrrw t0, mscratch, t0     # swap t0 y mscratch
sw t1, 0(t0)                 # [mscratch] = t1
sw t2, 4(t0)                 # [mscratch+4] = t2
csrr t1, mcausa              # t1 = mcausa
addi t2, x0, 2                # t2=2 (código de excepción de instrucción ilegal)
entradailegal:
bne t1, t2, comprobarotro    # rama si no es una instrucción ilegal
csrr t2, mepc                 # t2 = excepción PC
addi t2, t2, 4                 # incremento excepción PC
csrw mepc, t2                  # mepc = t2
j hecho
comprobarotro:
addi t2, x0, 4                 # t2=4 (código de excepción de dirección de carga desalineada)
bne t1, t2, hecho              # bifurcación si no es una carga desalineada
j salir                          # programa de salida
hecho:
lw t1, 0(t0)                    # t1 = [mscratch]
lw t2, 4(t0)                    # t2 = [mscratch+4]
csrrw t0, mscratch, t0          # swap t0 y mscratch
mret                              # volver al programa
salir:
...
```

*Comprueba dos tipos de excepciones: instrucción ilegal (mcause = 2) y dirección de carga desalineada (mcause = 4).*

## Resumen instrucciones
