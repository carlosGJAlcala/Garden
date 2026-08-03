---
title: "Doubly Linked Lists Circular Lists Ordered Lists"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---

# Variantes del List ADT

Tres variantes avanzadas del List ADT:
- **Doubly Linked Lists** (listas doblemente enlazadas)
- **Circular Lists** (listas circulares)
- **Ordered Lists** (listas ordenadas)

---

## 1. **Doubly Linked List (Lista doblemente enlazada)**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/DICCIONARIOS|DICCIONARIOS]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/recorridos|recorridos]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/List-ADT|List ADT]].

###  Estructura

Cada nodo tiene dos punteros: uno al siguiente nodo y otro al anterior.

```pseudocode
node = record
  value: ITEM
  next: pointer to node
  prev: pointer to node
endrecord

list = pointer al primer nodo
```

```
NULL ← [A] ⇄ [B] ⇄ [C] → NULL
```

### ️ Operaciones básicas

- `insertAfter(nodo, nuevo)`
    
- `insertBefore(nodo, nuevo)`
    
- `delete(nodo)`
    
- `traverseForward()` / `traverseBackward()`
    

###  Ventajas

- Puedes recorrer **hacia adelante y atrás**.
    
- Borrar un nodo en O(1) si tienes el puntero.
    
- Ideal para estructuras que requieren **retroceso** (como historial de navegación).
    

###  Desventajas

- Más uso de memoria (2 punteros por nodo).
    
- Mayor complejidad de mantenimiento de enlaces.
    

###  Usos reales

- Navegadores (historial).
    
- Editores de texto (buffers).
    
- Listas de reproducción con retroceso.
    

---

##  2. **Circular List (Lista circular)**

###  Estructura

El último nodo apunta al primero.  
Puede ser simple o doble.

```pseudocode
simple: [A] → [B] → [C] → [A]
doble:  [A] ⇄ [B] ⇄ [C] ⇄ [A]
```

- No hay `NULL`, el recorrido **es infinito** si no lo controlas.
    

### ️ Operaciones clave

- `next(nodo)` siempre es válido.
    
- Puedes insertar en cualquier posición sin necesidad de "fin".
    
- Ideal para estructuras cíclicas.
    

###  Ventajas

- Eficiente para recorrer en **bucle (ciclo)**.
    
- No necesitas reiniciar la lista: `next(last) = first`.
    

###  Desventajas

- Puede generar bucles infinitos si no se controla bien.
    
- Más difícil de depurar.
    

###  Usos reales

- Planificadores round-robin (sistemas operativos).
    
- Juegos de turnos circulares.
    
- Algoritmos de token ring (redes antiguas, procesos).
    

---

##  3. **Ordered List (Lista ordenada)**

###  Estructura

Una lista (enlazada o con array) donde **los elementos se insertan manteniendo un orden** (por clave o valor).

Ejemplo: lista ordenada de enteros crecientes

```
[2] → [5] → [9] → [13]
```

### ️ Operación principal

- `insert(item)` → busca la posición correcta y lo inserta ordenadamente.
    
- `delete`, `locate`, `retrieve` → igual que en listas normales.
    

###  Ventajas

- **`locate` puede optimizarse** (si usas arrays puedes hacer `binary search`).
    
- No hace falta ordenar después: **se mantiene automáticamente**.
    
- Útil como estructura base para diccionarios o listas de prioridad.
    

###  Desventajas

- `insert` siempre es O(n) (hay que buscar la posición).
    
- Acceso por índice en listas enlazadas es costoso.
    
- No permite desorden si lo necesitas.
    

###  Usos reales

- Listas de tareas por prioridad.
    
- Eventos ordenados por tiempo.
    
- Listas de espera por puntuación.
    
- Implementación base de colas con prioridad sin heap.
    

---

##  Comparativa rápida

|Característica|Doubly Linked|Circular|Ordered|
|---|---|---|---|
|Punteros por nodo|2|1 o 2|1 o 2|
|Permite recorrer atrás|| (si es doble)|Opcional|
|Ciclo infinito posible||||
|Inserta en orden||||
|`insert` eficiencia|O(1)*|O(1)*|O(n)|
|Acceso por índice|O(n)|O(n)|O(1) si es array|
|Uso real|Navegadores|Round-robin, OS|Prioridades, colas|

* Si se tiene puntero al nodo previo.

---

##  Conclusión

> Estas variantes del List ADT **ofrecen ventajas específicas según el caso de uso**:

- **Doubly linked**: cuando necesitas ir hacia atrás y hacia adelante.
    
- **Circular**: ideal para recorridos cíclicos sin fin claro.
    
- **Ordered**: cuando necesitas mantener los datos en orden desde el momento de inserción.
    
