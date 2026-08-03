---
title: "12 Introduccion A La Criptografiaseguridad"
date: 2025-01-01
tags:
  - ciberseguridad
---
### **Modelos de ataques y objetivos de seguridad**


> **Relacionado**: [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]].

Los ataques en criptografía se modelan según lo que el atacante puede observar y cómo puede interactuar con el sistema. Para ello, el sistema se considera un "oráculo" que procesa entradas y devuelve respuestas sin revelar su funcionamiento interno.

#### **Modelos de ataques**

Se dividen en dos grandes categorías:

1. **Modelos de caja negra:**
    
    - **COA (Ciphertext-Only Attack)**: El atacante solo tiene acceso a criptogramas.
    - **KPA (Known-Plaintext Attack)**: El atacante conoce pares de textos claros y sus criptogramas.
    - **CPA (Chosen-Plaintext Attack)**: El atacante puede elegir textos claros y obtener sus criptogramas.
    - **CCA (Chosen-Ciphertext Attack)**: El atacante elige criptogramas y recibe los textos claros descifrados.
2. **Modelos de caja gris:**
    
    - Ataques no invasivos: Basados en observación de tiempos de ejecución, mensajes de error, trazas de caché.
    - Ataques invasivos: Incluyen manipulación física del hardware, emisiones electromagnéticas, inyección de fallos con láser.

#### **Objetivos de seguridad**

Un sistema es seguro si, dado un criptograma, el atacante no obtiene información útil sobre el mensaje original.

1. **Indistinguibilidad**: Un criptograma debe ser indistinguible de una secuencia aleatoria.
2. **No maleabilidad**: El atacante no debe poder manipular criptogramas de forma predecible.

---

### **Tipos de seguridad**

1. **Seguridad incondicional**: El sistema es seguro incluso ante un adversario con recursos ilimitados. Se basa en principios de la **teoría de la información**, como en la **libreta de un solo uso (OTP)**.
2. **Seguridad computacional**: La seguridad depende de la capacidad computacional del atacante. Es el enfoque estándar en criptografía moderna.
3. **Seguridad heurística**: No se ha demostrado segura formalmente, pero no se conocen ataques efectivos.
4. **Seguridad condicional**: La seguridad se basa en hipótesis aún no demostradas, como la dificultad de ciertos problemas matemáticos.

---

### **Seguridad incondicional o secreto perfecto: la «libreta de usar y tirar»**

El concepto de **secreto perfecto** significa que un atacante que observe un criptograma no obtiene información adicional sobre el mensaje original.

#### **Definición formal del secreto perfecto**

Un esquema de cifrado es **perfectamente seguro** si para cualquier mensaje mm y criptograma cc, se cumple:

P(M=m∣C=c)=P(M=m)P(M = m \mid C = c) = P(M = m)

Esto significa que conocer cc no cambia la probabilidad de mm, lo que implica que el mensaje es completamente oculto al atacante.

#### **La Libreta de Un Solo Uso (One-Time Pad, OTP)**

Este es el único esquema de cifrado que ofrece secreto perfecto. Su funcionamiento es simple:

1. Se genera una clave aleatoria kk de la misma longitud que el mensaje mm.
2. Se cifra mediante XOR bit a bit: c=m⊕kc = m \oplus k
3. Se descifra aplicando XOR nuevamente: m=c⊕km = c \oplus k

#### **Demostración del secreto perfecto del OTP**

Dado que la clave es aleatoria y uniforme, cualquier mensaje puede ser transformado en cualquier criptograma con la misma probabilidad. Es decir, la distribución de los criptogramas es independiente del mensaje original.

P(C=c∣M=m)=P(C=c)P(C = c \mid M = m) = P(C = c)

Por lo tanto, el atacante no puede obtener ninguna información útil.

#### **Limitaciones del OTP**

1. **La clave debe ser tan larga como el mensaje**, lo que lo hace poco práctico para la mayoría de los casos.
2. **La clave debe ser aleatoria y usada solo una vez**. Si se reutiliza, se filtra información al realizar XOR entre dos criptogramas.
3. **Requiere un canal seguro para compartir claves**, lo que contradice la necesidad de un sistema de cifrado en primer lugar.

---

### **Expansión y aplicaciones prácticas**

- Aunque el **OTP** no es práctico en la mayoría de los escenarios, se usa en **sistemas de alta seguridad**, como en comunicaciones gubernamentales o militares.
- Un sistema derivado del OTP es **el cifrado de flujo**, que utiliza generadores de claves pseudoaleatorias en lugar de claves realmente aleatorias.
- En la criptografía cuántica, la distribución cuántica de claves (QKD) permite implementar un sistema similar al OTP con claves verdaderamente aleatorias.

