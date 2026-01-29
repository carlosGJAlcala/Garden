---
title: "Natural Language Processing"
date: 2025-03-19
tags:
  - ciberseguridad
---

# Natural Language Processing (NLP)


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

El **80% de los datos** no son estructurados, lo que implica que se necesitan técnicas especializadas para poder extraer información útil de ellos. Esto incluye el análisis de texto, que puede estar en formatos como artículos, correos electrónicos o publicaciones en redes sociales.

Aunque en la web no está tan representado el **indio** o el **chino**, estos idiomas representan aproximadamente el **50% de los hablantes del mundo**. Por lo tanto, las técnicas de procesamiento de lenguaje natural (NLP) deben ser capaces de manejar una gran diversidad lingüística.

En resumen, el NLP está estrechamente vinculado con el **lenguaje humano**, y su propósito es permitir que las máquinas comprendan, interpreten y generen lenguaje de una forma útil.

### Aplicaciones del NLP:

- **Análisis de sentimientos**: Determinar las emociones o actitudes expresadas en un texto, como si un comentario es positivo, negativo o neutral.
- **Búsqueda y análisis de documentos**: Extraer información relevante de grandes volúmenes de texto, por ejemplo, para análisis de contratos o la generación de documentos legales.
- **Generación automática de textos**: Como en los chatbots, que generan respuestas basadas en el texto proporcionado.

En el contexto de NLP, es crucial manejar **ambigüedades** de diversos tipos:

- **Sintácticas**: Diferentes interpretaciones de una misma estructura gramatical.
- **Referenciales**: Dificultad para identificar a qué hace referencia un pronombre o término.
- **Elípticas**: Omissión de partes del enunciado que deben ser inferidas.
- **Sarcasmo**: Un reto, ya que las máquinas pueden tener dificultades para identificar el tono irónico o contrario al significado literal de las palabras.

El **Out-Of-Vocabulary (OOV)** o palabras fuera del vocabulario es otro desafío importante en NLP, que se presenta cuando una palabra que no está en el modelo se encuentra durante el procesamiento (como "selfie" o "cryptomoneda").

Además, algunos idiomas, como el **persa**, no tienen género gramatical, lo que presenta un reto adicional al procesar su lenguaje.

---

# Niveles del lenguaje

El procesamiento de lenguaje natural involucra varios niveles de análisis:

1. **Fonemas**: Son las unidades más pequeñas de sonido en el lenguaje.
2. **Morfemas**: Son las unidades mínimas de significado que no se pueden dividir más.
3. **Lexemas**: Raíz de las palabras, a partir de la cual se pueden formar otras.
4. **Sintaxis**: Estructura y reglas que rigen cómo se organizan las palabras para formar oraciones, como el orden de sujeto, verbo y objeto.
5. **Semántica**: Significado de las palabras y las oraciones.

---

# NLP en la voz y el texto

El procesamiento de lenguaje natural no solo se aplica a texto escrito, sino también a **voz** y **discurso**. Por ejemplo:

- **Traducción de películas**: Los subtítulos automáticos pueden ser generados mediante técnicas de NLP, lo que permite traducir diálogos en tiempo real.


---

# Técnicas de Procesamiento de Texto

Aquí se describe cómo preparar el texto para su análisis dentro de un **pipeline de NLP**. El proceso completo generalmente sigue estos pasos:

1. **Adquisición y Exploración de Datos**: Recolección de los datos y análisis preliminar para entender el contenido.
2. **Procesamiento de Texto**: Limpieza, normalización y transformación de los datos textuales.
3. **Representación de Texto**: Conversión de texto a un formato adecuado para que el modelo pueda procesarlo (como vectores o embeddings).
4. **Selección y Entrenamiento del Modelo**: Elegir el modelo adecuado y entrenarlo con los datos.
5. **Evaluación del Modelo**: Medir el rendimiento del modelo con métricas específicas.
6. **Despliegue e Integración**: Implementar el modelo en un entorno de producción.
7. **Monitoreo y Mantenimiento**: Asegurar que el modelo continúe funcionando correctamente a lo largo del tiempo.

Una frase muy utilizada en el entrenamiento de modelos de NLP es:  
**"The quick brown fox jumps over the lazy dog"**. Esta frase es útil porque contiene todas las letras del alfabeto, lo que permite verificar el rendimiento del modelo con una variedad completa de caracteres.

# **TEXT PREPOCESSING**
### Stopwords and Text Cleaning

