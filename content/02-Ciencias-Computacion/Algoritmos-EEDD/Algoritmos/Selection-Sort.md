---
title: "Selection Sort"
date: 2025-01-01
tags:
  - ciencias-computacion
---

##  ¿Qué es Selection Sort?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Bubble-Sort|Bubble Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Insertion-Sort|Insertion Sort]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

**Selection Sort** (ordenamiento por selección) consiste en:

> Repetidamente encontrar el **mínimo (o máximo)** elemento del arreglo no ordenado, y colocarlo en su posición correcta **desde el inicio del arreglo hacia adelante**.

 Es como ordenar cartas **buscando siempre la más pequeña** y dejándola al principio.

---

##  ¿Cómo funciona?

### Ejemplo con:

```
[4, 2, 5, 1, 3]
```

1. Encuentra el mínimo → `1`, lo pone al principio → `[1, 2, 5, 4, 3]`
    
2. Encuentra el siguiente mínimo → `2`, ya está en su sitio
    
3. Encuentra el mínimo de lo que queda → `3` → `[1, 2, 3, 4, 5]`  
    ...
    

---

##  Pseudocódigo

```pseudocode
procedure selectionSort(A)
  n := length(A)
  for i from 0 to n-2:
    minIndex := i
    for j from i+1 to n-1:
      if A[j] < A[minIndex]:
        minIndex := j
    if minIndex ≠ i:
      swap A[i], A[minIndex]
```

---

##  Ejemplo en Python

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
```

---

##  Complejidad

|Caso|Comparaciones|Swaps|Tiempo|
|---|---|---|---|
|Mejor|O(n²)|O(n)|O(n²)|
|Promedio|O(n²)|O(n)|O(n²)|
|Peor|O(n²)|O(n)|O(n²)|

 Siempre hace el mismo número de comparaciones  
 Hace pocos swaps comparado con otros O(n²)

---

##  Ventajas

- **Simple de implementar**
    
- Hace **menos intercambios** que Bubble o Insertion Sort
    
- Funciona bien con estructuras donde intercambiar datos es muy costoso (por ejemplo: arrays con escritura lenta como EEPROM o memoria flash)
    

---

##  Desventajas

- **Muy ineficiente** en rendimiento (nunca mejor que O(n²))
    
- **No es estable** (puede reordenar elementos iguales)
    
- Siempre hace n² comparaciones, incluso si el array ya está ordenado
    

---

##  ¿Es estable?

 No. Si hay dos elementos con el mismo valor, el algoritmo **puede intercambiarlos y romper el orden relativo**.  
 Se puede **hacer estable** si en lugar de intercambiar, insertas el mínimo desplazando los elementos.

---

##  Comparación con otros algoritmos básicos

|Algoritmo|Comparaciones|Swaps|Estable|Rendimiento|
|---|---|---|---|---|
|Bubble Sort|O(n²)|O(n²)||Malo|
|Insertion Sort|O(n²)|O(n²)||Mejor si casi ordenado|
|**Selection Sort**|**O(n²)**|**O(n)**||Malo, constante|

---

##  Cuándo usar Selection Sort

Solo en contextos muy específicos:

- Cuando el **número de intercambios** debe ser mínimo.
    
- Como **algoritmo educativo**.
    
- En **sistemas embebidos** con escrituras lentas.
    

---

##  Conclusión

> **Selection Sort** es un algoritmo muy simple de entender y programar, útil para enseñanza, pero **ineficiente en casi todos los contextos prácticos**.  
> Aun así, su idea de seleccionar mínimos sucesivos **inspira otros algoritmos más avanzados**.

---