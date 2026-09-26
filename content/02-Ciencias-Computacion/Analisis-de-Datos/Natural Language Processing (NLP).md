---
title: "Natural Language Processing (NLP)"
---

# Natural Language Processing (NLP)

Análisis de datos para la ciberseguridad
Máster Universitario en Ciberseguridad
Universidad de Alcalá

## Introduction

### Why NLP is important?

- There are more than 7'000 languages in the world
- Language is more than communication, it is also culture
- English represents almost 50% of the content on the Internet
- It is estimated that 80% to 90% of enterprise data is unstructured and heterogeneous (text, images, etc.) (Harbert, 2021)
- Digital content is growing rapidly, requiring automated solutions for analysis and understanding.

Sources:
Harbert, T., 2021. Tapping the power of unstructured data. MIT Sloan. Feb 1, 3.
https://en.wikipedia.org/wiki/Languagesusedonthe_Internet

The most spoken languages worldwide in 2023 (by speakers in millions)
Source: The most spoken languages worldwide in 2023 - Statista

### What is NLP?

- NLP is the computer science subfield that enables machines to process data encoded in natural language.
- NLP is a subfield of AI at the intersection with linguistics, linked to information retrieval, knowledge representation and computational linguistics
- NLP enable the completion of tasks like translation, text generation, sentiment analysis, speech recognition and information retrieval.

### Real-NLP world applications

- Search engines
- Chatbots and Smart Assistants
- Translation

### Role of NLP in enterprise solutions

### The NLP market

- The market size in the Text-based NLP market is projected to reach US$10.68bn in 2025.
- The market size is expected to show an annual growth rate (CAGR 2025-2030) of 25.34%, resulting in a market volume of US$33.04bn by 2030.
- GenAI development accelerated the adoption of NLP technologies

### Challenges in NLP

Source: Explore Natural Language Processing Techniques & Metrics

- Ambiguity:
  - e.g. "I saw a boy on a hill with the telescope" (syntactic)
  - e.g. "Alice told Jane that she would win the prize." (referential)
  - e.g. "John likes apples, and Mary does too" (ellipsis)
  - e.g. "What a pleasant day" (when it is raining heavily) (irony)
- Out-of-vocabulary (OOV) words
  - e.g. "cryptocurrency", "selfie"
- Resource constraints for low-resource languages
  - e.g. English vs Chinese, Spanish vs Croatian
- Bias:
  - e.g.

Source: https://www.mcislanguages.com/mcis-blog/diversity-of-languages-in-the-world/

### Language levels

| Level | Correspondence | Application |
| --- | --- | --- |
| Phonemes | Sounds | Speech-to-text conversion (ASR - Automatic Speech Recognition); Text-to-speech conversion (TTS - Text-to-Speech) |
| Morphemes and Lexemes | Roots, Prefixes, Suffixes | Tokenization; Part-of-speech tagging (POS tagging); Word Embeddings (Vector representation of words) |
| Syntax | Subject, Predicate, Relationships between words/tokens | Named Entity Recognition (NER); Extraction of relationships between words |
| Semantics | Meaning | Sentiment analysis; Topic detection; Text summarisation |

### NLP & Speech

- Text (Linguistic Content):
  - This represents the words, grammar, and meaning of what is being said.
  - It is what NLP processes when dealing with written or transcribed language.
- Voice (Acoustic Properties of Speech):
  - This includes tone, pitch, volume, speed, and pronunciation.
  - It carries additional meaning, such as emotion, emphasis, and speaker identity.
- Speech is not just text being read aloud with a voice. Spoken language has unique features such as:
  - Prosody (rhythm, intonation, stress) that affects meaning.
  - Phonetics & Phonology (sounds and pronunciation).
  - Context & Pragmatics, where meaning depends on how something is said, not just the words.
- Relationship to NLP:
  - Speech Recognition (ASR) converts speech : text, removing voice but keeping meaning.
  - Speech Synthesis (TTS) converts text : speech, adding a synthetic voice but often missing natural prosody and emotion.

Source: https://www.devopsschool.com/blog/what-are-speech-recognition-tools-and-use-cases-of-speech-recognition-tools/

