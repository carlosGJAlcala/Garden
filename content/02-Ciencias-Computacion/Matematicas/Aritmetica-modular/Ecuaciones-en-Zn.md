---
title: "Ecuaciones en Zn - Aritmetica modular y resolucion"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-modular
---
# Ecuaciones en $\mathbb{Z}_n$ – Aritmética modular y resolución


> **Relacionado**: [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/Instalacion-y-Configuracion-de-Splunk-Universal-Forwarder-con-Snort-en-Windows-y-Ubuntu|Instalacion y Configuracion de Splunk Universal Forwarder con Snort en Windows y Ubuntu]]. [[01-Ciberseguridad/Ingenieria-Inversa/2025-01-21-INGENIERIA-INVERSA|2025 01 21 INGENIERIA INVERSA]]. [[01-Ciberseguridad/Ingenieria-Inversa/2025-01-28-Ingenieria-Inversa|2025 01 28 Ingenieria Inversa]].

Resolver ecuaciones en $\mathbb{Z}_n$ significa trabajar con enteros **módulo $n$**, donde dos números son equivalentes si su diferencia es divisible por $n$.

Este tipo de ecuaciones es clave en **criptografía, teoría de números, hashing, algoritmos de seguridad y sistemas distribuidos**.

---

##  ¿Qué es $\mathbb{Z}_n$?

Es el conjunto de **clases de equivalencia módulo $n$**:

$\mathbb{Z}_n = \{0, 1, 2, ..., n-1\}$

Dos números $a$ y $b$ son equivalentes módulo $n$ si:

$a \equiv b \mod n \quad \Longleftrightarrow \quad n \mid (a - b)$

---

##  Tipos comunes de ecuaciones

### 1. Ecuaciones lineales:

$ax \equiv b \mod n$

### 2. Ecuaciones cuadráticas:

$x^2 \equiv a \mod n$

---

##  Ecuación lineal: $ax \equiv b \mod n$

### ¿Cuándo tiene solución?

Tiene solución si y solo si:

$\gcd(a, n) \mid b$

Si $d = \gcd(a, n)$ divide a $b$, existen exactamente $d$ soluciones distintas módulo $n$.

---

## ️ Método de resolución

1. Calcular $d = \gcd(a, n)$  
2. Si $d \nmid b$ → no hay solución  
3. Si $d \mid b$:
   - Dividir la ecuación entre $d$:

     $(a/d)x \equiv b/d \mod (n/d)$

   - Calcular el **inverso modular** de $a/d$ módulo $n/d$
   - Multiplicar ambos lados por el inverso
   - Solución particular $x_0$
   - Todas las soluciones:

     $x \equiv x_0 + k(n/d) \mod n$, para $k = 0, 1, ..., d-1$

---

##  Ejemplo

Resolver $6x \equiv 8 \mod 14$

1. $\gcd(6, 14) = 2$ y $2 \mid 8$ → hay solución  
2. Dividir entre 2:

   $3x \equiv 4 \mod 7$

3. Inverso de 3 módulo 7:

   $3^{-1} \equiv 5 \mod 7$, porque $3 \cdot 5 = 15 \equiv 1 \mod 7$

4. Multiplicamos:

   $x \equiv 5 \cdot 4 = 20 \equiv 6 \mod 7$

5. Como hay 2 soluciones:

   $x \equiv 6, 13 \mod 14$

---

##  Aplicaciones prácticas

- Criptografía (RSA, ElGamal, ECC)
- Teorema chino del resto
- Hashing circular y estructuras cíclicas
- Algoritmos numéricos en seguridad y codificación

---

##  Código Python para resolver $ax \equiv b \mod n$

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    d, x1, y1 = extended_gcd(b, a % b)
    return d, y1, x1 - (a // b) * y1

def resolver_congruencia(a, b, n):
    d, x, _ = extended_gcd(a, n)
    if b % d != 0:
        return None  # No hay solución
    a_, b_, n_ = a // d, b // d, n // d
    _, inv, _ = extended_gcd(a_, n_)
    x0 = (inv * b_) % n
    return [(x0 + k * n_) % n for k in range(d)]
