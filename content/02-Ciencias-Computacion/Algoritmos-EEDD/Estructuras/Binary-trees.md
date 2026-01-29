---
title: "Binary Trees"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
Perfecto. Vamos a desarrollar a fondo el concepto de **Binary Trees (Árboles Binarios)**: qué son, cómo funcionan, cómo se implementan, sus operaciones clave, usos reales, y cómo se diferencian de otros árboles.

---

##  ¿Qué es un Binary Tree?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/recorridos|recorridos]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

Un **árbol binario** es una estructura de datos jerárquica donde **cada nodo tiene como máximo dos hijos**:

- Un **hijo izquierdo** (`left`)
    
- Un **hijo derecho** (`right`)
    

 A diferencia de un árbol general (n-ario), los binarios **restringen el número de hijos a 2** y **los hijos tienen un orden** (izquierdo ≠ derecho).

---

##  Estructura del nodo

```pseudocode
node = record
  value: ITEM
  left: pointer to node
  right: pointer to node
endrecord

binary_tree = pointer to root node
```

Ejemplo visual:

```
       A
      / \
     B   C
    / \
   D   E
```

---

##  Tipos de árboles binarios

|Tipo|Descripción|
|---|---|
|Árbol binario general|Cada nodo tiene 0, 1 o 2 hijos|
|Árbol binario completo|Todos los niveles llenos salvo quizás el último (de izquierda a derecha)|
|Árbol binario perfecto|Todos los niveles están completamente llenos|
|Árbol binario degenerado|Se comporta como una lista (cada nodo tiene solo un hijo)|
|Árbol binario lleno|Todos los nodos tienen 0 o 2 hijos|

---

##  Recorridos clásicos (tree traversals)

Hay 3 formas principales de **recorrer** un árbol binario:

###  Preorden (N → I → D)

```pseudocode
procedure preorder(n)
  if n ≠ null:
    visitar(n)
    preorder(n.left)
    preorder(n.right)
```

###  Inorden (I → N → D)

```pseudocode
procedure inorder(n)
  if n ≠ null:
    inorder(n.left)
    visitar(n)
    inorder(n.right)
```

###  Postorden (I → D → N)

```pseudocode
procedure postorder(n)
  if n ≠ null:
    postorder(n.left)
    postorder(n.right)
    visitar(n)
```

 _"N"_ = nodo actual, _"I"_ = hijo izquierdo, _"D"_ = hijo derecho.

---

##  Ejemplo simple (inorden)

Para este árbol:

```
       4
      / \
     2   5
    / \
   1   3
```

- **Inorden**: `1, 2, 3, 4, 5`
    
- **Preorden**: `4, 2, 1, 3, 5`
    
- **Postorden**: `1, 3, 2, 5, 4`
    

---

## ️ Operaciones comunes

|Operación|Descripción|
|---|---|
|`insert(valor)`|Inserta un nodo (no necesariamente ordenado, salvo en BST)|
|`search(valor)`|Busca un valor (sólo útil si está ordenado o balanceado)|
|`traverse()`|Recorre el árbol en alguna de las formas (inorden, etc.)|
|`height()`|Calcula la altura del árbol (profundidad máxima)|
|`count()`|Cuenta los nodos totales|

---

##  Complejidad (depende de la altura `h` del árbol)

|Operación|Árbol balanceado (altura log n)|Árbol degenerado (lista)|
|---|---|---|
|Insert|O(log n)|O(n)|
|Search|O(log n)|O(n)|
|Traverse|O(n)|O(n)|

---

##  Ejemplo en pseudocódigo – Insert en árbol binario

```pseudocode
procedure insert(nodo, valor)
  if valor < nodo.valor:
    if nodo.left == null:
      nodo.left := new node(valor)
    else:
      insert(nodo.left, valor)
  else:
    if nodo.right == null:
      nodo.right := new node(valor)
    else:
      insert(nodo.right, valor)
```

> Esto crea un **Binary Search Tree** (BST), donde los menores van a la izquierda, los mayores a la derecha.

---

##  Usos reales de árboles binarios

- **Binary Search Trees (BST)**: búsqueda rápida de datos ordenados.
    
- **Árboles de expresión**: representar expresiones aritméticas.
    
- **Compiladores**: árboles de sintaxis abstracta (AST).
    
- **IA (juegos, decisión)**: árboles de decisión, minimax.
    
- **Indexación**: árbol de sufijos, árboles B (variante balanceada).
    

---

##  Variantes más especializadas

|Tipo de árbol binario|Característica principal|
|---|---|
|BST|Binario de búsqueda (valores ordenados)|
|AVL|BST auto-balanceado (diferencia de alturas ≤ 1)|
|Red-Black Tree|BST balanceado por colores|
|Heap (max/min)|Árbol binario completo con orden parcial|
|Segment Tree / Fenwick|Estructuras avanzadas para rango y actualizaciones rápidas|

---

##  Conclusión

> El **Binary Tree** es la base de estructuras más potentes como BST, heaps, árboles balanceados, árboles de expresión, etc.  
> Su forma recursiva y su eficiencia lo hacen fundamental para algoritmos rápidos y estructuras dinámicas.

---

¿Te gustaría que te prepare una implementación completa en código (Python, Java o C)? ¿O ver cómo aplicar árboles binarios en un caso práctico como ordenar datos, evaluar expresiones o crear un índice?