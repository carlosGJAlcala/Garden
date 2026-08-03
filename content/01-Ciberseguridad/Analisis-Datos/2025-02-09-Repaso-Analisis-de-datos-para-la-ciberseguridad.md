---
title: "Tema 1 Introducción al aprendizaje automático"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---
# Tema 1 Introducción al aprendizaje automático


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

### Minería 
La minería de datos es el conjunto de análisis, tanto automáticos como semiautomáticos, que se utilizan para identificar patrones que se encuentran ocultos en los grandes conjuntos de datos."

Los patrones pueden ser de tres tipos relaciones de conjuntos de variables(regresión lineal).Identificación de grupos semejantes cluster e identifican de hechos de que suceden de forma conjunta ( reglas de asociación)
Un ejemplo de modelo de asociación puede ser el de la cesta de la compra que productos se compra conjuntamente porque guarda una relación macarrones y tomate por ejemplo.

La mínería de datos se enmarca dentro del proceso conocido como KDD knowlege discovery in databases

Si una empresa quiere predecir x seguirá estos paso :
- *Selección*  Elige que datos va manejar.
- *Análisis* revisa si falta datos , correlaciones y datos anómalos
- *Minería de datos * Entrena el modelo
- *Evaluación se valida la precisión del modelo con los datos de prueba*
- *Producción* Se usa el modelo para solventar un problema de negocio.
### Ciencia de datos
El tratamiento de los datos se divide en tres etapas
- **Etapa de Data Engineering y procesamiento de los datos:** Es donde se recolectan los datos e incluye tecnologías como _Big Data_.
- **Etapa de Data Science:** Con los datos procesados, la ciencia de datos emplea modelos estadísticos y algoritmos de _Machine Learning_ para extraer información útil.
- **DDD (Data-Driven Decision Making):** A partir de los datos, se toman decisiones, aunque dichas decisiones pueden ser tomadas de forma automática.
### Big data 

Los cinco principales atributos de **Big Data** son los siguientes:
- **Volumen:** Se refiere a las grandes cantidades de datos generados y almacenados.
- **Velocidad:** Es la rapidez con la que se manejan los datos, permitiendo procesar flujos casi en tiempo real.
- **Veracidad:** Los datos deben ser confiables, minimizando el ruido y la información incorrecta.
- **Valor:** Los datos deben aportar información útil y relevante para la toma de decisiones.
- **Variedad:** Implica el manejo de diferentes estructuras de datos, incluyendo datos estructurados, no estructurados y semiestructurados.
Dependiendo del enfoque a parte de de kdd se puede utilizar CRISP-DM (Cross Industry Standard Process for Data Mining) la diferencia principal entre uno y otro es que en kdd  no se parte de un modelo de negocio estableciodo o con una idea de negocio, si no que se intenta descubrir patrones y luego de esos patrones se hace el negocio.

### Evolución de la inteligencia artificial.
- **1950s – Inteligencia Artificial (IA Clásica)**
    
    - Primeras ideas sobre IA basadas en **sistemas expertos y reglas lógicas**.
    - No había aprendizaje, solo sistemas preprogramados.
- **1980s – Machine Learning**
    
    - Uso de modelos **probabilísticos y estadísticos** para detectar patrones en los datos.
    - Introducción de técnicas como árboles de decisión, regresión y redes neuronales básicas.
- **2010s – Deep Learning**
    
    - Expansión de las **redes neuronales profundas**, impulsadas por mejoras en hardware (GPUs).
    - Aplicaciones en **visión por computadora, reconocimiento de voz y procesamiento de texto**.
- **2020s – Modelos Generativos**
    
    - Nacimiento de IA generativa con modelos como **ChatGPT, Bard, Claude, WatsonX**, capaces de crear texto, imágenes, audio y más.
    - Avance en **modelos multimodales**, combinando texto, imagen y audio en un solo sistema.
Importante, en los 50 sale el test de turing , 60 ELIZA , En el 2017 google pública  Attention All you need
### ¿Qué es el aprendizaje automático?

Tiene tres partes:
+ Proceso de decision x-> y
+ Función de error evalua la predicción de le modelo
+ proceso de optimazación del modelo

### Clasificación de técnicas  de aprendizaje automático

Si tiene etiqueta puede ser de los siguiente tipos:
+ Clasificación
+ Regresión
Si no tiene puede ser 
+ Clustering, la diferencia con el de clasificación es que este no tiene etiqueta
Luego si toma acciones del entorno  es aprendizaje por refuerzo.
- Funciona sin necesidad de etiquetas aprende mediante recompesa y penalizaciones, toma las decisiones con fallo error imita el aprendizaje humano
### Algoritmos de machine learning
---

