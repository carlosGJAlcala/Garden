---
title: "Grafos"
---

# Grafos

Estructuras de Datos
Otoño 2021
Luis de Marcos Ortega
luis.demarcos@uah.es

## Índice

- Grafos dirigidos
- Terminología básica
- Representaciones para grafos dirigidos
- TADs de grafos dirigidos
- Problema de caminos más cortos desde un origen único
- Algoritmo de Dijkstra
- Grafos no dirigidos
- Árboles de expansión de costo mínimo
- Algoritmo de Prim
- Recorridos

## Bibliografía

- Capítulos 6 y 7 de:
- A.V. AHO, J.E. HOPCROFT, J.D. ULLMAN. 1987. “Data Structures and Algorithms.” Addison-Wesley.

## Grafos

- En problemas que surgen en informática, matemáticas, ingeniería y muchas otras disciplinas, a menudo necesitamos representar relaciones arbitrarias entre objetos de datos.
- Los grafos dirigidos y no dirigidos son modelos naturales de tales relaciones.

## Terminología básica

- Un grafo dirigido (o dígrafo) G consta de un conjunto de vértices V y un conjunto de aristas E.
  - Los vértices también se llaman nodos o puntos.
  - Las aristas se pueden llamar aristas dirigidas o líneas dirigidas. Una arista es un par ordenado de vértices (v, w).
- La arista (v, w) se expresa a menudo como v → w y se dibuja como.

## Terminología básica

- Ejemplo

*(diagrama no reconstruible a partir de la extracción OCR)*

## Terminología básica

- Los vértices de un dígrafo se pueden utilizar para representar objetos, y las aristas relaciones entre los objetos.
  - Por ejemplo, los vértices podrían representar ciudades y las aristas vuelos aéreos de una ciudad a otra.
  - Otro ejemplo: un dígrafo se puede utilizar para representar el flujo de control en un programa de computadora. Los vértices representan bloques básicos y las aristas posibles transferencias del flujo de control.

## Terminología básica

- Un camino en un dígrafo es una secuencia de vértices v₁, v₂, ..., vₙ, tales que v₁ → v₂, v₂ → v₃, ..., vₙ₋₁ → vₙ son aristas.
  - Este camino va del vértice v₁ al vértice vₙ y pasa a través de los vértices v₂, v₃, ..., vₙ₋₁ y termina en el vértice vₙ.
  - La longitud de un camino es el número de aristas en el camino, en este caso, n-1.

## Terminología básica

- Un ciclo es un camino simple de longitud al menos uno que comienza y termina en el mismo vértice.
- En muchas aplicaciones es útil adjuntar información a los vértices y aristas de un dígrafo. Para este propósito podemos usar un dígrafo etiquetado, un dígrafo en el cual cada arista y/o cada vértice puede tener una etiqueta asociada. Una etiqueta puede ser un nombre, un costo o un valor de cualquier tipo de dato dado.

## Terminología básica

- Ejemplo: Dígrafo de transición — un dígrafo etiquetado en el cual cada arista se etiqueta con una letra que causa una transición de un vértice a otro.

*(diagrama no reconstruible a partir de la extracción OCR)*

## Representaciones para dígrafos

- Una representación común para un dígrafo G = (V, E) es la matriz de adyacencia.
- Supongamos V = {1, 2, ..., n}. La matriz de adyacencia para G es una matriz n × n A de booleanos, donde A[i, j] es verdadero si y solo si hay una arista del vértice i al vértice j.

## Representaciones para dígrafos

- Estrechamente relacionada está la representación de matriz de adyacencia etiquetada de un dígrafo, donde A[i, j] es la etiqueta en la arista que va del vértice i al vértice j. Si no hay una arista de i a j, entonces se debe usar un valor que no pueda ser una etiqueta legítima como la entrada para A[i, j].

## Representaciones para dígrafos

- Matriz de adyacencia etiquetada para el dígrafo anterior

*(diagrama no reconstruible a partir de la extracción OCR)*

## Representaciones para dígrafos