Las **stopwords** son palabras de alta frecuencia que se eliminan durante el procesamiento porque no aportan mucho significado, como artículos o preposiciones (por ejemplo, "the", "in", "and"). Sin embargo, en algunos contextos, las stopwords pueden ser relevantes y no deben eliminarse, por ejemplo, en análisis de sentimientos donde las palabras de enlace pueden tener importancia.

También se suelen eliminar **símbolos de puntuación**, ya que a menudo no agregan información útil para el análisis. Sin embargo, los **emojis** pueden ser interesantes, especialmente en el análisis de sentimientos, ya que pueden transmitir emociones.

Si necesitas generar un texto formal, lo ideal es eliminar los emojis, pero en otros contextos, como el análisis de sentimientos o comunicaciones informales, los emojis podrían ser valiosos.

### Stemming y Lemmatization (Normalización)

El **stemming** y la **lemmatization** son técnicas para reducir el vocabulario, es decir, para agrupar las diferentes formas de una palabra y tratar de obtener su raíz o lema. Esto ayuda a reducir la variabilidad del texto sin perder el significado subyacente.

- **Stemming**: Esta técnica recorta las palabras hasta su raíz, pero no siempre produce una forma lingüísticamente correcta. Por ejemplo:
    
    - "Adjustable" se reduce a "adjust".
    
    El objetivo aquí es eliminar los sufijos y obtener una forma no lingüística que represente el concepto principal.
    
- **Lemmatization**: A diferencia del stemming, la lemmatización convierte una palabra a su forma base o lematizada, de manera que se mantiene su significado. Por ejemplo:
    
    - "Was" se convierte en "be".

En algunos idiomas, como el inglés, también se deben armonizar variaciones regionales, como el uso de **"-zation"** en inglés americano versus **"-sation"** en inglés británico.

Esto es útil para **normalizar** el lenguaje y garantizar que diferentes formas de una palabra se traten de manera coherente.

### Tokenización

La **tokenización** es el proceso de dividir el texto en unidades más pequeñas (tokens). Un token no siempre es una palabra; puede ser una palabra, un símbolo de puntuación o incluso una secuencia de caracteres. La tokenización permite obtener una estructura más pequeña que puede ser utilizada para entrenar el modelo.

Es importante recordar que en algunos modelos de lenguaje, como **GPT**, se paga por token, lo que significa que cada unidad de texto procesada se cuenta como un token. Esto hace que la tokenización eficiente sea un aspecto importante del procesamiento de texto.

Ejemplo: Si tomamos la frase **"The quick brown fox jumps over the lazy dog"** y la tokenizamos, obtenemos los tokens:

- ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"]

Sin embargo, los signos de puntuación también se pueden considerar tokens, dependiendo de cómo se configuren los modelos y el proceso de tokenización.


---

## **Procesamiento Sintáctico y Semántico**

El procesamiento de texto en el ámbito semántico y sintáctico se refiere a las técnicas que permiten comprender y analizar el significado de los textos, así como su estructura.

**Part of Speech(POS tagging)**
A cada palabra dentro de una frase se le da una categoría tan como nombre, verbo, adjetivo, adverbio, etc.
Sirve para ayudar algoritmo para que pueda diferenciar varias palabras dependiendo de su rol en la frase.
Es muy utlin en sintacti parsing sentiment analysis and machine translation.

**Reconocimiento de Entidades Nombradas (NER, por sus siglas en inglés)**

El Reconocimiento de Entidades Nombradas (Named Entity Recognition, NER) es una técnica utilizada para extraer información clave de un texto, asignando etiquetas específicas a ciertos elementos de dicho texto. Esta herramienta permite identificar y clasificar elementos como personas, lugares, fechas, organizaciones y otros tipos de entidades.

Por ejemplo, si se tiene la frase:

_“Barack Obama visitó Londres”_

El sistema NER identificaría las siguientes entidades:

- **Barack Obama**: Etiquetado como **Persona** (Person)
- **Londres**: Etiquetado como **Ubicación** (Location)

Este proceso es fundamental en áreas como la extracción de información, el análisis de sentimientos y la creación de sistemas de búsqueda más precisos.

Además del reconocimiento de entidades nombradas, el procesamiento semántico también se involucra en la interpretación y diseminación del significado de las palabras y frases dentro de un contexto más amplio.


---

# **Representación de texto**

Los textos deben ser representados de manera numérica para que las máquinas puedan procesarlos. Para convertir un texto en formato numérico, existen diversas técnicas que permiten transformarlo en vectores de características.

1. **Vectorización de texto con Word Embeddings (por ejemplo, King + Woman = Queen)**  
    Una técnica es la de _word embeddings_, que asigna un valor numérico (vector) a cada palabra en función de su contexto. Por ejemplo, en un modelo de word embeddings, las palabras "King" + "Woman" podrían resultar en el vector de la palabra "Queen". Este enfoque es útil para representar relaciones semánticas entre las palabras. Sin embargo, los embeddings no son la única opción.
    
