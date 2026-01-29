---
title: "2 Numeros Aleatorios Y Pseudo Aleatorios"
date: 2026-01-26
tags:
  - ciberseguridad
  - criptografia
---
### **Sucesiones Aleatorias y Pseudo-Aleatorias**


> **Relacionado**: [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]].

En criptografía, la generación de números aleatorios es crucial para la seguridad de los sistemas. Sin embargo, no todos los generadores de números aleatorios son iguales. Se pueden clasificar en:

1. **Generadores Verdaderamente Aleatorios (TRNG, True Random Number Generators)**
2. **Generadores Pseudo-Aleatorios (PRNG, Pseudo-Random Number Generators)**
3. **Generadores Pseudo-Aleatorios Criptográficamente Seguros (CSPRNG, Cryptographically Secure PRNG)**

---

### **Generadores Verdaderamente Aleatorios (TRNG)**

Un **TRNG** produce números que **no pueden ser reproducidos**, ya que provienen de fenómenos físicos impredecibles, como:

- Ruido térmico en circuitos electrónicos.
- Tiempo entre pulsaciones del teclado o movimientos del ratón.
- Variaciones en la frecuencia de la CPU.
- Fenómenos cuánticos en dispositivos especializados.

> **Ejemplo:** El sistema de lotería con bombos y bolas genera números verdaderamente aleatorios.

En sistemas Linux/Unix, se pueden obtener números verdaderamente aleatorios leyendo de `/dev/random`, aunque con una velocidad limitada.

### **Generadores Pseudo-Aleatorios (PRNG)**

Un **PRNG** genera una sucesión de números a partir de una semilla inicial y sigue un algoritmo determinista. Aunque los valores generados **parecen aleatorios**, en realidad **son completamente reproducibles** si se conoce la semilla.

> **Ejemplo:** La función `rand()` en muchos lenguajes de programación usa PRNG.

Los PRNG son útiles cuando la reproducibilidad es deseada (por ejemplo, en simulaciones), pero **no son seguros en criptografía**.

---

### **Características de una Sucesión Pseudo-Aleatoria**

Para que una sucesión sea aceptada como pseudo-aleatoria en criptografía, debe cumplir ciertas propiedades:

1. **Periodo Largo**: La secuencia no debe repetirse en un rango corto de valores. Idealmente, un PRNG criptográfico debe tener un periodo **≥2128\geq 2^{128}**.
2. **Distribución Equilibrada de Bits**: Los ceros y unos deben aparecer con la misma frecuencia (postulados de Golomb).
3. **Autocorrelación Baja**: No debe haber patrones evidentes en la secuencia.
4. **Imprevisibilidad**: No debe ser posible predecir el siguiente número de la secuencia con probabilidad mayor a 1/21/2.

---

### **Imprevisibilidad en Sucesiones Pseudo-Aleatorias**

Se distinguen tres tipos de imprevisibilidad:

1. **Imprevisibilidad de la clave**: Un atacante no debe ser capaz de recuperar la semilla a partir de la secuencia generada.
2. **Imprevisibilidad hacia adelante**: Conociendo una parte de la secuencia, no se debe poder predecir el siguiente número.
3. **Imprevisibilidad hacia atrás**: Conociendo una parte de la secuencia, no se debe poder deducir números anteriores.

---

### **Formalización Matemática**

En términos formales, una sucesión pseudo-aleatoria es aquella cuya distribución **no puede distinguirse** de una distribución aleatoria real mediante un algoritmo eficiente.

#### **Definición de Generador Pseudo-Aleatorio (PRNG)**

Un PRNG es una función GG que toma una semilla ss de nn bits y genera una secuencia de l(n)l(n) bits, con l(n)>nl(n) > n:

G:{0,1}n→{0,1}l(n)G: \{0,1\}^n \to \{0,1\}^{l(n)}

Un PRNG es **bueno** si **ningún algoritmo eficiente** puede distinguir su salida de una secuencia verdaderamente aleatoria con una probabilidad significativamente mayor que 1/21/2.

> **Ejemplo de PRNG:**  
> Un generador congruencial lineal:
> 
> Xn+1=(aXn+c)mod  mX_{n+1} = (a X_n + c) \mod m
> 
> Donde a,c,ma, c, m son constantes adecuadas.

---