- La principal desventaja de usar una matriz de adyacencia para representar un dígrafo es que la matriz requiere Θ(n²) almacenamiento incluso si el dígrafo tiene muchas menos de n² aristas.
- Simplemente leer o examinar la matriz requeriría O(n²) tiempo, lo que impediría algoritmos O(n) para manipular dígrafos con O(n) aristas.

## Representaciones para dígrafos

- Para evitar esta desventaja podemos usar otra representación común para un dígrafo G = (V, E) llamada representación de lista de adyacencia.
- La lista de adyacencia para un vértice i es una lista, en algún orden, de todos los vértices adyacentes a i. Podemos representar G por un array HEAD, donde HEAD[i] es un puntero a la lista de adyacencia para el vértice i.

## Representaciones para dígrafos

- La representación de lista de adyacencia de un dígrafo requiere almacenamiento proporcional a la suma del número de vértices más el número de aristas; se usa a menudo cuando el número de aristas es mucho menor que n².
- Sin embargo, una desventaja potencial de la representación de lista de adyacencia es que puede tomar O(n) tiempo determinar si hay una arista del vértice i al vértice j, ya que puede haber O(n) vértices en la lista de adyacencia para el vértice i.

## TADs de dígrafos

- Nos vamos a enfocar en describir algoritmos bien conocidos en grafos y no tanto en dar una definición formal de las operaciones en grafos (ya que estas también dependen bastante del problema específico).
- Usamos la noción de un tipo índice para el conjunto de vértices adyacentes a algún vértice v.

## TADs de dígrafos

```
spec GRAPH[node]
genres graph, vertex, index
operations
first: vertex -> index
next: vertex, index -> index
vertex: vertex, index -> vertex
endspec
```

## TADs de dígrafos — Matriz de adyacencia

```
const n := {some suitable constant}
graph = record
  vertexes: array[1..n] of vertex
  arcs: array[1..n, 1..n] of arc
endrecord
vertex: elementtype
arc: boolean {or other suitable}
index: integer
```

## TADs de dígrafos — Lista de adyacencia

```

const n := {some suitable constant}
node = record
vertex: elementtype
next: ^node
endrecord
graph: array[1..n] of node
index: integer

```

## Problema de caminos más cortos desde un origen único

- Se nos da un grafo dirigido G = (V, E) en el cual cada arista tiene una etiqueta no negativa, y un vértice se especifica como la fuente. Nuestro problema es determinar el costo del camino más corto desde la fuente a todos los demás vértices en V, donde la longitud de un camino es simplemente la suma de los costos de las aristas en el camino.

## Problema de caminos más cortos desde un origen único

- Ejemplo:
  - Podemos pensar en G como un mapa de vuelos aéreos, en el cual cada vértice representa una ciudad y cada arista v → w una ruta aérea de la ciudad v a la ciudad w. La etiqueta en la arista v → w es el tiempo para volar de v a w.
  - Resolver el problema de caminos más cortos desde un origen único para este grafo dirigido determinaría el tiempo de viaje mínimo desde una ciudad dada a todas las demás ciudades en el mapa.

## Problema de caminos más cortos desde un origen único

- Para resolver este problema utilizaremos una técnica "greedy" (codicioso), frecuentemente conocida como algoritmo de Dijkstra.
- El algoritmo funciona manteniendo un conjunto S de vértices cuya distancia más corta desde la fuente ya es conocida. Inicialmente, S contiene solo el vértice de la fuente. En cada paso, agregamos a S un vértice restante v cuya distancia desde la fuente es la más corta posible. Suponiendo que todas las aristas tienen costos no negativos, siempre podemos encontrar un camino más corto desde la fuente a v que pase solo a través de vértices en S.

## Algoritmo de Dijkstra

```
proc Dijkstra
  { Dijkstra calcula el costo de los caminos más cortos desde el vértice 1 hasta cada vértice de un grafo dirigido: }
  S := {1};
  for i := 2 to n do
    D[i] := C[1, i]; { inicializar D }
  endfor
  for i := 1 to n-1 do begin
    choose a vertex w in V-S such that D[w] is a minimum;
    add w to S;
    for each vertex v in V-S do
      D[v] := min(D[v], D[w] + C[w, v])
    endfor
  endfor
endproc { Dijkstra }
```

