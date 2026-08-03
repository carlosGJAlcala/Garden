---
title: "Big Oh Notation"
date: 2025-01-01
tags:
  - ciencias-computacion
---

##  ¿Qué es la Notación Big O?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/HeapSort|HeapSort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Merge-Sort|Merge Sort]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Bubble-Sort|Bubble Sort]].

La **notación Big O** se usa para expresar **la complejidad algorítmica** en términos del **tamaño del problema**.

- Se centra en cómo **escala** el rendimiento, no en tiempos exactos.
    
- Representa una **cota superior asintótica**: cuánto tiempo/memoria **como máximo** puede tomar un algoritmo para una entrada de tamaño `n`.
    

>  Se ignoran **constantes y factores menores**: lo que importa es el **comportamiento a gran escala**.

---

##  Definición formal

> Una función `f(n)` es `O(g(n))` si existen constantes `c > 0` y `n₀ ≥ 0` tales que:

```text
f(n) ≤ c · g(n)   para todo n ≥ n₀
```

- `f(n)` es el tiempo real del algoritmo.
    
- `g(n)` es la función de referencia.
    
- `O(g(n))` representa la clase de funciones que crecen no más rápido que `g(n)`.
    

---

##  Ejemplos comunes

|Notación|Nombre|Ejemplo|Descripción|
|---|---|---|---|
|`O(1)`|Tiempo constante|Acceso a array por índice|No depende del tamaño de entrada|
|`O(log n)`|Logarítmico|Búsqueda binaria|Crece lentamente|
|`O(n)`|Lineal|Recorrer un array|Crece proporcionalmente|
|`O(n log n)`|Quasilineal|Heapsort, Mergesort|Mejor caso general para ordenar|
|`O(n²)`|Cuadrático|Doble bucle, Bubble Sort|Tiempo crece rápidamente|
|`O(2ⁿ)`|Exponencial|Fuerza bruta en combinatoria|Tiempo se dispara muy rápido|
|`O(n!)`|Factorial|Backtracking completo (como TSP)|Inviable salvo para `n` muy pequeño|

---

##  Aplicación práctica: cómo usarla

###  Análisis de bucles

```c
for (int i = 0; i < n; i++) {
    // O(1) → constante
}
→ O(n)
```

```c
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // O(1)
    }
}
→ O(n²)
```

###  Recursividad (Ej. Fibonacci)

