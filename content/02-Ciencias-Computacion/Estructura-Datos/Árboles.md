---
title: "Árboles"
---

# Árboles

## Índice

- Terminología básica
- El TAD árbol
- Implementaciones de árboles
- Árboles binarios
- Árboles binarios de búsqueda
- Árboles AVL

## Bibliografía

- Capítulos 3 y 5 de:
  - A.V. AHO, J.E. HOPCROFT, J.D. ULLMAN. 1987. "Data Structures and Algorithms." Addison-Wesley.

## Terminología

- Un árbol impone una estructura jerárquica en una colección de elementos.
- Ejemplos familiares de árboles son los árboles genealógicos y los organigramas de empresas.
- Ejemplos de usos de árboles:
  - Analizar circuitos eléctricos
  - Representar la estructura de fórmulas matemáticas

## Terminología

- Los árboles surgen naturalmente en muchas áreas diferentes de la informática.
- Por ejemplo:
  - En sistemas de bases de datos, los árboles se utilizan para organizar información.
  - En compiladores, para representar la estructura sintáctica de programas fuente.
  - En sistemas de archivos (directorios)
  - En la jerarquía de clases en lenguajes orientados a objetos
  - En menús de aplicaciones

## Terminología

- Un árbol es una colección de elementos llamados nodos, uno de los cuales se distingue como raíz, junto con una relación ("paternidad") que coloca una estructura jerárquica en los nodos.
- Terminología – Definición
  - Formalmente, un árbol se puede definir recursivamente de la siguiente manera:

1. Un único nodo por sí solo es un árbol. Este nodo es también la raíz del árbol.
2. Supongamos que n es un nodo y T₁, T₂, …, Tₖ son árboles con raíces n₁, n₂, …, nₖ, respectivamente. Podemos construir un nuevo árbol haciendo que n sea el padre de los nodos n₁, n₂, …, nₖ. En este árbol, n es la raíz y T₁, T₂, …, Tₖ son los subárboles de la raíz. Los nodos n₁, n₂, …, nₖ se llaman los hijos del nodo n.
3. Un árbol nulo, un "árbol" sin nodos, que representaremos por Λ.

## Terminología

- Ejemplo: Tabla de contenidos de un libro

*(diagrama no reconstruible a partir de la extracción)*

## Terminología

- Padre, hijo, hermanos (hijos del mismo nodo)
- Camino de un nodo a otro
- Longitud de un camino
- Antecesor de un nodo
- Descendiente de un nodo
- Un nodo sin descendientes se llama hoja
- Altura de un nodo – la distancia más larga a una hoja
  - Altura de un árbol es la altura de la raíz.
- Profundidad de un nodo – distancia a la raíz
- Terminología – Orden de nodos
- Los hijos de un nodo generalmente se ordenan de izquierda a derecha.

## Terminología – Recorridos

- Hay varias formas útiles en las que podemos ordenar sistemáticamente (o recorrer) todos los nodos de un árbol. Los tres órdenes más importantes se llaman preorden, inorden y postorden. Estos órdenes se definen recursivamente de la siguiente manera:
  - Si un árbol T es nulo, entonces la lista vacía es el listado en preorden, inorden y postorden de T.
  - Si T consta de un único nodo, entonces ese nodo por sí solo es el listado en preorden, inorden y postorden de T.

## Terminología – Recorridos

- En caso contrario, sea T un árbol con raíz n y subárboles T₁, T₂, …, Tₖ, como se sugiere en la figura.

## Terminología – Recorridos

- El listado en preorden (o recorrido en preorden) de los nodos de T es la raíz n de T seguida por los nodos de T₁ en preorden, luego los nodos de T₂ en preorden, y así sucesivamente, hasta los nodos de Tₖ en preorden.
- El listado en inorden de los nodos de T es los nodos de T₁ en inorden, seguidos por el nodo n, seguidos por los nodos de T₂, …, Tₖ, cada grupo de nodos en inorden.
- El listado en postorden de los nodos de T es los nodos de T₁ en postorden, luego los nodos de T₂ en postorden, y así sucesivamente, hasta Tₖ, todo seguido por el nodo n.

## Terminología – Recorridos

