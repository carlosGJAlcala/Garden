---
title: "Introducción a la Inteligencia Artificial Generativa"
---

# Introducción a la Inteligencia Artificial Generativa

Análisis de datos para la ciberseguridad  
Máster Universitario en Ciberseguridad  
Universidad de Alcalá

## Introducción

### Pruebas Iniciales

Prueba estos ejemplos con herramientas de GenAI:

#### Ejemplo 1: Problemas de fechas

1. Open your most used GenAI tool
2. Insert the following prompt: "If today is 29th February, which day will be exactly in one year?"
3. What do you think about the answer?

#### Ejemplo 2: Generación de imágenes

1. Open your most used GenAI tool
2. Insert the following prompt: "Generate an image of a left-handed person writing with their left hand."
3. What do you think about the answer?

## El Futuro de los Empleos e IA

Source: The future of jobs report 2025 - World Economic Forum https://reports.weforum.org/docs/WEF_Futureof_Jobs_Report_2025.pdf

## ¿Qué es GenAI?

### Jerarquía de la Inteligencia Artificial

Artificial intelligence is not all machine learning, and machine learning is not all deep learning, deep learning is not all GenAI, and GenAI is not all LLMs!

- Artificial Intelligence
- Machine Learning
- Deep Learning
- Generative AI ( GenAI)
- LLMs, Computer Vision, Multimodal, Audio generation

### Definición

Generative AI ( GenAI) describes algorithms that can be used to create new content such as audio, text or images.

### Crecimiento Exponencial

Unprecedented path of growth and innovation

## Herramientas de GenAI

### Panorama de Herramientas

## El Mercado de GenAI

### Mercado Global

The GenAI market is experiencing unprecedented growth with numerous tools and platforms.

Fuente: https://iot-analytics.com/leading-generative-ai-companies/

### Limitaciones en Implementación Empresarial

The high interest in GenAI is hitting a speed limit in deploying at enterprise level

https://www.zdnet.com/article/enterprises-are-hitting-a-speed-limit-in-deploying-gen-ai-heres-why/

## Hype vs Realidad

### Consideraciones Críticas

- LLMs everywhere!

### Implicaciones de Soluciones Basadas en LLM

#### Limitaciones de LLM

- Lack of transparency
- Hallucinations

#### Costos

- Query with embeddings is 10x expensive than a traditional keyword search query

### Perspectiva Equilibrada

- What about "traditional" AI? ( e.g. LLMs for time series forecasting)
- Business value: Do we really need this latest model? Would a smaller/older SLM/LLMs do the work? Combination? ( e.g. agents)

### Transición Tecnológica

From task-oriented to general-purpose technologies

### Concentración de Poder

The power of AI in a handful companies vs AI as a commodity

- e.g. FAANG, OpenAI, NVIDIA

### Crecimiento Exponencial del Cómputo

Training Compute of Frontier AI Models Grows by 4-5x per Year

https://epoch.ai/blog/training-compute-of-frontier-ai-models-grows-by-4-5x-per-year  
https://epoch.ai/data-insights/llm-inference-price-trends

### IA Completando Tareas Complejas

AI completing more and more complex tasks

## Large Language Models ( LLMs)

### ¿Qué es un Language Model?

#### Concepto Fundamental

Language model predicts the next word given a context windows.

- Input: Sequence of words
- Output: Probability distribution over the dictionary/vocabulary

Source: https://lena-voita.github.io/nlpcourse/languagemodeling.html

## Foundation Models

### Definición

A foundation model, also referred to as a large X model ( LxM), is a machine learning or deep learning model trained on extensive datasets, enabling it to be applied across a broad spectrum of use cases.

### Costos y Recursos

Developing foundation models is highly resource-intensive, with the most advanced models incurring costs in the hundreds of millions of dollars. These expenses arise from acquiring, curating, and processing vast datasets, as well as the computational power needed for training. The high costs are driven by the need for sophisticated infrastructure, prolonged training durations, and specialised hardware such as GPUs.

