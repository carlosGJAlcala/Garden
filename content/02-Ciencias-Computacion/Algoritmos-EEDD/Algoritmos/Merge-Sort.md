---
title: "Merge Sort"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---

# Merge Sort

## ¿Qué es Merge Sort?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Quick-Sort|Quick Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/algoritmos-de-ordenamiento|algoritmos de ordenamiento]].

**Merge Sort** es un algoritmo de ordenamiento basado en el paradigma **divide y vencerás**, que:

1. **Divide** el array en dos mitades.
    
2. Ordena recursivamente cada mitad.
    
3. **Fusiona (merge)** las dos mitades ordenadas en un solo array ordenado.
    

> Siempre divide hasta que quedan arrays de tamaño 1 (que están ordenados por definición), y luego los fusiona en orden.

---

##  Ejemplo visual paso a paso

### Array original:

```
[8, 3, 1, 7, 0, 10, 2]
```

1. Divide:
    

```
[8, 3, 1]   y   [7, 0, 10, 2]
```

2. Divide más:
    

```
[8] [3,1]     y     [7,0] [10,2]
```

3. Divide hasta tamaño 1:
    

```
[8] [3] [1]   y   [7] [0] [10] [2]
```

4. Merge y ordena:
    

```
[3,8], [1] → [1,3,8]  
[0,7], [2,10] → [0,2,7,10]
```

5. Resultado final:
    

```
[0, 1, 2, 3, 7, 8, 10]
```

---

##  Pseudocódigo

```pseudocode
procedure mergeSort(A)
  if length(A) > 1:
    mid := length(A) / 2
    L := mergeSort(A[0..mid-1])
    R := mergeSort(A[mid..n])
    return merge(L, R)

procedure merge(L, R)
  crear array vacío result
  mientras L y R no estén vacíos:
    si L[0] < R[0]:
      agregar L[0] a result y eliminar de L
    si no:
      agregar R[0] a result y eliminar de R
  agregar cualquier resto de L o R a result
  return result
```

---

##  Ejemplo en Python

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    izquierda = merge_sort(arr[:mid])
    derecha = merge_sort(arr[mid:])
    return merge(izquierda, derecha)

def merge(left, right):
    resultado = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            resultado.append(left[i])
            i += 1
        else:
            resultado.append(right[j])
            j += 1
    resultado.extend(left[i:])
    resultado.extend(right[j:])
    return resultado
```

---

##  Complejidad

|Caso|Tiempo|
|---|---|
|Mejor|O(n log n)|
|Promedio|O(n log n)|
|Peor|O(n log n)|
|Espacio|**O(n)**|

- Siempre realiza log⁡n\log n divisiones y **merge de tamaño n** → rendimiento **estable**
    
- No es in-place (usa arrays temporales)
    

---

##  Ventajas

- **Estable** (no cambia el orden de elementos iguales)
    
- **Siempre O(n log n)**, sin importar los datos
    
- Muy usado en archivos grandes (porque es fácil de paralelizar y optimizar por bloques)
    

---

##  Desventajas

- Requiere **memoria extra**
    
- Es más lento que QuickSort para arrays pequeños (por las copias de datos)
    

---

##  Comparativa rápida

|Algoritmo|Mejor|Promedio|Peor|Estable|Memoria extra|
|---|---|---|---|---|---|
|QuickSort|n log n|n log n|n²||No (in-place)|
|MergeSort|n log n|n log n|n log n||Sí (O(n))|

---

##  Usos reales

- Librerías estándar donde se requiere estabilidad (como `stable_sort` en C++)
    
- Ordenar listas muy grandes en disco (external sorting)
    
- Paralelización de ordenamiento en múltiples cores
    
- Ordenamiento de registros (por nombre, clave, etc.)
    

---

##  Conclusión

> **Merge Sort** es el algoritmo ideal cuando necesitas:
> 
> - **rendimiento garantizado O(n log n)**
>     
> - **orden estable**
>     
> - y puedes asumir un poco más de uso de memoria
>     

---