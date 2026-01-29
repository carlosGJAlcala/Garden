---
title: "Bubble Sort"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - algoritmos
---
Perfecto. Vamos a detallar **Bubble Sort**, uno de los algoritmos de ordenamiento más simples y conocidos, ideal para aprendizaje y análisis básico, aunque **ineficiente en la práctica**.

---

##  ¿Qué es Bubble Sort?


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Insertion-Sort|Insertion Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Selection-Sort|Selection Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/algoritmos-de-ordenamiento|algoritmos de ordenamiento]].

**Bubble Sort** compara elementos adyacentes y los **intercambia si están en el orden incorrecto**, "burbujando" los valores más grandes hacia el final del arreglo en cada pasada.

 En cada iteración, el **elemento más grande se mueve al final** como si flotara.

---

##  Ejemplo paso a paso

### Arreglo original:

```
[5, 3, 8, 4, 2]
```

### Iteración 1:

- 5 > 3 → swap → [3, 5, 8, 4, 2]
    
- 5 < 8 → nada
    
- 8 > 4 → swap → [3, 5, 4, 8, 2]
    
- 8 > 2 → swap → [3, 5, 4, 2, 8]
    

→ Al final: **8 en su lugar**

Repite hasta que no haya intercambios.

---

##  Pseudocódigo clásico

```pseudocode
procedure bubbleSort(A)
  n := length(A)
  for i from 0 to n-1:
    for j from 0 to n-2-i:
      if A[j] > A[j+1]:
        swap A[j], A[j+1]
```

 Versión mejorada (detiene si no hay cambios):

```pseudocode
procedure bubbleSortOptimized(A)
  repeat
    swapped := false
    for i from 0 to n-2:
      if A[i] > A[i+1]:
        swap A[i], A[i+1]
        swapped := true
  until not swapped
```

---

##  Ejemplo en Python

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        intercambiado = False
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                intercambiado = True
        if not intercambiado:
            break
```

---

##  Complejidad

|Caso|Comparaciones|Tiempo|
|---|---|---|
|Mejor|O(n) (si optimizado)|O(n)|
|Promedio|O(n²)|O(n²)|
|Peor|O(n²)|O(n²)|
|Espacio|O(1)|In-place|

---

##  Ventajas

- Muy fácil de entender e implementar
    
- **In-place** (no requiere memoria adicional)
    
- Se puede optimizar para detenerse si ya está ordenado
    

---

##  Desventajas

- **Extremadamente ineficiente** para listas grandes
    
- **No se usa en la práctica profesional**
    
- Hace muchas comparaciones innecesarias
    

---

##  Comparativa con otros O(n²)

|Algoritmo|Comparaciones|Swaps|Estable|In-place|
|---|---|---|---|---|
|Bubble Sort|O(n²)|O(n²)|||
|Selection Sort|O(n²)|O(n)|||
|Insertion Sort|O(n²)|O(n²)|||

---

##  Conclusión

> **Bubble Sort** es un algoritmo de enseñanza, útil para ilustrar cómo funciona el ordenamiento.  
> **No es adecuado para producción**, pero es una buena forma de **introducir comparaciones, intercambios y eficiencia algorítmica**.

---

¿Quieres que prepare una animación o simulación paso a paso con arrays reales? ¿O comparar su tiempo con Insertion y Selection Sort en Python o C?