## Text Processing Techniques

### The "traditional" NLP pipeline

- Data acquisition and exploration
- Text preprocessing
- Text representation
- Model selection and training
- Model evaluation
- Deployment and integration
- Monitoring and maintenance

### Text Preprocessing

"The quick brown fox jumps over the lazy dog."

Source: The quick brown fox jumps over the lazy dog | Images

### Stopwords & Text Cleaning

- Stopwords are high-frequency words such as prepositions, articles (e.g. "the", "to", "and", "also") that usually have little lexical content, and their presence in a text fails to distinguish it from other texts.
  - Original input text: "The quick brown fox jumps over the lazy dog."
- Removing stopwords helps reduce noise in textual data, making it easier for algorithms to focus on meaningful content in natural language processing (NLP) tasks.
  - Removing stopwords: "quick brown fox jumps lazy dog"
- Text cleaning often involves lowercasing, punctuation removal, stemming, lemmatisation, and handling special characters (e.g. emojis) or typos.

Source: Bird, S., Klein, E., & Loper, E. (2009). Natural language processing with Python: analyzing text with the natural language toolkit. "O'Reilly Media, Inc.".

### Normalisation

- Normalisation in NLP refers to transforming words into a standard form to reduce variations caused by inflections, making text processing more efficient.
- Stemming reduces words to their root form by removing suffixes, often producing non-linguistic stems.
- Lemmatisation converts words to their base or dictionary form (lemma) using linguistic analysis, ensuring valid words.
- Stemming is faster and rule-based but can produce incorrect words (lazy : lazi), whereas lemmatisation is more accurate but computationally expensive.
- British vs American English: in the context of normalisation (British) vs. normalization (American) and lemmatisation vs. lemmatization:
  - British English: The programme was normalised to standardise spelling before lemmatisation.
  - American English: The program was normalized to standardize spelling before lemmatization.
- Here, "normalised," "standardise," "lemmatisation," and "programme" follow British spelling conventions, while "normalized," "standardize," "lemmatization," and "program" adhere to American conventions.

Original input text: "The quick brown fox jumps over the lazy dog."
Stemming: "The quick brown fox jump over the lazi dog"
Lemmatization: "The quick brown fox jump over the lazy dog"
After removing stopwords: "quick brown fox jump lazy dog"

Source: Bird, S., Klein, E., & Loper, E. (2009). Natural language processing with Python: analyzing text with the natural language toolkit. "O'Reilly Media, Inc.".

### Tokenisation

- Tokenisation is the process of splitting text into smaller units, called tokens, which can be individual words, phrases, or symbols.
  - Original input text: "The quick brown fox jumps over the lazy dog."
- It is a fundamental step in natural language processing (NLP) that helps convert raw text into a structured format for further analysis.
  - Tokenisation output: [The, quick, brown, fox, jumps, over, the, lazy, dog]
- Tokens are typically the building blocks for various NLP tasks, such as text analysis, sentiment analysis, or machine learning.
  - Output after cleaning and lemmatisation: [quick, brown, fox, jump, lazy, dog]
- A token is not always equivalent to a word due to punctuation marks, special characters, or multi-word expressions.
  - Original input text: "Hello, world!"
- e.g. Token as a unit of payment in text generation (e.g. OpenAI Cost models)
  - Tokenisation output: ["Hello", ",", "world", "!"]

Source: Bird, S., Klein, E., & Loper, E. (2009). Natural language processing with Python: analyzing text with the natural language toolkit. "O'Reilly Media, Inc.".

## Syntactic Processing

### Part-of-Speech (POS) Tagging

- Part-of-Speech (POS) Tagging is the process of assigning each word in a sentence to its appropriate grammatical category (part of speech), such as noun, verb, adjective, adverb, etc.
  - Original input text: "The quick brown fox jumps over the lazy dog."
- POS tagging is essential in understanding the structure and meaning of a sentence in natural language processing (NLP).
  - POS output:
    - "The" is tagged as determiner (DT)
    - "quick" is tagged as adjective (JJ)
    - "brown" is tagged as adjective (JJ)
    - "fox" is tagged as noun (NN)
    - "jumps" is tagged as verb (VBZ)
    - "over" is tagged as preposition (IN)
    - "the" is tagged as determiner (DT)
    - "lazy" is tagged as adjective (JJ)
    - "dog" is tagged as noun (NN)