## Algoritmo de Dijkstra

- Ejemplo:
  - Aplicar Dijkstra al grafo dirigido de la figura.
  - Inicialmente, S = {1}

*(diagrama no reconstruible a partir de la extracción OCR)*

## Algoritmo de Dijkstra

- Ejemplo:
  - Secuencia de valores D después de cada iteración

*(diagrama no reconstruible a partir de la extracción OCR)*

## Grafos no dirigidos

- Un grafo no dirigido G = (V, E) consta de un conjunto finito de vértices V y un conjunto de aristas E.
- Difiere de un grafo dirigido en que cada arista en E es un par no ordenado de vértices.
  - Si (v, w) es una arista no dirigida, entonces (v, w) = (w, v).
  - De aquí en adelante nos referiremos a un grafo no dirigido simplemente como grafo.

## Grafos no dirigidos

- Los grafos se utilizan en muchas disciplinas diferentes para modelar una relación simétrica entre objetos. Los objetos se representan por los vértices del grafo y dos objetos están conectados por una arista si los objetos están relacionados.

## Grafos no dirigidos

- Ejemplo de grafo (no dirigido)

*(diagrama no reconstruible a partir de la extracción OCR)*

## Métodos de representación

- Los métodos de representación de grafos dirigidos se pueden usar para representar grafos no dirigidos.
- Simplemente se representa una arista no dirigida entre v y w por dos aristas dirigidas, una de v a w y la otra de w a v.
- Claramente, la matriz de adyacencia para un grafo es simétrica.
- En la representación de lista de adyacencia, si (i, j) es una arista, entonces el vértice j está en la lista para el vértice i y el vértice i está en la lista para el vértice j.

## Grafos no dirigidos

- Decimos que el camino v₁, v₂, ..., vₙ conecta v₁ y vₙ. Un grafo es conectado si cada par de sus vértices está conectado.
- Un ciclo (simple) en un grafo es un camino (simple) de longitud tres o más que conecta un vértice consigo mismo.
- Un grafo es cíclico si contiene al menos un ciclo.
- Un grafo conectado y acíclico se llama árbol libre.

## Grafos no dirigidos

- Ejemplo:
  - Un grafo no conectado (dos componentes conectadas)
  - Cada componente conectada es un árbol libre

*(diagrama no reconstruible a partir de la extracción OCR)*

## Grafos no dirigidos

- Un árbol libre se puede convertir en un árbol ordinario si elegimos cualquier vértice que deseemos como la raíz e orientamos cada arista desde la raíz.
- Los árboles libres tienen dos propiedades importantes:
  1. Todo árbol libre con n ≥ 1 vértices contiene exactamente n-1 aristas.
  2. Si añadimos cualquier arista a un árbol libre, obtenemos un ciclo.

## Árboles de expansión de costo mínimo

- Supongamos que G = (V, E) es un grafo conectado en el cual cada arista (u, v) en E tiene un costo c(u, v) adjunto.
- Un árbol de expansión para G es un árbol libre que conecta todos los vértices en V.
- El costo de un árbol de expansión es la suma de los costos de las aristas en el árbol. En esta sección mostraremos cómo encontrar un árbol de expansión de costo mínimo para G.

## Árboles de expansión de costo mínimo

- Ejemplo:
  - Un grafo y un árbol de expansión de costo mínimo

*(diagrama no reconstruible a partir de la extracción OCR)*

## Árboles de expansión de costo mínimo

- Una aplicación típica de árboles de expansión de costo mínimo ocurre en el diseño de redes de comunicaciones.
  - Los vértices de un grafo representan ciudades y las aristas posibles enlaces de comunicación entre las ciudades.
  - El costo asociado con una arista representa el costo de seleccionar ese enlace para la red.
  - Un árbol de expansión de costo mínimo representa una red de comunicaciones que conecta todas las ciudades con costo mínimo.

## Algoritmo de Prim

- Para construir un árbol de expansión de costo mínimo a partir de un grafo ponderado G = (V, E):
- El algoritmo de Prim comienza con un conjunto U inicializado a {1}. Luego "cultiva" un árbol de expansión, una arista a la vez. En cada paso, encuentra una arista más corta (u, v) que conecte U y V-U y luego añade v, el vértice en V-U, a U. Repite este paso hasta que U = V.