### **Generadores Pseudo-Aleatorios Criptográficamente Seguros (CSPRNG)**

Un **CSPRNG** es un PRNG que no solo pasa las pruebas estadísticas básicas, sino que también es **impredecible para un atacante** con recursos computacionales realistas.

#### **Propiedades de un CSPRNG**

- **Resiste ataques de predicción**: Un atacante no puede predecir el siguiente bit de la secuencia aunque conozca muchos bits anteriores.
- **Resiste ataques inversos**: No permite reconstruir la semilla a partir de su salida.
- **Basado en problemas difíciles**: Su seguridad se basa en problemas matemáticos difíciles de resolver.

> **Ejemplo de CSPRNGs en uso:**
> 
> - **AES en modo CTR o OFB** (utilizando el cifrado AES para generar números aleatorios).
> - **ChaCha20** (Google lo usa en Android y TLS).
> - **/dev/urandom** en Linux, basado en SHA-1.

---

### **Diferencia entre PRNG y CSPRNG**

|**Característica**|**PRNG**|**CSPRNG**|
|---|---|---|
|Determinista|Sí|Sí|
|Puede ser reproducido|Sí|No (seguro ante ataques)|
|Seguridad criptográfica|No|Sí|
|Uso en simulaciones y videojuegos|Sí|No|
|Uso en criptografía (claves, IVs, firmas)|No|Sí|

---

### **¿Existen PRNGs Perfectamente Seguros?**

No hay **pruebas matemáticas absolutas** de que un PRNG sea **indistinguible de una sucesión aleatoria**, pero sí hay **indicadores** de seguridad si asumimos la existencia de funciones unidireccionales.

Por ejemplo:

- La **generación de claves en Diffie-Hellman** depende de PRNGs de alta calidad.
- La **firma digital RSA** necesita números pseudo-aleatorios de alta entropía.

---

### **Conclusión**

- **Los TRNG son ideales**, pero lentos y difíciles de usar a gran escala.
- **Los PRNG son rápidos, pero no son seguros para criptografía.**
- **Los CSPRNG son la mejor opción** para aplicaciones de seguridad, ya que combinan rapidez y resistencia a ataques.

### **Generadores Orientados a Hardware**

Los **generadores de números aleatorios por hardware** (HRNG o TRNG, _True Random Number Generators_) generan secuencias de bits a partir de fenómenos físicos impredecibles. Estos generadores se utilizan en criptografía cuando es necesario garantizar una alta calidad de aleatoriedad.

#### **Fuentes de entropía en hardware**

Los HRNG/TRNG se basan en mediciones de fenómenos físicos que son inherentemente caóticos, como:

- **Ruido térmico en circuitos electrónicos**: Variaciones en la corriente de un resistor o diodo.
- **Jitter en osciladores de reloj**: Pequeñas variaciones en la frecuencia de una señal de reloj digital.
- **Tiempo entre eventos en sistemas informáticos**: Intervalos entre pulsaciones de teclado, movimientos del ratón o tiempos de acceso al disco duro.
- **Ruido cuántico**: Fluctuaciones de partículas a nivel cuántico, utilizadas en dispositivos avanzados.

> **Ejemplo en sistemas Linux/Unix**  
> En sistemas operativos basados en Unix, se pueden obtener números verdaderamente aleatorios leyendo del dispositivo `/dev/random`. Este recolecta entropía del sistema, pero su velocidad es limitada.

---

### **Registro de desplazamiento de retroalimentación lineal (LFSR)**

Uno de los generadores más utilizados en hardware es el **LFSR (Linear Feedback Shift Register)**, que consiste en una cadena de registros de desplazamiento interconectados.

#### **Funcionamiento del LFSR**

Cada bit nuevo se obtiene como una combinación lineal (XOR) de bits anteriores, siguiendo una ecuación de la forma:

st+1=pn−1st+pn−2st−1+⋯+p0st−nmod  2s_{t+1} = p_{n-1} s_t + p_{n-2} s_{t-1} + \dots + p_0 s_{t-n} \mod 2

Donde:

- sts_t es el bit en el tiempo tt.
- pip_i son coeficientes de realimentación.
- Se usa XOR como operación de combinación.

> **Ejemplo**:  
> Un LFSR de 4 bits con realimentación dada por el polinomio x4+x+1x^4 + x + 1 genera una secuencia de longitud 15 antes de repetirse.

