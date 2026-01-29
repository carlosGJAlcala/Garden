---
title: "Extraccion De Iocs Utilizando Llm En Ciberseguridad"
date: 2025-04-01
tags:
  - ciberseguridad
---

## **Juan García López** - _Extracción de IoCs utilizando LLM en Ciberseguridad_


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Maltego|Maltego]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

En el campo de la **ciberseguridad**, el uso de **Modelos de Lenguaje de Gran Escala (LLMs)** está tomando un papel cada vez más relevante para la extracción de **Indicadores de Compromiso (IoCs)**. Estos modelos pueden facilitar la identificación de patrones maliciosos en grandes volúmenes de datos de forma eficiente.

---

## **IA en Ciberseguridad**

La **Inteligencia Artificial (IA)** se está utilizando cada vez más en el ámbito de la ciberseguridad para mejorar la detección de amenazas, la automatización de procesos y la mejora de la precisión de las herramientas de seguridad. Hay **dos técnicas principales** que se aplican en este campo:

1. **Machine Learning (ML)**:  
    Utiliza algoritmos para aprender patrones a partir de los datos. Estos algoritmos pueden clasificar y predecir comportamientos maliciosos al aprender de datos previos.
    
2. **Deep Learning (DL)**:  
    Utiliza redes neuronales profundas para modelar y reconocer patrones más complejos en los datos. Es especialmente eficaz en tareas como la detección de anomalías o el análisis de grandes volúmenes de datos, como el tráfico de red.
    

---

## **Algunos de los algoritmos utilizados en Ciberseguridad**

1. **Árboles de decisión**:  
    Un algoritmo simple y explicativo que divide el conjunto de datos en función de condiciones lógicas. Se utiliza para clasificación y regresión, y es útil en sistemas de detección de intrusiones.
    
2. **Random Forest**:  
    Un conjunto de árboles de decisión. Es más robusto que un único árbol, ya que reduce la sobreajuste y mejora la precisión en tareas de clasificación y predicción. Se usa para detectar patrones anómalos en el tráfico de red.
    
3. **K-means**:  
    Un algoritmo de **agrupamiento no supervisado**. Se usa en la **minería de datos** para agrupar elementos similares, lo cual es útil para identificar patrones de comportamiento o intrusiones basadas en datos sin etiquetar.
    
4. **Support Vector Machines (SVM)**:  
    Utilizado en problemas de clasificación, este algoritmo encuentra el hiperplano que mejor separa las clases. SVM es eficaz para detectar patrones complejos en datos de seguridad, como en el análisis de malware.
    
5. **ANNs (Artificial Neural Networks)**:  
    Las redes neuronales artificiales son fundamentales para tareas de clasificación y regresión en **redes neuronales profundas (Deep Learning)**. Su capacidad para aprender representaciones complejas las hace útiles en ciberseguridad para detectar amenazas avanzadas.
    
6. **CNNs (Convolutional Neural Networks)**:  
    Principalmente utilizadas en procesamiento de imágenes, las CNN también se aplican en ciberseguridad para el análisis de tráfico de red en forma de secuencias visuales o para analizar patrones en archivos de configuración.
    
7. **RNNs (Recurrent Neural Networks)**:  
    Son útiles para **datos temporales** como los logs de seguridad y los datos de red. Su capacidad para "recordar" información de pasos anteriores las hace ideales para detectar intrusiones en el tiempo.
    

---

## **LLMs (Modelos de Lenguaje de Gran Escala)**

Los **LLMs** han experimentado un **avance significativo** en los últimos años, lo que les permite ser más efectivos en tareas complejas de procesamiento de lenguaje natural (NLP). En ciberseguridad, su capacidad para entender y generar texto puede ser crucial para tareas como la **extracción de IoCs** y la generación de **reportes automatizados**.

1. **Tamaño de entrada y salida**:  
    El contexto de un modelo se determina por el número de **tokens**. En un LLM, la **entrada** y **salida** dependen de los tokens que se pueden procesar. La mayoría de los modelos limitan la longitud del contexto debido a las restricciones computacionales.
    
2. **Capacidad computacional**:  
    Los LLMs requieren una capacidad de computación significativa. Aunque es posible usar técnicas de **cuantización** para reducir la carga computacional y hacer que los modelos sean más eficientes, esta sigue siendo una limitación importante.
    
3. **Parámetros y temperatura**:  
    Los parámetros como la **temperatura** afectan la creatividad y diversidad de las respuestas del modelo. Una temperatura baja hará que el modelo sea más determinista, mientras que una temperatura alta permite respuestas más aleatorias.
    
