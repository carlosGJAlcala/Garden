---
title: "Redes Neuronales y Convoluciones"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---

# Redes Neuronales y Convoluciones


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[00-Inicio/HOME|HOME]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

Las **redes neuronales convolucionales (CNNs)** son un tipo de arquitectura de redes neuronales diseñadas específicamente para procesar datos con una estructura de cuadrícula, como imágenes.

Las **convoluciones** dentro de estas redes funcionan como filtros que extraen características relevantes de los datos de entrada. A través de la aplicación de **kernels (filtros convolucionales)**, la red puede detectar patrones como bordes, texturas y formas en diferentes capas de procesamiento.

El proceso de convolución ayuda a reducir la cantidad de información irrelevante, manteniendo solo los aspectos más importantes. Esto permite que la red neuronal **aprenda representaciones jerárquicas** de los datos de entrada, mejorando la capacidad del modelo para reconocer y clasificar objetos de manera eficiente.

Una CNN consta de varias capas clave:

- **Capa de Convolución:** Aplica filtros para extraer características esenciales.
- **Capa de Pooling:** Reduce la dimensionalidad de los datos y mejora la eficiencia computacional.
- **Capas Densas (Fully Connected):** Procesan la información extraída para realizar la clasificación o predicción final.

Las redes convolucionales son ampliamente utilizadas en **visión por computadora**, detección de objetos, reconocimiento facial, análisis de imágenes médicas y muchas otras aplicaciones.

---

## Video sobre Redes Neuronales

Explicación detallada del funcionamiento de las redes neuronales convolucionales, su estructura y cómo pueden aplicarse a diferentes problemas de clasificación y procesamiento de imágenes.

---

# Examen

Para la evaluación, se recomienda realizar una tabla en la que se analicen los siguientes aspectos clave:

- **Falsos positivos:** Casos en los que el modelo predice incorrectamente una clase positiva cuando en realidad es negativa.
    
- **Falsos negativos:** Casos en los que el modelo no detecta correctamente una clase positiva.
    
- **Accuracy:** Medida de la precisión global del modelo, calculada como:
    $$
    Accuracy=TP+TNTP+TN+FP+FNAccuracy = \frac{TP + TN}{TP + TN + FP + FN}
    $$
    Donde:
    
    - **TP (True Positives):** Casos correctamente clasificados como positivos.
    - **TN (True Negatives):** Casos correctamente clasificados como negativos.
    - **FP (False Positives):** Falsas alarmas.
    - **FN (False Negatives):** Omisiones de detección.

Además del accuracy, se pueden considerar otras métricas como **precisión, recall y F1-score** para evaluar el rendimiento del modelo de manera más completa.

---

# Instalación de Conda para Redes Neuronales (CDD)

Para trabajar con redes neuronales en entornos optimizados, se recomienda la instalación de **Conda**, un sistema de gestión de paquetes y entornos virtuales que facilita la instalación de bibliotecas especializadas en aprendizaje profundo.

### **Pasos para la instalación y configuración:**

1. **Configurar Conda y definir el `PATH` correctamente**
    
    - Si Conda no está en el `PATH`, se debe agregar manualmente en el archivo de configuración del sistema.
    - En Linux:
        
        ```bash
        echo 'export PATH="$HOME/miniconda3/bin:$PATH"' >> ~/.bashrc
        source ~/.bashrc
        ```
        
    - En Windows, agregar la ruta de Conda en las variables de entorno.
2. **Instalar las extensiones de Deep Learning**
    
    - Una vez instalado Conda, se recomienda crear un entorno virtual específico para redes neuronales:
        
        ```bash
        conda create --name deep_learning_env python=3.9
        conda activate deep_learning_env
        ```
        
    - Luego, instalar las bibliotecas necesarias para redes neuronales:
        
        ```bash
        conda install tensorflow keras pytorch torchvision torchaudio
        ```
        
3. **Configurar Python con Conda**
    
    - Para asegurarse de que Python esté correctamente configurado dentro del entorno de Conda, ejecutar:
        
        ```bash
        conda config --set auto_activate_base false
        ```
        
    - Si se usa Jupyter Notebook, instalarlo dentro del entorno:
        
        ```bash
        conda install -c conda-forge jupyterlab
        ```
        

Con esta configuración, se dispone de un entorno optimizado para el desarrollo de modelos de redes neuronales utilizando TensorFlow, Keras y PyTorch.

---


# Práctica en KNIME

## **1. Preprocesamiento de Datos**

- Verificar si hay **valores faltantes** en el dataset.
- Como el problema tiene **6 grupos**, se trata de una **tarea de clasificación**, y utilizaremos **redes neuronales** para resolverlo.
- Renombrar la columna `col36` a **`label`**, especialmente si su significado no está claro.
- **Normalización de los datos:**
    - Escalar los valores entre **0 y 1** para mejorar la estabilidad del entrenamiento.

## **2. Ingeniería de Características**