### Adaptabilidad Económica

By contrast, adapting an existing foundation model for a specific task or employing it directly is significantly more economical, as it capitalises on pre-trained capabilities and typically requires only fine-tuning with smaller, task-specific datasets.

### Cambio de Paradigma

Unlike earlier approaches that relied on bespoke, task-specific models, foundation models serve as general-purpose systems that function as reusable infrastructure. Their emergence has been facilitated by:

- Advancements in parallel computing ( e.g., CUDA-enabled GPUs)
- Innovations in neural network architectures ( e.g., Transformers)
- Growing reliance on large-scale training data with minimal supervision

Source: https://humanloop.com/blog/foundation-models

## Cómo Entrenar un LLM

### Requisitos

- Extensively expensive: Need for GPU infrastructure
- High environmental impact

## Reinforcement Learning from Human Feedback ( RLHF)

### Concepto

Reinforcement Learning from Human Feedback ( RLHF) is a technique that enhances reinforcement learning ( RL) by incorporating human input to guide an AI model's behaviour. Instead of relying solely on pre-defined reward functions, RLHF leverages human preferences, corrections, or demonstrations to improve the learning process.

### Proceso de RLHF

#### Pretraining

The AI model is usually pre-trained using traditional supervised learning methods on large datasets.

#### Reward Model Training

Human feedback, typically in the form of rankings or comparisons of different outputs, is collected and used to train a reward model. This model learns to predict human preferences.

#### Fine-tuning with RL

The AI is then fine-tuned using reinforcement learning, where the reward model serves as a proxy for human judgment, guiding the AI to generate more desirable outputs.

Source: https://huggingface.co/blog/rlhf

## Factores Clave de LLMs

### Parámetros Importantes

| Parámetro | Descripción |
|---|---|
| **Cost** | Includes licensing fees, API usage costs, hardware requirements, and energy consumption for running the model efficiently. |
| **Deployment & Infrastructure** | Determines whether the model runs on the cloud ( e.g., OpenAI, Google Cloud) or on-premises, and assesses compute requirements ( GPUs, TPUs). |
| **Open Source vs Black-Box** | Open-source models ( e.g., LLaMA, Falcon) allow full transparency and customisation, while black-box models ( e.g., GPT-4) offer ease of use but limited control. |
| **Size ( Number of Parameters)** | Refers to the model's complexity, expressed in billions of parameters ( e.g., 7B, 13B, 175B), affecting performance, accuracy, and computational demands. |
| **Benchmarks** | Evaluates model capabilities through standardised tests like Elo ( general intelligence ranking), MMLU ( multi-task accuracy), and HumanEval ( coding proficiency). |
| **Temperature** | Controls randomness in responses: lower values ( e.g., 0.2) lead to deterministic answers, while higher values ( e.g., 0.8) increase diversity. |
| **Context Window** | Defines the maximum token length the model can consider at once ( e.g., 4K, 32K, 128K tokens), affecting coherence over long conversations. |
| **Base vs Instruct** | The 'base' model is a raw pretrained model, while the 'instruct' version has been fine-tuned to follow user instructions more effectively. |
| **Knowledge Cut-off** | The latest point in time up to which the model has been trained ( e.g., 2023), affecting its ability to provide recent information. |

### MMLU ( Multi-task Language Understanding) Score

MMLU is a benchmark for testing knowledge and reasoning of LLMs via a suite of exams. The test covers 57 tasks including elementary mathematics, US history, computer science and law. An expert level human is expected to achieve 89.9%. It is a text and reasoning benchmark.

Disclaimer: MMLU values are reported using 5-shot methodology and different values may be obtained with different prompting methods. Moreover, the combination of benchmarks other than MMLU may lead to different rankings.

## Capacidades de LLMs

### Aplicaciones Principales

- Personal and employee assistant
- Content generation
- Code generation
- Translation
- RAG, document processing, document augmentation
- Synthetic data generation
- Summarisation
- Personalized recommendations
- Insights generation