4. **Alucinaciones**:  
    Es común que los modelos generen **respuestas incorrectas o "alucinaciones"** debido a las limitaciones en los datos de entrenamiento o en la comprensión contextual del modelo.
    
5. **Top-K y max tokens**:  
    El **Top-K** es un parámetro que se utiliza para controlar cuántas opciones el modelo puede considerar antes de tomar una decisión. **Max tokens** define la longitud máxima de las secuencias que el modelo puede procesar.
    
6. **Conversión de palabras a tokens**:  
    En muchos modelos de lenguaje, una palabra puede convertirse en **tres tokens**. Esto es clave para entender cómo los modelos manejan el texto y cómo se mide su capacidad de procesamiento.
    

---

## **Mitigación con LLMs**

Los LLMs pueden ser usados en la **mitigación de amenazas** mediante técnicas como **Modelos RAG** (Retrieval-Augmented Generation). Estos modelos combinan la capacidad de un LLM con la **búsqueda de información** en una base de datos o repositorio, lo que mejora la precisión en la extracción de información relevante.

---

## **Knowledge Distillation**

**Knowledge Distillation** es una técnica en la que se entrena un modelo grande y luego se utiliza para crear un modelo más pequeño y eficiente. El modelo grande transmite su "conocimiento" al modelo más pequeño, que aún conserva muchas de las capacidades de detección, pero de manera más eficiente.

---

## **Prompt Engineering**

El **Prompt Engineering** es el proceso de diseñar de manera óptima los **prompts** que alimentan a los modelos de lenguaje para obtener los mejores resultados posibles. En ciberseguridad, esto puede implicar diseñar preguntas específicas para que el modelo identifique **IoCs** o patrones de ataque dentro de grandes volúmenes de datos.

---

## **Algunas aplicaciones de LLMs en Ciberseguridad**

1. **Inteligencia de amenazas**:  
    Los LLMs pueden analizar grandes cantidades de datos de inteligencia de amenazas, como informes de seguridad, bases de datos de vulnerabilidades y logs, para identificar patrones o anomalías.
    
2. **Fuzzing**:  
    Se pueden usar LLMs para generar **inputs maliciosos** en aplicaciones y sistemas para detectar vulnerabilidades de seguridad. La capacidad de los modelos para generar código aleatorio puede ayudar a automatizar pruebas de penetración.
    
3. **Generación de código**:  
    Los LLMs pueden generar fragmentos de código automáticamente. Esto puede ser útil tanto para la generación de parches de seguridad como para crear herramientas de análisis automatizadas.
    
4. **Minería de datos**:  
    Los LLMs pueden analizar grandes volúmenes de datos en busca de patrones anómalos, ayudar a descubrir **IoCs** o identificar comportamientos sospechosos en el tráfico de red o archivos almacenados.
    


---

## **LLM Alignment**

El **alignment** de los **Modelos de Lenguaje de Gran Escala (LLMs)** se refiere a la alineación del modelo con los objetivos específicos que se desean lograr, como la generación de respuestas coherentes y seguras. Para ello, se utilizan métodos como **fine-tuning** o **tuning a través de filtros**.  
El **tuning** o **ajuste fino** se puede hacer mediante un proceso conocido como **tunneling**, donde se aplica un filtro o restricción para mejorar el rendimiento del modelo y hacerlo más adecuado para una tarea o contexto específico.

---

## **Modelos Primitivos vs Open Source**

1. **Modelos Primitivos**:  
    Estos son modelos que se entrenan desde cero utilizando una gran cantidad de datos, sin una estructura predefinida. El entrenamiento de estos modelos puede ser costoso y largo, pero ofrecen mucha flexibilidad.
    
2. **Open Source**:  
    Los **modelos de código abierto** son aquellos que están disponibles públicamente, lo que permite a los desarrolladores utilizarlos, modificarlos y mejorarlos. Esto facilita el acceso a modelos avanzados sin necesidad de entrenarlos desde cero.  
    **Hugging Face** es una plataforma popular para modelos de código abierto. Permite a los usuarios **compartir modelos** y buscar en un **repositorio** de modelos clasificados por categorías, como modelos de NLP, clasificación, traducción, entre otros. Los usuarios también pueden **descargar** modelos entrenados y adaptarlos a sus necesidades.
    

---

## **Herramientas para ver los parámetros de un LLM**