2. **One-Hot Encoding**  
    Esta técnica convierte cada palabra en un vector binario, en el cual solo un valor es 1, indicando la presencia de una palabra en el vocabulario, y todos los demás son 0. Aunque es un enfoque sencillo, no es el más adecuado para textos con grandes volúmenes de datos, ya que genera vectores muy dispersos y de alta dimensión.
    
3. **Count Vectorization (Vectorización por Frecuencia)**  
    La _count vectorization_ es una técnica similar al _one-hot encoding_, pero en lugar de usar valores binarios, cuenta cuántas veces aparece cada palabra en el texto. Aunque esta técnica tiene la ventaja de capturar la frecuencia de las palabras, no tiene en cuenta el contexto ni el orden de las palabras, lo que limita su efectividad en textos complejos.
    
4. **Bag of Words (BoW)**  
    El modelo _Bag of Words_ genera vectores que representan la ocurrencia de palabras en un documento, ignorando el orden y la gramática. Es una técnica muy útil para tareas de clasificación de texto, clustering y análisis de sentimientos. Sin embargo, presenta algunas limitaciones: no captura la sintaxis ni la estructura gramatical del lenguaje y, debido a la gran cantidad de características, puede generar vectores de alta dimensión, lo que hace que el procesamiento sea más complejo. Además, no refleja la importancia relativa de las palabras en un contexto.
    
5. **TF-IDF (Term Frequency - Inverse Document Frequency)**  
    Una técnica más avanzada es el _TF-IDF_, que combina dos factores: la frecuencia de un término en un documento (Term Frequency, TF) y la frecuencia inversa de dicho término en todo el corpus de documentos (Inverse Document Frequency, IDF). Este enfoque penaliza las palabras que aparecen con mucha frecuencia en todo el conjunto de datos (como "y", "de", "la", etc.), lo que ayuda a darle más peso a términos que son específicos para un documento en particular. El TF-IDF fue una de las primeras técnicas utilizadas en motores de búsqueda para mejorar la relevancia de los resultados.
    



---

**Word Embedding**

Representar texto en forma de vectores se llama **embedding**. Los **embeddings** son representaciones numéricas de palabras o frases en un espacio vectorial continuo y denso. Estos vectores son llamados **vectores densos** porque contienen valores numéricos que no son fácilmente interpretables por un ser humano, pero son útiles para que las máquinas puedan procesar y entender las relaciones semánticas entre las palabras.

1. **¿Qué es un Word Embedding?**  
    Los **word embeddings** son representaciones matemáticas de palabras en un espacio de alta dimensión. A diferencia de enfoques como el _one-hot encoding_, que representa cada palabra como un vector disperso (con muchos ceros), los **word embeddings** asignan a cada palabra un vector denso que captura su contexto y relaciones con otras palabras. Esto permite que el modelo entienda el significado de una palabra en relación con otras, considerando sinónimos, antonimos, y otras relaciones semánticas.
    
2. **Word2Vec y su Principio**  
    Uno de los métodos más populares para generar **word embeddings** es **Word2Vec**, desarrollado por Google. Word2Vec convierte palabras en vectores de tal forma que las palabras con significados similares tienen representaciones vectoriales cercanas entre sí en el espacio vectorial.
    
    - **Técnica CBOW (Continuous Bag of Words)**: En este enfoque, se predice una palabra central (objetivo) a partir de su contexto (las palabras que la rodean). Por ejemplo, si tenemos la frase "el perro corre rápido", el modelo intentaría predecir la palabra "perro" basándose en las palabras a su alrededor como "el", "corre", y "rápido".
        
    - **Técnica Skip-gram**: En este enfoque, el modelo predice el contexto de una palabra dada. Es decir, si se tiene una palabra central, el modelo trata de predecir las palabras que están cerca de ella. Por ejemplo, si la palabra central es "perro", el modelo predice palabras como "el", "corre", "rápido".
        
    
    **Word2Vec** se considera un avance significativo en el campo del aprendizaje profundo (Deep Learning), ya que permite capturar relaciones semánticas entre palabras de manera eficiente.
    