- It helps algorithms differentiate between words that may have different meanings or functions based on their role in the sentence.
- POS tagging identifies the grammatical role of each word, which is crucial for tasks such as syntactic parsing, sentiment analysis, and machine translation.

Source: Bird, S., Klein, E., & Loper, E. (2009). Natural language processing with Python: analyzing text with the natural language toolkit. "O'Reilly Media, Inc.".

## Named-entity recognition (NER)

- Named-Entity Recognition (NER) is a subtask of information extraction that aims to identify and classify named entities in text, such as the names of people, organisations, locations, dates, and more.
- Its main goal is to structure unstructured information.
- It can be domain-specific (e.g. healthcare, cybersecurity).
- For example, in cybersecurity, a NER pipeline can be trained to identify IP addresses, attack types, or vulnerabilities.
- The goal of NER is to recognise these specific entities and classify them into predefined categories.
- An ontology is a structured framework that defines the relationships between concepts within a specific domain. In NER, ontologies provide a rich set of predefined categories and relationships between entities, such as people, organisations, locations, and domain-specific terms.
- Applications: relationship extraction, metadata and ontology generation, query expansion and filters in search engines, recommendation engines, sentiment analysis.

Original input text: "Barack Obama visited London on Monday."

NER output:
Barack Obama: Person (PER)
London: Location (LOC)
Monday: Date (DATE)

## Representation of Text

### Text as a numerical representation

- Text is converted into numerical representations to enable machine learning models to process and understand it.
- Machines rely on numerical data for analysis, as they cannot inherently work with raw text.
- Algorithms like logistic regression, decision trees, and neural networks require numerical input for calculations.
- Text, being qualitative, must be transformed into a numerical format for these models to function.
- Many machine learning techniques, such as clustering and classification, rely on mathematical operations that are meaningful only with numerical data.
- Numerical representations allow for the extraction of features from text, such as word frequency, co-occurrence, and semantic relationships, which are essential for analysis.

Source: Bengfort, B., Bilbro, R., & Ojeda, T. (2018). Applied text analysis with Python: Enabling language-aware data products with machine learning. "O'Reilly Media, Inc.".

### Text as a numerical representation (continued)

- One-hot encoding
  - Each word in a text is represented as a vector with a length equal to the size of the vocabulary.
  - Each vector contains all zeros, except for a 1 at the position corresponding to the word's index in the vocabulary. This method creates a unique vector for every word.
  - One-hot encoding is simple but can lead to high-dimensional vectors, especially when the vocabulary size is large.
  - This can result in sparsity, where most of the values in the vectors are zeros, leading to inefficiencies.
  - e.g. vocabulary of three words: apple, banana and cherry
    - "apple": [1, 0, 0]
    - "banana": [0, 1, 0]
    - "cherry": [0, 0, 1]

Source: Bengfort, B., Bilbro, R., & Ojeda, T. (2018). Applied text analysis with Python: Enabling language-aware data products with machine learning. "O'Reilly Media, Inc.".
### Text as a numerical representation (continued II)

- Count vectorisation
  - Involves representing each document (or text) as a vector, where each element corresponds to the frequency of a word in the document. The entire corpus is examined to create a vocabulary, and then for each document, the frequency of words from the vocabulary is counted.
  - Count vectorisation is straightforward and captures word frequency but does not account for word order or semantic meaning. It can also lead to high-dimensional vectors, though it is less sparse than one-hot encoding.
  - For example, consider the corpus containing two sentences:
    - "apple banana apple"
    - "banana cherry cherry"
  - The vocabulary would be: ["apple", "banana", "cherry"].
  - The count vectors for each sentence would be:
    - "apple banana apple": [2, 1, 0] (2 apples, 1 banana, 0 cherries)
    - "banana cherry cherry": [0, 1, 2] (0 apples, 1 banana, 2 cherries)

Source: Bengfort, B., Bilbro, R., & Ojeda, T. (2018). Applied text analysis with Python: Enabling language-aware data products with machine learning. "O'Reilly Media, Inc.".