- Aplicar **filtrado de características** si es necesario.
- **Particionamiento de los datos:**
    - Utilizar un **muestreo estratificado**, lo que significa que los valores se extraen de manera balanceada por clase.
    - Se toma un **33% de los datos por clase** para el conjunto de prueba.
    - En problemas **multiclase**, este método evita que una clase esté sobrerrepresentada.

---

## **3. Implementación de la Red Neuronal en Python (TensorFlow)**

Dado que en KNIME puede ser más complejo configurar redes neuronales avanzadas, implementaremos el modelo en **Python con TensorFlow**.

### **Definición de la Red Neuronal**

- **Parámetros iniciales:**
    
    - Número de columnas (entradas).
    - Número de clases (salidas).
    - Número de neuronas en la capa oculta.
- **Estructura de la red:**
    
    1. **Capa de entrada** (Placeholder).
    2. **Capas ocultas**:
        - Usamos **10 capas ocultas** con activación **ReLU**.
        - La capa de entrada tiene tantas neuronas como **columnas de datos**.
    3. **Capa de salida**:
        - 6 neuronas para **6 clases**.
        - Función de activación **Softmax** para la clasificación multiclase.

### **Entrenamiento de la Red Neuronal**

- **Variables de entrenamiento:**
    
    - `x_train`: datos de entrada.
    - `y_train`: etiquetas de salida.
    - `batch_size = 32`: divide los datos en lotes pequeños para optimizar el entrenamiento.
    - `epoch = 100`: el número de iteraciones completas sobre el dataset.
- **Optimización y pérdida:**
    
    - Función de pérdida: **Error cuadrático medio (MSE)** o **Entropía cruzada**, según el caso.
    - Se selecciona un **optimizador adecuado** (ej. Adam).
- **Proceso de entrenamiento:**
    
    - Para cada época:
        1. Se divide el conjunto en **batches**.
        2. Se entrena la red neuronal.
        3. Se calcula el error y se ajustan los pesos para mejorar el rendimiento.
    - Se grafica la **pérdida** en cada época para monitorear la convergencia del modelo.

---

## **4. Evaluación del Modelo en KNIME**

- **Configuración de ejecución:**
    
    - Se utiliza el nodo `Network Execution`.
    - Configurar `input batch size`.
    - Marcar la opción **"Keep Input Column"** para conservar el dataset original.
- **Limitaciones de las Redes Neuronales:**
    
    - **Alto consumo computacional**, especialmente para redes profundas.
    - La salida es un conjunto de **6 neuronas** con probabilidades.
    - Se debe convertir la salida en un solo valor para facilitar la evaluación.
- **Conversión de la salida:**
    
    - Usar `Many-to-One` para reducir las 6 columnas de probabilidad a una única predicción.
    - Seleccionar la **categoría con la probabilidad más alta**.
- **Evaluación con métricas:**
    
    - Usar el nodo `Score` en KNIME.
    - Medir **precisión, recall y F1-score**.

**Nota:** Si importas un **workflow**, **resetea los datos** para evitar que pesen demasiado, especialmente cuando se despliega.

---

## **5. Implementación con Keras en KNIME**

El uso de **nodos de Keras en KNIME** permite mayor flexibilidad en la arquitectura, aunque requiere configuraciones adicionales.

### **Definición del Modelo con Keras**

- **Capa de entrada:**
    - Se requiere un **filtrado de datos** previo si el dataset contiene ruido.
- **Capas intermedias (Densas):**
    - Definir el número de **neuronas ocultas**.
    - Función de activación recomendada: **ReLU**.
- **Capa de salida:**
    - Se definen **6 neuronas** para clasificación.
    - Se usa la función de pérdida **Mean Squared Error**.

### **Entrenamiento del Modelo**

- Configuración en Keras:
    - `epochs = 32`
    - Se selecciona un **optimizador adecuado** para la convergencia de la función de pérdida.
    - **Compatibilidad con CUDA:** KNIME permite utilizar **GPU** para acelerar el entrenamiento.
- **Diferencias con el código en Python:**
    
    - En KNIME se usa **Keras en lugar de TensorFlow puro**.
    - Los hiperparámetros pueden modificar el resultado final.

---

## **6. Redes Neuronales Convolucionales en KNIME**

Las **redes convolucionales (CNNs)** son ideales para **procesamiento de imágenes**.

### **Estructura de la Red Convolucional**

- **Capas principales:**
    - **Capa de convolución con pooling:**
        - Aplicación de **filtros para extraer características**.
        - La cantidad de **neuronas no depende del tamaño de la imagen**.
    - **Capa `Flatten`**: convierte las características en una estructura lineal.
    - **Capa `Dropout`**: previene **overfitting**.
    - **Capa de salida:**
        - Se usa **una única neurona** para clasificación binaria con activación **sigmoide**.

### **Configuración en Keras para imágenes**

- Se utilizan imágenes de **150x150 píxeles** con **3 canales RGB**.
- **Parámetros importantes:**
    - Tamaño del **kernel** y el **stride**.
    - **Activación `ReLU`**.
    - Aplicación de **32 filtros** para extraer características.
    - **Capa densa con 64 neuronas**.
    - La **capa de salida usa activación sigmoide** para clasificación binaria.