More information: https://aws.amazon.com/ai/generative-ai/use-cases/

## Cómo Aplicar GenAI

### Estrategias de Customización

| Enfoque | Descripción | Complejidad & Costo |
|---|---|---|
| **Out-of-the-box functionality** | Use a pre-trained model and provide the model with access to the right knowledge. | Bajo |
| **Context optimization** | Create Foundation Model | Medio-Bajo |
| **Prompt Engineering** | Use a pre-trained LLM model, and enhance the quality of the output via prompt engineering. | Bajo |
| **Retrieval Augmented Generation ( RAG)** | Use a pre-trained model and a knowledge base to provide the model with relevant data. | Medio |
| **Fine Tuning** | Fine-tune a pre-trained model to improve its ability for specific tasks. | Medio-Alto |
| **Train a model from scratch** | Train a model from scratch. | Alto |

## GenAI vs NLP Tradicional

### Comparación

- Sentiment analysis
- Entity extraction
- Translation
- Summarization
- Relationship extraction

Xiao, T., & Zhu, J. ( 2025). Foundations of Large Language Models. arXiv preprint arXiv:2501.09223.

## Implementación de GenAI

### Casos de Uso Empresariales

#### Acelerar Crecimiento

**Increase revenue generation through personalized marketing for target customers.**

**Increase the pace of new product or new service development and speedier go-to-market.**

#### Reducción de Costos & Eficiencia de Procesos

- The costs associated with traditional molecule research methods can be reduced by generating large datasets and simulating scenarios.
- Create process efficiencies through automating standard tasks and reducing manual interventions.

#### Nuevos Descubrimientos e Insights

Uncover new ideas, insights, and questions and generally unleash creativity.

### Consideraciones de Implementación

- General-purpose technology
- Unstructured and multimodal data
- Partial or end-to-end processes
- Human-in-the-loop

### Riesgos Identificados

- Cost
- Hallucinations
- User experience
- Compliance ( e.g. copyright)

More information: https://cloud.google.com/transform/101-real-world-generative-ai-use-cases-from-industry-leaders

## IA y Valor

Sjödin, D., Parida, V., Palmié, M., & Wincent, J. ( 2021). How AI capabilities enable business model innovation: Scaling AI through co-evolutionary processes and feedback loops. Journal of Business Research, 134, 574-587.

## Casos de Uso en Ciberseguridad

Generative AI and Large Language Models for Cyber Security: All Insights You Need https://arxiv.org/abs/2405.12750

## Cuándo NO Usar IA

Source: When Not to Use Generative AI 19 March 2024 - ID G00806238 https://www.gartner.com/document/5290563

## Prompt Engineering

### Técnicas de Prompting

#### In-Context Learning ( ICL)

Help LLM identify task and generate a good completion

### Zero-Shot vs One-Shot vs Few-Shot Prompting

#### Zero-Shot Prompting

Prompting the model with a question or task it has never seen before.

Example prompt:
```
Classify this review: This medicine really helped my daughter.
Sentiment:
```

#### One-Shot Prompting

Provide the model a single example of the desired behavior of the model.

Example prompt:
```
Classify this review: This medicine really helped my daughter.
Sentiment: Positive

Classify this review: I have a headache after taking this drug.
Sentiment:
```

#### Few-Shot Prompting

Provide the model with a small number of examples to guide the model's behavior.

Example prompt:
```
Classify this review: This medicine really helped my daughter.
Sentiment: Positive

Classify this review: I have a headache after taking this drug.
Sentiment: Negative

Classify this review: It caused an allergy.
Sentiment:
```

Source: https://www.promptingguide.ai

### Frameworks de Prompting

#### Chain-of-Thought ( CoT)

A series of intermediate reasoning steps—significantly improves the ability of large language models to perform complex reasoning.

Chain-of-Thought Prompting Elicits Reasoning in Large Language Models https://openreview.net/pdf?id=_VjQlMeSB_J  
https://www.promptingguide.ai

