---
title: "List Adt"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---

# List ADT (Tipo Abstracto de Datos Lista)

El List ADT es uno de los ADT más fundamentales y flexibles. Las listas permiten **almacenar secuencias ordenadas de elementos** y realizar **operaciones dinámicas** como inserción, borrado, recorrido y búsqueda.

---

## ¿Qué es una Lista?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Una **lista** es una secuencia ordenada de elementos donde:

- Los elementos están **organizados por posición** (1er, 2do, …, n-ésimo).
    
- Se puede insertar o eliminar elementos en cualquier posición.
    
- Puede crecer o decrecer dinámicamente.
    

 A diferencia de pilas o colas, **no se restringe el acceso a los extremos**.

---

##  List ADT – Especificación formal

###  Operaciones fundamentales

|Operación|Descripción|
|---|---|
|`insert(item, pos)`|Inserta `item` en la posición `pos`|
|`delete(pos)`|Elimina el elemento en la posición `pos`|
|`locate(item)`|Retorna la posición del primer elemento igual a `item`|
|`retrieve(pos)`|Retorna el elemento en la posición `pos`|
|`next(pos)`|Retorna la siguiente posición|
|`previous(pos)`|Retorna la posición anterior|
|`makenull()`|Vacía la lista|
|`empty()`|Devuelve `true` si la lista está vacía|
|`first()`|Retorna la primera posición válida|
|`end()`|Retorna una posición "después del último"|
|`length()`|Número de elementos|
|`modify(pos, new_item)`|Modifica el elemento en `pos`|
|`onlist(item)`|Devuelve `true` si `item` está en la lista|

---

##  Pseudocódigo del List ADT

```pseudocode
spec LIST[ITEM]
genres list, item, position

operations
  insert: item × position × list → list
  delete: position × list → list
  locate: item × list → position
  retrieve: position × list → item
  next: position × list → position
  previous: position × list → position
  makenull: list → list
  empty: list → boolean
  first: list → position
  end: list → position
  length: list → natural
  modify: position × list × item → list
  onlist: item × list → boolean
endspec
```

---

## ️ Implementaciones comunes

###  1. Array (vector)

```pseudocode
list = record
  items[1..maxsize]: array of ITEM
  last: integer  // posición del último elemento
endrecord
```

- Ventajas: acceso rápido por índice (`O(1)`)
    
- Desventajas: insertar/borrar en medio → requiere desplazar (`O(n)`)
    

---

###  2. Lista enlazada (punteros)

```pseudocode
node = record
  value: ITEM
  next: pointer to node
endrecord

list = pointer to primer nodo
```

- Ventajas: inserción y borrado en `O(1)` si tienes el puntero correcto
    
- Desventajas: acceso por posición es `O(n)`
    

 Variantes:

- **Listas doblemente enlazadas**
    
- **Listas circulares**
    
- **Listas con nodo centinela (dummy)**
    

---

##  Complejidad temporal (por operación)

|Operación|Array|Lista enlazada|
|---|---|---|
|`insert`|O(n)|O(1) (si ya tienes el puntero)|
|`delete`|O(n)|O(1)|
|`retrieve`|O(1)|O(n)|
|`locate`|O(n)|O(n)|
|`next/previous`|O(1)|O(1) / O(n) (a menos que sea doble)|
|`empty`|O(1)|O(1)|

---

##  Usos reales del List ADT

- **Sistemas operativos**: gestión de tareas, buffers.
    
- **Compiladores**: listas de tokens, listas de instrucciones.
    
- **Interfaces gráficas**: listas de elementos (eventos, componentes).
    
- **Bases de datos**: listas de resultados de consultas.
    
- **Inteligencia artificial**: listas de nodos abiertos y cerrados (como en A*).
    
- **Lenguajes como Lisp, Prolog**: las listas son el tipo de datos dominante.
    

---

##  Ejemplo en pseudocódigo: eliminar duplicados

```pseudocode
procedure eliminarDuplicados(lista)
  p := first(lista)
  while p ≠ end(lista) do
    q := next(p, lista)
    while q ≠ end(lista) do
      if retrieve(p, lista) = retrieve(q, lista) then
        delete(q, lista)
      else
        q := next(q, lista)
    end
    p := next(p, lista)
  end
end procedure
```

---

##  Ejemplo en código real (Python, como clase)

```python
class Lista:
    def __init__(self):
        self.items = []

    def insert(self, item, pos):
        self.items.insert(pos, item)

    def delete(self, pos):
        del self.items[pos]

    def retrieve(self, pos):
        return self.items[pos]

    def locate(self, item):
        return self.items.index(item) if item in self.items else -1

    def empty(self):
        return len(self.items) == 0

    def length(self):
        return len(self.items)
```

---

##  Conclusión

> El **List ADT** es una estructura extremadamente versátil que permite **manipular secuencias de datos dinámicamente**.  
> Su riqueza de operaciones la hace **ideal para estructuras base en compiladores, procesamiento de texto, interpretes, motores de búsqueda, entornos gráficos, IA y más**.

---