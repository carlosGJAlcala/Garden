---
title: "Dictionaries"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
Perfecto. Vamos a desarrollar el **ADT Dictionary (Diccionario o Mapa Asociativo)**, una de las estructuras de datos más potentes y usadas tanto en software de alto nivel como en sistemas de bajo nivel.

---

##  ¿Qué es un Dictionary ADT?


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/DICCIONARIOS|DICCIONARIOS]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Un **Dictionary ADT** (diccionario) es una estructura que **asocia claves (keys) con valores (values)**, permitiendo:

> Buscar, insertar o eliminar un valor **usando su clave**.

Es una colección de **pares clave-valor (key → value)**, donde **las claves son únicas**.

---

##  Dictionary ADT – Especificación formal

###  Operaciones principales

|Operación|Descripción|
|---|---|
|`insert(k, v)`|Inserta el par `(clave, valor)` en el diccionario|
|`delete(k)`|Elimina la entrada con clave `k`|
|`lookup(k)`|Devuelve el valor asociado a la clave `k`|
|`member(k)`|Devuelve `true` si `k` está presente|
|`makenull()`|Vacía el diccionario|

---

###  Especificación en pseudocódigo

```pseudocode
spec DICTIONARY[KEY, VALUE]
genres dictionary, key, value

operations
  insert: dictionary × key × value → dictionary
  delete: dictionary × key → dictionary
  lookup: dictionary × key → value
  member: dictionary × key → boolean
  makenull: dictionary → dictionary
endspec
```

---

##  Comparación con otros ADT

|ADT|Acceso por posición|Acceso por clave|
|---|---|---|
|List|||
|Stack/Queue|||
|Set|| (solo clave)|
|**Dictionary**|| (clave + valor)|

---

## ️ Implementaciones comunes de diccionario

###  1. Hash Table (tabla hash)

- **Hash function `h(k)`** → transforma la clave en un índice del array.
    
- Se almacena el par clave-valor en ese índice.
    
- Colisiones se resuelven por **encadenamiento (listas)** o **rehashing (abierto)**.
    

 Operaciones promedio:

- `insert`, `lookup`, `delete` → **O(1)**  
     Peor caso: O(n) si hay muchas colisiones (mal hash o poca capacidad).
    

---

###  2. Árbol binario de búsqueda (BST)

- Claves se mantienen ordenadas.
    
- Permite recorrido ordenado (`inorder`).
    
- Coste medio: **O(log n)** si el árbol está balanceado.
    

 Usado cuando necesitas ordenar claves, rangos, o predecibilidad.

---

###  3. Trie (o radix tree)

- Claves son **strings** o secuencias.
    
- Cada nodo representa un prefijo.
    
- Útil para autocompletado, diccionarios de palabras, compresión.
    

---

##  Complejidad típica

|Implementación|Insert|Lookup|Delete|
|---|---|---|---|
|Hash Table|O(1)|O(1)|O(1)|
|BST|O(log n)|O(log n)|O(log n)|
|Trie|O(k)|O(k)|O(k)|

(k = longitud de la clave)

---

##  Ejemplo en pseudocódigo

```pseudocode
procedure buscarTelefono(dic, nombre)
  if member(dic, nombre) then
    return lookup(dic, nombre)
  else
    return "No encontrado"
```

---

##  Ejemplo en Python (dict = dictionary nativo)

```python
agenda = {}
agenda["Ana"] = "678-123456"
agenda["Luis"] = "610-987654"

print(agenda["Ana"])      # 678-123456
del agenda["Luis"]

if "Luis" in agenda:
    print("Existe")
else:
    print("No está")
```

---

##  Usos reales del Dictionary ADT

- **Bases de datos**: índices, claves primarias, relaciones clave-valor.
    
- **Lenguajes de programación**: `dict` (Python), `Map` (Java), `HashMap`, `Object` (JavaScript).
    
- **Compiladores**: tablas de símbolos (variables, funciones, etc.).
    
- **Cachés**: lookup rápido de datos previamente calculados.
    
- **IA / NLP**: conteo de palabras, vocabularios.
    
- **Redes y sistemas**: tablas de enrutamiento, sesiones de usuarios.
    

---

##  Conclusión

> El **Dictionary ADT** permite acceder a datos **por clave, no por posición**, lo que lo hace ideal para **estructuras de búsqueda rápida, relaciones complejas y sistemas con claves únicas**.  
> Su implementación más común es mediante **tablas hash**, pero también puede optimizarse con árboles o tries según el contexto.

---

¿Quieres ver una implementación manual de un diccionario con tabla hash en C, Python o Java? ¿O una versión especializada como un trie o un diccionario con ordenamiento?