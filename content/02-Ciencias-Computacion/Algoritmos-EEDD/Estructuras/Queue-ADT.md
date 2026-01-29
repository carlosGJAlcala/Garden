---
title: "Queue Adt"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---


##  ¿Qué es una Cola (Queue)?


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[02-Ciencias-Computacion/Redes/Kafka|Kafka]].

Una **cola** es una estructura de datos lineal basada en la regla **FIFO**:

> **First In, First Out**  
> El primero que entra es el primero que sale.

 Imagínate una fila en una tienda: el primero que llega es el primero en ser atendido.

---

##  Queue ADT – Especificación formal

###  Operaciones fundamentales:

|Operación|Descripción|
|---|---|
|`enqueue(item)`|Inserta un elemento al **final (rear)** de la cola|
|`dequeue()`|Elimina y retorna el elemento del **frente (front)** de la cola|
|`front()`|Retorna el primer elemento sin eliminarlo|
|`empty()`|Devuelve `true` si la cola está vacía|
|`makenull()`|Inicializa o vacía la cola|

---

##  ¿Cómo se comporta?

 Encolado (`enqueue(5)`, `enqueue(10)`)

```
Front → [ 5 ][ 10 ] ← Rear
```

 Desencolado (`dequeue()` devuelve `5`)

```
Front → [ 10 ] ← Rear
```

---

##  Pseudocódigo formal del Queue ADT

```pseudocode
spec QUEUE[ITEM]
genres queue, item

operations
  enqueue: queue × item → queue
  dequeue: queue → item
  front: queue → item
  empty: queue → boolean
  makenull: queue → queue
endspec
```

---

## ️ Implementaciones comunes

###  1. Con array (circular)

```pseudocode
queue = record
  items[0..N-1]: array of ITEM
  front: int
  rear: int
endrecord
```

- `enqueue`: `rear = (rear + 1) mod N; items[rear] = item`
    
- `dequeue`: `front = (front + 1) mod N; return items[front]`
    

> Esta técnica evita tener que mover todos los elementos en cada `dequeue`.

---

###  2. Con lista enlazada

```pseudocode
node = record
  value: ITEM
  next: pointer to node
endrecord

queue = record
  front: pointer to node
  rear: pointer to node
endrecord
```

- `enqueue`: añadir nodo al final (`rear.next`)
    
- `dequeue`: eliminar nodo del principio (`front`)
    

---

##  Complejidad temporal

|Operación|Array circular|Lista enlazada|
|---|---|---|
|`enqueue`|O(1)|O(1)|
|`dequeue`|O(1)|O(1)|
|`front`|O(1)|O(1)|
|`empty`|O(1)|O(1)|

---

##  Usos reales del Queue ADT

- **Sistemas operativos**: planificación de procesos (colas de ejecución).
    
- **Redes**: manejo de paquetes en routers y switches.
    
- **Impresoras**: colas de impresión.
    
- **Procesamiento por lotes / pipelines**.
    
- **BFS (búsqueda en anchura)**: grafos, árboles, resolución de puzzles.
    
- **Sistemas de mensajería y eventos**: colas de mensajes, RabbitMQ, Kafka, etc.
    

---

##  Ejemplo en pseudocódigo: búsqueda BFS

```pseudocode
procedure BFS(nodo_inicial)
  crear cola Q
  marcar nodo_inicial como visitado
  enqueue(Q, nodo_inicial)

  while not Q.empty() do
    nodo := dequeue(Q)
    para cada vecino en vecinos(nodo) do
      si vecino no visitado entonces
        marcar vecino como visitado
        enqueue(Q, vecino)
    end
  end
end procedure
```

---

##  Ejemplo en código real (Python)

```python
from collections import deque

class Queue:
    def __init__(self):
        self.q = deque()

    def enqueue(self, item):
        self.q.append(item)

    def dequeue(self):
        return self.q.popleft()

    def front(self):
        return self.q[0]

    def empty(self):
        return len(self.q) == 0
```

---

##  Conclusión

> El **Queue ADT** es fundamental para **procesar datos en orden de llegada**, con complejidad constante y gran utilidad en **sistemas concurrentes, búsqueda de caminos, procesamiento de eventos, planificación y mensajería**.

---