### Bag of Words (BoW)

- BoW is a simple method that represents text data as a collection of words, disregarding grammar and word order, but keeping track of word frequency.
- How it works:
  - A vocabulary is created from the entire corpus (collection of documents).
  - Each document is represented as a vector, where each dimension corresponds to a word in the vocabulary. The value of each dimension is the frequency of the word in the document.
- Advantages:
  - Simple and easy to understand.
  - Effective for many tasks like classification, clustering, etc.
- Disadvantages:
  - Ignores word order and grammar.
  - Can result in sparse vectors, especially with large vocabularies.
  - Doesn't account for the importance of words in different contexts.

Given two documents:
- Document 1: "I like cats"
- Document 2: "I like dogs"

The vocabulary would be: ["I", "like", "cats", "dogs"]

The BoW vectors would be:
- Document 1: [1, 1, 1, 0]
  - Explanation: (1 occurrence of "I", 1 of "like", 1 of "cats", 0 of "dogs")
- Document 2: [1, 1, 0, 1]
  - Explanation: (1 occurrence of "I", 1 of "like", 0 of "cats", 1 of "dogs")

Source: Bengfort, B., Bilbro, R., & Ojeda, T. (2018). Applied text analysis with Python: Enabling language-aware data products with machine learning. "O'Reilly Media, Inc.".

### Term Frequency - Inverse Document Frequency (TF-IDF)

- TF-IDF is a more advanced method that evaluates the importance of a word in a document relative to a corpus. It takes into account both the frequency of the word in a document and how unique or common it is across the corpus.
- Advantages:
  - Takes into account the importance of words in the entire corpus.
  - Reduces the weight of common words (e.g., "the", "is") and increases the importance of rare, more informative words.
- Disadvantages:
  - More complex than BoW.
  - May still result in sparse vectors for large corpora.
  - Doesn't capture word order or context.
- TF-IDF also has use cases in the field of information retrieval, with one common example being search engines. Since TF-IDF can tell you about the relevant importance of a term based upon a document, a search engine can use TF-IDF to help rank search results based on relevance, with results which are more relevant to the user having higher TF-IDF scores.

A = "The car is driven on the road"
B = "The truck is driven on the highway"

Source: Bengfort, B., Bilbro, R., & Ojeda, T. (2018). Applied text analysis with Python: Enabling language-aware data products with machine learning. "O'Reilly Media, Inc.".

## Co-occurrence N-grams & Statistical Language Models

### Co-occurrence N-grams

- Represent sequences of N words that appear together in a given context.
- Useful for capturing word dependencies and context.
- Commonly used in tasks like text prediction and language modelling.
- Example: In a bigram model, "data science" and "machine learning" are consecutive pairs.

### Statistical Language Models

- Predict the probability of a word given its context (previous words).
- Use N-grams (e.g., bigrams, trigrams) to estimate word sequences.
- Calculate likelihood based on word frequencies and co-occurrence in training data.
- Examples: n-gram models, Hidden Markov Models (HMM).

### Applications

- Text generation: Predict the next word in a sentence.
- Speech recognition: Improve word prediction from acoustic signals.
- Machine translation: Translate text based on learned word sequences.

### Co-occurrence networks

### NER - Example from research

The following is the raw text extracted from a research pipeline diagram (figure); the original layout could not be reliably reconstructed into linear prose, so it is preserved verbatim, line by line, in its original order:

```
1 Collect, preprocess and explore data A group of six experts validated the
relevance of the data set ( 95%
confidence and 10% margin error):
Query: Technology in healthcare
relevance = 73.90%
innovation
Krippendorff's alpha = 0.58 ( moderate)
Period: 01/01/2020-31/01/2023
API integration
Data preprocessing
Duplicates removal 74,813 headlines
Emoji and URL removal
GDELT 190,284 news articles Stopwords elimination 59,818 full articles Data trends and term frequency
Lemmatisation analysis
Text corpus
2 Generate a co-occurence network from entities to identify most relevant relationships
DBpedia
Entities are extracted from the text Most relevant relationships
The clusters of entities are identified
corpus using Spacy, leveraging the The co-occurrence network of are identified
based on modularity class and
DBpedia taxonomy. relationships is generated
eigenvector centrality
Co-occurrence entity network
Named-Entity
Text corpus Entity linking
Recognition
"In a groundbreaking development, a new
AI-powered medical device leveraging IoT AI label:Artificial intelligence entity1 1 entity2 1 entity3 1 entity4 1 entity1 2 entity2 2
technology and machine learning algorithms
DBpedia
has been introduced, revolutionising patient slidingwindow = 3
monitoring and telehealth."
Knowledge base
News article #1 News article #2
```

