---
title: "Dos procesos con ciclos de 4s y 6s"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-entera
---
### MCM y MCD – Relación con la programación


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

Los conceptos matemáticos de **MCD (Máximo Común Divisor)** y **MCM (Mínimo Común Múltiplo)** son fundamentales no solo en aritmética, sino también en muchas áreas de la **programación**, especialmente en **algoritmos, criptografía, programación de sistemas, optimización y estructuras de datos**.

---

##  Definiciones matemáticas

###  MCD (Máximo Común Divisor)

Dado dos enteros `a` y `b`, el MCD es el mayor número que los divide a ambos:

MCD(a,b)=max⁡{d∈Z+ ∣ d∣a y d∣b}\text{MCD}(a, b) = \max\{d \in \mathbb{Z}^+ \ | \ d \mid a \ \text{y} \ d \mid b\}

---

###  MCM (Mínimo Común Múltiplo)

Es el menor número entero positivo que es múltiplo de `a` y `b`:

MCM(a,b)=min⁡{m∈Z+ ∣ a∣m y b∣m}\text{MCM}(a, b) = \min\{m \in \mathbb{Z}^+ \ | \ a \mid m \ \text{y} \ b \mid m\}

Y se relacionan así:

MCM(a,b)=a⋅bMCD(a,b)\text{MCM}(a, b) = \frac{a \cdot b}{\text{MCD}(a, b)}

---

## ️ En programación: implementación de MCD

El **algoritmo de Euclides** es la forma más eficiente de calcular el MCD:

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

Y con eso, el MCM:

```python
def lcm(a, b):
    return abs(a * b) // gcd(a, b)
```

---

##  Aplicaciones prácticas en programación

### 1. **Reducción de fracciones**

Cuando se trabaja con racionales:

```python
def reducir_fraccion(numerador, denominador):
    d = gcd(numerador, denominador)
    return numerador // d, denominador // d
```

️ Esto es útil en librerías de álgebra simbólica o motores matemáticos como **SymPy**, **Mathematica**, etc.

---

### 2. **Co-primalidad y seguridad**

Si `gcd(a, b) == 1`, los números son **coprimos**, lo cual es fundamental para:

- Generar **claves criptográficas** (RSA, Diffie-Hellman).
    
- Calcular **inversos modulares**.
    
- Construir **hashes robustos** y funciones de mezcla.
    

---

### 3. **Sistemas de tiempo y sincronización**

Cuando necesitas encontrar cuándo dos procesos **se alinean** de nuevo:

```python
# Dos procesos con ciclos de 4s y 6s
lcm(4, 6) = 12 → se sincronizan cada 12 segundos
```

Aplicable en:

- Sistemas embebidos
    
- Juegos (eventos repetitivos)
    
- Cron jobs
    

---

### 4. **Teorema chino del resto (CRT)**

Para combinar resultados modulares, necesitas módulos **coprimos**, es decir:

```python
gcd(n1, n2) == 1
```

️ Fundamental en **RSA**, en **criptografía homomórfica**, y en **almacenamiento distribuido**.

---

### 5. **Cálculo de periodos o ciclos**

En estructuras de tipo `array circular`, simulaciones, o redes:

```python
# Cuándo dos animaciones o tareas cíclicas vuelven a coincidir
periodo_total = lcm(periodo1, periodo2)
```

---

### 6. **Ajustes de tamaño o resolución**

Ejemplo:

- Ajustar dos pantallas con resoluciones distintas al mismo múltiplo común.
    
- Encontrar bloques de datos que encajen perfectamente.
    

---

##  Conclusión

Tanto el **MCD como el MCM tienen un valor fundamental en programación**, porque permiten:

- **Reducir, simplificar y optimizar procesos**.
    
- **Detectar relaciones numéricas profundas** entre estructuras de datos.
    
- **Construir algoritmos criptográficos seguros**.
    
- **Resolver problemas de sincronización, periodos y memoria compartida**.
    

Su uso va mucho más allá de la teoría de números: **aparecen en bases de datos, redes, multimedia, programación competitiva y criptografía moderna**.

---

¿Quieres que prepare ejemplos de uso real de MCD/MCM en criptografía con Python o un mini sistema de sincronización de eventos con ciclos múltiples?