```
void tree::PREORDER ( n: node )
  ( 1) list n;
  ( 2) for each child c of n, if any, in order from
       the left do PREORDER ( c)
endmethod { PREORDER }
```

- Para convertirlo en un procedimiento POSTORDER, simplemente invertimos el orden de los pasos (1) y (2).

## Terminología – Recorridos

```
void tree::INORDER ( n: node )
  if n is a leaf then
    list n
  else begin
    INORDER ( leftmost child of n)
    list n
    for each child c of n, except for the leftmost, in order
      from the left do
    INORDER ( c)
  endelse
endmethod { INORDER }
```

## Terminología – Recorridos

- Un truco útil es caminar alrededor de la parte exterior del árbol, comenzando en la raíz, moviéndose en sentido contrario a las agujas del reloj.
- Para preorden, listamos un nodo la primera vez que lo pasamos. Para postorden, listamos un nodo la última vez que lo pasamos, mientras nos movemos hacia su padre. Para inorden, listamos una hoja la primera vez que la pasamos, pero listamos un nodo interior la segunda vez que lo pasamos.

## Terminología – Recorridos

## Terminología – Etiquetas

- A menudo es útil asociar una etiqueta, o valor, con cada nodo de un árbol, del mismo modo que asociamos un valor con un elemento de lista en el capítulo anterior. Es decir, la etiqueta de un nodo no es el nombre del nodo, sino un valor que se "almacena" en el nodo.

## Terminología – Etiquetas

- Ejemplo: árbol etiquetado que representa la expresión aritmética (a+b) * (a+c)

*(diagrama no reconstruible a partir de la extracción)*

## Terminología – Etiquetas

- Ejemplo:
  - Forma de prefijo en preorden de una expresión: +ab+ac
  - Representación de postfijo (o polaca) en postorden de una expresión: ab+ac+*
  - Expresión de infijo en inorden (sin paréntesis): a+b * a+c

## El TAD árbol

```
spec TREE[NODE]
  genres tree, node, label
  operations
    parent: node tree -> node
    leftmost_child: node tree -> node
    right_sibling: node tree -> node
    label: node tree -> label
    create: label tree tree -> tree
    root: tree -> node
    makenull: tree -> tree
endspec
```

## El TAD árbol

- PARENT(n, T). Esta función devuelve el padre del nodo n en el árbol T. Si n es la raíz, que no tiene padre, se devuelve Λ.
- LEFTMOST_CHILD(n, T) devuelve el hijo izquierdo más lejano del nodo n en el árbol T, y devuelve Λ si n es una hoja, que por lo tanto no tiene hijos.
- RIGHT_SIBLING(n, T) devuelve el hermano derecho del nodo n en el árbol T, definido como aquel nodo m con el mismo padre p que n tal que m se encuentra inmediatamente a la derecha de n en el ordenamiento de los hijos de p.

## El TAD árbol

- LABEL(n, T) devuelve la etiqueta del nodo n en el árbol T. Sin embargo, no requerimos que las etiquetas estén definidas para cada árbol.
- CREATEᵢ(v, T₁, T₂, …, Tᵢ) es una de una familia infinita de funciones, una para cada valor de i = 0, 1, 2, … CREATEᵢ hace un nuevo nodo r con etiqueta v y le da i hijos, que son las raíces de los árboles T₁, T₂, …, Tᵢ, en orden de izquierda a derecha. Se devuelve el árbol con raíz r. Observe que si i = 0, entonces r es tanto una hoja como la raíz.

## El TAD árbol

```
void tree::PREORDER ( n: node )
  {list the labels of the descendants of n in preorder}
  var c: node
  print ( LABEL ( n, T))
  c := LEFTMOST_CHILD ( n, T)
  while c <> null do
    PREORDER ( c)
    c := RIGHT_SIBLING ( c, T)
  endwhile
endproc { PREORDER }
```

- Llamamos a PREORDER(ROOT(T)) para obtener el preorden del árbol T.

## Implementaciones de árboles

- Vamos a presentar tres implementaciones diferentes:
  - Representación en array
  - Representación por lista de hijos
  - Representación hijo izquierdo, hermano derecho
- Vamos a considerar solo la tercera para nuestras implementaciones.

## Implementación de árboles

