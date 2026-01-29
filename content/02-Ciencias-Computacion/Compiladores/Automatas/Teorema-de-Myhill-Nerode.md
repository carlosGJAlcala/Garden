---
title: "Teorema De Myhill Nerode"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - automatas
---
## **Teorema de Myhill–Nerode**


> **Relacionado**: [[02-Ciencias-Computacion/Compiladores/Automatas/Automatas|Automatas]].

El **Teorema de Myhill–Nerode** es un resultado fundamental en la teoría de lenguajes formales que establece la base para **minimizar autómatas finitos deterministas (AFD)** y, al mismo tiempo, caracterizar si un lenguaje es **regular**.

En el contexto de los compiladores, este teorema se aplica para reducir el número de estados de un AFD sin perder la capacidad de reconocer el mismo lenguaje, lo que mejora la eficiencia del análisis léxico.

---

### **1. Planteamiento del teorema**

Un AFD puede contener **estados redundantes**: dos estados que, desde el punto de vista del lenguaje reconocido, son indistinguibles, es decir, **no existe ninguna cadena de entrada que permita diferenciar su comportamiento**.

**Definición de estados distinguibles:**  
Sean \( p \) y \( q \) dos estados de un AFD. Diremos que \( p \) y \( q \) son _distinguibles_ si existe al menos una cadena \( w \) tal que:

- Partiendo de \( p \), la lectura de \( w \) conduce a un estado **final**.
- Partiendo de \( q \), la lectura de \( w \) conduce a un estado **no final**, o viceversa.

Si no existe tal cadena \( w \), los estados son _indistinguibles_ y se pueden **fusionar** en el AFD minimizado.

---

### **2. Formulación formal del teorema**

Sea \( L \) un lenguaje sobre un alfabeto \( \Sigma \).  
Definimos la relación de equivalencia \( \equiv_L \) sobre \( \Sigma^* \) como:

$$
x \equiv_L y \iff \forall z \in \Sigma^*,\ (xz \in L \iff yz \in L)
$$

Es decir, dos cadenas \( x \) y \( y \) son equivalentes si, al añadirles cualquier sufijo \( z \), ambas pertenecen o no a \( L \).

El teorema afirma que:

1. El número de clases de equivalencia de \( \equiv_L \) es **igual** al número de estados del AFD mínimo que reconoce \( L \).
2. \( L \) es regular **si y solo si** el número de clases de equivalencia de \( \equiv_L \) es finito.

---

### **3. Algoritmo de minimización usando Myhill–Nerode**

**Entrada:** Un AFD \( M = (Q, \Sigma, \delta, q_0, F) \)  
**Salida:** Un AFD mínimo equivalente.

**Pasos:**

1. Construir una tabla para todos los pares posibles \( (Q_i, Q_j) \) de estados (sin repetición de orden).
2. **Inicialización:** marcar todos los pares en los que un estado es final y el otro no (distinguibles por definición).
3. **Propagación:** para cada par no marcado \( (Q_i, Q_j) \) y para cada símbolo \( a \in \Sigma \), comprobar si los estados \( (\delta(Q_i, a), \delta(Q_j, a)) \) ya están marcados.
   - Si lo están, marcar también el par \( (Q_i, Q_j) \).
   - Repetir hasta que no se puedan marcar más pares.
4. **Fusión:** todos los pares no marcados representan estados equivalentes que se pueden unir.
5. Reconstruir el AFD mínimo con los estados fusionados.

---

### **4. Ejemplo ilustrativo**

Supongamos un AFD con 6 estados \( Q = \{1, 2, 3, 4, 5, 6\} \) y un alfabeto \( \Sigma = \{a, b\} \).

- **Paso 1:** se construye la tabla de pares:
1 2 3 4 5 6  
1  
2  
3  
4  
5  
6
- **Paso 2:** se marcan todos los pares donde uno es final y el otro no.
- **Paso 3:** se revisan las transiciones: si algún par lleva a otro par ya marcado, también se marca.
- **Paso 4:** los pares no marcados representan estados equivalentes → se fusionan.

Este proceso es el que se ve en las diapositivas de tu documento, donde se parte de una tabla vacía, se marcan pares con diferencia final/no final y se propagan las marcas hasta estabilizar.

---

### **5. Relación con la minimización de AFD**

El teorema garantiza que:

- El AFD mínimo obtenido es **único** (salvo isomorfismos de nombres de estados).
- La minimización no afecta al lenguaje reconocido.
- Cualquier algoritmo de minimización correcto, explícito o implícito, está basado en la idea de **indistinguibilidad** que formaliza Myhill–Nerode.

---