### **Preprocesamiento del Dataset en KNIME**

1. **Carga de datos:**
    - KNIME permite el uso de repositorios en la nube, aunque en su versión de pago.
    - Las etiquetas suelen estar en el **nombre de los archivos**.
2. **Extracción de la ubicación:**
    - Ordenar los datos según la **dirección del `Path`**.
    - Extraer la localización como una columna adicional.
    - Usar `Rule Engine` para asignar etiquetas:
        
        ```plaintext
        $location$ LIKE "CAT" => "CAT"
        ```
        
    - Asegurarse de que los nombres de carpeta **no contengan etiquetas ambiguas**.

### **Transformación de Imágenes**

- Las redes neuronales trabajan con **valores numéricos**, por lo que:
    - Se asigna **True = 0** y se normalizan los demás valores.
    - Se usa `Image Reader` para cargar imágenes en memoria.
    - Se pueden usar **metadatos** para enriquecer el modelo.
    - Se redimensionan las imágenes con `Image Resizer`.
    - Se eliminan columnas innecesarias (`Path`).
    - Se divide el dataset en **80% entrenamiento y 20% prueba** con `Stratified Sampling`.

---

## **7. Configuración de Conda en KNIME**

- KNIME permite copiar configuraciones de Conda.
- Se recomienda configurar **Conda como hiperparámetro**.
- Activar las opciones:
    - **"Shuffle training data before each epoch"**.
    - **"Use random seed"** para mejorar la estabilidad del entrenamiento.
- **Optimizador recomendado:** `Adam`.
- **Función de pérdida:** `Binary Cross Entropy`.

---



Aquí tienes el texto corregido y expandido para mayor claridad y precisión:

---

# **Proximidad de Clases y Análisis de Redes**

Aunque el concepto de **proximidad de clases** no está directamente vinculado con **Machine Learning**, sí es relevante en el **análisis de redes** y en el entrenamiento de modelos en **grafos**.

### **Entrenamiento en Grafos y Procesamiento de Datos**

- El **procesamiento de grafos** es una técnica utilizada para analizar **relaciones complejas** en los datos.
- Se aplica en diversas áreas como:
    - **Sistemas de recomendación** (ej. algoritmos de propagación en redes sociales).
    - **Análisis de fraudes** en transacciones financieras.
    - **Optimización de redes de transporte**.
- **Diferencia con Machine Learning tradicional:**
    - En lugar de entrenar modelos basados en características tabulares o imágenes, se usan **estructuras de grafos** donde los **nodos representan entidades** y los **aristas representan conexiones**.

### **Procesamiento Natural del Lenguaje (NLP) e Inteligencia Artificial General (AGI)**

- NLP se enfoca en la interpretación y generación de lenguaje natural por parte de máquinas.
- La Inteligencia Artificial General (AGI) busca desarrollar sistemas capaces de razonar y aprender de manera similar a los humanos.
- Ambas áreas pueden beneficiarse del análisis de redes, especialmente en tareas como la representación de conocimiento y el aprendizaje basado en relaciones.

---

# **Datasets Relevantes**

Algunos datasets utilizados en análisis de redes y Machine Learning incluyen:

1. **DeepLi, Jarle y Kun MDSTI**
    
    - Son datasets avanzados utilizados en **investigaciones de IA**.
    - Meta (anteriormente Facebook) los ha utilizado en proyectos de vanguardia.
2. **Jarnel Pool**
    
    - Es un dataset de **números**, útil para **reconocimiento de matrículas**.
    - En lugar de usar redes neuronales, se pueden aplicar **filtros tradicionales** para mejorar la precisión.

---

# **Modelado Numérico en Machine Learning**

Para problemas de clasificación numérica, se pueden utilizar varias estrategias:

### **One-to-Many para Clasificación de Números**

- Permite transformar **una entrada numérica en varias clases**.
- Se usa cuando un solo número puede representar **múltiples categorías** en el modelo.

### **Función de Activación: Softmax**

- En modelos de clasificación, **Softmax** se usa para convertir una serie de valores numéricos en **probabilidades normalizadas**.
- Asegura que la suma de las probabilidades sea **1**, facilitando la toma de decisiones en problemas de clasificación multiclase.

### **Función de Pérdida: Entropía Cruzada**

- La **entropía cruzada** se utiliza en clasificación multiclase para medir la diferencia entre la distribución de probabilidad real y la predicha por el modelo.
    
- Se define como:
    
 $$   
 H(p,q)=−∑p(x)log⁡q(x)H(p, q) = -\sum p(x) \log q(x)
$$

    donde:
    
    - **p(x)** es la distribución real de las clases.
    - **q(x)** es la distribución de probabilidades generada por el modelo.

**Ejemplo de Aplicación:**

- En **reconocimiento de matrículas**, en lugar de entrenar un modelo con redes neuronales profundas, se pueden aplicar **filtros adaptativos** que segmenten y extraigan los caracteres de la imagen.
- Esto puede ser más eficiente en términos computacionales sin comprometer la precisión del modelo.

---
