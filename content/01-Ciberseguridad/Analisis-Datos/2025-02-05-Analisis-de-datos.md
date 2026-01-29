---
title: "2025 02 05 Analisis De Datos"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---

## **Selección de Características en Machine Learning**


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Kafka|Kafka]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/SISTEMA-DE-LAZO|SISTEMA DE LAZO]].

Existen tres enfoques principales para la **selección de características**, que buscan mejorar la eficiencia y precisión de un modelo al reducir la dimensionalidad de los datos:

1. **Filtrado de Métodos (Filter Methods)**
    
    - Se basa en técnicas estadísticas para evaluar la relevancia de cada característica de forma **independiente** del modelo de aprendizaje automático.
    - Algunos ejemplos de métodos de filtrado incluyen:
        - **Análisis discriminante lineal (LDA - Linear Discriminant Analysis)**: Evalúa qué variables separan mejor las clases.
        - **Chi-cuadrado (χ² test)**: Se utiliza para evaluar la relación entre características categóricas y la variable objetivo.
        - **Información Mutua**: Mide cuánta información sobre la variable objetivo aporta cada característica.
2. **Métodos Wrapper (Wrapper Methods)**
    
    - Utilizan el rendimiento de un modelo de aprendizaje automático para seleccionar la mejor combinación de características.
    - Funcionan como un **sistema de lazo cerrado**, donde se prueban múltiples subconjuntos de características y se elige aquel que optimiza el desempeño del modelo.
    - Técnicas comunes incluyen:
        - **Recursive Feature Elimination (RFE)**: Elimina características menos importantes de manera iterativa.
        - **Forward Selection**: Agrega características de una en una evaluando el rendimiento.
        - **Backward Elimination**: Comienza con todas las características y elimina una por una las menos relevantes.
3. **Métodos Embebidos (Embedded Methods)**
    
    - La selección de características se realiza **dentro del modelo** durante el entrenamiento, lo que mejora la eficiencia.
    - Algunos ejemplos incluyen:
        - **Random Forest**: Utiliza la importancia de características basada en árboles de decisión.
        - **Lasso Regression (L1 Regularization)**: Penaliza coeficientes pequeños, eliminando características irrelevantes.
        - **Gradient Boosting (XGBoost, LightGBM)**: Evalúa la contribución de cada variable al reducir el error.

 **Combinación de Métodos**  
En la práctica, estos enfoques pueden **complementarse** para mejorar la selección de características. Por ejemplo, un **filtro estadístico** puede usarse primero para descartar variables irrelevantes, seguido de un **wrapper method** para optimizar el modelo.

---

## **Regularización y Ajuste del Modelo**

La **regularización** es una técnica utilizada para evitar **sobreajuste (overfitting)** en los modelos de machine learning. Su objetivo es **encontrar un equilibrio** entre la complejidad del modelo y su capacidad de generalización.

 **Concepto de Regularización**  
Pasar de un modelo **mal ajustado** (overfitting) a un modelo **bien ajustado** (generalizable) mediante técnicas como:

- **L1 Regularization (Lasso)**: Elimina características poco relevantes estableciendo coeficientes en cero.
- **L2 Regularization (Ridge)**: Reduce el impacto de características menos importantes sin eliminarlas por completo.

---

## **Errores en Machine Learning: Sesgo y Varianza**

En la evaluación de modelos, existen dos tipos de errores fundamentales:

4. **Sesgo (Bias)**:
    
    - Representa la **simplificación excesiva** del modelo.
    - Un modelo con alto sesgo tiene **baja capacidad de aprendizaje** y es propenso a **underfitting**.
5. **Varianza (Variance)**:
    
    - Representa la **sensibilidad** del modelo a los datos de entrenamiento.
    - Un modelo con alta varianza se ajusta demasiado a los datos y **no generaliza bien** (overfitting).

El **trade-off entre sesgo y varianza** es crucial para obtener un modelo bien balanceado.

---

## **Detección de Anomalías**

La **detección de anomalías** es el proceso de identificar datos que se desvían significativamente del patrón normal de un conjunto de datos.

 **Eliminación de Outliers**  
Los **outliers** pueden afectar el rendimiento de los modelos, por lo que pueden eliminarse con técnicas como:

- **Métodos basados en estadística** (z-score, IQR).
- **Algoritmos basados en densidad o aislamiento**.

### **Algoritmos de Detección de Anomalías**

### **1. DBSCAN (Density-Based Spatial Clustering of Applications with Noise)**

- Es un algoritmo basado en **densidad** que **agrupa datos** y **detecta anomalías** como puntos aislados.
- Tiene dos **hiperparámetros** principales:
    - **ε (Epsilon)**: Radio dentro del cual los puntos se consideran parte de un mismo grupo.
    - **MinPts**: Número mínimo de puntos dentro de un radio **ε** para que una región sea considerada densa.
- **Clasificación de puntos**:
    - **Puntos internos**: Dentro de la densidad del clúster.
    - **Puntos frontera**: Cercanos al borde del clúster.
    - **Ruido**: Puntos fuera de cualquier clúster, considerados anomalías.

### **2. Isolation Forest (Bosque de Aislamiento)**

- Diseñado específicamente para **detección de anomalías**.
- Basado en el concepto de **Random Forest**.
- Funciona de la siguiente manera:
    1. Se toma un subconjunto aleatorio de los datos.
    2. Se construyen múltiples **árboles de decisión binarios**.
    3. Si un punto requiere **menos divisiones** para aislarse, es más probable que sea una **anomalía**.
- Se establece un **threshold** y si un punto supera ese umbral, se considera **anómalo**.

---

## **Conclusión**

- **La selección de características** es esencial para optimizar modelos de machine learning y puede lograrse con métodos de filtrado, wrappers o embebidos.
- **La regularización** ayuda a reducir el sobreajuste, mejorando la generalización del modelo.
- **La detección de anomalías** permite identificar outliers mediante algoritmos basados en densidad (DBSCAN) o aislamiento (Isolation Forest).



---

### **One-Class SVM**

El **One-Class SVM (Support Vector Machine)** es un método de **detección de anomalías** o **aprendizaje no supervisado** que aprende a diferenciar entre datos normales y valores atípicos (**outliers**).

 **Características principales:**  
 **Escalable a grandes volúmenes de datos** → Puede manejar conjuntos de datos grandes, aunque su eficiencia depende del kernel utilizado.  
 **Robusto** → Funciona bien con datos ruidosos y dispersos.  
 **Fácil de interpretar** → La idea básica es encontrar un hiperplano que encapsule la mayoría de los datos normales, y los puntos que quedan fuera se consideran **outliers**.

 **Ejemplo de uso:**

- **Detección de fraudes** en tarjetas de crédito.
- **Análisis de intrusiones en ciberseguridad**.
- **Control de calidad** en procesos industriales.

 **Cómo funciona:**

- Se ajusta un **hiperplano de separación** para modelar los datos normales.
- Cualquier punto que se aleje de esta frontera se considera un **outlier**.
- Se usa un **parámetro de umbral (nu)** para controlar la proporción de anomalías esperadas.

---

### **Hiperparámetro Tuning (Ajuste de Hiperparámetros)**

Los **hiperparámetros** afectan significativamente el rendimiento de un modelo de Machine Learning. Son parámetros que **no se aprenden directamente de los datos**, sino que se configuran antes del entrenamiento.

 **Ejemplo de hiperparámetro en modelos conocidos:**

- **Número de clusters en K-Means o KNN**.
- **Profundidad de un árbol en Random Forest**.
- **Tasa de aprendizaje en redes neuronales**.

 **Proceso de ajuste de hiperparámetros:**  
Se crea una **estructura iterativa** en la que se prueban diferentes valores de hiperparámetros para encontrar la mejor combinación. Esto se hace mediante:

1️⃣ **Grid Search (Búsqueda en rejilla)**

- Se prueban **todas las combinaciones posibles** de valores en un conjunto predefinido.
- **Desventaja:** Muy costoso computacionalmente.
- **Ejemplo en KNIME:** Usando **"Parameter Optimization Loop"**.

2️⃣ **Random Search (Búsqueda Aleatoria)**

- Se prueban combinaciones aleatorias de valores dentro de un rango.
- **Ventaja:** Menos costoso que Grid Search, pero no garantiza encontrar la mejor combinación.

3️⃣ **Bayesian Optimization (Optimización Bayesiana)**