### NER - Example from research (continued)

The same diagram is repeated on the next slide with the named entities highlighted in brackets:

```
1 Collect, preprocess and explore data A group of six experts validated the
relevance of the data set ( 95%
confidence and 10% margin error):
Query: Technology in healthcare
relevance = 73.90%
innovation
Krippendorff's alpha = 0.58 ( moderate)
Period: 01/01/2020-31/01/2023
API integration
Data preprocessing
Duplicates removal 74,813 headlines
Emoji and URL removal
GDELT 190,284 news articles Stopwords elimination 59,818 full articles Data trends and term frequency
Lemmatisation analysis
Text corpus
2 Generate a co-occurence network from entities to identify most relevant relationships
DBpedia
Entities are extracted from the text Most relevant relationships
The clusters of entities are identified
corpus using Spacy, leveraging the The co-occurrence network of are identified
based on modularity class and
DBpedia taxonomy. relationships is generated
eigenvector centrality
Co-occurrence entity network
Named-Entity
Text corpus Entity linking
Recognition
"In a groundbreaking development, a new
[AI]-powered [medical device] leveraging AI label:Artificial intelligence entity1 1 entity2 1 entity3 1 entity4 1 entity1 2 entity2 2
[IoT] technology and [machine learning]
DBpedia
algorithms has been introduced, slidingwindow = 3
revolutionising [patient monitoring] and
[telehealth]."
Knowledge base
News article #1 News article #2
```

## DBPedia

- The DBpedia community project extracts structured, multilingual knowledge from Wikipedia and makes it freely available on the Web using Semantic Web and Linked Data technologies.
- The project extracts knowledge from 111 different language editions of Wikipedia.
- The largest DBpedia knowledge base which is extracted from the English edition of Wikipedia consists of over 400 million facts that describe 3.7 million things.
- The DBpedia knowledge bases that are extracted from the other 110 Wikipedia editions together consist of 1.46 billion facts and describe 10 million additional things.
- The DBpedia project maps Wikipedia infoboxes from 27 different language editions to a single shared ontology consisting of 320 classes and 1,650 properties

Source: Lehmann, J., Isele, R., Jakob, M., Jentzsch, A., Kontokostas, D., Mendes, P. N., ... & Bizer, C. (2015). Dbpedia–a large-scale, multilingual knowledge base extracted from wikipedia. Semantic web, 6 (2), 167-195.

## Findings

- Headlines in news mining contain limited information
- Entity clusters:
  - COVID-19 pandemic
  - Healthcare systems
  - Technology in healthcare
  - Medical research
  - Healthcare market
  - Environmental health and sustainability
- Industry 4.0 technologies in enabling digital health:
  - Artificial Intelligence: Medical imaging, telehealth and precision medicine.
  - Blockchain: Electronic Health Records (EHR)
  - Big data: EHR, precision medicine.
  - Cloud computing: Telehealth, medical device, EHR.
  - IoT: Medical device, wearable technology and telehealth
  - Machine learning: EHR, medical imaging.

Akter, S., Michael, K., Uddin, M. R., McCarthy, G., & Rahman, M. (2022). Transforming business using digital innovations: The application of AI, blockchain, cloud and data analytics. Annals of Operations Research, 1-33.
Karatas, M., Eriskin, L., Deveci, M., Pamucar, D., & Garg, H. (2022). Big Data for Healthcare Industry 4.0: Applications, challenges and future perspectives. Expert Systems with Applications, 200, 116912.
Kasoju, N., Remya, N. S., Sasi, R., Sujesh, S., Soman, B., Kesavadas, C., ... & Behari, S. (2023). Digital health: trends, opportunities and challenges in medical devices, pharma and bio-technology. CSI Transactions on ICT, 1-20.

