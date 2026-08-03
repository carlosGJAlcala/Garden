---
title: "Stack Adt"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---

# Stack ADT (Tipo Abstracto de Datos Pila)

Definición formal, operaciones, usos reales, implementación, complejidad y ejemplos en pseudocódigo y código real.

---

## ¿Qué es un Stack (pila)?

Una **pila** es una estructura de datos **lineal** donde los elementos se insertan y eliminan **por un solo extremo**, llamado el **tope (top)**.

> Sigue la regla **LIFO** → **Last In, First Out**  
> El último en entrar es el primero en salir.

---

##  Stack ADT – Especificación

###  Operaciones fundamentales del Stack ADT:

|Operación|Descripción|
|---|---|
|`push(item)`|Inserta un elemento en la cima (top) de la pila|
|`pop()`|Elimina el elemento de la cima y lo retorna|
|`top()` o `peek()`|Retorna el elemento de la cima **sin eliminarlo**|
|`empty()`|Devuelve `true` si la pila está vacía|
|`makenull()`|Reinicia la pila (la vacía por completo)|

---

##  Ejemplo conceptual

Supón que apilas platos:

```
Top → [ plato5 ]
        plato4
        plato3
        plato2
Bottom→[ plato1 ]
```

- Si haces `push(plato6)`, se pone encima de `plato5`.
    
- Si haces `pop()`, `plato6` es el que se va.
    
- `top()` devuelve `plato6` sin quitarlo.
    

---

##  Pseudocódigo para Stack ADT

```pseudocode
spec STACK[ITEM]
genres stack, item

operations
  push: stack × item → stack
  pop: stack → item
  top: stack → item
  empty: stack → boolean
  makenull: stack → stack
endspec
```

---

## ️ Implementaciones comunes

### 1. Array (estática o dinámica)

```pseudocode
stack = record
  items[1..maxsize]: array of ITEM
  top: integer
endrecord
```

- `push`: `items[++top] = item`
    
- `pop`: `return items[top--]`
    

### 2. Lista enlazada (dinámica)

```pseudocode
node = record
  value: ITEM
  next: pointer to node
endrecord

stack = pointer to node (top)
```

- `push`: crear nodo, apuntar a top, mover top
    
- `pop`: guardar top, mover top, liberar nodo
    

---

##  Complejidad temporal

|Operación|Array|Lista enlazada|
|---|---|---|
|`push`|O(1)|O(1)|
|`pop`|O(1)|O(1)|
|`top`|O(1)|O(1)|
|`empty`|O(1)|O(1)|
|`makenull`|O(1)|O(1) o O(n)*|

* Si liberas nodos, puede ser O(n)

---

##  Usos reales del Stack ADT

- **Recursión**: pila de llamadas del sistema (call stack).
    
- **Evaluación de expresiones**: conversión infija → posfija, evaluación de RPN.
    
- **Deshacer/rehacer**: en editores, navegadores (historial).
    
- **Backtracking**: algoritmos de exploración (DFS, puzzles, juegos).
    
- **Compiladores**: verificación de paréntesis, símbolos anidados, análisis sintáctico.
    

---

##  Ejemplo en código real (Python)

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

    def top(self):
        return self.items[-1]

    def empty(self):
        return len(self.items) == 0
```

---

##  Ejemplo en pseudocódigo: evaluación con backspace

Entrada: `abc##d#e` → Salida: `ae`

```pseudocode
procedure procesarTexto(texto)
  s := new stack
  for cada caracter c en texto:
    if c == '#' then
      if not s.empty() then
        s.pop()
    else
      s.push(c)
  endfor

  imprimir contenido de s en orden inverso
end procedure
```

---

##  Conclusión

> Un **Stack ADT** es simple pero extremadamente poderoso.  
> Su capacidad para manejar **estructuras reversibles, recursivas o de exploración** lo hace fundamental en lenguajes de programación, algoritmos, compiladores y lógica de sistemas.

---