#### **Desventaja del LFSR**

Si un atacante conoce suficientes bits de la secuencia generada, puede resolver un sistema de ecuaciones y determinar el estado interno del generador, haciéndolo predecible.

#### **Solución: LFSR con combinaciones no lineales**

Para aumentar la seguridad, se combinan varios LFSR usando funciones no lineales o métodos como:

- **Desplazamientos irregulares**: No siempre se desplaza un bit fijo en cada iteración.
- **Decimación de la secuencia**: Se eliminan ciertos bits de la secuencia para aumentar la entropía.

---

### **Generadores Orientados a Software**

Los **generadores de números pseudo-aleatorios por software** (PRNGs y CSPRNGs) utilizan algoritmos deterministas para generar secuencias de bits a partir de una semilla inicial.

#### **Tipos de generadores por software**

1. **PRNG (Pseudo-Random Number Generators)**
    - Generan secuencias que _parecen_ aleatorias pero son reproducibles si se conoce la semilla.
    - **Ejemplo:** Función `rand()` en C.
2. **CSPRNG (Cryptographically Secure PRNG)**
    - Diseñados para aplicaciones criptográficas, resistentes a ataques de predicción.
    - **Ejemplo:** Generador basado en AES en modo CTR.

---

### **Ejemplo de PRNGs en Software**

#### **Generador Congruencial Lineal (LCG)**

Uno de los PRNG más antiguos es el **generador congruencial lineal**, definido por:

Xn+1=(aXn+c)mod  mX_{n+1} = (a X_n + c) \mod m

Donde:

- XnX_n es el número generado en el paso nn.
- a,c,ma, c, m son constantes adecuadas.

> **Ejemplo en ANSI C**  
> Algunos compiladores de C usan un LCG con:
> 
> Xn+1=(1103515245Xn+12345)mod  231X_{n+1} = (1103515245 X_n + 12345) \mod 2^{31}

#### **Problema del LCG**

El generador congruencial lineal **no es seguro** para criptografía porque:

1. **Tiene un periodo corto** si mm no es suficientemente grande.
2. **Es predecible** si se conocen algunos valores de la secuencia.

---

### **Generadores Criptográficamente Seguros (CSPRNGs)**

Un **CSPRNG** es un PRNG que:

1. **Resiste ataques de predicción**.
2. **Genera números que parecen aleatorios a cualquier adversario eficiente**.
3. **Está basado en problemas matemáticos difíciles**.

#### **Ejemplo 1: Generador Blum-Blum-Shub (BBS)**

El generador **BBS** se basa en la dificultad de la **residualidad cuadrática**:

xn+1=xn2mod  nx_{n+1} = x_n^2 \mod n

Donde:

- n=p⋅qn = p \cdot q es el producto de dos primos grandes.
- El bit menos significativo de xnx_n se usa como bit aleatorio.

> **Seguridad**:
> 
> - Si se puede invertir xn2mod  nx_n^2 \mod n, se puede factorizar nn, lo cual es computacionalmente difícil.

#### **Ejemplo 2: Generador RSA**

Basado en la seguridad de la **factorización de enteros**:

xn+1=xnemod  nx_{n+1} = x_n^e \mod n

Donde:

- ee es un exponente público.
- n=p⋅qn = p \cdot q.

> **Ventaja**: Su seguridad depende de la dificultad de factorizar nn.

---

### **Comparación entre Generadores de Hardware y Software**

|Característica|Generadores de Hardware (TRNG)|Generadores de Software (CSPRNG)|
|---|---|---|
|**Aleatoriedad verdadera**|Sí|No|
|**Basado en fenómenos físicos**|Sí|No|
|**Reproducible**|No|Sí|
|**Velocidad**|Puede ser lento|Rápido|
|**Resistencia a predicción**|Alta|Depende del algoritmo|

---

### **Conclusión**

- **Los generadores de hardware (TRNGs) son los más seguros**, pero su uso es limitado por su velocidad y disponibilidad.
- **Los PRNGs son rápidos pero predecibles**, por lo que **no deben usarse en criptografía**.
- **Los CSPRNGs combinan seguridad y rapidez**, y son la mejor opción para la mayoría de las aplicaciones criptográficas.

Si quieres más detalles sobre un generador específico o su implementación, dime.