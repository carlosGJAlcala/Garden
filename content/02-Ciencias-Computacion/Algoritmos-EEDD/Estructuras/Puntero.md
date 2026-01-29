---
title: "Puntero"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
Vamos a desarrollar el concepto de **punteros** en profundidad, incluyendo su estructura, uso práctico, ventajas, peligros, aplicaciones y ejemplos reales.

---

##  ¿Qué es un puntero?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

Un **puntero** es una variable cuyo **contenido es una dirección de memoria**. Es decir, **no guarda un valor directamente, sino la ubicación donde está ese valor** en la memoria.

> En lugar de contener el número `42`, contiene algo como `0x7ffeefbff58c`, que es la dirección donde está guardado el `42`.

---

##  ¿Para qué sirven los punteros?

- Para **acceder y modificar datos indirectamente** (por referencia).
    
- Para **crear estructuras dinámicas**: listas enlazadas, árboles, grafos, colas, etc.
    
- Para **optimizar rendimiento**, evitando copiar grandes cantidades de datos.
    
- Para **compartir datos entre funciones o estructuras**.
    
- Para **gestionar memoria dinámica** en tiempo de ejecución (`malloc`, `free`).
    

---

##  Sintaxis general (ej. C/C++)

```c
int x = 10;         // variable normal
int* p = &x;        // p apunta a x
printf("%d", *p);   // accede al contenido de x a través del puntero
```

### Elementos clave:

- `*p`: desreferencia → accede al valor apuntado por `p`
    
- `&x`: referencia → da la dirección de memoria de `x`
    

---

##  Ejemplo: Lista enlazada con punteros

```c
typedef struct Node {
    int valor;
    struct Node* siguiente;
} Node;

Node* cabeza = NULL;  // lista vacía

// Crear primer nodo
Node* nuevo = malloc(sizeof(Node));
nuevo->valor = 10;
nuevo->siguiente = NULL;

cabeza = nuevo;
```

Aquí estás **reservando memoria dinámica**, enlazando nodos entre sí mediante punteros.

---

##  Tipos de punteros comunes

|Tipo|Descripción|
|---|---|
|`int*`|Puntero a entero|
|`char*`|Puntero a carácter (usado en strings)|
|`void*`|Puntero genérico (sin tipo definido)|
|`struct tipo*`|Puntero a estructura (listas, árboles, etc.)|
|`NULL`|Valor especial que indica que un puntero no apunta a nada|

---

## ️ Peligros de los punteros

Los punteros son muy potentes, pero también **peligrosos si se usan mal**. Algunos problemas comunes:

1. **Punteros colgantes (dangling pointers):**
    
    - Acceder a memoria que ya ha sido liberada.
        
    
    ```c
    free(p);
    *p = 42; // error
    ```
    
2. **Fugas de memoria:**
    
    - No liberar memoria dinámica (`malloc` sin `free`).
        
    - Puede acumularse y agotar los recursos del sistema.
        
3. **Punteros nulos:**
    
    - Acceder a un puntero no inicializado (`NULL`).
        
4. **Acceso fuera de límites:**
    
    - Puntero apuntando fuera de un array, corrompiendo memoria.
        

---

##  ¿Dónde se usan los punteros realmente?

###  En sistemas de bajo nivel:

- Sistemas operativos, drivers, firmware.
    
- Ej. manejo de procesos, buffers, punteros a funciones, estructuras complejas.
    

###  En estructuras de datos:

- Listas enlazadas, pilas, árboles, grafos, montículos (heaps).
    

###  En programación con C/C++:

- Gestión directa de memoria, arrays dinámicos, paso de argumentos por referencia.
    

###  En programación de alto rendimiento:

- En videojuegos, procesamiento de señales, gráficos 3D, simulaciones científicas.
    

---

##  Comparativa: Punteros vs Variables normales

|Característica|Variable normal|Puntero|
|---|---|---|
|Guarda un valor|Sí|No, guarda una dirección|
|Acceso a datos|Directo (`x`)|Indirecto (`*p`)|
|Permite estructuras dinámicas|No|Sí|
|Requiere memoria fija|Sí|No, puede reservar dinámicamente|
|Uso compartido de datos|Por copia|Por referencia|

---

##  Conclusión

> Un **puntero es una herramienta de bajo nivel que permite manipular datos y estructuras de forma eficiente y dinámica**. Es fundamental en estructuras de datos avanzadas y sistemas donde el rendimiento y el control de memoria son críticos.

---