- Representación en array
  - Array lineal A en el que la entrada A[i] es un puntero o un cursor al padre del nodo i
  - A[i] = 0 si el nodo i es la raíz
  - Esta representación utiliza la propiedad de los árboles de que cada nodo tiene un padre único
  - No facilita operaciones que requieren información de los hijos

## Implementación de árboles

- Representación por lista de hijos
  - Para cada nodo se forma una lista de sus hijos

## Implementaciones de árboles

- Representación hijo izquierdo, hermano derecho
  - Cada nodo tiene una referencia solo a su hijo izquierdo y hermano derecho.
  - Cada hoja tiene un nulo para el hijo izquierdo y cada hijo más a la derecha tiene un nulo para la referencia del hermano derecho.

## Implementaciones de árboles

```
node = record
  element: label
  leftmostchild: ^node
  rightsibling: ^node
endrecord
tree: ^node {or a full class}

label: elementtype
```

## Implementaciones de árboles

- Tiempo de ejecución de las operaciones
  - parent – O(n)
  - leftmost_child – O(1)
  - right_sibling – O(1)
  - label – O(1)
  - create – O(1)
  - makenull – O(1)
  - O(n) para liberar cada elemento – recorrer el árbol (postorden)
  - root – O(1)

## Árboles binarios

- Un árbol binario es un árbol que es vacío, o un árbol en el cual cada nodo tiene ningún hijo, un hijo izquierdo, un hijo derecho, o tanto un hijo izquierdo como un hijo derecho.
- El hecho de que cada hijo en un árbol binario se designe como hijo izquierdo o como hijo derecho hace que un árbol binario sea diferente del árbol orientado, ordenado (también llamado árbol "ordinario" o "general").
- Árboles binarios
  - Dos árboles binarios diferentes

*(diagrama no reconstruible a partir de la extracción)*

- El TAD árbol binario

```
spec BINARY_TREE[NODE]
  genres b_tree, node, label
  operations
    parent: node b_tree -> node
    left_child: node b_tree -> node
    right_child: node b_tree -> node
    label: node b_tree -> label
    create: b_tree b_tree -> tree
    root: b_tree -> node
    makenull: b_tree -> b_tree
endspec
```

## El TAD árbol binario

```
node = record
  element: label
  leftchild: ^node
  rightchild: ^node
  parent: ^node {optional}
endrecord
b_tree: ^node {or a class}

label: elementtype
```

- Árboles binarios
  - Tiempo de ejecución de las operaciones
    - parent: – O(1) si el puntero al padre está presente, O(n) si no
    - left_child – O(1)
    - right_child – O(1)
    - label – O(1)
    - create – O(1)
    - makenull – O(1)
    - O(n) para liberar cada elemento – recorrer el árbol (postorden)
    - root – O(1)
  - Árboles binarios de búsqueda
    - Un árbol binario de búsqueda (BST) es un árbol binario en el cual:

1. Los nodos se etiquetan con elementos de un conjunto.
2. Todos los elementos almacenados en el subárbol izquierdo de cualquier nodo x son todos menores que el elemento almacenado en x, y todos los elementos almacenados en el subárbol derecho de x son mayores que el elemento almacenado en x.
- Esta condición, llamada la propiedad del árbol binario de búsqueda, se cumple para cada nodo del árbol binario de búsqueda, incluyendo la raíz.
- Los BST también se llaman árbol binario ordenado o ordenado.
- Árboles binarios de búsqueda
  - Dos árboles binarios de búsqueda que representan el mismo conjunto de enteros

*(diagrama no reconstruible a partir de la extracción)*

## Árboles binarios de búsqueda

- Una propiedad interesante: si listamos los nodos de un árbol binario de búsqueda en inorden, entonces los elementos almacenados en esos nodos se listan en orden ordenado.
- Las operaciones en un árbol binario de búsqueda requieren comparaciones entre nodos. Estas comparaciones se realizan con llamadas a un comparador, que es una subrutina que calcula el orden total (orden lineal) en dos valores cualesquiera. Este comparador puede definirse explícita o implícitamente, dependiendo del lenguaje en el que se implemente el BST.

## El TAD BST