**LLM Cal** es una herramienta que te permite **ver la cantidad de parámetros** que tiene un modelo de lenguaje. Esta herramienta es útil para evaluar la capacidad computacional de un modelo y determinar si un modelo es adecuado para un entorno específico o si necesita ser ajustado o reemplazado por otro más eficiente.

---

## **Despliegue en Local**

### **vLLM**

El **vLLM** es una herramienta que se utiliza para el **despliegue de modelos de alto rendimiento** en entornos locales. Está diseñado para facilitar la **implementación eficiente** de modelos grandes en máquinas locales, aprovechando al máximo los recursos de hardware disponibles.

> **Ventajas**:
> 
> - **Eficiencia** en el uso de la memoria y el poder de cómputo.
>     
> - **Optimización** para trabajar con modelos grandes en entornos de hardware no tan potentes.
>     

### **NVIDIA-SMI**

**nvidia-smi** es una herramienta de línea de comandos que se utiliza en sistemas **Linux** (y otros sistemas operativos) para interactuar con **GPU de NVIDIA**. Permite ver la **utilización de la GPU** y los procesos que están utilizando las unidades de procesamiento gráfico, lo cual es fundamental para **monitorear el rendimiento** al ejecutar modelos de aprendizaje profundo que requieren una gran capacidad computacional.

> **Uso de ei**:  
> Puedes usar este comando para **ver cuántos recursos está utilizando tu modelo** y ajustar parámetros o liberar recursos si es necesario.

---


---

## **Variable `cua_visible_devices`**

La variable **`cua_visible_devices`** es utilizada en el contexto de la gestión de dispositivos CUDA (para trabajar con GPUs) para **especificar qué GPUs** deben ser visibles y utilizadas por un programa o un modelo.  
Esta variable permite controlar de manera eficiente el uso de **dispositivos de GPU**, especialmente cuando se trabaja en entornos con múltiples GPUs disponibles. Al configurarla, puedes asegurarte de que un modelo solo se ejecute en la GPU deseada, lo cual es útil para optimizar recursos en servidores o estaciones de trabajo con múltiples dispositivos de procesamiento.

---

## **Hugging Face con vLLM**

**Hugging Face** es una plataforma popular que aloja una gran cantidad de modelos de IA, principalmente relacionados con el procesamiento de lenguaje natural (NLP). Para trabajar con **vLLM** (un modelo de alto rendimiento optimizado para entornos locales), se puede utilizar **Hugging Face** para buscar y descargar modelos preentrenados que sean compatibles con la estructura de vLLM.

- **Ventajas**: Hugging Face ofrece una **biblioteca de modelos optimizados** que se pueden cargar fácilmente en entornos locales, lo que reduce el tiempo de entrenamiento y facilita la implementación.
    
- **vLLM** se puede usar para ejecutar estos modelos de manera eficiente en una máquina local sin la necesidad de grandes recursos de servidor, **optimizado** para manejar modelos grandes.
    

---

## **Ollama vs vLLM**

**Ollama** es una plataforma de **IA** que permite ejecutar modelos de lenguaje a gran escala, pero tiene una diferencia clave respecto a **vLLM**:

- **Facilidad de uso**: Ollama está diseñado para ser más **fácil de usar**, proporcionando una experiencia más accesible para desarrolladores que no tienen experiencia en el manejo avanzado de GPUs o en la optimización de modelos. La configuración es generalmente más directa, lo que lo convierte en una opción atractiva para desarrolladores menos experimentados.
    
- **Optimización de VRAM**: A diferencia de **vLLM**, que está específicamente optimizado para trabajar con **VRAM** de manera eficiente, **Ollama** no está tan optimizado para usar únicamente la **VRAM**. Esto significa que puede no aprovechar de forma tan eficiente los recursos de la memoria gráfica, lo que puede generar un rendimiento subóptimo en tareas de alto rendimiento.
    

> **Resumen**: Ollama es ideal para tareas más sencillas o proyectos donde la facilidad de uso es crucial, pero si tu objetivo es optimizar el uso de recursos como la VRAM para modelos grandes y de alto rendimiento, vLLM puede ser la opción preferible.

---


---

## **Uso de Ollama desde Python**

Para ejecutar un modelo de **Ollama** desde Python, puedes utilizar los comandos correspondientes para interactuar con los modelos. Algunos ejemplos:

- **Ejecutar el modelo**:
    
    ```bash
    ollama run gemma3
    ```
    
    Este comando ejecuta el modelo llamado **gemma3**.
    
