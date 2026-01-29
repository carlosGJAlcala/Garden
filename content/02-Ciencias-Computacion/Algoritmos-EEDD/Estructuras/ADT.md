---
title: "Adt"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
  - estructuras
---
Un **ADT** (Abstract Data Type o Tipo Abstracto de Datos) es un modelo teórico que define un conjunto de **datos** y las **operaciones** válidas sobre ellos, **sin especificar cómo están implementados internamente**.

---

###  ¿Qué significa esto?


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Hash-tables|Hash tables]].

Un ADT se centra en **qué se puede hacer** con los datos (es decir, las operaciones disponibles), **no en cómo** se implementan esas operaciones.

Por ejemplo, una **pila (stack)** como ADT tiene operaciones como:

- `push`: añadir un elemento al tope.
    
- `pop`: quitar el elemento del tope.
    
- `top` o `peek`: mirar el elemento del tope.
    
- `empty`: comprobar si está vacía.
    

Pero no dice **si está hecha con arrays, listas enlazadas, o punteros**. Eso es parte de su implementación, no de su definición como ADT.

---

###  Utilidad de los ADT

1. **Encapsulan la complejidad**
    
    - El usuario puede usar el ADT sin saber cómo funciona por dentro.
        
    - Por ejemplo, puedes usar una lista sin saber si es una lista doblemente enlazada o un vector dinámico.
        
2. **Permiten el diseño modular**
    
    - Puedes cambiar la implementación sin modificar el resto del sistema.
        
    - Si implementas una cola con un array circular en lugar de con una lista, el usuario no debería notar el cambio si el ADT está bien diseñado.
        
3. **Facilitan la reutilización de código**
    
    - Un mismo ADT puede usarse en distintos contextos (p. ej., una pila para análisis de expresiones o para backtracking en algoritmos de grafos).
        
4. **Base del diseño de estructuras de datos**
    
    - Los ADT son el puente entre la **lógica del problema** y la **estructura física de los datos**.
        
    - Permiten pensar a nivel lógico (ej. “necesito una colección donde elimine el mínimo”) sin preocuparse de la implementación (¿heap binario? ¿árbol AVL?).
        
5. **Favorecen la claridad del código y la documentación**
    
    - Cuando defines un ADT estás declarando lo que una estructura **puede hacer y cómo se espera que se comporte**.
        

---

###  Ejemplos de ADT comunes

|ADT|Operaciones típicas|
|---|---|
|Lista|insert, delete, locate, retrieve, next, previous|
|Pila (stack)|push, pop, top, empty, makenull|
|Cola (queue)|enqueue, dequeue, front, empty|
|Árbol|parent, leftmost_child, right_sibling, label, create|
|Diccionario|insert, delete, member (a veces se representa con hash tables)|
|Cola con prioridad|insert, deletemin o deletemax, findmin/findmax|

---

###  Resumen

> Un ADT define **qué operaciones** se pueden realizar sobre una colección de datos y **qué comportamiento** deben tener, sin decir cómo se implementa. Su uso permite diseñar software **modular, reutilizable, mantenible y más fácil de entender**.

**las interfaces son una forma directa de representar un ADT** en programación orientada a objetos.

---

###  ¿Por qué una interfaz representa un ADT?

Un **ADT** define un **modelo abstracto** con **operaciones públicas**, pero **oculta la implementación interna**. Una **interfaz en Java** hace exactamente eso:

- Define **qué operaciones** (métodos) debe tener una clase.
    
- **No especifica cómo** esas operaciones están implementadas.
    
- Cualquier clase que implemente la interfaz puede tener **su propia implementación interna**.
    

---

###  Ejemplo real: Lista

En Java:

java

CopiarEditar

`public interface List<E> {     void add(E element);     E get(int index);     E remove(int index);     int size();     boolean isEmpty(); }`

Esto representa un **ADT tipo Lista**.

Luego tienes múltiples **implementaciones**:

- `ArrayList<E>`: usa un array dinámico.
    
- `LinkedList<E>`: usa nodos enlazados.
    
- `CopyOnWriteArrayList<E>`: versión concurrente.
    

El código cliente puede usar la interfaz `List` sin saber qué clase concreta hay detrás:

java

CopiarEditar

`List<String> nombres = new ArrayList<>(); nombres.add("Ana"); nombres.add("Luis");`

Si mañana cambias `ArrayList` por `LinkedList`, el resto del código puede seguir igual. Esa es la **potencia del ADT como interfaz**.

---

###  Otros ejemplos comunes en Java

|Interfaz (ADT)|Implementaciones|
|---|---|
|`List`|`ArrayList`, `LinkedList`, etc.|
|`Set`|`HashSet`, `TreeSet`, `LinkedHashSet`|
|`Map` (diccionario)|`HashMap`, `TreeMap`, `LinkedHashMap`|
|`Queue`|`LinkedList`, `PriorityQueue`, etc.|
|`Deque`|`ArrayDeque`, `LinkedList`, etc.|

Todas estas interfaces definen un **ADT**, y cada implementación tiene **distintas características de rendimiento, orden, concurrencia, etc.**

---

###  Conclusión

> Sí, en Java las **interfaces son la forma natural de implementar ADTs**. Permiten diseñar software flexible, extensible y desacoplado. Separan la lógica de “qué hace” una estructura (interfaz) de “cómo lo hace” (clase concreta), que es justamente la filosofía detrás de los Tipos Abstractos de Datos.

¿Quieres que te muestre cómo crear tu propio ADT como interfaz en Java paso a paso?