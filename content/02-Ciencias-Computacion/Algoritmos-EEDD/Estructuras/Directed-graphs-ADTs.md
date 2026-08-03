---
title: "Directed Graphs Adts"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---

# Directed Graph ADTs (Grafos Dirigidos)

Tipos Abstractos de Datos para grafos dirigidos, que permiten representar relaciones unidireccionales entre entidades. Esenciales en análisis de redes, algoritmos de búsqueda, compiladores, grafos de dependencia, control de flujo, etc.

---

## ¿Qué es un grafo dirigido?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/recorridos|recorridos]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Un **grafo dirigido** (digraph) es una estructura matemática compuesta por:

- Un conjunto de **vértices (nodos)**: VV
    
- Un conjunto de **arcos (aristas dirigidas)**: E⊆V×VE \subseteq V \times V
    

Cada arco es un **par ordenado**: (u,v)(u, v), lo que significa que va **de u hacia v**, y no al revés.

---

##  Directed Graph ADT – Especificación abstracta

###  Operaciones típicas

|Operación|Descripción|
|---|---|
|`addVertex(v)`|Añade un nuevo vértice|
|`addEdge(u, v)`|Crea una arista dirigida de `u` a `v`|
|`removeEdge(u, v)`|Elimina la arista `u → v`|
|`adjacent(u, v)`|Retorna `true` si hay una arista de `u` a `v`|
|`neighbors(v)`|Retorna los vértices adyacentes desde `v`|
|`inDegree(v)` / `outDegree(v)`|Grados de entrada/salida del nodo `v`|
|`traverseDFS(v)` / `traverseBFS(v)`|Recorrido en profundidad o amplitud desde `v`|

---

##  Representaciones internas

###  1. **Matriz de adyacencia (Adjacency Matrix)**

- Usa una **matriz booleana** A[n][n]A[n][n]
    
- Si hay una arista de `i → j`, entonces `A[i][j] = true`
    

####  Ventajas:

- Acceso a `adjacent(i, j)` en **O(1)**
    
- Ideal para grafos densos
    

####  Desventajas:

- Ocupa **O(n²)** espacio, incluso si hay pocas aristas
    

---

###  2. **Lista de adyacencia (Adjacency List)**

- Para cada nodo, se guarda una lista de vecinos a los que apunta
    

```pseudocode
graph = array[1..n] of list

graph[2] = [3, 4]  // nodo 2 tiene aristas hacia 3 y 4
```

####  Ventajas:

- Mucho más eficiente en espacio para grafos dispersos: O(n + e)
    
- Recorrer vecinos de un nodo es más natural
    

####  Desventajas:

- Comprobar existencia de una arista `u → v` cuesta **O(k)** (k = vecinos de u)
    

---

##  Ejemplo de ADT en pseudocódigo

```pseudocode
spec DIGRAPH[VERTEX]
genres graph, vertex, index

operations
  addVertex: graph × vertex → graph
  addEdge: graph × vertex × vertex → graph
  adjacent: graph × vertex × vertex → boolean
  neighbors: graph × vertex → list of vertex
  first: vertex → index
  next: vertex × index → index
  vertex: vertex × index → vertex
endspec
```

---

##  Recorridos sobre digraphs

###  DFS (Depth-First Search)

```pseudocode
procedure dfs(v)
  mark v as visited
  for each w in neighbors(v):
    if w not visited:
      dfs(w)
```

###  BFS (Breadth-First Search)

```pseudocode
procedure bfs(v)
  mark v as visited
  enqueue v into queue
  while queue not empty:
    u = dequeue
    for each w in neighbors(u):
      if w not visited:
        mark w
        enqueue w
```

---

##  Operaciones derivadas y útiles

- **Detectar ciclos**
    
- **Orden topológico** (en DAGs – grafos acíclicos dirigidos)
    
- **Cálculo de caminos mínimos**: (Dijkstra, Bellman-Ford)
    
- **Cálculo de componentes fuertemente conexas**
    

---

##  Usos reales de digraphs

- **Compiladores**: dependencia entre módulos/clases
    
- **Workflows**: procesos que dependen de otros
    
- **Redes sociales**: seguidores en Twitter (A sigue a B ≠ B sigue a A)
    
- **Control de flujo en programas**: flujo entre bloques de código
    
- **Análisis de tráfico**: rutas con dirección
    
- **Bases de datos**: modelos de herencia o dependencias entre entidades
    

---

##  Complejidad por representación

|Operación|Matriz de adyacencia|Lista de adyacencia|
|---|---|---|
|`addEdge(u, v)`|O(1)|O(1)|
|`removeEdge(u, v)`|O(1)|O(k)|
|`adjacent(u, v)`|O(1)|O(k)|
|`neighbors(u)`|O(n)|O(k)|
|`space complexity`|O(n²)|O(n + e)|

---

##  Conclusión

> El **Directed Graph ADT** permite modelar **relaciones direccionales** entre objetos. Su representación más eficiente depende de la **densidad del grafo** y del tipo de operaciones que necesites priorizar.  
> Es fundamental para algoritmos de caminos, ordenaciones, dependencias y control de flujo.

---