### **Clasificación**

- **SGD (Descenso por Gradiente Estocástico):** Se usa cuando se tiene un volumen de datos muy grande. La idea es encontrar una recta o un plano que separe las clases, pero en lugar de utilizar todos los puntos para calcular el descenso de gradiente y encontrar la mejor frontera, se utiliza una selección de puntos en lotes (_mini-batch_).
    
- **SVC (Support Vector Classifier):** Similar a SGD, pero en lugar de resolver un problema de descenso por gradiente, resuelve una ecuación cuadrática para encontrar el hiperplano óptimo de separación.
    
- **KNN (K-Nearest Neighbors):** Clasifica según la distancia entre los puntos.
    
- **Naive Bayes:** Utiliza el teorema de Bayes para determinar la probabilidad de que un elemento pertenezca a una determinada clase.
    
- **Kernel Approximation:** Transforma los datos en un espacio de mayor dimensión para encontrar una separación lineal en el modelo SVC.
    

---

### **Clustering**

- **MiniBatch K-Means:** Es una versión optimizada de K-Means que no usa todos los datos en cada iteración, sino que toma pequeños lotes aleatorios para actualizar los centroides.
    
- **K-Means:** Algoritmo de clustering no supervisado donde se eligen centroides de forma aleatoria y se actualizan iterativamente con el promedio de los puntos asignados a cada clúster, hasta alcanzar la convergencia.
    
- **GMM (Gaussian Mixture Model):** Supone que los datos provienen de una combinación de múltiples distribuciones gaussianas. En lugar de asignar etiquetas binarias, asigna probabilidades de pertenencia a cada clúster. Se usa cuando los datos no están claramente separados por bordes definidos y no tienen distribuciones compactas.
    
- **Spectral Clustering:** Método basado en teoría de grafos que usa álgebra lineal (descomposición espectral) para encontrar la mejor forma de dividir el grafo en comunidades. Antes de aplicar K-Means, se construye un grafo donde cada nodo representa un dato y las conexiones indican similitud. Es útil cuando se tienen estructuras complejas en conjuntos de datos grandes.
    

---

### **Regresión**

- **SGD Regressor:** Funciona igual que en clasificación, pero en este caso resuelve un problema de regresión.
    
- **Lasso Regression:** Técnica que elimina automáticamente variables irrelevantes, ayudando a prevenir el sobreajuste.
    
- **ElasticNet:** Combina **Lasso (L1)** y **Ridge (L2)** en un solo modelo, mejorando la capacidad de generalización y manejando la colinealidad entre variables. Es útil cuando hay muchas características correlacionadas y se quiere hacer selección de variables sin eliminar demasiadas.
    
- **Ridge Regression:** Variante de la regresión lineal que usa **regularización L2**, agregando una penalización por el uso de coeficientes grandes para reducir el sobreajuste.
    
- **SVR (Kernel='linear')**: Variante de SVM (**Support Vector Regression**) que busca la mejor recta de ajuste. Es una versión robusta de la regresión lineal.
    
- **SVR (Kernel='rbf')**: Permite modelar relaciones no lineales utilizando el **kernel RBF (Radial Basis Function)**. Transforma los datos en un espacio de mayor dimensión donde es más fácil encontrar un ajuste adecuado.
    
- **Ensemble Regressor:** Combina múltiples modelos de regresión para mejorar la precisión y estabilidad de las predicciones.
    

---

### **Reducción de Dimensionalidad**

- **Randomized PCA (Randomized Principal Component Analysis):** Versión optimizada de PCA que reduce la dimensionalidad de un dataset grande de forma más eficiente.
    
- **Isomap (Isometric Mapping):** Método de reducción de dimensionalidad no lineal basado en teoría de grafos y geometría, útil cuando los datos tienen estructuras curvas o manifolds.
    
- **Kernel Approximation:** Técnica utilizada para aproximar funciones kernel en Machine Learning, permitiendo que métodos lineales trabajen en espacios no lineales sin necesidad de calcular explícitamente la matriz del kernel.
    
- **LLE (Locally Linear Embedding):** Método de reducción de dimensionalidad no lineal que preserva la estructura local de los datos. Se basa en la idea de que los datos de alta dimensión suelen estar distribuidos en un espacio de menor dimensión (**manifold**) y busca representarlos en una dimensión más baja sin perder su estructura geométrica.
    

---

### Mlops
Paradigma objetivo implemntear y manterne modelos de manera confianca  es un compuesto de aprendizaje automático y desarrrollo continuao.