---
title: "Quick Sort"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---

# Quick Sort

## ¿Qué es Quick Sort?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Merge-Sort|Merge Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Insertion-Sort|Insertion Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/algoritmos-de-ordenamiento|algoritmos de ordenamiento]].

**Quick Sort** es un algoritmo **divide y vencerás** que:

1. **Elige un pivote**
    
2. **Divide** el array en dos partes:
    
    - Elementos menores al pivote
        
    - Elementos mayores (o iguales)
        
3. Ordena **recursivamente** cada parte
    

---

##  Ejemplo visual paso a paso

Array original:

```
[9, 4, 7, 3, 6, 2]
```

1. Elijo pivote = **9**
    
2. Menores = `[4, 7, 3, 6, 2]`
    
3. Mayores = `[]`
    
4. Recursivamente ordeno menores → `[2, 3, 4, 6, 7]`
    
5. Resultado: `[2, 3, 4, 6, 7, 9]`
    

---

##  Pseudocódigo

```pseudocode
procedure quicksort(A, low, high)
  if low < high:
    p = partition(A, low, high)
    quicksort(A, low, p - 1)
    quicksort(A, p + 1, high)

procedure partition(A, low, high)
  pivot := A[high]
  i := low - 1
  for j = low to high - 1:
    if A[j] ≤ pivot:
      i := i + 1
      swap A[i], A[j]
  swap A[i+1], A[high]
  return i + 1
```

---

##  Ejemplo en Python

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[-1]
    menores = [x for x in arr[:-1] if x <= pivot]
    mayores = [x for x in arr[:-1] if x > pivot]
    return quicksort(menores) + [pivot] + quicksort(mayores)
```

Versión **in-place**:

```python
def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i+1], arr[high] = arr[high], arr[i+1]
    return i + 1

def quicksort(arr, low, high):
    if low < high:
        p = partition(arr, low, high)
        quicksort(arr, low, p - 1)
        quicksort(arr, p + 1, high)
```

---

##  Complejidad

|Caso|Tiempo|
|---|---|
|Mejor caso|O(n log n)|
|Promedio|O(n log n)|
|Peor caso|O(n²)|
|Espacio|O(log n)*|

* Por recursión. Es in-place en versión clásica.

---

## ️ ¿Cuándo cae en el peor caso?

Cuando el **pivote es siempre el mínimo o máximo** → por ejemplo en arrays ya ordenados y si eliges el último elemento como pivote.

️ Para evitarlo, se usa:

- **Pivote aleatorio**
    
- **Mediana de tres elementos**
    
- **Versión híbrida con insertion sort**
    

---

##  Ventajas

- Rápido en la práctica (mejor que MergeSort para arrays)
    
- No necesita memoria extra (in-place)
    
- Fácil de adaptar a arrays, listas y estructuras personalizadas
    

---

##  Desventajas

- No es **estable** (puede reordenar elementos iguales)
    
- Puede caer en O(n²) sin buena elección de pivote
    
- Menos predecible en entornos críticos
    

---

##  Conclusión

> **Quick Sort** es uno de los algoritmos más eficientes y prácticos para ordenamiento general. Su rendimiento en promedio es excelente, y su estructura recursiva lo hace elegante, aunque requiere atención en la **elección del pivote** para evitar el peor caso.

---