#### ReACT

A ReAct prompt consists of few-shot task-solving trajectories, with human-written text reasoning traces and actions, as well as environment observations in response to actions.

ReAct prompting is intuitive and flexible to design, and achieves state-of-the-art few-shot performances across a variety of tasks.

ReAct: Synergizing Reasoning and Acting in Language Models https://arxiv.org/abs/2210.03629  
https://www.promptingguide.ai

## Cómo Escribir un Buen Prompt

### Componentes Clave

- **Context**: Everything that the LLM needs to know for the task. Be very specific.
- **Persona**: Who is doing the task? Tell the LLM how it should act like, it will role play.
- **Task**: Clearly describe what is the task you ask for
- **Format**: How should the output look like? E.g: 300 words essay, short email, ...
- **Tone**: In which style should the output? E.g: formal, encouraging, excited...
- **Example**: Do you have any example of what you want? Then provide them.

## Retrieval-Augmented Generation ( RAG)

### Limitaciones de LLMs

## Alucinaciones en LLMs

### Concepto

Hallucinations in LLMs refer to the generation of content that is irrelevant, made-up, or inconsistent with the input data. This problem leads to incorrect information, challenging the trust placed in these models.

### Naturaleza No Determinista

LLMs are non-deterministic. This means that given the same input, they may generate different outputs on different occasions.

### Causas Raíz

- Training Data Issues
- Architectural and Training Objectives
- Inference Stage Challenges
- Prompt Engineering
- Stochastic Nature of Decoding Strategies ( e.g. temperature & creativity)
- Ambiguity Handling
- Over-Optimization for Specific Objectives

## Limitaciones de LLMs

### Conocimiento Limitado

#### Fechas de Corte de Conocimiento

| Modelo | Fecha de Corte | Búsqueda en Internet |
|---|---|---|
| ChatGPT Plus ( GPT-4) | December 2023 | Yes, via Bing search integration |
| GPT-4o | October 2023 | Yes, via Bing search integration |
| GPT-4o mini | October 2023 | Yes, via Bing search integration |
| OpenAI o1-preview | October 2023 | Yes, via Bing search integration |
| OpenAI o1-mini | October 2023 | Yes, via Bing search integration |
| Microsoft Copilot | 2021, with updates via Bing search and internal knowledge base | Yes, via Bing search integration |
| Meta AI | December 2023 | Yes |
| Google Gemini | No specific cutoff date, continuously updated | No direct search, but trained on extensive datasets including real-world information |
| Claude ( Anthropic) | August 2023 | No |

Source: https://github.com/HaoooWang/llm-knowledge-cutoff-dates

### LLMs Son Estáticos

LLMs are static: LLMs are trained on data from the past. It means that if LLMs don't have access to the internet or any way to look up information in real time, their knowledge remains frozen at their training date.

### Falta de Conocimiento de Dominio

LLMs lack domain knowledge

### Caja Negra ( Black-box)

LLMs act as black-boxes

## Retrieval-Augmented Generation ( RAG)

### Proceso General

#### Etapas de RAG

- Content and data collection → Chunking & Storage Indexing
- Chunk size, Chunk overlapping, Chunk strategy/Text splitter, Structure Aware Splitting ( by Sentence, Paragraph), Content-aware splitting ( HTML, LaTeX, code), NLP Chunking ( e.g. topic)
- Vectorisation → Embedding model with Dimensions, Quantization
- Retrieval → Vector database, Vector retrieval algorithm ( ANN, HNSW), Cosine similarity, Dot product, Reranking ( Content-based, Keyword based relevance, Hybrid search ( BM25))
- Augmentation → Prompt with LLM Model & Temperature, Toxicity
- Generation

### Vector Embeddings

#### Concepto

Vector embeddings are representations of data ( words, text, images) in a high-dimensional space where semantic meaning is captured through geometric proximity.

#### Ejemplo 2D

Palabras similares se ubican cerca en el espacio:

