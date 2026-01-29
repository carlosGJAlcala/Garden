---
title: "Neuronas Artificiales"
date: 2025-02-26
tags:
  - deep-learning
  - redes-neuronales
---

## S7 Deep Learning


### Perceptrones y neuronas artificiales

Los perceptrones y las neuronas artificiales son la base del aprendizaje profundo. Estas unidades utilizan funciones de activación como ReLU (Rectified Linear Unit), softmax y sigmoide para transformar las entradas y producir una salida útil en los modelos de redes neuronales.

### Tipos de aprendizaje en redes neuronales

1. **Aprendizaje por transferencia**: Permite reutilizar modelos previamente entrenados en nuevas tareas, aprovechando el conocimiento adquirido en grandes conjuntos de datos.
2. **Aprendizaje supervisado**: Se entrena la red con datos etiquetados, ajustando sus pesos para minimizar el error en las predicciones.
3. **Aprendizaje no supervisado (Unsupervised learning)**: No se cuenta con etiquetas en los datos; en su lugar, se agrupan patrones similares mediante técnicas como clustering o autoencoders.
4. **Backpropagation**: Es el algoritmo central del entrenamiento de redes neuronales, permitiendo ajustar los pesos mediante la retropropagación del error en función de la derivada de la función de pérdida.

---

### Redes Neuronales Convolucionales (CNN)

Las redes neuronales convolucionales se utilizan principalmente en el procesamiento de imágenes. Su principio se basa en aplicar convoluciones a una imagen para extraer características esenciales, como bordes, texturas y formas.

El proceso de convolución consiste en utilizar filtros (kernels) que recorren la imagen y generan mapas de características, reduciendo la dimensionalidad y capturando información relevante. Se combinan con capas de pooling para reducir la cantidad de datos procesados sin perder información clave.

Las CNN han demostrado ser extremadamente efectivas en tareas de visión por computadora, como el reconocimiento facial, la detección de objetos y la segmentación de imágenes.

---

### Redes Neuronales Recurrentes (RNN)

Las redes neuronales recurrentes (RNN) están diseñadas para trabajar con datos secuenciales, como el procesamiento de lenguaje natural (NLP) y series temporales. Su principal ventaja es la capacidad de recordar información pasada a través de una memoria interna que se actualiza con cada nuevo dato.

Sin embargo, las RNN tradicionales tienen problemas con secuencias largas debido al desvanecimiento del gradiente. Por ello, en la actualidad se utilizan modelos más avanzados como LSTM y transformers.

Los transformers han reemplazado en gran medida a las RNN en tareas de NLP, ya que manejan mejor dependencias de largo plazo sin necesidad de procesar la información secuencialmente.

---

### LSTM (Long Short-Term Memory)

Las redes LSTM son un tipo de red neuronal recurrente que incorpora mecanismos específicos para mitigar el problema del desvanecimiento del gradiente. Su estructura incluye tres puertas principales:

1. **Puerta de entrada**: Controla qué información nueva se agrega a la memoria.
2. **Puerta de olvido**: Decide qué información se descarta de la memoria.
3. **Puerta de salida**: Determina qué información se utilizará en la salida de la red.

Gracias a estas puertas, las LSTM pueden retener información relevante durante períodos de tiempo más largos en comparación con las RNN estándar, lo que las hace útiles para tareas como traducción automática, modelado de lenguaje y análisis de sentimientos.

Aquí tienes el texto corregido y expandido:


## Transformers

Los **Transformers** son una arquitectura de redes neuronales que ha revolucionado el campo del procesamiento de lenguaje natural (NLP) y otras aplicaciones de aprendizaje profundo. Su principal innovación es el mecanismo de **multi-head attention**, que permite a la red enfocarse en diferentes partes de la secuencia de entrada simultáneamente.

### Características clave:

- **Mecanismo de atención**: Evalúa la importancia de cada palabra en relación con las demás dentro de la oración, sin necesidad de procesarlas de forma secuencial.
- **Embeddings**: Se utilizan para convertir palabras en vectores numéricos que capturan su significado semántico.
- **Estructura escalable**: Facilita el entrenamiento en grandes volúmenes de datos y permite generalizar mejor en diversas tareas.

Los Transformers han reemplazado a modelos más antiguos como las RNN y LSTM en muchas aplicaciones, y son la base de modelos avanzados como **GPT (Generative Pre-trained Transformer)** y **BERT (Bidirectional Encoder Representations from Transformers)**.

---

## Redes Generativas Antagónicas (GAN)

Las **GAN (Generative Adversarial Networks)** son redes neuronales utilizadas para generar datos sintéticos realistas a partir de ruido aleatorio. Funcionan mediante dos redes enfrentadas entre sí:

1. **Generador**: Crea imágenes o datos a partir de ruido aleatorio.
2. **Discriminador**: Intenta distinguir entre los datos generados y los reales.

El objetivo es que el generador aprenda a engañar al discriminador, produciendo datos cada vez más realistas.

### Aplicaciones de las GAN:

