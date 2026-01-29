---
title: "C"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - c
---


## T1: Introducción a la Programación


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

### Conceptos Fundamentales

- **Programa**: Consta de *código* y *datos*, y se define como una secuencia de instrucciones que opera sobre datos.
- **Lenguajes de Programación**:
  - Lenguaje máquina (binario) y lenguajes de alto nivel (como C).
  - Compiladores traducen el código a lenguaje máquina.
- **Compilación y Depuración**: Permite transformar el código fuente en ejecutables y corregir errores.
- **Entrada y Salida**: Interacción del programa con el usuario o dispositivos externos.

### Estructura de Memoria

- **Memoria Volátil (SRAM y SDRAM)**: Almacena variables temporales y se borra al apagar el dispositivo.
- **Memoria No Volátil (PROM, EEPROM, FLASH, MRAM)**: Almacena el código y datos permanentes, vitales en aplicaciones como las misiones espaciales.

### Programación en C

- **Lenguaje de Bajo Nivel**: Ensamblador; adecuado para manipulación directa de memoria.
- **Lenguaje C**:
  - Permite manejar bajo y alto nivel, ideal para programación de sistemas y aplicaciones científicas.
  - Popular en software crítico, como el *software de vuelo* en misiones espaciales (ej. NASA y ESA).

### Ejemplo en C: Algoritmo de Euclides

```c
int main() {
    int m, n;
    m = getInt();
    n = getInt();
    while (n > 0) {
        int r = m % n;
        m = n;
        n = r;
    }
    return m;
}
```

---

## T2: Variables y Operadores en C

### Declaración de Variables

- **Formato Básico**: `tipo nombre = valor_inicial;`
  - Ejemplo: `int velocidad = 9600;`
- **Reglas de Identificadores**:
  - Deben comenzar con una letra o guion bajo.
  - No pueden ser palabras reservadas ni contener caracteres especiales.

### Tipos de Datos en C

1. **Entero (`int`)**: Puede tener tamaños diferentes según la arquitectura.
2. **Carácter (`char`)**: Almacena caracteres ASCII, también puede tratarse como un entero de 8 bits.
3. **Punto Flotante (`float`, `double`)**: Maneja números decimales, con `double` permitiendo más precisión.

### Modificadores de Tipo

- **short** y **long**: Modifican el tamaño de enteros.
- **signed** y **unsigned**: Especifican si una variable es con o sin signo.

### Constantes

- Uso del modificador `const` para declarar valores inmutables, ej. `const int PI = 3.1416;`.

### Operadores en C

- **Aritméticos**: `+`, `-`, `*`, `/`, `%` para operaciones básicas.
- **Relacionales**: `==`, `!=`, `>`, `<`, `>=`, `<=` para comparaciones.
- **Lógicos**: `&&`, `||`, `!` para operaciones de lógica booleana.

### Sentencias y Estructuras de Control

1. **Condicionales**:
   - `if`, `else` y `switch` permiten decisiones en el flujo del programa.
2. **Bucles**:
   - `while`, `do-while` y `for` para iteración.
3. **Sentencias de Control de Flujo**:
   - `break` y `continue` manejan el flujo en bucles.
   - `return` termina una función y devuelve un valor.
¡Claro! Vamos a revisar estos conceptos fundamentales en C: **punteros**, **`malloc` y `free`** (para manejo de memoria dinámica), y el modificador **`volatile`**.

---

## 1. Punteros en C

Un puntero es una variable que almacena la dirección de memoria de otra variable. Trabajar con punteros permite manipular datos directamente en memoria, acceder a arrays, manipular cadenas y trabajar con estructuras de datos dinámicas como listas y árboles.

### Declaración y Uso Básico de Punteros

- **Declaración**: Se usa `*` para declarar un puntero.
  ```c
  int x = 10;
  int *ptr = &x;  // ptr ahora apunta a la dirección de x
  ```
- **Dereferencia**: `*ptr` accede al valor almacenado en la dirección de memoria a la que apunta `ptr`.
  ```c
  printf("%d\n", *ptr);  // Imprime 10, el valor de x
  ```

### Punteros y Arrays

Los punteros y los arrays están estrechamente relacionados:
  ```c
  int arr[] = {1, 2, 3};
  int *p = arr;  // `p` apunta al primer elemento de arr (arr[0])
  printf("%d\n", *(p + 1));  // Imprime 2 (arr[1])
  ```

