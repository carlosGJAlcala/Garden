---
title: "Qubo Quadratic Unconstrained Binary Optimization"
date: 2025-01-01
tags:
  - ciencias-computacion
---

###  Problema del Viajante (TSP simplificado)

Un viajante debe visitar **3 ciudades** y volver al origen, pasando por cada ciudad **exactamente una vez**.  
Queremos encontrar el recorrido de **menor coste**.

---

###  Formulación QUBO

1. **Variables binarias**  
    Sea xi,tx_{i,t} una variable que vale 1 si la ciudad ii se visita en el paso tt, y 0 en caso contrario.
    

- i∈{1,2,3}i \in \{1,2,3\}
    
- t∈{1,2,3}t \in \{1,2,3\}
    

Ejemplo: x2,1=1x_{2,1}=1 significa que en el paso 1 vamos a la ciudad 2.

2. **Restricciones**
    

- Cada ciudad debe visitarse una vez:
    

∑txi,t=1,∀i\sum_t x_{i,t} = 1, \quad \forall i

- En cada paso, debe visitarse exactamente una ciudad:
    

∑ixi,t=1,∀t\sum_i x_{i,t} = 1, \quad \forall t

Estas restricciones se convierten en **penalizaciones cuadráticas** en la matriz QQ.

3. **Coste del recorrido**  
    Si el coste de viajar de la ciudad ii a la ciudad jj es dijd_{ij}, entonces:
    

Cdistancia=∑i,j,tdij xi,t xj,t+1C_{\text{distancia}} = \sum_{i,j,t} d_{ij} \, x_{i,t} \, x_{j,t+1}

4. **Función QUBO total**
    

C(x)=A⋅(restricciones)+B⋅(distancia)C(x) = A \cdot (\text{restricciones}) + B \cdot (\text{distancia})

donde AA y BB son pesos que equilibran restricciones y costes.

---

###  Ejemplo numérico con distancias

Supongamos:

d=[010151002015200]d = \begin{bmatrix} 0 & 10 & 15 \\ 10 & 0 & 20 \\ 15 & 20 & 0 \end{bmatrix}

- Ciudad 1 ↔ 2: distancia 10
    
- Ciudad 1 ↔ 3: distancia 15
    
- Ciudad 2 ↔ 3: distancia 20
    

El QUBO resultante es una matriz QQ de tamaño 9×99\times 9 (porque tenemos 9 variables binarias xi,tx_{i,t}).

D-Wave procesaría esta matriz y, tras el recocido, devolvería la ruta óptima:  
 1→2→3→11 \to 2 \to 3 \to 1 con coste total = **45** (10 + 20 + 15).

---

###  Conclusión

Este es un **ejemplo real**:

- Variables binarias representan elecciones de ruta.
    
- Restricciones se codifican como penalizaciones.
    
- El coste se minimiza buscando el recorrido más corto.
    

Es exactamente lo que hacen empresas como **Volkswagen** y **DHL** con D-Wave: optimizar rutas y logística en la vida real.