```
spec BINARY_SEARCH_TREE[NODE]
  genres bst, node, label
  operations
    search: label BST -> boolean
    insert: label BST -> BST
    delete: label BST -> BST
endspec
```

## El TAD BST

```
node = record
  element: label
  leftchild: ^node
  rightchild: ^node
endrecord
bst: ^node {or a class}

label: elementtype
```

- Árboles binarios de búsqueda
  - SEARCH (también llamado member). Examinar el nodo raíz:
    - Si el árbol es nulo, el valor que buscamos no existe en el árbol.
    - Si el valor es igual a la raíz, la búsqueda es exitosa.
    - Si el valor es menor que la raíz, buscar el subárbol izquierdo.
    - De forma similar, si es mayor que la raíz, buscar el subárbol derecho.
  - Este proceso se repite hasta que el valor se encuentra o el subárbol indicado es nulo.

## Árboles binarios de búsqueda

- INSERT(x, T)
  - Probar si T = nulo, es decir, si el BST está vacío. Si es así, creamos un nuevo nodo para contener x y hacemos que A apunte a él.
  - Si el BST no está vacío, buscamos x más o menos como lo hace SEARCH, pero cuando encontramos un puntero nulo durante nuestra búsqueda, lo reemplazamos por un puntero a un nuevo nodo que contiene x. Entonces x estará en el lugar correcto, es decir, el lugar donde la función SEARCH lo encontrará.
- Árboles binarios de búsqueda
  - DELETE(x, A):
    - Localizar el elemento x que se va a eliminar en el árbol.
    - Si x está en una hoja, podemos eliminar esa hoja y hemos terminado.
    - Si es un nodo interior, eliminarlo desconectaría el árbol.
    - Si x tiene solo un hijo, podemos reemplazar x por ese hijo, y nos quedará con el BST apropiado.
    - Si x tiene dos hijos, entonces debemos encontrar el elemento con el valor más bajo entre los descendientes del hijo derecho y reemplazar el nodo a eliminar con él.
    - El descendiente de valor más alto entre los descendientes de la izquierda también funcionaría igual de bien.

## Árboles binarios de búsqueda

- Para escribir DELETE, es útil tener una función DELETEMIN(A) que elimine el elemento más pequeño de un árbol no vacío y devuelva el valor del elemento eliminado.

## Ejemplo

- Eliminar 10 del siguiente BST

*(diagrama no reconstruible a partir de la extracción)*

## Ejemplo

- El elemento de valor más bajo entre los descendientes del hijo derecho es 12

*(diagrama no reconstruible a partir de la extracción)*

- Árboles binarios de búsqueda
  - Tiempos de ejecución de las operaciones del BST:

| Operación | Caso promedio | Peor caso |
|-----------|---------------|-----------|
| Search    | O(log n)      | O(n)      |
| Insert    | O(log n)      | O(n)      |
| Delete    | O(log n)      | O(n)      |

- Análisis de tiempo de los BST
  - Véase (AHO, HOPCROFT & ULLMAN, 1987) "Data Structures and Algorithms." Capítulo 5. Sección 5.2.

## Árboles balanceados

- Un árbol (de altura) balanceado es un árbol donde ninguna hoja está mucho más lejos de la raíz que cualquier otra hoja.
- Definición: Un árbol vacío está balanceado. Un árbol binario no vacío T está balanceado si:
  1. El subárbol izquierdo de T está balanceado
  2. El subárbol derecho de T está balanceado
  3. La diferencia entre las alturas del subárbol izquierdo y el subárbol derecho no es más de 1.

## Árboles balanceados

- Árbol completo – Un árbol en el cual cada nivel, excepto posiblemente el más profundo, está completamente lleno. A profundidad n, la altura del árbol, todos los nodos están tan a la izquierda como sea posible.
- Un árbol completo está balanceado, pero un árbol balanceado no es necesariamente completo.

## Árboles balanceados

- En un BST, algunas secuencias de inserciones y eliminaciones pueden producir árboles binarios de búsqueda cuya profundidad promedio es proporcional (o cercana) a n. Esto sugiere que podríamos intentar reorganizar el árbol después de cada inserción y eliminación para que siempre esté balanceado o completo; entonces el tiempo para SEARCH y operaciones similares siempre sería O(log n).

## Árboles balanceados