3. **Ventajas de los Word Embeddings**
    
    - **Captura de semántica y contexto**: A diferencia de las técnicas anteriores como _one-hot encoding_, los **word embeddings** permiten que se capture la semántica de las palabras y su contexto dentro de un espacio vectorial. Las palabras con significados similares estarán representadas por vectores cercanos, lo que permite que los modelos comprendan sinónimos, analogías y otras relaciones semánticas.
        
    - **Consideración del orden**: Una de las grandes ventajas de los **word embeddings** sobre técnicas más simples es que preservan el orden de las palabras, lo cual es crucial en muchos contextos lingüísticos. El modelo tiene en cuenta no solo las palabras individuales, sino también cómo se relacionan entre sí dentro de un determinado contexto.
        
4. **Deep Learning y Word Embeddings**  
    El desarrollo de técnicas como los **word embeddings** marcó el principio del uso de **Deep Learning** (aprendizaje profundo) para tareas de procesamiento de lenguaje natural (PLN). A través de redes neuronales profundas, los modelos pueden aprender representaciones cada vez más complejas y precisas del lenguaje. Los **word embeddings** son ahora la base para muchos modelos modernos, como **BERT**, **GPT** y otros.
    
5. **Similitudes Semánticas y Aplicaciones**  
    Los **word embeddings** son fundamentales para calcular similitudes semánticas entre palabras, lo que permite aplicaciones como:
    
    - **Búsqueda de información**: Encontrar sinónimos o términos relacionados para mejorar la búsqueda.
    - **Traducción automática**: Facilitar la traducción al identificar equivalencias semánticas entre palabras en diferentes idiomas.
    - **Clasificación de texto**: Ayudar en la clasificación de documentos al entender el significado detrás de las palabras.

---



---

# **Técnicas tradicionales en NLP (Natural Language Processing)**

El **Procesamiento de Lenguaje Natural (NLP)** ha avanzado considerablemente en los últimos años gracias a enfoques de **aprendizaje profundo (Deep Learning)**, pero aún se utilizan muchas técnicas tradicionales en NLP que son efectivas, especialmente cuando los recursos computacionales son limitados o cuando se necesita una solución más interpretable. Estas técnicas incluyen métodos clásicos de **aprendizaje automático** y de **vectorización de características**.

### 1. **Modelos de Aprendizaje Automático Tradicionales en NLP**

**Naive Bayes** es uno de los algoritmos más populares en las primeras etapas del procesamiento de lenguaje natural. Aunque este enfoque es simple, sigue siendo efectivo para tareas como clasificación de texto y análisis de sentimientos. El principio detrás de Naive Bayes es asumir que las características (en este caso, las palabras) son independientes entre sí, lo que simplifica mucho el modelo y hace que sea computacionalmente eficiente. Es especialmente útil cuando se tiene un conjunto de datos grande, pero no se espera que las relaciones entre las palabras sean demasiado complejas.

### 2. **Vectorización de Características para NLP**

Una parte clave del procesamiento de texto en NLP es convertir el texto no estructurado en un formato que pueda ser interpretado por modelos de aprendizaje automático. Existen varias técnicas de **vectorización de características**:

- **TF (Term Frequency)**: Esta técnica cuenta cuántas veces aparece un término en un documento. Cuanto mayor sea el número de apariciones de una palabra en el texto, mayor será su frecuencia. Sin embargo, no tiene en cuenta la importancia de la palabra en relación con todo el corpus.
    
- **TF-IDF (Term Frequency-Inverse Document Frequency)**: Esta técnica mejora el **TF** al penalizar las palabras que son demasiado frecuentes en todo el corpus (como palabras comunes como "el", "de", etc.). El **TF-IDF** da más peso a las palabras que son específicas para un documento determinado, lo que mejora la relevancia en tareas como la clasificación de texto y la búsqueda de información.
    

Estas técnicas de **vectorización** son esenciales para convertir el texto en un formato adecuado para que los modelos de aprendizaje automático puedan realizar tareas como clasificación, análisis de sentimientos o extracción de información.

### 3. **Clasificación de Sentimientos: Ekman y Friesen**

En 1972, los psicólogos **Paul Ekman** y **Wallace V. Friesen** propusieron una clasificación de las emociones humanas basada en expresiones faciales universales. Aunque su trabajo se centró más en las emociones faciales, su clasificación ha sido muy influyente en el análisis de sentimientos. En NLP, la clasificación de sentimientos busca identificar el sentimiento detrás de un texto, ya sea positivo, negativo o neutral. Esta clasificación es fundamental en tareas como la evaluación de opiniones de productos, comentarios en redes sociales, y análisis de opiniones de clientes.

### 4. **Selección de Características (Feature Selection) en NLP**