- **Ver el uso del modelo**:
    
    ```bash
    ollama show gemma3:27
    ```
    
    Este comando muestra el uso del modelo **gemma3**, especificando la versión **27**.
    

Ollama también cuenta con una **API de Python** que te permite interactuar programáticamente con el modelo. Además, proporciona una **interfaz web** (WebUI) para interactuar de manera visual.

### **Crear un entorno virtual para usar Ollama**

Para trabajar con Ollama en un entorno de Python, primero debes crear un entorno virtual para instalar las librerías necesarias:

```bash
python3 -m venv nombre_del_entorno
```

Esto creará un entorno virtual en el directorio especificado. Luego, activa el entorno:

```bash
source nombre_del_entorno/bin/activate  # En Linux/macOS
nombre_del_entorno\Scripts\activate    # En Windows
```

Una vez que el entorno esté activo, puedes instalar las dependencias necesarias y trabajar con **Ollama**.

### **Servicio en el puerto 8080**

Cuando instales y configures Ollama, se crea un **servicio** que escucha en el puerto **8080**, lo que te permite interactuar con el modelo desde un cliente HTTP, como Postman o a través de solicitudes **API**.

---

## **Threat Intelligence**

### **Crecimiento de amenazas cibernéticas**

El crecimiento de las amenazas cibernéticas ha generado la necesidad de mejorar las herramientas y enfoques tradicionales en la detección y mitigación de riesgos.

### **Limitaciones de los métodos tradicionales en la extracción de entidades**

Los métodos tradicionales, como el **scraping**, tienen limitaciones cuando se trata de **extraer entidades** de grandes volúmenes de datos de manera eficiente y precisa. Las herramientas automatizadas de IA, como los **LLMs**, ofrecen una ventaja al ser más adaptables y capaces de procesar datos más complejos de forma dinámica.

### **Uso de IA para automatización y adaptabilidad**

La **IA** permite la **automatización** de tareas que anteriormente requerían intervención manual. Esto es crucial en la **gestión de amenazas** y la **extracción de indicadores de compromiso** (IoCs), ya que los modelos pueden adaptarse a nuevas amenazas de manera más rápida que los enfoques tradicionales.

Si una máquina **no contemplada** en las bases de datos de seguridad aparece en el entorno, los **LLMs** pueden analizarla y ajustarse automáticamente a los nuevos patrones de comportamiento, mejorando la detección de amenazas en tiempo real.

---

## **IoCs (Indicadores de Compromiso)**

### **Pieza crítica de información para identificar actividades maliciosas**

Los **IoCs** son fundamentales en la identificación de actividades maliciosas dentro de sistemas y redes. Estos indicadores son utilizados para identificar ataques y intrusiones en tiempo real. Los **IoCs** se comparten a través de plataformas como **Maltego**, **MITRE**, **TAXII** y **STIX**.

### **Métodos de intercambio de CTI**

- **STIX (Structured Threat Information eXpression)**:  
    STIX es un formato estándar para compartir información de amenazas cibernéticas (CTI). Se representa en formato **JSON** y permite mapear relaciones entre diferentes objetos de amenaza, lo cual es útil para generar **gráficos** que muestran cómo los ataques se propagan a través de una red.
    
    Lo bueno de **STIX** es que **todos los sistemas de intercambio de CTI** como **TAXII**, **Maltego** y otros, soportan el formato STIX, lo que facilita el intercambio de información sobre amenazas entre diferentes plataformas de seguridad.
    

---

## **Extracción de IoCs y TTPs**

### **Datos de entrada**: Foros

Uno de los lugares más comunes para encontrar información sobre **IoCs** y **TTPs** (tácticas, técnicas y procedimientos) es en **foros de seguridad** y **comunidades cibernéticas**.

- **BreachForum**: Este foro es una fuente común de información sobre brechas de seguridad y actividades cibernéticas maliciosas. Los usuarios pueden crearse una cuenta para acceder a información compartida por otros actores.
    
- **Altennes.is**: Otro foro interesante donde se pueden encontrar **indicadores de compromiso** y análisis relacionados con ataques cibernéticos. Estos foros son frecuentemente monitoreados por investigadores de ciberseguridad para obtener datos valiosos sobre las amenazas emergentes.
    


---

## **¿Qué modelo es el mejor?**

Para determinar cuál es el mejor modelo en una tarea específica, es importante considerar el **contexto de los datos**. Por ejemplo, si estamos trabajando con **HTML**, el modelo debe ser capaz de manejar grandes volúmenes de datos estructurados, como en el caso de **IoCs** (Indicadores de Compromiso).