- Se basa en modelos probabilísticos para **elegir los hiperparámetros más prometedores** en cada iteración.
- **Ventaja:** Más eficiente que Grid y Random Search.

---

### **Causal Machine Learning**

El **Causal Machine Learning** busca analizar la **relación causa-efecto** entre variables, en lugar de solo detectar correlaciones. Se usa en **gráficos causales** para evaluar si existe una relación real entre eventos.

 **Ejemplo:**

- **Medicina:** Evaluar si un medicamento causa un efecto positivo en pacientes.
- **Economía:** Determinar si un aumento en la inversión en publicidad realmente causa un aumento en las ventas.

 **Problema de correlaciones espurias:**  
A veces, dos variables parecen estar correlacionadas, pero no hay una relación causal real.

 **Ejemplo famoso:**

- **Número de películas de Nicolas Cage estrenadas por año vs. número de ahogamientos en piscinas.**
- Aunque los datos puedan mostrar correlación, **no hay una relación causal real**.

 **Técnicas utilizadas en causal ML:**

- **DAGs (Directed Acyclic Graphs)** → Representan relaciones causales.
- **Propensity Score Matching** → Para estimar efectos causales en estudios observacionales.
- **Instrumental Variables** → Método econométrico para inferir causalidad.

---

### **Datos en Streaming (Real-Time Data Processing)**

Los **datos en streaming** se generan y procesan en tiempo real, en lugar de almacenarse primero y analizarse después.

 **Ejemplo de aplicaciones:**

- **Bolsa de valores:** Análisis en tiempo real de precios de acciones.
- **Redes sociales:** Procesamiento en tiempo real de comentarios y tendencias.
- **Sensores IoT:** Monitoreo en fábricas o ciudades inteligentes.

 **Desafíos en procesamiento de datos en streaming:**  
1️⃣ **Alto volumen de datos** → Se necesitan técnicas para procesarlos sin almacenar todo.  
2️⃣ **Latencia** → Responder en tiempo real requiere sistemas altamente optimizados.  
3️⃣ **Técnicas de reducción de datos** → Métodos como **muestreo estadístico** o **agregaciones en ventana** ayudan a manejar grandes volúmenes.

 **Técnicas utilizadas:**

- **Apache Kafka** o **Apache Flink** para manejar datos en streaming.
- **Ventanas de tiempo (time windows)** para resumir los datos sin procesar cada evento individualmente.

---

### **Fine-Tuning y Modelos en Instancia**

El **fine-tuning** se refiere al ajuste final de un modelo después de haber sido preentrenado en un conjunto de datos grande.

 **Ejemplo:**

- En **LLMs (Large Language Models)** como **GPT o BERT**, el fine-tuning se realiza sobre datos específicos para adaptar el modelo a una tarea concreta.
- **Ejemplo en Visión Artificial:** Un modelo de clasificación preentrenado en imágenes generales se ajusta para reconocer **especies específicas de plantas**.

 **Modelos en Instancia:**  
Algunos modelos de Machine Learning funcionan **en tiempo real para cada instancia de datos** en lugar de entrenarse previamente en un dataset fijo.  
Ejemplo:

- **Sistemas de recomendación en e-commerce**, que ajustan su salida con cada nueva interacción del usuario.

---

### **Alta latencia en Machine Learning**

 **Alta latencia es un problema cuando el tiempo de respuesta del modelo es demasiado alto.**  
Ejemplo:

- En sistemas de **reconocimiento facial en aeropuertos**, la respuesta debe ser inmediata.
- En **trading algorítmico**, milisegundos pueden significar ganancias o pérdidas millonarias.

 **Soluciones para reducir la latencia:**

1. **Uso de modelos optimizados** (TensorRT, ONNX).
2. **Inferencia distribuida en la nube** para manejar grandes volúmenes.
3. **Caché de predicciones** para evitar recomputaciones innecesarias.

 **Es un problema complejo que requiere arquitecturas distribuidas y especialistas en optimización.**

---

### **MLOps (Machine Learning Operations)**

 **MLOps (Machine Learning Operations) es la disciplina encargada de la gestión del ciclo de vida de los modelos de ML en producción.**

 **Objetivos de MLOps:**

- **Monitoreo del modelo** en producción (accuracy, drift, latencia).
- **Automatización del despliegue** (CI/CD para modelos de ML).
- **Gestión de datos y experimentos**.

 **Ejemplo:**