### Punteros a Punteros

Un puntero a puntero es una variable que contiene la dirección de otro puntero.
  ```c
  int a = 5;
  int *ptr = &a;
  int **ptr_to_ptr = &ptr;  // Puntero a puntero
  printf("%d\n", **ptr_to_ptr);  // Imprime 5
  ```

---

## 2. `malloc` y `free` (Manejo de Memoria Dinámica)

En C, el manejo de memoria dinámica se hace con funciones como `malloc` (memory allocation) y `free` (liberación de memoria).

### `malloc`

`malloc` reserva un bloque de memoria en el heap (memoria dinámica) y devuelve un puntero al primer byte de este bloque. El tamaño se especifica en bytes.

- **Sintaxis**:
  ```c
  int *ptr = (int *)malloc(sizeof(int) * 5);  // Reserva espacio para 5 enteros
  ```
  Si `malloc` falla en asignar memoria (por ejemplo, si no hay suficiente espacio), devolverá `NULL`.

### `free`

Después de usar memoria asignada con `malloc`, es esencial liberar esta memoria usando `free`. Esto ayuda a evitar *fugas de memoria*.

- **Sintaxis**:
  ```c
  free(ptr);  // Libera el bloque de memoria apuntado por ptr
  ```
  > Nota: Llamar a `free` no cambia el valor del puntero, por lo que es buena práctica establecer el puntero a `NULL` después de liberar la memoria (`ptr = NULL;`).

### Ejemplo de Uso Completo

```c
int *array = (int *)malloc(10 * sizeof(int));  // Reserva memoria para 10 enteros

if (array != NULL) {
    for (int i = 0; i < 10; i++) {
        array[i] = i * 2;  // Inicializa el array
    }
    // Uso de array...
}

free(array);  // Libera la memoria asignada
array = NULL; // Previene el uso de punteros colgantes
```

---

## 3. Modificador `volatile`

`volatile` es un modificador que indica al compilador que una variable puede ser modificada inesperadamente por factores externos al programa, como hardware o interrupciones. Esto previene que el compilador optimice el acceso a esa variable, garantizando que siempre se lea su valor actual.

### Uso Común de `volatile`

1. **Variables de Hardware**: Cuando una variable representa el estado de un dispositivo que puede cambiar fuera del control del programa.
2. **Variables en Multihilo**: Si una variable puede ser modificada por varios hilos o en un contexto de interrupción.

### Ejemplo de `volatile`

```c
volatile int sensor_status;  // Se lee cada vez del sensor

while (sensor_status == 0) {
    // Espera hasta que el sensor cambie el estado
}
```

> **Nota**: Usar `volatile` evita que el compilador almacene `sensor_status` en un registro para optimizar el código, asegurando que siempre lea el valor actualizado desde la memoria.

---

### Resumen de Usos

- **Punteros**: Acceso directo y manipulación de memoria.
- **`malloc` y `free`**: Gestión de memoria dinámica, esencial para estructuras complejas en C.
- **`volatile`**: Controla el acceso a variables sujetas a cambios inesperados, útil en sistemas embebidos y programación concurrente.

Estos conceptos son claves para aprovechar al máximo el potencial de C, especialmente en el desarrollo de sistemas y aplicaciones de bajo nivel.

¡Claro! Vamos a profundizar en los **punteros a punteros** y los **punteros a función** en C, dos características que permiten una gran flexibilidad y poder en la programación, especialmente en estructuras de datos complejas y en el manejo de funciones de manera dinámica.

---

## 1. Puntero a Puntero

Un **puntero a puntero** es un puntero que almacena la dirección de otro puntero. Esto permite crear **estructuras jerárquicas** o **matrices dinámicas** y pasar punteros por referencia a funciones.

### Utilidad de Punteros a Punteros

1. **Matrices Dinámicas**: En C, puedes usar punteros a punteros para crear matrices 2D dinámicas. Cada elemento en la primera dimensión apunta a un array, permitiendo construir una estructura flexible y de tamaño variable.

2. **Paso de Punteros por Referencia**: Si quieres que una función modifique un puntero, puedes pasar un puntero a ese puntero. Esto es útil en funciones que asignan memoria con `malloc` y devuelven el puntero asignado a la memoria.

