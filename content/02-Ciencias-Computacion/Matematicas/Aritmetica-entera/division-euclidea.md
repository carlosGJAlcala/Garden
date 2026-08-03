---
title: "Verificación: 23 = 5 * 4 + 3"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-entera
---
### División euclídea – Relación entre matemáticas y programación


> **Relacionado**: [[08-Personal/Rutinas/Horario|Horario]]. [[02-Ciencias-Computacion/Matematicas/Aritmetica-entera/Aritmetica-entera|Aritmetica entera]].

La **división euclídea** es un concepto fundamental en aritmética entera, y **tiene aplicaciones directas y constantes en programación**, especialmente en algoritmos, criptografía, optimización, compresión y estructuras de datos.

---

##  ¿Qué es la división euclídea?

Dados dos enteros `a` (dividendo) y `b` (divisor, distinto de 0), **la división euclídea** garantiza la existencia de dos enteros:

q=cociente,r=restoq = \text{cociente}, \quad r = \text{resto}

Tales que:

a=bq+r,con 0≤r<∣b∣a = bq + r, \quad \text{con } 0 \le r < |b|

---

##  En programación

En lenguajes como Python, C, Java:

```python
q = a // b  # División entera (cociente)
r = a % b   # Resto (módulo)
```

 Esto implementa directamente la división euclídea.

Ejemplo:

```python
a = 23
b = 5
q = 23 // 5  # 4
r = 23 % 5   # 3
# Verificación: 23 = 5 * 4 + 3
```

---

## ️ Aplicaciones en programación

### 1. **Cálculo del MCD con el algoritmo de Euclides**

El algoritmo de Euclides usa división euclídea repetidamente:

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

️ Este algoritmo es la base para:

- Reducir fracciones.
    
- Comprobar co-primalidad.
    
- Calcular **inversos modulares** (RSA, criptografía).
    

---

### 2. **Aritmética modular**

El resto de la división (`a % b`) permite trabajar en un **conjunto finito de residuos**:

Zn={0,1,...,n−1}\mathbb{Z}_n = \{0, 1, ..., n-1\}

️ Usado en:

- Tablas hash.
    
- Generación pseudoaleatoria.
    
- Cifrado de clave pública y privada.
    
- Relojes (hora % 12, % 24).
    

---

### 3. **Conversión de base (base-N)**

La división euclídea permite convertir un número decimal a cualquier otra base:

```python
n = 25
base = 2
digits = []
while n > 0:
    digits.append(n % base)
    n = n // base
# Resultado: 11001 (binario de 25)
```

---

### 4. **Distribución cíclica y estructuras circulares**

Cuando necesitas operar en estructuras **circulares**, como:

- **Arrays circulares**
    
- **Buffers de cola (circular buffer)**
    
- **Horarios (turnos rotativos, relojes)**
    

Usas:

```python
i = (i + 1) % N  # pasar al siguiente índice circularmente
```

---

### 5. **Compresión y algoritmos de codificación**

Muchas transformaciones (como en **códigos cíclicos**) dependen del uso de residuos para manipular posiciones en secuencias, y aplican división euclídea para **alinear y dividir bloques**.

---

##  En seguridad (criptografía)

- **RSA, Diffie-Hellman, curvas elípticas**: se basan en operaciones sobre `ℤ_n`, es decir, números enteros módulo `n`.
    
- El inverso modular `a⁻¹ mod n` se calcula **usando la división euclídea extendida**.
    

---

##  Conclusión

La división euclídea no es solo una operación matemática elemental, sino una **herramienta clave en la programación**, usada para:

- control de bucles
    
- gestión de índices
    
- cifrado
    
- algoritmos fundamentales
    
- estructuras de datos circulares
    
- eficiencia algorítmica
    

Es uno de esos conceptos matemáticos **con impacto inmediato en el código**, en todos los niveles.

---