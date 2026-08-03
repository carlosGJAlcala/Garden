---
title: "Priority Queues"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---

# Priority Queue (Cola con Prioridad)

La Priority Queue se basa en el **Heap ADT** y es fundamental en algoritmos, sistemas operativos, redes, planificación, simulaciones, IA y muchas otras áreas.

---

## ¿Qué es una Priority Queue?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Queue-ADT|Queue ADT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Una **Priority Queue** es una cola donde **cada elemento tiene una prioridad asociada**, y **el elemento con mayor prioridad se atiende primero**, sin importar el orden en que fue insertado.

> A diferencia de una cola normal (FIFO), **no se atiende el primero en llegar, sino el más importante**.

---

##  Priority Queue ADT – Especificación

###  Operaciones principales

|Operación|Descripción|
|---|---|
|`insert(x, p)`|Inserta el elemento `x` con prioridad `p`|
|`deleteMax()` / `deleteMin()`|Elimina y devuelve el elemento con mayor (o menor) prioridad|
|`peek()`|Devuelve el elemento de mayor prioridad sin eliminarlo|
|`empty()`|Indica si la cola está vacía|

---

##  Tipos de Priority Queue

|Tipo|Orden por prioridad|Estructura usada|
|---|---|---|
|Max-Priority|Mayor prioridad sale primero|Max-Heap|
|Min-Priority|Menor prioridad sale primero|Min-Heap|

---

##  Ejemplo

Supón que insertamos:

```
(“tarea1”, prioridad 5)
(“tarea2”, prioridad 8)
(“tarea3”, prioridad 2)
```

Una cola con prioridad **máxima** devolvería:

```plaintext
deleteMax() → “tarea2”
deleteMax() → “tarea1”
deleteMax() → “tarea3”
```

---

## ️ Implementación: usando Heaps

La estructura **más eficiente** para implementar una Priority Queue es un **heap binario**.

### Con un **array** como heap:

- Insertar: O(log n) usando `heapify-up`
    
- Eliminar máximo/mínimo: O(log n) usando `heapify-down`
    
- Peek: O(1)
    

---

##  Complejidad

|Operación|Complejidad|
|---|---|
|`insert`|O(log n)|
|`deleteMin/Max`|O(log n)|
|`peek`|O(1)|
|`empty`|O(1)|

---

##  Ejemplo en pseudocódigo

```pseudocode
procedure insert(Q, x, p)
  heapInsert(Q.heap, (p, x))  // usa la prioridad como clave en el heap

procedure deleteMax(Q)
  return heapExtractMax(Q.heap)

procedure peek(Q)
  return Q.heap[1]
```

---

##  Ejemplo en Python (usando `heapq` con prioridades negativas para MaxHeap)

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.q = []

    def insert(self, item, priority):
        heapq.heappush(self.q, (-priority, item))  # negamos prioridad para max-heap

    def deleteMax(self):
        return heapq.heappop(self.q)[1]

    def peek(self):
        return self.q[0][1]

    def empty(self):
        return len(self.q) == 0
```

---

##  Usos reales de Priority Queues

###  Algoritmos

- **Dijkstra**: para elegir el nodo más cercano.
    
- **A***: en algoritmos de búsqueda heurística.
    
- **Prim**: mínimo árbol de expansión.
    

###  Sistemas operativos

- Planificación de procesos (scheduling)
    
- Interrupciones por prioridad
    

###  Redes

- Enrutamiento de paquetes
    
- Buffers con prioridad
    

###  Simulación y eventos

- Simulación de eventos con tiempo (event-driven simulation)
    
- Juegos: gestión de turnos
    

---

##  Implementaciones alternativas

|Estructura|Inserción|Eliminación|Estable|Comentario|
|---|---|---|---|---|
|Array ordenado|O(n)|O(1)|No|rápido eliminar, lento insertar|
|Array no ordenado|O(1)|O(n)|No|simple pero ineficiente|
|**Binary Heap**|O(log n)|O(log n)|No|estándar y eficiente|
|Binomial Heap|O(log n)|O(log n)|No|útil en merges frecuentes|
|Fibonacci Heap|O(1)*|O(log n)|No|*Amortizado: usado en teoría|

---

##  Conclusión

> Una **Priority Queue** te permite modelar situaciones donde **el orden de procesamiento depende del “peso” o “urgencia” de los elementos**, no del orden de llegada.  
> Su implementación más eficiente y usada en la práctica es mediante un **heap binario**, lo que permite insertar y extraer el elemento prioritario en **O(log n)**.

---