---
title: "Introduction to Generative AI"
date: 2025-03-26
tags:
  - ciberseguridad
  - ia
  - deep-learning
---

**El examen dura 100 minutos**  
Tipo test, 4 opciones, teórico y práctica.  
Parte teórico/práctica: 3 preguntas, 72 PREGUNTAS.  
Se espera 1 párrafo, 2 o dos, pensamiento crítico. Se espera que se sea concreto.  
Tipo test: 2 mal quitan una bien. Entra desde Deep Learning.

# Apuntes


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[03-Desarrollo-Software/Bases-Datos/MongoDB|MongoDB]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

Los futuros trabajos que están creciendo son más los granjeros.  
Los roles se están especificando.  
Cuando se habla de inteligencia artificial hoy en día, se establece que es inteligencia generativa, pero eso no es así, hay más campos. La GenAI es el conjunto de algoritmos para generar nuevos datos, imágenes y texto. Está asociado con grandes modelos de lenguaje, audio o imágenes. Es importante el impacto que dan estas tecnologías. ChatGPT solo tardó dos meses en alcanzar 2 millones de usuarios. Hay mucha innovación en estos modelos. La innovación es muy grande, es casi imposible de seguir; cada semana sale algo nuevo, haciendo difícil su seguimiento.  
Hay multitud de herramientas. En esta sesión veremos varios ejemplos.  
ChatGPT usa un 3 por ciento del tráfico a nivel mundial.

# The disruptive potential of AI

Se espera que aumente el producto interior bruto en 25 trillones y es disruptiva en todos los trabajos.

# AI market

Nvidia, AWS son los que más se benefician por el tema de que utilizan herramientas.  
En tema de infraestructura se necesita GPU, por eso Nvidia.  
Hay otra rama que son los integradores de servicio, que son los que integran en diferentes herramientas. Por ejemplo, Accenture gana más solo con la implementación que OpenAI.  
Todo el mundo ve ese valor y se están haciendo un gran volumen de pruebas de conceptos (POCs), y muchos fallan debido a varios problemas: evolución de los distintos empleados que lo vean como un apoyo y no se despidan, los casos de uso que se ponen en las compañías son muy pocos. En volumen de empresa, 20–30 se hacen casos de uso en paralelo porque la mayoría no pasan a producción. El volumen solo llega al 10 por ciento.

# Hype

LLMs en todos lados.  
No tiene a veces buena calidad. Se usa en demasía y a veces alucina. También hay que ver en términos de coste. La API de OpenAI te cobra por token.  
Hay una tendencia de que se usan LLMs para todo, incluso para series temporales.  
Algo positivo es que el desarrollo ha supuesto pasar de un modelo orientado a tareas a obtener tecnología de alcance general, que vale para todo.  
Hay que tener en cuenta el beneficio en contexto empresarial: es ver la rentabilidad.  
El despliegue de LLM tiene un gran coste si confías en proveedores de servicios como OpenAI; tienes que pagar el coste de consumo.  
Proveedores de servicios como AWS son los que se llevan el pastel.  
El coste se está elevando mucho a la hora de entrenar, ya que casi se usa todo el contenido de Internet.  
En términos de rendimiento de modelos, se ha multiplicado por 5 cada año en términos de parámetros o de FLOPs. Si revisamos distintas compañías, se ve que tiene un crecimiento muy grande.  
Lo que está pasando: hay una competición entre modelos libres (Meta) y como servicio, y está produciendo que se reduzca el precio del token. Se va a convertir en una commodity, se van a abaratar a medida que avanza.  
Estos modelos pueden hacer tareas más complejas.

## LLM – Large Language Models

W2B y BERT son modelos anteriores a estos.  
Estos predicen la siguiente palabra dentro de un contexto.  
El principio: genera siguientes palabras de forma probabilística. Arquitectura de transformer, predicen siguiente término de forma iterativa. Lo mismo ocurre con las imágenes.

# Foundation Models

Modelos que se entrenan con grandes cantidades de manera pública.  
Requiere un gran coste de arquitectura distribuida en la nube y muchas GPUs.  
A partir de un foundation model se pueden hacer diferentes tareas, por ejemplo, responder preguntas.  
Fine tuning: darle una capa extra. El primer cambio: ML tradicional, tareas específicas. Estos modelos foundation se pueden usar para cualquier tarea.  
Estos modelos tienen un gran coste medioambiental. Tienen una relación directa con las emisiones de CO₂. Es importante tener en cuenta que ese costo grande va a estar limitado con esos modelos.

## Reinforcement Learning from Human Feedback – RLHF

Se parte de un modelo ya entrenado y se le da una capa dando ejemplos que han sido hechos por humanos.  
A partir de ahí se hace un modelo de recompensa que utilizan humanos.  
Se hace una capa de fine tuning en el cual se corrige. Se hace luego un reentreno con los comentarios de retroalimentación humanos. Ya así lo tienes orientado a ciertas tareas.

