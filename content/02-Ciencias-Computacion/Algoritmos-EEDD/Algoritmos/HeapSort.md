---
title: "Heapsort"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a explicar a fondo el algoritmo **Heapsort**, cómo funciona, por qué es eficiente, cómo se implementa con un **heap (montículo)**, y sus ventajas respecto a otros algoritmos de ordenación como Quicksort o Mergesort.

---

##  ¿Qué es Heapsort?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Merge-Sort|Merge Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Quick-Sort|Quick Sort]].

**Heapsort** es un algoritmo de ordenación **basado en el Heap ADT**, específicamente en un **Max-Heap** (para orden ascendente) o un **Min-Heap** (para orden descendente).

> Idea central: usar un **Max-Heap** para extraer repetidamente el valor máximo y colocarlo al final del array.
 q
---

##  Pasos del algoritmo Heapsort (orden ascendente)

1. **Construir un Max-Heap** a partir del array original.
    
2. Repetir:
    
    - Intercambiar el primer elemento (máximo) con el último elemento no ordenado.
        
    - Reducir el tamaño del heap en 1.
        
    - Aplicar `heapify` para restaurar la propiedad de heap.
        

---

##  Ejemplo

Array inicial:

```
[4, 10, 3, 5, 1]
```

1. Se convierte en Max-Heap:
    

```
      10
     /  \
    5    3
   / \
  4   1
```

→ Array en heap: `[10, 5, 3, 4, 1]`

2. Extraes el 10, lo colocas al final → `[1, 5, 3, 4, **10**]`
    
3. Heapify sobre los 4 primeros elementos
    
4. Repetir hasta que todo quede ordenado
    

Resultado final:

```
[1, 3, 4, 5, 10]
```

---

##  Pseudocódigo de Heapsort

```pseudocode
procedure heapsort(A)
  n := length(A)
  buildMaxHeap(A, n)

  for i := n downto 2
    swap(A[1], A[i])
    heapify(A, 1, i - 1)
end
```

### Subrutina `heapify`:

```pseudocode
procedure heapify(A, i, n)
  left := 2 * i
  right := 2 * i + 1
  largest := i

  if left ≤ n and A[left] > A[largest]
    largest := left

  if right ≤ n and A[right] > A[largest]
    largest := right

  if largest ≠ i
    swap(A[i], A[largest])
    heapify(A, largest, n)
end
```

---

##  Complejidad temporal

|Etapa|Tiempo|
|---|---|
|Construir heap|O(n)|
|Reordenar (heapify)|O(n log n)|
|**Total**|**O(n log n)**|

### Comparativa con otros algoritmos

|Algoritmo|Mejor caso|Promedio|Peor caso|
|---|---|---|---|
|Heapsort|O(n log n)|O(n log n)|O(n log n)|
|Quicksort|O(n log n)|O(n log n)|O(n²)|
|Mergesort|O(n log n)|O(n log n)|O(n log n)|

---

##  Ventajas y desventajas de Heapsort

###  Ventajas

- **No requiere memoria adicional** (in-place).
    
- Tiempo garantizado O(n log n) en todos los casos.
    
- Útil para estructuras que requieren acceso incremental al mayor o menor valor.
    

###  Desventajas

- No es estable (puede cambiar el orden relativo de elementos iguales).
    
- En la práctica suele ser más **lento que Quicksort** por constantes mayores.
    
- No tiene acceso secuencial (como Mergesort), lo que lo hace menos eficiente para datos parcialmente ordenados.
    

---

##  Ejemplo en Python

```python
def heapify(arr, n, i):
    largest = i
    l = 2*i + 1
    r = 2*i + 2

    if l < n and arr[l] > arr[largest]:
        largest = l

    if r < n and arr[r] > arr[largest]:
        largest = r

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heapsort(arr):
    n = len(arr)

    # Build max heap
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)

    # Heap sort
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)
```

---

##  Relación con el Heap ADT

- Usa el Heap ADT (estructura de datos) como **estructura auxiliar**.
    
- Usa operaciones `insert`, `deleteMax`, `heapify`.
    
- Implementado **como array** siguiendo la estructura de árbol binario completo.
    

---

##  Relación con la memoria

- Heapsort se implementa **in-place** (no requiere heap de memoria dinámica).
    
- El **heap** en heapsort es una estructura **lógica**, no la región de RAM conocida como heap memory.
    

---

##  Conclusión

> **Heapsort** es un algoritmo de ordenación eficiente, basado en Max-Heap, con un rendimiento garantizado de **O(n log n)**, sin uso extra de memoria. Aunque no es el más rápido en la práctica, **es determinista, robusto y excelente para ciertos contextos técnicos**.

---

¿Te gustaría que prepare una versión en C, Java o que lo visualicemos paso a paso con un array? ¿O una variante como un `heapsort` descendente (min-heap)?