*(This "Findings" slide was repeated identically three times in the original deck; the duplicates have been collapsed here.)*

## Word embeddings

- Context-sensitive: Words are represented based on the context in which they appear. Word embeddings capture the relationships between words based on the surrounding words (e.g., words that frequently appear in similar contexts will have similar vector representations).
- Captures semantic relationships: Word embeddings can capture relationships between words, such as synonyms, antonyms, or analogies. For example, the words "king" and "queen" will have vectors that are very close in the vector space due to their shared semantic meaning.
- Produce dense, low-dimensional vectors. Word2Vec, for instance, typically generates vectors of fixed size (e.g., 100, 200, or 300 dimensions), much smaller than the dimensionality of BoW or TF-IDF representations.
- Main Word Embeddings techniques: Word2Vec, GloVe, FastText

### Word2Vec

- Uses shallow neural networks to predict word context in either a skip-gram (predicting context words from a target word) or continuous bag of words (CBOW) model.
- The result is a vector that captures the meaning of the word based on its context in a corpus.
- Skip-gram: autocompletion, recommendation systems, word similarity (e.g. synonyms).
- CBOW: text classification, NER

Source: Mikolov, T., Chen, K., Corrado, G., & Dean, J. (2013). Efficient estimation of word representations in vector space. arXiv preprint arXiv:1301.3781.

## Traditional NLP Techniques

### Traditional ML approaches in NLP

