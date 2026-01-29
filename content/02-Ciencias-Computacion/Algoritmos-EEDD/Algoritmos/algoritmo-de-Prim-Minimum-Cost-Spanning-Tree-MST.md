---
title: "Algoritmo De Prim Minimum Cost Spanning Tree Mst"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a desarrollar completamente el algoritmo de **Prim** para encontrar un **Minimum-Cost Spanning Tree (MST)** en un grafo no dirigido y conexo. Este algoritmo es fundamental en optimización de redes, telecomunicaciones, planificación de infraestructuras y algoritmos de grafos.

---

##  ¿Qué es un Spanning Tree?


> **Relacionado**: [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

Un **árbol de expansión** (_spanning tree_) de un grafo **conexo y no dirigido** es un **subgrafo acíclico** que:

- **Conecta todos los vértices**
    
- Tiene exactamente **n − 1 aristas** (donde n = número de vértices)
    

 **Minimum-cost spanning tree**: el spanning tree cuya **suma de pesos de aristas es mínima**.

---

##  ¿Qué hace Prim’s algorithm?

El **algoritmo de Prim** construye un árbol de expansión mínimo **agregando nodos uno por uno**. En cada paso:

- Se agrega **la arista de menor peso** que conecta un nodo dentro del árbol con uno fuera.
    

> Usa una estrategia **greedy (voraz)**.

---

##  Requisitos del grafo

- Grafo **no dirigido**
    
- **Conexo**
    
- Las aristas tienen **pesos no negativos**
    

---

##  Estructura del algoritmo

### Estructuras clave:

- `U`: conjunto de nodos incluidos en el árbol actual (empieza con un solo nodo)
    
- `T`: conjunto de aristas del árbol
    
- Cola de prioridad con los **nodos frontera** (fuera del árbol) y sus **pesos mínimos conocidos**
    

---

##  Pseudocódigo (Prim con heap)

```pseudocode
procedure Prim(G, start)
  for each vertex v in G:
    key[v] := ∞
    parent[v] := null
  key[start] := 0

  Q := conjunto de todos los nodos

  while Q ≠ vacío:
    u := nodo en Q con menor key[u]
    eliminar u de Q

    para cada vecino v de u:
      if v ∈ Q and peso(u, v) < key[v]:
        parent[v] := u
        key[v] := peso(u, v)
```

El árbol final está definido por las aristas `parent[v] → v`

---

##  Complejidad

|Implementación|Complejidad|
|---|---|
|Lista + búsqueda lineal|O(n²)|
|Heap binario + listas|**O((n + e) log n)**|
|Fibonacci heap|O(e + n log n)|

---

##  Ejemplo gráfico simple

```
     (A)
   1 /   \ 4
   (B)---(C)
      3

Pesos: A-B = 1, A-C = 4, B-C = 3

Prim desde A:
1. Empieza en A
2. A–B (peso 1)
3. B–C (peso 3, mejor que A–C)
→ MST = {A–B, B–C}, coste total = 4
```

---

##  Ejemplo en Python (simplificado)

```python
import heapq

def prim(graph, start):
    visited = set()
    min_heap = [(0, start, None)]
    mst = []

    while min_heap:
        cost, u, parent = heapq.heappop(min_heap)
        if u in visited:
            continue
        visited.add(u)
        if parent:
            mst.append((parent, u, cost))
        for v, weight in graph[u]:
            if v not in visited:
                heapq.heappush(min_heap, (weight, v, u))
    return mst
```

Grafo ejemplo:

```python
graph = {
  'A': [('B', 1), ('C', 4)],
  'B': [('A', 1), ('C', 3)],
  'C': [('A', 4), ('B', 3)]
}
```

---

##  Aplicaciones reales

- **Diseño de redes de computadoras o fibra óptica**
    
- **Rutas eléctricas** (tendido mínimo de cable)
    
- **Construcción de carreteras** entre ciudades
    
- **Infraestructuras mínimas de transporte**
    
- **Clusterización en Machine Learning** (algoritmos jerárquicos)
    

---

##  Comparación con Kruskal

|Característica|Prim|Kruskal|
|---|---|---|
|Enfoque|Expande desde un nodo|Añade aristas ordenadas|
|Estructura principal|Cola de prioridad|Union-Find|
|Mejor para|Grafos densos|Grafos dispersos|
|Necesita estar conexo|Sí|No, devuelve bosque|

---

##  Conclusión

> El **algoritmo de Prim** encuentra el árbol de expansión mínima de forma eficiente, **siempre eligiendo la arista más barata** que conecta el árbol parcial con el resto del grafo.  
> Es especialmente útil cuando trabajas con **grafos densos** y puedes mantener una cola de prioridad eficiente.

---

¿Quieres que lo visualicemos paso a paso con una matriz de adyacencia? ¿O que lo compare con Kruskal con un grafo real? También puedo implementarlo en C, Java o Python, según prefieras.