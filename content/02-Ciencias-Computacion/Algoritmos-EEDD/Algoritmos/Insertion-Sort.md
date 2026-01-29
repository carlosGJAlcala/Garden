---
title: "Insertion Sort"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a desarrollar en detalle **Insertion Sort**, uno de los algoritmos de ordenamiento más simples pero mucho más útil que Bubble o Selection Sort en algunos contextos.

---

##  ¿Qué es Insertion Sort?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Bubble-Sort|Bubble Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Merge-Sort|Merge Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Selection-Sort|Selection Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/algoritmos-de-ordenamiento|algoritmos de ordenamiento]].

**Insertion Sort** ordena un array **construyendo gradualmente una porción ordenada**, insertando cada nuevo elemento en la **posición correcta** dentro de esa porción.

> Se comporta como cuando ordenas cartas en la mano: insertas cada carta nueva donde debe ir.

---

##  ¿Cómo funciona?

Dado:

```
[5, 2, 4, 6, 1, 3]
```

1. Empieza desde el segundo elemento (`2`)
    
2. Lo compara hacia atrás con los elementos anteriores
    
3. Si `2 < 5`, lo mueve antes de `5`
    
4. Sigue con `4`, y así sucesivamente
    

Resultado final:

```
[1, 2, 3, 4, 5, 6]
```

---

##  Pseudocódigo

```pseudocode
procedure insertionSort(A)
  for i from 1 to length(A)-1:
    key := A[i]
    j := i - 1
    while j ≥ 0 and A[j] > key:
      A[j+1] := A[j]
      j := j - 1
    A[j+1] := key
```

---

##  Ejemplo en Python

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        clave = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > clave:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = clave
```

---

##  Complejidad

|Caso|Comparaciones|Tiempo|
|---|---|---|
|Mejor|O(n) (ya ordenado)|O(n)|
|Promedio|O(n²)|O(n²)|
|Peor|O(n²)|O(n²)|
|Espacio|O(1)|In-place|

---

##  Ventajas

- **Sencillo de implementar**
    
- Muy eficiente para:
    
    - **arrays pequeños**
        
    - **listas casi ordenadas**
        
- **Estable**
    
- **In-place** (no usa memoria adicional)
    
- Se puede optimizar fácilmente
    

---

##  Desventajas

- Ineficiente para arrays grandes completamente desordenados (O(n²))
    

---

##  Comparativa rápida

|Algoritmo|Mejor|Promedio|Peor|Estable|In-place|
|---|---|---|---|---|---|
|Bubble Sort|O(n)|O(n²)|O(n²)|||
|Selection Sort|O(n²)|O(n²)|O(n²)|||
|**Insertion Sort**|**O(n)**|**O(n²)**|**O(n²)**|||

---

##  Usos reales

- En sistemas embebidos (arrays pequeños)
    
- Como paso final en algoritmos híbridos (ej: Timsort)
    
- En aplicaciones donde los datos ya están casi ordenados
    
- En estructuras como listas ligadas, donde es fácil insertar
    

---

##  Conclusión

> **Insertion Sort** es ideal cuando los datos están casi ordenados, o en situaciones donde el array es pequeño.  
> Es **estable, simple y muy eficiente en esos casos**, aunque no escala bien para listas largas desordenadas.

---

¿Quieres que lo compare gráficamente con Bubble o Merge Sort? ¿O que te prepare una versión optimizada con conteo de movimientos?