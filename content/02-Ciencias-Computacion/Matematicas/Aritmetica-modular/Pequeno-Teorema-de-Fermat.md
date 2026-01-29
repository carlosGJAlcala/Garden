---
title: "Pequeño Teorema de Fermat – Explicación y aplicación en programación"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-modular
---
# Pequeño Teorema de Fermat – Explicación y aplicación en programación

El **Pequeño Teorema de Fermat** es un resultado fundamental de la teoría de números que tiene aplicaciones directas en **[[01-Ciberseguridad/Criptografia/Repaso-de-Matematicas|criptografía]]**, optimización de algoritmos, pruebas de primalidad y cálculo modular eficiente.

> **Relacionado**: [[Teorema-Chino-de-los-Restos-CRT]], [[Congruencias]], [[01-Ciberseguridad/Criptografia/AES256|Criptografía AES]].

---

##  Enunciado

Sea $p$ un número primo, y $a$ un entero tal que $$a \not\equiv 0 \mod p$$. Entonces:

$$
a^{p-1} \equiv 1 \mod p
$$

Una forma equivalente, válida para **todo** $$a \in \mathbb{Z}$$, es:

$$
a^p \equiv a \mod p
$$

---

##  Interpretación

Este teorema establece que si elevas un número no divisible por un primo $$p$$ a la potencia $$p-1$$, el resultado es congruente con 1 módulo $$p$$.

Sirve para **reducir exponentes** en cálculos modulares y como base para diversas construcciones criptográficas.

---

## ️ Aplicaciones en programación

### 1. Cálculo de potencias modulares optimizadas

El teorema permite reducir exponentes grandes:

$$
a^b \mod p \equiv a^{b \mod (p-1)} \mod p \quad \text{(si } a \not\equiv 0 \mod p)
$$

Esto se usa en:

- Firmas digitales (RSA, DSA)
- Claves públicas (Diffie-Hellman, ElGamal)
- Generadores pseudoaleatorios

---

### 2. Pruebas de primalidad (Fermat Primality Test)

Si $$n$$ es primo, entonces para cualquier $$a < n$$:

$$
a^{n-1} \equiv 1 \mod n
$$

Si esto **no se cumple**, entonces $$n$$ **no es primo**.

Aunque hay falsos positivos (números de Carmichael), el test de Fermat es una base para algoritmos más complejos como **Miller-Rabin**.

---

### 3. Cálculo de inversos modulares

Cuando $$p$$ es primo, el inverso modular de $$a$$ se puede calcular como:

$$
a^{-1} \equiv a^{p - 2} \mod p
$$

**Código en Python:**

```python
def inverse_mod(a, p):
    return pow(a, p - 2, p)  # Solo si p es primo