- King: [4, 5]
- Woman: [3, 3.5]
- Man: [5, 3]
- Apple: [2.5, -2]
- Banana: [2.5, -3]
- Orange: [4, -2.5]
- Football: [-3, 4]
- Golf: [-1.5, 3]
- Tennis: [-2, 2]

### Vector Database

Exploring Vector Databases: Pinecone, Chroma, Weaviate, Qdrant, Milvus, PgVector, and Redis | by Mehmet Ozkaya | Medium  
What is a Vector Database: A Beginner's Guide! - DEV Community

### RAG Pipeline

#### Etapas Detalladas

1. **Query Classification & Rewriting**
2. **Content and Data Collection → Chunking & Storage Indexing**
   - Chunk size
   - Chunk overlapping
   - Chunk strategy/Text splitter
   - Structure Aware Splitting ( by Sentence, Paragraph)
   - Content-aware splitting ( HTML, LaTeX, code)
   - NLP Chunking ( e.g. topic)
3. **Vectorisation**
   - Embedding model
   - Dimensions
   - Quantization
4. **Retrieval**
   - Vector database
   - Vector retrieval algorithm ( ANN, HNSW)
   - Cosine similarity
   - Dot product
   - Reranking ( Content-based, Keyword based relevance)
   - Hybrid search ( BM25)
5. **Augmentation & Generation**
   - Relevant data/chunks
   - Prompt = Query + Relevant data
   - LLM Model
   - Temperature
   - Toxicity

### Métricas de Evaluación RAG

#### RAG Assessment Framework ( RAGAs)

RAGAs is a framework that helps you evaluate your RAG pipeline on a component level ( generator + retriever).

#### Evaluación de Generación

##### Faithfulness ( Fidelidad)

Measures the factual consistency of the generated answer against the retrieved context. The faithfulness will be high if all the claims made in the answer can be inferred from the context.

- Answer ↔ Context

Ejemplo:
- Question: Where and when was Einstein born?
- Context: Albert Einstein ( born 14 March 1879) was a German-born theoretical physicist, widely held to be one of the greatest scientists of all time
- High faithfulness answer: Einstein was born in Germany on 14th March 1879.
- Low faithfulness answer: Einstein was born in Germany on 20th March 1879.

##### Answer Relevancy ( Relevancia de la Respuesta)

Measures how relevant is the generated answer to the question. The answer relevancy will be high if there is not incomplete or redundant information in the generated answers.

- Answer ↔ Question

Ejemplo:
- Question: Where is France and what is its capital?
- High relevance answer: France is in western Europe and Paris is its capital.
- Low relevance answer: France is in western Europe.

#### Evaluación de Recuperación

##### Context Precision ( Precisión del Contexto)

It measures the proportion of relevant chunks in the retrieved context. Context precision will be high if the higher-ranked items in the retrieved context are indeed present in the ground truth.

- Context ↔ Ground Truth

Ejemplo:
- Question: Where is France and what is its capital?
- Ground truth: France is in Western Europe and its capital is Paris.
- High context precision: ["France, in Western Europe, encompasses medieval cities, alpine villages and Mediterranean beaches. Paris, its capital, is famed for its fashion houses, classical art museums including the Louvre and monuments like the Eiffel Tower", "The country is also renowned for its wines and sophisticated cuisine. Lascaux's ancient cave drawings, Lyon's Roman theater and the vast Palace of Versailles attest to its rich history."]

##### Context Recall ( Exhaustividad del Contexto)

Measures how many of the relevant documents ( or pieces of information) were successfully retrieved. In short, recall is about not missing anything important.

- Context ↔ Ground Truth

Ejemplo:
- Question: Where is France and what is its capital?
- Ground truth: France is in Western Europe and its capital is Paris.
- High context recall: France, in Western Europe, encompasses medieval cities, alpine villages and Mediterranean beaches. Paris, its capital, is famed for its fashion houses, classical art museums including the Louvre and monuments like the Eiffel Tower.

