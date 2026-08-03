---
title: "Entrenamiento y Evaluación de Modelos"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---

# **Entrenamiento y Evaluación de Modelos**


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

#### **Oversampling y Undersampling**

- **Oversampling:** Técnica utilizada para aumentar la cantidad de ejemplos de la clase minoritaria en datasets desbalanceados. Ejemplo común: **SMOTE (Synthetic Minority Oversampling Technique)**, que genera ejemplos sintéticos interpolando entre puntos reales de la clase minoritaria.
- **Undersampling:** Reduce la cantidad de ejemplos de la clase mayoritaria, equilibrando el dataset al eliminar muestras. Esto puede llevar a pérdida de información si no se hace correctamente.

#### **Train-Test Split**

Dividir los datos en conjuntos de entrenamiento y prueba es esencial para evaluar el desempeño del modelo. En tu caso:

- Se utilizarán **20 datos para evaluación** (test set), mientras que el resto serán los datos de entrenamiento (train set). Esto asegura que el modelo se pruebe en datos no vistos previamente.
- El subconjunto de prueba **no debe tocarse** durante el entrenamiento para evitar sesgos.

#### **Fold Cross-Validation**

El método **k-fold cross-validation** divide los datos en `k` subconjuntos (folds):

1. Se entrena el modelo en `k-1` folds y se evalúa en el fold restante.
2. Este proceso se repite `k` veces, cambiando el fold de evaluación en cada iteración.
3. El resultado final es el promedio de las métricas en los `k` folds, ofreciendo una evaluación más robusta.

---

### **Métricas de Evaluación**

#### **R-cuadrado (R²)**

- Indica el porcentaje de varianza en los datos que el modelo es capaz de explicar.
- **Valor cercano a 1:** Buen ajuste.
- **Valor cercano a 0:** El modelo no explica bien los datos.

#### **Matriz de Confusión**

La matriz de confusión mide el desempeño de un modelo de clasificación, dividiendo las predicciones en cuatro categorías:

- **True Positives (TP):** Predicciones correctas de la clase positiva.
- **False Positives (FP):** Predicciones incorrectas como positivas.
- **True Negatives (TN):** Predicciones correctas de la clase negativa.
- **False Negatives (FN):** Predicciones incorrectas como negativas.

#### **Precisión y Exactitud**

- **Precisión:** Proporción de predicciones positivas correctas entre todas las predicciones positivas.  
    Fórmula: Precisioˊn=TPTP+FP\text{Precisión} = \frac{TP}{TP + FP}
- **Exactitud (Accuracy):** Proporción de predicciones correctas entre todas las predicciones.  
    Fórmula: Exactitud=TP+TNTP+TN+FP+FN\text{Exactitud} = \frac{TP + TN}{TP + TN + FP + FN}

#### **Curva ROC (Receiver Operating Characteristic)**

- Muestra la relación entre la **tasa de verdaderos positivos (TPR)** y la **tasa de falsos positivos (FPR)** para diferentes umbrales.
- El **AUC (Área Bajo la Curva)** es una métrica que resume el desempeño del modelo:
    - **AUC cercano a 1:** Modelo excelente.
    - **AUC = 0.5:** Modelo no mejor que el azar.

---

### **Equilibrio entre Sesgo y Varianza**

- **Sesgo alto:** Modelo demasiado simple (no captura la complejidad de los datos, underfitting).
- **Varianza alta:** Modelo demasiado complejo (se ajusta demasiado al conjunto de entrenamiento, overfitting).
- **Objetivo:** Encontrar un equilibrio entre la complejidad del modelo y el error, reduciendo tanto el sesgo como la varianza para mejorar el desempeño en la práctica.

---

### **Modelos Basados en Instancias y Basados en Modelos**

#### **Basados en Instancias:**

- Utilizan directamente los datos de entrenamiento para hacer predicciones.
- Ejemplo: **k-Nearest Neighbors (kNN).**
    - Ideal para bases de datos vectorizadas, donde se calcula la distancia entre puntos para clasificar o predecir.

#### **Basados en Modelos:**

- Construyen un modelo general a partir de los datos de entrenamiento.
- Ejemplo: **Regresión lineal, árboles de decisión, redes neuronales.**

---

### **Outliers en Modelos Basados en Valores**

- Los modelos basados en regresión o clasificación pueden verse afectados por outliers, que son valores extremos que no siguen la tendencia general de los datos.
- Técnicas para manejar outliers:
    1. **Eliminación:** Si se confirma que son errores de muestreo.
    2. **Transformaciones:** Aplicar logaritmos o escalado robusto para reducir su impacto.

---

### **Árboles de Decisión y Entropía**

En los árboles de decisión, la **entropía** se utiliza para medir la impureza de un nodo:

- **Entropía alta:** Mezcla de clases (mala clasificación).
- **Entropía baja:** Dominancia de una sola clase (buena clasificación).  
    El objetivo es reducir la entropía en cada división del árbol.

---

### **Modelos Ensemble: Bagging y Boosting**

#### **Bagging (Bootstrap Aggregating):**

- Combina varios modelos independientes para reducir la varianza.
- Ejemplo: **Random Forest**, que genera múltiples árboles de decisión y promedia sus predicciones.

#### **Boosting:**

- Combina modelos secuenciales, donde cada modelo corrige los errores del anterior.
- Ejemplo: **Gradient Boosting**, **AdaBoost**.

---

r2 = 1 es bueno puede que no generalice  la curva de ro tiene que ser una curva

metanodo agrupa varios nodos

hay que utilizar particion 
y  para poder utilizar  unos datos
dataset balanceado?
enlaces de tomen ?