- Modelos de predicción de demanda que se actualizan diariamente con nuevos datos.
- Detección de cambios en los datos (**Data Drift**) que pueden afectar el rendimiento del modelo.

 **Los modelos suelen estar en la nube y necesitan observabilidad para garantizar su desempeño en producción.**

---

### **Conclusión**

 Todos estos conceptos forman parte de la **ingeniería aplicada en Machine Learning**, ya sea para mejorar modelos, ajustar parámetros o resolver problemas de negocio.

 **"All models are wrong, but some are useful."**  
Esta frase destaca que **ningún modelo es perfecto**, pero si se ajusta correctamente, puede ser útil para la toma de decisiones.

Si necesitas más detalles sobre alguno de estos conceptos en **KNIME o Python**, dime y te ayudo a implementarlo. 

---

### **Detección de anomalías y SMOTE**

La **detección de anomalías** no requiere el uso de **SMOTE**. SMOTE (**Synthetic Minority Over-sampling Technique**) se usa para **balancear datasets desbalanceados en problemas de clasificación supervisada**, mientras que la **detección de anomalías es un problema no supervisado** en el que se buscan valores atípicos sin necesidad de igualar la proporción de clases.

---

### **WEKA en KNIME**

**WEKA** es un conjunto de herramientas de **aprendizaje automático**, y en KNIME puede utilizarse tanto para **modelos supervisados como no supervisados**. En la caja de WEKA en KNIME, si el modelo que usas es no supervisado (como clustering o detección de anomalías), no es necesario **remover la caja de etiquetas**, ya que el modelo trabaja sin etiquetas.

---

### **Dataset desbalanceado**

Un **dataset desbalanceado** es aquel en el que una clase es mucho más frecuente que otra.  
Ejemplo:

- En un dataset de detección de fraude, el **99% de las transacciones son legítimas** y solo el **1% son fraudulentas**.
- Este desequilibrio puede causar que un modelo aprenda a predecir siempre la clase mayoritaria, obteniendo una precisión engañosa.

 **Importante:** La **detección de anomalías** no entra en esta categoría, ya que en anomalías **no hay clases bien definidas**, sino que se buscan valores que difieren significativamente del patrón normal.

---

### **Normalización de datos**

La normalización se aplica cuando las variables tienen **valores en escalas muy diferentes**, lo que podría afectar modelos sensibles a magnitudes numéricas.  
 **Ejemplo:**

- Si tienes un dataset con **edad (20-80 años) y salario (1000-50000 euros)**, la diferencia de escala es grande y puede afectar algoritmos como **KNN, K-Means y SVM**.
- Si las diferencias entre valores son pequeñas o están en la misma escala, **no es necesario normalizar**.

 **Regla práctica:**

- **Usa normalización** cuando los valores varían en órdenes de magnitud diferentes.
- **No la uses** si las variables ya están en una escala similar y su magnitud no afecta el modelo.

---

### **Backward Elimination (Eliminación hacia atrás)**

La técnica de **Backward Elimination** comienza con **todas las características disponibles** y **va eliminando una a una** aquellas que aportan menos al modelo. En cada paso, se evalúa el impacto de eliminar una característica sobre el rendimiento del modelo.

 **Ejemplo:**

- Se entrena un modelo con todas las variables.
- Se elimina la característica menos significativa.
- Se vuelve a entrenar el modelo y se mide su rendimiento.
- Se repite hasta que solo quedan las características más relevantes.

 En **KNIME**, la evaluación se puede hacer con nodos como **"Scorer"** o en la **caja de evaluación (eva)**.

---

### **Líneas rojas en KNIME**

En KNIME, las **líneas rojas representan variables de flujo (Flow Variables)**. Estas variables permiten **pasar información de configuración o parámetros entre nodos sin modificar los datos tabulares**.

Ejemplo de uso:

- **Controlar dinámicamente el número de clusters en K-Means** sin modificar manualmente el nodo.
- **Configurar el número de iteraciones en un modelo de Machine Learning**.

---

### **Wrapper y entrenamiento del modelo**

El método **Wrapper** está estrechamente ligado al proceso de entrenamiento del modelo. Este enfoque evalúa la calidad de las características seleccionadas basándose en el desempeño del modelo.

 **Cómo funciona**:

4. Se elige un subconjunto de características.
5. Se entrena un modelo con esas características.
6. Se mide el rendimiento del modelo.
7. Se prueban diferentes combinaciones de características hasta encontrar la mejor.

 **Diferencia con otros métodos**:

- **Filtro**: Evalúa la importancia de las características sin entrenar un modelo.
- **Wrapper**: Usa el modelo para evaluar la selección de características (más costoso en computación).

---

### **Modelo sobreajustado (Overfitting) por pocas características**

Un modelo puede estar **sobreajustado** si tiene muy **pocas características** y se entrena en un conjunto de datos **muy pequeño o específico**.  
 **Ejemplo:**

- Si un modelo de detección de fraude usa **solo una o dos características**, es probable que se ajuste demasiado a esos valores y no generalice bien.
- La solución es **agregar más características relevantes o usar regularización**.

---

### **Gradient Boosting y XGBoost**

 **XGBoost (Extreme Gradient Boosting) es una implementación optimizada de Gradient Boosting.**

 **Gradient Boosting** → Algoritmo que construye árboles de decisión en secuencia, donde cada árbol corrige los errores del anterior.  
 **XGBoost** → Versión mejorada de Gradient Boosting con optimización en velocidad y regularización para evitar overfitting.

 **Cuándo usar XGBoost:**

- Datos estructurados con muchas variables.
- Competencias de Machine Learning (Kaggle).
- Cuando se necesita un modelo más rápido y preciso que Gradient Boosting estándar.

---

### **Diagrama de caja y cuartiles (Box Plot)**

Un **diagrama de caja (box plot)** representa la distribución de los datos mediante **cuartiles**:

8. **Línea central** → Mediana (Q2, 50% de los datos).
9. **Bordes de la caja** → Primer y tercer cuartil (Q1 y Q3).
10. **Bigotes** → Extensión de los datos sin incluir outliers.
11. **Puntos fuera de los bigotes** → Posibles **outliers**.

 **Se usa para visualizar la dispersión y detectar valores atípicos.**

---

### **Normalización en KNN y K-Means**

 **La normalización es fundamental en modelos basados en distancia como KNN y K-Means.**

- KNN clasifica con base en la distancia a los vecinos más cercanos.
- K-Means agrupa datos con base en la distancia a los centroides.

 **Si las características tienen escalas muy diferentes, los valores grandes dominarán el cálculo de distancia.**  
 Solución: **Normalizar o estandarizar los datos antes de usar KNN o K-Means**.

---

### **Supervisado vs. Clustering**

- **Si tienes un dataset con una columna de clase (label), estás haciendo clasificación supervisada**.
- **Si no tienes una columna de clase, es un problema de clustering (no supervisado)**.

 **Ejemplo:**  
 **Clasificación (supervisado)**: Detección de fraude (fraude/no fraude).  
 **Clustering (no supervisado)**: Agrupar clientes según comportamiento sin una etiqueta predefinida.

---

### **K-Means y características numéricas**

 **K-Means solo trabaja con características numéricas.**  
Si hay variables categóricas (texto), se deben **convertir a números** o eliminarlas antes de aplicar K-Means.

 **Solución:**

- **Usar One-Hot Encoding** para convertir texto en variables numéricas.
- **Eliminar variables categóricas irrelevantes**.

 **Antes de fijar la cantidad de clusters (K), revisa la distribución de los datos y usa el método del codo ("Elbow Method").**

---

### **Rule Engine para reemplazo de valores**

El nodo **Rule Engine** en KNIME permite **reemplazar valores de texto por valores numéricos** de manera eficiente.

 **Ejemplo:**  
Si tienes una columna "Categoría" con valores "Alto", "Medio" y "Bajo", puedes convertirlos en:

```
$Categoría$ = "Alto" => 3
$Categoría$ = "Medio" => 2
$Categoría$ = "Bajo" => 1
```

Así, la variable se convierte en numérica y puede usarse en modelos como **K-Means o Random Forest**.

---

### ** Conclusión**

Este texto mejora la claridad y profundidad de cada concepto. Si necesitas más detalles sobre **cómo implementarlo en KNIME**, dime y te ayudo con ejemplos específicos. 