- **Generación de rostros**: Se pueden crear caras artificiales a partir de ruido, logrando imágenes indistinguibles de las reales.
- **Superresolución de imágenes**: Mejoran la calidad de imágenes de baja resolución.
- **Creación de datos sintéticos**: Útil cuando los datos reales son escasos o difíciles de obtener.
- **Transferencia de estilo**: Transformar imágenes en el estilo de una pintura o una estética particular.

---

## Tipos de Redes Neuronales y sus Aplicaciones

- **Redes convolucionales (CNN)**: Especializadas en procesamiento de imágenes, extracción de características y reconocimiento de patrones visuales.
- **Redes Feedforward**: Son redes de tipo supervisado utilizadas principalmente para clasificación de datos.
- **Redes Recurrentes (RNN)**: Se aplican en el análisis de texto y procesamiento de datos secuenciales.
- **LSTM (Long Short-Term Memory)**: Variante de RNN diseñada para retener información a largo plazo, utilizada en predicción de secuencias y procesamiento de lenguaje natural.
- **Autoencoders**: Se emplean para detección de anomalías y reducción de dimensionalidad en conjuntos de datos complejos.

Los **Transformers**, como ChatGPT, han superado a muchos de estos modelos en NLP, permitiendo generar texto con coherencia y contexto avanzado.


los epoch  son un pas throug que represeant una entramiento

# scaling law


### **El Triángulo de Constrain, Scaling y Choice**

En el desarrollo de modelos de inteligencia artificial y redes neuronales, existe un equilibrio entre tres factores clave: **constrain (restricciones), scaling (escalabilidad) y choice (elección de arquitectura y diseño del modelo)**.

- **Constrain**: Representa las limitaciones en los datos, la capacidad computacional o el entorno de implementación.
- **Scaling**: Se refiere a la capacidad de aumentar la escala del modelo, como incrementar el número de parámetros o mejorar la eficiencia computacional.
- **Choice**: Es la elección de arquitecturas, funciones de activación, algoritmos de optimización y otros aspectos que afectan el desempeño del modelo.

El equilibrio entre estos tres factores determina la viabilidad y eficiencia de un modelo de deep learning.

---

### **Evolución del Tamaño de las Redes Neuronales**

Las primeras redes neuronales tenían **apenas cientos de parámetros**, mientras que los modelos actuales pueden contener **billones de parámetros**.

- Por ejemplo, modelos como **GPT-4** cuentan con más de **1.7 billones de parámetros**, lo que les permite generar respuestas de manera altamente sofisticada.
- El aumento exponencial en el tamaño de las redes ha sido posible gracias a mejoras en hardware, algoritmos de entrenamiento y técnicas de optimización.

---

### **Métricas de Rendimiento en Deep Learning**

La performance de los modelos de redes neuronales se evalúa en **operaciones de coma flotante por segundo (FLOPS)**.

- Se utiliza **coma flotante** porque las **GPU (unidades de procesamiento gráfico)** están optimizadas para cálculos de alta precisión en este formato.
- En comparación, el **cerebro humano** tiene una capacidad de procesamiento estimada en **10¹⁵ operaciones por segundo**, lo que sigue siendo superior a los modelos actuales en muchas tareas cognitivas.

---

### **Métricas de Entrenamiento**

Para evaluar la calidad del entrenamiento de una red neuronal se utilizan varias métricas, entre ellas:

- **Training Loss**: Mide el error del modelo durante el entrenamiento.
- **Learning Rate**: Es un **hiperparámetro** que controla qué tan rápido se ajustan los pesos de los nodos de la red neuronal.
    - Si el learning rate es demasiado alto, el modelo puede no converger.
    - Si es demasiado bajo, el entrenamiento será lento y costoso computacionalmente.

Para evitar un entrenamiento excesivo y sobreajuste (**overfitting**), se emplea una técnica llamada **Early Stopping**, que detiene el entrenamiento cuando la métrica de validación deja de mejorar, evitando desperdiciar recursos.

---

### **Curvas de Aprendizaje (Learning Curves)**

Las **curvas de aprendizaje** representan la relación entre la **pérdida (loss)** y el **número de iteraciones o épocas** del entrenamiento.

- Una curva de aprendizaje bien ajustada muestra una disminución constante de la pérdida hasta alcanzar un punto óptimo.
- Si la curva no mejora, puede indicar problemas de sobreajuste o subajuste del modelo.

---

Una limitación a tener en cuenta es la limitacion de explainability 

no son modelos que razones 
un conche autono no razono solo detecta patrones  contxtual undestanding
intevide trainig compute
las redes neuronales sirven para completar tareas pero no razonan


para clasificar 
no puedes utilizar un modelo de una sola capa problema de xor  hay que utilizar la relu

los eppoch se utilizan para el tema del ajuste de los hiperparametros 

con dos capas eran necesarias para entrenar cualquier 

para coger la funcion de activación depende en parte de prueba de erro  pero ya hay estudios sobre eso no tenemos porque preocuparnos. es ajuste de hiperparametros expermintación  hay un articulo en la presentación
los transforme utilizan softmax