- Techniques: Naive Bayes, SVM, Logistic regression, Decision tree, Random forest, KNN
- Feature selection: TF, TF-IDF, Information Gain, Entropy, etc.
- Limitations: noise, redundancy, contextual information, high dimensionality, data quality
- Tasks: text classification, sentiment analysis (binary: positive/negative, multi-class: anger, disgust, fear, joy, sadness and surprise (Ekman & Friesen, 1971), information retrieval, entity recognition.

Source:
Bird, S., Klein, E., & Loper, E. (2009). Natural language processing with Python: analyzing text with the natural language toolkit. "O'Reilly Media, Inc.".
Ekman, P., & Friesen, W. V. (1971). Constants across cultures in the face and emotion. Journal of personality and social psychology, 17 (2), 124.

## Topic modelling

- Topic Modelling is a type of statistical model used in Natural Language Processing (NLP) to discover abstract topics that occur in a collection of documents.
- It is an unsupervised learning technique that aims to automatically identify patterns in text data, grouping words that frequently occur together and assigning them to topics.
- A topic is a collection of words that frequently occur together within a given set of documents. For example, in a collection of articles, a topic might include words like "economy," "money," and "banking," which all point toward a financial topic.
- Techniques: LDA, NMF, etc.
- Applications: text summarisation, social network analysis

Blei, D. M., Ng, A. Y., & Jordan, M. I. (2003). Latent Dirichlet Allocation (LDA). Journal of machine Learning research, 3 (Jan), 993-1022.
Luo, Minnan, et al. "Probabilistic non-negative matrix factorization and its robust extensions for topic modeling." Proceedings of the AAAI Conference on Artificial Intelligence. Vol. 31. No. 1. 2017.

### Keyword co-occurrence graph-based topic modelling

The following is the raw text extracted from a methodology diagram (graph/formula figure) on this slide. The original spatial layout could not be reliably reconstructed into linear prose or a real table, so — per the note on irrecoverable extractor scrambling — it is preserved verbatim, line by line, in its original order, with only the pure junk table-separator rows (`| --- | ... |`) removed:

```
Methodology
-
-
-
-
-
-
-
-
d = 3
-
-
-
-
| | | | | | | | | d = 2 | | | w : initial weight | | |
| | | | | Graph topic modelling | | | | | | | 0 | | |
| | | | | | | | | d = 1 | | | d: distance/sliding window | | |
| | | a | | | | | | | w | w -1 | w -2 | | |
| | | 2 | | | | | | | 0 | 0 | 0 | | |
co-occurred
| | mentioned | | | | | | doc 1 | term1 | term2 | term3 | term4 … | term m | |
{weight}
| | | | | | | | | | 1 | 1 | 1 1 | | 1 |
a
| | | 1 | | t | | t | | | | w | w -1 w -2 | | |
| | | | | 1 | | 2 | | | d = 1 | | | | |
| | | | | | | | | | | 0 | 0 0 | | |
createdby
d = 2
G ( V,E) where:
| | | T | | | | | | | | d = 3 | | | |
G is a directed graph
1
V = {v1, …vj} = {v ∈ C}, j ∈ ℕ
E = {e,...e} where E ⊆ {{x,y} | x,y ∈ V}, x,y,k ∈ ℕ
1 k
used used used W = Σw | w = f ( e , d ) = w-d +1, where e ∈ E, x,y ∈ V, d ∈ {1,2,3}, d ∈ ℕ ( Paranyushkin, 2019)
| | | | | | | | k k | x,y x,y | 0 x,y | | | | |
Weight
| | | | | | | W = Σw | w = f ( e | | , d ) = 2w0-d ( x,y) where e ∈ E, x,y ∈ V, d ∈ {1,2,3}, d ∈ ℕ W = Σw | w = f ( e | | | | | , d ) = |
| | | | | | | | k k | x,y x,y | | | | k k | x,y x,y |
+1)1+γ, where e ∈ E, x,y ∈ V, d ∈ {1,2,3} where:
( w-d
| | | | | | | | 0 x,y | | | | | | |
| | | | | | Relevance | | γ=alpha·verifiedrelevance+beta·f ( followersrelevance)+delta·f ( statsrelevance) | | | | | | |
Distance d = distance ( term,term)
- t
-
- t
-
-
- t
-
- x,y
- x
- y
-
-
-
-
- 1
-
- 2
-
-
- 3
-
-
-
-
-
-
-
-
| | | | | | | | | | | | e ( W | ) | |
| | | | | | | Sampling | | | | | k-1 | k-1 | |
| | co-occurred | | co-occurred | | | | | | | v | | | |
2
e ( W)
| | | | | | | | | | e ( W) | | 4 4 | | |
| | | | | | | | | | 2 2 | | | e ( W) | |
k k
- Node type
-
-
-
-
-
-
-
-
-
- e ( W)
-
-
-
| | | co-occurred | | | | | | v | | | | | |
- ○ Tweet ( T)
-
-
-
-
-
-
-
- 1
-
- 3
- 3
-
- v
v j
4
○ Author ( a)
| | | | | | | | | | e ( W ) | | e ( W ) | | |
- ○ Term ( t)
-
-
-
-
-
-
-
-
- 1 1
-
-
-
-
5 5
| | | | | | | | | | | v | | Centrality parameter | |
3
Network layout
e ( W)
```

Paranyushkin, D. (2019, May). InfraNodus: Generating insight using text network analysis. In The world wide web conference (pp. 3584-3589). 6 6

## Limitations

- Difficulty in capturing context
  - Struggles with long-range dependencies
  - Limited Understanding of Semantics (e.g. co-occurrence)
- Sparsity
- Handling of unstructured data
- Curse of dimensionality and scalability Issues
- Overfitting and high variance
- Feature engineering complexity

## NLP frameworks in Python

## Language models

Source: Image from The Evolution of NLP (& How Dataiku Can Help)

## Deep Learning NLP

### Multilayer Perceptron (MLP)

### Neural Network Architectures

## RNNs & LSTMs

### Recurrent Neural Networks (RNNs)

- Designed for sequence-based tasks (e.g., text, speech).
- Maintain hidden states to process sequential data.
- Struggle with long-term dependencies due to vanishing gradients.

### Long Short-Term Memory (LSTMs)

- An improved version of RNNs with gates (input, forget, output) to manage memory.
- Handle long-range dependencies better by controlling what information is retained or discarded.

Applications:
- Text generation, machine translation, speech recognition, NER

#### Limitations

- Computationally expensive – LSTMs require more memory and processing power.
- Slow training – Sequential processing makes training inefficient.
- Limited parallelism – Cannot fully leverage modern GPUs like Transformers.
- Still struggles with very long sequences – Transformers (e.g., BERT, GPT) outperform LSTMs in many NLP tasks.

Jurafsky, D., & Martin, J. H. Speech and Language Processing: An Introduction to Natural Language Processing, Computational Linguistics, and Speech Recognition. 8.pdf

## Attention Mechanism & Transformer Architecture

Source: Vaswani et al. (2017). "Attention Is All You Need"

### Translation with transformers

Source: https://jalammar.github.io/images/t/transformerdecoding_1.gif

### Bidirectional Encoder Representations from Transformers (BERT)

- BERT is a deep learning-based NLP model developed by Google.
- It is built on the Transformer architecture and uses a bidirectional approach to understand the full context of words in a sentence
- Bidirectional Learning: Unlike traditional models that process text left-to-right (like RNNs) or right-to-left, BERT learns from both directions simultaneously to capture deeper meaning.
- Pre-training & Fine-tuning:
  - Pre-trained on large datasets (e.g., Wikipedia, BooksCorpus).
  - Fine-tuned for specific NLP tasks (e.g., sentiment analysis, question answering).
- Masked Language Modelling (MLM):
  - BERT randomly masks some words in a sentence and trains the model to predict them, improving contextual understanding.
- Next Sentence Prediction (NSP):
  - Trains the model to predict whether two sentences logically follow each other, improving coherence in tasks like summarisation and dialogue generation.

Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2019, June). Bert: Pre-training of deep bidirectional transformers for language understanding. In Proceedings of the 2019 conference of the North American chapter of the association for computational linguistics: human language technologies, volume 1 (long and short papers) (pp. 4171-4186).

