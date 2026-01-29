---
title: "Pointer And Cursor"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
###  Pointer and Cursor: qué son y para qué se usan


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

En estructuras de datos y programación, **pointers (punteros)** y **cursors (cursores)** son herramientas fundamentales para **acceder y manipular datos dinámicamente**, especialmente en estructuras como listas, árboles y grafos.

---

##  1. **Pointers (punteros)**

Un **puntero** es una variable que **almacena la dirección de memoria de otro dato**. Es decir, no guarda el dato en sí, sino dónde está.

###  ¿Para qué sirven?

- Permiten crear estructuras **dinámicas** (listas enlazadas, árboles, grafos).
    
- Se usan para **acceder, modificar o liberar memoria**.
    
- En lenguajes como C, C++ o Pascal, son fundamentales para trabajar con memoria de bajo nivel.
    

###  Ejemplo en pseudocódigo:

```pseudocode
record Nodo
  valor: entero
  siguiente: ^Nodo  // puntero a otro nodo
endrecord

var p: ^Nodo
allocate(p)         // reserva memoria para un nodo
p^.valor := 10
```

> `p^` se usa para **acceder al valor apuntado** por el puntero `p`.

###  Operaciones típicas con punteros:

|Operación|Descripción|
|---|---|
|`allocate(p)`|Reserva memoria para un nuevo objeto|
|`dispose(p)`|Libera la memoria del objeto apuntado|
|`p^ := valor`|Modifica el contenido apuntado|
|`p := q`|Copia la dirección de `q` en `p`|

---

##  2. **Cursors (cursores)**

Un **cursor** es una alternativa a los punteros, **usada cuando el lenguaje no soporta punteros directamente** (como Java). Es una **variable de tipo entero** que indica **la posición de un objeto en una estructura de datos**, como una lista o array.

###  ¿Dónde se usan?

- En implementaciones de listas enlazadas con arrays (lista con cursores).
    
- En lenguajes sin punteros explícitos.
    
- En **programación funcional** o entornos educativos.
    

###  Ejemplo:

Supongamos que tenemos un array `SPACE[1..N]`, y cada posición representa un nodo.

```pseudocode
SPACE[5] = Nodo(valor=10, next=3)
cursor := 5
siguiente := SPACE[cursor].next  // siguiente = 3
```

Aquí, `cursor` es simplemente el índice dentro del array.

---

###  Comparativa rápida

|Característica|Pointer|Cursor|
|---|---|---|
|¿Qué almacena?|Dirección de memoria real|Índice entero en un array simulado|
|¿Lenguaje típico?|C, C++, Pascal|Java, pseudocódigo educativo|
|¿Acceso a datos?|`p^`|`SPACE[cursor]`|
|¿Memoria dinámica?|Sí, usando `allocate`/`dispose`|No directamente, pero se simula|
|¿Uso común?|Listas enlazadas, árboles, grafos|Simulación de estructuras dinámicas|

---

##  Conclusión

> **Punteros y cursores son mecanismos para conectar datos.** Los punteros apuntan directamente a memoria; los cursores simulan ese comportamiento con índices. Ambos permiten construir estructuras dinámicas como listas, árboles o grafos.

---

¿Quieres que te haga un ejemplo completo de lista enlazada con punteros y otro con cursores para ver la diferencia práctica?