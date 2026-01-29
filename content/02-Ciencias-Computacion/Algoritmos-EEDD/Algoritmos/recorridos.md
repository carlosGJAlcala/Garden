---
title: "Recorridos"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a explicar a fondo los **recorridos (traversals)** en **árboles** y **grafos**, incluyendo:

1. Tipos de **traversals en árboles binarios**: preorder, inorder, postorder
    
2. **Traversals en grafos**: DFS (Depth-First Search) y BFS (Breadth-First Search)
    
3. Cuándo usar cada uno y su relación con algoritmos clásicos
    
4. Implementaciones y complejidades
    

---

##  1. **Recorridos en Árboles Binarios**


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

Los **recorridos** de árboles consisten en visitar **todos los nodos** de un árbol **en un orden sistemático**.  
Para **árboles binarios**, hay tres formas clásicas, definidas de forma **recursiva**.

###  a) **Preorden (Preorder)** – N, I, D

> Visita el **nodo actual**, luego el **subárbol izquierdo**, luego el **derecho**.

```pseudocode
procedure preorder(node)
  if node ≠ null:
    visitar(node)
    preorder(node.left)
    preorder(node.right)
```

 Usos:

- Serialización de árboles
    
- Evaluación de árboles de expresión (prefijo)
    

---

###  b) **Inorden (Inorder)** – I, N, D

> Visita el **izquierdo**, luego el **nodo actual**, luego el **derecho**.

```pseudocode
procedure inorder(node)
  if node ≠ null:
    inorder(node.left)
    visitar(node)
    inorder(node.right)
```

 Usos:

- Para **árboles binarios de búsqueda (BST)** devuelve los elementos en orden.
    

---

###  c) **Postorden (Postorder)** – I, D, N

> Visita el **izquierdo**, luego el **derecho**, y al final el **nodo actual**.

```pseudocode
procedure postorder(node)
  if node ≠ null:
    postorder(node.left)
    postorder(node.right)
    visitar(node)
```

 Usos:

- Liberación de memoria (liberar hijos antes que el padre).
    
- Evaluación de expresiones postfijas (RPN).
    

---

##  Ejemplo de los tres

Dado el árbol:

```
       A
      / \
     B   C
    / \
   D   E
```

- **Preorden**: A, B, D, E, C
    
- **Inorden**: D, B, E, A, C
    
- **Postorden**: D, E, B, C, A
    

---

##  2. **Recorridos en Grafos**

En grafos, como puede haber ciclos, hay que **marcar los nodos visitados** para no entrar en bucle.

---

###  a) **DFS (Depth-First Search)**

> Explora todo el camino por un vecino antes de retroceder.

```pseudocode
procedure dfs(v)
  marcar v como visitado
  for cada w ∈ vecinos(v):
    if w no visitado:
      dfs(w)
```

 Usos:

- Detectar ciclos
    
- Componentes conexas
    
- Backtracking (sudoku, laberintos)
    
- Orden topológico (DAG)
    

**Implementación**: recursiva o con **pila (stack)**

---

###  b) **BFS (Breadth-First Search)**

> Visita primero todos los vecinos, luego los vecinos de los vecinos.

```pseudocode
procedure bfs(v)
  marcar v como visitado
  enqueue(v)

  while cola no vacía:
    u := dequeue()
    for cada w ∈ vecinos(u):
      if w no visitado:
        marcar w
        enqueue(w)
```

 Usos:

- Caminos mínimos en grafos sin pesos
    
- Detección de niveles
    
- IA y búsqueda de soluciones óptimas
    

**Implementación**: con **cola (queue)**

---

##  Complejidades

|Recorrrido|Tiempo|Espacio (extra)|
|---|---|---|
|Árbol (todos)|O(n)|O(h)|
|DFS (grafo)|O(n + e)|O(n)|
|BFS (grafo)|O(n + e)|O(n)|

- n = número de nodos
    
- e = número de aristas
    
- h = altura del árbol
    

---

##  Aplicaciones reales

|Traversal|Usos prácticos|
|---|---|
|Preorden|Serializar estructuras, construir árboles|
|Inorden|Obtener elementos ordenados (en BST)|
|Postorden|Eliminar jerarquías, evaluar expresiones|
|DFS|Laberintos, análisis de dependencias, árbol de juego|
|BFS|Caminos más cortos, propagación, IA con soluciones óptimas|

---

##  Conclusión

> Los **recorridos (traversals)** son herramientas clave para **visitar sistemáticamente estructuras jerárquicas (árboles) o relacionales (grafos)**.  
> Elegir el tipo adecuado depende de la **estructura** y el **problema que resuelves**.

---

¿Te gustaría que prepare una simulación visual de DFS y BFS? ¿O ejemplos en código Python o Java para cada uno, aplicados a casos reales como laberintos, rutas o expresiones matemáticas?