## Language models

## Deploying NLP

### Performance Metrics in NLP

| Metric | Definition | Interpretation |
| --- | --- | --- |
| Perplexity | Measures how well a probabilistic language model predicts a sequence of words. | Lower values indicate the model assigns higher probabilities to correct sequences, meaning better performance. |
| BLEU (Bilingual Evaluation Understudy) | Evaluates machine translation quality by measuring n-gram overlap between generated and reference translations. | Higher scores indicate better translations, but BLEU does not consider fluency or semantic correctness. |
| ROUGE (Recall-Oriented Understudy for Gisting Evaluation) | Measures word overlap, n-gram overlap, and longest common subsequences between generated and reference texts. | Higher scores indicate better coverage of reference content. |
| F1-Score | Assesses the balance between precision (correct positive predictions) and recall (capturing all actual positives). | A high F1-score indicates a good balance between precision and recall. |

### Cosine similarity

- Cosine similarity measures the similarity between two vectors by calculating the cosine of the angle between them.
- It is commonly used in NLP to compare word, sentence, or document embeddings.

Applications:
- Finding similar words/documents (e.g., search engines, recommendation systems).
- Measuring semantic similarity in NLP tasks (e.g., sentence similarity, text clustering).
- Used with word embeddings (e.g., Word2Vec, GloVe, BERT) for efficient text comparison.

## Ethical Considerations

| Ethical Concern | Description | Challenges | Possible Solutions |
| --- | --- | --- | --- |
| Bias in NLP Models | Models learn and reinforce societal biases. | Gender, racial, and cultural biases in word embeddings and decision-making. | Curate diverse datasets, apply fairness-aware training, and use bias detection tools. |
| Explainability & Transparency | Many NLP models act as "black boxes," making decisions hard to interpret. | Reduced trust in AI, especially in sensitive fields like healthcare or law. | Use explainable AI (XAI) techniques like attention visualisation and SHAP values. |
| Privacy & Data Security | NLP systems process sensitive personal data. | Risk of data leaks, unintended memorisation, and surveillance concerns. | Apply anonymisation, differential privacy, and secure data storage. |
| Misuse of NLP Technologies | AI can be exploited for harmful purposes. | Fake news, automated harassment, deepfake text, and plagiarism. | Develop content moderation tools and ethical AI usage policies. |
| Access & Fairness | NLP models require high computational power, leading to accessibility gaps. | Exclusion of low-resource languages and underrepresented communities. | Encourage open-source research and promote multilingual NLP initiatives. |