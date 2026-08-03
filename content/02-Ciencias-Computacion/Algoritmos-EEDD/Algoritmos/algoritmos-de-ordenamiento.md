---
title: "Algoritmos De Ordenamiento"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---

<<<<<<< HEAD
=======
# Algoritmos de Ordenamiento (Sorting Algorithms)
>>>>>>> 788cfbd6a7588493c9844126e17f19f7b6628750

## ¿Qué es ordenar?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Dado un conjunto de elementos con una **relación de orden** (como `<`, `>`), el objetivo de un algoritmo de ordenamiento es **reorganizarlos en una secuencia creciente o decreciente**.

---

##  Clasificación general de algoritmos de ordenamiento

###  Por método

|Tipo|Ejemplos|
|---|---|
|**Comparativos**|Bubble, Insertion, Merge, Quick, Heap|
|**No comparativos**|Counting, Radix, Bucket|

###  Por rendimiento

|Criterio|Definición|
|---|---|
|**Estabilidad**|No cambia el orden de elementos iguales|
|**In-place**|No necesita memoria extra significativa|
|**Complejidad**|Mejor, promedio, peor caso|

---

## ️ Principales algoritmos de ordenamiento comparativo

---

### 1. **[[Bubble-Sort]]**

> Recorre el array varias veces, intercambiando elementos adyacentes si están fuera de orden.

```pseudocode
for i = 0 to n-1:
  for j = 0 to n-2:
    if A[j] > A[j+1]:
      swap(A[j], A[j+1])
```

 Simple, pero **muy lento**

| Complejidad | Valor |
| ----------- | ----- |
| Tiempo      | O(n²) |
| Espacio     | O(1)  |
| Estable     |      |
| In-place    |      |

---

### 2. **[[Insertion-Sort]]**

> Inserta elementos en la posición correcta uno por uno, como en un juego de cartas.

```pseudocode
for i = 1 to n-1:
  key := A[i]
  j := i - 1
  while j >= 0 and A[j] > key:
    A[j+1] = A[j]
    j -= 1
  A[j+1] = key
```

 Bueno para arrays pequeños o casi ordenados

| Complejidad | Valor |
| ----------- | ----- |
| Tiempo      | O(n²) |
| Espacio     | O(1)  |
| Estable     |      |

---

### 3. **[[Selection-Sort]]**

> Encuentra el mínimo y lo pone al principio, luego el segundo menor, etc.

```pseudocode
for i = 0 to n-1:
  min_idx = i
  for j = i+1 to n-1:
    if A[j] < A[min_idx]:
      min_idx = j
  swap(A[i], A[min_idx])
```

 Poca utilidad práctica por su ineficiencia

|Complejidad|Valor|
|---|---|
|Tiempo|O(n²)|
|Estable||

---

### 4. **[[Merge-Sort]]**

> Divide el array en mitades, las ordena recursivamente y luego las fusiona.

```pseudocode
function mergeSort(A):
  if length(A) > 1:
    mid = n // 2
    L = mergeSort(A[0:mid])
    R = mergeSort(A[mid:n])
    return merge(L, R)
```

 Muy eficiente y **estable**, pero **usa memoria extra**

|Complejidad|Valor|
|---|---|
|Tiempo|O(n log n)|
|Espacio|O(n)|
|Estable||

---

### 5. **[[Quick-Sort]]**

> Elige un pivote, separa los elementos menores y mayores, y ordena recursivamente.

```pseudocode
function quicksort(A):
  if length(A) ≤ 1: return A
  pivot = A[0]
  left = [x < pivot]
  right = [x ≥ pivot]
  return quicksort(left) + [pivot] + quicksort(right)
```

 Muy rápido en la práctica, pero puede ser O(n²) si el pivote es malo

|Complejidad|Valor|
|---|---|
|Promedio|O(n log n)|
|Peor caso|O(n²)|
|Espacio|O(log n)|
|Estable| (normalmente)|

---

### 6. **[[HeapSort]]**

> Construye un Max-Heap y extrae el mayor elemento repetidamente.

 No necesita memoria extra, pero menos rápido que quicksort en la práctica

|Complejidad|Valor|
|---|---|
|Tiempo|O(n log n)|
|Espacio|O(1)|
|Estable||

---

##  Comparativa general

|Algoritmo|Mejor|Promedio|Peor|Estable|In-place|
|---|---|---|---|---|---|
|Bubble|O(n)|O(n²)|O(n²)|||
|Insertion|O(n)|O(n²)|O(n²)|||
|Selection|O(n²)|O(n²)|O(n²)|||
|Merge Sort|O(n log n)|O(n log n)|O(n log n)|||
|Quick Sort|O(n log n)|O(n log n)|O(n²)|||
|Heap Sort|O(n log n)|O(n log n)|O(n log n)|||

---

##  Algoritmos no comparativos

Cuando los datos son **enteros pequeños o estructuras especiales**, se puede usar:

###  Counting Sort

- Cuenta ocurrencias de cada valor
    
- Complejidad: **O(n + k)**
    
- Solo funciona si los valores son enteros en rango limitado
    
- **Estable**
    

###  Radix Sort

- Ordena por dígitos desde el menos significativo
    
- Usa Counting Sort como subrutina
    
- **O(n·k)** donde `k` es el número de dígitos
    

---

##  Conclusión

> No hay un algoritmo de ordenamiento “mejor para todo”.  
> Debes elegir según **tipo de datos, volumen, memoria disponible y si necesitas estabilidad**.

|Necesitas…|Usa…|
|---|---|
|Ordenamiento general eficiente|QuickSort|
|Estabilidad y seguridad|MergeSort|
|Memoria constante (in-place)|HeapSort|
|Datos pequeños o preordenados|InsertionSort|
|Ordenar enteros en rango pequeño|Counting/Radix|

---