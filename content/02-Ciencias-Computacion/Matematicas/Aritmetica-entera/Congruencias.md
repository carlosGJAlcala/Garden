---
title: "¿Es par?"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-entera
---
### Congruencias – Nota expandida y aplicación en programación


> **Relacionado**: [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/Instalacion-y-Configuracion-de-Splunk-Universal-Forwarder-con-Snort-en-Windows-y-Ubuntu|Instalacion y Configuracion de Splunk Universal Forwarder con Snort en Windows y Ubuntu]]. [[01-Ciberseguridad/Ingenieria-Inversa/2025-01-21-INGENIERIA-INVERSA|2025 01 21 INGENIERIA INVERSA]]. [[01-Ciberseguridad/Ingenieria-Inversa/2025-01-28-Ingenieria-Inversa|2025 01 28 Ingenieria Inversa]].

Las **congruencias** son una herramienta fundamental de la aritmética modular y tienen aplicaciones directas en programación, **especialmente en criptografía, algoritmos, seguridad, hashing, estructuras de datos y sistemas distribuidos**.

---

##  Definición matemática

Dado un módulo n∈Z+n \in \mathbb{Z}^+, se dice que:

a≡b (mod n)a \equiv b \ (\text{mod } n)

si y solo si n∣(a−b)n \mid (a - b), es decir:

a y b tienen el mismo resto al dividir entre n.a \text{ y } b \text{ tienen el mismo resto al dividir entre } n.

Ejemplo:

17≡5mod  12(porque 17−5=12)17 \equiv 5 \mod 12 \quad \text{(porque } 17 - 5 = 12)

---

##  Interpretación en programación

En código, esto se expresa así:

```python
if a % n == b % n:
    print("a ≡ b mod n")
```

Ejemplo:

```python
17 % 12 == 5  →  True
```

---

##  Aplicaciones en programación

###  1. **Criptografía (RSA, ECC, Diffie-Hellman...)**

Toda la criptografía moderna se basa en **operaciones en Zn\mathbb{Z}_n**:

- Cálculo de potencias modulares:  
    c=memod  nc = m^e \mod n
    
- Inversos modulares:  
    Encontrar xx tal que ax≡1mod  nax \equiv 1 \mod n
    

---

### ️ 2. **Optimización de estructuras de datos (hashing)**

- Las funciones hash usan congruencias para mapear claves a índices:
    

```python
index = hash(key) % table_size
```

- También en algoritmos de dispersión, partición de datos, sharding...
    

---

###  3. **Sistemas cíclicos y programación de tiempo**

Cuando un evento ocurre en ciclos, se usa congruencia para determinar cuándo vuelve a repetirse una condición:

```python
if time % cycle == 0:
    activar_evento()
```

️ Aplicable a juegos, animaciones, cron jobs, alarmas...

---

###  4. **Teorema chino del resto (CRT)**

Resuelve sistemas de congruencias simultáneas:

x≡a1mod  n1x≡a2mod  n2x \equiv a_1 \mod n_1 \\ x \equiv a_2 \mod n_2

→ Si n1,n2n_1, n_2 son coprimos, hay **una solución única modulo n1⋅n2n_1 \cdot n_2**.

Muy usado en:

- Cálculo modular eficiente.
    
- Criptografía (optimización de RSA).
    
- Distribución paralela de datos.
    

---

###  5. **Comparaciones eficientes**

Algunos algoritmos evitan divisiones costosas comparando por módulo:

```python
# ¿Es par?
if n % 2 == 0:
    ...
```

O aplicando reglas congruentes:

- Si a≡bmod  na \equiv b \mod n, entonces:
    
    - a+c≡b+cmod  na + c \equiv b + c \mod n
        
    - a⋅c≡b⋅cmod  na \cdot c \equiv b \cdot c \mod n
        
    - ak≡bkmod  na^k \equiv b^k \mod n
        

️ Esto se usa para **simplificar cálculos grandes sin perder exactitud**.

---

##  Ejemplo práctico: potencia modular (exponenciación rápida)

Cálculo eficiente de abmod  na^b \mod n – fundamental en seguridad:

```python
def mod_pow(a, b, n):
    result = 1
    a = a % n
    while b > 0:
        if b % 2 == 1:
            result = (result * a) % n
        a = (a * a) % n
        b //= 2
    return result
```

️ Se usa en RSA, DH, blockchain...

---

##  Cuidado: divisiones en modular

No siempre puedes “dividir” directamente en módulo:

ab≢a⋅b−1mod  n(a menos que b tenga inverso)\frac{a}{b} \not\equiv a \cdot b^{-1} \mod n \quad \text{(a menos que \( b \) tenga inverso)}

Para dividir, necesitas calcular el **inverso modular de `b` módulo `n`**, lo que se hace con el **algoritmo extendido de Euclides**.

---

##  Conclusión

Las congruencias son **una forma de operar en espacios finitos**, donde solo nos interesa el residuo respecto a un número. En programación, **permiten trabajar con ciclos, optimizar cálculos, garantizar seguridad criptográfica, crear funciones hash robustas y más**.

---

¿Quieres que prepare una práctica con:

- sistema de congruencias con el Teorema Chino del Resto,
    
- potencia modular,
    
- y cálculo del inverso modular en Python?
    

Así verás cómo todo se conecta con criptografía y seguridad.