En **Hugging Face**, puedes **buscar modelos** que ya han sido entrenados y afinados para tareas específicas, como la detección de **IoCs**. Esto permite acceder a modelos que ya han demostrado ser efectivos para ciertos tipos de análisis.

---

## **Prueba científica de modelos**

Una vez que tienes una lista de modelos, **¿cómo pruebas cuál es el mejor desde un método científico?**  
La clave está en crear un **marco de pruebas** para evaluar los diferentes modelos de manera objetiva.

### **Marco de prueba para comparar modelos**

El marco de prueba debe tener en cuenta varios factores, entre ellos:

1. **Veracidad fundamental**:  
    Por ejemplo, comprobar que el **JSON** generado o procesado por el modelo es correcto, consistente y válido.
    
2. **Metodología de evaluación**:
    
    - Usa un **archivo de datos** como `main.py` con **batches** de datos para hacer la **inferencias**.
        
    - Realiza **llamadas a la API** para evaluar cómo el modelo procesa los datos.
        
    - **Preprocesa** el HTML y valida el JSON generado, para asegurarte de que el formato es el correcto y que los resultados son coherentes.
        
3. **Evaluación y resultados**: El **JRC** (Joint Research Centre) ha publicado resultados en investigaciones relacionadas con modelos de IA, y puedes usar este tipo de **resultados de investigación** como base para comparar tu modelo con otros preexistentes.
    

---

## **Fine-tuning y RAG con Llama**

Con **Llama**, puedes realizar **capas de fine-tuning** para adaptar el modelo a tareas específicas, como la **extracción de IoCs**.  
Además, puedes implementar **RAG (Retrieval-Augmented Generation)** para combinar la capacidad de generación del modelo con la búsqueda de información externa, lo que mejora su rendimiento al realizar tareas complejas.

Los parámetros que puedes ajustar incluyen:

- **Max Context**: Define el tamaño máximo del contexto que el modelo puede manejar.
    
- **Output Context**: Define el contexto de salida generado por el modelo.
    
- **Temperatura**: Controla la aleatoriedad de las respuestas generadas. Una temperatura baja hará que el modelo sea más determinista, mientras que una temperatura alta generará respuestas más variadas.
    

---

## **Métricas importantes en la evaluación**

### **Latencia y Tokens por segundo**

Las **métricas de latencia** y los **tokens por segundo** son fundamentales para evaluar la eficiencia de un modelo, especialmente en tareas de ciberseguridad donde la velocidad de respuesta puede ser crucial.

- **Latencia**: El tiempo que tarda el modelo en generar una respuesta.
    
- **Tokens por segundo**: La cantidad de tokens que el modelo puede procesar por segundo, lo cual afecta su capacidad para manejar grandes volúmenes de datos de forma eficiente.
    

---

### **Uso de Langfuse y Opik para métricas**

Para medir y mejorar el rendimiento de los modelos, puedes usar herramientas como **Langfuse** y **Opik**:

- **Langfuse** es una herramienta que permite el seguimiento y la **trazabilidad de las métricas** de los modelos, proporcionando información sobre su rendimiento a lo largo del tiempo.
    
- **Opik** es útil para la **observabilidad de los modelos** y permite obtener métricas adicionales relacionadas con la eficiencia y la precisión de las respuestas generadas.
    

---

## **Integraciones con Ollama**

Cuando trabajas con **Ollama**, puedes integrar estas herramientas de seguimiento de métricas de manera sencilla:

1. **Declarar variables de entorno**:  
    Al instalar Ollama, puedes configurar **variables de entorno** para habilitar la integración con herramientas como Langfuse.
    
2. **Uso desde Python**:  
    Una vez configurado, puedes llamar a Langfuse directamente desde el cliente de Python y automáticamente las trazas del modelo se enviarán a **Langfuse** para su análisis.
    

### Ejemplo de uso con Ollama:

```bash
ollama run gemma3 --verbose
```

Este comando ejecuta el modelo **gemma3** y, con el parámetro `--verbose`, te proporciona información detallada sobre el rendimiento del modelo y las métricas correspondientes.

---
Es mejor usar llama para hacer inferencia loca y tienes unas webuid aunque necesistas una versión especifica 
puedes utilizar python 
fine tunning tienes que evaluarlo por temas 
evolucionar a una arquictetura rag
 fien tuniin para que aprenden nuevas cosas
 olla te da diferentes tamaños de modelo 
 one time hacen un sacrificio con los pesos para que puedan ejecutarse con menos requisitos
 modelos o1
 