- Implementaciones balanceadas de árboles:
  - Árboles AVL
  - Árboles 2-3
  - Árboles rojo-negro
  - Árboles B (árboles B+)
  - Árboles T

## Árboles AVL

- Un árbol AVL es un árbol binario de búsqueda autobalanceado.
  - Nombrado en honor a sus dos inventores, G.M. Adelson-Velskii y E.M. Landis (1962)
- El factor de balance de un nodo es la altura de su subárbol izquierdo menos la altura de su subárbol derecho (a veces lo opuesto).
- Un nodo con factor de balance 1, 0, o −1 se considera balanceado. Un nodo con cualquier otro factor de balance se considera desbalanceado y requiere rebalancear el árbol. El factor de balance generalmente se almacena directamente en cada nodo.

## Árboles AVL

- TAD similar al de un BST
  - Las mismas operaciones: Search, Insert, Delete
- La estructura de datos necesita incorporar un entero en cada nodo para almacenar el factor de balance.
  - Factor de balance = altura hijo_izquierdo – altura hijo_derecho
- SEARCH se realiza exactamente como en un árbol binario de búsqueda sin balancear.
  - La estructura del árbol no se modifica por búsquedas.

## Árboles AVL

- INSERT – Después de insertar un nodo, es necesario verificar cada uno de los ancestros del nodo para
- Consistencia con las reglas de AVL. Para cada nodo verificado, si el factor de balance permanece −1, 0, o +1, entonces no se necesitan rotaciones. Sin embargo, si el factor de balance se convierte en ±2, entonces el subárbol enraizado en este nodo está desbalanceado.

## Árboles AVL

- INSERT – cuatro casos que deben considerarse
  - Caso Right-Right
  - Caso Right-Left
  - Caso Left-Left
  - Caso Left-Right
- Los factores de balance determinan cuál es el caso que estamos tratando.

## Árboles AVL

- Caso Right-Right y caso Right-Left:
  - Si el factor de balance de un nodo (P) es -2, entonces el subárbol derecho supera en peso al subárbol izquierdo del nodo dado, y se debe verificar el factor de balance del hijo derecho (R). Se necesita una rotación izquierda con P como raíz.
  - Si el factor de balance de R es -1 o 0, se necesita una sola rotación izquierda (con P como raíz) (caso Right-Right).
  - Si el factor de balance de R es +1, se necesitan dos rotaciones diferentes. La primera rotación es una rotación derecha con R como raíz. La segunda es una rotación izquierda con P como raíz (caso Right-Left).

## Árboles AVL

- Caso Left-Left y caso Left-Right:
  - Si el factor de balance de un nodo (P) es +2, entonces el subárbol izquierdo supera en peso al subárbol derecho del nodo dado, y se debe verificar el factor de balance del hijo izquierdo (L). Se necesita una rotación derecha con P como raíz.
  - Si el factor de balance de L es +1 o 0, se necesita una sola rotación derecha (con P como raíz) (caso Left-Left).
  - Si el factor de balance de L es -1, se necesitan dos rotaciones diferentes. La primera rotación es una rotación izquierda con L como raíz. La segunda es una rotación derecha con P como raíz (caso Left-Right).

## Árboles AVL

- DELETE
  - Si el nodo es una hoja o tiene solo un hijo, elimínalo.
  - De lo contrario, reemplázalo con el más grande en su subárbol izquierdo (predecesor en inorden) o el más pequeño en su subárbol derecho (sucesor en inorden), y elimina ese nodo. (Igual que en un BST)
- El nodo que se encontró como reemplazo tiene a lo más un subárbol. Después de la eliminación, retrocede a lo largo de la ruta hacia arriba en el árbol (padre del reemplazo) hasta la raíz, ajustando los factores de balance según sea necesario. Rebalancea como en la inserción si es necesario.

## Árboles AVL

- Tiempos de ejecución de operaciones en un árbol AVL

| Operación | Caso promedio | Peor caso |
|-----------|---------------|-----------|
| Search    | O(log n)      | O(log n)  |
| Insert    | O(log n)      | O(log n)  |
| Delete    | O(log n)      | O(log n)  |

Árboles
Luis de Marcos Ortega
luis.demarcos@uah.es