### Ejemplo: Matriz Dinámica

Aquí, `matriz` es un puntero a puntero que se utiliza para crear una matriz de enteros:

```c
int **matriz;
int filas = 3, columnas = 4;

// Reserva memoria para un array de punteros (filas)
matriz = (int **)malloc(filas * sizeof(int *));
for (int i = 0; i < filas; i++) {
    // Reserva memoria para cada fila (array de enteros)
    matriz[i] = (int *)malloc(columnas * sizeof(int));
}

// Asignar valores
matriz[0][0] = 1;
matriz[1][2] = 5;

// Liberar memoria
for (int i = 0; i < filas; i++) {
    free(matriz[i]);
}
free(matriz);
```

En este ejemplo:
- `matriz` apunta a un array de punteros, donde cada puntero apunta a un array de enteros. Esto permite una estructura tipo matriz de tamaño flexible.

### Ejemplo: Paso de Punteros por Referencia

Si necesitas asignar memoria en una función y devolver el resultado mediante un puntero:

```c
void asignar_memoria(int **ptr) {
    *ptr = (int *)malloc(10 * sizeof(int));  // Asigna memoria al puntero original
}

int main() {
    int *array = NULL;
    asignar_memoria(&array);  // Pasa la dirección de array
    array[0] = 5;  // Ahora podemos usar array con la memoria asignada

    free(array);  // Libera la memoria después de su uso
}
```

Aquí:
- Pasamos `&array` a `asignar_memoria`, que permite que la función modifique el puntero original (`array`) y le asigne memoria.

---

## 2. Punteros a Función

Un **puntero a función** es un puntero que almacena la dirección de una función, permitiendo invocar funciones de manera dinámica y pasar funciones como parámetros. Esto es útil para construir **callbacks** y **tablas de funciones**, entre otros.

### Declaración de un Puntero a Función

- Para declarar un puntero a función, especifica el tipo de retorno y los parámetros de la función a la que apunta. Por ejemplo, para una función que toma dos `int` y devuelve un `int`:
  
  ```c
  int (*func_ptr)(int, int);
  ```

### Ejemplo: Uso Básico de Puntero a Función

Definimos un puntero a función y lo usamos para invocar una función:

```c
int sumar(int a, int b) {
    return a + b;
}

int main() {
    int (*operacion)(int, int) = &sumar;  // Puntero a función sumar
    int resultado = operacion(5, 3);  // Llama a sumar(5, 3)
    printf("%d\n", resultado);  // Imprime 8
}
```

Aquí:
- `operacion` es un puntero que apunta a `sumar`, permitiendo invocar `sumar` usando el puntero.

### Ejemplo: Callback con Puntero a Función

Los punteros a función son útiles para callbacks, donde puedes pasar una función como argumento a otra función:

```c
#include <stdio.h>

void ejecutar(int (*func)(int, int), int x, int y) {
    printf("Resultado: %d\n", func(x, y));
}

int multiplicar(int a, int b) {
    return a * b;
}

int main() {
    ejecutar(multiplicar, 3, 4);  // Ejecuta la función multiplicar
}
```

Aquí:
- `ejecutar` recibe un puntero a función como argumento y puede llamar a esa función con los parámetros `x` y `y`.

### Ejemplo: Tabla de Funciones

Usar un array de punteros a función para implementar una tabla de funciones:

```c
#include <stdio.h>

int sumar(int a, int b) { return a + b; }
int restar(int a, int b) { return a - b; }

int main() {
    int (*operaciones[2])(int, int) = { sumar, restar };

    printf("Suma: %d\n", operaciones[0](5, 3));  // Llama a sumar(5, 3)
    printf("Resta: %d\n", operaciones[1](5, 3));  // Llama a restar(5, 3)
}
```

Aquí:
- `operaciones` es un array de punteros a función. Puedes invocar las funciones `sumar` y `restar` dinámicamente según el índice.

---

### Resumen de Usos

- **Punteros a Punteros**: Eficientes para trabajar con estructuras multidimensionales y para pasar punteros a funciones de manera que puedan modificar el puntero original.
- **Punteros a Función**: Permiten ejecutar funciones dinámicamente, crear callbacks y construir tablas de funciones, proporcionando flexibilidad y modularidad.

Estos conceptos son esenciales para una programación en C avanzada y ofrecen control sobre estructuras y lógica del programa.