En los enfoques tradicionales de **NLP**, se utilizan técnicas de **selección de características** para elegir las características más relevantes (palabras o n-grams) para el modelo. El objetivo es reducir la dimensionalidad del conjunto de datos y mejorar la precisión del modelo. Las técnicas de selección de características pueden basarse en la frecuencia de las palabras, el **TF-IDF**, o en la información mutua, entre otras métricas.

### 5. **Modelo Clásico de Aprendizaje Automático en NLP**

Después de realizar la vectorización de las características y la selección de las características relevantes, se utilizan **modelos clásicos de aprendizaje automático** como:

- **Máquinas de soporte vectorial (SVM)**: Son muy eficaces para tareas de clasificación, como la clasificación de sentimientos, donde se busca separar los textos en categorías como "positivo" o "negativo".
- **Regresión logística**: También utilizada para tareas de clasificación, especialmente en tareas binarias como la clasificación de sentimientos (positivo/negativo).
- **Árboles de decisión** y **Random Forests**: Se usan para clasificar texto basándose en las características extraídas, y pueden ser especialmente útiles para tareas con estructuras jerárquicas de texto.


---



### **Keyword Co-occurrence Graph-Based Topic Modeling**

En **modelado de temas basado en gráficos de co-ocurrencia de palabras clave**, no es necesario recurrir a técnicas avanzadas de inteligencia artificial. Este enfoque utiliza una **red** en la que cada nodo representa uno de los términos (palabras clave) de un corpus de texto. Se establece un **parámetro de distancia** entre los nodos según la frecuencia o la proximidad con la que aparecen las palabras juntas en los documentos. Esta distancia se puede definir en función de su co-ocurrencia en el mismo párrafo, documento o contexto.

Este método es útil para identificar **temas** o **conceptos clave** en un conjunto de datos, y es una de las formas clásicas de realizar **modelado de temas**. Los **gráficos de co-ocurrencia** pueden revelar patrones sobre qué términos se suelen usar juntos, lo que facilita la agrupación de términos relacionados en temas comunes.

---

### **Limitaciones de los Métodos Clásicos de Modelado de Temas**

Aunque los enfoques basados en gráficos de co-ocurrencia pueden ser efectivos para tareas básicas de modelado de temas, tienen varias limitaciones:

1. **Dificultad para Capturar el Contexto**:  
    Los gráficos de co-ocurrencia no tienen en cuenta el contexto semántico de las palabras. Aunque una palabra pueda co-ocurrir frecuentemente con otras, no siempre significa que estén relacionadas en un sentido semántico. No se captura la complejidad del lenguaje ni las relaciones más profundas entre los términos.
    
2. **Problemas de **Sparsity**:  
    Los modelos de co-ocurrencia tienden a ser dispersos. Esto significa que muchas combinaciones de términos no ocurren con frecuencia en el corpus, lo que lleva a matrices de co-ocurrencia muy grandes y con muchos ceros. Esta dispersión hace que los modelos sean difíciles de procesar y más lentos.
    
3. **Sesgos**:  
    Los gráficos de co-ocurrencia pueden tener sesgos hacia términos comunes o aquellos que ocurren frecuentemente en contextos generales. Esto puede dificultar la identificación de términos menos comunes pero importantes para el tema de interés.
    

---




### **Modelado de Temas**

El **modelado de temas** es una técnica de **aprendizaje no supervisado** utilizada en el **procesamiento de lenguaje natural (NLP)** para identificar y agrupar temas dentro de un conjunto de documentos. Esta técnica permite descubrir automáticamente los temas subyacentes en grandes colecciones de texto, sin necesidad de tener etiquetas o categorías previamente definidas.

#### **¿Qué es un Tema?**

En el contexto del modelado de temas, un **tema** se define como un conjunto de términos (palabras) que aparecen con frecuencia en un conjunto de documentos y que, por lo tanto, pueden representar un concepto o categoría subyacente en esos documentos. Por ejemplo, en un conjunto de artículos relacionados con **informática**, los términos como "virus", "denegación de servicio" (DoS), "seguridad", "informática", etc., podrían ser identificados como un tema relacionado con **seguridad informática**.

Otro ejemplo podría ser el tema **económico**, en el cual términos como "dinero", "finanzas", "mercado", "economía", etc., suelen estar presentes.

El objetivo del modelado de temas es identificar estos patrones de términos que aparecen con frecuencia en documentos y asociarlos con un tema que resume el contenido general.

---

### **Técnicas Comunes para el Modelado de Temas**

Existen varias técnicas estadísticas y matemáticas que se utilizan para el modelado de temas en NLP. Las más comunes son:

1. **LDA (Latent Dirichlet Allocation)**  
    **LDA** es uno de los métodos más populares para el modelado de temas. Es un **modelo generativo probabilístico** que asume que cada documento en un corpus es una mezcla de varios temas y que cada palabra en el documento proviene de uno de esos temas. LDA asigna a cada palabra en un documento una probabilidad de pertenecer a un tema específico. La **idea central** de LDA es descubrir, a partir de los datos observados (documentos y palabras), qué temas subyacen en el conjunto de documentos. Esta técnica es ampliamente utilizada para tareas de **descubrimiento de temas** en grandes colecciones de texto.
    
2. **NMF (Non-Negative Matrix Factorization)**  
    La **factorización de matrices no negativa (NMF)** es otra técnica popular para el modelado de temas. A diferencia de LDA, NMF descompone la **matriz de términos por documentos** en dos matrices más pequeñas que contienen los **temas** y las **palabras** asociadas con esos temas. La ventaja de NMF es que obliga a que los valores en las matrices resultantes sean **no negativos**, lo que facilita la interpretación de los temas, ya que se evita la presencia de valores negativos en las representaciones de los temas. Es útil para la reducción de dimensionalidad y el análisis de la estructura latente en los datos.
    
3. **Factorización Matricial No Negativa (NMF)**  
    Aunque mencionada anteriormente, la **factorización matricial no negativa** merece una mención separada. En el caso de NMF, la idea es representar un conjunto de documentos y sus términos en forma de una matriz de **términos por documentos**. NMF intenta factorizar esta matriz en dos componentes: una matriz de **temas** y una matriz de **documentos por tema**. Esta técnica ayuda a extraer patrones de temas de los datos, similar a LDA, pero de manera diferente, utilizando álgebra lineal.
    

---

### **Limitaciones del Modelado de Temas**

Aunque las técnicas de modelado de temas son muy poderosas, tienen algunas limitaciones:

1. **Dificultad en la Interpretación**:  
    A pesar de que los temas identificados pueden tener una alta coherencia estadística, a veces es difícil interpretar el significado exacto de un tema. Esto es especialmente cierto si los términos identificados como parte de un tema son ambiguos o tienen múltiples significados.
    
2. **Dependencia de la Calidad de los Datos**:  
    La efectividad de los modelos de temas depende en gran medida de la calidad del conjunto de datos. Si los datos están mal etiquetados o contienen ruido (información irrelevante), los temas generados pueden ser poco coherentes o inexactos.
    
3. **Limitación en la Captura de Contexto**:  
    Los enfoques como LDA y NMF no capturan el contexto completo de las palabras. Por ejemplo, el significado de una palabra puede depender del contexto en el que se use (por ejemplo, "banco" en el contexto de un **río** frente a "banco" en el contexto de **finanzas**). Técnicas más avanzadas, como los **word embeddings** y los modelos basados en **transformers**, pueden capturar mejor este tipo de contexto.
    

---



---

Si te gustaría saber más detalles sobre alguna de las técnicas o conceptos mencionados, ¡avísame!
### **NLP Frameworks en Python**

En el ámbito de NLP en Python, existen varias librerías y frameworks populares para el procesamiento de texto y el desarrollo de modelos de lenguaje:

1. **NLTK (Natural Language Toolkit)**:  
    Es una de las librerías más antiguas y ampliamente utilizadas para trabajar con texto en Python. Ofrece herramientas para **tokenización**, **etiquetado gramatical**, **análisis de sentimientos**, **stemización**, y más. Es excelente para tareas básicas de procesamiento de texto y educación.
    
2. **SpaCy**:  
    SpaCy es más eficiente y rápido que NLTK para tareas más complejas de NLP. Está diseñado para producción y se utiliza en aplicaciones de gran escala, incluyendo **análisis sintáctico**, **entidad nombrada (NER)**, y **análisis de dependencias**. SpaCy es más adecuado para trabajos de **procesamiento en tiempo real** y análisis de texto a gran escala.
    
3. **TensorFlow** y **PyTorch**:  
    Estas dos librerías son fundamentales en el mundo del **Deep Learning** y también se utilizan ampliamente en NLP. Son más potentes para crear modelos **de aprendizaje profundo** y permiten trabajar con grandes volúmenes de datos y realizar tareas complejas, como **traducción automática** o **generación de texto**.
    
4. **Hugging Face Transformers**:  
    Esta librería ha ganado popularidad rápidamente gracias a su implementación de modelos preentrenados de **transformers** como **BERT**, **GPT-2**, y **T5**, que son los modelos de lenguaje de última generación. Hugging Face hace que trabajar con **modelos de NLP avanzados** sea mucho más accesible, incluso para quienes no tienen experiencia previa en redes neuronales profundas.
    

