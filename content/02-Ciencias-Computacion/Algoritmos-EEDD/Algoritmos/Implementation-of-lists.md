---
title: "Implementation Of Lists"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a explorar en detalle las **implementaciones del List ADT**, cubriendo las principales técnicas: **arrays (vectores)**, **listas enlazadas simples**, **listas doblemente enlazadas**, **listas circulares**, y **cursores**.

Te mostraré su estructura, ventajas/desventajas, complejidades, ejemplos visuales y cuándo elegir cada una.

---

##  1. **Implementación con Arrays (estática o dinámica)**


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/List-ADT|List ADT]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]].

###  Estructura

```pseudocode
list = record
  elements[1..maxlength] of ITEM
  last: integer  // número de elementos actuales
endrecord
```

- `elements[i]`: accede directamente al elemento i.
    
- `last`: indica cuántos elementos hay.
    

###  Ejemplo

```pseudocode
insert(x, pos, L):
  for i = L.last down to pos:
    L.elements[i+1] = L.elements[i]
  L.elements[pos] = x
  L.last = L.last + 1
```

###  Ventajas

- Acceso aleatorio en **O(1)**.
    
- Implementación sencilla.
    

###  Desventajas

- Inserción/borrado en medio: **O(n)** (hay que desplazar).
    
- Tamaño fijo si no es dinámico.
    

###  Complejidad

|Operación|Coste|
|---|---|
|`insert`|O(n)|
|`delete`|O(n)|
|`retrieve`|O(1)|
|`locate`|O(n)|
|`next`|O(1)|
|`previous`|O(1)|

---

##  2. **Lista enlazada simple (singly-linked list)**

###  Estructura

```pseudocode
node = record
  value: ITEM
  next: pointer to node
endrecord

list = pointer to primer nodo
```

Cada nodo apunta al siguiente. El último apunta a `null`.

###  Ejemplo

```pseudocode
insert(x, pos):
  nuevo := new node
  nuevo.value := x
  nuevo.next := pos.next
  pos.next := nuevo
```

###  Ventajas

- Inserción/borrado en **O(1)** si conoces la posición.
    
- Crece dinámicamente.
    

###  Desventajas

- Acceso por índice es **O(n)**.
    
- No se puede retroceder.
    

###  Complejidad

|Operación|Coste|
|---|---|
|`insert`|O(1)|
|`delete`|O(1)|
|`retrieve`|O(1)|
|`locate`|O(n)|
|`next`|O(1)|
|`previous`|O(n)|

---

##  3. **Lista doblemente enlazada (doubly-linked list)**

###  Estructura

```pseudocode
node = record
  value: ITEM
  next: pointer to node
  prev: pointer to node
endrecord

list = pointer a nodo cabecera
```

Cada nodo conoce a su anterior y siguiente.

###  Ventajas

- Recorrido hacia adelante y atrás.
    
- `previous` en **O(1)**.
    
- Muy útil en estructuras como listas de historial.
    

###  Desventajas

- Consume más memoria (2 punteros por nodo).
    
- Inserción/borrado más complejos (mantenimiento de punteros).
    

---

##  4. **Lista circular**

- El último nodo apunta al primero.
    
- Puede ser simple o doble.
    

```pseudocode
nodo.final.next = nodo.inicio
```

 Útil para algoritmos que requieren recorrido cíclico (como en round-robin scheduling).

---

##  5. **Implementación con Cursores (en arrays)**

Para lenguajes **sin punteros**, como pseudocódigo educativo o JavaScript de bajo nivel.

###  Estructura

```pseudocode
SPACE[1..N] = array de nodos
cada nodo = (element, next)
```

- La posición en el array actúa como "dirección".
    
- Se mantiene una lista de "espacios disponibles".
    

###  Ventajas

- Simula punteros sin necesidad de direcciones de memoria reales.
    
- Control total del espacio.
    

---

##  Comparación resumen

|Implementación|Acceso aleatorio|Inserción/Borrado rápido|Uso de memoria|Flexibilidad|
|---|---|---|---|---|
|Array| O(1)| O(n)|Eficiente|Estática o dinámica|
|Lista enlazada| O(n)| O(1)|Más costosa|Dinámica|
|Doble enlazada| O(n)| O(1) (más compleja)|Más costosa|Muy flexible|
|Lista circular| O(n)| (para ciclos)|Igual que enlazada|Cíclica|
|Cursores| O(n)||Eficiente|Simulada|

---

##  Conclusión

> Las listas pueden implementarse de múltiples formas, y **cada implementación tiene ventajas según el uso**:  
> rapidez, memoria, acceso aleatorio, recorrido en ambas direcciones o compatibilidad con lenguajes.

---

¿Quieres que te prepare ejemplos en código real (C, Java, Python) con punteros o arrays? ¿O te interesa ver visualmente cómo se comportan las operaciones en una lista enlazada o circular?