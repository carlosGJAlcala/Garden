---
title: "Hash Tables"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
# Hash Tables

> **Relacionado**: Ver [[Dictionaries]] para abstracción. [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]] usa hash tables para cracking. [[02-Ciencias-Computacion/Compiladores_PNP/Tabla-de-Simbolos/Tabla-de-simbolos|Tabla de símbolos]] en compiladores. [[Big-Oh-Notation]] para complejidad.

---

## ¿Qué es una Hash Table?

Una **tabla hash** es una estructura que permite almacenar pares **clave → valor**, y **acceder a ellos rápidamente** (en tiempo promedio **O(1)**), usando una **función hash** que transforma la clave en un índice.

---

##  Estructura de una Hash Table

1. Una **función hash `h(k)`** que transforma la clave `k` en un índice numérico.
    
2. Una **tabla (array)** que almacena los datos en la posición `h(k)`.
    

### Ejemplo básico:

```plaintext
Clave     → Hash     → Índice en array
"ana"     → h("ana") → 3
"luis"    → h("luis") → 7
```

---

##  Operaciones básicas

|Operación|Descripción|Complejidad (promedio)|
|---|---|---|
|`insert(k, v)`|Inserta o actualiza el valor `v` asociado a `k`|O(1)|
|`lookup(k)`|Devuelve el valor asociado a la clave `k`|O(1)|
|`delete(k)`|Elimina la entrada con clave `k`|O(1)|

> ️ En el **peor caso** (muchas colisiones mal gestionadas), puede llegar a O(n)

---

##  ¿Qué es una función hash?

Es una función `h(k)` que convierte una clave (entero, string, objeto…) en un número entero, **dentro del rango del tamaño del array**.

Ejemplo simple:

```pseudocode
function h(k):
  return k mod 10
```

Para strings:

```pseudocode
function h(s):
  hash := 0
  for cada c en s:
    hash := hash * 31 + ASCII(c)
  return hash mod B
```

---

## ️ Colisiones y cómo resolverlas

### ¿Qué pasa si dos claves caen en la misma posición? → **Colisión**

#### Métodos para resolver colisiones:

###  1. **Open Hashing (Encadenamiento)**

Cada celda del array tiene una **lista enlazada de elementos** con el mismo hash.

```plaintext
tabla[3] → [ ("ana", 5), ("mario", 8) ]
```

- Fácil de implementar.
    
- No hay límite superior en la cantidad de elementos.
    

###  2. **Closed Hashing (Hashing abierto o direccionamiento abierto)**

Todos los datos se almacenan **dentro del array**. Si una celda está ocupada, se busca otra:

#### Estrategias:

- **Linear probing**:
    
    ```pseudocode
    h(k) = (hash(k) + i) mod B
    ```
    
- **Quadratic probing**
    
- **Double hashing** (usa segunda función hash)
    

> Más eficiente en memoria, pero más difícil de implementar.

---

##  Diseño de tamaño y carga

### ️ Load factor (factor de carga)

```pseudocode
α = n / B  // número de elementos dividido entre tamaño de la tabla
```

- Ideal mantener `α ≤ 0.7` para mantener rendimiento en O(1)
    
- Si `α` crece demasiado → **rehashing** (doblar tamaño y reinsertar todos los elementos)
    

---

##  Complejidad temporal

|Operación|Promedio|Peor caso (mala hash o carga)|
|---|---|---|
|Insert|O(1)|O(n)|
|Lookup|O(1)|O(n)|
|Delete|O(1)|O(n)|

Con buena función hash y factor de carga bajo, el comportamiento es cercano a O(1).

---

##  Ejemplo en pseudocódigo (open hashing)

```pseudocode
const B := 10
tabla := array[0..B-1] of lista

function insert(k, v):
  i := h(k)
  agregar (k, v) a tabla[i]

function lookup(k):
  i := h(k)
  buscar en tabla[i] el par con clave k
```

---

##  Ejemplo en Python (usando dict)

```python
d = {}
d["ana"] = 42
d["luis"] = 55
print(d["ana"])  # → 42
del d["luis"]
```

Bajo el capó, `dict` usa **hash tables con open addressing** y **hashing perfecto adaptativo**.

---

##  Usos reales de Hash Tables

- **Dictionaries / Maps** en lenguajes modernos (`dict`, `Map`, `HashMap`, `Hashtable`)
    
- **Bases de datos**: índices hash (no ordenados)
    
- **Compiladores**: tablas de símbolos
    
- **Caches**: acceso rápido a datos temporales
    
- **Firewalls y redes**: lookup de IPs o sesiones
    
- **Contadores**: conteo de ocurrencias (`Counter` en Python)
    

---

##  Conclusión

> Las **hash tables** son la estructura por excelencia cuando necesitas **acceso ultra-rápido por clave**, sin importar el orden.  
> El secreto está en **una buena función hash**, el manejo correcto de colisiones y mantener bajo el **load factor**.

---