---

### **El Impacto de la Inteligencia Artificial Generativa y los Modelos LLM**

Con el auge de los **Modelos de Lenguaje Grande (LLM)** y las **técnicas de inteligencia artificial generativa**, como los modelos basados en **GPT-3** o **GPT-4**, las técnicas tradicionales de **modelado de temas** han quedado en gran medida obsoletas. Los **LLM** no solo son capaces de generar texto coherente, sino también de comprender el contexto semántico de las palabras, lo que les permite realizar tareas mucho más complejas, como **respuestas a preguntas**, **generación de texto** y **traducción automática**.

Estos avances han llevado a que el modelado de temas clásico, como los gráficos de co-ocurrencia y la **vectorización de características** (por ejemplo, **TF-IDF**), ya no sean necesarios en muchas aplicaciones modernas de NLP. Los **LLM** pueden generar y comprender temas sin necesidad de pasos intermedios, lo que ha revolucionado la forma en que procesamos el lenguaje.

---

### **Deep Learning en NLP**

El **Deep Learning** ha revolucionado el procesamiento de lenguaje natural en los últimos años, gracias a su capacidad para capturar patrones complejos en datos grandes y no estructurados. Entre las técnicas más relevantes se encuentran:

1. **MLP (Multi-Layer Perceptrons)**:  
    Es una red neuronal de alimentación directa que se utiliza para tareas simples de clasificación o regresión en texto. Aunque menos común en NLP hoy en día, sigue siendo útil para tareas de clasificación de texto pequeñas.
    
2. **RNNs (Redes Neuronales Recurrentes)**:  
    Las **RNNs** son una clase de redes neuronales que son excelentes para procesar secuencias, como **texto**. Son capaces de tomar en cuenta el orden temporal de las palabras en una secuencia, lo que las hace útiles para tareas como la **traducción automática** o la **generación de texto**.
    
3. **LSTM (Long Short-Term Memory)**:  
    Las **LSTM** son una mejora de las **RNNs** que resuelven el problema del **desvanecimiento del gradiente** en secuencias largas. Estas redes son excelentes para tareas que requieren modelar dependencias a largo plazo en texto, como **análisis de sentimientos**, **resumen de texto**, y **traducción**.
    

---


### **BERT (Bidirectional Encoder Representations from Transformers)**

**BERT** es un modelo de **lenguaje preentrenado** basado en la arquitectura de **Transformers**, desarrollado por Google. Se ha convertido en uno de los modelos más populares y efectivos en el campo del **Procesamiento de Lenguaje Natural (NLP)** debido a su capacidad para entender el contexto completo de las palabras dentro de una oración, lo que lo hace particularmente útil para tareas que requieren una comprensión profunda del texto. Es un **embedding contextual**

#### **¿Qué hace BERT?**

BERT  es excelente para **predecir términos faltantes** en una oración, lo que significa que puede predecir cuál es la siguiente palabra o las palabras faltantes en un contexto dado. Esto lo convierte en un modelo muy útil para una amplia gama de tareas de **comprensión de texto**, incluyendo:

1. **Predicción de la siguiente palabra**:  
    BERT puede predecir una palabra faltante en una oración a partir de su contexto. Por ejemplo, dado un fragmento como "El gato está en el ___", BERT puede predecir que la palabra faltante es "techo" o "sofá", dependiendo del contexto del texto.
    
2. **Generación de respuestas a preguntas**:  
    BERT es ampliamente utilizado en tareas de **respuestas a preguntas**. Al haber sido entrenado con grandes cantidades de texto, puede comprender el significado detrás de una pregunta y generar una respuesta relevante basada en el contexto proporcionado. Por ejemplo, dado un pasaje de texto y una pregunta relacionada, BERT puede identificar la parte del pasaje que contiene la respuesta correcta.
    

#### **Características Clave de BERT:**

1. **Entrenamiento bidireccional**:  
    A diferencia de otros modelos de lenguaje tradicionales que leen el texto de forma unidireccional (de izquierda a derecha o de derecha a izquierda), BERT utiliza un enfoque **bidireccional**. Esto significa que BERT tiene en cuenta tanto el contexto anterior como el posterior a una palabra para generar una representación más completa de su significado. Este enfoque bidireccional es crucial para entender el contexto completo y ambigüedad de las palabras.
    
2. **Preentrenamiento y ajuste fino (fine-tuning)**:  
    BERT es un modelo preentrenado, lo que significa que se entrena inicialmente en grandes cantidades de texto para aprender representaciones generales del lenguaje. Luego, puede ser ajustado (fine-tuned) para tareas específicas, como análisis de sentimientos, clasificación de texto, o respuestas a preguntas, proporcionando resultados muy precisos sin necesidad de grandes cantidades de datos etiquetados para cada tarea.
    