Perfecto. Vamos a profundizar en los **doble punteros** (`**`) —una de las herramientas más potentes y a veces confusas en lenguajes como **C y C++**— y que tienen aplicaciones muy importantes en estructuras dinámicas, manipulación de punteros desde funciones, y más.

---

##  ¿Qué es un doble puntero?

Un **doble puntero** (`int** p`) es un **puntero que apunta a otro puntero**.  
Es decir:

- `int* p`: un puntero a un entero.
    
- `int** pp`: un puntero a un puntero a un entero.
    

> Puedes imaginarlo como una “caja” que contiene la dirección de otra “caja”, que a su vez contiene la dirección del valor real.

---

##  Visualización (en C)

```c
int x = 10;
int* p = &x;      // p apunta a x
int** pp = &p;    // pp apunta a p
```

 Accesos:

- `x`: valor → `10`
    
- `p`: dirección de `x`
    
- `*p`: valor de `x` → `10`
    
- `pp`: dirección de `p`
    
- `*pp`: valor de `p` → dirección de `x`
    
- `**pp`: valor de `x` → `10`
    

---

##  ¿Para qué sirven los doble punteros?

###  1. **Modificar punteros desde funciones**

C no pasa punteros por referencia; por tanto, para modificar el puntero original dentro de una función, se necesita un puntero al puntero.

```c
void asignarMemoria(int** p) {
    *p = malloc(sizeof(int));
    **p = 42;
}
```

Uso:

```c
int* ptr;
asignarMemoria(&ptr);
printf("%d", *ptr);  // Imprime 42
```

---

###  2. **Matrices dinámicas (arrays de arrays)**

Una matriz dinámica es esencialmente un **puntero a puntero**:

```c
int** matriz = malloc(filas * sizeof(int*));
for (int i = 0; i < filas; i++) {
    matriz[i] = malloc(columnas * sizeof(int));
}
```

Así accedes a `matriz[i][j]` como en una matriz normal.

> Este enfoque es fundamental para estructuras dinámicas multidimensionales.

---

###  3. **Listas enlazadas y estructuras complejas**

En listas enlazadas, usar doble puntero permite modificar la cabeza (head) directamente desde una función:

```c
typedef struct Nodo {
    int valor;
    struct Nodo* siguiente;
} Nodo;

void insertarInicio(Nodo** cabeza, int valor) {
    Nodo* nuevo = malloc(sizeof(Nodo));
    nuevo->valor = valor;
    nuevo->siguiente = *cabeza;
    *cabeza = nuevo;
}
```

Llamada desde main:

```c
Nodo* lista = NULL;
insertarInicio(&lista, 10);
```

---

##  Ejemplo completo: insertar en lista enlazada

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Nodo {
    int valor;
    struct Nodo* siguiente;
} Nodo;

void insertarInicio(Nodo** cabeza, int valor) {
    Nodo* nuevo = malloc(sizeof(Nodo));
    nuevo->valor = valor;
    nuevo->siguiente = *cabeza;
    *cabeza = nuevo;
}

void imprimir(Nodo* cabeza) {
    while (cabeza != NULL) {
        printf("%d -> ", cabeza->valor);
        cabeza = cabeza->siguiente;
    }
    printf("NULL\n");
}

int main() {
    Nodo* lista = NULL;
    insertarInicio(&lista, 30);
    insertarInicio(&lista, 20);
    insertarInicio(&lista, 10);
    imprimir(lista);  // 10 -> 20 -> 30 -> NULL
    return 0;
}
```

---

## ️ Peligros de los doble punteros

- **Complejidad mental**: pueden ser difíciles de leer y entender si se abusa de ellos.
    
- **Errores de desreferenciación**: `*pp`, `**pp`, `***ppp`… errores comunes.
    
- **Fugas de memoria** si no se libera correctamente cada nivel de puntero.
    
- **Fácil de perder el control** sobre la gestión de la memoria cuando hay punteros que apuntan a punteros que apuntan a memoria dinámica.
    

---

##  Conclusión

> Los **doble punteros** (`**`) permiten:
> 
> - Pasar punteros por referencia a funciones.
>     
> - Gestionar estructuras de datos complejas como listas, árboles o matrices dinámicas.
>     
> - Tener un control total sobre la memoria y la estructura de los datos.
>     

---

¿Quieres que prepare un ejemplo de uso de **triple puntero** (`***`) o matrices 3D dinámicas? ¿O prefieres ver cómo esto se usa en estructuras como árboles binarios o colas dinámicas?