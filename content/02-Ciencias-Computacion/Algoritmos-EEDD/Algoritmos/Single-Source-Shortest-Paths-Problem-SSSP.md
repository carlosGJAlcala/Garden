---
title: "Single Source Shortest Paths Problem Sssp"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---

# Single Source Shortest Paths Problem (SSSP)

## ¿Qué es el problema SSSP?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Priority-queues|Priority queues]].

Dado un **grafo dirigido o no dirigido con pesos no negativos** y un **nodo fuente `s`**, el problema consiste en encontrar el **camino más corto desde `s` hacia todos los demás nodos del grafo**.

> Se busca minimizar la **suma de los pesos de las aristas** desde el nodo fuente hasta cada nodo.

---

##  ¿Qué es el algoritmo de Dijkstra?

Es un **algoritmo voraz (greedy)** que resuelve el SSSP cuando **todas las aristas tienen pesos no negativos**.

###  Idea clave:

- Comienza en el nodo fuente.
    
- En cada paso, **elige el nodo alcanzable más cercano** (de menor coste total acumulado).
    
- **Actualiza los caminos mínimos a sus vecinos**.
    
- Repite hasta visitar todos los nodos.
    

---

##  Representación del grafo

- Grafo dirigido: G=(V,E)G = (V, E)
    
- Pesos: w(u,v)≥0w(u, v) ≥ 0
    
- Fuente: s∈Vs ∈ V
    

---

##  Estructuras necesarias

- `dist[v]`: distancia mínima conocida desde `s` hasta `v`
    
- `prev[v]`: nodo anterior en el camino más corto (opcional)
    
- `Q`: conjunto de nodos no visitados, implementado como **priority queue** (heap)
    

---

## ️ Pseudocódigo de Dijkstra

```pseudocode
procedure Dijkstra(G, s)
  for each vertex v in G:
    dist[v] := ∞
    prev[v] := null
  dist[s] := 0

  Q := todos los vértices de G

  while Q ≠ vacío:
    u := nodo en Q con menor dist[u]
    eliminar u de Q

    para cada vecino v de u:
      alt := dist[u] + peso(u, v)
      if alt < dist[v]:
        dist[v] := alt
        prev[v] := u
```

---

##  Ejemplo paso a paso

Grafo:

```
   (A)
  /   \
 1     4
/       \
(B)---3--(C)
```

Pesos:

- A→B: 1
    
- A→C: 4
    
- B→C: 3
    

Desde A:

- dist[A] = 0
    
- dist[B] = 1 (A→B)
    
- dist[C] = 1 + 3 = 4 (A→B→C) — mejor que A→C (4)
    

Resultado:

- Camino más corto A→B→C con costo 4
    

---

##  Complejidad temporal

|Estructura usada|Complejidad|
|---|---|
|Priority Queue + Lista|O(n²)|
|Priority Queue + Heap|**O((n + e) log n)**|

- n = número de nodos
    
- e = número de aristas
    

> Con un **binary heap + listas de adyacencia**, el rendimiento es eficiente para grafos dispersos.

---

## ️ Restricción importante

Dijkstra **no funciona con aristas de peso negativo**.  
En ese caso se usa **Bellman-Ford**.

---

##  Usos reales de Dijkstra

- GPS y navegación (Google Maps, Waze)
    
- Reducción de latencia en redes
    
- Algoritmos de juegos y pathfinding (A* usa una variante de Dijkstra)
    
- Análisis de redes (enrutamiento, dependencias)
    
- Planificación logística y cadenas de suministro
    

---

##  Ejemplo en Python (simplificado)

```python
import heapq

def dijkstra(graph, start):
    dist = {node: float('inf') for node in graph}
    dist[start] = 0
    pq = [(0, start)]

    while pq:
        current_dist, u = heapq.heappop(pq)
        if current_dist > dist[u]:
            continue
        for v, weight in graph[u]:
            alt = current_dist + weight
            if alt < dist[v]:
                dist[v] = alt
                heapq.heappush(pq, (alt, v))
    return dist
```

Ejemplo de grafo:

```python
graph = {
  'A': [('B', 1), ('C', 4)],
  'B': [('C', 3)],
  'C': []
}
```

---

##  Conclusión

> **Dijkstra's Algorithm** es una solución eficiente al problema del camino más corto desde una fuente, **siempre que no existan aristas de peso negativo**.  
> Combinado con **priority queues (heaps)**, logra rendimientos óptimos para grafos reales y dispersos.

---