```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

️ Este algoritmo tiene complejidad **O(2ⁿ)**

---

##  Comparativa de crecimiento

Si `n = 10`, ¿cuántas operaciones harías según cada notación?

|Notación|Aproximación para `n = 10`|
|---|---|
|O(1)|1 operación|
|O(log n)|~3 operaciones|
|O(n)|10 operaciones|
|O(n log n)|~30 operaciones|
|O(n²)|100 operaciones|
|O(2ⁿ)|1024 operaciones|
|O(n!)|3.6 millones de operaciones|

>  A medida que `n` crece, las diferencias **explotan exponencialmente**.

---

## ️ Otras notaciones relacionadas

Además de **Big O**, existen otras notaciones asintóticas útiles:

|Notación|Significado|
|---|---|
|**O(g(n))**|Cota superior (lo máximo que puede tardar)|
|**Ω(g(n))**|Cota inferior (lo mínimo que tarda)|
|**Θ(g(n))**|Cota ajustada (tiempo exacto asintótico)|
|**o(g(n))**|Crece estrictamente más lento que `g(n)`|
|**ω(g(n))**|Crece estrictamente más rápido que `g(n)`|

Pero en la práctica, **Big O** es la más usada, especialmente para describir el **peor caso**.

---

##  Conclusión

> La **notación Big O** te permite **razonar sobre el rendimiento de un algoritmo sin necesidad de ejecutarlo**, ayudándote a:
> 
> - Comparar alternativas.
>     
> - Elegir la estructura de datos adecuada.
>     
> - Optimizar código que debe escalar con grandes volúmenes de datos.
>     

---

# Ejemplos en código y cálculo de complejidad

Ejemplos paso a paso de cómo calcular complejidad con operaciones matemáticas (sumas, productos, potencias, logaritmos). Contar operaciones elementales lleva directamente a la notación Big O.

---

## Ejemplo 1: Bucle simple – **O(n)**

```c
void imprimir(int n) {
    for (int i = 0; i < n; i++) {
        printf("%d\n", i);
    }
}
```

###  Análisis:

- La línea `printf` se ejecuta **una vez por iteración**.
    
- El bucle se ejecuta **n veces**.
    

###  Total de operaciones:

T(n)=1+n×O(1)=O(n)T(n) = 1 + n × O(1) = O(n)

> **Resultado**: Tiempo lineal → **O(n)**

---

##  Ejemplo 2: Bucle anidado – **O(n²)**

```c
void imprimirPares(int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d, %d\n", i, j);
        }
    }
}
```

###  Análisis:

- El bucle exterior se ejecuta **n veces**.
    
- Por cada iteración del bucle exterior, el bucle interior se ejecuta **n veces**.
    

###  Total de operaciones:

T(n)=n×n×O(1)=n2×O(1)=O(n2)T(n) = n × n × O(1) = n² × O(1) = O(n²)

> **Resultado**: Tiempo cuadrático → **O(n²)**

---

##  Ejemplo 3: Búsqueda binaria – **O(log n)**

```c
int busquedaBinaria(int arr[], int n, int x) {
    int izq = 0, der = n - 1;
    while (izq <= der) {
        int medio = (izq + der) / 2;
        if (arr[medio] == x) return medio;
        if (arr[medio] < x) izq = medio + 1;
        else der = medio - 1;
    }
    return -1;
}
```

###  Análisis:

- Cada iteración **reduce el tamaño del problema a la mitad**.
    
- La pregunta es: ¿cuántas veces puedo dividir `n` entre 2 hasta que sea 1?
    

###  Total de operaciones:

n→n/2→n/4→n/8→...→1Nuˊmerodeiteraciones≈log2(n)T(n)=O(logn)n → n/2 → n/4 → n/8 → ... → 1 Número de iteraciones ≈ log₂(n) T(n) = O(log n)

> **Resultado**: Tiempo logarítmico → **O(log n)**

---

##  Ejemplo 4: Mergesort – **O(n log n)**

```c
void mergeSort(int arr[], int izq, int der) {
    if (izq < der) {
        int medio = (izq + der) / 2;
        mergeSort(arr, izq, medio);
        mergeSort(arr, medio+1, der);
        merge(arr, izq, medio, der); // combina los subarrays
    }
}
```

###  Análisis:

- Divide el array en 2 mitades → **log₂(n)** divisiones.
    
- Combina los subarrays (función `merge`) → O(n) en cada nivel.
    

###  Total de operaciones:

T(n)=O(n)trabajopornivel×O(logn)niveles=O(nlogn)T(n) = O(n) trabajo por nivel × O(log n) niveles = O(n log n)

> **Resultado**: Tiempo quasilineal → **O(n log n)**

---

##  Ejemplo 5: Fibonacci recursivo – **O(2ⁿ)**

```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

###  Análisis:

- El árbol de recursión crece exponencialmente:
    

```text
fib(n)
├─ fib(n-1)
│  ├─ fib(n-2)
│  │  ├─ ...
├─ fib(n-2)
```

- Cada llamada genera **2 llamadas recursivas**, menos en los casos base.
    

###  Total de operaciones:

T(n)≈2nT(n) ≈ 2^n

> **Resultado**: Tiempo exponencial → **O(2ⁿ)**

---

##  Reglas básicas para calcular la complejidad

###  Regla 1: **Sumas → se queda el mayor**

T(n)=O(n2+n+1)→O(n2)T(n) = O(n² + n + 1) → O(n²)

### ️ Regla 2: **Bucles anidados → multiplicación**

foriin1..nforjin1..n→O(n×n)=O(n2)for i in 1..n for j in 1..n → O(n × n) = O(n²)

###  Regla 3: **División recursiva → O(log n)** (si se parte en 2)

while(n>1)n=n/2while (n > 1) n = n / 2

---

##  Bonus: Big O en operaciones concretas

|Operación|Complejidad|
|---|---|
|Acceder a elemento array|O(1)|
|Buscar en lista enlazada|O(n)|
|Insertar al final en array|O(1)|
|Insertar en lista enlazada|O(1)|
|Búsqueda binaria|O(log n)|
|Merge Sort|O(n log n)|
|Bubble Sort|O(n²)|

---

##  Conclusión

> La notación Big O es una **herramienta matemática** que permite **predecir el comportamiento de un algoritmo** para grandes entradas.  
> Contando operaciones elementales (sumas, multiplicaciones, recursión), puedes **analizar el rendimiento** de cualquier algoritmo.

---