##### Answer Correctness ( Corrección de la Respuesta)

The accuracy of the generated answer when compared to the ground truth. It encompasses two critical aspects: semantic similarity between the generated answer and the ground truth, as well as factual similarity.

- Answer ↔ Ground Truth

Ejemplo:
- Ground truth: Einstein was born in 1879 in Germany.
- High answer correctness: In 1879, Einstein was born in Germany.
- Low answer correctness: Einstein was born in Spain in 1879.

## Ejemplos Prácticos

### Ejemplo 1: Preparar una Entrevista

**Tool:** ChatGPT

**Prompt:**
```
"I want you to act as an interviewer. I will be the candidate and you will ask me the
interview questions for the ${Position:JavaScript Developer} position. I want you to
only reply as the interviewer. Do not write all the conversation at once. I want you
to only do the interview with me. Ask me the questions and wait for my answers.
Do not write explanations. Ask me the questions one by one like an interviewer
does and wait for my answers. My first sentence is "Hi""
```

### Ejemplo 2: Excel Expert

**Tool:** ChatGPT

**Prompt:**
```
"You have an Excel spreadsheet tracking sales data with the following columns: A
( Date), B ( Product), C ( Sales Amount), and D ( Region). You need to calculate the
total sales for a specific product ( e.g., 'Laptop') in a given region ( e.g., 'North').
Write an Excel formula that performs this calculation efficiently. Explain how the
formula works and suggest any possible improvements or alternatives."
```

### Ejemplo 3: Tu Desarrollador IA

**Tool:** ChatGPT

**Prompt:**
```
"You need to write a [program/script/function] in [programming language] that performs [specific task]. The code
should be efficient, well-structured, and include error handling where necessary. Ensure that it follows best practices
and is easy to understand. Additionally, provide a brief explanation of how the code works and suggest possible
improvements or alternative approaches."
```

**Ejemplo específico:** Write a Python script to build a Convolutional Neural Network ( CNN) pipeline for classifying images of cats and dogs. The images are stored in a folder with subdirectories 'cats' and 'dogs'. The pipeline should include: data preprocessing, model creation using TensorFlow/Keras, training with validation, and evaluation using a confusion matrix. Ensure proper data augmentation and implement error handling for missing or corrupted images. Finally, explain the implementation and suggest improvements for better accuracy.

### Ejemplo 4: Tu Probador IA

**Tool:** ChatGPT

**Prompt:**
```
"Act as a software tester and identify potential bugs in the given [program/script/system] written in [programming language]. Perform
rigorous testing, including edge cases, performance issues, and security vulnerabilities. Document any bugs found and suggest fixes
with explanations. If applicable, provide optimised code to resolve the issues while maintaining best coding practices."
```

**Ejemplo específico:**
```
"You are testing a Python web application that handles user authentication. Identify potential security vulnerabilities, such as SQL
injection and improper session handling. Suggest fixes with explanations and provide improved code snippets where necessary."
```

### Ejemplo 5: Preparación de Examen

**Prompt:**
```
"You are preparing for an upcoming [subject] exam and want to test your understanding of key concepts. Create a structured study
plan that includes a mix of revision strategies, practice questions, and time management techniques. Additionally, generate five
challenging exam-style questions on [specific topic] and provide detailed solutions. Aim to highlight common pitfalls and effective
problem-solving approaches. Your goal is to reinforce your knowledge and identify areas requiring further review."
```

**Ejemplo específico:**
```
"You are preparing for an upcoming Data analysis in cybersecurity and AI exam and want to test your understanding of key
concepts. Create a structured study plan that includes a mix of revision strategies, practice questions, and time management
techniques. Additionally, generate five challenging exam-style questions on deep learning and provide detailed solutions. Aim to
highlight common pitfalls and effective problem-solving approaches. Your goal is to reinforce your knowledge and identify areas
requiring further review. Questions should be in test format with four responses and only one is correct"
```

### Ejemplo 6: Extracción de Entidades en Documentos