## LLMs

ChatGPT ha sacado nuevos modelos que se van a dar una capa de razonamiento.  
Se partió de BERT y se utilizó la arquitectura de transformer.

DeepSeek: modelo open way y tenía rendimiento como ChatGPT-4.

## LLM Factors

Para escoger un LLM tenemos que tener en cuenta parámetros como:

- el coste,
    
- deployment e infraestructura,
    
- open source vs black box,
    
- size (número de parámetros),
    
- benchmarks,
    
- temperatura,
    
- ventana de contexto,
    
- base vs instruct,
    
- knowledge cut-off.
    

La temperatura es un valor de la creatividad, mide cuánto de aleatorio es. “Yo soy feliz”, pero se puede recurrir a probabilidades más bajas.  
La ventana de contexto es el conjunto de tokens que le puedes pasar: 4k, 32k, 128k.  
Para tener el histórico de conversaciones se queda en la ventana de contexto. Publicar el contenido de 100 páginas viene determinado por las redes neuronales, cuántos parámetros se pueden coger.  
Hay distintos modelos dependiendo de su fine tuning: sin fine tuning, base vs instruct (es el chat).  
Es importante el knowledge cut-off: es el corte de conocimiento hasta donde se ha entrenado.  
Se pueden usar como asistente personal. Funcionan muy bien con generación de código porque ha cogido todo Stack Overflow.  
Término RAG: document processing, document augmentation.

## How to Apply GenAI

En un entorno corporativo hay diferentes capas. Todo pasa por un modelo foundation. ¿Cuál va a ser el coste?  
**Context optimization.**  
Prompt engineering: cómo se puede dar un texto para que dé la mejor respuesta.  
Retrieval augmented – RAG.  
**Dar el contexto a una información.**
LLM optimization.  
Fine tuning.  
Create foundation model.  
Roche hace modelos para generar moléculas. Roche tiene colaboración con Nvidia para generar nuevas líneas.

## GenAI vs Traditional NLP (importante, cae en examen)

ML tradicional: uno por cada

- Análisis de sentimiento
    
- Extracción de entidades (nombres de productos)
    
- Traducción
    
- Resumen
    

Se ha cambiado el foco: ahora un LLM te lo hace todo.  
Leyes de escalabilidad:  
Mejor dato → mayor infraestructura.

# Cómo implementar AIgen

¿Qué queremos?

- Reducir costes, despedir al equipo de soporte.
    
- Crecimiento: queremos aumentar nuestros beneficios.
    
- Generación de contenido por IA.
    
- Eficiencia de un proceso a título individual.
    
- Acelerar la innovación.
    
- Nuevos descubrimientos, nuevos fármacos, analizar nueva información.  
    El 80 % de los datos de una empresa no son estructurados. Se puede usar para encontrar patrones, ya que el ML tradicional necesita datos estructurados.  
    Para ver las cláusulas de nuevos contratos.
    

# Use Cases

Hay varias cosas donde no se pueden usar según la capacidad.  
Formato multimodal (audio, imágenes, etc.) permite automatizar procesos end to end. En algunos casos se necesita human-in-the-loop para verificar.  
Riesgo, coste, alucinaciones, user experience, compliance, copyright (implicaciones legales).  
En ciberseguridad: para generación de documentación legal, en auditoría, en análisis de logs, cualquier tipo de aplicación: malware, spam, formato texto.

**Por resumen de la asignatura**, se pone el foco en herramientas como ChatGPT.  
Hay otros modelos en función del área. Depende del contexto, si tenemos acceso a los recursos, etc.  
Hay identificadas otras tareas para generación de código.  
Hay decisiones automáticas, sistemas de percepción. En grafo se utiliza mucho en modelos de recomendación.

# Prompt Engineering

Es cómo te diriges:

- Zero-shot prompting: obtener una respuesta sin ejemplos.
    
- One-shot prompting: con un ejemplo.
    
- Few-shot prompting: diferentes ejemplos para contextualizar.
    
- Chain-of-thought (CoT): quieres que el modelo reflexione (“tómate un descanso y reflexiona”).
    
- Estándar: “Rogue tiene X + Y, ¿cuánto tiene ahora?”
    
- Ejemplo de chain-of-thought prompting: para que piense paso a paso.
    
- ReAct: tiene el objetivo de que el modelo actúe. Se da una serie de pasos para que un modelo razone.
    

## Cómo hacer un buen prompt

- Ser específico en la tarea.
    
- El contexto en que se da (ej. contexto legal).
    
- Persona: qué rol está actuando, por ejemplo, que actúa como tester.
    
- Formato: que sea información estructurada.
    
- El tono en que lo generes: tono formal o amistoso.  
    Ejemplo: one-shot, few-shot.
    

