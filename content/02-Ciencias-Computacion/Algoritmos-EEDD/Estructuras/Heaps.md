---
title: "Heaps"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
Muy buena pregunta. Vamos a explicar qué son los **heaps** (montículos), cómo funcionan como **estructura de datos (Heap ADT)** y su relación con el **heap de memoria** del sistema. Aunque comparten nombre, **son conceptos distintos pero relacionados por la idea de "estructura jerárquica y dinámica"**.

---

##  1. **Heap como estructura de datos (Heap ADT)**


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/HeapSort|HeapSort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

###  ¿Qué es un Heap?

Un **heap** es un **árbol binario completo** que satisface una propiedad de orden específica:

- **Max-Heap**: el padre siempre es **mayor o igual** que sus hijos.
    
- **Min-Heap**: el padre siempre es **menor o igual** que sus hijos.
    

> La raíz siempre contiene el **valor máximo (max-heap)** o **mínimo (min-heap)** de todo el árbol.

###  Ejemplo de Min-Heap:

```
       1
      / \
     3   5
    / \
   6   8
```

---

###  Operaciones básicas del Heap ADT

|Operación|Descripción|Coste|
|---|---|---|
|`insert(x)`|Inserta elemento y lo posiciona ("bubble up")|O(log n)|
|`deleteMin()` / `deleteMax()`|Elimina el valor raíz y reordena ("heapify down")|O(log n)|
|`findMin()` / `findMax()`|Devuelve el valor raíz|O(1)|

###  Implementación

Un heap **no se implementa como árbol con punteros**, sino como **array**:

- El padre en índice `i`:
    
    - hijo izquierdo: `2i`
        
    - hijo derecho: `2i+1`
        
    - padre: `floor(i/2)`
        

---

##  ¿Para qué se usan los Heaps?

- **Colas con prioridad**: ejecutar primero las tareas de mayor prioridad.
    
- **Algoritmos de grafos**: Dijkstra, Prim.
    
- **Heapsort**: algoritmo de ordenación con O(n log n).
    
- **Simulaciones**: eventos por tiempo (event queue).
    
- **Sistemas operativos**: planificación por prioridades.
    

---

##  2. **Heap como región de memoria (Heap Memory)**

Ahora, pasamos al otro uso del término **"heap"**: la **zona de memoria dinámica** que gestiona el sistema operativo o el runtime.

---

###  ¿Qué es el heap de memoria?

El **heap de memoria** es una **región de RAM** usada para **asignación dinámica**:

- Cuando usas `malloc()` en C o `new` en Java, Python, C#, etc.
    
- Los objetos creados **viven en el heap** hasta que los liberas (C/C++) o el **GC** (garbage collector) los recoja (Java, Python).
    

###  Comparación rápida: Stack vs Heap

|Aspecto|Stack (pila)|Heap (memoria dinámica)|
|---|---|---|
|Acceso|Rápido, automático|Más lento, dinámico|
|Vida|Local, temporal (función)|Global, hasta que se libere|
|Asignación|Estática o automática|Dinámica (`malloc`, `new`, etc.)|
|Control|Sistema|Programador o Garbage Collector|
|Tamaño|Pequeño|Grande|
|Uso|Variables locales, llamadas|Objetos, estructuras grandes|

---

###  Ejemplo en C

```c
int* p = malloc(sizeof(int) * 10);  // Asigna en el heap
*p = 5;
free(p);  // Libera manualmente
```

###  Ejemplo en Java

```java
Person p = new Person();  // El objeto vive en el heap
```

---

##  ¿Cómo se relacionan _Heap ADT_ y _Heap Memory_?

Aunque son cosas distintas, hay puntos de conexión:

|Conexión|Explicación|
|---|---|
|Ambas son "montículos"|El término "heap" sugiere una **estructura sin forma fija**, como un montón|
|Estructuras dinámicas|El Heap ADT **se almacena en heap memory** (si lo implementas en C, Java...)|
|Operaciones con punteros|Un `heap` de datos gestiona sus nodos mediante **índices o referencias**|
|Uso de memoria eficiente|Los heaps pueden crecer dinámicamente, como lo hace el heap de RAM|

> En resumen, **puedes implementar un Heap ADT dentro del heap de memoria del sistema**.

---

##  Conclusión

|Término|Definición breve|
|---|---|
|**Heap ADT**|Estructura de datos jerárquica usada para colas de prioridad|
|**Heap de memoria**|Región de RAM usada para crear objetos y estructuras dinámicas|

>  Aunque comparten nombre, uno es **una estructura lógica**, y el otro es **una zona física de memoria**, pero **se relacionan en que ambos permiten manejar datos dinámicos con flexibilidad**.

---

 w