### **Seguridad Computacional**

Dado que la **seguridad incondicional** (como en el **One-Time Pad**) es poco práctica, en la mayoría de los casos se recurre a la **seguridad computacional**, donde la seguridad de un criptosistema se basa en la **dificultad computacional** de ciertos problemas matemáticos.

---

### **¿Qué significa seguridad computacional?**

La seguridad computacional **no garantiza** que un sistema sea invulnerable, sino que su ataque **requeriría demasiado tiempo o recursos computacionales** para ser factible en la práctica.

#### **Conceptos clave:**

1. **Un sistema criptográfico es computacionalmente seguro si cualquier ataque requiere un tiempo de ejecución prohibitivo.**
2. **Se admite una pequeña probabilidad de éxito para un atacante, pero esta probabilidad es despreciable en términos prácticos.**
3. **Se basa en la teoría de la complejidad computacional**, es decir, en la dificultad de resolver ciertos problemas en un tiempo razonable.

#### **Ejemplo de cuantificación de la seguridad computacional:**

Si un ataque por **fuerza bruta** requiere probar todas las posibles claves de un cifrado con espacio de claves de 21282^{128}, se dice que el sistema tiene **128 bits de seguridad**.

- Un atacante necesitaría **21282^{128} operaciones** para romperlo, lo cual es **inviable incluso con los supercomputadores actuales**.

---

### **Definición Formal de Seguridad Computacional**

Un sistema criptográfico es **(t, ε)-seguro** si:

- Cualquier atacante eficiente con **un tiempo máximo tt** de cómputo tiene una probabilidad de éxito **menor que ε\varepsilon**.

Ejemplo:  
Un cifrado con seguridad de **(280,2−60)(2^{80}, 2^{-60})** significa que:

- Un atacante necesitaría **2802^{80}** ciclos de CPU para romperlo.
- La probabilidad de éxito del ataque es como máximo **2−602^{-60}**.

---

### **Relación con problemas matemáticos difíciles**

La seguridad computacional suele basarse en la suposición de que ciertos **problemas matemáticos son difíciles de resolver**. Algunos ejemplos clave:

1. **Factorización de enteros grandes** → Base de RSA
    
    - Es difícil encontrar los factores primos de un número grande N=p×qN = p \times q.
2. **Logaritmo discreto** → Base de Diffie-Hellman y DSA
    
    - Dado gxmod  pg^x \mod p, encontrar xx es computacionalmente costoso.
3. **Problema del logaritmo discreto en curvas elípticas** → Base de ECDSA
    
    - Similar al logaritmo discreto, pero en el contexto de curvas elípticas.
4. **Problemas de retículos** → Base de criptografía poscuántica
    
    - Se usan en esquemas resistentes a ataques de computadoras cuánticas.

---

### **Punto de vista asintótico**

Para evaluar la seguridad de un sistema en términos más generales, usamos la notación de **complejidad asintótica**:

- **Tiempo polinómico**: Si un algoritmo resuelve un problema en tiempo O(nc)O(n^c) (con cc constante), se considera **fácil**.
- **Tiempo exponencial**: Si requiere O(2n)O(2^n) pasos, se considera **difícil**.

Ejemplo:

- La **factorización de enteros** parece requerir tiempo **subexponencial**, lo que la hace un problema difícil en la práctica.

---

### **Definición de adversario eficiente**

Un **adversario eficiente** es aquel que puede ejecutar **algoritmos de tiempo polinómico** para intentar romper un sistema criptográfico.

Si la probabilidad de éxito de un adversario eficiente es **insignificante** (2−n2^{-n} con nn grande), el sistema es considerado **seguro en términos computacionales**.

---

### **Diferencia entre seguridad computacional y secreto perfecto**

|**Concepto**|**Secreto Perfecto (One-Time Pad)**|**Seguridad Computacional**|
|---|---|---|
|**Seguridad garantizada**|Sí (imposible de romper)|No (pero el ataque es inviable en la práctica)|
|**Dependencia de la clave**|La clave debe ser tan larga como el mensaje|Claves más cortas, pero basadas en problemas difíciles|
|**Reutilización de clave**|No (cada clave se usa solo una vez)|Sí (puede reutilizarse en múltiples sesiones)|
|**Ejemplo**|One-Time Pad|AES, RSA, ECDSA|

---

### **Conclusión**

- **La seguridad computacional es la base de la criptografía moderna**, ya que permite usar claves más cortas y evitar los problemas del One-Time Pad.
- **Se fundamenta en problemas matemáticos difíciles**, como la factorización de números grandes o el logaritmo discreto.
- **Admite una pequeña probabilidad de éxito del atacante**, pero esta es despreciable en términos prácticos.