3. **Transformers**:  
    La arquitectura de **transformers** es fundamental para el funcionamiento de BERT. Los transformers permiten que BERT capture las dependencias entre las palabras en un texto, independientemente de la distancia entre ellas, lo que mejora enormemente su capacidad para comprender contextos complejos.
    

#### **Aplicaciones de BERT**

BERT es especialmente útil en diversas aplicaciones de **NLP**, tales como:

- **Análisis de sentimientos**: Comprender el tono o sentimiento detrás de un texto (positivo, negativo o neutral).
- **Clasificación de texto**: Asignar categorías a textos, como clasificación de correos electrónicos, clasificación de noticias, etc.
- **Respuestas a preguntas**: Dada una pregunta y un pasaje de texto, generar la respuesta correcta basada en la información contenida en el pasaje.
- **Reconocimiento de entidades nombradas (NER)**: Identificar entidades clave como personas, lugares, organizaciones, etc., dentro de un texto.

#### **Ventajas de BERT:**

- **Entendimiento profundo del contexto**: Gracias a su entrenamiento bidireccional y a su arquitectura basada en transformers, BERT entiende de manera más precisa el contexto de las palabras dentro de una oración.
- **Rendimiento de vanguardia**: BERT ha alcanzado resultados de vanguardia en varias tareas de **NLP**, estableciendo nuevos estándares en tareas como la clasificación de texto, la respuesta a preguntas y el análisis de sentimientos.

#### **Limitaciones de BERT:**

- **Requiere muchos recursos computacionales**: Debido a su tamaño y la cantidad de datos con los que es entrenado, BERT requiere una gran cantidad de poder de cómputo, lo que puede hacer que su entrenamiento y ejecución sean costosos.
- **No es perfecto para todos los casos**: Aunque BERT es muy efectivo en muchas tareas, hay ciertos contextos o tareas más complejas en los que su rendimiento puede verse limitado o donde pueden surgir problemas relacionados con el **contexto ambiguo** o **contextos a largo plazo**.

### **Similitud del Coseno y F1 Score en LLMs**

**Similitud del Coseno**:  
La similitud del coseno mide la **similitud** entre dos vectores en un espacio vectorial. Se usa para comparar textos y evaluar qué tan similares son en cuanto a contenido, sin importar su longitud. Es útil en **LLMs** para medir la relación entre respuestas generadas y respuestas esperadas.

**F1 Score**:  
El **F1 score** es la media armónica entre **precisión** y **recall**. Se utiliza para evaluar modelos de **clasificación de texto**, como en **análisis de sentimientos** o **clasificación de documentos**, buscando un balance entre ambos aspectos, especialmente cuando las clases están desbalanceadas.
# KnIme


---

**Ejemplo 1:**

1. Obtenemos los documentos.
2. Realizamos un preprocesamiento (sacar los términos más relevantes).
3. Hacemos una vectorización del documento (usando One-Hot Encoding para crear un vector por cada documento).
4. Convertimos las categorías en clases.
5. El **Color Manager** es para saber qué color corresponde a cada etiqueta.
6. Entrenamos dos modelos: **Decision Tree Learning** y **XGBoost** (un modelo de ensamble).

---

**Ejemplo 2:**

7. Deben trabajar con documentos.
8. En el preprocesamiento, tenemos que armonizar el texto (por ejemplo, poner todo en minúsculas).
9. El siguiente paso es eliminar las **stop words**.
10. Realizamos **stemming**, aunque es mejor usar **lemmatización**, pero tiene un coste mayor.
11. Con **Document Viewer**, se pueden ver los pasos a medida que se aplican.
12. **Term Filtering** elimina los términos más frecuentes y clasifica cada uno.
13. Lo analizamos con **SVM** (es un buen modelo, ya que no se necesita conocer el nivel de la infraestructura; siempre es importante tenerlo en cuenta, ya que este pensamiento crítico se valora en los exámenes).

---
Ejemplo 3:
es un ejemplo extraer entidades se puede utilizar para paginas web
De etiquetado POS taggin and named entity recognition 
1. Utilizamos un tokenizar de ignles usando POS tagger 
2. Abner Tagger cada token lo identifica en que contexto ser refiere en un contexto biomedico  si es un tipo de célula 
3. tag filter 
4. crea bag of word que es el conjunto de nuestro vocabulario
5. luego hace un tf para filtrar con la frecuencia
En el siguiente día utilizamos la ia generativa