---
title: "Maquinas De Boltzmann"
date: 2026-01-26
tags:
  - ciencias-computacion
  - ia
---


## 1. Origen e inspiración física


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Las máquinas de Boltzmann (BM) nacen en 1985 (Hinton & Sejnowski) y se basan en la **mecánica estadística**.  
En física, la **distribución de Boltzmann** describe cómo un sistema en equilibrio térmico reparte su energía entre diferentes estados con una probabilidad:

$$
P(E) \propto e^{-\frac{E}{T}}
$$

donde:

- \( E \) = energía del estado  
- \( T \) = temperatura del sistema  

La idea en las BM es **asociar cada configuración de la red con un valor de energía**, y que la probabilidad de que la red adopte esa configuración siga esta distribución.



## 2. Arquitectura y neuronas

Una BM tiene:

- **Unidades visibles** (\( v \)): representan datos observables.  
- **Unidades ocultas** (\( h \)): aprenden representaciones internas.  
- **Pesos sin dirección fija** (\( W \)): conexiones **bidireccionales y simétricas**.  
- **Umbrales (bias)**: afectan la probabilidad de activación de cada neurona.  

Cada neurona es **binaria y estocástica**:

$$
s_i \in \{0,1\}
$$

pero no se activa de forma determinista, sino según una probabilidad logística dependiente de las entradas que recibe.

---

## 3. Función de energía

El corazón del modelo es la **función de energía**, que mide la “compatibilidad” de un estado \((v,h)\):

$$
E(v,h) = -\sum_{i} a_i v_i \;-\; \sum_{j} b_j h_j \;-\; \sum_{i,j} v_i W_{ij} h_j
$$

donde:

- \( a_i \) = bias de la neurona visible \( i \)  
- \( b_j \) = bias de la neurona oculta \( j \)  
- \( W_{ij} \) = peso entre la visible \( i \) y la oculta \( j \)  

Menor energía ⇒ mayor probabilidad.

La probabilidad de un estado es:

$$
P(v,h) = \frac{e^{-E(v,h)}}{Z}
$$

donde \( Z \) es la constante de normalización (_función de partición_), costosa de calcular porque implica sumar sobre todas las configuraciones posibles.

---

## 4. Entrenamiento

El entrenamiento busca ajustar \( W, a, b \) para que la distribución de la red se parezca a la de los datos.

**Procedimiento estándar (Contrastive Divergence en RBMs)**:

1. **Fase positiva**: fijar las visibles a un dato real y medir las correlaciones entre visibles y ocultas.  
2. **Fase negativa**: dejar que la red evolucione libremente y medir las correlaciones generadas.  
3. **Ajuste de pesos**:

$$
\Delta W \propto \langle v h \rangle_{\text{datos}} - \langle v h \rangle_{\text{modelo}}
$$

Este ajuste acerca la red a los datos y la aleja de estados irrelevantes.

---

## 5. Problema del coste computacional

En una BM completa, calcular \( Z \) y las fases es extremadamente lento, sobre todo en redes grandes.  
Esto llevó a crear la **Restricted Boltzmann Machine (RBM)**:

- **Restricción clave**: no hay conexiones dentro de visibles ni dentro de ocultas, sólo entre capas.  
- Esto permite que visibles y ocultas sean condicionalmente independientes y acelera el muestreo.

---

## 6. Aplicaciones

Aunque hoy las BM puras casi no se usan por su coste, sus derivadas (RBM, Deep Belief Networks) fueron esenciales en el renacimiento del _deep learning_. Ejemplos:

- **Reducción de dimensionalidad** (preentrenamiento antes de redes profundas).  
- **Modelos generativos** de datos binarios o continuos.  
- **Sistemas de recomendación** (Netflix Prize usó RBMs).  
- **Reconocimiento de patrones** en datos con estructura probabilística compleja.

---

## 7. Variantes modernas

- **RBM**: versión restringida y mucho más rápida.  
- **GB-RBM (Gaussian-Bernoulli RBM)**: para datos continuos.  
- **Deep Boltzmann Machines (DBM)**: varias capas de ocultas para capturar representaciones jerárquicas.  
- **Conditional RBM (CRBM)**: modela secuencias y datos temporales.

---