**Tool:** ChatGPT

**Prompt:** Extract all the relevant entities on a JSON format

### Ejemplo 7: Extracción de Entidades en Imágenes

**Tool:** ChatGPT

**Prompt:** Extract all the relevant table on a JSON format

### Ejemplo 8: Planificador de Viajes

**Tool:** Bing Microsoft Copilot

**Prompt:** You are an experienced travel agent. I would like to visit China in April. I will be arriving to Shanghai on Friday, 4th April. I would like to learn about the culture and local gastronomy. Prepare an itinerary travelling from Shanghai to other relevant cities in China. I am flying back to Madrid on Sunday, 13th April.

### Ejemplo 9: Pronóstico del Tiempo

**Tool:** Perplexity

**Prompt:** Can you provide the latest weather forecast for [specific location] for the next [timeframe, e.g., 3 days]? I'd like details on temperature, precipitation, wind speed, and any severe weather warnings if available.

**Ejemplo específico:** Can you provide the latest weather forecast for Alcalá de Henares for the next 4 days? I'd like details on temperature, precipitation, wind speed, and any severe weather warnings if available.

### Ejemplo 10: Asistente de Escritura

**Tool:** ChatGPT, LeChat, Copilot

**Aplicaciones:** Adjust tone, rewrite, translate, proofread, brainstorming, summary

### Ejemplo 11: Generación de Imágenes

**Tool:** Bing vs LeChat vs ChatGPT

**Ejemplo:** "Generate an image of a Blue magical fairy tale land with a castle centered between trees with fairy lights and flowers with the text blue magic castle"

### Ejemplo 12: Notebook de Gemini

**Tool:** Gemini Notebook LM

### Ejemplo 13: Generación de Esquemas con Napkin.ai

**Tool:** Napkin.ai

**Prompt:**
```
"Summarise the best techniques for learning about machine learning applied to cybersecurity"
```

### Ejemplo 14: Generación de Música con Suno

**Tool:** Suno

**Ejemplo:** Create a song in Spanish, commercial reggaeton style with flutes and electric guitar, talking about how interesting is learning about data & analytics in cybersecurity

Result: https://suno.com/song/06897747-a665-438d-a358-f686cdaa618c?sh=o27neRHeBCn4B7hg

## Riesgos y Limitaciones

### El Lado Oscuro de la IA

OpenAI Used Kenyan Workers on Less Than $2 Per Hour to Make ChatGPT Less Toxic

## LLMs y Ciberseguridad: Vulnerabilidades y Riesgos

### Vulnerabilidades de LLM

- Prompt Injection
- Insecure output handling
- Data poisoning ( e.g. training, Search Index Poisoning)
- DDoS attacks
- Adversarial instructions ( e.g. Model Misuse and Control Biasness)
- Violations of Intellectual Property and Lack of Legal and Regulatory Compliance
- Risks associated with lifecycle management ( LLMOps)

### Estrategias de Mitigación

Las vulnerabilidades de LLM requieren estrategias de mitigación:

- Guardrails
- Toxicity filtering
- Regular audits
- Robust Security Policies
- Encryption
- Watermark: embedding signals into generated text that are invisible to humans but algorithmically detectable from a short span of tokens

Generative AI and Large Language Models for Cyber Security: All Insights You Need https://arxiv.org/abs/2405.12750  
A Watermark for Large Language Models https://arxiv.org/abs/2301.10226

## ¿Por Qué Open Source para LLMs?

### Limitaciones de Modelos Cerrados

- Data privacy
- Lack of transparency, bias, copyright

### Evolución del Open Source en LLMs

Open source LLMs is evolving with:

- Open weights and architecture
  - Open weight models ( e.g. LLama family, DeepSeek) are commoditizing the foundation-model layer
- Availability of model for deployment
- Public code for training
- Open data

#### Problemas en Modelos Open Source

Ejemplo: Bias/Censorship in DeepSeek

## IA Responsable

### Regulación de IA