# Retrieval Augmented Generation – RAG

## LLMs Limitation

- Alucinaciones: “mano izquierda”, puede dar mayor riesgo como en tema de soporte a usuarios, recomendaciones incorrectas.
    
- LLMs are non-deterministic: para una misma pregunta genera diferentes respuestas.
    
- Para extracción de entidades en JSON.  
    Por ejemplo, le pides traducir una pregunta y te contesta la pregunta.  
    Tiene una fecha de límite de conocimiento.
    

El RAG permite limitar estas limitaciones, sobre todo limitar alucinaciones. A parte del prompt, le das un contexto y te aporta escalabilidad.

Consiste en:

- Retrieval: traer ese contenido relevante como contexto.
    
- Motores de bases de datos.
    
- Vector guarda, motores de búsqueda, retrieval, information retrieval.
    
- Perplexity, por ejemplo: hacer un asistente que coja la documentación en tu wiki privada.  
    La documentación se vectoriza en formato numérico (embedding), se almacena en una base de datos vectorial.  
    Utilizas redes neuronales. Tiene formato numérico.  
    Un usuario introduce una query que se convierte en vector. El mismo modelo busca vectores similares (similitud coseno o semántica), texto que contenga información que tenemos. Obtiene esos vectores, se comparten en el prompt.  
    El concepto de embedding se almacena en bases de datos vectoriales. MongoDB, PostgreSQL están dando soporte para vectorización y Azure también.
    

# Parte práctica

Hay que tener que el ChatGPT tiene capas de seguridad, de controles.  
Tienes capas con control.  
Subirle documentos es como RAG. Si haces un search estás conectando el RAG a internet.  
El objetivo del retrieval es obtener el contexto.

---
**Multimodal** va más allá de un LLM.  
El botón de rechazo va a tener varios LLMs, va pensando paso a paso.

En motores de búsqueda se está implementando que las búsquedas se hagan con lenguajes de tiempo.

En Google Meet se puede transcribir el resto, aunque te hace un resumen. Tiene ciertas limitaciones.

# Gemini Notebook LLM

Tiene acceso a la documentación, presentación. Utiliza tu Google Drive y genera nuevos documentos. Te genera un documento y te genera un documento.  
Utiliza agentes, son varios LLM que van utilizando Gemini Notebook LLM, arquitectura LLAMA.  
Arquitectura de core generativa.  
Napkin: herramienta que genera documentos. Puedes utilizar Napkin, imágenes a partir del texto.

# Music Generation with Suno

Genera música.

# Risks and Limitations (es importante)

Es el objetivo de la clase.  
Sesgos en los datos: mano derecha, no incluye la población.  
Compliance, propiedad intelectual.  
Problemas de alucinación.  
Problemas de explicabilidad (ChatGPT).

Pérdida de pensamiento crítico: la información que se genera no es fiable, tiene limitaciones de contenido.  
Términos de seguridad.  
Problemas de calidad de datos. Entorno empresarial: empresas cuyos datos no tienen metadatos.  
Metodologías de aprendizaje.  
Problemas de interoperabilidad.  
Coste en escala: se paga por cada token.  
Sostenibilidad: es muy costoso, gran energía.  
Rapid change rate: cambia cada semana.  
Vector databases: puede que no se utilicen el día de mañana.

# Hay una cara oculta de la IA

Los modelos ChatGPT en Kenia: para mitigar eso, comentarios se les pagaban 2 dólares la hora.  
Vulnerabilidades: conseguir tokens a través de LLMs (prompt injection).  
Denial of Service a estos modelos.  
Estos datos se utilizan para estos modelos para entrenar.  
Data poisoning.  
Insecure output handling.  
¿Qué limitaciones están? Los guardrails.  
Métrica de la toxicidad.  
Encriptación.  
Modelo open source, on-premise.  
Modelos open source con arquitecturas abiertas.  
OpenWeight: publican los pesos, por ejemplo LLAMA y DeepSeek.  
En DeepSeek hay capa con ciertos sesgos, sesgos de género.

# Responsible AI

Cómo mitigar: hacer un cumplimiento de las normativas.  
Normativas de Europa: EU AI Act es un acto.  
En Estados Unidos no se firma el ciudadano.  
Estos modelos son de doble filo.  
Google no cumple con estos objetivos por el tema del AI Act.  
Consumo de agua en data center: en general, medio litro de agua.

**SMLs**: modelos pequeños.

# Reasoning Models

Generativo, Business Intelligence.  
Dashboard conversacional: Tableau, Pull, para visualizar.  
Text to SQL.  
Se pueden vectorizar los datos para que me dé la respuesta.  
Multimodal LLM.

# Agentes

Hay tres conceptos: por un lado tienes el modelo, capa de orquestación, acceso a funcionalidad, acceso a memoria y herramientas.  
Agente RAG Workflow