## Algoritmo de Prim

```
proc Prim (G: graph; var T: set of edges)
  {Prim construye un árbol de expansión de costo mínimo T para G}
  var U: set of vertexes
      u, v: vertex
  T := Ø
  U := {1}
  while U ≠ V do begin
    let (u, v) be a lowest cost edge such that
      u is in U and v is in V-U
    T := T ∪ {(u, v)}
    U := U ∪ {v}
  endwhile
endproc { Prim }
```

## Algoritmo de Prim

- El algoritmo de Prim es un algoritmo greedy (codicioso).
- El tiempo de ejecución del algoritmo de Prim es O(n²), donde n es el número de nodos.
- Un algoritmo alternativo es el algoritmo de Kruskal con un tiempo de ejecución de O(e log e), donde e es el número de aristas.

## Recorridos

- En varios problemas de grafos, necesitamos visitar los vértices de un grafo sistemáticamente.
- La búsqueda en profundidad y la búsqueda en anchura son dos técnicas importantes para hacer esto.
- Ambas técnicas se pueden usar para determinar eficientemente todos los vértices que están conectados a un vértice dado.

## Búsqueda en profundidad

- Supongamos que tenemos un grafo dirigido G en el cual todos los vértices están marcados inicialmente como no visitados.
- La búsqueda en profundidad (BEP) funciona seleccionando un vértice v de G como vértice de inicio; v se marca como visitado. Luego cada vértice no visitado adyacente a v se busca a su vez, usando búsqueda en profundidad recursivamente. Una vez que todos los vértices que pueden alcanzarse desde v han sido visitados, la búsqueda de v está completa.
- Si algunos vértices permanecen no visitados, seleccionamos un vértice no visitado como nuevo vértice de inicio. Repetimos este proceso hasta que todos los vértices de G hayan sido visitados.

## Búsqueda en profundidad

```
proc dfs (v: vertex)
  var w: vertex
  mark[v] := visited
  for each vertex w on L[v] do
    if mark[w] = unvisited then
      dfs(w)
endproc { dfs }
```

## Búsqueda en profundidad

- Ejemplo:
  - Un grafo y su búsqueda en profundidad.

*(diagrama no reconstruible a partir de la extracción OCR)*

## Búsqueda en anchura

- Otra forma sistemática de visitar los vértices se llama búsqueda en anchura (BEA).
- El enfoque se llama "búsqueda en anchura" porque desde cada vértice v que visitamos buscamos lo más ampliamente posible visitando a continuación todos los vértices adyacentes a v.
- La BEP y la BEA se pueden usar para crear árboles de expansión (o bosques de expansión) de grafos.

## Búsqueda en anchura

```
proc bfs (v) { bfs visita todos los vértices conectados a v usando búsqueda en anchura }
  var Q: QUEUE of vertex;
      x, y: vertex;
  mark[v] := visited;
  ENQUEUE(v, Q);
  while not EMPTY(Q) do
    x := FRONT(Q);
    DEQUEUE(Q);
    for each vertex y adjacent to x do
      if mark[y] = unvisited then
        mark[y] := visited;
        ENQUEUE(y, Q);
      endif
  endwhile
endproc { bfs }
```

## Búsqueda en anchura

- Ejemplo:
  - Un grafo y su búsqueda en anchura.

*(diagrama no reconstruible a partir de la extracción OCR)*

## Tiempos de ejecución

- Algoritmos comunes y operaciones en grafos:
  - n es el número de nodos (vértices)
  - e es el número de aristas (arcos)

| Algoritmo | Caso promedio | Peor caso |
|-----------|---------------|-----------|
| Dijkstra | O(e log n) | O(n²) |
| Prim | O(n²) | O(n²) |
| Búsqueda en profundidad | O(max(n,e)) | O(n + e) |
| Búsqueda en anchura | O(max(n,e)) | O(n + e) |

(*) Usando las representaciones dadas aquí

## Grafos

Luis de Marcos Ortega
luis.demarcos@uah.es