### Sostenibilidad

[1] Kaack, Lynn H., et al. "Aligning artificial intelligence with climate change mitigation." Nature Climate Change 12.6 ( 2022): 518-527.

[2] 'Thirsty' ChatGPT uses four times more water than previously thought https://www.thetimes.com/uk/technology-uk/article/thirsty-chatgpt-uses-four-times-more-water-than-previously-thought-bc0pqswdr

[3] https://www2.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/genai-power-consumption-creates-need-for-more-sustainable-data-centers.html

## Detalles Adicionales

### Mixtures of Experts ( MoE)

#### Características

- Are pretrained much faster vs. dense models
- Have faster inference compared to a model with the same number of parameters
- Require high VRAM as all experts are loaded in memory
- Face many challenges in fine-tuning, but recent work with MoE instruction-tuning is promising

Source: https://huggingface.co/blog/moe

### Large Language Diffusion Models

#### LLaDA ( Large Language Diffusion with Masking)

LLaDA is a novel approach to large language models ( LLMs) that utilises diffusion-based generative modelling instead of the traditional autoregressive modelling ( ARM) used in most LLMs.

LLaDA models language distributions through a forward data masking process and a reverse process, predicting masked tokens using a Transformer-based mask predictor.

Source: [2502.09992] Large Language Diffusion Models

### Small Language Models ( SLMs)

## Reasoning Models

### Concepto

Reasoning models, like OpenAI o1 and o3-mini, are new large language models trained with reinforcement learning to perform complex reasoning.

#### Características

- Reasoning models think before they answer, producing a long internal chain of thought before responding to the user.

- Reasoning models excel in complex problem solving, coding, scientific reasoning, and multi-step planning for agentic workflows.

#### Ejemplo: Trying Grok

## Fine-tuning de LLMs

## Business Intelligence Generativa

## Text-to-SQL

Source: https://www.star-history.com/assets/blog/text2sql/vanna.webp

## Entity Extraction

Source: https://github.com/run-llama/llamacloudservices/blob/main/examples/extract/resumescreening.ipynb

## Multimodalidad

## Agents ( Agentes IA)

### ¿Qué es un Agente?

#### Definición

Generative AI agent can be defined as an application that attempts to achieve a goal by observing the world and acting upon it using the tools that it has at its disposal.

#### Autonomía

- Agents are autonomous and can act independently of human intervention, especially when provided with proper goals or objectives they are meant to achieve.
- Agents can also be proactive in their approach to reaching their goals

Source: Agents by Julia Wiesinger, Patrick Marlow and Vladimir Vuskovic | Kaggle  
Source: https://weaviate.io/blog/what-are-agentic-workflows  
Agent Design Pattern Catalogue: A Collection of Architectural Patterns for Foundation Model Based Agents ( arXiv paper)

### Beneficios de Agents

- Improved productivity
- Reduced costs
- Informed decision-making
- Improved customer experience

### Limitaciones de Agents

- Limited compute resources
- Data privacy concerns
- Ethical challenges
- Technical complexities

## Beneficios, Limitaciones y Pensamiento Crítico

### Beneficios

- Flexibility, adaptability, and customizability.
- Improved performance on complex tasks
- Self-correcting and continuous learning.
- Operational efficiency and scalability.

### Limitaciones y Desafíos

- Interoperability y Data limitation
- Reduced reliability as a result of increased autonomy.
- No free lunch: Unnecessary complexity for simple tasks.
- Maintenance overhead
- Ethical and practical considerations. Not all decisions should be delegated to AI systems.

### Pensamiento Crítico

Al considerar agents, preguntar:

- Is the task complex enough to require adaptive decision-making, or would a deterministic approach suffice?
- Would a simpler AI-assisted tool ( such as RAG without an agent) achieve the same outcome?
- Does the workflow involve uncertainty, changing conditions, or multi-step reasoning that an agent could handle more effectively?
- What are the risks associated with giving the agent autonomy, and can they be mitigated?
