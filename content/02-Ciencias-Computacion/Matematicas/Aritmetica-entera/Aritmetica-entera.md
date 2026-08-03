---
title: "Aritmetica Entera"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-entera
---

# Aritmética Entera y Programación

Relación del tema de **Aritmética entera** con la **programación**, con aplicaciones reales en desarrollo de software y algoritmos.

---

## 1. Números enteros en programación


> **Relacionado**: [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Integer-overflow|Integer overflow]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

En matemáticas, los números enteros son el conjunto **ℤ = {..., -2, -1, 0, 1, 2, ...}**. En programación, los **tipos de datos enteros (`int`)** son su equivalente, aunque con **límites de tamaño** según el lenguaje y arquitectura (por ejemplo, `int32`, `int64`, etc.).

#### Aplicaciones en programación:

- Representación de **contadores, índices, identificadores**, etc.
    
- Uso en **algoritmos de búsqueda, ordenación, estructuras de datos**.
    
- Control de **desbordamientos**: el _integer overflow_ puede ser una vulnerabilidad si no se gestiona.
    

---

###  2. División euclídea

La **división euclídea** de un entero `a` entre `b` (con `b ≠ 0`) da un **cociente `q`** y un **resto `r`** tales que:

a=bq+r,0≤r<∣b∣a = bq + r, \quad 0 \leq r < |b|

#### En programación:

```python
q = a // b  # cociente
r = a % b   # resto
```

#### Usos comunes:

- Algoritmos de **división segura**.
    
- Implementación de **módulos aritméticos**.
    
- En **criptografía** y algoritmos como RSA (para trabajar con restos).
    

---

###  3. Máximo común divisor (MCD) y mínimo común múltiplo (mcm)

#### MCD (`gcd(a, b)`): el mayor número que divide a ambos.

#### mcm(a, b) = (a * b) / gcd(a, b)

#### Algoritmo de Euclides (eficiente, usado en todos los lenguajes):

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

#### Aplicaciones:

- **Reducción de fracciones**.
    
- **Criptografía**: RSA, teoría de números.
    
- Determinar **co-primalidad** (si `gcd(a,b)=1`).
    
- **Cálculo de hash dispersos**, para evitar colisiones.
    

---

###  4. Teorema fundamental de la aritmética

Todo entero positivo mayor que 1 puede **descomponerse de forma única como producto de números primos**.

#### En programación:

- Pruebas de primalidad.
    
- **Factorización para seguridad** (ej: romper RSA requiere factorizar un número muy grande).
    
- Uso en **generadores de números pseudoaleatorios**.
    

---

###  5. Ecuaciones diofánticas lineales

Son ecuaciones del tipo:

ax+by=c,donde buscamos soluciones enteras x,yax + by = c, \quad \text{donde buscamos soluciones enteras } x, y

#### Programación:

- Resolver con **algoritmo extendido de Euclides**, útil para hallar **inversos modulares**.
    
- Muy usados en **criptografía, firmas digitales**, y sistemas como el RSA o el Teorema Chino de los Restos.
    

#### Ejemplo:

```python
def extended_gcd(a, b):
    if b == 0:
        return (a, 1, 0)
    else:
        d, x1, y1 = extended_gcd(b, a % b)
        return (d, y1, x1 - (a // b) * y1)
```

---

###  Conexión práctica: ¿para qué sirve todo esto en programación?

- En **sistemas de criptografía modernos** (RSA, Diffie-Hellman, ECC), se usa aritmética entera y modular constantemente.
    
- En **blockchains** y criptomonedas, las firmas, claves, hashes y contratos inteligentes operan sobre números enteros grandes, usando MCD, inversos modulares, factorizaciones...
    
- En algoritmos de **redes P2P, compresión, análisis de datos y teoría de grafos**, se usan propiedades aritméticas.
    
- Aritmética entera es **base de todo lenguaje de programación**, incluso en áreas como gráficos (pixelado), inteligencia artificial (parámetros discretos), y bases de datos (ID primos, clustering).
    

---